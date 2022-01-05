# 反完全数

> 原文:[https://www.geeksforgeeks.org/anti-perfect-number/](https://www.geeksforgeeks.org/anti-perfect-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为**反完美数字**。如果 **N** 是**反完善号**，则打印**“是”**否则打印**“否”**。

> 一个**反完型**数是一个等于其适当除数的倒数之和的数。

**例:**

> **输入:** N = 244
> **输出:**是
> **说明:**
> 24 的适当除数为 1、2、4、61、122
> 它们的倒数之和为 1 + 2 + 4 + 16 + 221 = 244 = N.
> **输入:** N = 28
> **输出:**否

**逼近**思路是求 N 个数的适当除数的倒数之和，检查和 if 是否等于 **N** 。如果总和等于 **N** ，则 **N** 为**反完善号**则打印**“是”**否则打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Iterative function to reverse
// digits of num
int rev(int num)
{
    int rev_num = 0;

    while (num > 0) {
        rev_num = rev_num * 10
                  + num % 10;

        num = num / 10;
    }

    // Return the reversed num
    return rev_num;
}

// Function to calculate sum
// of reverse all proper divisors
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
            // then add it only once
            // else add both
            if (i == (num / i))
                result += rev(i);
            else
                result += (rev(i)
                           + rev(num / i));
        }
    }

    // Add 1 to the result as 1
    // is also a divisor
    return (result + 1);
}

// Function to check if N is
// anti-perfect or not
bool isAntiPerfect(int n)
{
    return divSum(n) == n;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 244;

    // Function Call
    if (isAntiPerfect(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Iterative function to reverse
// digits of num
static int rev(int num)
{
    int rev_num = 0;

    while (num > 0)
    {
        rev_num = rev_num * 10 +
                      num % 10;

        num = num / 10;
    }

    // Return the reversed num
    return rev_num;
}

// Function to calculate sum
// of reverse all proper divisors
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
           // then add it only once
           // else add both
           if (i == (num / i))
               result += rev(i);
           else
               result += (rev(i) +
                          rev(num / i));
       }
    }

    // Add 1 to the result as 1
    // is also a divisor
    return (result + 1);
}

// Function to check if N is
// anti-perfect or not
static boolean isAntiPerfect(int n)
{
    return divSum(n) == n;
}

// Driver Code
public static void main (String[] args)
{

    // Given Number N
    int N = 244;

    // Function Call
    if (isAntiPerfect(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Iterative function to reverse
# digits of num
def rev(num):
    rev_num = 0
    while (num > 0) :
        rev_num = rev_num * 10 + num % 10
        num = num // 10

    # Return the reversed num
    return rev_num

# Function to calculate sum
# of reverse all proper divisors
def divSum(num) :

    # Final result of summation
    # of divisors
    result = 0

    # Find all divisors of num
    for i in range(2, int(num**0.5)):

        # If 'i' is divisor of 'num'
        if (num % i == 0) :

            # If both divisors are same
            # then add it only once
            # else add both
            if (i == (num / i)):
                result += rev(i)
            else:
                result += (rev(i) + rev(num / i))

    # Add 1 to the result as 1
    # is also a divisor
    return (result + 1)

# Function to check if N is
# anti-perfect or not
def isAntiPerfect(n):
    return divSum(n) == n

# Driver Code

# Given Number N
N = 244

# Function Call
if (isAntiPerfect(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Iterative function to reverse
// digits of num
static int rev(int num)
{
    int rev_num = 0;

    while (num > 0)
    {
        rev_num = rev_num * 10 +
                      num % 10;
        num = num / 10;
    }

    // Return the reversed num
    return rev_num;
}

// Function to calculate sum
// of reverse all proper divisors
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
            // then add it only once
            // else add both
            if (i == (num / i))
                result += rev(i);
            else
                result += (rev(i) +
                           rev(num / i));
        }
    }

    // Add 1 to the result as 1
    // is also a divisor
    return (result + 1);
}

// Function to check if N is
// anti-perfect or not
static Boolean isAntiPerfect(int n)
{
    return divSum(n) == n;
}

// Driver Code
public static void Main (String[] args)
{

    // Given Number N
    int N = 244;

    // Function Call
    if (isAntiPerfect(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript implementation

// Iterative function to reverse
// digits of num
function rev(num)
{
    var rev_num = 0;

    while (num > 0) {
        rev_num = rev_num * 10 + num % 10;
        num = Math.floor(num / 10);
    }

    // Return the reversed num

    return rev_num;
}

// Function to calculate sum
// of reverse all proper divisors
function divSum(num)
{
    // Final result of summation
    // of divisors
    var result = 0;

    // Find all divisors of num
    for (var i = 2; i <= Math.floor(Math.sqrt(num)); i++) {

        // If 'i' is divisor of 'num'
        if (num % i == 0) {

            // If both divisors are same
            // then add it only once
            // else add both
            if (i == (num / i))
                result += rev(i);
            else
                result += (rev(i)
                           + rev(num / i));
        }
    }

    // Add 1 to the result as 1
    // is also a divisor
     result += 1;
    return result;
}

// Function to check if N is
// anti-perfect or not
function isAntiPerfect(n)
{
    return divSum(n) == n;
}

// Driver Code
// Given Number N
var N = 244;

// Function Call
if (isAntiPerfect(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(sqrt(N))*