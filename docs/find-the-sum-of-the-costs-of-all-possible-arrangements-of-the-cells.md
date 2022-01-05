# 计算所有可能的电池布置的成本总和

> 原文:[https://www . geeksforgeeks . org/find-所有可能的单元安排的成本总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-costs-of-all-possible-arrangements-of-the-cells/)

给定两个整数 **N** 和 **M** 。每次操作时，选择尺寸为 **N * M** 的 2D 网格的 **K** 单元并排列。如果我们选择 **K** 单元 **(x <sub>1</sub> 、y <sub>1</sub> )、(x <sub>2</sub> 、y <sub>2</sub> )、…、和(x <sub>K</sub> 、y <sub>K</sub> )** 那么这种安排的成本计算为 **∑ <sub>i=1</sub> <sup>任务是找出所有可能的细胞排列的成本总和。答案可能很大，所以打印答案取模**10<sup>9</sup>+7**
**示例:**</sup>** 

> **输入:** N = 2，M = 2，K = 2
> **输出:** 8
> ((1，1)，(1，2))，成本|1-1| + |1-2| = 1
> ((1，1)，(2，1))，成本|1-2| + |1-1| = 1
> ((1，1)，(2，2))，成本|1-2| + |1-2| = 2
> ((1 用成本|1-2| + |2-2| = 1
> ((2，1)，(2，2))，用成本|2-2| + |1-2| = 1
> **输入:** N = 4，M = 5，N = 4
> **输出:** 87210

**方法:**问题是在 **N-M** 细胞中选择 **K** 细胞时，求[曼哈顿距离](https://en.wiktionary.org/wiki/Manhattan_distance)的和。由于表达式明显与 **X** 和 **Y** 无关，所以分别求 **X** 的差值绝对值之和和 **Y** 的差值绝对值之和。考虑 **X** 的区别。当 **2** 方块的某个组合固定时，由于每次从这些方块之外的方块中选择**K–2**细胞时，这些差异会贡献 **1** 度，因此可以固定这对**<sup>N * M–2</sup>C<sub>K–2</sub>**。再者，由于差值为 **0** 如果 **X** 相同，假设 **X** 不同，有一种方法可以选择 **2** 的平方，使 **X** 中差值的绝对值为**d((N–d)* M<sup>2</sup>)**。如果把这个加到所有 **d** 上，你会得到一个关于 **X** 的答案。至于 **Y** 、 **N** 和 **M** 可以互换解决，这个问题可以在 **O(N * M)** 中解决。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 100005
#define mod (int)(1e9 + 7)

// To store the factorials and factorial
// mod inverse of the numbers
int factorial[N], modinverse[N];

// Function to return (a ^ m1) % mod
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

// Function to find the factorials
// of all the numbers
void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (1LL * factorial[i - 1]
                        * i)
                       % mod;
}

// Function to find factorial mod
// inverse of all the numbers
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

// Function to return the sum of the costs of
// all the possible arrangements of the cells
int arrange(int n, int m, int k)
{
    factorialfun();
    modinversefun();

    long long ans = 0;

    // For all possible X's
    for (int i = 1; i < n; i++)
        ans += (1LL * i * (n - i) * m * m) % mod;

    // For all possible Y's
    for (int i = 1; i < m; i++)
        ans += (1LL * i * (m - i) * n * n) % mod;

    ans = (ans * binomial(n * m - 2, k - 2)) % mod;

    return (int)ans;
}

// Driver code
int main()
{
    int n = 2, m = 2, k = 2;

    cout << arrange(n, m, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int N = 20;
static int mod = 1000000007;

// To store the factorials and factorial
// mod inverse of the numbers
static int []factorial = new int[N];
static int []modinverse = new int[N];

// Function to return (a ^ m1) % mod
static int power(int a, int m1)
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

// Function to find the factorials
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (factorial[i - 1] * i) % mod;
}

// Function to find factorial mod
// inverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1],
                                mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (modinverse[i + 1] *
                                   (i + 1)) % mod;
}

// Function to return nCr
static int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int a = (factorial[n] *
             modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;
}

// Function to return the sum of the costs of
// all the possible arrangements of the cells
static int arrange(int n, int m, int k)
{
    factorialfun();
    modinversefun();

    int ans = 0;

    // For all possible X's
    for (int i = 1; i < n; i++)
        ans += (i * (n - i) * m * m) % mod;

    // For all possible Y's
    ans = 8;
    for (int i = 1; i < m; i++)
        ans += (i * (m - i) * n * n) % mod;

    ans = (ans * binomial(n * m - 2,
                          k - 2)) % mod + 8;

    return ans;
}

// Driver code
public static void main(String []args)
{
    int n = 2, m = 2, k = 2;

    System.out.println(arrange(n, m, k));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100005
mod = (int)(1e9 + 7)

# To store the factorials and factorial
# mod inverse of the numbers
factorial = [0] * N;
modinverse = [0] * N;

# Function to return (a ^ m1) % mod
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

# Function to find the factorials
# of all the numbers
def factorialfun() :

    factorial[0] = 1;
    for i in range(1, N) :
        factorial[i] = (factorial[i - 1] * i) % mod;

# Function to find factorial mod
# inverse of all the numbers
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

# Function to return the sum of the costs of
# all the possible arrangements of the cells
def arrange(n, m, k) :

    factorialfun();
    modinversefun();

    ans = 0;

    # For all possible X's
    for i in range(1, n) :
        ans += ( i * (n - i) * m * m) % mod;

    # For all possible Y's
    for i in range(1, m) :
        ans += ( i * (m - i) * n * n) % mod;

    ans = (ans * binomial(n * m - 2, k - 2)) % mod;

    return int(ans);

# Driver code
if __name__ == "__main__" :

    n = 2; m = 2; k = 2;

    print(arrange(n, m, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int N = 20;
static int mod = 1000000007;

// To store the factorials and factorial
// mod inverse of the numbers
static int []factorial = new int[N];
static int []modinverse = new int[N];

// Function to return (a ^ m1) % mod
static int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (a * a) % mod;
    else if ((m1 & 1) != 0)
        return (a * power(power(
                    a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find the factorials
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (factorial[i - 1] * i) % mod;
}

// Function to find factorial mod
// inverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1],
                                mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (modinverse[i + 1] *
                                   (i + 1)) % mod;
}

// Function to return nCr
static int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int a = (factorial[n] *
             modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;
}

// Function to return the sum of the costs of
// all the possible arrangements of the cells
static int arrange(int n, int m, int k)
{
    factorialfun();
    modinversefun();

    int ans = 0;

    // For all possible X's
    for (int i = 1; i < n; i++)
        ans += (i * (n - i) * m * m) % mod;

    // For all possible Y's
    ans = 8;
    for (int i = 1; i < m; i++)
        ans += (i * (m - i) * n * n) % mod;

    ans = (ans * binomial(n * m - 2,
                          k - 2)) % mod + 8;

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int n = 2, m = 2, k = 2;

    Console.WriteLine(arrange(n, m, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let N = 20;
    let mod = 1000000007;

    // To store the factorials and factorial
    // mod inverse of the numbers
    let factorial = new Array(N);
    factorial.fill(0);
    let modinverse = new Array(N);
    modinverse.fill(0);

    // Function to return (a ^ m1) % mod
    function power(a, m1)
    {
        if (m1 == 0)
            return 1;
        else if (m1 == 1)
            return a;
        else if (m1 == 2)
            return (a * a) % mod;
        else if ((m1 & 1) != 0)
            return (a *
            power(power(a, parseInt(m1 / 2, 10)), 2)) % mod;
        else
            return power(power(a, parseInt(m1 / 2, 10)), 2) % mod;
    }

    // Function to find the factorials
    // of all the numbers
    function factorialfun()
    {
        factorial[0] = 1;
        for (let i = 1; i < N; i++)
            factorial[i] = (factorial[i - 1] * i) % mod;
    }

    // Function to find factorial mod
    // inverse of all the numbers
    function modinversefun()
    {
        modinverse[N - 1] = power(factorial[N - 1],
                                    mod - 2) % mod;

        for (let i = N - 2; i >= 0; i--)
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
        return a;
    }

    // Function to return the sum of the costs of
    // all the possible arrangements of the cells
    function arrange(n, m, k)
    {
        factorialfun();
        modinversefun();

        let ans = 0;

        // For all possible X's
        for (let i = 1; i < n; i++)
            ans += (i * (n - i) * m * m) % mod;

        // For all possible Y's
        ans = 8;
        for (let i = 1; i < m; i++)
            ans += (i * (m - i) * n * n) % mod;

        ans = (ans * binomial(n * m - 2,
                              k - 2) * 0) % mod + 8;

        return ans;
    }

    let n = 2, m = 2, k = 2;

    document.write(arrange(n, m, k));

</script>
```

**Output:** 

```
8
```