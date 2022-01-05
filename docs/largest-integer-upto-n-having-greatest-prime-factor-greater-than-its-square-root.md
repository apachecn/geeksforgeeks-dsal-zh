# 最大整数 up 至 N，其最大质因数大于其平方根

> 原文:[https://www . geeksforgeeks . org/maximum-integer-upto-n-具有大于其平方根的最大质因数/](https://www.geeksforgeeks.org/largest-integer-upto-n-having-greatest-prime-factor-greater-than-its-square-root/)

给定一个正整数 **N** ，任务是找到范围**【1，N】**中最大的数，使得数的[平方根小于其](https://www.geeksforgeeks.org/square-root-of-an-integer/)[最大质因数](https://www.geeksforgeeks.org/find-largest-prime-factor-number/)。

> **输入:** N = 15
> **输出:** 15
> **说明:**15 的素因子为{3，5}。15 的平方根是 3.87(即 3.87 < 5)。因此，15 是给定范围内最大的有效整数。
> 
> **输入:**N = 25
> T3】输出: 23

**方法:**给定的问题可以通过使用厄拉多塞的[筛进行少量修改来解决。创建一个数组 **gpf[]** ，它存储给定范围内所有整数的](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[最大质因数](https://www.geeksforgeeks.org/find-largest-prime-factor-number/)。最初， **gpf[] = {0}** 。使用 Sieve，初始化数组**GPF【】**的所有索引，使用相应索引的最大质因数，类似于本文中讨论的算法。

现在，[以相反的方式迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N，1】**，并打印第一个整数，其数字的[平方根小于其](https://www.geeksforgeeks.org/square-root-of-an-integer/)[最大质因数](https://www.geeksforgeeks.org/find-largest-prime-factor-number/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int maxn = 100001;

// Stores the Greatest Prime Factor
int gpf[maxn];

// Modified Sieve to find the Greatest
// Prime Factor of all integers in the
// range [1, maxn]
void modifiedSieve()
{
    // Initialize the array with 0
    memset(gpf, 0, sizeof(gpf));
    gpf[0] = 0;
    gpf[1] = 1;

    // Iterate through all values of i
    for (int i = 2; i < maxn; i++) {

        // If i is not a prime number
        if (gpf[i] > 0)
            continue;

        // Update the multiples of i
        for (int j = i; j < maxn; j += i) {
            gpf[j] = max(i, gpf[j]);
        }
    }
}

// Function to find integer in the range
// [1, N] such that its Greatest Prime
// factor is greater than its square root
int greatestValidInt(int N)
{

    modifiedSieve();

    // Iterate through all values of
    // i in the range [N, 1]
    for (int i = N; i > 0; i--) {

        // If greatest prime factor of i
        // is greater than its square root
        if (gpf[i] > sqrt(i)) {

            // Return answer
            return i;
        }
    }

    // If no valid integer exist
    return -1;
}

// Driver Code
int main()
{
    int N = 25;
    cout << greatestValidInt(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    final static int maxn = 100001;

    // Stores the Greatest Prime Factor
    static int gpf[] = new int[maxn];

    // Modified Sieve to find the Greatest
    // Prime Factor of all integers in the
    // range [1, maxn]
    static void modifiedSieve()
    {

        // Initialize the array with 0
        for (int i = 0; i < maxn; i++ )
            gpf[i] = 0;

        gpf[0] = 0;
        gpf[1] = 1;

        // Iterate through all values of i
        for (int i = 2; i < maxn; i++) {

            // If i is not a prime number
            if (gpf[i] > 0)
                continue;

            // Update the multiples of i
            for (int j = i; j < maxn; j += i) {
                gpf[j] = Math.max(i, gpf[j]);
            }
        }
    }

    // Function to find integer in the range
    // [1, N] such that its Greatest Prime
    // factor is greater than its square root
    static int greatestValidInt(int N)
    {

        modifiedSieve();

        // Iterate through all values of
        // i in the range [N, 1]
        for (int i = N; i > 0; i--) {

            // If greatest prime factor of i
            // is greater than its square root
            if (gpf[i] > Math.sqrt(i)) {

                // Return answer
                return i;
            }
        }

        // If no valid integer exist
        return -1;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 25;
        System.out.println(greatestValidInt(N));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

import math

maxn = 100001

# Stores the Greatest Prime Factor
gpf = [0 for _ in range(maxn)]

# Modified Sieve to find the Greatest
# Prime Factor of all integers in the
# range [1, maxn]

def modifiedSieve():

    # Initialize the array with 0
    gpf[0] = 0
    gpf[1] = 1

    # Iterate through all values of i
    for i in range(2, maxn):

        # If i is not a prime number
        if (gpf[i] > 0):
            continue

        # Update the multiples of i
        for j in range(i, maxn, i):
            gpf[j] = max(i, gpf[j])

# Function to find integer in the range
# [1, N] such that its Greatest Prime
# factor is greater than its square root
def greatestValidInt(N):

    modifiedSieve()

    # Iterate through all values of
    # i in the range [N, 1]
    for i in range(N, 0, -1):

        # If greatest prime factor of i
        # is greater than its square root
        if (gpf[i] > math.sqrt(i)):

            # Return answer
            return i

    # If no valid integer exist
    return -1

# Driver Code
if __name__ == "__main__":

    N = 25
    print(greatestValidInt(N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    static int maxn = 100001;

    // Stores the Greatest Prime Factor
    static int[] gpf = new int[maxn];

    // Modified Sieve to find the Greatest
    // Prime Factor of all integers in the
    // range [1, maxn]
    static void modifiedSieve()
    {

        // Initialize the array with 0
        for (int i = 0; i < maxn; i++)
            gpf[i] = 0;

        gpf[0] = 0;
        gpf[1] = 1;

        // Iterate through all values of i
        for (int i = 2; i < maxn; i++) {

            // If i is not a prime number
            if (gpf[i] > 0)
                continue;

            // Update the multiples of i
            for (int j = i; j < maxn; j += i) {
                gpf[j] = Math.Max(i, gpf[j]);
            }
        }
    }

    // Function to find integer in the range
    // [1, N] such that its Greatest Prime
    // factor is greater than its square root
    static int greatestValidInt(int N)
    {

        modifiedSieve();

        // Iterate through all values of
        // i in the range [N, 1]
        for (int i = N; i > 0; i--) {

            // If greatest prime factor of i
            // is greater than its square root
            if (gpf[i] > Math.Sqrt(i)) {

                // Return answer
                return i;
            }
        }

        // If no valid integer exist
        return -1;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 25;
        Console.WriteLine(greatestValidInt(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

const maxn = 100001;

// Stores the Greatest Prime Factor
let gpf = new Array(maxn);

// Modified Sieve to find the Greatest
// Prime Factor of all integers in the
// range [1, maxn]
function modifiedSieve()
{

  // Initialize the array with 0
  gpf.fill(0);
  gpf[0] = 0;
  gpf[1] = 1;

  // Iterate through all values of i
  for (let i = 2; i < maxn; i++)
  {

    // If i is not a prime number
    if (gpf[i] > 0) continue;

    // Update the multiples of i
    for (let j = i; j < maxn; j += i) {
      gpf[j] = Math.max(i, gpf[j]);
    }
  }
}

// Function to find integer in the range
// [1, N] such that its Greatest Prime
// factor is greater than its square root
function greatestValidInt(N) {
  modifiedSieve();

  // Iterate through all values of
  // i in the range [N, 1]
  for (let i = N; i > 0; i--)
  {

    // If greatest prime factor of i
    // is greater than its square root
    if (gpf[i] > Math.sqrt(i))
    {

      // Return answer
      return i;
    }
  }

  // If no valid integer exist
  return -1;
}

// Driver Code
let N = 25;
document.write(greatestValidInt(N));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
23
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*