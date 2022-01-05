# 打印最长公共子序列|集合 2(全部打印)

> 原文:[https://www . geesforgeks . org/printing-最长-公共-子序列-set-2-printing/](https://www.geeksforgeeks.org/printing-longest-common-subsequence-set-2-printing/)

给定两个序列，打印两个序列中所有最长的子序列。
**例:**

```
Input: 
string X = "AGTGATG"
string Y = "GTTAG"
Output: 
GTAG
GTTG

Input: 
string X = "AATCC"
string Y = "ACACG"
Output:  
ACC
AAC

Input: 
string X = "ABCBDAB"
string Y = "BDCABA"
Output:  
BCAB
BCBA
BDAB
```

我们在这里讨论了最长公共子序列(LCS)问题。那里讨论的函数主要是求 LCS 的长度。我们还讨论了如何打印最长的子序列[这里](https://www.geeksforgeeks.org/printing-longest-common-subsequence/)。但是由于 LCS 对于两个字符串并不是唯一的，在这篇文章中我们将打印出 LCS 问题的所有可能的解决方案。
下面是打印全 LCS 的详细算法。
我们构建 L[m+1][n+1]表，如[之前的](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)帖子中所述，并从 L[m][n]开始遍历 2D 阵列。对于矩阵中的当前单元格 L[i][j]，
a)如果 X 和 Y 的最后一个字符相同(即 X[i-1] == Y[j-1])，则该字符必须出现在子串 X[0…i-1]和 Y[0]的所有 LCS 中..j-1]。我们简单地在矩阵中递归 L[i-1][j-1]，并将当前字符附加到子串 X[0…i-2]和 Y[0]的所有 LCS 可能值上..j-2]。
b)如果 X 和 Y 的最后一个字符不相同(即 X[i-1]！= Y[j-1])，那么根据哪个值更大，可以从矩阵的顶部(即 L[i-1][j])或从矩阵的左侧(即 L[i][j-1])构造 LCS。如果两个值相等(即 L[i-1][j] == L[i][j-1])，则从矩阵的两边构造。所以基于 L[i-1][j]和 L[i][j-1]的值，我们往更大值的方向走，或者如果值相等，往两个方向走。
以下是上述思想的递归实现–

## C++

```
/* Dynamic Programming implementation of LCS problem */
#include <bits/stdc++.h>
using namespace std;

// Maximum string length
#define N 100

int L[N][N];

/* Returns set containing all LCS for X[0..m-1], Y[0..n-1] */
set<string> findLCS(string X, string Y, int m, int n)
{
    // construct a set to store possible LCS
    set<string> s;

    // If we reaches end of either string, return
    // a empty set
    if (m == 0 || n == 0)
    {
        s.insert("");
        return s;
    }

    // If the last characters of X and Y are same
    if (X[m - 1] == Y[n - 1])
    {
        // recurse for X[0..m-2] and Y[0..n-2] in
        // the matrix
        set<string> tmp = findLCS(X, Y, m - 1, n - 1);

        // append current character to all possible LCS
        // of substring X[0..m-2] and Y[0..n-2].
        for (string str : tmp)
            s.insert(str + X[m - 1]);
    }

    // If the last characters of X and Y are not same
    else
    {
        // If LCS can be constructed from top side of
        // the matrix, recurse for X[0..m-2] and Y[0..n-1]
        if (L[m - 1][n] >= L[m][n - 1])
            s = findLCS(X, Y, m - 1, n);

        // If LCS can be constructed from left side of
        // the matrix, recurse for X[0..m-1] and Y[0..n-2]
        if (L[m][n - 1] >= L[m - 1][n])
        {
            set<string> tmp = findLCS(X, Y, m, n - 1);

            // merge two sets if L[m-1][n] == L[m][n-1]
            // Note s will be empty if L[m-1][n] != L[m][n-1]
            s.insert(tmp.begin(), tmp.end());
        }
    }
    return s;
}

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int LCS(string X, string Y, int m, int n)
{
    // Build L[m+1][n+1] in bottom up fashion
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;
            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }
    return L[m][n];
}

/* Driver program to test above function */
int main()
{
    string X = "AGTGATG";
    string Y = "GTTAG";
    int m = X.length();
    int n = Y.length();

    cout << "LCS length is " << LCS(X, Y, m, n) << endl;

    set<string> s = findLCS(X, Y, m, n);

    for (string str : s)
        cout << str << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming implementation of LCS problem */
import java.util.*;
class GFG
{

// Maximum String length
static int N = 100;

static int [][]L = new int[N][N];

/* Returns set containing all LCS for
   X[0..m-1], Y[0..n-1] */
static Set<String> findLCS(String X,
                           String Y, int m, int n)
{
    // construct a set to store possible LCS
    Set<String> s = new HashSet<>();

    // If we reaches end of either String,
    // return a empty set
    if (m == 0 || n == 0)
    {
        s.add("");
        return s;
    }

    // If the last characters of X and Y are same
    if (X.charAt(m - 1) == Y.charAt(n - 1))
    {
        // recurse for X[0..m-2] and Y[0..n-2]
        // in the matrix
        Set<String> tmp = findLCS(X, Y, m - 1, n - 1);

        // append current character to all possible LCS
        // of subString X[0..m-2] and Y[0..n-2].
        for (String str : tmp)
            s.add(str + X.charAt(m - 1));
    }

    // If the last characters of X and Y are not same
    else
    {
        // If LCS can be constructed from top side of
        // the matrix, recurse for X[0..m-2] and Y[0..n-1]
        if (L[m - 1][n] >= L[m][n - 1])
            s = findLCS(X, Y, m - 1, n);

        // If LCS can be constructed from left side of
        // the matrix, recurse for X[0..m-1] and Y[0..n-2]
        if (L[m][n - 1] >= L[m - 1][n])
        {
            Set<String> tmp = findLCS(X, Y, m, n - 1);

            // merge two sets if L[m-1][n] == L[m][n-1]
            // Note s will be empty if L[m-1][n] != L[m][n-1]
            s.addAll(tmp);
        }
    }
    return s;
}

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
static int LCS(String X, String Y, int m, int n)
{
    // Build L[m+1][n+1] in bottom up fashion
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X.charAt(i - 1) == Y.charAt(j - 1))
                L[i][j] = L[i - 1][j - 1] + 1;
            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }
    return L[m][n];
}

// Driver Code
public static void main(String[] args)
{
    String X = "AGTGATG";
    String Y = "GTTAG";
    int m = X.length();
    int n = Y.length();

    System.out.println("LCS length is " +
                        LCS(X, Y, m, n));

    Set<String> s = findLCS(X, Y, m, n);

    for (String str : s)
        System.out.println(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Dynamic Programming implementation of LCS problem

# Maximum string length
N = 100
L = [[0 for i in range(N)]
        for j in range(N)]

# Returns set containing all LCS
# for X[0..m-1], Y[0..n-1]
def findLCS(x, y, m, n):

    # construct a set to store possible LCS
    s = set()

    # If we reaches end of either string, return
    # a empty set
    if m == 0 or n == 0:
        s.add("")
        return s

    # If the last characters of X and Y are same
    if x[m - 1] == y[n - 1]:

        # recurse for X[0..m-2] and Y[0..n-2] in
        # the matrix
        tmp = findLCS(x, y, m - 1, n - 1)

        # append current character to all possible LCS
        # of substring X[0..m-2] and Y[0..n-2].
        for string in tmp:
            s.add(string + x[m - 1])

    # If the last characters of X and Y are not same
    else:

        # If LCS can be constructed from top side of
        # the matrix, recurse for X[0..m-2] and Y[0..n-1]
        if L[m - 1][n] >= L[m][n - 1]:
            s = findLCS(x, y, m - 1, n)

        # If LCS can be constructed from left side of
        # the matrix, recurse for X[0..m-1] and Y[0..n-2]
        if L[m][n - 1] >= L[m - 1][n]:
            tmp = findLCS(x, y, m, n - 1)

            # merge two sets if L[m-1][n] == L[m][n-1]
            # Note s will be empty if L[m-1][n] != L[m][n-1]
            for i in tmp:
                s.add(i)
    return s

# Returns length of LCS for X[0..m-1], Y[0..n-1]
def LCS(x, y, m, n):

    # Build L[m+1][n+1] in bottom up fashion
    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0 or j == 0:
                L[i][j] = 0
            elif x[i - 1] == y[j - 1]:
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])
    return L[m][n]

# Driver Code
if __name__ == "__main__":
    x = "AGTGATG"
    y = "GTTAG"
    m = len(x)
    n = len(y)

    print("LCS length is", LCS(x, y, m, n))

    s = findLCS(x, y, m, n)

    for i in s:
        print(i)

# This code is contributed by
# sanjeev2552
```

## C#

```
// Dynamic Programming implementation
// of LCS problem
using System;
using System.Collections.Generic;

class GFG
{

// Maximum String length
static int N = 100;

static int [,]L = new int[N, N];

/* Returns set containing all LCS for
X[0..m-1], Y[0..n-1] */
static HashSet<String> findLCS(String X,
                               String Y,
                               int m, int n)
{
    // construct a set to store possible LCS
    HashSet<String> s = new HashSet<String>();

    // If we reaches end of either String,
    // return a empty set
    if (m == 0 || n == 0)
    {
        s.Add("");
        return s;
    }

    // If the last characters of X and Y are same
    if (X[m - 1] == Y[n - 1])
    {
        // recurse for X[0..m-2] and Y[0..n-2]
        // in the matrix
        HashSet<String> tmp = findLCS(X, Y, m - 1, n - 1);

        // append current character to all possible LCS
        // of subString X[0..m-2] and Y[0..n-2].
        foreach (String str in tmp)
            s.Add(str + X[m - 1]);
    }

    // If the last characters of X and Y are not same
    else
    {
        // If LCS can be constructed from top side of
        // the matrix, recurse for X[0..m-2] and Y[0..n-1]
        if (L[m - 1, n] >= L[m, n - 1])
            s = findLCS(X, Y, m - 1, n);

        // If LCS can be constructed from left side of
        // the matrix, recurse for X[0..m-1] and Y[0..n-2]
        if (L[m, n - 1] >= L[m - 1, n])
        {
            HashSet<String> tmp = findLCS(X, Y, m, n - 1);

            // merge two sets if L[m-1,n] == L[m,n-1]
            // Note s will be empty if L[m-1,n] != L[m,n-1]
            foreach (String str in tmp)
                s.Add(str);
        }
    }
    return s;
}

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
static int LCS(String X, String Y, int m, int n)
{
    // Build L[m+1,n+1] in bottom up fashion
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i, j] = 0;
            else if (X[i - 1] == Y[j - 1])
                L[i, j] = L[i - 1, j - 1] + 1;
            else
                L[i, j] = Math.Max(L[i - 1, j],
                                   L[i, j - 1]);
        }
    }
    return L[m, n];
}

// Driver Code
public static void Main(String[] args)
{
    String X = "AGTGATG";
    String Y = "GTTAG";
    int m = X.Length;
    int n = Y.Length;

    Console.WriteLine("LCS length is " +
                       LCS(X, Y, m, n));

    HashSet<String> s = findLCS(X, Y, m, n);

    foreach (String str in s)
        Console.WriteLine(str);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

/* Dynamic Programming implementation of LCS problem */

// Maximum String length
let N = 100;
let L = new Array(N);
for(let i=0;i<N;i++)
{
    L[i]=new Array(N);

}

/* Returns set containing all LCS for
   X[0..m-1], Y[0..n-1] */
function findLCS(X,Y,m,n)
{
    // construct a set to store possible LCS
    let s = new Set();

    // If we reaches end of either String,
    // return a empty set
    if (m == 0 || n == 0)
    {
        s.add("");
        return s;
    }

    // If the last characters of X and Y are same
    if (X[m-1] == Y[n-1])
    {
        // recurse for X[0..m-2] and Y[0..n-2]
        // in the matrix
        let tmp = findLCS(X, Y, m - 1, n - 1);

        // append current character to all possible LCS
        // of subString X[0..m-2] and Y[0..n-2].
        for (let str of tmp.values())
            s.add(str + X[m-1]);
    }

    // If the last characters of X and Y are not same
    else
    {
        // If LCS can be constructed from top side of
        // the matrix, recurse for X[0..m-2] and Y[0..n-1]
        if (L[m - 1][n] >= L[m][n - 1])
            s = findLCS(X, Y, m - 1, n);

        // If LCS can be constructed from left side of
        // the matrix, recurse for X[0..m-1] and Y[0..n-2]
        if (L[m][n - 1] >= L[m - 1][n])
        {
            let tmp = findLCS(X, Y, m, n - 1);

            // merge two sets if L[m-1][n] == L[m][n-1]
            // Note s will be empty if L[m-1][n] != L[m][n-1]

            for (let item of tmp.values())
                s.add(item)
        }
    }
    return s;
}

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
function LCS(X,Y,m,n)
{
    // Build L[m+1][n+1] in bottom up fashion
    for (let i = 0; i <= m; i++)
    {
        for (let j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i - 1][j - 1] + 1;
            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }
    return L[m][n];
}

// Driver Code
let X = "AGTGATG";
let Y = "GTTAG";
let m = X.length;
let n = Y.length;

document.write("LCS length is " +
                   LCS(X, Y, m, n)+"<br>");

let s = findLCS(X, Y, m, n);

for (let str of s.values())
    document.write(str+"<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
LCS length is 4
GTAG
GTTG
```

参考资料:[维基图书–阅读所有 LCS](https://en.wikibooks.org/wiki/Algorithm_Implementation/Strings/Longest_common_subsequence#Reading_out_all_LCSs)
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。