# 没有三个项形成递增子序列的排列数

> 原文:[https://www . geesforgeks . org/排列数-这样-没有-三项-形式-增加-子序列/](https://www.geeksforgeeks.org/number-of-permutations-such-that-no-three-terms-forms-increasing-subsequence/)

给定一个数 N，任务是找出 1 到 N 的排列数，这样排列的三个项就不会形成一个递增的子序列。

**示例**:

```
Input : N = 3
Output : 5
Valid permutations : 132, 213, 231, 312 and 321 and not 123

Input : N = 4
Output : 14 
```

以上问题是加泰罗尼亚数字的一个[应用。所以，任务是只找到第 n 个加泰罗尼亚数字。前几个加泰罗尼亚数字是 1，1，2，5，14，42，132，429，1430，4862，…(从第 0 个数字开始考虑)](https://www.geeksforgeeks.org/applications-of-catalan-numbers/)

下面是寻找 [N <sup>th</sup> 加泰罗尼亚语号码](https://www.geeksforgeeks.org/program-nth-catalan-number/)的程序:

## C++

```
// C++ program to find the
// nth catalan number
#include <bits/stdc++.h>
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
unsigned long int binomialCoeff(unsigned int n,
                                unsigned int k)
{
    unsigned long int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient based function
// to find nth catalan
// number in O(n) time
unsigned long int catalan(unsigned int n)
{
    // Calculate value of 2nCn
    unsigned long int c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
int main()
{
    int n = 3;

    cout << catalan(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// nth catalan number
import java.io.*;

class GFG
{

// Returns value of Binomial
// Coefficient C(n, k)
static long binomialCoeff(long n, long k)
{
    long res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] /
    // [k*(k-1)*---*1]
    for (int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient based
// function to find nth catalan
// number in O(n) time
static long catalan(long n)
{
    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
public static void main (String[] args)
{
    int n = 3;

    System.out.println(catalan(n));
}
}

// This code has been contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python program to find the
# nth catalan number

# Returns value of Binomial
# Coefficient C(n, k)
def binomialCoeff(n, k):
    res = 1

    # Since C(n, k) = C(n, n-k)
    if k > n - k:
        k=n-k
    # Calculate value of
    # [n*(n-1)*---*(n-k+1)] //
    # [k*(k-1)*---*1]

    for i in range(k):
        res = res * (n - i)
        res = res // (i + 1)
    return res

# A Binomial coefficient based
# function to find nth catalan
# number in O(n) time
def catalan(n):

    # Calculate value of 2nCn
    c = binomialCoeff(2 * n, n)

    # return 2nCn/(n+1)
    return c // (n + 1)

# Driver code
n = 3
print(catalan(n))

# This code is contributed
# by sahil shelangia
```

## C#

```
// C# program to find the
// nth catalan number
using System;

class GFG
{

// Returns value of Binomial
// Coefficient C(n, k)
static long binomialCoeff(long n,
                          long k)
{
    long res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] /
    // [k*(k-1)*---*1]
    for (int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient based
// function to find nth catalan
// number in O(n) time
static long catalan(long n)
{
    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
public static void Main (String[] args)
{
    int n = 3;

    Console.WriteLine(catalan(n));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// nth catalan number

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff($n, $k)
{
    $res = 1;

    // Since C(n, k) = C(n, n-k)
    if($k >$n - $k)
        $k = $n - $k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] //
    // [k*(k-1)*---*1]
    for ($i = 0; $i < $k; $i++)
    {
        $res = $res * ($n - $i);
        $res = $res / ($i + 1);
    }
    return $res;
}

// A Binomial coefficient based
// function to find nth catalan
// number in O(n) time
function catalan($n)
{
    // Calculate value of 2nCn
    $c = binomialCoeff(2 * $n, $n);

    // return 2nCn/(n+1)
    return $c / ($n + 1);
}

// Driver code
$n = 3;
print(catalan($n));

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// nth catalan number

// Returns value of Binomial Coefficient C(n, k)
function binomialCoeff(n, k)
{
    var res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for (var i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient based function
// to find nth catalan
// number in O(n) time
function catalan(n)
{
    // Calculate value of 2nCn
    var c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
var n = 3;
document.write( catalan(n));

</script>
```

**Output:** 

```
5
```