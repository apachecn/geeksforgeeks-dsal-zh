# 找出两个数字，使它们的平方差等于 N

> 原文:[https://www . geeksforgeeks . org/find-two-numbers-这样它们的平方差等于 n/](https://www.geeksforgeeks.org/find-two-numbers-such-that-difference-of-their-squares-equal-to-n/)

给定一个整数 **N** ，任务是找到两个非负整数 **A** 和 **B** ，使得**A<sup>2</sup>–B<sup>2</sup>= N**。如果不存在这样的整数，则打印 **-1** 。

**示例:**

> **输入:** N = 7
> **输出:** 4 3
> **说明:**
> 两个整数 4 和 3 可以表示为**4<sup>2</sup>–3<sup>2</sup>= 7**。
> **输入:** N = 6
> **输出:** -1
> **说明:**
> 不存在满足要求条件的(A，B)对。

**进场:**

*   **A<sup>2</sup>–B<sup>2</sup>**可以表示为**(A–B)*(A+B)**。

> A<sup>2</sup>–B<sup>2</sup>=(A–B)*(A+B)

*   因此，要使**A<sup>2</sup>–B<sup>2</sup>**等于 **N** ，则 **(A + B)** 和**(A–B)**都应该是 **N** 的约数。
*   考虑到 **A + B** 和**A–B**分别等于 **C** 和 **D** ，那么 **C** 和 **D** 必须是 **N** 的除数，这样 **C ≤ D** 和 **C** 和 **D** 应该是相同的奇偶性。
*   因此，为了解决这个问题，我们只需要找到满足上述条件的任意一对 **C** 和 **D** 。如果不存在这样的 **C & D** ，那么打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ Program to find two numbers
// with difference of their
// squares equal to N

#include <bits/stdc++.h>
using namespace std;

// Function to check and print
// the required two positive integers
void solve(int n)
{

    // Iterate till sqrt(n) to find
    // factors of N
    for (int x = 1; x <= sqrt(n); x++) {

        // Check if x is one
        // of the factors of N
        if (n % x == 0) {

            // Store the factor
            int small = x;

            // Compute the other factor
            int big = n / x;

            // Check if the two factors
            // are of the same parity
            if (small % 2 == big % 2) {

                // Compute a and b
                int a = (small + big) / 2;
                int b = (big - small) / 2;

                cout << a << " "
                     << b << endl;
                return;
            }
        }
    }

    // If no pair exists
    cout << -1 << endl;
}

// Driver Code
int main()
{
    int n = 7;

    solve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find two numbers
// with difference of their
// squares equal to N
import java.util.*;
class GFG{

// Function to check and print
// the required two positive integers
static void solve(int n)
{

    // Iterate till sqrt(n) to find
    // factors of N
    for (int x = 1; x <= Math.sqrt(n); x++)
    {

        // Check if x is one
        // of the factors of N
        if (n % x == 0)
        {

            // Store the factor
            int small = x;

            // Compute the other factor
            int big = n / x;

            // Check if the two factors
            // are of the same parity
            if (small % 2 == big % 2)
            {

                // Compute a and b
                int a = (small + big) / 2;
                int b = (big - small) / 2;

                System.out.print(a + " " + b);
                return;
            }
        }
    }

    // If no pair exists
    System.out.print(-1);
}

// Driver Code
public static void main(String args[])
{
    int n = 7;

    solve(n);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 Program to find two numbers
# with difference of their
# squares equal to N
from math import sqrt

# Function to check and print
# the required two positive integers
def solve(n) :

    # Iterate till sqrt(n) to find
    # factors of N
    for x in range(1, int(sqrt(n)) + 1) :

        # Check if x is one
        # of the factors of N
        if (n % x == 0) :

            # Store the factor
            small = x;

            # Compute the other factor
            big = n // x;

            # Check if the two factors
            # are of the same parity
            if (small % 2 == big % 2) :

                # Compute a and b
                a = (small + big) // 2;
                b = (big - small) // 2;
                print(a, b) ;
                return;

    # If no pair exists
    print(-1);

# Driver Code
if __name__ == "__main__" :
    n = 7;
    solve(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# Program to find two numbers
// with difference of their
// squares equal to N
using System;
class GFG{

// Function to check and print
// the required two positive integers
static void solve(int n)
{

    // Iterate till sqrt(n) to find
    // factors of N
    for (int x = 1; x <= Math.Sqrt(n); x++)
    {

        // Check if x is one
        // of the factors of N
        if (n % x == 0)
        {

            // Store the factor
            int small = x;

            // Compute the other factor
            int big = n / x;

            // Check if the two factors
            // are of the same parity
            if (small % 2 == big % 2)
            {

                // Compute a and b
                int a = (small + big) / 2;
                int b = (big - small) / 2;

                Console.WriteLine(a + " " + b);
                return;
            }
        }
    }

    // If no pair exists
    Console.WriteLine(-1);
}

// Driver Code
public static void Main()
{
    int n = 7;

    solve(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript Program to find two numbers
// with difference of their
// squares equal to N

    // Function to check and print
    // the required two positive integers
    function solve(n) {

        // Iterate till sqrt(n) to find
        // factors of N
        for (var x = 1; x <= Math.sqrt(n); x++) {

            // Check if x is one
            // of the factors of N
            if (n % x == 0) {

                // Store the factor
                var small = x;

                // Compute the other factor
                var big = n / x;

                // Check if the two factors
                // are of the same parity
                if (small % 2 == big % 2) {

                    // Compute a and b
                    var a = (small + big) / 2;
                    var b = (big - small) / 2;

                    document.write(a + " " + b);
                    return;
                }
            }
        }

        // If no pair exists
        document.write(-1);
    }

    // Driver Code

        var n = 7;

        solve(n);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
4 3
```

**时间复杂度:***O(sqrt(N))*
T5】辅助空间: *O(1)*