# 一个数的 GCD 升到某个幂，另一个数的 GCD

> 原文:[https://www . geeksforgeeks . org/gcd-of-a-number-up-to-some-power-and-other-number/](https://www.geeksforgeeks.org/gcd-of-a-number-raised-to-some-power-and-another-number/)

给定三个数字 a，b，n，求 GCD(a <sup>n</sup> ，b)。
**例:**

```
Input : a = 2, b = 3, n = 3
Output : 1
2^3 = 8\. GCD of 8 and 3 is 1\. 

Input : a = 2, b = 4, n = 5
Output : 4
```

**第一种方法:**强力方法是首先计算 a^n，然后计算 a^n 和 b 的 gcd。

## C++

```
// CPP program to find GCD of a^n and b.
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

ll gcd(ll a, ll b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Returns GCD of a^n and b.
ll powGCD(ll a, ll n, ll b)
{
    for (int i = 0; i < n; i++)
        a = a * a;

    return gcd(a, b);
}

// Driver code
int main()
{
    ll a = 10, b = 5, n = 2;
    cout << powGCD(a, n, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find GCD of a^n and b.

import java.io.*;

class GFG {

static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Returns GCD of a^n and b.
static long powGCD(long a, long n, long b)
{
    for (int i = 0; i < n; i++)
        a = a * a;

    return gcd(a, b);
}

// Driver code
    public static void main (String[] args) {
    long a = 10, b = 5, n = 2;
    System.out.println(powGCD(a, n, b));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find
# GCD of a^n and b.
def gcd(a, b):
    if (a == 0):
        return b
    return gcd(b % a, a)

# Returns GCD of a^n and b.
def powGCD(a, n, b):
    for i in range(0, n + 1, 1):
        a = a * a

    return gcd(a, b)

# Driver code
if __name__ == '__main__':
    a = 10
    b = 5
    n = 2
    print(powGCD(a, n, b))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to find GCD of a^n and b.
using System;

class GFG
{
public static long gcd(long a, long b)
{
    if (a == 0)
    {
        return b;
    }
    return gcd(b % a, a);
}

// Returns GCD of a^n and b.
public static long powGCD(long a,
                          long n, long b)
{
    for (int i = 0; i < n; i++)
    {
        a = a * a;
    }

    return gcd(a, b);
}

// Driver code
public static void Main(string[] args)
{
    long a = 10, b = 5, n = 2;
    Console.WriteLine(powGCD(a, n, b));
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD of a^n and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Returns GCD of a^n and b.
function powGCD($a, $n, $b)
{
    for ($i = 0; $i < $n; $i++)
        $a = $a * $a;

    return gcd($a, $b);
}

// Driver code
$a = 10;
$b = 5;
$n = 2;

echo powGCD($a, $n, $b);

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>
// javascript program to find GCD of a^n and b.   
function gcd(a , b)
{
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Returns GCD of a^n and b.
    function powGCD(a , n , b)
    {
        for (i = 0; i < n; i++)
            a = a * a;

        return gcd(a, b);
    }

    // Driver code
        var a = 10, b = 5, n = 2;
        document.write(powGCD(a, n, b));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
5
```

但是，如果 n 很大呢(比如说> 10^9).**模幂**是办法。我们知道(a*b) % m = ( (a%m) * (b%m) ) % m)。我们也知道 **gcd(a，b) = gcd(b%a，a)** 。所以我们不用计算“幂(a，n)”，而是使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)。

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

/* Calculates modular exponentiation, i.e.,
   (x^y)%p in O(log y) */
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

ll gcd(ll a, ll b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Returns GCD of a^n and b
ll powerGCD(ll a, ll b, ll n)
{
    ll e = power(a, n, b);
    return gcd(e, b);
}

// Driver code
int main()
{
    ll a = 5, b = 4, n = 2;
    cout << powerGCD(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
class Solution{

/* Calculates modular exponentiation, i.e.,
   (x^y)%p in O(log y) */
static long power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with result
        if ((y & 1)!=0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Returns GCD of a^n and b
static long powerGCD(long a, long b, long n)
{
    long e = power(a, n, b);
    return gcd(e, b);
}

// Driver code
public static void main(String args[])
{
    long a = 5, b = 4, n = 2;
    System.out.print( powerGCD(a, b, n));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Calculates modular exponentiation, i.e.,
 # (x^y)%p in O(log y)
def power( x,  y,  p):

    res = 1  # Initialize result

    x = x % p # Update x if it is more than or
    # equal to p

    while (y > 0) :

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1   # y = y/2
        x = (x * x) % p

    return res

def gcd(a,  b):

    if (a == 0):
        return b
    return gcd(b % a, a)

# Returns GCD of a^n and b
def powerGCD( a,  b,  n):

    e = power(a, n, b)
    return gcd(e, b)

# Driver code
if __name__ == "__main__":

    a = 5
    b = 4
    n = 2
    print (powerGCD(a, b, n))
```

## C#

```
// C# program of the above approach
using System;
class GFG
{

/* Calculates modular exponentiation,
i.e.,  (x^y)%p in O(log y) */
static long power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Returns GCD of a^n and b
static long powerGCD(long a, long b,
                             long n)
{
    long e = power(a, n, b);
    return gcd(e, b);
}

// Driver code
public static void Main()
{
    long a = 5, b = 4, n = 2;
    Console.Write( powerGCD(a, b, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of the above approach
// Calculates modular exponentiation,
// i.e.,(x^y)%p in O(log y)

function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it is more
                  // than or equal to p

    while ($y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

function gcd ($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Returns GCD of a^n and b
function powerGCD($a, $b, $n)
{
    $e = power($a, $n, $b);
    return gcd($e, $b);
}

// Driver code
$a = 5;
$b = 4;
$n = 2;
echo powerGCD($a, $b, $n);

// This code is contributed by Sachin.
?>
```

## java 描述语言

```
<script>

// Javascript program of the above approach

    /*
      Calculates modular exponentiation,
      i.e., (x^y)%p in O(log y)
     */
    function power(x , y , p) {
        var res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0) {

            // If y is odd, multiply x with result
            if ((y & 1) != 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    function gcd(a , b) {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Returns GCD of a^n and b
    function powerGCD(a , b , n) {
        var e = power(a, n, b);
        return gcd(e, b);
    }

    // Driver code

        var a = 5, b = 4, n = 2;
        document.write(powerGCD(a, b, n));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1
```