# 想办法在 N 个球中排列 K 个绿球，这样收集所有 K 个绿球就需要精确的 I 个动作

> 原文:[https://www . geesforgeks . org/find-way-to-arrange-k-green-balls-in-n-balls-to-o-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-to-](https://www.geeksforgeeks.org/find-ways-to-arrange-k-green-balls-among-n-balls-such-that-exactly-i-moves-is-needed-to-collect-all-k-green-balls/)

给定两个整数 **N** 和 **K** 。有 **N** 个球排成一排。其中 **K** 为绿色，**N–K**为黑色。任务是找到排列 **N** 球的方法数量，这样一个人将需要精确的 **i ( 1 ≤ i ≤ K )** 移动来收集所有的绿色球。在一个动作中，我们可以收集任何一组连续的绿球。请注意，答案可能非常大。于是，输出答案模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** N = 5，K = 3
> **输出:** 3 6 1
> 有三种排列球的方法，这样
> 一个人只需要一次移动:
> (G，G，G，B，B)，(B，G，G，G，B)和(B，B，G，G，G，G)。
> 有六种方法来排列球，这样
> 一个人只需要两个动作:
> (G，G，B，G，B，G)，(G，G，B，G，G，B，G)，(B，G，B，G，G，G，G)，
> (G，B，G，G，G，B)，和(G，B，B，G，G)。
> 只有一种方法来排列球，这样
> 一个人只需要三个动作:(G，B，G，B，G)。
> 
> **输入:** N = 100，K = 5
> **输出:**96 18240 857280 13287840 61124064

**进场:**只需进行 **i** 招式即可收集 **K** 绿球，也就是说 **K** 绿球被黑球分隔到 **i** 位置。因此，让我们考虑如下组合。

*   首先将**N–K**黑球排成一排。
*   在这些黑球之间，从左端到右端选择 **i** 位置，并考虑在那里放置 **K** 绿球。有**<sup>N–K+1</sup>C<sub>I</sub>**的方式选择这些。
*   对于每一个选择，考虑每个间隙将分配多少个绿球。由于需要给每个分配一个或多个，因此有**<sup>K–1</sup>C<sub>I–1</sub>**的方法来确定。

因此，对于每一个 **i** ，答案都是**T3】N–K+1C<sub>I</sub>*<sup>K–1</sup>C<sub>I–1</sub>**。寻找**<sup>n</sup>C<sub>r</sub>**在此讨论。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005
#define mod (int)(1e9 + 7)

// To store the factorial and the
// factorial mod inverse of a number
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
        return (1LL * a
                * power(power(a, m1 / 2), 2))
               % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial
// of all the numbers
void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (1LL
                        * factorial[i - 1] * i)
                       % mod;
}

// Function to find the factorial
// mod inverse of all the numbers
void modinversefun()
{
    modinverse[N - 1]
        = power(factorial[N - 1], mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (1LL * modinverse[i + 1]
                         * (i + 1))
                        % mod;
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

// Function to find ways to arrange K green
// balls among N balls such that we need
// exactly i moves to collect all K green balls
void arrange_balls(int n, int k)
{
    factorialfun();
    modinversefun();

    for (int i = 1; i <= k; i++)
        cout << (1LL * binomial(n - k + 1, i)
                 * binomial(k - 1, i - 1))
                    % mod
             << " ";
}

// Driver code
int main()
{
    int n = 5, k = 3;

    // Function call
    arrange_balls(n, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100005
mod = (int)(1e9 + 7)

# To store the factorial and the
# factorial mod inverse of a number
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
        return (a * power(power(a, m1// 2), 2)) % mod;
    else :
        return power(power(a, m1 // 2), 2) % mod;

# Function to find factorial
# of all the numbers
def factorialfun() :

    factorial[0] = 1;
    for i in range(1, N) :
        factorial[i] = (factorial[i - 1] * i) % mod;

# Function to find the factorial
# mod inverse of all the numbers
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

    a = (factorial[n] *
         modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;

# Function to find ways to arrange K green
# balls among N balls such that we need
# exactly i moves to collect all K green balls
def arrange_balls(n, k) :
    factorialfun();
    modinversefun();

    for i in range(1, k + 1) :
        print((binomial(n - k + 1, i) *
               binomial(k - 1, i - 1)) % mod,
                                  end = " ");

# Driver code
if __name__ == "__main__" :

    n = 5; k = 3;

    # Function call
    arrange_balls(n, k);

# This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG{
static final int N = 100005;
static final int mod = (int)(1e9 + 7);

// To store the factorial and the
// factorial mod inverse of a number
static long []factorial = new long[N];
static long []modinverse = new long[N];

// Function to find (a ^ m1) % mod
static long power(long a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1L * a * a) % mod;
    else if (m1 %2== 1)
        return (1L * a
                * power(power(a, m1 / 2), 2))
               % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (1L
                        * factorial[i - 1] * i)
                       % mod;
}

// Function to find the factorial
// mod inverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1]
        = (int) (power(factorial[N - 1], mod - 2) % mod);

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (1 * modinverse[i + 1]
                         * (i + 1))
                        % mod;
}

// Function to return nCr
static long binomial(int n, int r)
{
    if (r > n)
        return 0;

    long a = (1L * factorial[n]
             * modinverse[n - r])
            % mod;

    a = (1 * a * modinverse[r]) % mod;
    return a;
}

// Function to find ways to arrange K green
// balls among N balls such that we need
// exactly i moves to collect all K green balls
static void arrange_balls(int n, int k)
{
    factorialfun();
    modinversefun();

    for (int i = 1; i <= k; i++)
        System.out.print((1L * binomial(n - k + 1, i)
                 * binomial(k - 1, i - 1))
                    % mod
            + " ");
}

// Driver code
public static void main(String[] args)
{
    int n = 5, k = 3;

    // Function call
    arrange_balls(n, k);

}
}

// This code contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

static readonly int N = 100005;
static readonly int mod = (int)(1e9 + 7);

// To store the factorial and the
// factorial mod inverse of a number
static long []factorial = new long[N];
static long []modinverse = new long[N];

// Function to find (a ^ m1) % mod
static long power(long a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1L * a * a) % mod;
    else if (m1 % 2 == 1)
        return (1L * a *
        power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;
    for(int i = 1; i < N; i++)
        factorial[i] = (1L * factorial[i - 1] * i) % mod;
}

// Function to find the factorial
// mod inverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = (int)(power(factorial[N - 1],
                                            mod - 2) % mod);
    for(int i = N - 2; i >= 0; i--)
        modinverse[i] = (1 * modinverse[i + 1] *
                        (i + 1)) % mod;
}

// Function to return nCr
static long binomial(int n, int r)
{
    if (r > n)
        return 0;

    long a = (1L * factorial[n] *
    modinverse[n - r]) % mod;

    a = (1 * a * modinverse[r]) % mod;
    return a;
}

// Function to find ways to arrange K green
// balls among N balls such that we need
// exactly i moves to collect all K green balls
static void arrange_balls(int n, int k)
{
    factorialfun();
    modinversefun();

    for(int i = 1; i <= k; i++)
        Console.Write((1L * binomial(n - k + 1, i) *
                            binomial(k - 1, i - 1)) %
                                   mod + " ");
}

// Driver code
public static void Main(String[] args)
{
    int n = 5, k = 3;

    // Function call
    arrange_balls(n, k);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
3 6 1
```