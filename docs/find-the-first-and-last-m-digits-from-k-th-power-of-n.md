# 从 N 的 K 次幂中找出第一个和最后一个 M 位

> 原文:[https://www . geesforgeks . org/find-第 k 次幂 n 的第一个和最后一个 m 位数/](https://www.geeksforgeeks.org/find-the-first-and-last-m-digits-from-k-th-power-of-n/)

给定一个两个整数 **N** 和 **K** ，任务是找到数字**N<sup>K</sup>T11】的第一个 **M** 和最后一个 **M** 位数。
**示例:**** 

> **输入:** N = 2345，K = 3，M = 3
> **输出:** 128 625
> **说明:**
> 2345<sup>3</sup>=**128**95213**625**
> 因此，前 M(= 3)位为 128，后三位为 625。
> **输入:** N = 12，K = 12，M = 4
> **输出:** 8916 8256
> **解释:**
> 12<sup>12</sup>=**8916**10044**8256**

**天真法:**
解决问题最简单的方法就是计算 **N <sup>K</sup>** 的值，迭代到第一个 **M** 位，通过**N<sup>K</sup>mod 10<sup>M</sup>**找到最后的 M 位。
***时间复杂度:** O(K)*
***辅助空间:** O(1)*
**高效途径:**
通过以下观察可以优化上述途径:

> 让我们考虑一个数字 **x** ，可以写成**10<sup>y</sup>T5<sup>T7【其中 y 是十进制数。
> 让 x = N<sup>K</sup>
> N<sup>K</sup>= 10<sup>y</sup>
> 取上述表达式两边的**log<sub>10</sub>T20】，我们得到:
> K * log<sub>10</sub>(N)= log<sub>10</sub>(10<sup>y</sup>)
> =
> xyz—**
> 因此，
> N <sup>K</sup> = 10 <sup>abc—。XYZ—</sup>
> =>N<sup>K</sup>= 10<sup>ABC—+0 . XYZ—</sup>
> =>N<sup>K</sup>= 10<sup>ABC—</sup>* 10<sup>0 . XYZ—</sup>
> 在上式中，10 <sup>abc—</sup> 只向前移动小数点。
> 通过计算 10 <sup>0.xyz—</sup> ，向前移动小数点可以算出第一个 **M** 位。</sup>**

按照以下步骤解决问题:

*   通过计算[**(N<sup>K</sup>)mod(10<sup>M</sup>)**](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)找到**N<sup>K</sup>T5 的前 **M** 位。**
*   计算 **K * log <sub>10</sub> (N)** 。
*   计算**10<sup>K * log</sup><sub><sup>10</sup></sub><sup>(N)</sup>**。
*   通过计算**10<sup>K * log</sup>T5<sup>10</sup><sup>(N)</sup>* 10<sup>M–1</sup>**找到第一个 **M** 数字。
*   打印获得的第一个和最后一个 **M** 数字。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find a^b modulo M
ll modPower(ll a, ll b, ll M)
{
    ll res = 1;
    while (b) {
        if (b & 1)
            res = res * a % M;
        a = a * a % M;
        b >>= 1;
    }
    return res;
}

// Function to find the first and last
// M digits from N^K
void findFirstAndLastM(ll N, ll K, ll M)
{
    // Calculate Last M digits
    ll lastM
        = modPower(N, K, (1LL) * pow(10, M));

    // Calculate First M digits
    ll firstM;

    double y = (double)K * log10(N * 1.0);

    // Extract the number after decimal
    y = y - (ll)y;

    // Find 10 ^ y
    double temp = pow(10.0, y);

    // Move the Decimal Point M - 1 digits forward
    firstM = temp * (1LL) * pow(10, M - 1);

    // Print the result
    cout << firstM << " " << lastM << endl;
}

// Driver Code
int main()
{
    ll N = 12, K = 12, M = 4;

    findFirstAndLastM(N, K, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find a^b modulo M
static long modPower(long a, long b, long M)
{
    long res = 1;
    while (b > 0)
    {
        if (b % 2 == 1)
            res = res * a % M;

        a = a * a % M;
        b >>= 1;
    }
    return res;
}

// Function to find the first and last
// M digits from N^K
static void findFirstAndLastM(long N, long K,
                              long M)
{

    // Calculate Last M digits
    long lastM = modPower(N, K, (1L) *
                 (long)Math.pow(10, M));

    // Calculate First M digits
    long firstM;

    double y = (double)K * Math.log10(N * 1.0);

    // Extract the number after decimal
    y = y - (long)y;

    // Find 10 ^ y
    double temp = Math.pow(10.0, y);

    // Move the Decimal Point M - 1 digits forward
    firstM = (long)(temp * (1L) *
             Math.pow(10, (M - 1)));

    // Print the result
    System.out.print(firstM + " " +
                      lastM + "\n");
}

// Driver Code
public static void main(String[] args)
{
    long N = 12, K = 12, M = 4;

    findFirstAndLastM(N, K, M);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import *

# Function to find a^b modulo M
def modPower(a, b, M):

    res = 1
    while (b):
        if (b & 1):
            res = res * a % M

        a = a * a % M
        b >>= 1

    return res

# Function to find the first and
# last M digits from N^K
def findFirstAndLastM(N, K, M):

    # Calculate Last M digits
    lastM = modPower(N, K, int(pow(10, M)))

    # Calculate First M digits
    firstM = 0

    y = K * log10(N * 1.0)

    # Extract the number after decimal
    y = y - int(y)

    # Find 10 ^ y
    temp = pow(10.0, y)

    # Move the Decimal Point M - 1
    # digits forward
    firstM = int(temp * pow(10, M - 1))

    # Print the result
    print(firstM, lastM)

# Driver Code
N = 12
K = 12
M = 4

findFirstAndLastM(N, K, M)

# This code is contributed by himanshu77
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find a^b modulo M
static long modPower(long a, long b, long M)
{
    long res = 1;
    while (b > 0)
    {
        if (b % 2 == 1)
            res = res * a % M;

        a = a * a % M;
        b >>= 1;
    }
    return res;
}

// Function to find the first and last
// M digits from N^K
static void findFirstAndLastM(long N, long K,
                              long M)
{

    // Calculate Last M digits
    long lastM = modPower(N, K, (1L) *
                 (long)Math.Pow(10, M));

    // Calculate First M digits
    long firstM;

    double y = (double)K * Math.Log10(N * 1.0);

    // Extract the number after decimal
    y = y - (long)y;

    // Find 10 ^ y
    double temp = Math.Pow(10.0, y);

    // Move the Decimal Point M - 1 digits forward
    firstM = (long)(temp * (1L) *
             Math.Pow(10, (M - 1)));

    // Print the result
    Console.Write(firstM + " " +
                   lastM + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    long N = 12, K = 12, M = 4;

    findFirstAndLastM(N, K, M);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to find a^b modulo M
function modPower(a, b, M)
{
    var res = 1;
    while (b) {
        if (b & 1)
            res = res * a % M;
        a = a * a % M;
        b >>= 1;
    }
    return res;
}

// Function to find the first and last
// M digits from N^K
function findFirstAndLastM(N, K, M)
{
    // Calculate Last M digits
    var lastM
        = modPower(N, K, Math.pow(10, M));

    // Calculate First M digits
    var firstM;

    var y = K * Math.log10(N * 1.0);

    // Extract the number after decimal
    y = y - parseInt(y);

    // Find 10 ^ y
    var temp = Math.pow(10.0, y);

    // Move the Decimal Point M - 1 digits forward
    firstM = temp  * Math.pow(10, M - 1);

    // Print the result
    document.write( parseInt(firstM) + " "
    + parseInt(lastM) );
}

// Driver Code
var N = 12, K = 12, M = 4;
findFirstAndLastM(N, K, M);

</script>
```

**Output:** 

```
8916 8256
```

***时间复杂度:** O(log K)*
***辅助空间:** O(1)*