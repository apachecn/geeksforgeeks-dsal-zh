# 将一根长度为 N 的棍子切成 K 块的方法数量

> 原文:[https://www . geesforgeks . org/number-way-cut-stick-length-n-k-pieces/](https://www.geeksforgeeks.org/number-ways-cut-stick-length-n-k-pieces/)

给定一根 N 号的棍子，找出它可以被切成 K 块的方法，这样每块的长度都大于 0。

**示例:**

```
Input : N = 5
        K = 2
Output : 4
```

![](img/8fde318d77c6765b1df8b8898d827ae9.png)

```
Input : N = 15
        K = 5
Output : 1001
```

解这道题相当于解数学方程 **x <sub>1</sub> + x <sub>2</sub> + …..+ x <sub>K</sub> = N**
我们可以用组合学中的**条和星**方法来求解，从中我们得到这个方程的正积分解个数为**<sup>(N–1)</sup>C<sub>(K–1)</sub>**，其中 <sup>N</sup> C <sub>K</sub> 为 N！/((N–K)！* (K！))，哪里！代表阶乘。
在 C++和 Java 中，对于阶乘的大值，可能会出现溢出错误。在这种情况下，我们可以引入一个大质数如 10 <sup>7</sup> + 7 来修改答案。我们可以利用[卢卡斯定理](https://www.geeksforgeeks.org/compute-ncr-p-set-2-lucas-theorem/)计算 nCr % p。
但是，python 可以处理大值而不会溢出。

## C++

```
// C++ program to calculate the number of ways
// to divide a stick of length n into k pieces
#include <bits/stdc++.h>
using namespace std;

// function to generate nCk or nChoosek
unsigned long long nCr(unsigned long long n,
                       unsigned long long r)
{
    if (n < r)
        return 0;

    // Reduces to the form n! / n!
    if (r == 0)
        return 1;

    // nCr has been simplified to this form by
    // expanding numerator and denominator to
    // the form   n(n - 1)(n - 2)...(n - r + 1)
    //             -----------------------------
    //                         (r!)
    // in the above equation, (n - r)! is cancelled
    // out in the numerator and denominator

    unsigned long long numerator = 1;
    for (int i = n; i > n - r; i--)
        numerator = (numerator * i);

    unsigned long long denominator = 1;
    for (int i = 1; i < r + 1; i++)
        denominator = (denominator * i);

    return (numerator / denominator);
}

// Returns number of ways to cut
// a rod of length N into K pieces.
unsigned long long countWays(unsigned long long N,
                             unsigned long long K)
{
    return nCr(N - 1, K - 1);
}

// Driver code
int main()
{
    unsigned long long N = 5;
    unsigned long long K = 2;
    cout << countWays(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ways in which
// a stick of length n can be divided into K pieces
import java.io.*;
import java.util.*;

class GFG
{
    // function to generate nCk or nChoosek
    public static int nCr(int n, int r)
    {
        if (n < r)
            return 0;

        // Reduces to the form n! / n!
        if (r == 0)
            return 1;

        // nCr has been simplified to this form by
        // expanding numerator and denominator to
        // the form  n(n - 1)(n - 2)...(n - r + 1)
        //             -----------------------------
        //                          (r!)
        // in the above equation, (n-r)! is cancelled
        // out in the numerator and denominator

        int numerator = 1;
        for (int i = n ; i > n - r ; i--)
            numerator = (numerator * i);

        int denominator = 1;
        for (int i = 1 ; i < r + 1 ; i++)
            denominator = (denominator * i);

        return (numerator / denominator);
    }

    // Returns number of ways to cut
    // a rod of length N into K pieces
    public static int countWays(int N, int K)
    {
        return nCr(N - 1, K - 1);
    }

    public static void main(String[] args)
    {
        int N = 5;
        int K = 2;
        System.out.println(countWays(N, K));
    }
}
```

## 蟒蛇 3

```
# Python program to find the number
# of ways  in which a stick of length
# n can be divided into K pieces

# function to generate nCk or nChoosek
def nCr(n, r):

    if (n < r):
        return 0

    # reduces to the form n! / n!
    if (r == 0):
        return 1

    # nCr has been simplified to this form by
    # expanding numerator and denominator to
    # the form     n(n - 1)(n - 2)...(n - r + 1)
    #             -----------------------------
    #                         (r!)
    # in the above equation, (n-r)! is cancelled
    # out in the numerator and denominator

    numerator = 1
    for i in range(n, n - r, -1):
        numerator = numerator * i

    denominator = 1
    for i in range(1, r + 1):
        denominator = denominator * i

    return (numerator // denominator)

# Returns number of ways to cut
# a rod of length N into K pieces.
def countWays(N, K) :
    return nCr(N - 1, K - 1);

# Driver code
N = 5
K = 2
print(countWays(N, K))
```

## C#

```
// C# program to find the number of
// ways in which a stick of length n
// can be divided into K pieces
using System;

class GFG
{
    // function to generate nCk or nChoosek
    public static int nCr(int n, int r)
    {
        if (n < r)
            return 0;

        // Reduces to the form n! / n!
        if (r == 0)
            return 1;

        // nCr has been simplified to this form by
        // expanding numerator and denominator to
        // the form  n(n - 1)(n - 2)...(n - r + 1)
        //             -----------------------------
        //                          (r!)
        // in the above equation, (n-r)! is cancelled
        // out in the numerator and denominator

        int numerator = 1;
        for (int i = n; i > n - r; i--)
            numerator = (numerator * i);

        int denominator = 1;
        for (int i = 1; i < r + 1; i++)
            denominator = (denominator * i);

        return (numerator / denominator);
    }

    // Returns number of ways to cut
    // a rod of length N into K pieces
    public static int countWays(int N, int K)
    {
        return nCr(N - 1, K - 1);
    }

    public static void Main()
    {
        int N = 5;
        int K = 2;
        Console.Write(countWays(N, K));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate the
// number of ways to divide a
// stick of length n into k pieces

// function to generate nCk or nChoosek
function nCr($n, $r)
{
    if ($n < $r)
        return 0;

    // Reduces to the form n! / n!
    if ($r == 0)
        return 1;

    // nCr has been simplified to this form by
    // expanding numerator and denominator to
    // the form n(n - 1)(n - 2)...(n - r + 1)
    //             -----------------------------
    //                         (r!)
    // in the above equation, (n - r)! is cancelled
    // out in the numerator and denominator

    $numerator = 1;
    for ($i = $n; $i > $n - $r; $i--)
        $numerator = ($numerator * $i);

    $denominator = 1;
    for ($i = 1; $i < $r + 1; $i++)
        $denominator = ($denominator * $i);

    return (floor($numerator / $denominator));
}

// Returns number of ways to cut
// a rod of length N into K pieces.
function countWays($N, $K)
{
    return nCr($N - 1, $K - 1);
}

// Driver code
$N = 5;
$K = 2;
echo countWays($N, $K);
return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
//Javascript Implementation
// to calculate the number of ways
// to divide a stick of length n into k pieces

// function to generate nCk or nChoosek
function nCr(n,r)
{
    if (n < r)
        return 0;

    // Reduces to the form n! / n!
    if (r == 0)
        return 1;

    // nCr has been simplified to this form by
    // expanding numerator and denominator to
    // the form   n(n - 1)(n - 2)...(n - r + 1)
    //             -----------------------------
    //                         (r!)
    // in the above equation, (n - r)! is cancelled
    // out in the numerator and denominator

    var numerator = 1;
    for (var i = n; i > n - r; i--)
        numerator = (numerator * i);

    var denominator = 1;
    for (var i = 1; i < r + 1; i++)
        denominator = (denominator * i);

    return Math.floor(numerator / denominator);
}

// Returns number of ways to cut
// a rod of length N into K pieces.
function countWays(N,K)
{
    return nCr(N - 1, K - 1);
}

// Driver code
var N = 5;
var K = 2;
document.write(countWays(N, K));

// This code is contributed by shubhamsingh10
</script>
```

**输出:**

```
4 
```

**练习:**
用允许的 0 个长度片扩展上述问题。提示:同样可以通过将每个 x <sub>i</sub> 写成 y<sub>I</sub>–1 来找到解的个数，我们得到一个等式 **y <sub>1</sub> + y <sub>2</sub> + …..+ y <sub>K</sub> = N + K** 。该方程解的个数为**<sup>(N+K–1)</sup>C<sub>(K–1)</sub>**
本文由 **Deepak Srivatsav** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。