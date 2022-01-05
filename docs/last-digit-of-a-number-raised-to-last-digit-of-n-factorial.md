# 升到 N 阶乘最后一位的数字的最后一位

> 原文:[https://www . geeksforgeeks . org/数字的最后一位-从 n 的最后一位-阶乘/](https://www.geeksforgeeks.org/last-digit-of-a-number-raised-to-last-digit-of-n-factorial/)

给定两个数字 **X** 和 **N** ，任务是找到 **X** 的最后一个数字上升到[N 阶乘](https://www.geeksforgeeks.org/last-non-zero-digit-factorial/)的最后一个数字，即![X^{\left ( N! \right )mod 10}    ](img/e2943bae2f4e34ce3a8ccfd1223dd0ae.png "Rendered by QuickLaTeX.com")。
**举例:**

> **输入:** X = 5，N = 2
> **输出:** 5
> **说明:**
> 自，2！mod 10 = 2
> 因此 5 <sup>2</sup> = 25，25 的最后一位是 5。
> **输入:** X = 10，N = 4
> **输出:** 0
> **解释:**
> 自，4！mod 10 = 24 mod 10 = 4
> 因此 10 <sup>4</sup> = 10000，10000 的最后一位是 0。

**方法:**解决这个问题最有效的方法就是在需要的最后一位找到任意模式，借助[最后一位的 N！](https://www.geeksforgeeks.org/last-non-zero-digit-factorial/)和[X 的最后一位数字上升到 Y](https://www.geeksforgeeks.org/find-unit-digit-x-raised-power-y/)
下面是对上述等式的各种观察:

*   如果 **N = 0** 或 **N = 1** ，则最后一位分别为 1 或![X mod 10    ](img/2b0015b080f6389c679f8d809f5672b2.png "Rendered by QuickLaTeX.com")。
*   自 **5！是 120** ，因此为 **N ≥ 5** 的值 **(N！mod 10)** 将为零。
*   现在我们只剩下数字 2，3，4。为此，我们有:

> 对于 N = 2，
> N！mod 10 = 2！mod 10 = 2
> 代表 N = 3，
> 代表 N！mod 10 = 3！mod 10 = 6
> 代表 N = 4，
> 代表 N！mod 10 = 4！mod 10 = 24 mod 10 = 4
> 现在对于 X <sup>2</sup> ，X <sup>4</sup> ，X <sup>6</sup>
> 我们将检查在此之后 X<sup>n 次方 X <sup>n</sup> 的最后一位数值重复，
> 即在此之后 X <sup>n</sup> 的最后一位数值的**n**次方重复。</sup>

*   下表列出了任意数字从 0 到 9 的最后一位的幂重复次数:

<figure class="table">

| 数字 | 周期性 |
| --- | --- |
| Zero | one |
| one | one |
| Two | four |
| three | four |
| four | Two |
| five | one |
| six | one |
| seven | four |
| eight | four |
| nine | Two |

</figure>

以下是基于上述观察的步骤:

1.  如果 **X** 不是 **10** 的倍数，那么将![X^{\left ( N! \right )mod 10}    ](img/e2943bae2f4e34ce3a8ccfd1223dd0ae.png "Rendered by QuickLaTeX.com")的评估值除以 **X** 最后一位的循环度。如果余数(如 **r** )为 0，则执行以下操作:
    *   如果 **X** 的最后一位数字是 **2、4、6 或 8** 中的任何一个，那么答案将是 **6** 。
    *   如果 **X** 的最后一位数字是 **1、3、7 或 9** 中的任何一个，那么答案将是 **1** 。
    *   如果 **X** 的最后一位数字是 **5** ，那么答案将是 **5** 。
2.  否则，如果余数(如 **r** )为非零，则答案为![l^{r} mod 10    ](img/5aa013867eb0723f0dc2e542996a7a7a.png "Rendered by QuickLaTeX.com")，其中**‘l’**为 **X** 的最后一位数字。
3.  否则如果 **X** 是 **10** 的倍数，那么答案总是 **0** 。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find a^b using
// binary exponentiation
long power(long a, long b, long c)
{

    // Initialise result
    long result = 1;

    while (b > 0)
    {

        // If b is odd then,
        // multiply result by a
        if ((b & 1) == 1)
        {
            result = (result * a) % c;
        }

        // b must be even now
        // Change b to b/2
        b /= 2;

        // Change a = a^2
        a = (a * a) % c;
    }
    return result;
}

// Function to find the last digit
// of the given equation
long calculate(long X, long N)
{
    int a[10];

    // To store cyclicity
    int cyclicity[11];

    // Store cyclicity from 1 - 10
    cyclicity[1] = 1;
    cyclicity[2] = 4;
    cyclicity[3] = 4;
    cyclicity[4] = 2;
    cyclicity[5] = 1;
    cyclicity[6] = 1;
    cyclicity[7] = 4;
    cyclicity[8] = 4;
    cyclicity[9] = 2;
    cyclicity[10] = 1;

    // Observation 1
    if (N == 0 || N == 1)
    {
        return (X % 10);
    }

    // Observation 3
    else if (N == 2 || N == 3 || N == 4)
    {
        long temp = (long)1e18;

        // To store the last digits
        // of factorial 2, 3, and 4
        a[2] = 2;
        a[3] = 6;
        a[4] = 4;

        // Find the last digit of X
        long v = X % 10;

        // Step 1
        if (v != 0)
        {
            int u = cyclicity[(int)v];

            // Divide a[N] by cyclicity
            // of v
            int r = a[(int)N] % u;

            // If remainder is 0
            if (r == 0)
            {

                // Step 1.1
                if (v == 2 || v == 4 ||
                    v == 6 || v == 8)
                {
                    return 6;
                }

                // Step 1.2
                else if (v == 5)
                {
                    return 5;
                }

                // Step 1.3
                else if (v == 1 || v == 3 ||
                         v == 7 || v == 9)
                {
                    return 1;
                }
            }

            // If r is non-zero,
            // then return (l^r) % 10
            else
            {
                return (power(v, r, temp) % 10);
            }
        }

        // Else return 0
        else
        {
            return 0;
        }
    }

    // Else return 1
    return 1;
}

// Driver Code
int main()
{

    // Given Numbers
    int X = 18;
    int N = 4;

    // Function Call
    long result = calculate(X, N);

    // Print the result
    cout << result;
}

// This code is contributed by spp____
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class TestClass {

    // Function to find a^b using
    // binary exponentiation
    public static long power(long a,
                             long b,
                             long c)
    {
        // Initialise result
        long result = 1;

        while (b > 0) {

            // If b is odd then,
            // multiply result by a
            if ((b & 1) = = 1) {
                result = (result * a) % c;
            }

            // b must be even now
            // Change b to b/2
            b / = 2;

            // Change a = a^2
            a = (a * a) % c;
        }
        return result;
    }

    // Function to find the last digit
    // of the given equation
    public static long calculate(long X,
                                 long N)
    {
        int a[] = new int[10];

        // To store cyclicity
        int cyclicity[] = new int[11];

        // Store cyclicity from 1 - 10
        cyclicity[1] = 1;
        cyclicity[2] = 4;
        cyclicity[3] = 4;
        cyclicity[4] = 2;
        cyclicity[5] = 1;
        cyclicity[6] = 1;
        cyclicity[7] = 4;
        cyclicity[8] = 4;
        cyclicity[9] = 2;
        cyclicity[10] = 1;

        // Observation 1
        if (N = = 0 || N = = 1) {
            return (X % 10);
        }
        // Observation 3
        else if (N = = 2
                       || N
                 = = 3
                     || N
                 = = 4) {

            long temp = (long)1e18;

            // To store the last digits
            // of factorial 2, 3, and 4
            a[2] = 2;
            a[3] = 6;
            a[4] = 4;

            // Find the last digit of X
            long v = X % 10;

            // Step 1
            if (v ! = 0) {
                int u = cyclicity[(int)v];

                // Divide a[N] by cyclicity
                // of v
                int r = a[(int)N] % u;

                // If remainder is 0
                if (r = = 0) {

                    // Step 1.1
                    if (v = = 2
                              || v
                        = = 4
                            || v
                        = = 6
                            || v
                        = = 8) {
                        return 6;
                    }

                    // Step 1.2
                    else if (v = = 5) {
                        return 5;
                    }

                    // Step 1.3
                    else if (
                        v = = 1
                              || v
                        = = 3
                            || v
                        = = 7
                            || v
                        = = 9) {
                        return 1;
                    }
                }

                // If r is non-zero,
                // then return (l^r) % 10
                else {
                    return (power(v,
                                  r,
                                  temp)
                            % 10);
                }
            }

            // Else return 0
            else {
                return 0;
            }
        }

        // Else return 1
        return 1;
    }

    // Driver's Code
    public static void main(String args[])
        throws Exception
    {

        // Given Numbers
        int X = 18;
        int N = 4;

        // Function Call
        long result = calculate(X, N);

        // Print the result
        System.out.println(result);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a^b using
# binary exponentiation
def power(a, b, c):

    # Initialise result
    result = 1

    while (b > 0):

        # If b is odd then,
        # multiply result by a
        if ((b & 1) == 1):
            result = (result * a) % c

        # b must be even now
        # Change b to b/2
        b //= 2

        # Change a = a^2
        a = (a * a) % c

    return result

# Function to find the last digit
# of the given equation
def calculate(X, N):

    a = 10 * [0]

    # To store cyclicity
    cyclicity = 11 * [0]

    # Store cyclicity from 1 - 10
    cyclicity[1] = 1
    cyclicity[2] = 4
    cyclicity[3] = 4
    cyclicity[4] = 2
    cyclicity[5] = 1
    cyclicity[6] = 1
    cyclicity[7] = 4
    cyclicity[8] = 4
    cyclicity[9] = 2
    cyclicity[10] = 1

    # Observation 1
    if (N == 0 or N == 1):
        return (X % 10)

    # Observation 3
    elif (N == 2 or N == 3 or N == 4):
        temp = 1e18;

        # To store the last digits
        # of factorial 2, 3, and 4
        a[2] = 2
        a[3] = 6
        a[4] = 4

        # Find the last digit of X
        v = X % 10

        # Step 1
        if (v != 0):
            u = cyclicity[v]

            # Divide a[N] by cyclicity
            # of v
            r = a[N] % u

            # If remainder is 0
            if (r == 0):

                # Step 1.1
                if (v == 2 or v == 4 or
                    v == 6 or v == 8):
                    return 6

                # Step 1.2
                elif (v == 5):
                    return 5

                # Step 1.3
                elif (v == 1 or v == 3 or
                      v == 7 or v == 9):
                    return 1

            # If r is non-zero,
            # then return (l^r) % 10
            else:
                return (power(v, r, temp) % 10)

        # Else return 0
        else:
            return 0

    # Else return 1
    return 1

# Driver Code
if __name__ == "__main__":

    # Given numbers
    X = 18
    N = 4

    # Function call
    result = calculate(X, N)

    # Print the result
    print(result)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find a^b using
// binary exponentiation
static long power(long a, long b, long c)
{

    // Initialise result
    long result = 1;

    while (b > 0)
    {

        // If b is odd then,
        // multiply result by a
        if ((b & 1) == 1)
        {
            result = (result * a) % c;
        }

        // b must be even now
        // Change b to b/2
        b /= 2;

        // Change a = a^2
        a = (a * a) % c;
    }
    return result;
}

// Function to find the last digit
// of the given equation
public static long calculate(long X,
                             long N)
{
    int[] a = new int[10];

    // To store cyclicity
    int[] cyclicity = new int[11];

    // Store cyclicity from 1 - 10
    cyclicity[1] = 1;
    cyclicity[2] = 4;
    cyclicity[3] = 4;
    cyclicity[4] = 2;
    cyclicity[5] = 1;
    cyclicity[6] = 1;
    cyclicity[7] = 4;
    cyclicity[8] = 4;
    cyclicity[9] = 2;
    cyclicity[10] = 1;

    // Observation 1
    if (N == 0 || N == 1)
    {
        return (X % 10);
    }
    // Observation 3
    else if (N == 2 || N == 3 || N == 4)
    {
        long temp = (long)1e18;

        // To store the last digits
        // of factorial 2, 3, and 4
        a[2] = 2;
        a[3] = 6;
        a[4] = 4;

        // Find the last digit of X
        long v = X % 10;

        // Step 1
        if (v != 0)
        {
            int u = cyclicity[(int)v];

            // Divide a[N] by cyclicity
            // of v
            int r = a[(int)N] % u;

            // If remainder is 0
            if (r == 0)
            {

                // Step 1.1
                if (v == 2 || v == 4 ||
                    v == 6 || v == 8)
                {
                    return 6;
                }

                // Step 1.2
                else if (v == 5)
                {
                    return 5;
                }

                // Step 1.3
                else if ( v == 1 || v == 3 ||
                          v == 7 || v == 9)
                {
                    return 1;
                }
            }

            // If r is non-zero,
            // then return (l^r) % 10
            else
            {
                return (power(v, r, temp) % 10);
            }
        }

        // Else return 0
        else
        {
            return 0;
        }
    }

    // Else return 1
    return 1;
}

// Driver code
static void Main()
{

    // Given numbers
    int X = 18;
    int N = 4;

    // Function call
    long result = calculate(X, N);

    // Print the result
    Console.Write(result);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find a^b using
      // binary exponentiation
      function power(a, b, c) {
        // Initialise result
        var result = 1;

        while (b > 0) {
          // If b is odd then,
          // multiply result by a
          if ((b & 1) == 1) {
            result = (result * a) % c;
          }

          // b must be even now
          // Change b to b/2
          b /= 2;

          // Change a = a^2
          a = (a * a) % c;
        }
        return result;
      }

      // Function to find the last digit
      // of the given equation
      function calculate(X, N) {
        var a = [...Array(10)];

        // To store cyclicity
        var cyclicity = [...Array(11)];

        // Store cyclicity from 1 - 10
        cyclicity[1] = 1;
        cyclicity[2] = 4;
        cyclicity[3] = 4;
        cyclicity[4] = 2;
        cyclicity[5] = 1;
        cyclicity[6] = 1;
        cyclicity[7] = 4;
        cyclicity[8] = 4;
        cyclicity[9] = 2;
        cyclicity[10] = 1;

        // Observation 1
        if (N == 0 || N == 1) {
          return X % 10;
        }

        // Observation 3
        else if (N == 2 || N == 3 || N == 4) {
          var temp = 1e18;

          // To store the last digits
          // of factorial 2, 3, and 4
          a[2] = 2;
          a[3] = 6;
          a[4] = 4;

          // Find the last digit of X
          var v = X % 10;

          // Step 1
          if (v != 0) {
            var u = cyclicity[parseInt(v)];

            // Divide a[N] by cyclicity
            // of v
            var r = a[parseInt(N)] % u;

            // If remainder is 0
            if (r == 0)
            {

              // Step 1.1
              if (v == 2 || v == 4 || v == 6 || v == 8) {
                return 6;
              }

              // Step 1.2
              else if (v == 5) {
                return 5;
              }

              // Step 1.3
              else if (v == 1 || v == 3 || v == 7 || v == 9) {
                return 1;
              }
            }

            // If r is non-zero,
            // then return (l^r) % 10
            else {
              return power(v, r, temp) % 10;
            }
          }

          // Else return 0
          else {
            return 0;
          }
        }

        // Else return 1
        return 1;
      }

      // Driver Code
      // Given Numbers
      var X = 18;
      var N = 4;

      // Function Call
      var result = calculate(X, N);

      // Print the result
      document.write(result);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
6
```

**时间复杂度:** *O(1)*

**辅助空间:** O(11)