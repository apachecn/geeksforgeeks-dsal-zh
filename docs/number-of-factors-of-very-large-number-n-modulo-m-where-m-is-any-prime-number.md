# 极大数 N 模 M 的因子数，其中 M 是任意素数

> 原文:[https://www . geesforgeks . org/非常大数因子数 n 模 m 其中 m 是任意素数/](https://www.geeksforgeeks.org/number-of-factors-of-very-large-number-n-modulo-m-where-m-is-any-prime-number/)

给定一个很大的数 N，任务是求数 N 模 M 的因子总数，其中 M 是任意素数。
**例:**

> **输入:** N = 9699690，M = 17
> **输出:** 1
> **说明:**
> 9699690 的因子总数为 256 和(256 % 17) = 1
> **输入:** N = 193748576239475639，M = 9
> **输出:**8【T11

## [推荐:请先在 ***<u>{IDE}</u>*** 上尝试您的方法，然后再进入解决方案。](https://ide.geeksforgeeks.org/)

**一个数的因子的定义:**
在数学中，一个整数 N 的因子也叫 N 的除数，是一个可以乘以某个整数产生 N 的整数 M。
任何数都可以写成:

> n =(P1<sup>A1</sup>)*(P2<sup>A2</sup>)*(P3<sup>A3</sup>)…。(Pn <sup>An</sup> )

其中 P1、P2、P3…Pn 是不同的素数，A1、A2、A3…An 是对应素数出现的次数。
给定数的因子总数的通式为:

> 因子=(1+A1)*(1+A2)*(1+A3)*……(1+An)

其中 A1、A2、A3、… An 是 n 的不同质因数的计数。
这里[筛的实现](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)不能用于寻找大数的质因数分解，因为它需要比例空间。
**进场:**

1.  计算次数 **2** 是给定数 n 的因子
2.  从 **3** 到 **√(N)** 迭代，求一个素数除以一个特定数的次数，每次减 **N / i** 。
3.  将数字 **N** 除以其对应的最小质因数，直到 **N 变为 1** 。
4.  利用公式
    求出该数的因子数

> 因子=(1+A1)*(1+A2)*(1+A3)*……(1+An)

下面是上述方法的实现。

## C++

```
// C++ implementation to find the
// Number of factors of very
// large number N modulo M

#include <bits/stdc++.h>
using namespace std;

#define ll long long
ll mod = 1000000007;

// Function for modular
// multiplication
ll mult(ll a, ll b)
{
    return ((a % mod) *
        (b % mod)) % mod;
}

// Function to find the number
// of factors of large Number N
ll calculate_factors(ll n)
{
    ll ans, cnt;
    cnt = 0;
    ans = 1;

    // Count the number of times
    // 2 divides the number N
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    // Condition to check
    // if 2 divides it
    if (cnt) {
        ans = mult(ans, (cnt + 1));
    }

    // Check for all the possible
    // numbers that can divide it
    for (int i = 3; i <= sqrt(n);
                         i += 2) {
        cnt = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        // Condition to check if
        // prime number i divides it
        if (cnt) {
            ans = mult(ans, (cnt + 1));
        }
    }
    // Condition to check if N
    // at the end is a prime number.
    if (n > 2) {
        ans = mult(ans, (2));
    }
    return ans % mod;
}

// Driver Code
int main()
{
    ll n = 193748576239475639;
    mod = 17;

    cout << calculate_factors(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Number of factors of very
// large number N modulo M
class GFG{

static long  mod = 1000000007L;

// Function for modular
// multiplication
static long  mult(long  a, long  b)
{
    return ((a % mod) *
        (b % mod)) % mod;
}

// Function to find the number
// of factors of large Number N
static long  calculate_factors(long  n)
{
    long  ans, cnt;
    cnt = 0;
    ans = 1;

    // Count the number of times
    // 2 divides the number N
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    // Condition to check
    // if 2 divides it
    if (cnt % 2 == 1) {
        ans = mult(ans, (cnt + 1));
    }

    // Check for all the possible
    // numbers that can divide it
    for (int i = 3; i <= Math.sqrt(n);
                         i += 2) {
        cnt = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        // Condition to check if
        // prime number i divides it
        if (cnt % 2 == 1) {
            ans = mult(ans, (cnt + 1));
        }
    }
    // Condition to check if N
    // at the end is a prime number.
    if (n > 2) {
        ans = mult(ans, (2));
    }
    return ans % mod;
}

// Driver Code
public static void main(String[] args)
{
    long  n = 193748576239475639L;
    mod = 17;

    System.out.print(calculate_factors(n) +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# Number of factors of very
# large number N modulo M
from math import sqrt

mod = 1000000007

# Function for modular
# multiplication
def mult(a, b):
    return ((a % mod) * (b % mod)) % mod

# Function to find the number
# of factors of large Number N
def calculate_factors(n):
    cnt = 0
    ans = 1

    # Count the number of times
    # 2 divides the number N
    while (n % 2 == 0):
        cnt += 1
        n = n // 2

    # Condition to check
    # if 2 divides it
    if (cnt):
        ans = mult(ans, (cnt + 1))

    # Check for all the possible
    # numbers that can divide it
    for i in range(3, int(sqrt(n)), 2):
        cnt = 0

        # Loop to check the number
        # of times prime number
        # i divides it
        while (n % i == 0):
            cnt += 1
            n = n // i

        # Condition to check if
        # prime number i divides it
        if (cnt):
            ans = mult(ans, (cnt + 1))

    # Condition to check if N
    # at the end is a prime number.
    if (n > 2):
        ans = mult(ans, 2)
    return ans % mod

# Driver Code
if __name__ == '__main__':
    n = 19374857
    mod = 17

    print(calculate_factors(n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find the
// Number of factors of very
// large number N modulo M
using System;

class GFG{

static long  mod = 1000000007L;

// Function for modular
// multiplication
static long  mult(long  a, long  b)
{
    return ((a % mod) *
        (b % mod)) % mod;
}

// Function to find the number
// of factors of large Number N
static long  calculate_factors(long  n)
{
    long  ans, cnt;
    cnt = 0;
    ans = 1;

    // Count the number of times
    // 2 divides the number N
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    // Condition to check
    // if 2 divides it
    if (cnt % 2 == 1) {
        ans = mult(ans, (cnt + 1));
    }

    // Check for all the possible
    // numbers that can divide it
    for (int i = 3; i <= Math.Sqrt(n);
                         i += 2) {
        cnt = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        // Condition to check if
        // prime number i divides it
        if (cnt % 2 == 1) {
            ans = mult(ans, (cnt + 1));
        }
    }

    // Condition to check if N
    // at the end is a prime number.
    if (n > 2) {
        ans = mult(ans, (2));
    }
    return ans % mod;
}

// Driver Code
public static void Main(String[] args)
{
    long  n = 193748576239475639L;
    mod = 17;

    Console.Write(calculate_factors(n) +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// javascript implementation to find the
// Number of factors of very
// large number N modulo M

mod = 1000000007;

// Function for modular
// multiplication
function  mult( a ,  b)
{
    return ((a % mod) *
        (b % mod)) % mod;
}

// Function to find the number
// of factors of large Number N
function  calculate_factors( n)
{
    var  ans, cnt;
    cnt = 0;
    ans = 1;

    // Count the number of times
    // 2 divides the number N
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    // Condition to check
    // if 2 divides it
    if (cnt % 2 == 1) {
        ans = mult(ans, (cnt + 1));
    }

    // Check for all the possible
    // numbers that can divide it
    for (i = 3; i <= Math.sqrt(n);
                         i += 2) {
        cnt = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        // Condition to check if
        // prime number i divides it
        if (cnt % 2 == 1) {
            ans = mult(ans, (cnt + 1));
        }
    }
    // Condition to check if N
    // at the end is a prime number.
    if (n > 2) {
        ans = mult(ans, (2));
    }
    return ans % mod;
}

// Driver Code
var  n = 193748576239475639;
mod = 17;

document.write(calculate_factors(n));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(sqrt(N))
**辅助空间** : O(1)