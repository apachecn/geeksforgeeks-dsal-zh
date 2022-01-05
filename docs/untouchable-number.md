# 不可接触号码

> 原文:[https://www.geeksforgeeks.org/untouchable-number/](https://www.geeksforgeeks.org/untouchable-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为**不可触碰数字**。如果 **N** 是**不可碰号**，则打印**“是”**否则打印**“否”**。

> **不可碰数**是不是任何数的适当除数之和的数。

**例:**

> **输入:** N = 5
> **输出:**是
> **输入:** N = 20
> **输出:**否

**逼近:**思路是求 N 数的真约数的[和，检查和是否等于 **N** 。如果总和不等于 **N** ，则 **N** 为**不可碰数**则打印**“是”**否则打印**“否”**。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/) 

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// all proper divisors of num
int divSum(int num)
{
    // Final result of summation
    // of divisors
    int result = 0;

    // Find all divisors of num
    for (int i = 2; i <= sqrt(num); i++) {

        // If 'i' is divisor of 'num'
        if (num % i == 0) {

            // If both divisors are same
            // then add it only once else
            // add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }

    // Add 1 to the result as
    // 1 is also a divisor
    return (result + 1);
}

// Function to check if N is a
// Untouchable Number
bool isUntouchable(int n)
{
    for (int i = 1; i <= 2 * n; i++) {
        if (divSum(i) == n)
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 52;

    // Function Call
    if (isUntouchable(n))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate sum of
// all proper divisors of num
static int divSum(int num)
{

    // Final result of summation
    // of divisors
    int result = 0;

    // Find all divisors of num
    for(int i = 2; i <= Math.sqrt(num); i++)
    {

       // If 'i' is divisor of 'num'
       if (num % i == 0)
       {

           // If both divisors are same
           // then add it only once else
           // add both
           if (i == (num / i))
               result += i;
           else
               result += (i + num / i);
       }
    }

    // Add 1 to the result as
    // 1 is also a divisor
    return (result + 1);
}

// Function to check if N is a
// Untouchable Number
static boolean isUntouchable(int n)
{
    for(int i = 1; i <= 2 * n; i++)
    {
       if (divSum(i) == n)
           return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int n = 52;

    // Function Call
    if (isUntouchable(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math;

# Function to calculate sum of
# all proper divisors of num
def divSum(num):

    # Final result of summation
    # of divisors
    result = 0;

    # Find all divisors of num
    for i in range(2, int(math.sqrt(num))):

        # If 'i' is divisor of 'num'
        if (num % i == 0):

            # If both divisors are same
            # then add it only once else
            # add both
            if (i == (num // i)):
                result += i;
            else:
                result += (i + num // i);

    # Add 1 to the result as
    # 1 is also a divisor
    return (result + 1);

# Function to check if N is a
# Untouchable Number
def isUntouchable(n):

    for i in range(1, 2 * n):
        if (divSum(i) == n):
            return False;

    return True;

# Driver Code

# Given Number N
N = 52;

# Function Call
if (isUntouchable(N)):
    print("Yes");
else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to calculate sum of
// all proper divisors of num
static int divSum(int num)
{

    // Final result of summation
    // of divisors
    int result = 0;

    // Find all divisors of num
    for(int i = 2; i <= Math.Sqrt(num); i++)
    {

       // If 'i' is divisor of 'num'
       if (num % i == 0)
       {

           // If both divisors are same
           // then add it only once else
           // add both
           if (i == (num / i))
               result += i;
           else
               result += (i + num / i);
       }
    }

    // Add 1 to the result as
    // 1 is also a divisor
    return (result + 1);
}

// Function to check if N is a
// Untouchable Number
static bool isUntouchable(int n)
{
    for(int i = 1; i <= 2 * n; i++)
    {
       if (divSum(i) == n)
           return false;
    }
    return true;
}

// Driver code
public static void Main()
{

    // Given Number N
    int n = 52;

    // Function Call
    if (isUntouchable(n))
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
// JavaScript program for the above approach

// Function to calculate sum of
// all proper divisors of num
function divSum(num)
{

    // Final result of summation
    // of divisors
    let result = 0;

    // Find all divisors of num
    for (let i = 2; i <= Math.sqrt(num); i++)
    {

        // If 'i' is divisor of 'num'
        if (num % i == 0)
        {

            // If both divisors are same
            // then add it only once else
            // add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }

    // Add 1 to the result as
    // 1 is also a divisor
    return (result + 1);
}

// Function to check if N is a
// Untouchable Number
function isUntouchable(n)
{
    for (let i = 1; i <= 2 * n; i++)
    {
        if (divSum(i) == n)
            return false;
    }
    return true;
}

// Driver Code

// Given Number n
let n = 52;

// Function Call
if (isUntouchable(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by blalverma92
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(sqrt(N))*