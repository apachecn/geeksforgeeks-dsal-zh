# 完美数字不变量数

> 原文:[https://www . geesforgeks . org/perfect-digital-不变量-number/](https://www.geeksforgeeks.org/perfect-digital-invariants-number/)

如果一个正整数的数字的某个固定幂的和等于数字本身，则称之为**完美数字不变数**。
对于任意数， **abcd… =幂(a，n) +幂(b，n) +幂(c，n) +幂(d，n) + …。**、
其中 n 可以是大于 0 的任意整数。

### 检查 N 是否是完美数字不变数

给定一个数字 **N** ，任务是检查给定的数字 **N** 是否为**完美数字不变数**。如果 **N** 是**完美数字不变数**，则打印**“是”**否则打印**“否”**。
**例:**

> **输入:** N = 153
> **输出:**是
> **解释:**
> 153 是一个完美的数字不变量数至于 n = 3 我们有
> 1<sup>3</sup>+5<sup>3</sup>+3<sup>3</sup>= 153
> **输入:** 4150
> **输出:**是

**逼近:**对于数字 **N** 中的每一位数字，从固定的数字 1 开始计算其数位幂的和，直到 **N** 的数位幂之和超过 **N** 。如果 **N** 是**完美数字不变数**，则打印**“是”**否则打印**“否”**。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate x raised
// to the power y
int power(int x, unsigned int y)
{
    if (y == 0) {
        return 1;
    }

    if (y % 2 == 0) {
        return (power(x, y / 2)
                * power(x, y / 2));
    }
    return (x
            * power(x, y / 2)
            * power(x, y / 2));
}

// Function to check whether the given
// number is Perfect Digital Invariant
// number or not
bool isPerfectDigitalInvariant(int x)
{
    for (int fixed_power = 1;; fixed_power++) {

        int temp = x, sum = 0;

        // For each digit in temp
        while (temp) {

            int r = temp % 10;
            sum += power(r, fixed_power);
            temp = temp / 10;
        }

        // If satisfies Perfect Digital
        // Invariant condition
        if (sum == x) {
            return true;
        }
        // If sum exceeds n, then not possible
        if (sum > x) {
            return false;
        }
    }
}

// Driver Code
int main()
{
    // Given Number N
    int N = 4150;

    // Function Call
    if (isPerfectDigitalInvariant(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to calculate x raised
// to the power y
static int power(int x, int y)
{
    if (y == 0)
    {
        return 1;
    }

    if (y % 2 == 0)
    {
        return (power(x, y / 2) *
                power(x, y / 2));
    }
    return (x * power(x, y / 2) *
                power(x, y / 2));
}

// Function to check whether the given
// number is Perfect Digital Invariant
// number or not
static boolean isPerfectDigitalInvariant(int x)
{
    for (int fixed_power = 1;; fixed_power++)
    {
        int temp = x, sum = 0;

        // For each digit in temp
        while (temp > 0)
        {
            int r = temp % 10;
            sum += power(r, fixed_power);
            temp = temp / 10;
        }

        // If satisfies Perfect Digital
        // Invariant condition
        if (sum == x)
        {
            return true;
        }
        // If sum exceeds n, then not possible
        if (sum > x)
        {
            return false;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 4150;

    // Function Call
    if (isPerfectDigitalInvariant(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the
# sum of divisors
def power(x, y):
    if (y == 0):
        return 1
    if (y % 2 == 0):
        return (power(x, y//2) * power(x, y//2))
    return (x * power(x, y//2) * power(x, y//2))

# Function to check whether the given
# number is Perfect Digital Invariant
# number or not
def isPerfectDigitalInvariant(x):
    fixed_power = 0
    while True:
        fixed_power += 1
        temp = x
        summ = 0

        # For each digit in temp
        while (temp):
            r = temp % 10
            summ = summ + power(r, fixed_power)
            temp = temp//10

        # If satisfies Perfect Digital
        # Invariant condition
        if (summ == x):
            return (True)

        # If sum exceeds n, then not possible
        if (summ > x):
            return (False)

# Driver code
# Given Number N
N = 4150

# Function Call
if (isPerfectDigitalInvariant(N)):
    print("Yes")
else:
    print("No")

    # This code is contributed by vikas_g
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate x raised
// to the power y
static int power(int x, int y)
{
    if (y == 0)
    {
        return 1;
    }

    if (y % 2 == 0)
    {
        return (power(x, y / 2) *
                power(x, y / 2));
    }
    return (x * power(x, y / 2) *
                power(x, y / 2));
}

// Function to check whether the given
// number is Perfect Digital Invariant
// number or not
static bool isPerfectDigitalInvariant(int x)
{
    for(int fixed_power = 1;; fixed_power++)
    {
        int temp = x, sum = 0;

        // For each digit in temp
        while (temp > 0)
        {
            int r = temp % 10;
            sum += power(r, fixed_power);
            temp = temp / 10;
        }

        // If satisfies Perfect Digital
        // Invariant condition
        if (sum == x)
        {
            return true;
        }
        // If sum exceeds n, then not possible
        if (sum > x)
        {
            return false;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N
    int N = 4150;

    // Function call
    if (isPerfectDigitalInvariant(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation

// Function to calculate x raised
// to the power y
function power(x, y)
{
    if (y == 0) {
        return 1;
    }

    if (y % 2 == 0) {
        return (power(x, Math.floor(y / 2))
                * power(x, Math.floor(y / 2)));
    }
    return (x
            * power(x, Math.floor(y / 2))
            * power(x, Math.floor(y / 2)));
}

// Function to check whether the given
// number is Perfect Digital Invariant
// number or not
function isPerfectDigitalInvariant(x)
{
    for (var fixed_power = 1;; fixed_power++) {

        var temp = x, sum = 0;

        // For each digit in temp
        while (temp) {

            var r = temp % 10;
            sum += power(r, fixed_power);
            temp = Math.floor(temp / 10);
        }

        // If satisfies Perfect Digital
        // Invariant condition
        if (sum == x) {
            return true;
        }
        // If sum exceeds n, then not possible
        if (sum > x) {
            return false;
        }
    }
}

// Driver Code
// Given Number N
var N = 4150;

// Function Call
if (isPerfectDigitalInvariant(N))
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