# 从 2 到 N/2 的所有基数中写入的数字 N 的位数之和

> 原文:[https://www . geesforgeks . org/数字总和-n-in-all-base-from-2-n-2/](https://www.geeksforgeeks.org/sum-of-the-digits-of-a-number-n-written-in-all-bases-from-2-to-n-2/)

给定一个整数 **N** ，任务是找出从 **2** 到 **N / 2** 的所有基数中所写的数字 **N** 的位数之和。
**举例:**

> **输入:** N = 6
> **输出:** 4
> 在基数 2 中，6 表示为 110。
> 在基数 3 中，6 表示为 20。
> Sum = 1 + 1 + 0 + 2 + 0 = 4
> **输入:** N = 8
> **输出:** 7

**进场:**

*   对于从 **2** 到 **(n / 2)** 的每个基数，用以下公式计算特定基数中 **n** 的位数:
    *   将 **n** 除以**基数**计算**余数**，余数为该基数中 **n** 的一位数。
    *   将数字加到**和**上，更新 n 为 **(n = n /基数)**。
    *   重复上述步骤，同时 **n > 0**
*   打印上一步计算的**和**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of the digits of
// n in the given base
int solve(int n, int base)
{
    // Sum of digits
    int sum = 0;

    while (n > 0) {

        // Digit of n in the given base
        int remainder = n % base;

        // Add the digit
        sum += remainder;
        n = n / base;
    }

    return sum;
}

// Function to calculate the sum of
// digits of n in bases from 2 to n/2
void SumsOfDigits(int n)
{
    // to store digit sum in all bases
    int sum = 0;

    // function call for multiple bases
    for (int base = 2; base <= n / 2; ++base)
        sum += solve(n, base);

    cout << sum;
}

// Driver program
int main()
{
    int n = 8;
    SumsOfDigits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Function to calculate the sum of the digits of
// n in the given base
static int solve(int n, int base)
{
    // Sum of digits
    int sum = 0;

    while (n > 0) {

        // Digit of n in the given base
        int remainder = n % base;

        // Add the digit
        sum += remainder;
        n = n / base;
    }

    return sum;
}

// Function to calculate the sum of
// digits of n in bases from 2 to n/2
static void SumsOfDigits(int n)
{
    // to store digit sum in all bases
    int sum = 0;

    // function call for multiple bases
    for (int base = 2; base <= n / 2; ++base)
        sum += solve(n, base);

    System.out.println(sum);
}

// Driver program

    public static void main (String[] args) {
        int n = 8;
    SumsOfDigits(n);
    }

}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import floor
# Function to calculate the sum of the digits of
# n in the given base
def solve(n, base):
    # Sum of digits
    sum = 0

    while (n > 0):
        # Digit of n in the given base
        remainder = n % base

        # Add the digit
        sum = sum + remainder
        n = int(n / base)

    return sum

# Function to calculate the sum of
# digits of n in bases from 2 to n/2
def SumsOfDigits(n):

    # to store digit sum in all base
    sum = 0
    N = floor(n/2)
    # function call for multiple bases
    for base in range(2,N+1,1):
        sum = sum + solve(n, base)

    print(sum)

# Driver program
if __name__ == '__main__':
    n = 8
    SumsOfDigits(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate the sum of
// the digits of n in the given base
static int solve(int n, int base1)
{
    // Sum of digits
    int sum = 0;

    while (n > 0)
    {

        // Digit of n in the given base
        int remainder1 = n % base1;

        // Add the digit
        sum += remainder1;
        n = n / base1;
    }

    return sum;
}

// Function to calculate the sum of
// digits of n in base1s from 2 to n/2
static void SumsOfDigits(int n)
{
    // to store digit sum in all bases
    int sum = 0;

    // function call for multiple bases
    for (int base1 = 2;
             base1 <= n / 2; ++base1)
        sum += solve(n, base1);

    Console.WriteLine(sum);
}

// Driver Code
public static void Main (String []args)
{
    int n = 8;
    SumsOfDigits(n);
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to calculate the sum of
// the digits of n in the given base
function solve($n, $base)
{
    // Sum of digits
    $sum = 0;

    while ($n > 0)
    {

        // Digit of n in the given base
        $remainder = $n % $base;

        // Add the digit
        $sum += $remainder;
        $n = $n / $base;
    }

    return $sum;
}

// Function to calculate the sum of
// digits of n in bases from 2 to n/2
function SumsOfDigits($n)
{
    // to store digit sum in all bases
    $sum = 0;

    // function call for multiple bases
    for ($base = 2;
         $base <= $n / 2; ++$base)
        $sum += solve($n, $base);

    echo $sum;
}

// Driver Code
$n = 8;
SumsOfDigits($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to calculate the sum of the digits of
    // n in the given base
    function solve(n , base)
    {

        // Sum of digits
        var sum = 0;

        while (n > 0) {

            // Digit of n in the given base
            var remainder = n % base;

            // Add the digit
            sum += remainder;
            n = parseInt(n / base);
        }

        return sum;
    }

    // Function to calculate the sum of
    // digits of n in bases from 2 to n/2
    function SumsOfDigits(n)
    {

        // to store digit sum in all bases
        var sum = 0;

        // function call for multiple bases
        for (base = 2; base <= n / 2; ++base)
            sum += solve(n, base);

        document.write(sum);
    }

    // Driver program
        var n = 8;
        SumsOfDigits(n);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
7
```