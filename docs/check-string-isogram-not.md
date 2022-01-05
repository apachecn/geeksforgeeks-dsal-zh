# 检查一个字符串是否为等值线

> 原文:[https://www.geeksforgeeks.org/check-string-isogram-not/](https://www.geeksforgeeks.org/check-string-isogram-not/)

给定一个单词或短语，检查它是否是等值线图。等值线是一个字母出现不超过一次的单词。
**例:**

```
Input : Machine
Output : True
"Machine" does not have any character repeating, 
it is an Isogram

Input : Geek
Output : False
"Geek" has 'e' as repeating character, 
it is not an Isogram
```

## C++

```
// C++ program to check
// if a given string is isogram or not
#include <bits/stdc++.h>
using namespace std;

// Function to check
// if a given string is isogram or not
string is_isogram(string str)
{
    int len = str.length();

    // Convert the string in lower case letters
    for (int i = 0; i < len; i++)
        str[i] = tolower(str[i]);

    sort(str.begin(), str.end());

    for (int i = 0; i < len; i++) {
        if (str[i] == str[i + 1])
            return "False";
    }
    return "True";
}

// driver program
int main()
{
    string str1 = "Machine";
    cout << is_isogram(str1) << endl;

    string str2 = "isogram";
    cout << is_isogram(str2) << endl;

    string str3 = "GeeksforGeeks";
    cout << is_isogram(str3) << endl;

    string str4 = "Alphabet";
    cout << is_isogram(str4) << endl;

    return 0;
}

// Contributed by nuclode
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if a given string is isogram or not
import java.io.*;
import java.util.*;

class GFG {
    // Function to check
    // if a given string is isogram or not
    static boolean is_isogram(String str)
    {
        // Convert the string in lower case letters
        str = str.toLowerCase();
        int len = str.length();

        char arr[] = str.toCharArray();

        Arrays.sort(arr);
        for (int i = 0; i < len - 1; i++) {
            if (arr[i] == arr[i + 1])
                return false;
        }
        return true;
    }

    // driver program
    public static void main(String[] args)
    {
        String str1 = "Machine";
        System.out.println(is_isogram(str1));

        String str2 = "isogram";
        System.out.println(is_isogram(str2));

        String str3 = "GeeksforGeeks";
        System.out.println(is_isogram(str3));

        String str4 = "Alphabet";
        System.out.println(is_isogram(str4));
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to check
# if a word is isogram or not
def is_isogram(word):

    # Convert the word or sentence in lower case letters.
    clean_word = word.lower()

    # Make an empty list to append unique letters
    letter_list = []

    for letter in clean_word:

        # If letter is an alphabet then only check
        if letter.isalpha():
            if letter in letter_list:
                return False
            letter_list.append(letter)

    return True

if __name__ == '__main__':
    print(is_isogram("Machine"))                            
    print(is_isogram("isogram"))                        
    print(is_isogram("GeeksforGeeks"))                    
    print(is_isogram("Alphabet "))                                              
```

## C#

```
// C# program to check if a given
// string is isogram or not
using System;

public class GFG {

    // Function to check if a given
    // string is isogram or not
    static bool is_isogram(string str)
    {
        // Convert the string in lower case letters
        str = str.ToLower();
        int len = str.Length;

        char[] arr = str.ToCharArray();

        Array.Sort(arr);
        for (int i = 0; i < len - 1; i++) {
            if (arr[i] == arr[i + 1])
                return false;
        }
        return true;
    }

    // driver program
    public static void Main()
    {
        string str1 = "Machine";
        Console.WriteLine(is_isogram(str1));

        string str2 = "isogram";
        Console.WriteLine(is_isogram(str2));

        string str3 = "GeeksforGeeks";
        Console.WriteLine(is_isogram(str3));

        string str4 = "Alphabet";
        Console.WriteLine(is_isogram(str4));
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>
    // Javascript program to check if a given
    // string is isogram or not

    // Function to check if a given
    // string is isogram or not
    function is_isogram(str)
    {
        // Convert the string in lower case letters
        str = str.toLowerCase();
        let len = str.length;

        let arr = str.split('');

        arr.sort();
        for (let i = 0; i < len - 1; i++) {
            if (arr[i] == arr[i + 1])
                return false;
        }
        return true;
    }

    let str1 = "Machine";
    if(is_isogram(str1))
    {
        document.write("True" + "</br>");
    }
    else{
        document.write("False" + "</br>");
    }

    let str2 = "isogram";
    if(is_isogram(str2))
    {
        document.write("True" + "</br>");
    }
    else{
        document.write("False" + "</br>");
    }

    let str3 = "GeeksforGeeks";
    if(is_isogram(str3))
    {
        document.write("True" + "</br>");
    }
    else{
        document.write("False" + "</br>");
    }

    let str4 = "Alphabet";
    if(is_isogram(str4))
    {
        document.write("True" + "</br>");
    }
    else{
        document.write("False" + "</br>");
    }

    // This code is contributed by suresh07.
</script>
```

输出:

```
True
True
False
False
```

**另一种方法:**在这种情况下，字符串的字符数存储在 hashmap 中，如果发现任何字符的字符数大于 1，则返回 false，否则返回 true。

## C++

```
// CPP code to check string is isogram or not
#include <bits/stdc++.h>

using namespace std;

// function to check isogram
bool check_isogram(string str)
{

    int length = str.length();
    int mapHash[26] = { 0 };

    // loop to store count of chars and check if it is greater than 1
    for (int i = 0; i < length; i++)
    {
        mapHash[str[i] - 'a']++;

        // if count > 1, return false
        if (mapHash[str[i]-'a'] > 1)
        {
            return false;
        }
    }

    return true;
}

// Driver code
int main()
{
    string str = "geeks";
    string str2 = "computer";

    // checking str as isogram
    if (check_isogram(str)) {
        cout << "True" << endl;
    }
    else {
        cout << "False" << endl;
    }

    // checking str2 as isogram
    if (check_isogram(str2)) {
        cout << "True" << endl;
    }
    else {
        cout << "False" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check string is isogram or not
class GFG
{

// function to check isogram
static boolean check_isogram(String str)
{

    int length = str.length();
    int mapHash[] = new int[26];

    // loop to store count of chars and
    // check if it is greater than 1
    for (int i = 0; i < length; i++)
    {
        mapHash[str.charAt(i) - 'a']++;

        // if count > 1, return false
        if (mapHash[str[i]-'a'] > 1)
        {
            return false;
        }
    }

    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeks";
    String str2 = "computer";

    // checking str as isogram
    if (check_isogram(str))
        System.out.println("True");
    else
        System.out.println("False");

    // checking str2 as isogram
    if (check_isogram(str2))
            System.out.println("True");
    else
        System.out.println("False");
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to check string is isogram or not

# function to check isogram
def check_isogram(string) :

    length = len(string);
    mapHash = [0] * 26;

    # loop to store count of chars
    # and check if it is greater than 1
    for i in range(length) :

        mapHash[ord(string[i]) - ord('a')] += 1;

        # if count > 1, return false
        if (mapHash[ord(string[i]) - ord('a')] > 1) :

            return False;

    return True;

# Driver code
if __name__ == "__main__" :

    string = "geeks";
    string2 = "computer";

    # checking str as isogram
    if (check_isogram(string)) :
        print("True");
    else :
        print("False");

    # checking str2 as isogram
    if (check_isogram(string2)) :
        print("True")

    else :
        print("False");

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to check string is isogram or not
using System;
public class GFG
{

// function to check isogram
static bool check_isogram(String str)
{

    int length = str.Length;
    int []mapHash = new int[26];

    // loop to store count of chars and
    // check if it is greater than 1
    for (int i = 0; i < length; i++)
    {
        mapHash[str[i] - 'a']++;

        // if count > 1, return false
        if (mapHash[str[i] - 'a'] > 1)
        {
            return false;
        }
    }

    return true;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeks";
    String str2 = "computer";

    // checking str as isogram
    if (check_isogram(str))
        Console.WriteLine("True");
    else
        Console.WriteLine("False");

    // checking str2 as isogram
    if (check_isogram(str2))
            Console.WriteLine("True");
    else
        Console.WriteLine("False");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript code to check string is isogram or not

    // function to check isogram
    function check_isogram(str)
    {

        let length = str.length;
        let mapHash = new Array(26);
        mapHash.fill(0);

        // loop to store count of chars and
        // check if it is greater than 1
        for (let i = 0; i < length; i++)
        {
            mapHash[str[i].charCodeAt() - 'a'.charCodeAt()]++;

            // if count > 1, return false
            if (mapHash[str[i].charCodeAt() - 'a'.charCodeAt()] > 1)
            {
                return false;
            }
        }

        return true;
    }

    let str = "geeks";
    let str2 = "computer";

    // checking str as isogram
    if (check_isogram(str))
        document.write("True" + "</br>");
    else
        document.write("False" + "</br>");

    // checking str2 as isogram
    if (check_isogram(str2))
          document.write("True" + "</br>");
    else
        document.write("False" + "</br>");

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
False
True
```

//感谢**萨赫勒班萨尔**提出上述方法。

本文由**萨基提瓦里**供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。