# 检查 N 位数之和是否为回文

> 原文:[https://www . geesforgeks . org/check-if-of-n-is-回文数字总和/](https://www.geeksforgeeks.org/check-if-the-sum-of-digits-of-n-is-palindrome/)

给定一个整数 **N** ，任务是检查 **N** 的位数之和是否回文。
**例:**

> **输入:** N = 56
> **输出:**是
> 数字和为(5 + 6) = 11
> 为回文。
> **输入:** N = 51241
> **输出:** No
> (5 + 1 + 2 + 4 + 1) = 13

**逼近:**求 **N** 的位数之和，存入变量 **sum** 。现在使用本文[中讨论的方法检查**和**是否是回文。
以下是上述方法的实施:](https://www.geeksforgeeks.org/check-number-palindrome-not-without-using-extra-space/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// sum of digits of n
int digitSum(int n)
{
    int sum = 0;
    while (n > 0) {
        sum += (n % 10);
        n /= 10;
    }
    return sum;
}

// Function that returns true
// if n is palindrome
bool isPalindrome(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0) {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function that returns true if
// the digit sum of n is palindrome
bool isDigitSumPalindrome(int n)
{

    // Sum of the digits of n
    int sum = digitSum(n);

    // If the digit sum is palindrome
    if (isPalindrome(sum))
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 56;

    if (isDigitSumPalindrome(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// sum of digits of n
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += (n % 10);
        n /= 10;
    }
    return sum;
}

// Function that returns true
// if n is palindrome
static boolean isPalindrome(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0)
    {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function that returns true if
// the digit sum of n is palindrome
static boolean isDigitSumPalindrome(int n)
{

    // Sum of the digits of n
    int sum = digitSum(n);

    // If the digit sum is palindrome
    if (isPalindrome(sum))
        return true;
    return false;
}

// Driver code
public static void main(String []args)
{
    int n = 56;

    if (isDigitSumPalindrome(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# sum of digits of n
def digitSum(n) :

    sum = 0;
    while (n > 0) :
        sum += (n % 10);
        n //= 10;

    return sum;

# Function that returns true
# if n is palindrome
def isPalindrome(n) :

    # Find the appropriate divisor
    # to extract the leading digit
    divisor = 1;
    while (n // divisor >= 10) :
        divisor *= 10;

    while (n != 0) :
        leading = n // divisor;
        trailing = n % 10;

        # If first and last digit
        # not same return false
        if (leading != trailing) :
            return False;

        # Removing the leading and trailing
        # digit from number
        n = (n % divisor) // 10;

        # Reducing divisor by a factor
        # of 2 as 2 digits are dropped
        divisor = divisor // 100;

    return True;

# Function that returns true if
# the digit sum of n is palindrome
def isDigitSumPalindrome(n) :

    # Sum of the digits of n
    sum = digitSum(n);

    # If the digit sum is palindrome
    if (isPalindrome(sum)) :
        return True;
    return False;

# Driver code
if __name__ == "__main__" :

    n = 56;

    if (isDigitSumPalindrome(n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// sum of digits of n
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += (n % 10);
        n /= 10;
    }
    return sum;
}

// Function that returns true
// if n is palindrome
static bool isPalindrome(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0)
    {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function that returns true if
// the digit sum of n is palindrome
static bool isDigitSumPalindrome(int n)
{

    // Sum of the digits of n
    int sum = digitSum(n);

    // If the digit sum is palindrome
    if (isPalindrome(sum))
        return true;
    return false;
}

// Driver code
static public void Main ()
{
    int n = 56;

    if (isDigitSumPalindrome(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the
    // sum of digits of n
    function digitSum(n)
    {
        let sum = 0;
        while (n > 0)
        {
            sum += (n % 10);
            n = parseInt(n / 10, 10);
        }
        return sum;
    }

    // Function that returns true
    // if n is palindrome
    function isPalindrome(n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        let divisor = 1;
        while (parseInt(n / divisor, 10) >= 10)
            divisor *= 10;

        while (n != 0)
        {
            let leading = parseInt(n / divisor, 10);
            let trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digit from number
            n = parseInt((n % divisor) / 10, 10);

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = parseInt(divisor / 100, 10);
        }
        return true;
    }

    // Function that returns true if
    // the digit sum of n is palindrome
    function isDigitSumPalindrome(n)
    {

        // Sum of the digits of n
        let sum = digitSum(n);

        // If the digit sum is palindrome
        if (isPalindrome(sum))
            return true;
        return false;
    }

    let n = 56;

    if (isDigitSumPalindrome(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(logN)
T3】辅助空间: O(1)