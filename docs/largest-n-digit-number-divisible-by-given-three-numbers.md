# 可被给定三个数整除的最大 N 位数

> 原文:[https://www . geesforgeks . org/最大 n 位数可被给定三位数除尽/](https://www.geeksforgeeks.org/largest-n-digit-number-divisible-by-given-three-numbers/)

给定四个整数 *x，y，z 和 n* ，任务是找到最大的 *n* 位数，该位数可被 *x，y 和 z* 整除。
**举例:**

> **输入:** x = 2，y = 3，z = 5，n = 4
> **输出:** 9990
> 9990 是可被 2、3、5 整除的最大 4 位数。
> **输入:** x = 3，y = 23，z = 6，n = 2
> **输出:**不可能

**进场:**

*   找到最大的 *n* 位数，即*幂(10，n)–1*，并将其存储在变量 *largestN* 中。
*   找出给定的三个数字 *x，y，z* 的 LCM，说 *LCM* 。
*   计算*最大值*除以 *LCM* 即*最大值% LCM* 时的余数，并将其存储在变量*余数*中。
*   从*大*中减去*余数*。如果结果仍然是 *n* 数字，则打印结果。
*   否则打印*不可能*。

以下是上述方法的实现:

## C++

```
// C++ program to find largest n digit number
// which is divisible by x, y and z.
#include <bits/stdc++.h>
using namespace std;

// Function to return the LCM of three numbers
int LCM(int x, int y, int z)
{
    int ans = ((x * y) / (__gcd(x, y)));
    return ((z * ans) / (__gcd(ans, z)));
}

// Function to return the largest n-digit
// number which is divisible by x, y and z
int findDivisible(int n, int x, int y, int z)
{

    // find the LCM
    int lcm = LCM(x, y, z);

    // find largest n-digit number
    int largestNDigitNum = pow(10, n) - 1;

    int remainder = largestNDigitNum % lcm;

    // If largest number is the answer
    if (remainder == 0)
        return largestNDigitNum ;

    // find closest smaller number
    // divisible by LCM
    largestNDigitNum -= remainder;

    // if result is an n-digit number
    if (largestNDigitNum >= pow(10, n - 1))
        return largestNDigitNum;
    else
        return 0;
}

// Driver code
int main()
{
    int n = 2, x = 3, y = 4, z = 6;
    int res = findDivisible(n, x, y, z);

    // if the number is found
    if (res != 0)
        cout << res;
    else
        cout << "Not possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest n digit number
// which is divisible by x, y and z.
import java.math.*;
class GFG {

// Recursive function to return gcd of a and b
    static int gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a-b, b);
        return gcd(a, b-a);
    }

// Function to return the LCM of three numbers
static int LCM(int x, int y, int z)
{
    int ans = ((x * y) / (gcd(x, y)));
    return ((z * ans) / (gcd(ans, z)));
}

// Function to return the largest n-digit
// number which is divisible by x, y and z
static int findDivisible(int n, int x, int y, int z)
{

    // find the LCM
    int lcm = LCM(x, y, z);

    // find largest n-digit number
    int largestNDigitNum = (int)Math.pow(10, n) - 1;

    int remainder = largestNDigitNum % lcm;

    // If largest number is the answer
    if (remainder == 0)
        return largestNDigitNum ;

    // find closest smaller number
    // divisible by LCM
    largestNDigitNum -= remainder;

    // if result is an n-digit number
    if (largestNDigitNum >= (int)Math.pow(10, n - 1))
        return largestNDigitNum;
    else
        return 0;
}

// Driver code
public static void main(String args[])
{
    int n = 2, x = 3, y = 4, z = 6;
    int res = findDivisible(n, x, y, z);

    // if the number is found
    if (res != 0)
        System.out.println(res);
    else
        System.out.println("Not possible");

}
}
```

## 蟒蛇 3

```
# Python3 program to find largest n digit
# number which is divisible by x, y and z.

# Recursive function to return
# gcd of a and b
def gcd(a, b):

    # Everything divides 0
    if (a == 0):
        return b;
    if (b == 0):
        return a;

    # base case
    if (a == b):
        return a;

    # a is greater
    if (a > b):
        return gcd(a - b, b);
    return gcd(a, b - a);

# Function to return the LCM
# of three numbers
def LCM(x, y, z):
    ans = ((x * y) / (gcd(x, y)));
    return ((z * ans) / (gcd(ans, z)));

# Function to return the largest n-digit
# number which is divisible by x, y and z
def findDivisible(n, x, y, z):

    # find the LCM
    lcm = LCM(x, y, z);

    # find largest n-digit number
    largestNDigitNum = int(pow(10, n)) - 1;

    remainder = largestNDigitNum % lcm;

    # If largest number is the answer
    if (remainder == 0):
        return largestNDigitNum ;

    # find closest smaller number
    # divisible by LCM
    largestNDigitNum -= remainder;

    # if result is an n-digit number
    if (largestNDigitNum >= int(pow(10, n - 1))):
        return largestNDigitNum;
    else:
        return 0;

# Driver code
n = 2; x = 3;
y = 4; z = 6;
res = int(findDivisible(n, x, y, z));

# if the number is found
if (res != 0):
    print(res);
else:
    print("Not possible");

# This code is contributed
# by mits
```

## C#

```
// C# program to find largest n
// digit number which is divisible
// by x, y and z.
using System;

class GFG
{
// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to return the
// LCM of three numbers
static int LCM(int x, int y, int z)
{
    int ans = ((x * y) / (gcd(x, y)));
    return ((z * ans) / (gcd(ans, z)));
}

// Function to return the largest
// n-digit number which is divisible
// by x, y and z
static int findDivisible(int n, int x,
                         int y, int z)
{

    // find the LCM
    int lcm = LCM(x, y, z);

    // find largest n-digit number
    int largestNDigitNum = (int)Math.Pow(10, n) - 1;

    int remainder = largestNDigitNum % lcm;

    // If largest number is the answer
    if (remainder == 0)
        return largestNDigitNum ;

    // find closest smaller number
    // divisible by LCM
    largestNDigitNum -= remainder;

    // if result is an n-digit number
    if (largestNDigitNum >= (int)Math.Pow(10, n - 1))
        return largestNDigitNum;
    else
        return 0;
}

// Driver code
static void Main()
{
    int n = 2, x = 3, y = 4, z = 6;
    int res = findDivisible(n, x, y, z);

    // if the number is found
    if (res != 0)
        Console.WriteLine(res);
    else
        Console.WriteLine("Not possible");
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest n digit number
// which is divisible by x, y and z.

// Recursive function to return gcd of a and b
function gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0)
        return $b;
    if ($b == 0)
        return $a;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return gcd($a - $b, $b);
    return gcd($a, $b - $a);
}

// Function to return the LCM
// of three numbers
function LCM($x, $y, $z)
{
$ans = (($x * $y) / (gcd($x, $y)));
return (($z * $ans) / (gcd($ans, $z)));
}

// Function to return the largest n-digit
// number which is divisible by x, y and z
function findDivisible($n, $x, $y, $z)
{

    // find the LCM
    $lcm = LCM($x, $y, $z);

    // find largest n-digit number
    $largestNDigitNum = (int)pow(10, $n) - 1;

    $remainder = $largestNDigitNum % $lcm;

    // If largest number is the answer
    if ($remainder == 0)
        return $largestNDigitNum ;

    // find closest smaller number
    // divisible by LCM
    $largestNDigitNum -= $remainder;

    // if result is an n-digit number
    if ($largestNDigitNum >= (int)pow(10, $n - 1))
        return $largestNDigitNum;
    else
        return 0;
}

// Driver code
$n = 2; $x = 3; $y = 4; $z = 6;
$res = findDivisible($n, $x, $y, $z);

// if the number is found
if ($res != 0)
    echo $res;
else
    echo "Not possible";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript program to find largest n
// digit number which is divisible
// by x, y and z.

// Recursive function to return
// gcd of a and b
function gcd(a, b)
{
    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to return the
// LCM of three numbers
function LCM(x, y, z)
{
    var ans = parseInt((x * y) / (gcd(x, y)));
    return parseInt((z * ans) / (gcd(ans, z)));
}

// Function to return the largest
// n-digit number which is divisible
// by x, y and z
function findDivisible(n, x, y, z)
{

    // find the LCM
    var lcm = LCM(x, y, z);

    // find largest n-digit number
    var largestNDigitNum = Math.pow(10, n) - 1;

    var remainder = largestNDigitNum % lcm;

    // If largest number is the answer
    if (remainder == 0)
        return largestNDigitNum ;

    // find closest smaller number
    // divisible by LCM
    largestNDigitNum -= remainder;

    // if result is an n-digit number
    if (largestNDigitNum >= Math.pow(10, n - 1))
        return largestNDigitNum;
    else
        return 0;
}

// Driver code
var n = 2, x = 3, y = 4, z = 6;
var res = findDivisible(n, x, y, z);
// if the number is found
if (res != 0)
    document.write(res);
else
    document.write("Not possible");

</script>
```

**Output:** 

```
96
```