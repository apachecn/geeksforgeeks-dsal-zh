# 检查一个数字是否是一个完美的正方形，它的所有数字都是完美的正方形

> 原文:[https://www . geesforgeks . org/check-如果一个数字是一个完美的正方形，那么它的所有数字都是一个完美的正方形/](https://www.geeksforgeeks.org/check-if-a-number-is-a-perfect-square-having-all-its-digits-as-a-perfect-square/)

给定一个整数 **N** ，任务是[检查给定的数字是否是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，它的所有数字是否都是一个[完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果发现是真的，则打印“**是”**。否则，打印“**否”**。
**示例:**

> **输入:** N = 144
> **输出:**是
> **说明:**
> 数字 144 是一个完美的正方形，数字{1(= 1 <sup>2</sup> ，4(= 2 <sup>2</sup> }的位数也是一个完美的正方形。
> **输入:** N = 81
> **输出:**否

**方法:**想法是检查给定的数字 **N** 是否是一个完美的正方形。如果发现是真的，检查其所有数字是 **0** 、 **1** 、 **4** 还是 **9** 。如果发现是真的，打印“**是”**。否则，打印“**否”**。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if digits of
// N is a perfect square or not
bool check_digits(long N)
{

    // Iterate over the digits
    while (N > 0) {

        // Extract the digit
        int n = N % 10;

        // Check if digit is a
        // perfect square or not
        if ((n != 0) && (n != 1)
            && (n != 4) && (n != 9)) {
            return 0;
        }

        // Divide N by 10
        N = N / 10;
    }

    // Return true
    return 1;
}

// Function to check if N is
// a perfect square or not
bool is_perfect(long N)
{
    long double n = sqrt(N);

    // If floor and ceil of n
    // is not same
    if (floor(n) != ceil(n)) {
        return 0;
    }
    return 1;
}

// Function to check if N satisfies
// the required conditions or not
void isFullSquare(long N)
{
    // If both the conditions
    // are satisfied
    if (is_perfect(N)
        && check_digits(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    long N = 144;

    // Function Call
    isFullSquare(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to check if digits of
// N is a perfect square or not
static boolean check_digits(long N)
{
  // Iterate over the digits
  while (N > 0)
  {
    // Extract the digit
    int n = (int) (N % 10);

    // Check if digit is a
    // perfect square or not
    if ((n != 0) && (n != 1) &&
        (n != 4) && (n != 9))
    {
      return false;
    }

    // Divide N by 10
    N = N / 10;
  }

  // Return true
  return true;
}

// Function to check if N is
// a perfect square or not
static boolean is_perfect(long N)
{
  double n = Math.sqrt(N);

  // If floor and ceil of n
  // is not same
  if (Math.floor(n) != Math.ceil(n))
  {
    return false;
  }
  return true;
}

// Function to check if N satisfies
// the required conditions or not
static void isFullSquare(long N)
{
  // If both the conditions
  // are satisfied
  if (is_perfect(N) &&
      check_digits(N))
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}

// Driver Code
public static void main(String[] args)
{
  long N = 144;

  // Function Call
  isFullSquare(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if digits of
# N is a perfect square or not
def check_digits(N):

    # Iterate over the digits
    while (N > 0):

        # Extract the digit
        n = N % 10

        # Check if digit is a
        # perfect square or not
        if ((n != 0) and (n != 1) and
            (n != 4) and (n != 9)):
            return 0

        # Divide N by 10
        N = N // 10

    # Return true
    return 1

# Function to check if N is
# a perfect square or not
def is_perfect(N):

    n = math.sqrt(N)

    # If floor and ceil of n
    # is not same
    if (math.floor(n) != math.ceil(n)):
        return 0

    return 1

# Function to check if N satisfies
# the required conditions or not
def isFullSquare(N):

    # If both the conditions
    # are satisfied
    if (is_perfect(N) and
      check_digits(N)):
        print("Yes")
    else:
        print("No")

# Driver Code
N = 144

# Function call
isFullSquare(N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check if digits of
// N is a perfect square or not
static bool check_digits(long N)
{
  // Iterate over the digits
  while (N > 0)
  {
    // Extract the digit
    int n = (int) (N % 10);

    // Check if digit is a
    // perfect square or not
    if ((n != 0) && (n != 1) &&
        (n != 4) && (n != 9))
    {
      return false;
    }

    // Divide N by 10
    N = N / 10;
  }

  // Return true
  return true;
}

// Function to check if N is
// a perfect square or not
static bool is_perfect(long N)
{
  double n = Math.Sqrt(N);

  // If floor and ceil of n
  // is not same
  if (Math.Floor(n) != Math.Ceiling(n))
  {
    return false;
  }
  return true;
}

// Function to check if N satisfies
// the required conditions or not
static void isFullSquare(long N)
{
  // If both the conditions
  // are satisfied
  if (is_perfect(N) &&
      check_digits(N))
  {
    Console.Write("Yes");
  }
  else
  {
    Console.Write("No");
  }
}

// Driver Code
public static void Main()
{
  long N = 144;

  // Function Call
  isFullSquare(N);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if digits of
// N is a perfect square or not
function check_digits(N)
{

    // Iterate over the digits
    while (N > 0) {

        // Extract the digit
        let n = N % 10;

        // Check if digit is a
        // perfect square or not
        if ((n != 0) && (n != 1)
            && (n != 4) && (n != 9)) {
            return 0;
        }

        // Divide N by 10
        N = Math.floor(N / 10);
    }

    // Return true
    return 1;
}

// Function to check if N is
// a perfect square or not
function is_perfect(N)
{
    let n = Math.sqrt(N);

    // If floor and ceil of n
    // is not same
    if (Math.floor(n) != Math.ceil(n)) {
        return 0;
    }
    return 1;
}

// Function to check if N satisfies
// the required conditions or not
function isFullSquare(N)
{
    // If both the conditions
    // are satisfied
    if (is_perfect(N)
        && check_digits(N)) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }
}

// Driver Code

    let N = 144;

    // Function Call
    isFullSquare(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*