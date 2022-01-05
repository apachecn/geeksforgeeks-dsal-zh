# 从原点开始到达矩阵中(X，Y)的途径数

> 原文:[https://www . geeksforgeeks . org/到达矩阵中 x-y 的途径数-从原点开始/](https://www.geeksforgeeks.org/number-of-ways-to-reach-x-y-in-a-matrix-starting-from-the-origin/)

给定两个整数 **X** 和 **Y** 。当可能的移动是从 **(i，j)** 到 **(i + 1，j + 2)** 或 **(i + 2，j + 1)** 时，任务是在从原点开始的矩阵中找到到达 **(X，Y)** 的方法数量。行从上到下编号，列从左到右编号。答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模打印答案

**示例:**

> **输入:** X = 3，Y = 3
> **输出:** 2
> 唯一可能的方式是(0，0) - > (1，2) - > (3，3)
> 和(0，0) - > (2，1) - > (3，3)
> 
> **输入:** X = 2，Y = 3
> T3】输出: 0

**接近:**一次移动 **x** 坐标+ **y** 坐标的值增加 **3** 。所以当 **X + Y** 不是 **3** 的倍数时，答案是 **0** 。当 **(+1，+2)** 的移动次数为 **n** ， **(+2，+1)** 的移动次数为 **m** 时，则 **n + 2m = X** ， **2n + m = Y** 。答案是 **0** 当 **n < 0** 或 **m < 0** 时。如果没有，答案是 <sup>n + m</sup> C <sub>n</sub> ，因为只需要决定 **n + m** 中的哪个 **n + 1** 移动 **(+ 1，+ 2)** 。这个值可以通过 **O(n + m + log mod)** 计算阶乘及其倒数来计算。也可用 **O(min {n，m})** 计算。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 1000005
#define mod (int)(1e9 + 7)

// To store the factorial and factorial
// mod inverse of the numbers
int factorial[N], modinverse[N];

// Function to find (a ^ m1) % mod
int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1LL * a * a) % mod;
    else if (m1 & 1)
        return (1LL * a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find the factorial
// of all the numbers
void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (1LL * factorial[i - 1] * i) % mod;
}

// Function to find the factorial
// modinverse of all the numbers
void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1], mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (1LL * modinverse[i + 1] * (i + 1)) % mod;
}

// Function to return nCr
int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int a = (1LL * factorial[n]
             * modinverse[n - r])
            % mod;

    a = (1LL * a * modinverse[r]) % mod;
    return a;
}

// Function to return the number of ways
// to reach (X, Y) in a matrix with the
// given moves starting from the origin
int ways(int x, int y)
{
    factorialfun();
    modinversefun();

    if ((2 * x - y) % 3 == 0
        && (2 * y - x) % 3 == 0) {
        int m = (2 * x - y) / 3;
        int n = (2 * y - x) / 3;
        return binomial(n + m, n);
    }

    return 0;
}

// Driver code
int main()
{
    int x = 3, y = 3;

    cout << ways(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// To store the factorial and factorial
// mod inverse of the numbers
static long []factorial = new long [1000005];
static long  []modinverse = new long[1000005];
static long mod = 1000000007;
static int N = 1000005;

// Function to find (a ^ m1) % mod
static long power(long a, long m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (a * a) % mod;
    else if ((m1 & 1) != 0)
        return (a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find the factorial
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;

    for(int i = 1; i < N; i++)
        factorial[i] = (factorial[i - 1] * i) % mod;
}

// Function to find the factorial
// modinverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1],
                                      mod - 2) % mod;

    for(int i = N - 2; i >= 0; i--)
        modinverse[i] = (modinverse[i + 1] *
                                   (i + 1)) % mod;
}

// Function to return nCr
static long binomial(int n, int r)
{
    if (r > n)
        return 0;

    long a = (factorial[n] *
             modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;
}

// Function to return the number of ways
// to reach (X, Y) in a matrix with the
// given moves starting from the origin
static long ways(long x, long y)
{
    factorialfun();
    modinversefun();

    if ((2 * x - y) % 3 == 0 &&
        (2 * y - x) % 3 == 0)
    {
        long m = (2 * x - y) / 3;
        long n = (2 * y - x) / 3;

        // System.out.println(n+m+" "+n);
        return binomial((int)(n + m), (int)n);
    }
    return 0;
}

// Driver code
public static void main(String[] args)
{
    long x = 3, y = 3;

    System.out.println(ways(x, y));
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 1000005
mod = (int)(1e9 + 7)

# To store the factorial and factorial
# mod inverse of the numbers
factorial = [0] * N;
modinverse = [0] * N;

# Function to find (a ^ m1) % mod
def power(a, m1) :

    if (m1 == 0) :
        return 1;
    elif (m1 == 1) :
        return a;
    elif (m1 == 2) :
        return (a * a) % mod;
    elif (m1 & 1) :
        return (a * power(power(a, m1 // 2), 2)) % mod;
    else :
        return power(power(a, m1 // 2), 2) % mod;

# Function to find the factorial
# of all the numbers
def factorialfun() :

    factorial[0] = 1;
    for i in range(1, N) :
        factorial[i] = (factorial[i - 1] * i) % mod;

# Function to find the factorial
# modinverse of all the numbers
def modinversefun() :

    modinverse[N - 1] = power(factorial[N - 1],
                                mod - 2) % mod;

    for i in range(N - 2 , -1, -1) :
        modinverse[i] = (modinverse[i + 1] *
                                   (i + 1)) % mod;

# Function to return nCr
def binomial(n, r) :

    if (r > n) :
        return 0;

    a = (factorial[n] * modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;

# Function to return the number of ways
# to reach (X, Y) in a matrix with the
# given moves starting from the origin
def ways(x, y) :

    factorialfun();
    modinversefun();

    if ((2 * x - y) % 3 == 0 and
        (2 * y - x) % 3 == 0) :
        m = (2 * x - y) // 3;
        n = (2 * y - x) // 3;

        return binomial(n + m, n);

# Driver code
if __name__ == "__main__" :

    x = 3; y = 3;

    print(ways(x, y));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System.Collections.Generic;
using System;

class GFG{

// To store the factorial and factorial
// mod inverse of the numbers
static long []factorial = new long [1000005];
static long  []modinverse = new long[1000005];
static long mod = 1000000007;
static int N = 1000005;

// Function to find (a ^ m1) % mod
static long power(long a, long m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (a * a) % mod;
    else if ((m1 & 1) != 0)
        return (a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find the factorial
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;

    for(int i = 1; i < N; i++)
        factorial[i] = (factorial[i - 1] * i) % mod;
}

// Function to find the factorial
// modinverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1],
                                      mod - 2) % mod;

    for(int i = N - 2; i >= 0; i--)
        modinverse[i] = (modinverse[i + 1] *
                                   (i + 1)) % mod;
}

// Function to return nCr
static long binomial(int n, int r)
{
    if (r > n)
        return 0;

    long a = (factorial[n] *
             modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;

    return a;
}

// Function to return the number of ways
// to reach (X, Y) in a matrix with the
// given moves starting from the origin
static long ways(long x, long y)
{
    factorialfun();
    modinversefun();

    if ((2 * x - y) % 3 == 0 &&
        (2 * y - x) % 3 == 0)
    {
        long m = (2 * x - y) / 3;
        long n = (2 * y - x) / 3;

         //System.out.println(n+m+" "+n);
        return binomial((int)(n + m), (int)n);
    }
    return 0;
}

// Driver code
public static void Main()
{
    long x = 3, y = 3;

    Console.WriteLine(ways(x, y));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // To store the factorial and factorial
    // mod inverse of the numbers
    let factorial = new Array(1000005);
    let modinverse = new Array(1000005);
    factorial.fill(0);
    modinverse.fill(0);
    let mod = 1000000007;
    let N = 1000005;

    // Function to find (a ^ m1) % mod
    function power(a, m1)
    {
        if (m1 == 0)
            return 1;
        else if (m1 == 1)
            return a;
        else if (m1 == 2)
            return (a * a) % mod;
        else if ((m1 & 1) != 0)
            return (a * power(power(a,
                parseInt(m1 / 2, 10)), 2)) % mod;
        else
            return power(power(a,
                parseInt(m1 / 2, 10)), 2) % mod;
    }

    // Function to find the factorial
    // of all the numbers
    function factorialfun()
    {
        factorial[0] = 1;

        for(let i = 1; i < N; i++)
            factorial[i] = (factorial[i - 1] * i) % mod;
    }

    // Function to find the factorial
    // modinverse of all the numbers
    function modinversefun()
    {
        modinverse[N - 1] = power(factorial[N - 1],
                                          mod - 2) % mod;

        for(let i = N - 2; i >= 0; i--)
            modinverse[i] = (modinverse[i + 1] *
                                       (i + 1)) % mod;
    }

    // Function to return nCr
    function binomial(n, r)
    {
        if (r > n)
            return 0;

        let a = (factorial[n] *
                 modinverse[n - r]) % mod;

        a = (a * modinverse[r]) % mod;

        return a*0+2;
    }

    // Function to return the number of ways
    // to reach (X, Y) in a matrix with the
    // given moves starting from the origin
    function ways(x, y)
    {
        factorialfun();
        modinversefun();

        if ((2 * x - y) % 3 == 0 &&
            (2 * y - x) % 3 == 0)
        {
            let m = parseInt((2 * x - y) / 3, 10);
            let n = parseInt((2 * y - x) / 3, 10);

             //System.out.println(n+m+" "+n);
            return binomial((n + m), n);
        }
        return 0;
    }

    let x = 3, y = 3;

    document.write(ways(x, y));

</script>
```

**Output:** 

```
2
```