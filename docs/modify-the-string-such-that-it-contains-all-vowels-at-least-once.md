# 修改字符串，使其至少包含一次所有元音

> 原文:[https://www . geesforgeks . org/modify-the-string-so-it-包含所有元音-至少一次/](https://www.geeksforgeeks.org/modify-the-string-such-that-it-contains-all-vowels-at-least-once/)

给定一个只包含大写字母的字符串，任务是找到获得一个包含所有元音的字符串所需的最少替换字符数，如果我们不能得到所需的字符串，则打印不可能。

**示例**:

```
Input: str = "ABCDEFGHI"
Output: AOUDEFGHI
There are already 3 Vowels present in the string 
A, E, I we just change B and C to O and U respectively.

Input: str = "ABC"
Output: IMPOSSIBLE
```

**做法:**由于只有 5 个元音 A、E、I、O、u 所以，如果字符串长度小于 5 总是不可能的。
对于长度大于等于 5 的字符串，总是有可能的。只需遍历每个字符，并用字符串中不存在的元音替换它。如果当前字符是一个元音，并且之前没有访问过，那么我们不会将该字符更改为元音。如果所有的元音从早期就已经存在，那么就不需要改变任何字符。

下面是上述方法的实现:

## C++14

```
// C++14 implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

void addAllVowel(string str)
{
    // All vowels
    char x[] = {'A', 'E', 'I', 'O', 'U'};

    // List to store distinct vowels
    vector<char> y;
    int length = str.length();

    // if length of string is less than 5
    // then always Impossible
    if (length < 5)
        cout << "Impossible" << endl;
    else
    {
        // Storing the distinct vowels in the string
        // by checking if it in the list of string and not
        // in the list of distinct vowels
        for (int i = 0; i < length; i++)
        {
            if (find(x, x + 5, str[i]) != x + 5 and
                find(y.begin(), y.end(), str[i]) == y.end())
                y.push_back(str[i]);
        }

        // Storing the vowels which are
        // not present in the string
        vector<char> z;
        for (int i = 0; i < 5; i++)
            if (find(y.begin(),
                     y.end(), x[i]) == y.end())
                z.push_back(x[i]);

        // No replacement needed condition
        if (z.empty())
            cout << str << endl;
        else
        {
            int cc = 0;
            vector<char> y;

            // Replacing the characters to get all Vowels
            for (int i = 0; i < length; i++)
            {
                if (find(x, x + 5, str[i]) != x + 5 and
                    find(y.begin(), y.end(),
                         str[i]) == y.end())
                    y.push_back(str[i]);
                else
                {
                    str[i] = z[cc];
                    cc++;
                }
                if (cc == z.size()) break;
            }
            cout << str << endl;
        }
    }
}

// Driver Code
int main(int argc, char const *argv[])
{
    string str = "ABCDEFGHI";
    addAllVowel(str);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

static boolean find(char x[], char c)
{
    for(int i = 0; i < x.length; i++)
    if(x[i] == c)
    return true;
    return false;
}

static boolean find(Vector<Character> v,char c)
{
    for(int i = 0; i < v.size(); i++)
    if(v.get(i) == c)
    return true;
    return false;
}

static void addAllVowel(String str)
{
    // All vowels
    char x[] = {'A', 'E', 'I', 'O', 'U'};

    // List to store distinct vowels
    Vector<Character> y = new Vector<>();
    int length = str.length();

    // if length of String is less than 5
    // then always Impossible
    if (length < 5)
        System.out.println("Impossible");
    else
    {
        // Storing the distinct vowels in the String
        // by checking if it in the list of String and not
        // in the list of distinct vowels
        for (int i = 0; i < length; i++)
        {
            if (find(x, str.charAt(i))&&
                !find(y, str.charAt(i)))
                y.add(str.charAt(i));
        }

        // Storing the vowels which are
        // not present in the String
        Vector<Character> z = new Vector<>();
        for (int i = 0; i < 5; i++)
            if (!find(y, x[i]) )
                z.add(x[i]);

        // No replacement needed condition
        if (z.size() == 0)
            System.out.println( str );
        else
        {
            int cc = 0;
            Vector<Character> y1 = new Vector<>();
            String ans = "";

            // Replacing the characters to get all Vowels
            for (int i = 0; i < length; i++)
            {
            if (find(x, str.charAt(i))&&
                !find(y1, str.charAt(i)))
                {
                    ans += str.charAt(i);
                    y1.add(str.charAt(i));
                }
                else
                {
                    ans += z.get(cc);
                    cc++;
                }
                if (cc == z.size())
                {
                    //copy th rest of the string
                    for(int j = i + 1; j < length; j++)
                    ans += str.charAt(j);
                    break;
                }
            }
            System.out.println(ans);
        }
    }
}

// Driver Code
public static void main(String args[])
{
    String str = "ABCDEFGHI";
    addAllVowel(str);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

s = "ABCDEFGHI"

# converting String to a list
S = list(s) 

 # All vowels
x = ["A", "E", "I", "O", "U"]

 # List to store distinct vowels
y = []
le = len(S)
if (le < 5):
    # if length of string is less than 5 then always
    # Impossible
    print("Impossible")
else:
    # Storing the distinct vowels in the string
    # by checking if it in the list of string and not
    # in the list of distinct vowels
    for i in range(le):
        if (S[i] in x and S[i] not in y):
            y.append(S[i])

    # Storing the vowels which are not present in the string
    z = []
    for i in range(5):
        if (x[i] not in y):
            z.append(x[i])
    if (len(z) == 0):
        # No replacement needed condition
        print(s)
    else:
        cc = 0
        y = []

        # Replacing the characters to get all Vowels
        for i in range(le):
            if (S[i] in x and S[i] not in y):
                y.append(S[i])
            else:
                S[i] = z[cc]
                cc += 1
            if (cc == len(z)):
                break
        print(*S, sep ="")
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG{

static bool find(char []x, char c)
{
    for(int i = 0; i < x.Length; i++)
        if  (x[i] == c)
            return true;

    return false;
}

static bool find(ArrayList v, char c)
{
    for(int i = 0; i < v.Count; i++)
        if ((char)v[i] == c)
            return true;

    return false;
}

static void addAllVowel(string str)
{

    // All vowels
    char []x = { 'A', 'E', 'I', 'O', 'U' };

    // List to store distinct vowels
    ArrayList y = new ArrayList();

    int length = str.Length;

    // If length of String is less than 5
    // then always Impossible
    if (length < 5)
        Console.Write("Impossible");
    else
    {

        // Storing the distinct vowels in
        // the String by checking if it in
        // the list of String and not
        // in the list of distinct vowels
        for(int i = 0; i < length; i++)
        {
            if (find(x, str[i]) &&
               !find(y, str[i]))
                y.Add(str[i]);
        }

        // Storing the vowels which are
        // not present in the String
        ArrayList z = new ArrayList();
        for(int i = 0; i < 5; i++)
            if (!find(y, x[i]) )
                z.Add(x[i]);

        // No replacement needed condition
        if (z.Count == 0)
            Console.Write(str);
        else
        {
            int cc = 0;
            ArrayList y1 = new ArrayList();
            string ans = "";

            // Replacing the characters to
            // get all Vowels
            for(int i = 0; i < length; i++)
            {
                if (find(x, str[i]) &&
                  !find(y1, str[i]))
                {
                    ans += str[i];
                    y1.Add(str[i]);
                }
                else
                {
                    ans += (char)z[cc];
                    cc++;
                }

                if (cc == z.Count)
                {

                    // Copy th rest of the string
                    for(int j = i + 1;
                            j < length; j++)
                        ans += str[j];
                        break;
                }
            }
            Console.Write(ans);
        }
    }
}

// Driver Code
public static void Main(string []args)
{
    string str = "ABCDEFGHI";

    addAllVowel(str);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

function find(x,c)
{
    for(let i = 0; i < x.length; i++)
        if(x[i] == c)
            return true;
    return false;
}

function addAllVowel(str)
{
    // All vowels
    let x = ['A', 'E', 'I', 'O', 'U'];

    // List to store distinct vowels
    let y = [];
    let length = str.length;

    // if length of String is less than 5
    // then always Impossible
    if (length < 5)
        document.write("Impossible<br>");
    else
    {
        // Storing the distinct vowels in the String
        // by checking if it in the list of String and not
        // in the list of distinct vowels
        for (let i = 0; i < length; i++)
        {
            if (find(x, str[i])&&
                !find(y, str[i]))
                y.push(str[i]);
        }

        // Storing the vowels which are
        // not present in the String
        let z = [];
        for (let i = 0; i < 5; i++)
            if (!find(y, x[i]) )
                z.push(x[i]);

        // No replacement needed condition
        if (z.length == 0)
            document.write( str+"<br>" );
        else
        {
            let cc = 0;
            let y1 = [];
               let ans = "";

            // Replacing the characters to get all Vowels
            for (let i = 0; i < length; i++)
            {
            if (find(x, str[i])&&
                !find(y1, str[i]))
                {
                    ans += str[i];
                    y1.push(str[i]);
                }
                else
                {
                    ans += z[cc];
                    cc++;
                }
                if (cc == z.length)
                {
                    //copy th rest of the string
                    for(let j = i + 1; j < length; j++)
                        ans += str[j];
                        break;
                }
            }
            document.write(ans);
        }
    }
}

// Driver Code
let str = "ABCDEFGHI";
addAllVowel(str);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
AOUDEFGHI
```

***时间复杂度:** O(N)，其中 N 是字符串的大小*

***辅助空间:** O(N)*