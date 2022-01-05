# n+2 条边的凸多边形通过连接顶点分裂成三角形的方式数

> 原文:[https://www . geeksforgeeks . org/路数-一个由 n2 条边组成的凸多边形-可以通过连接顶点分割成三角形/](https://www.geeksforgeeks.org/number-of-ways-a-convex-polygon-of-n2-sides-can-split-into-triangles-by-connecting-vertices/)

给定一个 n+2 边的凸多边形。任务是计算用不相交的线段连接顶点形成三角形的方法的数量。
**例:**

> **输入** : n = 1
> **输出** : 1
> 已经是三角形了，所以只能用 1 种方式形成。
> **输入** : n = 2
> **输出** : 2
> 可以用任意一对相对的顶点切割成 2 个三角形。

![](img/5bace3434393d4ef57d90a5049f95b71.png)

上面的问题是一个加泰罗尼亚数字的应用。所以，任务就是只找到[第 n 个加泰罗尼亚号](https://www.geeksforgeeks.org/program-nth-catalan-number/)。前几个加泰罗尼亚数字是 1 1 2 5 14 42 132 429 1430 4862，…(从第 0 个数字开始考虑)
下面是查找第 n 个加泰罗尼亚数字的程序:

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
class GFG
{

// Returns value of Binomial
// Coefficient C(n, k)
static long binomialCoeff(int n,
                          int k)
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

// A Binomial coefficient
// based function to find
// nth catalan number in
// O(n) time
static long catalan( int n)
{
    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.println(catalan(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the
# nth catalan number

# Returns value of Binomial
# Coefficient C(n, k)
def binomialCoeff(n, k):

    res = 1;

    # Since C(n, k) = C(n, n-k)
    if (k > n - k):
        k = n - k;

    # Calculate value of
    # [n*(n-1)*---*(n-k+1)] /
    # [k*(k-1)*---*1]
    for i in range(k):

        res *= (n - i);
        res /= (i + 1);

    return res;

# A Binomial coefficient based
# function to find nth catalan
# number in O(n) time
def catalan(n):

    # Calculate value of 2nCn
    c = binomialCoeff(2 * n, n);

    # return 2nCn/(n+1)
    return int(c / (n + 1));

# Driver code
n = 3;
print(catalan(n));

# This code is contributed
# by mits
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
static long binomialCoeff(int n,
                          int k)
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

// A Binomial coefficient
// based function to find
// nth catalan number in
// O(n) time
static long catalan( int n)
{
    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code
public static void Main()
{
    int n = 3;
    Console.WriteLine(catalan(n));
}
}

// This code is contributed
// by Subhadeep
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
    if ($k > $n - $k)
        $k = $n - $k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] /
    // [k*(k-1)*---*1]
    for ($i = 0; $i < $k; ++$i)
    {
        $res *= ($n - $i);
        $res /= ($i + 1);
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
echo catalan($n);

// This code is contributed
// by chandan_jnu.
?>
```

## java 描述语言

```
<script>
// javascript program to find the
// nth catalan number// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff(n, k)
{
    var res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n*(n-1)*---*(n-k+1)] /
    // [k*(k-1)*---*1]
    for (i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

// A Binomial coefficient
// based function to find
// nth catalan number in
// O(n) time
function catalan(n)
{

    // Calculate value of 2nCn
    var c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Driver code

var n = 3;
document.write(catalan(n));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
5
```