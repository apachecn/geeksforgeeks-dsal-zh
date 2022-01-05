# 检查一个字符串中是否存在两个相同的子序列

> 原文:[https://www . geesforgeks . org/check-如果两个相同的子序列存在于一个字符串中或不存在/](https://www.geeksforgeeks.org/check-if-two-same-sub-sequences-exist-in-a-string-or-not/)

给定一个字符串，任务是检查在给定的字符串中是否存在两个相等的子序列。如果两个子序列具有以相同的词典顺序排列的相同字符，但是字符的位置不同于原始字符串中的位置，则称这两个子序列相等。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:** YES
> 两个可能的子序列是“geeks”和“geeks”。
> **输入:** str = "bhuvan"
> **输出:**否

**方法:**解决这个问题的方法是检查是否有任何字符出现不止一次。由于匹配子序列的最小长度可以是 1，因此如果一个字符在一个字符串中出现不止一次，那么两个相似的子序列是可能的。初始化一个长度为 26 的 *freq[]* 数组。迭代字符串并增加字符的频率。迭代 freq 数组并检查 0-26 范围内的任何 I 的 freq[i]是否大于 1，那么这是可能的。
以下是上述办法的实施情况。

## C++

```
// C++ program to Check if
// similar subsequences exist or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if similar subsequences
// occur in a string or not
bool check(string s, int l)
{

    int freq[26] = { 0 };
    // iterate and count the frequency
    for (int i = 0; i < l; i++) {
        freq[s[i] - 'a']++; // counting frequency of the letters
    }

    // check if frequency is more
    // than once of any character
    for (int i = 0; i < 26; i++) {
        if (freq[i] >= 2)
            return true;
    }
    return false;
}
// Driver Code
int main()
{
    string s = "geeksforgeeks";
    int l = s.length();
    if (check(s, l))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check
// if similar subsequences
// exist or not
import java.io.*;
import java.util.*;
import java.util.Arrays;

class GFG
{
// Function to check if
// similar subsequences
// occur in a string or not
static boolean check(String s,
                     int l)
{
    int freq[] = new int[26];
    Arrays.fill(freq, 0);

    // iterate and count
    // the frequency
    for (int i = 0; i < l; i++)
    {
        // counting frequency
        // of the letters
        freq[s.charAt(i) - 'a']++;
    }

    // check if frequency is more
    // than once of any character
    for (int i = 0; i < 26; i++)
    {
        if (freq[i] >= 2)
            return true;
    }
    return false;
}

// Driver Code
public static void main(String args[])
{
    String s = "geeksforgeeks";
    int l = s.length();
    if (check(s, l))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}
```

## 蟒蛇 3

```
# Python 3 program to Check if
# similar subsequences exist or not

# Function to check if similar subsequences
# occur in a string or not
def check(s, l):
    freq = [0 for i in range(26)]

    # iterate and count the frequency
    for i in range(l):

        # counting frequency of the letters
        freq[ord(s[i]) - ord('a')] += 1

    # check if frequency is more
    # than once of any character
    for i in range(26):
        if (freq[i] >= 2):
            return True

    return False

# Driver Code
if __name__ == '__main__':
    s = "geeksforgeeks"
    l = len(s)
    if (check(s, l)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# Pprogram to Check if similar subsequences
// exist or not
using System;
using System.Collections.Generic;            

class GFG
{

// Function to check if similar subsequences
// occur in a string or not
static bool check(String s, int l)
{
    int []freq = new int[26];

    // iterate and count the frequency
    for (int i = 0; i < l; i++)
    {
        // counting frequency of the letters
        freq[s[i] - 'a']++;
    }

    // check if frequency is more
    // than once of any character
    for (int i = 0; i < 26; i++)
    {
        if (freq[i] >= 2)
            return true;
    }
    return false;
}

// Driver Code
public static void Main(String []args)
{
    String s = "geeksforgeeks";
    int l = s.Length;
    if (check(s, l))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to Check
// if similar subsequences
// exist or not

// Function to check if
// similar subsequences
// occur in a string or not
function check(s, l)
{
    let freq = new Array(26).fill(0);

    // iterate and count
    // the frequency
    for (let i = 0; i < l; i++)
    {
        // counting frequency
        // of the letters
        freq[s[i].charCodeAt() - 'a'.charCodeAt()]++;
    }

    // check if frequency is more
    // than once of any character
    for (let i = 0; i < 26; i++)
    {
        if (freq[i] >= 2)
            return true;
    }
    return false;
}

// Driver Code

    let s = "geeksforgeeks";
    let l = s.length;
    if (check(s, l))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
**注**:如果提到相似子序列的长度，那么解决问题的方法也会有所不同。在[这篇](https://www.geeksforgeeks.org/repeated-subsequence-length-2/)文章中讨论了检查一个字符串是否包含两个长度为两个或更多的重复子序列的方法。