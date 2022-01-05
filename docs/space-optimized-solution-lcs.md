# LCS 的一个空间优化解

> 原文:[https://www.geeksforgeeks.org/space-optimized-solution-lcs/](https://www.geeksforgeeks.org/space-optimized-solution-lcs/)

给定两个字符串，找出两个字符串中最长子序列的长度。

**示例:**

```
LCS for input Sequences “ABCDGH” and “AEDFHR” is “ADH” of length 3. 
LCS for input Sequences “AGGTAB” and “GXTXAYB” is “GTAB” of length 4.
```

我们已经讨论了 LCS 典型的基于动态规划的解决方案。我们可以优化 LCS 问题所使用的空间。我们知道 LCS 问题的重现关系是

## 卡片打印处理机（Card Print Processor 的缩写）

```
/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs(string &X, string &Y)
{
    int m = X.length(), n = Y.length();
    int L[m+1][n+1];

    /* Following steps build L[m+1][n+1] in bottom up
       fashion. Note that L[i][j] contains length of
       LCS of X[0..i-1] and Y[0..j-1] */
    for (int i=0; i<=m; i++)
    {
        for (int j=0; j<=n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;

            else
                L[i][j] = max(L[i-1][j], L[i][j-1]);
        }
    }

    /* L[m][n] contains length of LCS for X[0..n-1] and
       Y[0..m-1] */
    return L[m][n];
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // Returns length of LCS for X[0..m-1], Y[0..n-1]

    public static int lcs(String X, String Y)
    {

        // Find lengths of two strings
        int m = X.length(), n = Y.length();

        int L[][] = new int[m + 1][n + 1];

        /* Following steps build L[m+1][n+1] in bottom up
        fashion. Note that L[i][j] contains length of
        LCS of X[0..i-1] and Y[0..j-1] */

        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    L[i][j] = 0;

                else if (X[i - 1] == Y[j - 1])
                    L[i][j] = L[i - 1][j - 1] + 1;

                else
                    L[i][j] = max(L[i - 1][j], L[i][j - 1]);
            }
        }

        /* L[m][n] contains length of LCS for X[0..n-1] and
           Y[0..m-1] */
        return L[m][n];
    }
}

// This code is contributed by rajsanghavi9.
```

## java 描述语言

```
<script>

// Dynamic Programming Java implementation of LCS problem

// Utility function to get max of 2 integers
function max(a, b)
{
    if (a > b)
        return a;
    else
        return b;
}

// Returns length of LCS for X[0..m-1], Y[0..n-1]
function lcs(X, Y, m, n)
{
    var L = new Array(m + 1);
    for(var i = 0; i < L.length; i++)
    {
        L[i] = new Array(n + 1);
    }
    var i, j;

    /* Following steps build L[m+1][n+1] in
    bottom up fashion. Note that L[i][j]
    contains length of LCS of X[0..i-1]
    and Y[0..j-1] */
    for(i = 0; i <= m; i++)
    {
        for(j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;
            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    /* L[m][n] contains length of LCS
    for X[0..n-1] and Y[0..m-1] */
    return L[m][n];
}

// This code is contributed by akshitsaxenaa09.
</script>
```

**如何求 LCS 的长度是 O(n)辅助空间？**

[**我们强烈建议您点击此处进行练习，然后再进入解决方案。**](https://practice.geeksforgeeks.org/problems/longest-common-subsequence-1587115620/1)
在上面的简单实现中，一个重要的观察是，在外环的每次迭代中，我们只需要来自前一行的所有列的**值。所以不需要在我们的 DP 矩阵中存储所有的行，我们可以一次只存储两行并使用它们。这样，已用空间将从 L[m+1][n+1]减少到 L[2][n+1]。以下是上述想法的实现。**

## C++

```
// Space optimized C++ implementation
// of LCS problem
#include<bits/stdc++.h>
using namespace std;

// Returns length of LCS
// for X[0..m-1], Y[0..n-1]
int lcs(string &X, string &Y)
{

    // Find lengths of two strings
    int m = X.length(), n = Y.length();

    int L[2][n + 1];

    // Binary index, used to
    // index current row and
    // previous row.
    bool bi;

    for (int i = 0; i <= m; i++)
    {

        // Compute current
        // binary index
        bi = i & 1;

        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[bi][j] = 0;

            else if (X[i-1] == Y[j-1])
                 L[bi][j] = L[1 - bi][j - 1] + 1;

            else
                L[bi][j] = max(L[1 - bi][j],
                               L[bi][j - 1]);
        }
    }

    // Last filled entry contains
    // length of LCS
    // for X[0..n-1] and Y[0..m-1]
    return L[bi][n];
}

// Driver code
int main()
{
    string X = "AGGTAB";
    string Y = "GXTXAYB";

    printf("Length of LCS is %d\n", lcs(X, Y));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for A Space Optimized
// Solution of LCS

class GFG {

    // Returns length of LCS
    // for X[0..m - 1],
    // Y[0..n - 1]
    public static int lcs(String X,
                          String Y)
    {

        // Find lengths of two strings
        int m = X.length(), n = Y.length();

        int L[][] = new int[2][n+1];

        // Binary index, used to index
        // current row and previous row.
        int bi=0;

        for (int i = 0; i <= m; i++)
        {

            // Compute current binary index
            bi = i & 1;

            for (int j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[bi][j] = 0;

                else if (X.charAt(i - 1) ==
                         Y.charAt(j - 1))
                    L[bi][j] = L[1 - bi][j - 1] + 1;

                else
                    L[bi][j] = Math.max(L[1 - bi][j],
                                        L[bi][j - 1]);
            }
        }

        // Last filled entry contains length of
        // LCS for X[0..n-1] and Y[0..m-1]
        return L[bi][n];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";

        System.out.println("Length of LCS is " +
                                    lcs(X, Y));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Space optimized Python
# implementation of LCS problem

# Returns length of LCS for
# X[0..m-1], Y[0..n-1]
def lcs(X, Y):

    # Find lengths of two strings
    m = len(X)
    n = len(Y)

    L = [[0 for i in range(n+1)] for j in range(2)]

    # Binary index, used to index current row and
    # previous row.
    bi = bool

    for i in range(m):
        # Compute current binary index
        bi = i&1

        for j in range(n+1):
            if (i == 0 or j == 0):
                L[bi][j] = 0

            elif (X[i] == Y[j - 1]):
                L[bi][j] = L[1 - bi][j - 1] + 1

            else:
                L[bi][j] = max(L[1 - bi][j],
                               L[bi][j - 1])

    # Last filled entry contains length of LCS
    # for X[0..n-1] and Y[0..m-1]
    return L[bi][n]

# Driver Code
X = "AGGTAB"
Y = "GXTXAYB"

print("Length of LCS is", lcs(X, Y))

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# Code for A Space
// Optimized Solution of LCS
using System;

class GFG
{

    // Returns length of LCS
    // for X[0..m - 1],
    // Y[0..n - 1]
    public static int lcs(string X,
                          string Y)
    {

        // Find lengths of
        // two strings
        int m = X.Length, n = Y.Length;

        int [,]L = new int[2, n + 1];

        // Binary index, used to
        // index current row and
        // previous row.
        int bi = 0;

        for (int i = 0; i <= m; i++)
        {

            // Compute current
            // binary index
            bi = i & 1;

            for (int j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[bi, j] = 0;

                else if (X[i - 1] == Y[j - 1])
                    L[bi, j] = L[1 - bi,
                                 j - 1] + 1;

                else
                    L[bi, j] = Math.Max(L[1 - bi, j],
                                        L[bi, j - 1]);
            }
        }

        // Last filled entry contains
        // length of LCS for X[0..n-1]
        // and Y[0..m-1]
        return L[bi, n];
    }

    // Driver Code
    public static void Main()
    {
        string X = "AGGTAB";
        string Y = "GXTXAYB";

        Console.Write("Length of LCS is " +
                                lcs(X, Y));
    }
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Space optimized PHP implementation
// of LCS problem

// Returns length of LCS
// for X[0..m-1], Y[0..n-1]
function lcs($X, $Y)
{

    // Find lengths of two strings
    $m = strlen($X);
    $n = strlen($Y);

    $L = array(array());

    // Binary index, used to index
    // current row and previous row.
    for ($i = 0; $i <= $m; $i++)
    {

        // Compute current binary index
        $bi = $i & 1;

        for ($j = 0; $j <= $n; $j++)
        {
            if ($i == 0 || $j == 0)
                $L[$bi][$j] = 0;

            else if ($X[$i - 1] == $Y[$j - 1])
                $L[$bi][$j] = $L[1 - $bi][$j - 1] + 1;

            else
                $L[$bi][$j] = max($L[1 - $bi][$j],
                                  $L[$bi][$j - 1]);
        }
    }

    // Last filled entry contains
    // length of LCS
    // for X[0..n-1] and Y[0..m-1]
    return $L[$bi][$n];
}

// Driver code
$X = "AGGTAB";
$Y = "GXTXAYB";

echo "Length of LCS is : ",
               lcs($X, $Y);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript Code for A Space Optimized Solution of LCS

    // Returns length of LCS
    // for X[0..m - 1],
    // Y[0..n - 1]
    function lcs(X, Y)
    {

        // Find lengths of two strings
        let m = X.length, n = Y.length;

        let L = new Array(2);
        for (let i = 0; i < 2; i++)
        {
            L[i] = new Array(n + 1);
            for (let j = 0; j < n + 1; j++)
            {
                L[i][j] = 0;
            }
        }

        // Binary index, used to index
        // current row and previous row.
        let bi=0;

        for (let i = 0; i <= m; i++)
        {

            // Compute current binary index
            bi = i & 1;

            for (let j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[bi][j] = 0;

                else if (X[i - 1] ==
                         Y[j - 1])
                    L[bi][j] = L[1 - bi][j - 1] + 1;

                else
                    L[bi][j] = Math.max(L[1 - bi][j],
                                        L[bi][j - 1]);
            }
        }

        // Last filled entry contains length of
        // LCS for X[0..n-1] and Y[0..m-1]
        return L[bi][n];
    }

    let X = "AGGTAB";
    let Y = "GXTXAYB";

    document.write("Length of LCS is " +
                       lcs(X, Y));

</script>
```

**输出:**

```
Length of LCS is 4
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(n)

本文由 **Shivam Mittal** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。