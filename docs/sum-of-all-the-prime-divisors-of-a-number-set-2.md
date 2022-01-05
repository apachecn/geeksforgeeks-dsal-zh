# 一个数的所有质因数之和|集合 2

> 原文:[https://www . geeksforgeeks . org/所有数集素数之和-2/](https://www.geeksforgeeks.org/sum-of-all-the-prime-divisors-of-a-number-set-2/)

给定一个数字 **N** ，任务是找出 **N** 的所有[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的和。

**示例:**

> **输入** : 10
> **输出** : 7
> **说明:** 2、5 是 10 的质因数
> 
> **输入** : 20
> **输出** : 7
> **解释** : 2、5 是 20 的质因数

**方法:**这个问题可以通过找到这个数的所有[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)来解决。按照以下步骤解决此问题:

*   将变量**和**初始化为 **0** ，以存储 **N.** 的素数之和
*   如果 **N** 被 **2 整除，**将 **2** 加到**和**上，再将 **N** 除以 **2** 直到整除。
*   [使用变量 **i、**在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【3，sqrt(N)】**中迭代，增量为 **2** :
    *   如果 **N** 被 **i 整除，**将 **i** 加到**和**上，再将 **N** 除以 **i** 直到整除。
*   如果 **N** 是大于 **2 的素数，**将 **N** 加到**和。**
*   完成以上步骤后，打印**和**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find sum of prime
// divisors of the given number N
int SumOfPrimeDivisors(int n)
{

    int sum = 0;

    // Add the number 2 if it divides N
    if (n % 2 == 0) {
        sum = sum + 2;
    }

    while (n % 2 == 0) {
        n = n / 2;
    }

    // Traverse the loop from [3, sqrt(N)]
    for (int i = 3; i <= sqrt(n); i = i + 2) {

        // If i divides N, add i and divide N
        if (n % i == 0) {
            sum = sum + i;
        }

        while (n % i == 0) {
            n = n / i;
        }
    }

    // This condition is to handle the case when N
    // is a prime number greater than 2
    if (n > 2) {
        sum = sum + n;
    }

    return sum;
}

// Driver code
int main()
{
    // Given Input
    int n = 10;

    // Function Call
    cout << SumOfPrimeDivisors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
  // Function to find sum of prime
  // divisors of the given number N
  public static int SumOfPrimeDivisors(int n)
  {

    int sum = 0;

    // Add the number 2 if it divides N
    if (n % 2 == 0) {
      sum = sum + 2;
    }

    while (n % 2 == 0) {
      n = n / 2;
    }

    // Traverse the loop from [3, sqrt(N)]
    for (int i = 3; i <= Math.sqrt(n); i = i + 2) {

      // If i divides N, add i and divide N
      if (n % i == 0) {
        sum = sum + i;
      }

      while (n % i == 0) {
        n = n / i;
      }
    }

    // This condition is to handle the case when N
    // is a prime number greater than 2
    if (n > 2) {
      sum = sum + n;
    }

    return sum;
  }

  // Driver code
  public static void main (String[] args)
  {

    // Given Input
    int n = 10;

    // Function Call
    System.out.println(SumOfPrimeDivisors(n));
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find sum of prime
# divisors of the given number N
def SumOfPrimeDivisors(n):

    sum = 0

    # Add the number 2 if it divides N
    if n % 2 == 0:
        sum += 2

    while n % 2 == 0:
        n //= 2

    # Traverse the loop from [3, sqrt(N)]
    k = int(math.sqrt(n))

    for i in range(3, k + 1, 2):

        # If i divides N, add i and divide N
        if n % i == 0:
            sum += i

        while n % i == 0:
            n //= i

    # This condition is to handle the case when N
    # is a prime number greater than 2
    if n > 2:
        sum += n

    # Return the sum
    return sum

# Driver code
if __name__ == '__main__':

    # Given input
    n = 10

    # Function call
    print(SumOfPrimeDivisors(n))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach

using System;

class GFG {
  // Function to find sum of prime
  // divisors of the given number N
  public static int SumOfPrimeDivisors(int n)
  {

    int sum = 0;

    // Add the number 2 if it divides N
    if (n % 2 == 0) {
      sum = sum + 2;
    }

    while (n % 2 == 0) {
      n = n / 2;
    }

    // Traverse the loop from [3, sqrt(N)]
    for (int i = 3; i <= Math.Sqrt(n); i = i + 2) {

      // If i divides N, add i and divide N
      if (n % i == 0) {
        sum = sum + i;
      }

      while (n % i == 0) {
        n = n / i;
      }
    }

    // This condition is to handle the case when N
    // is a prime number greater than 2
    if (n > 2) {
      sum = sum + n;
    }

    return sum;
  }

  // Driver code
  public static void Main (String[] args)
  {

    // Given Input
    int n = 10;

    // Function Call
    Console.Write(SumOfPrimeDivisors(n));
  }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to find sum of prime
        // divisors of the given number N
        function SumOfPrimeDivisors(n) {

            let sum = 0;

            // Add the number 2 if it divides N
            if (n % 2 == 0) {
                sum = sum + 2;
            }

            while (n % 2 == 0) {
                n = n / 2;
            }

            // Traverse the loop from [3, sqrt(N)]
            for (let i = 3; i <= Math.sqrt(n); i = i + 2) {

                // If i divides N, add i and divide N
                if (n % i == 0) {
                    sum = sum + i;
                }

                while (n % i == 0) {
                    n = n / i;
                }
            }

            // This condition is to handle the case when N
            // is a prime number greater than 2
            if (n > 2) {
                sum = sum + n;
            }

            return sum;
        }

        // Driver code

        // Given Input
        let n = 10;

        // Function Call
        document.write(SumOfPrimeDivisors(n));

// This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
7
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*