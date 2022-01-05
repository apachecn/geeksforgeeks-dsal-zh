# 加拿大数字

> 原文:[https://www.geeksforgeeks.org/canada-numbers/](https://www.geeksforgeeks.org/canada-numbers/)

**加拿大数字**是一个数字 **N** 使得 **N** 的数字的平方和等于 **N** 的非平凡除数之和，即(N-1–N 的除数之和)
很少有加拿大数字是:

> 125，581，8549，16999……

### 检查 N 是否为加拿大数字

给定一个数字 **N** ，任务是检查 **N** 是否是**加拿大号**。如果 **N** 是加拿大号码，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 125
> **输出:** Yes
> **解释:**
> 125 的因子是 1，5，25，125
> 和 1^2 + 2^2 + 5^2 = 30 = 5 + 25。
> **输入:** N = 16
> **输出:**否

**方法:**思路是求一个数的所有适当除数的[和，从中减去 N 和 1。另外，求 n 位数的平方和。现在检查两个和是否相同。如果所有适当除数的和与 N 位数的平方和相等，那么这个数就是加拿大数。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/) 

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// all trivial divisors
// of given natural number
int divSum(int num)
{
    // Final result of summation
    // of trivial divisors
    int result = 0;

    // Find all divisors which
    // divides 'num'
    for (int i = 1; i <= sqrt(num); i++) {

        // if 'i' is divisor of 'num'
        if (num % i == 0) {

            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }
    return (result - 1 - num);
}

// Function to return sum
// of squares
// of digits of N
int getSum(int n)
{
    int sum = 0;
    while (n != 0) {
        int r = n % 10;
        sum = sum + r * r;
        n = n / 10;
    }
    return sum;
}

// Function to check if N is a
// Canada number
bool isCanada(int n)
{
    return divSum(n) == getSum(n);
}

// Driver Code
int main()
{
    // Given Number
    int n = 125;

    // Function Call
    if (isCanada(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
import java.io.*;
class GFG{

// Function to calculate sum of
// all trivial divisors
// of given natural number
static int divSum(int num)
{
    // Final result of summation
    // of trivial divisors
    int result = 0;

    // Find all divisors which
    // divides 'num'
    for (int i = 1; i <= Math.sqrt(num); i++)
    {

        // if 'i' is divisor of 'num'
        if (num % i == 0)
        {

            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }
    return (result - 1 - num);
}

// Function to return sum
// of squares
// of digits of N
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        int r = n % 10;
        sum = sum + r * r;
        n = n / 10;
    }
    return sum;
}

// Function to check if N is a
// Canada number
static boolean isCanada(int n)
{
    return divSum(n) == getSum(n);
}

// Driver Code
public static void main (String[] args)
{
    // Given Number
    int n = 125;

    // Function Call
    if (isCanada(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation for the
# above approach
import math

# Function to calculate sum of
# all trivial divisors
# of given natural number
def divSum(num):

    # Final result of summation
    # of trivial divisors
    result = 0

    # Find all divisors which
    # divides 'num'
    for i in range(1, int(math.sqrt(num)) + 1):

        # if 'i' is divisor of 'num'
        if (num % i == 0):

            # if both divisors are same then add
            # it only once else add both
            if (i == (num // i)):
                result += i
            else:
                result += (i + num // i)
    return (result - 1 - num)

# Function to return sum
# of squares
# of digits of N
def getSum(n):
    sum = 0
    while (n != 0):
        r = n % 10
        sum = sum + r * r
        n = n // 10
    return sum

# Function to check if N is a
# Canada number
def isCanada(n):
    return divSum(n) == getSum(n)

# Driver Code

# Given Number
n = 125

# Function Call
if (isCanada(n)):
    print('Yes')
else:
    print('No')

# This code is contributed by Yatin
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to calculate sum of
// all trivial divisors
// of given natural number
static int divSum(int num)
{
    // Final result of summation
    // of trivial divisors
    int result = 0;

    // Find all divisors which
    // divides 'num'
    for (int i = 1; i <= Math.Sqrt(num); i++)
    {

        // if 'i' is divisor of 'num'
        if (num % i == 0)
        {

            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }
    return (result - 1 - num);
}

// Function to return sum
// of squares
// of digits of N
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        int r = n % 10;
        sum = sum + r * r;
        n = n / 10;
    }
    return sum;
}

// Function to check if N is a
// Canada number
static bool isCanada(int n)
{
    return divSum(n) == getSum(n);
}

// Driver Code
public static void Main()
{
    // Given Number
    int n = 125;

    // Function Call
    if (isCanada(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation for the
// above approach

    // Function to calculate sum of
    // all trivial divisors
    // of given natural number
    function divSum( num) {
        // Final result of summation
        // of trivial divisors
        let result = 0;

        // Find all divisors which
        // divides 'num'
        for (let i = 1; i <= Math.sqrt(num); i++) {

            // if 'i' is divisor of 'num'
            if (num % i == 0) {

                // if both divisors are same then add
                // it only once else add both
                if (i == (num / i))
                    result += i;
                else
                    result += (i + num / i);
            }
        }
        return (result - 1 - num);
    }

    // Function to return sum
    // of squares
    // of digits of N
    function getSum( n) {
        let sum = 0;
        while (n != 0) {
            let r = n % 10;
            sum = sum + r * r;
            n = parseInt(n / 10);
        }
        return sum;
    }

    // Function to check if N is a
    // Canada number
    function isCanada( n) {
        return divSum(n) == getSum(n);
    }

    // Driver Code

        // Given Number
        let n = 125;

        // Function Call
        if (isCanada(n))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(n <sup>1/2</sup> )*

***辅助空间:** O(1)*

**参考:**T2http://www.numbersaplenty.com/set/Canada_number/