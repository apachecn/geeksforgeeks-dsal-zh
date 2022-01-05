# 打印所有 N 的除数，并且与其除数的商同素的数字

> 原文:[https://www . geeksforgeeks . org/print-all-numbers-这些数字都是 n 的除数和它们的商的同素除法/](https://www.geeksforgeeks.org/print-all-numbers-that-are-divisors-of-n-and-are-co-prime-with-the-quotient-of-their-division/)

给定一个正整数 **N** ，任务是打印所有的数字，比如说 **K** ，这样 **K** 就是 **N** 的[除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)，而 **K** 和 **N / K** 就是[互素](https://www.geeksforgeeks.org/check-if-all-the-pairs-of-an-array-are-coprime-with-each-other/)。

**示例:**

> **输入:** N = 12
> **输出:** 1 3 4 12
> **解释:**
> 所有数字 K 都是 N 的除数(= 12)，K 和 N/K 是互素:
> 
> 1.  1:因为 1 是 12 的除数，1 和 12(= 12/1)是互素。
> 2.  3:因为 3 是 12 的除数，所以 3 和 4( = 12/3)是互素。
> 3.  4:因为 4 是 12 的除数，所以 4 和 3( = 12/4)是互素。
> 4.  12:因为 12 是 12 的除数，所以 12 和 1( = 12/12)是互素。
> 
> **输入:**N = 100
> T3】输出: 1 4 25 100

**天真方法:**解决给定问题最简单的方法是[迭代范围**【1，N】**](https://www.geeksforgeeks.org/range-based-loop-c/)**并检查每个数字 **K** 是否 [**K** 是**N**](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)和[的除数 K 和 N/K](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的 GCD 是否为 **1** 。如果发现**为真**，则打印 **K** 。否则，检查下一个号码。**

*****时间复杂度:** O(N*log N)*
***辅助空间:** O(1)***

****有效方法:**上述方法也可以通过观察所有除数成对出现来优化。比如 **N** 是 **100** ，那么所有的除数对都是: **(1，100)、(2，50)、(4，25)、(5，20)、(10，10)** 。**

**因此，思路是[在](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，√N】**的范围内迭代，检查两个给定条件是否都满足，即 [**K** 是否为**N**](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)**T11】和[的除数 **K** 和 **N/K**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 是否为 **1** 。如果发现**为真**，则打印两个数字。如果是两个相等的除数，只打印其中一个。****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print all numbers
// that are divisors of N and are
// co-prime with the quotient
// of their division
void printUnitaryDivisors(int n)
{
    // Iterate upto square root of N
    for (int i = 1; i <= sqrt(n); i++) {

        if (n % i == 0) {

            // If divisors are equal and gcd is
            // 1, then print only one of them
            if (n / i == i && __gcd(i, n / i) == 1) {
                printf("%d ", i);
            }

            // Otherwise print both
            else {
                if (__gcd(i, n / i) == 1) {
                    printf("%d %d ", i, n / i);
                }
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 12;
    printUnitaryDivisors(N);

    return 0;
}
```

## **蟒蛇 3**

```
# python 3 program for the above approach
from math import sqrt, gcd

# Function to print all numbers
# that are divisors of N and are
# co-prime with the quotient
# of their division
def printUnitaryDivisors(n):

    # Iterate upto square root of N
    for i in range(1,int(sqrt(n)) + 1, 1):
        if (n % i == 0):

            # If divisors are equal and gcd is
            # 1, then print only one of them
            if (n // i == i and gcd(i, n // i) == 1):
                print(i)

            # Otherwise print both
            else:
                if (gcd(i, n // i) == 1):
                    print(i, n // i,end = " ")

# Driver Code
if __name__ == '__main__':
    N = 12
    printUnitaryDivisors(N)

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

static int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}
// Function to print all numbers
// that are divisors of N and are
// co-prime with the quotient
// of their division
static void printUnitaryDivisors(int n)
{
    // Iterate upto square root of N
    for (int i = 1; i <= (int)Math.Sqrt(n); i++) {

        if (n % i == 0) {

            // If divisors are equal and gcd is
            // 1, then print only one of them
            if (n / i == i && gcd(i, n / i) == 1) {
                Console.Write(i+" ");
            }

            // Otherwise print both
            else {
                if (gcd(i, n / i) == 1) {
                    Console.Write(i + " " +n / i+ " ");
                }
            }
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 12;
    printUnitaryDivisors(N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for tha above approach
import java.util.*;

class GFG {

    static int gcd(int a, int b)
    {
        return b == 0 ? a : gcd(b, a % b);
    }
    // Function to print all numbers
    // that are divisors of N and are
    // co-prime with the quotient
    // of their division
    static void printUnitaryDivisors(int n)
    {
        // Iterate upto square root of N
        for (int i = 1; i <= (int)Math.sqrt(n); i++) {

            if (n % i == 0) {

                // If divisors are equal and gcd is
                // 1, then print only one of them
                if (n / i == i && gcd(i, n / i) == 1) {
                    System.out.print(i + " ");
                }

                // Otherwise print both
                else {
                    if (gcd(i, n / i) == 1) {
                        System.out.print(i + " " + n / i
                                         + " ");
                    }
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 12;
        printUnitaryDivisors(N);
    }
}
```

## **java 描述语言**

```
<script>

// JavaScript program for tha above approach
function gcd( a,  b)
    {
        return b == 0 ? a : gcd(b, a % b);
    }
    // Function to print all numbers
    // that are divisors of N and are
    // co-prime with the quotient
    // of their division
    function printUnitaryDivisors( n)
    {
        // Iterate upto square root of N
        for (var i = 1; i <= Math.sqrt(n); i++) {

            if (n % i == 0) {

                // If divisors are equal and gcd is
                // 1, then print only one of them
                if (n / i == i && gcd(i, n / i) == 1) {
                    document.write(i + " ");
                }

                // Otherwise print both
                else {
                    if (gcd(i, n / i) == 1) {
                        document.write(i + " " + n / i
                                         + " ");
                    }
                }
            }
        }
    }

    // Driver Code
        var N = 12;
        printUnitaryDivisors(N);

// This code is contributed by shivanisingh2110  

 </script>
```

****Output:** 

```
1 12 3 4
```** 

*****时间复杂度:** O(√N*log N)*
***辅助空间:** O(1)***