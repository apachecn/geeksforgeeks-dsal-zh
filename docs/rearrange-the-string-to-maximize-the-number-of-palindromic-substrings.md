# 重新排列字符串以最大化回文子串的数量

> 原文:[https://www . geeksforgeeks . org/重排字符串以最大化回文子字符串的数量/](https://www.geeksforgeeks.org/rearrange-the-string-to-maximize-the-number-of-palindromic-substrings/)

给定一个仅由小写字符(a-z)组成的字符串 S，任务是通过以最大化回文子字符串数量的方式重新排列字符串来打印一个新字符串。如果有多个答案，打印任意一个。
**注意:**即使某些子字符串重合，也要按照它们在获得的字符串中出现的次数进行计数。
**示例:**

> **输入:** s = "aabab"
> **输出:**亚的斯亚贝巴
> 字符串“亚的斯亚贝巴”有 9 个回文子串:“a”、“b”、“a”、“b”、“a”、“aba”、“bab”、“aba”、“亚的斯亚贝巴”。
> **输入:** s = "aa"
> **输出:** aa
> 给定的字符串具有可能的最大数量的回文子串，“a”、“a”和“aa”。

这个问题看起来可能很复杂，但通过解决各种情况并进行观察，将会得到一个简单的解决方案。
一个**简单的**解决方案是将字符串排序并打印出来。排序取 **O(N * log N)** 。
一种**高效的**解决方案是使用 **freq[]** 数组计算每个字符的频率，然后使用 freq[]数组构建字符串。
以下是上述办法的实施情况。

## C++

```
// C++ program to rearrange the
// string such to maximize the
// number of palindromic substrings
#include <bits/stdc++.h>
using namespace std;

// Function to return the newString
string newString(string s)
{
    // length of string
    int l = s.length();

    // hashing array
    int freq[26] = { 0 };

    // iterate and count
    for (int i = 0; i < l; i++) {
        freq[s[i] - 'a'] += 1;
    }

    // resulting string
    string ans = "";

    // form the resulting string
    for (int i = 0; i < 26; i++) {

        // number of times character appears
        for (int j = 0; j < freq[i]; j++) {

            // append to resulting string
            ans += (char)(97 + i);
        }
    }

    return ans;
}

// Driver Code
int main()
{

    string s = "aabab";

    cout << newString(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange the
// string such to maximize the
// number of palindromic substrings

public class GFG {

    // Function to return the newString
    static String newString(String s)
    {
        // length of string
        int l = s.length();

        // hashing array
        int freq[] = new int [26] ;

        // iterate and count
        for (int i = 0; i < l; i++) {
            freq[s.charAt(i) - 'a'] += 1;
        }

        // resulting string
        String ans = "";

        // form the resulting string
        for (int i = 0; i < 26; i++) {

            // number of times character appears
            for (int j = 0; j < freq[i]; j++) {

                // append to resulting string
                ans += (char)(97 + i);
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
           String s = "aabab";
            System.out.println(newString(s));
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to rearrange the
# string such to maximize the
# number of palindromic substrings

# Function to return the newString
def newString(s):

    # length of string
    l = len(s)

    # hashing array
    freq = [0] * (26)

    # iterate and count
    for i in range(0, l):
        freq[ord(s[i]) - ord('a')] += 1

    # resulting string
    ans = ""

    # form the resulting string
    for i in range(0, 26):

        # number of times character appears
        for j in range(0, freq[i]):

            # append to resulting string
            ans += chr(97 + i)

    return ans

# Driver Code
if __name__ == "__main__":

    s = "aabab"
    print(newString(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to rearrange the
// string such to maximize the
// number of palindromic substrings
using System;
class GFG
{

// Function to return the newString
static String newString(string s)
{
    // length of string
    int l = s.Length;

    // hashing array
    int[] freq = new int [26];

    // iterate and count
    for (int i = 0; i < l; i++)
    {
        freq[s[i] - 'a'] += 1;
    }

    // resulting string
    string ans = "";

    // form the resulting string
    for (int i = 0; i < 26; i++)
    {

        // number of times character appears
        for (int j = 0; j < freq[i]; j++)
        {

            // append to resulting string
            ans += (char)(97 + i);
        }
    }

    return ans;
}

// Driver code
public static void Main()
{
    string s = "aabab";
    Console.Write(newString(s));
}
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>
    // Javascript program to rearrange the
    // string such to maximize the
    // number of palindromic substrings

    // Function to return the newString
    function newString(s)
    {
        // length of string
        let l = s.length;

        // hashing array
        let freq = new Array(26);
        freq.fill(0);

        // iterate and count
        for (let i = 0; i < l; i++)
        {
            freq[s[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        }

        // resulting string
        let ans = "";

        // form the resulting string
        for (let i = 0; i < 26; i++)
        {

            // number of times character appears
            for (let j = 0; j < freq[i]; j++)
            {

                // append to resulting string
                ans += String.fromCharCode(97 + i);
            }
        }

        return ans;
    }

     let s = "aabab";
    document.write(newString(s));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
aaabb
```

**时间复杂度**:O(N)
T3】辅助空间: O(26)