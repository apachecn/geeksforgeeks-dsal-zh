# 大于或等于 N 且能被非零数字整除的最小数

> 原文:[https://www . geeksforgeeks . org/最小数字大于或等于可被其位数整除的 n/](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-which-is-divisible-by-its-digits/)

给定一个整数 **N** ，任务是找到大于或等于 **N** 的最小数，这样它就可以被它的所有非零数字整除。

**示例:**

> **输入:** N = 31
> **输出:** 33
> **说明:** 33 是满足给定条件的最小数。
> 单位所在地:33%3 = 0
> 单位所在地:33%3 = 0
> 
> **输入:** N = 30
> **输出:** 30
> **说明:** 30 是满足给定条件的最小数。
> 原地踏步:30%3 = 0

**逼近:**能被 1 到 9 的所有数字整除的最小数等于(1，2，3，4，5，6，7，8，9)=(2520)的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。所以 **2520** 的倍数也是可以被 **1** 到 **9** 的所有数字整除的，暗示着 **(N + 2520)** 永远满足条件。因此，在**【N，2520+N】**范围内迭代，检查满足给定条件的最小数。按照以下步骤解决问题:

*   将**和**初始化为 **0** 以存储大于或等于 **N** 的最小数字，这样它可以被其所有非零数字整除。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N，N+2520】**。
    *   初始化一个变量**可能**为 **1** ，检查当前号码 **i** 是否满足给定条件。
    *   [获取 **i**](https://www.geeksforgeeks.org/c-program-to-print-all-digits-of-a-given-number/) 的所有非零数字，检查我是否能被它们整除。如果发现为真，则更新**可能**为 **1** ，更新 **ans** 为 **i** ，[破环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number
// greater than or equal to N such that
// it is divisible by its non-zero digits
void findSmallestNumber(int n)
{

    // Iterate in range[N, N + 2520]
    for (int i = n; i <= (n + 2520); ++i) {

        // To check if the current number
        // satisfies the given condition
        bool possible = 1;

        // Store the number in a temporary
        // variable
        int temp = i;

        // Loop until temp > 0
        while (temp) {

            // Check only for non zero digits
            if (temp % 10 != 0) {

                // Extract the current digit
                int digit = temp % 10;

                // If number is divisible
                // by current digit or not
                if (i % digit != 0) {

                    // Otherwise, set
                    // possible to 0
                    possible = 0;

                    // Break out of the loop
                    break;
                }
            }

            // Divide by 10
            temp /= 10;
        }

        if (possible == 1) {
            cout << i;
            return;
        }
    }
}

// Driver Code
int main()
{
    int N = 31;

    // Function Call
    findSmallestNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the smallest number
// greater than or equal to N such that
// it is divisible by its non-zero digits
static void findSmallestNumber(int n)
{

    // Iterate in range[N, N + 2520]
    for(int i = n; i <= (n + 2520); ++i)
    {

        // To check if the current number
        // satisfies the given condition
        int possible = 1;

        // Store the number in a temporary
        // variable
        int temp = i;

        // Loop until temp > 0
        while (temp != 0)
        {

            // Check only for non zero digits
            if (temp % 10 != 0)
            {

                // Extract the current digit
                int digit = temp % 10;

                // If number is divisible
                // by current digit or not
                if (i % digit != 0)
                {

                    // Otherwise, set
                    // possible to 0
                    possible = 0;

                    // Break out of the loop
                    break;
                }
            }

            // Divide by 10
            temp /= 10;
        }

        if (possible == 1)
        {
            System.out.println(i);
            return;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 31;

    // Function Call
    findSmallestNumber(N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest number
# greater than or equal to N such that
# it is divisible by its non-zero digits
def findSmallestNumber(n):

    # Iterate in range[N, N + 2520]
    for i in range(n, n + 2521):

        # To check if the current number
        # satisfies the given condition
        possible = 1

        # Store the number in a temporary
        # variable
        temp = i

        # Loop until temp > 0
        while (temp):

            # Check only for non zero digits
            if (temp % 10 != 0):

                # Extract the current digit
                digit = temp % 10

                # If number is divisible
                # by current digit or not
                if (i % digit != 0):

                    # Otherwise, set
                    # possible to 0
                    possible = 0

                    # Break out of the loop
                    break

            # Divide by 10
            temp //= 10

        if (possible == 1):
            print(i, end = "")
            return

# Driver Code
if __name__ == "__main__" :

    N = 31

    # Function Call
    findSmallestNumber(N)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the smallest number
// greater than or equal to N such that
// it is divisible by its non-zero digits
static void findSmallestNumber(int n)
{

    // Iterate in range[N, N + 2520]
    for(int i = n; i <= (n + 2520); ++i)
    {

        // To check if the current number
        // satisfies the given condition
        int possible = 1;

        // Store the number in a temporary
        // variable
        int temp = i;

        // Loop until temp > 0
        while (temp != 0)
        {

            // Check only for non zero digits
            if (temp % 10 != 0)
            {

                // Extract the current digit
                int digit = temp % 10;

                // If number is divisible
                // by current digit or not
                if (i % digit != 0)
                {

                    // Otherwise, set
                    // possible to 0
                    possible = 0;

                    // Break out of the loop
                    break;
                }
            }

            // Divide by 10
            temp /= 10;
        }

        if (possible == 1)
        {
            Console.Write(i);
            return;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 31;

    // Function Call
    findSmallestNumber(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to find the smallest number
// greater than or equal to N such that
// it is divisible by its non-zero digits
function findSmallestNumber(n)
{

    // Iterate in range[N, N + 2520]
    for(i = n; i <= (n + 2520); ++i)
    {

        // To check if the current number
        // satisfies the given condition
        var possible = 1;

        // Store the number in a temporary
        // variable
        var temp = i;

        // Loop until temp > 0
        while (temp != 0)
        {

            // Check only for non zero digits
            if (temp % 10 != 0)
            {

                // Extract the current digit
                var digit = temp % 10;

                // If number is divisible
                // by current digit or not
                if (i % digit != 0)
                {

                    // Otherwise, set
                    // possible to 0
                    possible = 0;

                    // Break out of the loop
                    break;
                }
            }

            // Divide by 10
            temp  = parseInt(temp / 10);
        }

        if (possible == 1)
        {
            document.write(i);
            return;
        }
    }
}

// Driver code
var N = 31;

// Function Call
findSmallestNumber(N);

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
33
```

***时间复杂度:**O(2520 * log<sub>10</sub>N)*
*T8】辅助空间: O(1)*