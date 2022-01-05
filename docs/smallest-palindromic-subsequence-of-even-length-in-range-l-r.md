# 范围[L，R]

内偶数长度的最小回文子序列

> 原文:[https://www . geesforgeks . org/minist-回文-范围内偶长度子序列-l-r/](https://www.geeksforgeeks.org/smallest-palindromic-subsequence-of-even-length-in-range-l-r/)

给定一串大小为 **N** 的字符串和一些查询，任务是为每个查询找到范围为**【L，R】**的偶数长度的字典最小回文子序列。如果不存在这样的回文子序列，则打印 **-1** 。
**示例:**

> **输入:** str = "dbdeke "，query[][] = {{0，5}，{1，5}，{1，3}}
> **输出:** dd
> ee
> -1
> **解释:** dd
> 在第一次查询中，可能的回文子序列是“dd”、“ee”、“ddee”和“dd”，它们在字典上是最小的。
> 在第二个查询中，唯一可能的回文子序列是“ee”。
> 在第三个查询中，不可能有这样的回文子序列。
> **输入:** str = "abcd "，查询[][] = {{0，3}}
> **输出:** -1

**方法:**这个问题的主要观察是如果存在回文子序列，那么它一定是**长度> 2** 。因此，结果子序列将是一串具有相同字符的**长度> 2** 。在**【L，R】**范围内频率大于 **1** 的字符中选择最小的字符，并打印该字符两次。如果不存在这样的字符，则打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ program to find lexicographically smallest
// palindromic subsequence of even length

#include <bits/stdc++.h>
using namespace std;
const int N = 100001;

// Frequency array for each character
int f[26][N];

// Preprocess the frequency array calculation
void precompute(string s, int n)
{
    // Frequency array to track each character
    // in position 'i'
    for (int i = 0; i < n; i++) {
        f[s[i] - 'a'][i]++;
    }

    // Calculating prefix sum
    // over this frequency array
    // to get frequency of a character
    // in a range [L, R].
    for (int i = 0; i < 26; i++) {
        for (int j = 1; j < n; j++) {
            f[i][j] += f[i][j - 1];
        }
    }
}

// Util function for palindromic subsequences
int palindromicSubsequencesUtil(int L, int R)
{

    int c, ok = 0;

    // Find frequency of all characters
    for (int i = 0; i < 26; i++) {

        // For each character
        // find it's frequency
        // in range [L, R]
        int cnt = f[i][R];
        if (L > 0)
            cnt -= f[i][L - 1];

        if (cnt > 1) {

            // If frequency in this range is > 1,
            // then we must take this character,
            // as it will give
            // lexicographically smallest one
            ok = 1;
            c = i;
            break;
        }
    }

    // There is no character
    // in range [L, R] such
    // that it's frequency is > 1.
    if (ok == 0) {

        return -1;
    }

    // Return the character's value
    return c;
}

// Function to find lexicographically smallest
// palindromic subsequence of even length
void palindromicSubsequences(int Q[][2], int l)
{
    for (int i = 0; i < l; i++) {

        // Find in the palindromic subsequences
        int x
            = palindromicSubsequencesUtil(
                Q[i][0], Q[i][1]);

        // No such subsequence exists
        if (x == -1) {
            cout << -1 << "\n";
        }
        else {
            char c = 'a' + x;
            cout << c << c << "\n";
        }
    }
}

// Driver Code
int main()
{
    string str = "dbdeke";
    int Q[][2] = { { 0, 5 },
                   { 1, 5 },
                   { 1, 3 } };
    int n = str.size();
    int l = sizeof(Q) / sizeof(Q[0]);

    // Function calls
    precompute(str, n);

    palindromicSubsequences(Q, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographically smallest
// palindromic subsequence of even length
import java.util.*;

class GFG{
static int N = 100001;

// Frequency array for each character
static int [][]f = new int[26][N];

// Preprocess the frequency array calculation
static void precompute(String s, int n)
{
    // Frequency array to track each character
    // in position 'i'
    for (int i = 0; i < n; i++)
    {
        f[s.charAt(i) - 'a'][i]++;
    }

    // Calculating prefix sum
    // over this frequency array
    // to get frequency of a character
    // in a range [L, R].
    for (int i = 0; i < 26; i++)
    {
        for (int j = 1; j < n; j++)
        {
            f[i][j] += f[i][j - 1];
        }
    }
}

// Util function for palindromic subsequences
static int palindromicSubsequencesUtil(int L, int R)
{
    int c = 0, ok = 0;

    // Find frequency of all characters
    for (int i = 0; i < 26; i++)
    {

        // For each character
        // find it's frequency
        // in range [L, R]
        int cnt = f[i][R];
        if (L > 0)
            cnt -= f[i][L - 1];

        if (cnt > 1)
        {

            // If frequency in this range is > 1,
            // then we must take this character,
            // as it will give
            // lexicographically smallest one
            ok = 1;
            c = i;
            break;
        }
    }

    // There is no character
    // in range [L, R] such
    // that it's frequency is > 1.
    if (ok == 0)
    {
        return -1;
    }

    // Return the character's value
    return c;
}

// Function to find lexicographically smallest
// palindromic subsequence of even length
static void palindromicSubsequences(int Q[][], int l)
{
    for (int i = 0; i < l; i++)
    {

        // Find in the palindromic subsequences
        int x = palindromicSubsequencesUtil(
                           Q[i][0], Q[i][1]);

        // No such subsequence exists
        if (x == -1)
        {
            System.out.print(-1 + "\n");
        }
        else
        {
            char c = (char) ('a' + x);
            System.out.print((char) c + "" +
                             (char) c + "\n");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "dbdeke";
    int Q[][] = { { 0, 5 },
                  { 1, 5 },
                  { 1, 3 } };
    int n = str.length();
    int l = Q.length;

    // Function calls
    precompute(str, n);

    palindromicSubsequences(Q, l);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find lexicographically
# smallest palindromic subsequence of even length
N = 100001

# Frequency array for each character
f = [[ 0 for x in range (N)]
         for y in range (26)]

# Preprocess the frequency array calculation
def precompute(s, n):

    # Frequency array to track each character
    # in position 'i'
    for i in range(n):
        f[ord(s[i]) - ord('a')][i] += 1

    # Calculating prefix sum
    # over this frequency array
    # to get frequency of a character
    # in a range [L, R].
    for i in range(26):
        for j in range(1, n):
            f[i][j] += f[i][j - 1]

# Util function for palindromic subsequences
def palindromicSubsequencesUtil(L, R):

    ok = 0

    # Find frequency of all characters
    for i in range(26):

        # For each character
        # find it's frequency
        # in range [L, R]
        cnt = f[i][R]
        if (L > 0):
            cnt -= f[i][L - 1]

        if (cnt > 1):

            # If frequency in this range is > 1,
            # then we must take this character,
            # as it will give
            # lexicographically smallest one
            ok = 1
            c = i
            break

    # There is no character
    # in range [L, R] such
    # that it's frequency is > 1.
    if (ok == 0):
        return -1

    # Return the character's value
    return c

# Function to find lexicographically smallest
# palindromic subsequence of even length
def palindromicSubsequences(Q, l):

    for i in range(l):

        # Find in the palindromic subsequences
        x = palindromicSubsequencesUtil(Q[i][0],
                                        Q[i][1])

        # No such subsequence exists
        if (x == -1):
            print(-1)

        else :
            c = ord('a') + x
            print(2 * chr(c))

# Driver Code
if __name__ == "__main__":

    st = "dbdeke"
    Q = [ [ 0, 5 ],
          [ 1, 5 ],
          [ 1, 3 ] ]

    n = len(st)
    l = len(Q)

    # Function calls
    precompute(st, n)

    palindromicSubsequences(Q, l)

# This code is contributed by chitranayal   
```

## C#

```
// C# program to find lexicographically smallest
// palindromic subsequence of even length
using System;

class GFG{

static int N = 100001;

// Frequency array for each character
static int [,]f = new int[26, N];

// Preprocess the frequency array calculation
static void precompute(String s, int n)
{

    // Frequency array to track each character
    // in position 'i'
    for(int i = 0; i < n; i++)
    {
        f[s[i] - 'a', i]++;
    }

    // Calculating prefix sum
    // over this frequency array
    // to get frequency of a character
    // in a range [L, R].
    for(int i = 0; i < 26; i++)
    {
        for(int j = 1; j < n; j++)
        {
            f[i, j] += f[i, j - 1];
        }
    }
}

// Util function for palindromic subsequences
static int palindromicSubsequencesUtil(int L, int R)
{
    int c = 0, ok = 0;

    // Find frequency of all characters
    for(int i = 0; i < 26; i++)
    {

        // For each character
        // find it's frequency
        // in range [L, R]
        int cnt = f[i, R];
        if (L > 0)
            cnt -= f[i, L - 1];

        if (cnt > 1)
        {

            // If frequency in this range is > 1,
            // then we must take this character,
            // as it will give
            // lexicographically smallest one
            ok = 1;
            c = i;
            break;
        }
    }

    // There is no character
    // in range [L, R] such
    // that it's frequency is > 1.
    if (ok == 0)
    {
        return -1;
    }

    // Return the character's value
    return c;
}

// Function to find lexicographically smallest
// palindromic subsequence of even length
static void palindromicSubsequences(int [,]Q, int l)
{
    for(int i = 0; i < l; i++)
    {

        // Find in the palindromic subsequences
        int x = palindromicSubsequencesUtil(Q[i, 0],
                                            Q[i, 1]);

        // No such subsequence exists
        if (x == -1)
        {
            Console.Write(-1 + "\n");
        }
        else
        {
            char c = (char)('a' + x);
            Console.Write((char) c + "" +
                          (char) c + "\n");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str = "dbdeke";
    int [,]Q = { { 0, 5 },
                 { 1, 5 },
                 { 1, 3 } };
    int n = str.Length;
    int l = Q.GetLength(0);

    // Function calls
    precompute(str, n);

    palindromicSubsequences(Q, l);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to find lexicographically smallest
// palindromic subsequence of even length
var N = 100001;

// Frequency array for each character
var f = Array.from(Array(26), ()=> Array(N).fill(0));

// Preprocess the frequency array calculation
function precompute(s, n)
{
    // Frequency array to track each character
    // in position 'i'
    for (var i = 0; i < n; i++) {
        f[s[i].charCodeAt(0) - 'a'.charCodeAt(0)][i]++;
    }

    // Calculating prefix sum
    // over this frequency array
    // to get frequency of a character
    // in a range [L, R].
    for (var i = 0; i < 26; i++) {
        for (var j = 1; j < n; j++) {
            f[i][j] += f[i][j - 1];
        }
    }
}

// Util function for palindromic subsequences
function palindromicSubsequencesUtil(L, R)
{

    var c, ok = 0;

    // Find frequency of all characters
    for (var i = 0; i < 26; i++) {

        // For each character
        // find it's frequency
        // in range [L, R]
        var cnt = f[i][R];
        if (L > 0)
            cnt -= f[i][L - 1];

        if (cnt > 1) {

            // If frequency in this range is > 1,
            // then we must take this character,
            // as it will give
            // lexicographically smallest one
            ok = 1;
            c = i;
            break;
        }
    }

    // There is no character
    // in range [L, R] such
    // that it's frequency is > 1.
    if (ok == 0) {

        return -1;
    }

    // Return the character's value
    return c;
}

// Function to find lexicographically smallest
// palindromic subsequence of even length
function palindromicSubsequences(Q, l)
{
    for (var i = 0; i < l; i++) {

        // Find in the palindromic subsequences
        var x
            = palindromicSubsequencesUtil(
                Q[i][0], Q[i][1]);

        // No such subsequence exists
        if (x == -1) {
            document.write( -1 + "<br>");
        }
        else {
            var c = String.fromCharCode('a'.charCodeAt(0) + x);
            document.write( c + c + "<br>");
        }
    }
}

// Driver Code
var str = "dbdeke";
var Q = [ [ 0, 5 ],
               [ 1, 5 ],
               [ 1, 3 ] ];
var n = str.length;
var l = Q.length;

// Function calls
precompute(str, n);
palindromicSubsequences(Q, l);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
dd
ee
-1
```

***时间复杂度:** O(26 * N + 26 * Q)，其中 N 为弦的长度*