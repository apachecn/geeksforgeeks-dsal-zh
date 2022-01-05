# 一次取 N 个物体排列 K 个不同物体的方式数量

> 原文:[https://www . geeksforgeeks . org/排列不同对象的方式数-一次取 n 个对象/](https://www.geeksforgeeks.org/number-of-ways-to-arrange-k-different-objects-taking-n-objects-at-a-time/)

给定两个整数 **K** 和 **N** ，任务是统计一次取 **N** 个对象排列 **K** 个不同对象的方式数。每个排列最多包含一个对象。答案可能很大，所以以 10 <sup>9</sup> + 7 为模返回答案。
**注:**1<=**N**T31】=**K**T32】= 10<sup>5</sup>。
**先决条件:** [一个数的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)、[计算 nCr % p](https://www.geeksforgeeks.org/compute-ncr-p-set-3-using-fermat-little-theorem/)
**示例:**

> **输入:** N = 3，K = 3
> **输出:** 6
> 如果 1、2 和 3 是 K 个不同的对象，那么可能的排列是{123、132、213、231、312、321}。
> **输入:** N = 4，K = 6
> **输出:** 360

**方法:**问题可以用排列组合来解决。由于 **N** 始终小于或等于 **K** ，大于 0 的答案始终存在。 **K** 可用对象中的任何对象在一个排列中最多可以使用一次。因此，我们需要从 **K** 可用对象中选择 N 个对象进行单一排列。所以，从 **K** 对象中选择 **N** 对象的方式总数为 <sup>K</sup> C <sub>N</sub> 。然后，任何选定的 N 个对象的组都可以用 N 种方式在它们之间进行置换。所以，问题的答案是:

> (N！*<sup>K</sup>C<sub>N</sub>)%(10<sup>9</sup>+7)

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define mod (ll)(1e9 + 7)

// Function to return n! % p
ll factorial(ll n, ll p)
{
    ll res = 1; // Initialize result
    for (int i = 2; i <= n; i++)
        res = (res * i) % p;
    return res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
ll power(ll x, ll y, ll p)
{
    ll res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
ll modInverse(ll n, ll p)
{
    return power(n, p - 2, p);
}

// Returns nCr % p using Fermat's little
// theorem.
ll nCrModP(ll n, ll r, ll p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    ll fac[n + 1];
    fac[0] = 1;
    for (int i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[n] * modInverse(fac[r], p) % p
                    * modInverse(fac[n - r], p) % p) % p;
}

// Function to return the number of ways to
// arrange K different objects taking N objects
// at a time
ll countArrangements(ll n, ll k, ll p)
{
    return (factorial(n, p) * nCrModP(k, n, p)) % p;
}

// Drivers Code
int main()
{
    ll N = 5, K = 8;

    // Function call
    cout << countArrangements(N, K, mod);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static long mod =(long) (1e9 + 7);

// Function to return n! % p
static long factorial(long n, long p)
{
    long res = 1; // Initialize result
    for (int i = 2; i <= n; i++)
        res = (res * i) % p;
    return res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
static long power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if ((y & 1)==1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
static long modInverse(long n, long p)
{
    return power(n, p - 2, p);
}

// Returns nCr % p using Fermat's little
// theorem.
static long nCrModP(long n, long r, long p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    long fac[] = new long[(int)n + 1];
    fac[0] = 1;
    for (int i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[(int)n] * modInverse(fac[(int)r], p) % p
                    * modInverse(fac[(int)n - (int)r], p) % p) % p;
}

// Function to return the number of ways to
// arrange K different objects taking N objects
// at a time
static long countArrangements(long n, long k, long p)
{
    return (factorial(n, p) * nCrModP(k, n, p)) % p;
}

// Driver Code
public static void main(String[] args)
{
    long N = 5, K = 8;
    // Function call
    System.out.println(countArrangements(N, K, mod));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 10**9 + 7

# Function to return n! % p
def factorial(n, p):

    res = 1 # Initialize result
    for i in range(2, n + 1):
        res = (res * i) % p
    return res

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is
              # more than or equal to p

    while (y > 0):

        # If y is odd,
        # multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Returns n^(-1) mod p
def modInverse(n, p):

    return power(n, p - 2, p)

# Returns nCr % p using Fermat's little
# theorem.
def nCrModP(n, r, p):

    # Base case
    if (r == 0):
        return 1

    # Fifactorial array so that we
    # can find afactorial of r, n
    # and n-r
    fac = [0 for i in range(n + 1)]
    fac[0] = 1
    for i in range(1, n + 1):
        fac[i] = fac[i - 1] * i % p

    return (fac[n] * modInverse(fac[r], p) % p *
                     modInverse(fac[n - r], p) % p) % p

# Function to return the number of ways
# to arrange K different objects taking
# N objects at a time
def countArrangements(n, k, p):

    return (factorial(n, p) *
            nCrModP(k, n, p)) % p

# Drivers Code
N = 5
K = 8

# Function call
print(countArrangements(N, K, mod))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static long mod =(long) (1e9 + 7);

// Function to return n! % p
static long factorial(long n, long p)
{
    long res = 1; // Initialize result
    for (int i = 2; i <= n; i++)
        res = (res * i) % p;
    return res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
static long power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if ((y & 1)==1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
static long modInverse(long n, long p)
{
    return power(n, p - 2, p);
}

// Returns nCr % p using Fermat's little
// theorem.
static long nCrModP(long n, long r, long p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    long[] fac = new long[(int)n + 1];
    fac[0] = 1;
    for (int i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[(int)n] * modInverse(fac[(int)r], p) % p
                    * modInverse(fac[(int)n - (int)r], p) % p) % p;
}

// Function to return the number of ways to
// arrange K different objects taking N objects
// at a time
static long countArrangements(long n, long k, long p)
{
    return (factorial(n, p) * nCrModP(k, n, p)) % p;
}

// Driver Code
public static void Main()
{
    long N = 5, K = 8;

    // Function call
    Console.WriteLine(countArrangements(N, K, mod));
}
}

/* This code is contributed by Code_Mech */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$mod = (1e9 + 7);

// Function to return n! % p
function factorial($n,$p)
{
    $res = 1; // Initialize result
    for ($i = 2; $i <= $n; $i++)
        $res = ($res * $i) % $p;
    return $res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it is more than or
    // equal to p

    while ($y > 0)
    {
        // If y is odd, multiply x with result
        if (($y & 1)==1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Returns n^(-1) mod p
function modInverse($n, $p)
{
    return power($n, $p - 2, $p);
}

// Returns nCr % p using Fermat's little
// theorem.
function nCrModP($n, $r, $p)
{
    // Base case
    if ($r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    $fac= array((int)$n + 1);
    $fac[0] = 1;
    for ($i = 1; $i <= $n; $i++)
        $fac[$i] = $fac[$i - 1] * $i % $p;

    return ($fac[(int)$n] * modInverse($fac[(int)$r], $p) % $p
                    * modInverse($fac[(int)$n - (int)$r], $p) % $p) % $p;
}

// Function to return the number of ways to
// arrange K different objects taking N objects
// at a time
function countArrangements($n, $k, $p)
{
    return (factorial($n, $p) * nCrModP($k, $n, $p)) % $p;
}

// Driver Code
{
    $N = 5; $K = 8;
    // Function call
    echo(countArrangements($N, $K, $mod));
}

/* This code is contributed by Code_Mech*/
```

## java 描述语言

```
<script>

// javascript implementation of the approach  
var mod =parseInt(1e4 + 7);

// Function to return n! % p
function factorial(n , p)
{
    var res = 1; // Initialize result
    for (var i = 2; i <= n; i++)
        res = (res * i) % p;
    return res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
function power(x , y , p)
{
    var res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if ((y & 1)==1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
function modInverse(n , p)
{
    return power(n, p - 2, p);
}

// Returns nCr % p using Fermat's little
// theorem.
function nCrModP(n , r , p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    var fac = Array.from({length: n+1}, (_, i) => 0);;
    fac[0] = 1;
    for (var i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[parseInt(n)] * modInverse(fac[parseInt(r)], p) % p
                    * modInverse(fac[parseInt(n) - parseInt(r)], p) % p) % p;
}

// Function to return the number of ways to
// arrange K different objects taking N objects
// at a time
function countArrangements(n , k , p)
{
    return (factorial(n, p) * nCrModP(k, n, p)) % p;
}

// Driver Code
var N = 5, K = 8;
// Function call
document.write(countArrangements(N, K, mod));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
6720
```