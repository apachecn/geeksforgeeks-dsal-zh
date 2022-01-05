# 等式 f(n)=(2 * f(n–1))% 10^9+7

的给定第 n 项的第一项

> 原文:[https://www . geesforgeks . org/第一项从给定的第 n 项方程-fn-2-fn-1-109-7/](https://www.geeksforgeeks.org/first-term-from-given-nth-term-of-the-equation-fn-2-fn-1-109-7/)

给定一个整数 **N** 和一个整数**F<sub>N</sub>T5【表示线性方程**F(N)=(2 * F(N–1))% M**，其中 M 为 **10 <sup>9</sup> + 7** ，任务是求 **F(1)** 的值。**

**示例:**

> **输入:** N = 2，F<sub>N</sub>= 6
> T5】输出:3
> T8】说明:
> 如果 F(1) = 3，F(2) = (2 * F(1)) % M = (2 * 3) % M = 6。
> 对于 F(1) = 3，给定的线性方程满足 F(2)的值。
> 因此，F(1)的值为 3。
> 
> **输入** : N = 3，F <sub>N</sub> = 6
> **输出:** 500000005
> **说明:**
> 如果 F(1)= 500000005
> F(2)=(2 * 50000005)% M = 3
> F(3)=(2 * 3)% M = 6
> 对于 F(1)= 50005
> 因此，F(1)的值为 500000005

**天真法:**解决这个问题最简单的方法是在**【1，M–1】**范围内尝试 **F(1)** 的所有可能值，检查是否有任何值满足给定的线性方程。如果发现为真，则打印 **F(1)** 的值。

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 给定线性方程，F(N)= 2 * F(N–1)—(1)
> 将 F(N–1)= 2 * F(N–2)的值放入方程(1)
> =>F(N)= 2 *(2 * F(N–2))—(2)
> 将 F(N–2)= 2 * F(N–3)的值放入方程(2)
> =>F(N)= 2 *(2×)
> ……………………………。
> =>F(N)= 2<sup>(N–1)</sup>F(N –( N–1))= 2<sup>(N–1)</sup>F(1)
> =>F(1)= F(N)/2<sup>(N–1)</sup>

按照以下步骤解决问题:

*   在模 **M** 下计算**2<sup>(N–1)</sup>**的[模乘逆，说**modnv**。](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)
*   最后打印 **F(N) * modInv** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define M 1000000007

// Function to find the value
// of power(X, N) % M
long long power(long long x,
                long long N)
{
    // Stores the value
    // of (X ^ N) % M
    long long res = 1;

    // Calculate the value of
    // power(x, N) % M
    while (N > 0) {

        // If N is odd
        if (N & 1) {

            // Update res
            res = (res * x) % M;
        }

        // Update x
        x = (x * x) % M;

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find modulo multiplicative
// inverse of X under modulo M
long long moduloInverse(long long X)
{
    return power(X, M - 2);
}

// Function to find the value of F(1)
long long F_1(long long N,
              long long F_N)
{

    // Stores power(2, N - 1)
    long long P_2 = power(2, N - 1);

    // Stores modulo multiplicative
    // inverse of P_2 under modulo M
    long long modInv = moduloInverse(P_2);

    // Stores the value of F(1)
    long long res;

    // Update res
    res = ((modInv % M) * (F_N % M)) % M;

    return res;
}

// Driver code
int main()
{

    long long N = 3;
    long long F_N = 6;
    cout << F_1(N, F_N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static final int M = 1000000007;

// Function to find the
// value of power(X, N) % M
static long power(long x,
                  long N)
{
  // Stores the value
  // of (X ^ N) % M
  long res = 1;

  // Calculate the value
  // of power(x, N) % M
  while (N > 0)
  {
    // If N is odd
    if (N % 2 == 1)
    {
      // Update res
      res = (res * x) % M;
    }

    // Update x
    x = (x * x) % M;

    // Update N
    N = N >> 1;
  }
  return res;
}

// Function to find modulo
// multiplicative inverse
// of X under modulo M
static long moduloInverse(long X)
{
  return power(X, M - 2);
}

// Function to find the
// value of F(1)
static long F_1(long N,
                long F_N)
{
  // Stores power(2, N - 1)
  long P_2 = power(2, N - 1);

  // Stores modulo multiplicative
  // inverse of P_2 under modulo M
  long modInv = moduloInverse(P_2);

  // Stores the value of F(1)
  long res;

  // Update res
  res = ((modInv % M) *
         (F_N % M)) % M;

  return res;
}

// Driver code
public static void main(String[] args)
{
  long N = 3;
  long F_N = 6;
  System.out.print(F_1(N, F_N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
M = 1000000007

# Function to find the value
# of power(X, N) % M
def power(x, N):

    # Stores the value
    # of (X ^ N) % M
    res = 1

    # Calculate the value of
    # power(x, N) % M
    while (N > 0):

        # If N is odd
        if (N & 1):

            # Update res
            res = (res * x) % M

        # Update x
        x = (x * x) % M

        # Update N
        N = N >> 1

    return res

# Function to find modulo multiplicative
# inverse of X under modulo M
def moduloInverse(X):

    return power(X, M - 2)

#Function to find the value of F(1)
def F_1(N, F_N):

    # Stores power(2, N - 1)
    P_2 = power(2, N - 1)

    # Stores modulo multiplicative
    # inverse of P_2 under modulo M
    modInv = moduloInverse(P_2)

    # Stores the value of F(1)
    res = 0

    # Update res
    res = ((modInv % M) * (F_N % M)) % M

    return res

# Driver code
if __name__ == '__main__':

    N = 3
    F_N = 6

    print(F_1(N, F_N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static readonly int M = 1000000007;

// Function to find the
// value of power(X, N) % M
static long power(long x,
                  long N)
{
  // Stores the value
  // of (X ^ N) % M
  long res = 1;

  // Calculate the value
  // of power(x, N) % M
  while (N > 0)
  {
    // If N is odd
    if (N % 2 == 1)
    {
      // Update res
      res = (res * x) % M;
    }

    // Update x
    x = (x * x) % M;

    // Update N
    N = N >> 1;
  }
  return res;
}

// Function to find modulo
// multiplicative inverse
// of X under modulo M
static long moduloInverse(long X)
{
  return power(X, M - 2);
}

// Function to find the
// value of F(1)
static long F_1(long N,
                long F_N)
{
  // Stores power(2, N - 1)
  long P_2 = power(2, N - 1);

  // Stores modulo multiplicative
  // inverse of P_2 under modulo M
  long modInv = moduloInverse(P_2);

  // Stores the value of F(1)
  long res;

  // Update res
  res = ((modInv % M) *
         (F_N % M)) % M;

  return res;
}

// Driver code
public static void Main(String[] args)
{
  long N = 3;
  long F_N = 6;
  Console.Write(F_1(N, F_N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach
var M = 100000007;

// Function to find the
// value of power(X, N) % M
function power(x, N)
{

  // Stores the value
  // of (X ^ N) % M
  var res = 1;

  // Calculate the value
  // of power(x, N) % M
  while (N > 0)
  {
    // If N is odd
    if (N % 2 == 1)
    {
      // Update res
      res = (res * x) % M;
    }

    // Update x
    x = (x * x) % M;

    // Update N
    N = N >> 1;
  }
  return res;
}

// Function to find modulo
// multiplicative inverse
// of X under modulo M
function moduloInverse( X)
{
  return power(X, M - 2);
}

// Function to find the
// value of F(1)
function F_1( N, F_N)
{
  // Stores power(2, N - 1)
  var P_2 = power(2, N - 1);

  // Stores modulo multiplicative
  // inverse of P_2 under modulo M
  var modInv = moduloInverse(P_2);

  // Stores the value of F(1)
  var res;

  // Update res
  res = ((modInv % M) *
         (F_N % M)) % M;

  return res;
}

// Driver code
var N = 3;
var F_N = 6;
document.write(F_1(N, F_N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
500000005
```

***时间复杂度:**O(log<sub>2</sub>N)*
*T8】辅助空间: O(1)*