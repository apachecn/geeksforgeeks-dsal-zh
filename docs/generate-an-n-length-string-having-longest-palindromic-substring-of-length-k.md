# 生成长度为 K 的 N 长度的回文子串

> 原文:[https://www . geesforgeks . org/generate-an-n-length-string-having-最长回文-长度为-k 的子串/](https://www.geeksforgeeks.org/generate-an-n-length-string-having-longest-palindromic-substring-of-length-k/)

给定两个整数 **N** 和 **K** ( *K ≤ N* )，任务是获得长度为 **N** 的字符串，使得该字符串的回文子串的最大长度为 **K** 。

**示例:**

> **输入:** N = 5，K = 3
> **输出:**【abacd】
> **说明:**回文子串为“a”、“b”、“c”、“d”和“aba”。因此，给定字符串中最长的回文子串长度为 3。
> 
> **输入:** N = 8，K = 4
> **输出:**“abcdef”
> **解释:**回文子串为“a”、“b”、“c”、“d”、“e”、“f”、“bb”、“abba”。因此，给定字符串中最长的回文子串长度为 4。

**方法:**这个想法基于以下观察:由单个字符组成的任何长度的字符串总是回文，例如{'a '，' bbbbb '，' ccc'}。因此，为了生成具有所需条件的字符串，打印“a”**K**次，使其具有长度为 **K** 的最长回文子串，并用非回文序列填充剩余的**N–K**槽。

按照以下步骤解决问题:

*   精确打印“a”次 **K** 。
*   考虑一个非回文序列，比如“bcd”。
*   打印字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate a string of
// length N having longest palindromic
// substring of length K
void string_palindrome(int N, int K)
{

    // Fill first K characters with 'a'
    for (int i = 0; i < K; i++)
        cout << "a";

    // Stores a non-palindromic sequence
    // to be repeated for N - k slots
    string s = "bcd";

    // Print N - k remaining characters
    for (int i = 0; i < N - K; i++)
        cout << s[i % 3];
}

// Driver Code
int main()
{

    // Given N and K
    int N = 5, K = 3;
    string_palindrome(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.*;

class GFG
{

// Function to generate a String of
// length N having longest palindromic
// subString of length K
static void String_palindrome(int N, int K)
{

    // Fill first K characters with 'a'
    for (int i = 0; i < K; i++)
        System.out.print("a");

    // Stores a non-palindromic sequence
    // to be repeated for N - k slots
    String s = "bcd";

    // Print N - k remaining characters
    for (int i = 0; i < N - K; i++)
        System.out.print(s.charAt(i % 3));
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 5, K = 3;
    String_palindrome(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to generate a string of
# length N having longest palindromic
# substring of length K
def string_palindrome(N, K):

    # Fill first K characters with 'a'
    for i in range(K):
        print("a", end = "")

    # Stores a non-palindromic sequence
    # to be repeated for N - k slots
    s = "bcd"

    # PrN - k remaining characters
    for i in range(N - K):
        print(s[i % 3], end = "")

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N, K = 5, 3
    string_palindrome(N, K)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement the above approach
using System;
class GFG
{

    // Function to generate a String of
    // length N having longest palindromic
    // subString of length K
    static void String_palindrome(int N, int K)
    {

        // Fill first K characters with 'a'
        for (int i = 0; i < K; i++)
            Console.Write("a");

        // Stores a non-palindromic sequence
        // to be repeated for N - k slots
        string s = "bcd";

        // Print N - k remaining characters
        for (int i = 0; i < N - K; i++)
            Console.Write(s[i % 3]);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Given N and K
        int N = 5, K = 3;
        String_palindrome(N, K);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript program for above approach

    // Function to generate a String of
    // length N having longest palindromic
    // subString of length K
    function String_palindrome(N, K)
    {

        // Fill first K characters with 'a'
        for (let i = 0; i < K; i++)
            document.write("a");

        // Stores a non-palindromic sequence
        // to be repeated for N - k slots
        let s = "bcd";

        // Print N - k remaining characters
        for (let i = 0; i < N - K; i++)
            document.write(s[i % 3]);
    }

// Driver Code

     // Given N and K
        let N = 5, K = 3;
        String_palindrome(N, K);

</script>
```

**Output:** 

```
aaabc
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)