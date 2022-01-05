# 求 N 的两个适当因子，使它们的和与 N 同素

> 原文:[https://www . geeksforgeeks . org/find-two-professional-of-n-so-它们的和是-n 的互质/](https://www.geeksforgeeks.org/find-two-proper-factors-of-n-such-that-their-sum-is-coprime-with-n/)

给定一个整数 **N** ，你必须找到 **N** 的两个适当因子，使得它们的和与给定的整数 **N** 同素。如果不存在这样的因素，打印-1。

**示例:**

> **输入:** N = 15
> **输出:** 3、5
> **说明:** 3、5 为 15 的适当因子，3+5 - > 8 与 15 为互素。
> 
> **输入:** N = 4
> **输出:** -1
> **说明:**没有满足要求条件的合适因素

**天真方法:**生成 N 的所有适当因子的列表，对于每个可能的对，检查它们的和是否与 N 互质，即 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (整数对的和，N) = 1。这里 GCD 的意思是最大公约数。

**有效方法:**如果两个数字 **A** 和 **B** 是互质的，那么它们的和就是它们的乘积的互质。牢记这一点，[找出 N](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的所有因子，对于每个因子 **d1** ，计算出 N 的最大因子， **d2** ，与 **d1** 互质。要计算 d2，只需将 **N** 除以 **d1** 直到 **N%d1** ！= **0** 。最后，检查 **d1** 和 **d2** 是否为 **N** 的适当因子(即 d1 > 1 和 d2 > 1)。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find two proper
// factors of N such that their
// sum is coprime with N
void printFactors(int n)
{

    // Find factors in sorted order
    for (int i = 2; i <= sqrt(n); i++) {

        if (n % i == 0) {
            int d1 = i, d2 = n;

            // Find largest value of d2 such
            // that d1 and d2 are co-prime
            while (d2 % d1 == 0) {
                d2 = d2 / d1;
            }

            // Check if d1 and d2 are proper
            // factors of N
            if (d1 > 1 && d2 > 1) {
                // Print answer
                cout << d1 << ", " << d2;
                return;
            }
        }
    }

    // No such factors exist
    cout << -1;
}

// Driver code
int main()
{
    int N = 10;

    // Function Call
    printFactors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find two proper
// factors of N such that their
// sum is coprime with N   
static void printFactors(int n)
{

    // Find factors in sorted order
    for(int i = 2; i <= (int)Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            int d1 = i, d2 = n;

            // Find largest value of d2 such
            // that d1 and d2 are co-prime
            while (d2 % d1 == 0)
            {
                d2 = d2 / d1;
            }

            // Check if d1 and d2 are proper
            // factors of N
            if (d1 > 1 && d2 > 1)
            {

                // Print answer
                System.out.print(d1 + ", " + d2);
                return;
            }
        }
    }

    // No such factors exist
    System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    // Function Call
    printFactors(N);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python Program for the above approach
import math

# Function to find two proper
# factors of N such that their
# sum is coprime with N
def printFactors(n):
    # Find factors in sorted order
    for i in range(2, int(math.sqrt(n))+1):
        if (n % i == 0):
            d1 = i
            d2 = n

            # Find largest value of d2 such
            # that d1 and d2 are co-prime
            while (d2 % d1 == 0):
                d2 = d2 // d1

            # Check if d1 and d2 are proper
            # factors of N
            if (d1 > 1 and d2 > 1):

                # Print answer
                print(d1, d2, sep=", ")
                return
    # No such factors exist
    print(-1)
# Driver code
N = 10

# Function Call
printFactors(N)

# This code is contributed by Shivani
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find two proper
// factors of N such that their
// sum is coprime with N
static void printFactors(int n)
{

    // Find factors in sorted order
    for (int i = 2; i <= (int)Math.Sqrt(n); i++) {

        if (n % i == 0) {
            int d1 = i, d2 = n;

            // Find largest value of d2 such
            // that d1 and d2 are co-prime
            while (d2 % d1 == 0) {
                d2 = d2 / d1;
            }

            // Check if d1 and d2 are proper
            // factors of N
            if (d1 > 1 && d2 > 1)
            {

                // Print answer
                Console.Write(d1 + ", "+d2);
                return;
            }
        }
    }

    // No such factors exist
    Console.Write(-1);
}

// Driver code
public static void Main()
{
    int N = 10;

    // Function Call
    printFactors(N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript Program for the above approach

// Function to find two proper
// factors of N such that their
// sum is coprime with N
function printFactors(n) {
  // Find factors in sorted order
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i == 0) {
      let d1 = i,
        d2 = n;

      // Find largest value of d2 such
      // that d1 and d2 are co-prime
      while (d2 % d1 == 0) {
        d2 = Math.floor(d2 / d1);
      }

      // Check if d1 and d2 are proper
      // factors of N
      if (d1 > 1 && d2 > 1) {
        // Print answer
        document.write(d1 + ", " + d2);
        return;
      }
    }
  }

  // No such factors exist
  document.write(-1);
}

// Driver code

let N = 10;

// Function Call
printFactors(N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2, 5
```

**时间复杂度:***O(√N)*
T5】辅助空间: *O(1)*