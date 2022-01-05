# 检查一个数字是否为全斐波那契数

> 原文:[https://www . geesforgeks . org/check-a-number-full-Fibonacci-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-full-fibonacci-or-not/)

给定一个数字 **N** ，任务是检查给定的数字及其所有数字是否都是斐波那契数列。如果是，那么给定的数字是一个完整的斐波那契数，否则不是。
**例:**

> **输入:** 13
> **输出:**是
> **说明:** 13 及其数字 1 和 3 均为斐波那契数
> 
> **输入:** 34
> **输出:**否
> **说明:** 4 不是斐波那契数。

**方法:**
首先检查 **N** 的所有数字是否都是[斐波那契](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。如果是，同样地，如果且仅当 **(5*N <sup>2 + 4)</sup>** 或**(5 * N<sup>2</sup>–4)**中的一个或两个是一个完美的正方形，则根据一个数是斐波那契数的原理检查 **N** 是否是斐波那契数。
下面的代码是上述方法的实现:

## C++

```
// C++ program to check
// if a given number is
// a Full Fibonacci
// Number or not

#include <bits/stdc++.h>
using namespace std;

// A utility function that
// returns true if x is
// perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Returns true if N is a
// Fibonacci Number
// and false otherwise
bool isFibonacci(int n)
{
    // N is Fibonacci if one
    // of 5*N^2 + 4 or 5*N^2 - 4
    // or both is a perferct square
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to check digits
bool checkDigits(int n)
{
    // Check if all digits
    // are fibonacci or not
    while (n) {

        // Extract digit
        int dig = n % 10;

        // Check if the current
        // digit is not fibonacci
        if (dig == 4 && dig == 6
            && dig == 7 && dig == 9)
            return false;

        n /= 10;
    }

    return true;
}

// Function to check and
// return if N is a Full
// Fibonacci number or not
int isFullfibonacci(int n)
{
    return (checkDigits(n)
            && isFibonacci(n));
}

// Driver Code
int main()
{
    int n = 13;
    if (isFullfibonacci(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// number is a full fibonacci
// number or not
import java.util.*;

class GFG {

// A utility function that returns
// true if x is perfect square
static boolean isPerfectSquare(int x)
{
    int s = (int) Math.sqrt(x);
    return (s * s == x);
}

// Returns true if N is a fibonacci
// number and false otherwise
static boolean isFibonacci(int n)
{

    // N is fibonacci if one of
    //  5 * N ^ 2 + 4 or 5 * N ^ 2 - 4
    // or both is a perferct square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to check digits
static boolean checkDigits(int n)
{

    // Check if all digits
    // are fibonacci or not
    while (n != 0)
    {

        // Extract digit
        int dig = n % 10;

        // Check if the current
        // digit is not fibonacci
        if (dig == 4 && dig == 6 &&
            dig == 7 && dig == 9)
            return false;

        n /= 10;
    }
    return true;
}

// Function to check and return if N
// is a full fibonacci number or not
static boolean isFullfibonacci(int n)
{
    return (checkDigits(n) &&
            isFibonacci(n));
}

// Driver code
public static void main(String[] args)
{
    int n = 13;

    if (isFullfibonacci(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to check
# if a given number is
# a Full Fibonacci
# Number or not
from math import *

# A utility function that
# returns true if x is
# perfect square
def isPerfectSquare(x):

    s = sqrt(x)
    return (s * s == x)

# Returns true if N is a
# Fibonacci Number
# and false otherwise
def isFibonacci(n):

    # N is Fibonacci if one
    # of 5 * N ^ 2 + 4 or 5 * N ^ 2 - 4
    # or both is a perferct square
    return (isPerfectSquare(5 * n * n + 4) or
            isPerfectSquare(5 * n * n - 4))

# Function to check digits
def checkDigits(n):

    # Check if all digits
    # are fibonacci or not
    while (n):

        # Extract digit
        dig = n % 10

        # Check if the current
        # digit is not fibonacci
        if (dig == 4 and dig == 6 and
            dig == 7 and dig == 9):
            return False

        n /= 10
    return True

# Function to check and
# return if N is a Full
# Fibonacci number or not
def isFullfibonacci(n):

    return (checkDigits(n) and isFibonacci(n))

# Driver Code
if __name__ == '__main__':

    n = 13

    if (isFullfibonacci(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Samarth
```

## C#

```
// C# program to check if a given
// number is a full fibonacci
// number or not
using System;

class GFG{

// A utility function that returns
// true if x is perfect square
static bool isPerfectSquare(int x)
{
    int s = (int)Math.Sqrt(x);
    return (s * s == x);
}

// Returns true if N is a fibonacci
// number and false otherwise
static bool isFibonacci(int n)
{

    // N is fibonacci if one of
    // 5 * N ^ 2 + 4 or 5 * N ^ 2 - 4
    // or both is a perferct square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to check digits
static bool checkDigits(int n)
{

    // Check if all digits
    // are fibonacci or not
    while (n != 0)
    {

        // Extract digit
        int dig = n % 10;

        // Check if the current
        // digit is not fibonacci
        if (dig == 4 && dig == 6 &&
            dig == 7 && dig == 9)
            return false;

        n /= 10;
    }
    return true;
}

// Function to check and return if N
// is a full fibonacci number or not
static bool isFullfibonacci(int n)
{
    return (checkDigits(n) &&
            isFibonacci(n));
}

// Driver code
public static void Main(String[] args)
{
    int n = 13;

    if (isFullfibonacci(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// Javascript program to check if a given
// number is a full fibonacci
// number or not

    // A utility function that returns
    // true if x is perfect square
    function isPerfectSquare(x) {
        var s = parseInt( Math.sqrt(x));
        return (s * s == x);
    }

    // Returns true if N is a fibonacci
    // number and false otherwise
    function isFibonacci(n) {

        // N is fibonacci if one of
        // 5 * N ^ 2 + 4 or 5 * N ^ 2 - 4
        // or both is a perferct square
        return isPerfectSquare(5 * n * n + 4) ||
        isPerfectSquare(5 * n * n - 4);
    }

    // Function to check digits
    function checkDigits(n) {

        // Check if all digits
        // are fibonacci or not
        while (n != 0) {

            // Extract digit
            var dig = n % 10;

            // Check if the current
            // digit is not fibonacci
            if (dig == 4 && dig == 6 && dig == 7
            && dig == 9)
                return false;

            n /= 10;
        }
        return true;
    }

    // Function to check and return if N
    // is a full fibonacci number or not
    function isFullfibonacci(n) {
        return (checkDigits(n) && isFibonacci(n));
    }

    // Driver code

        var n = 13;

        if (isFullfibonacci(n))
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

**时间复杂度:** O(1)

**辅助空间:** O(1)