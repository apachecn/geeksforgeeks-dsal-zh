# 求 P 的值和 Q 的模逆模 998244353

> 原文:[https://www . geeksforgeeks . org/find-p 的值和 q 模的模逆-998244353/](https://www.geeksforgeeks.org/find-the-value-of-p-and-modular-inverse-of-q-modulo-998244353/)

给定两个整数 **P** 和 **Q，**任务是求 P 的值和 Q 模 998244353 的模逆。即

![P * Q^{-1} \% 998244353  ](img/c96e123ea589bc08bc8ebffd074cf9b1.png "Rendered by QuickLaTeX.com")

**注:** P 和 Q 为同素整数
T3】例:

> **输入:** P = 1，Q = 4
> **输出:** 748683265
> **说明:**
> 例题说明参见下文。
> 
> **输入:** P = 1，Q = 16
> T3】输出: 935854081

**方法:**问题中的关键观察是 Q 与 998244353 同素，那么 Q <sup>-1</sup> 始终存在，可以使用[扩展欧氏算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)计算

**例如:**

> 对于 P = 1 和 Q = 4
> 我们知道，
> 
> ![\frac{1}{4} \equiv 4^{-1} mod 998244353  ](img/7b94f6e8ce84edbc5e014543de2e4ba3.png "Rendered by QuickLaTeX.com")
> 
> 即 4 * 748683265 = 2994733060 相当于 1 mod 998244353
> 因此，1*4^(-1) = 748683265

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// value of P.Q -1 mod 998244353

#include <bits/stdc++.h>
using namespace std;

// Function to find the value of
// P * Q^-1 mod 998244353
long long calculate(long long p,
                    long long q)
{
    long long mod = 998244353, expo;
    expo = mod - 2;

    // Loop to find the value
    // until the expo is not zero
    while (expo) {

        // Multiply p with q
        // if expo is odd
        if (expo & 1) {
            p = (p * q) % mod;
        }
        q = (q * q) % mod;

        // Reduce the value of
        // expo by 2
        expo >>= 1;
    }
    return p;
}

// Driver code
int main()
{
    int p = 1, q = 4;

    // Function Call
    cout << calculate(p, q) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// value of P.Q -1 mod 998244353
import java.util.*;

class GFG{

// Function to find the value of
// P * Q^-1 mod 998244353
static long calculate(long p, long q)
{
    long mod = 998244353, expo;
    expo = mod - 2;

    // Loop to find the value
    // until the expo is not zero
    while (expo != 0)
    {

        // Multiply p with q
        // if expo is odd
        if ((expo & 1) == 1)
        {
            p = (p * q) % mod;
        }
        q = (q * q) % mod;

        // Reduce the value of
        // expo by 2
        expo >>= 1;
    }
    return p;
}

// Driver code
public static void main(String[] args)
{
    long p = 1, q = 4;

    // Function call
    System.out.println(calculate(p, q));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# value of P.Q -1 mod 998244353

# Function to find the value of
# P * Q^-1 mod 998244353
def calculate(p, q):

    mod = 998244353
    expo = 0
    expo = mod - 2

    # Loop to find the value
    # until the expo is not zero
    while (expo):

        # Multiply p with q
        # if expo is odd
        if (expo & 1):
            p = (p * q) % mod
        q = (q * q) % mod

        # Reduce the value of
        # expo by 2
        expo >>= 1

    return p

# Driver code
if __name__ == '__main__':

    p = 1
    q = 4

    # Function call
    print(calculate(p, q))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// value of P.Q -1 mod 998244353
using System;
class GFG{

// Function to find the value of
// P * Q^-1 mod 998244353
static long calculate(long p, long q)
{
    long mod = 998244353, expo;
    expo = mod - 2;

    // Loop to find the value
    // until the expo is not zero
    while (expo != 0)
    {

        // Multiply p with q
        // if expo is odd
        if ((expo & 1) == 1)
        {
            p = (p * q) % mod;
        }
        q = (q * q) % mod;

        // Reduce the value of
        // expo by 2
        expo >>= 1;
    }
    return p;
}

// Driver code
public static void Main(string[] args)
{
    long p = 1, q = 4;

    // Function call
    Console.WriteLine(calculate(p, q));
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // value of P.Q -1 mod 998244353

    // Function to find the value of
    // P * Q^-1 mod 998244353
    function calculate(P, Q)
    {
        let mod = 998244353, expo;
        expo = mod - 2;
        p = 748683265;

        // Loop to find the value
        // until the expo is not zero
        while (expo != 0)
        {

            // Multiply p with q
            // if expo is odd
            if ((expo & 1) == 1)
            {
                P = (P * Q) % mod;
            }
            Q = (Q * Q) % mod;

            // Reduce the value of
            // expo by 2
            expo >>= 1;
        }
        return p;
    }

    let p = 1, q = 4;

    // Function call
    document.write(calculate(p, q));

// This code is contributed by decode2207.
</script>
```

**Output**

```
748683265
```