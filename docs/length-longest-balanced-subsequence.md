# 最长平衡子序列的长度

> 原文:[https://www . geesforgeks . org/length-最长-平衡-子序列/](https://www.geeksforgeeks.org/length-longest-balanced-subsequence/)

给定一个字符串 **S** ，求其中最长的平衡子序列的长度。平衡字符串定义为:-

*   空字符串是平衡字符串。
*   如果 X 和 Y 是平衡字符串，那么(X)Y 和 XY 就是平衡字符串。

**示例:**

```
Input : S = "()())"
Output : 4

()() is the longest balanced subsequence 
of length 4.

Input : s = "()(((((()"
Output : 4
```

**方法 1:** 一种**蛮力**方法是找到给定字符串 S 的所有子序列，并检查所有可能的子序列是否形成平衡序列。如果是，将其与最大值进行比较。
更好的**方法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。
最长平衡子序列(LBS)，可以递归定义如下。**

```
LBS of substring str[i..j] : 
If str[i] == str[j]
    LBS(str, i, j) = LBS(str, i + 1, j - 1) + 2
Else
    LBS(str, i, j) = max(LBS(str, i, k) +
                         LBS(str, k + 1, j))
                     Where i <= k < j   
```

声明一个 2D 矩阵 dp[][]，其中我们的状态 dp[i][j]将表示从索引 I 到 j 的最长平衡子序列的长度。我们将按照 j–I 递增的顺序计算这个状态。对于特定的状态 dp[i][j]，我们将尝试将 jth 符号与 kth 符号进行匹配。只有当 S[k]为“(”且 S[j]为“)”时，才能这样做。对于所有这些可能的 k，我们将取最大值 2+DP[I][k–1]+DP[k+1][j–1]以及最大值(dp[i + 1][j]，DP[I][j–1])，并将该值放入 dp[i][j]中。这样，我们就可以填写所有的 dp 状态。DP[0][字符串长度–1](考虑 0 索引)将是我们的答案。
以下是本办法的实施情况:

## C++

```
// C++ program to find length of
// the longest balanced subsequence
#include <bits/stdc++.h>
using namespace std;

int maxLength(char s[], int n)
{
    int dp[n][n];
    memset(dp, 0, sizeof(dp));

    // Considering all balanced
    // substrings of length 2
    for (int i = 0; i < n - 1; i++)
        if (s[i] == '(' && s[i + 1] == ')')
            dp[i][i + 1] = 2;

    // Considering all other substrings
    for (int l = 2; l < n; l++) {
        for (int i = 0, j = l; j < n; i++, j++) {
            if (s[i] == '(' && s[j] == ')')
                dp[i][j] = 2 + dp[i + 1][j - 1];

            for (int k = i; k < j; k++)
                dp[i][j] = max(dp[i][j],
                               dp[i][k] + dp[k + 1][j]);
        }
    }

    return dp[0][n - 1];
}

// Driver Code
int main()
{
    char s[] = "()(((((()";
    int n = strlen(s);
    cout << maxLength(s, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the
// longest balanced subsequence.
import java.io.*;

class GFG {
    static int maxLength(String s, int n)
    {
        int dp[][] = new int[n][n];

        // Considering all balanced substrings
        // of length 2
        for (int i = 0; i < n - 1; i++)
            if (s.charAt(i) == '(' && s.charAt(i + 1) == ')')
                dp[i][i + 1] = 2;

        // Considering all other substrings
        for (int l = 2; l < n; l++) {
            for (int i = 0, j = l; j < n; i++, j++) {
                if (s.charAt(i) == '(' && s.charAt(j) == ')')
                    dp[i][j] = 2 + dp[i + 1][j - 1];

                for (int k = i; k < j; k++)
                    dp[i][j] = Math.max(dp[i][j],
                                        dp[i][k] + dp[k + 1][j]);
            }
        }

        return dp[0][n - 1];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "()(((((()";
        int n = s.length();
        System.out.println(maxLength(s, n));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to find length of
# the longest balanced subsequence

def maxLength(s, n):

    dp = [[0 for i in range(n)]
             for i in range(n)]

    # Considering all balanced
    # substrings of length 2
    for i in range(n - 1):
        if (s[i] == '(' and s[i + 1] == ')'):
            dp[i][i + 1] = 2

    # Considering all other substrings
    for l in range(2, n):
        i = -1
        for j in range(l, n):
            i += 1
            if (s[i] == '(' and s[j] == ')'):
                dp[i][j] = 2 + dp[i + 1][j - 1]
            for k in range(i, j):
                dp[i][j] = max(dp[i][j], dp[i][k] +
                                         dp[k + 1][j])
    return dp[0][n - 1]

# Driver Code
s = "()(((((()"
n = len(s)
print(maxLength(s, n))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to find length of the
// longest balanced subsequence.
using System;

class GFG {

    static int maxLength(String s, int n)
    {
        int[, ] dp = new int[n, n];

        // Considering all balanced substrings
        // of length 2
        for (int i = 0; i < n - 1; i++)
            if (s[i] == '(' && s[i + 1] == ')')
                dp[i, i + 1] = 2;

        // Considering all other substrings
        for (int l = 2; l < n; l++) {
            for (int i = 0, j = l; j < n; i++, j++) {
                if (s[i] == '(' && s[j] == ')')
                    dp[i, j] = 2 + dp[i + 1, j - 1];

                for (int k = i; k < j; k++)
                    dp[i, j] = Math.Max(dp[i, j],
                                        dp[i, k] + dp[k + 1, j]);
            }
        }

        return dp[0, n - 1];
    }

    // Driver Code
    public static void Main()
    {
        string s = "()(((((()";
        int n = s.Length;
        Console.WriteLine(maxLength(s, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of
// the longest balanced subsequence
function maxLength($s, $n)
{
    $dp = array_fill(0, $n,
          array_fill(0, $n, NULL));

    // Considering all balanced
    // substrings of length 2
    for ($i = 0; $i < $n - 1; $i++)
        if ($s[$i] == '(' && $s[$i + 1] == ')')
            $dp[$i][$i + 1] = 2;

    // Considering all other substrings
    for ($l = 2; $l < $n; $l++)
    {
        for ($i = 0, $j = $l; $j < $n; $i++, $j++)
        {
            if ($s[$i] == '(' && $s[$j] == ')')
                $dp[$i][$j] = 2 + $dp[$i + 1][$j - 1];

            for ($k = $i; $k < $j; $k++)
                $dp[$i][$j] = max($dp[$i][$j],
                                  $dp[$i][$k] +
                                  $dp[$k + 1][$j]);        
        }
    }

    return $dp[0][$n - 1];
}

// Driver Code
$s = "()(((((()";
$n = strlen($s);
echo maxLength($s, $n)."\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
    // Javascript program to find length of the
    // longest balanced subsequence.

    function maxLength(s, n)
    {
        let dp = new Array(n);
        for (let i = 0; i < n; i++)
        {
            dp[i] = new Array(n);
            for (let j = 0; j < n; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Considering all balanced substrings
        // of length 2
        for (let i = 0; i < n - 1; i++)
            if (s[i] == '(' && s[i + 1] == ')')
                dp[i][i + 1] = 2;

        // Considering all other substrings
        for (let l = 2; l < n; l++) {
            for (let i = 0, j = l; j < n; i++, j++) {
                if (s[i] == '(' && s[j] == ')')
                    dp[i][j] = 2 + dp[i + 1][j - 1];

                for (let k = i; k < j; k++)
                    dp[i][j] = Math.max(dp[i][j],
                                        dp[i][k] + dp[k + 1][j]);
            }
        }

        return dp[0][n - 1];
    }

    let s = "()(((((()";
    let n = s.length;
    document.write(maxLength(s, n));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

**方法 2:** 这种方法以更有效的方式解决问题。

1.  计算要删除的括号数，以获得最长的平衡括号子序列。
2.  如果右大括号的第 I 个索引号大于左大括号的数量，则必须移除右大括号。
3.  计算需要移除的右大括号的数量。
4.  最后，额外的开放支架的数量也将被移除。
5.  因此，要删除的总计数将是额外的左大括号和无效的右大括号的总和。

## C++

```
// C++ program to find length of
// the longest balanced subsequence
#include <bits/stdc++.h>
using namespace std;

int maxLength(char s[], int n)
{
    // As it's subsequence - assuming first
    // open brace would map to a first close
    // brace which occurs after the open brace
    // to make subsequence balanced and second
    // open brace would map to second close
    // brace and so on.

    // Variable to count all the open brace
    // that does not have the corresponding
    // closing brace.
    int invalidOpenBraces = 0;

    // To count all the close brace that
    // does not have the corresponding open brace.
    int invalidCloseBraces = 0;

    // Iterating over the String
    for (int i = 0; i < n; i++) {
        if (s[i] == '(') {

            // Number of open braces that
            // hasn't been closed yet.
            invalidOpenBraces++;
        }
        else {
            if (invalidOpenBraces == 0) {

                // Number of close braces that
                // cannot be mapped to any open
                // brace.
                invalidCloseBraces++;
            }
            else {

                // Mapping the ith close brace
                // to one of the open brace.
                invalidOpenBraces--;
            }
        }
    }
    return (
        n - (invalidOpenBraces
             + invalidCloseBraces));
}

// Driver Code
int main()
{
    char s[] = "()(((((()";
    int n = strlen(s);
    cout << maxLength(s, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the
// longest balanced subsequence.
import java.io.*;

class GFG {
    static int maxLength(String s, int n)
    {
        // As it's subsequence - assuming first
        // open brace would map to a first close
        // brace which occurs after the open brace
        // to make subsequence balanced and second
        // open brace would map to second close
        // brace and so on.

        // Variable to count all the open brace
        // that does not have the corresponding
        // closing brace.
        int invalidOpenBraces = 0;

        // To count all the close brace that
        // does not have the corresponding open brace.
        int invalidCloseBraces = 0;

        // Iterating over the String
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '(') {

                // Number of open braces that
                // hasn't been closed yet.vvvvvv
                invalidOpenBraces++;
            }
            else {
                if (invalidOpenBraces == 0) {

                    // Number of close braces that
                    // cannot be mapped to any open
                    // brace.
                    invalidCloseBraces++;
                }
                else {

                    // Mapping the ith close brace
                    // to one of the open brace.
                    invalidOpenBraces--;
                }
            }
        }
        return (
            n - (invalidOpenBraces
                 + invalidCloseBraces));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "()(((((()";
        int n = s.length();
        System.out.println(maxLength(s, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find length of
# the longest balanced subsequence

def maxLength(s, n):

    # As it's subsequence - assuming first
    # open brace would map to a first close
    # brace which occurs after the open brace
    # to make subsequence balanced and second
    # open brace would map to second close
    # brace and so on.

    # Variable to count all the open brace
    # that does not have the corresponding
    # closing brace.
    invalidOpenBraces = 0;

    # To count all the close brace that does
    # not have the corresponding open brace.
    invalidCloseBraces = 0;

    # Iterating over the String
    for i in range(n):
        if( s[i] == '(' ):

                # Number of open braces that
                # hasn't been closed yet.
                invalidOpenBraces += 1
        else:
            if(invalidOpenBraces == 0):
                # Number of close braces that
                # cannot be mapped to any open
                # brace.
                invalidCloseBraces += 1
            else:
                # Mapping the ith close brace
                # to one of the open brace.
                invalidOpenBraces -= 1

    return (
n - (
invalidOpenBraces + invalidCloseBraces))

# Driver Code
s = "()(((((()"
n = len(s)
print(maxLength(s, n))
```

## C#

```
// C# program to find length of the
// longest balanced subsequence.
using System;

class GFG {

    static int maxLength(String s, int n)
    {

        // As it's subsequence - assuming first
        // open brace would map to a first close
        // brace which occurs after the open brace
        // to make subsequence balanced and second
        // open brace would map to second close
        // brace and so on.

        // Variable to count all the open brace
        // that does not have the corresponding
        // closing brace.
        int invalidOpenBraces = 0;

        // To count all the close brace that
        // does not have the corresponding open brace.
        int invalidCloseBraces = 0;

        // Iterating over the String
        for (int i = 0; i < n; i++) {
            if (s[i] == '(') {

                // Number of open braces that
                // hasn't been closed yet.
                invalidOpenBraces++;
            }
            else {
                if (invalidOpenBraces == 0) {

                    // Number of close braces that
                    // cannot be mapped to any open brace.
                    invalidCloseBraces++;
                }
                else {

                    // Mapping the ith close brace to
                    // one of the open brace.
                    invalidOpenBraces--;
                }
            }
        }
        return (
            n - (invalidOpenBraces
                 + invalidCloseBraces));
    }

    // Driver Code
    public static void Main()
    {
        string s = "()(((((()";
        int n = s.Length;
        Console.WriteLine(maxLength(s, n));
    }
}
```

## java 描述语言

```
<script>

// Javascript program to find the length of the
// longest balanced subsequence.

    function maxLength(s, n)
    {
        // As it's subsequence - assuming first
        // open brace would map to a first close
        // brace which occurs after the open brace
        // to make subsequence balanced and second
        // open brace would map to second close
        // brace and so on.

        // Variable to count all the open brace
        // that does not have the corresponding
        // closing brace.
        let invalidOpenBraces = 0;

        // To count all the close brace that
        // does not have the corresponding open brace.
        let invalidCloseBraces = 0;

        // Iterating over the String
        for (let i = 0; i < n; i++) {
            if (s[i] == '(') {

                // Number of open braces that
                // hasn't been closed yet.vvvvvv
                invalidOpenBraces++;
            }
            else {
                if (invalidOpenBraces == 0) {

                    // Number of close braces that
                    // cannot be mapped to any open
                    // brace.
                    invalidCloseBraces++;
                }
                else {

                    // Mapping the ith close brace
                    // to one of the open brace.
                    invalidOpenBraces--;
                }
            }
        }
        return (
            n - (invalidOpenBraces
                 + invalidCloseBraces));
    }

// driver program

        let s = "()(((((()";
        let n = s.length;
        document.write(maxLength(s, n));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。