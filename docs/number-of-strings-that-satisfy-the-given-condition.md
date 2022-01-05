# 满足给定条件的字符串数量

> 原文:[https://www . geesforgeks . org/满足给定条件的字符串数/](https://www.geeksforgeeks.org/number-of-strings-that-satisfy-the-given-condition/)

给定相等长度的 N 根弦。字符串只包含数字(1 到 9)。任务是计算具有索引位置的字符串的数量，使得该索引位置的数字大于所有其他字符串的相同索引位置的数字。
**例:**

> **输入:**arr[]= {“223”、“232”、“112”}
> **输出:**2
> 1<sup>ST</sup>和 2 <sup>nd</sup> 的第一位数字最大。
> 字符串 2 的第二个数字<sup>和</sup>最大。
> 字符串 1 的第三位数字 <sup>st</sup> 最大。
> **输入:**arr[]= {“999”、“122”、“111”}
> **输出:** 1

**方法:**对于每个索引位置，在所有字符串中找到该位置的最大数字。并将满足给定条件的字符串的索引存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，以便同一字符串不会在不同的索引位置被计数两次。最后，返回集合的大小。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid strings
int countStrings(int n, int m, string s[])
{

    // Set to store indices of valid strings
    unordered_set<int> ind;
    for (int j = 0; j < m; j++) {
        int mx = 0;

        // Find the maximum digit for current position
        for (int i = 0; i < n; i++)
            mx = max(mx, (int)s[i][j] - '0');

        // Add indices of all the strings in the set
        // that contain maximal digit
        for (int i = 0; i < n; i++)
            if (s[i][j] - '0' == mx)
                ind.insert(i);
    }

    // Return number of strings in the set
    return ind.size();
}

// Driver code
int main()
{
    string s[] = { "223", "232", "112" };
    int m = s[0].length();
    int n = sizeof(s) / sizeof(s[0]);
    cout << countStrings(n, m, s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GfG
{

// Function to return the count of valid strings
static int countStrings(int n, int m, String s[])
{

    // Set to store indices of valid strings
    HashSet<Integer> ind = new HashSet<Integer>();
    for (int j = 0; j < m; j++)
    {
        int mx = 0;

        // Find the maximum digit for current position
        for (int i = 0; i < n; i++)
            mx = Math.max(mx, (int)(s[i].charAt(j) - '0'));

        // Add indices of all the strings in the set
        // that contain maximal digit
        for (int i = 0; i < n; i++)
            if (s[i].charAt(j) - '0' == mx)
                ind.add(i);
    }

    // Return number of strings in the set
    return ind.size();
}

// Driver code
public static void main(String[] args)
{
    String s[] = { "223", "232", "112" };
    int m = s[0].length();
    int n = s.length;
    System.out.println(countStrings(n, m, s));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# valid strings
def countStrings(n, m, s):

    # Set to store indices of
    # valid strings
    ind = dict()
    for j in range(m):
        mx = 0

        str1 = s[j]

        # Find the maximum digit for
        # current position
        for i in range(n):
            mx = max(mx, int(str1[i]))

        # Add indices of all the strings in
        # the set that contain maximal digit
        for i in range(n):
            if int(str1[i]) == mx:
                ind[i] = 1

    # Return number of strings
    # in the set
    return len(ind)

# Driver code
s = ["223", "232", "112"]
m = len(s[0])
n = len(s)
print(countStrings(n, m, s))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GfG
{

// Function to return the count of valid strings
static int countStrings(int n, int m, String[] s)
{

    // Set to store indices of valid strings
    HashSet<int> ind = new HashSet<int>();
    for (int j = 0; j < m; j++)
    {
        int mx = 0;

        // Find the maximum digit for current position
        for (int i = 0; i < n; i++)
            mx = Math.Max(mx, (int)(s[i][j] - '0'));

        // Add indices of all the strings in the set
        // that contain maximal digit
        for (int i = 0; i < n; i++)
            if (s[i][j] - '0' == mx)
                ind.Add(i);
    }

    // Return number of strings in the set
    return ind.Count;
}

// Driver code
public static void Main()
{
    String []s = { "223", "232", "112" };
    int m = s[0].Length;
    int n = s.Length;
    Console.WriteLine(countStrings(n, m, s));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of valid strings
function countStrings(n,m,s)
{
    // Set to store indices of valid strings
    let ind = new Set();
    for (let j = 0; j < m; j++)
    {
        let mx = 0;

        // Find the maximum digit for current position
        for (let i = 0; i < n; i++)
            mx = Math.max(mx, (s[i][j].charCodeAt(0) -
            '0'.charCodeAt(0)));

        // Add indices of all the strings in the set
        // that contain maximal digit
        for (let i = 0; i < n; i++)
            if (s[i][j].charCodeAt(0) - '0'.charCodeAt(0) == mx)
                ind.add(i);
    }

    // Return number of strings in the set
    return ind.size;
}

// Driver code
let s=[ "223", "232", "112"];
let m = s[0].length;
let n = s.length;
document.write(countStrings(n, m, s));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N * M)，其中 N 为字符串的个数，M 为字符串的长度。