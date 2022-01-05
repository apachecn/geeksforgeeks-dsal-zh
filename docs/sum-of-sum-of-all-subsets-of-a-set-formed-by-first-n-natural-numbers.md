# 由前 N 个自然数构成的集合的所有子集的和的和

> 原文:[https://www . geesforgeks . org/由第一个 n 个自然数构成的集合的所有子集的和之和/](https://www.geeksforgeeks.org/sum-of-sum-of-all-subsets-of-a-set-formed-by-first-n-natural-numbers/)

给定 N，ff(N) = f(1) + f(2) + …… + f(N)，其中 f(k)是由前 k 个自然数组成的集合的所有子集的[和。任务是求 ff(N)模 1000000007。
**例:**](https://www.geeksforgeeks.org/sum-subsets-set-formed-first-n-natural-numbers/) 

> **输入:** 2
> **输出:**7
> f(1)+f(2)
> f(1)= 1 = 1
> f(2)= 1+2+{ 1+2 } = 6
> **输入:** 3
> **输出:**31
> f(1)+f(2)+f(3)
> f(1)= 1 = 1
> f

**接近**:找到将要形成的序列模式。f(1)、f(2)、f(3)的值分别为 1、6 和 31。让我们找到 f(4)。

```
f(4) =  1 + 2 + 3 + 4 + {1 + 2} + {1 + 3} + {1 + 4} 
        + {2 + 3} + {2 + 4} + {3 + 4} + {1 + 2 + 3} + {1 + 2 + 4}
        + {1 + 3 + 4} + {2 + 3 + 4} + {1 + 2 + 3 + 4} = 80.
```

因此 ff(N)将是

```
ff(1) = f(1) = 1
ff(2) = f(1) + f(2) = 7
ff(3) = f(1) + f(2) + f(3) = 31
ff(4) = f(1) + f(2) + f(3) + f(4) = 111
.
.
.
```

形成的级数是 1，7，31，111…有一个公式是**2^n*(n^2+n+2)–1**。其中，N 从零开始。
以下是上述办法的实施情况。

## C++

```
// C++ program to find Sum of all
// subsets of a set formed by
// first N natural numbers | Set-2
#include <bits/stdc++.h>
using namespace std;

// modulo value
#define mod (int)(1e9 + 7)

// Iterative Function to calculate (x^y)%p in O(log y)
int power(int x, int y, int p)
{
    int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with the result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// function to find ff(n)
int check(int n)
{
    // In formula n is starting from zero
    n--;

    // calculate answer using
    // formula 2^n*(n^2 + n + 2) - 1
    int ans = n * n;

    // whenever answer is greater than
    // or equals to mod then modulo it.
    if (ans >= mod)
        ans %= mod;

    ans += n + 2;

    if (ans >= mod)
        ans %= mod;

    ans = (power(2, n, mod) % mod * ans % mod) % mod;

    // adding modulo while subtraction is very necessary
    // otherwise it will cause wrong answer
    ans = (ans - 1 + mod) % mod;

    return ans;
}

// Driver code
int main()
{
    int n = 4;

    // function call
    cout << check(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum of all
// subsets of a set formed by
// first N natural numbers | Set-2

class Geeks {

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(int x, int y, int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x
        // with the result
        if (y != 0)
            res = (res * x) % p;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// function to find ff(n)
static int check(int n)
{

    // modulo value
    int  mod = (int)(1e9 + 7);

    // In formula n is
    // starting from zero
    n--;

    // calculate answer using
    // formula 2^n*(n^2 + n + 2) - 1
    int ans = n * n;

    // whenever answer is greater than
    // or equals to mod then modulo it.
    if (ans >= mod)
        ans %= mod;

    ans += n + 2;

    if (ans >= mod)
        ans %= mod;

    ans = (power(2, n, mod) % mod *
                  ans % mod) % mod;

    // adding modulo while subtraction
    // is very necessary otherwise it
    // will cause wrong answer
    ans = (ans - 1 + mod) % mod;

    return ans;
}

// Driver Code
public static void main(String args[])
{
    int n = 4;

    // function call
    System.out.println(check(n));
}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
#Python3 program to find Sum of all
# subsets of a set formed by
# first N natural numbers | Set-2

# modulo value
mod = (int)(1e9 + 7)

# Iterative Function to calculate (x^y)%p in O(log y)
def power(x,y,p):
    res = 1 # Initialize result

    x = x % p # Update x if it is more than or
    # equal to p

    while (y > 0):

        # If y is odd, multiply x with the result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p
    return res

# function to find ff(n)
def check(n):
    # In formula n is starting from zero
    n=n-1

    # calculate answer using
    # formula 2^n*(n^2 + n + 2) - 1
    ans = n * n

    # whenever answer is greater than
    # or equals to mod then modulo it.
    if (ans >= mod):
        ans %= mod

    ans += n + 2

    if (ans >= mod):
        ans %= mod

    ans = (pow(2, n, mod) % mod * ans % mod) % mod

    # adding modulo while subtraction is very necessary
    # otherwise it will cause wrong answer
    ans = (ans - 1 + mod) % mod

    return ans

#Driver code
if __name__=='__main__':
    n = 4

# function call
    print(check(n))

# This code is contributed by ash264
```

## C#

```
// C# program to find Sum
// of all subsets of a set
// formed by first N natural
// numbers | Set-2
using System;

class GFG
{

// Iterative Function
// to calculate (x^y)%p
// in O(log y)
static int power(int x, int y,
                 int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with the result
        if (y != 0)
            res = (res * x) % p;

        // y must be even
        // now y = y / 2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// function to find ff(n)
static int check(int n)
{

    // modulo value
    int mod = (int)(1e9 + 7);

    // In formula n is
    // starting from zero
    n--;

    // calculate answer
    // using formula
    // 2^n*(n^2 + n + 2) - 1
    int ans = n * n;

    // whenever answer is
    // greater than or equals
    // to mod then modulo it.
    if (ans >= mod)
        ans %= mod;

    ans += n + 2;

    if (ans >= mod)
        ans %= mod;

    ans = (power(2, n, mod) % mod *
                 ans % mod) % mod;

    // adding modulo while
    // subtraction is very
    // necessary otherwise it
    // will cause wrong answer
    ans = (ans - 1 + mod) % mod;

    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int n = 4;

    // function call
    Console.WriteLine(check(n));
}
}

// This code is contributed
// by ankita_saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Sum
// of all subsets of a set
// formed by first N natural
// numbers | Set-2

// modulo value

// Iterative Function to
// calculate (x^y)%p in O(log y)
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it
                  // is more than or
                  // equal to p

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with the result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// function to find ff(n)
function check($n)
{
    $mod = 1e9+7;

    // In formula n is
    // starting from zero
    $n--;

    // calculate answer using
    // formula 2^n*(n^2 + n + 2) - 1
    $ans = $n * $n;

    // whenever answer is greater
    // than or equals to mod then
    // modulo it.
    if ($ans >= $mod)
        $ans %= $mod;

    $ans += $n + 2;

    if ($ans >= $mod)
        $ans %= $mod;

    $ans = (power(2, $n, $mod) %
                   $mod * $ans %
                   $mod) % $mod;

    // adding modulo while subtraction
    // is very necessary otherwise it
    // will cause wrong answer
    $ans = ($ans - 1 + $mod) % $mod;

    return $ans;
}

// Driver code
$n = 4;

// function call
echo check($n) ."\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// javascript program to find Sum of all
// subsets of a set formed by
// first N natural numbers | Set-2

// modulo value
const mod = (1e9 + 7);

// Iterative Function to calculate (x^y)%p in O(log y)
function power( x,  y,  p)
{
    let res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {

        // If y is odd, multiply x with the result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// function to find ff(n)
function check( n)
{

    // In formula n is starting from zero
    n--;

    // calculate answer using
    // formula 2^n*(n^2 + n + 2) - 1
    let ans = n * n;

    // whenever answer is greater than
    // or equals to mod then modulo it.
    if (ans >= mod)
        ans %= mod;
    ans += n + 2;
    if (ans >= mod)
        ans %= mod;

    ans = (power(2, n, mod) % mod * ans % mod) % mod;

    // adding modulo while subtraction is very necessary
    // otherwise it will cause wrong answer
    ans = (ans - 1 + mod) % mod;

    return ans;
}

// Driver code
    let n = 4;

    // function call
     document.write(check(n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
111
```

**时间复杂度:** O(log n)。