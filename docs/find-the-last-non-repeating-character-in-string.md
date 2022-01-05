# 查找字符串中最后一个不重复的字符

> 原文:[https://www . geesforgeks . org/find-最后一个非重复字符串字符/](https://www.geeksforgeeks.org/find-the-last-non-repeating-character-in-string/)

给定一个字符串 **str** ，任务是找到其中最后一个不重复的字符。
例如，如果输入字符串是**“GeeksForGeeks”**，那么输出应该是**‘r’**，如果输入字符串是**“GeeksQuiz”**，那么输出应该是**‘z’**。如果没有不重复字符，则打印 **-1** 。
**举例:**

> **输入:**str = " GeeksForGeeks "
> T3】输出:r
> “r”是从末尾开始的第一个字符，频率为 1。
> **输入:** str = "aabbcc"
> **输出:** -1
> 给定字符串的所有字符的频率都大于 1。

**方法:**创建一个频率数组，存储给定字符串中每个字符的频率。频率更新后，开始逐个字符遍历字符串，如果当前字符的频率为 1，则这是最后一个不重复的字符。如果所有字符的频率都大于 1，则打印-1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Maximum distinct characters possible
const int MAX = 256;

// Function to return the last non-repeating character
static string lastNonRepeating(string str, int n)
{

    // To store the frequency of each of
    // the character of the given string
    int freq[MAX] = {0};

    // Update the frequencies
    for (int i = 0; i < n; i++)
        freq[str.at(i)]++;

    // Starting from the last character
    for (int i = n - 1; i >= 0; i--)
    {

        // Current character
        char ch = str.at(i);

        // If frequency of the current character is 1
        // then return the character
        if (freq[ch] == 1)
        {
            string res;
            res+=ch;
            return res;
        }
    }

    // All the characters of the
    // string are repeating
    return "-1";
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    int n = str.size();
    cout<< lastNonRepeating(str, n);
    return 0;
}

// This code has been contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Maximum distinct characters possible
    static final int MAX = 256;

    // Function to return the last non-repeating character
    static String lastNonRepeating(String str, int n)
    {

        // To store the frequency of each of
        // the character of the given string
        int freq[] = new int[MAX];

        // Update the frequencies
        for (int i = 0; i < n; i++)
            freq[str.charAt(i)]++;

        // Starting from the last character
        for (int i = n - 1; i >= 0; i--) {

            // Current character
            char ch = str.charAt(i);

            // If frequency of the current character is 1
            // then return the character
            if (freq[ch] == 1)
                return ("" + ch);
        }

        // All the characters of the
        // string are repeating
        return "-1";
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "GeeksForGeeks";
        int n = str.length();
        System.out.println(lastNonRepeating(str, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Maximum distinct characters possible
MAX = 256;

# Function to return the last non-repeating character
def lastNonRepeating(string, n) :

    # To store the frequency of each of
    # the character of the given string
    freq = [0]*MAX;

    # Update the frequencies
    for i in range(n) :
        freq[ord(string[i])] += 1;

    # Starting from the last character
    for i in range(n-1,-1,-1) :

        # Current character
        ch = string[i];

        # If frequency of the current character is 1
        # then return the character
        if (freq[ord(ch)] == 1) :
            return ("" + ch);

    # All the characters of the
    # string are repeating
    return "-1";

# Driver code
if __name__ == "__main__" :

    string = "GeeksForGeeks";
    n = len(string);

    print(lastNonRepeating(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Maximum distinct characters possible
    static readonly int MAX = 256;

    // Function to return the last non-repeating character
    static String lastNonRepeating(String str, int n)
    {

        // To store the frequency of each of
        // the character of the given string
        int []freq = new int[MAX];

        // Update the frequencies
        for (int i = 0; i < n; i++)
            freq[str[i]]++;

        // Starting from the last character
        for (int i = n - 1; i >= 0; i--)
        {

            // Current character
            char ch = str[i];

            // If frequency of the current character is 1
            // then return the character
            if (freq[ch] == 1)
                return ("" + ch);
        }

        // All the characters of the
        // string are repeating
        return "-1";
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "GeeksForGeeks";
        int n = str.Length;
        Console.WriteLine(lastNonRepeating(str, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

     // Maximum distinct characters possible
    let MAX = 256;

    // Function to return the last non-repeating character
    function lastNonRepeating(str,n)
    {
        // To store the frequency of each of
        // the character of the given string
        let freq = new Array(MAX);
          for(let i=0;i<MAX;i++)
        {
            freq[i]=0;
        }
        // Update the frequencies
        for (let i = 0; i < n; i++)
            freq[str[i].charCodeAt(0)]++;

        // Starting from the last character
        for (let i = n - 1; i >= 0; i--) {

            // Current character
            let ch = str[i];

            // If frequency of the current character is 1
            // then return the character
            if (freq[ch.charCodeAt(0)] == 1)
                return ("" + ch);
        }

        // All the characters of the
        // string are repeating
        return "-1";
    }

    // Driver code
    let str = "GeeksForGeeks";
    let n = str.length;
    document.write(lastNonRepeating(str, n));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
r
```