# 长度为 3 的回文字符串，可以使用给定字符串的字符

> 原文:[https://www . geeksforgeeks . org/回文-长度为 3 的字符串-通过使用给定字符串的可能字符/](https://www.geeksforgeeks.org/palindromic-strings-of-length-3-possible-by-using-characters-of-a-given-string/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是按照字典顺序打印所有长度为 **3** 的[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)，这些字符串可以使用给定字符串 **S** 的字符形成。

**示例:**

> **输入:**S = " aabc "
> T3】输出:T5】ABA
> ACA
> 
> **输入:**S = " ddad BAC "
> T3】输出:T5】ABA
> ACA
> ada
> dad
> DBD
> DCD
> DDD

**方法:**给定的问题可以通过使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)的概念来解决，通过使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储字符数来实现它。按照以下步骤解决问题:

*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如说**哈希**，存储每个字符的计数。
*   将字符串每个字符的[频率存储在地图**哈希**](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/) 中。
*   初始化一组[字符串，比如 **st** ，来存储所有长度为 **3** 的回文字符串。](https://www.geeksforgeeks.org/set-in-cpp-stl/)
*   [使用变量 **i** 迭代字符【a，z】](https://www.geeksforgeeks.org/program-to-display-all-alphabets-from-a-to-z-in-uppercase-and-lowercase-both/)，并执行以下步骤:
    *   如果**散列【I】**的值是 **2** ，则[使用变量 **j** 迭代范围【a，z】](https://www.geeksforgeeks.org/program-to-display-all-alphabets-from-a-to-z-in-uppercase-and-lowercase-both/)内的字符。如果 **Hash[j]** 的值大于 **0** 且 **i** 不等于 **j** ，则将**字符串(i + j + i)** 插入到 Set **st** 中。
    *   否则，如果 **Hash[i]** 的值大于 **2** ，则[使用变量 **j** 迭代范围【a，z】](https://www.geeksforgeeks.org/program-to-display-all-alphabets-from-a-to-z-in-uppercase-and-lowercase-both/)内的字符，如果 **Hash[j]** 的值大于 **0** ，则在集合 **st** 中插入**字符串(i + j + i)** 。
*   完成上述步骤后，[遍历设置的](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/) **st** 并打印其中存储的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print all palindromic
// strings of length 3 that can be
// formed using characters of string S
void generatePalindrome(string S)
{
    // Stores the count of character
    unordered_map<char, int> Hash;

    // Traverse the string S
    for (auto ch : S) {
        Hash[ch]++;
    }

    // Stores all palindromic strings
    set<string> st;

    // Iterate over the charchaters
    // over the range ['a', 'z']
    for (char i = 'a'; i <= 'z'; i++) {

        // If Hash[ch] is equal to 2
        if (Hash[i] == 2) {

            // Iterate over the characters
            // over the range ['a', 'z']
            for (char j = 'a'; j <= 'z'; j++) {

                // Stores all the
                // palindromic string
                string s = "";
                if (Hash[j] && i != j) {

                    s += i;
                    s += j;
                    s += i;

                    // Push the s into
                    // the set st
                    st.insert(s);
                }
            }
        }

        // If Hash[i] is greater than
        // or equal to 3
        if (Hash[i] >= 3) {

            // Iterate over charchaters
            // over the range ['a', 'z']
            for (char j = 'a';
                 j <= 'z'; j++) {

                // Stores all the
                // palindromic string
                string s = "";

                // If Hash[j] is positive
                if (Hash[j]) {
                    s += i;
                    s += j;
                    s += i;

                    // Push s into
                    // the set st
                    st.insert(s);
                }
            }
        }
    }

    // Iterate over the set
    for (auto ans : st) {
        cout << ans << "\n";
    }
}

// Driver Code
int main()
{
    string S = "ddabdac";
    generatePalindrome(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to print all palindromic
    // strings of length 3 that can be
    // formed using characters of string S
    static void generatePalindrome(String S)
    {

        // Stores the count of character
        HashMap<Character, Integer> Hash = new HashMap<>();

        // Traverse the string S
        for(int i = 0; i < S.length(); i++)
        {
            if (Hash.containsKey(S.charAt(i)))
                Hash.put(S.charAt(i), Hash.get(S.charAt(i))+1);
            else
                Hash.put(S.charAt(i), 1);
        }

        // Stores all palindromic strings
        TreeSet<String> st = new TreeSet<String>();

        // Iterate over the charchaters
        // over the range ['a', 'z']
        for(char i = 'a'; i <= 'z'; i++)
        {

            // If Hash[ch] is equal to 2
            if (Hash.containsKey(i) && Hash.get(i) == 2)
            {

                // Iterate over the characters
                // over the range ['a', 'z']
                for(char j = 'a'; j <= 'z'; j++)
                {

                    // Stores all the
                    // palindromic string
                    String s = "";

                    if (Hash.containsKey(j) && i != j)
                    {
                        s += i;
                        s += j;
                        s += i;

                        // Push the s into
                        // the set st
                        st.add(s);
                    }
                }
            }

            // If Hash[i] is greater than
            // or equal to 3
            if (Hash.containsKey(i) && Hash.get(i) >= 3)
            {

                // Iterate over charchaters
                // over the range ['a', 'z']
                for(char j = 'a'; j <= 'z'; j++)
                {

                    // Stores all the
                    // palindromic string
                    String s = "";

                    // If Hash[j] is positive
                    if (Hash.containsKey(j))
                    {
                        s += i;
                        s += j;
                        s += i;

                        // Push s into
                        // the set st
                        st.add(s);
                    }
                }
            }
        }

        // Iterate over the set
        for(String ans : st)
        {
            System.out.println(ans);
        }
    }

  // Driver code
    public static void main(String[] args) {
        String S = "ddabdac";

        generatePalindrome(S);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all palindromic
# strings of length 3 that can be
# formed using characters of string S
def generatePalindrome(S):

    # Stores the count of character
    Hash = {}

    # Traverse the string S
    for ch in S:
        Hash[ch] = Hash.get(ch,0) + 1

    # Stores all palindromic strings
    st = {}

    # Iterate over the charchaters
    # over the range ['a', 'z']
    for i in range(ord('a'), ord('z') + 1):

        # If Hash[ch] is equal to 2
        if (chr(i) in Hash and Hash[chr(i)] == 2):

            # Iterate over the characters
            # over the range ['a', 'z']
            for j in range(ord('a'), ord('z') + 1):

                # Stores all the
                # palindromic string
                s = ""

                if (chr(j) in Hash and i != j):
                    s += chr(i)
                    s += chr(j)
                    s += chr(i)

                    # Push the s into
                    # the set st
                    st[s] = 1

        # If Hash[i] is greater than
        # or equal to 3
        if ((chr(i) in Hash) and Hash[chr(i)] >= 3):

            # Iterate over charchaters
            # over the range ['a', 'z']
            for j in range(ord('a'), ord('z') + 1):

                # Stores all the
                # palindromic string
                s = ""

                # If Hash[j] is positive
                if (chr(j) in Hash):
                    s += chr(i)
                    s += chr(j)
                    s += chr(i)

                    # Push s into
                    # the set st
                    st[s] = 1

    # Iterate over the set
    for ans in st:
        print(ans)

# Driver Code
if __name__ == '__main__':

    S = "ddabdac"

    generatePalindrome(S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print all palindromic
// strings of length 3 that can be
// formed using characters of string S
static void generatePalindrome(string S)
{

    // Stores the count of character
    Dictionary<char,
               int> Hash = new Dictionary<char,
                                          int>();

    // Traverse the string S
    foreach (char ch in S)
    {
        if (Hash.ContainsKey(ch))
            Hash[ch]++;
        else
            Hash.Add(ch, 1);
    }

    // Stores all palindromic strings
    HashSet<string> st = new HashSet<string>();

    // Iterate over the charchaters
    // over the range ['a', 'z']
    for(char i = 'a'; i <= 'z'; i++)
    {

        // If Hash[ch] is equal to 2
        if (Hash.ContainsKey(i) && Hash[i] == 2)
        {

            // Iterate over the characters
            // over the range ['a', 'z']
            for(char j = 'a'; j <= 'z'; j++)
            {

                // Stores all the
                // palindromic string
                string s = "";

                if (Hash.ContainsKey(j) && i != j)
                {
                    s += i;
                    s += j;
                    s += i;

                    // Push the s into
                    // the set st
                    st.Add(s);
                }
            }
        }

        // If Hash[i] is greater than
        // or equal to 3
        if (Hash.ContainsKey(i) && Hash[i] >= 3)
        {

            // Iterate over charchaters
            // over the range ['a', 'z']
            for(char j = 'a'; j <= 'z'; j++)
            {

                // Stores all the
                // palindromic string
                string s = "";

                // If Hash[j] is positive
                if (Hash.ContainsKey(j))
                {
                    s += i;
                    s += j;
                    s += i;

                    // Push s into
                    // the set st
                    st.Add(s);
                }
            }
        }
    }

    // Iterate over the set
    foreach(string ans in st)
    {
        Console.WriteLine(ans);
    }
}

// Driver Code
public static void Main()
{
    string S = "ddabdac";

    generatePalindrome(S);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print all palindromic
// strings of length 3 that can be
// formed using characters of string S
function generatePalindrome(S)
{
    // Stores the count of character
    let Hash=new Map();

    // Traverse the string S
    for (let ch=0;ch< S.length;ch++) {
        if(!Hash.has(S[ch]))
            Hash.set(S[ch],1);
        else
        {
            Hash.set(S[ch],Hash.get(S[ch])+1)
        }

    }

    // Stores all palindromic strings
    let st=new Set();

    // Iterate over the charchaters
    // over the range ['a', 'z']
    for (let i = 'a'.charCodeAt(0); i <= 'z'.charCodeAt(0); i++) {

        // If Hash[ch] is equal to 2
        if (Hash.get(String.fromCharCode(i)) == 2) {

            // Iterate over the characters
            // over the range ['a', 'z']
            for (let j = 'a'.charCodeAt(0); j <= 'z'.charCodeAt(0); j++) {

                // Stores all the
                // palindromic string
                let s = "";
                if (Hash.get(String.fromCharCode(j)) && i != j) {

                    s += String.fromCharCode(i);
                    s += String.fromCharCode(j);
                    s += String.fromCharCode(i);

                    // Push the s into
                    // the set st
                    st.add(s);
                }
            }
        }

        // If Hash[i] is greater than
        // or equal to 3
        if (Hash.get(String.fromCharCode(i)) >= 3) {

            // Iterate over charchaters
            // over the range ['a', 'z']
            for (let j = 'a'.charCodeAt(0);
                 j <= 'z'.charCodeAt(0); j++) {

                // Stores all the
                // palindromic string
                let s = "";

                // If Hash[j] is positive
                if (Hash.get(String.fromCharCode(j))) {
                    s += String.fromCharCode(i);
                    s += String.fromCharCode(j);
                    s += String.fromCharCode(i);

                    // Push s into
                    // the set st
                    st.add(s);
                }
            }
        }
    }

    // Iterate over the set
    for (let item of st.values()) {
        document.write(item+"<br>")
    }
}

// Driver Code
let S = "ddabdac";
generatePalindrome(S);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
aba
aca
ada
dad
dbd
dcd
ddd
```

***时间复杂度:**O(26 * 26)*
T5**辅助空间:** O(26)