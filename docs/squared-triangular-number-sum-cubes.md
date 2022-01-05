# 三角形的平方数(立方体的和)

> 原文:[https://www . geesforgeks . org/squared-triangular-number-sum-cubes/](https://www.geeksforgeeks.org/squared-triangular-number-sum-cubes/)

给定一个数字 s (1 <= s <= 1000000000). If s is [前 n 个自然数](https://www.geeksforgeeks.org/sum-cubes-even-odd-natural-numbers/)的立方之和，然后打印 n，否则打印-1。
前几个[方形三角数](https://en.wikipedia.org/wiki/Square_triangular_number)分别是 1、9、36、100、225、441、784、1296、2025、3025、……
**例:**

```
Input : 9
Output : 2
Explanation : The given number is
sum of cubes of first 2 natural
numbers.  1*1*1 + 2*2*2 = 9

Input : 13
Output : -1
```

一个**简单的解决方法**就是一个一个的把自然数的立方相加。如果当前总和等于给定的数字，那么我们返回到目前为止相加的自然数的计数。否则我们返回-1。

## C++

```
// C++ program to check if a
// given number is sum of
// cubes of natural numbers.
#include <iostream>
using namespace std;

// Function to find if
// the given number is
// sum of the cubes of
// first n natural numbers
int findS(int s)
{
    int sum = 0;

    // Start adding cubes of
    // the numbers from 1
    for (int n = 1; sum < s; n++)
    {
        sum += n * n * n;

        // If sum becomes equal to s
        // return n
        if (sum == s)
            return n;
    }

    return -1;
}

// Driver code
int main()
{
    int s = 9;
    int n = findS(s);
    n == -1 ? cout << "-1" : cout << n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a given number is sum of
// cubes of natural numbers.
class GFG
{

    // Function to find if
    // the given number is
    // sum of the cubes of
    // first n natural numbers
    static int findS(int s)
    {
        int sum = 0;

        // Start adding cubes of
        // the numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n * n * n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code
    public static void main(String[] args)
    {

        int s = 9;
        int n = findS(s);
        if (n == -1)
            System.out.println("-1");
        else
            System.out.println(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# if the given number is
# sum of the cubes of first
# n natural numbers

# Function to find if the
# given number is sum of
# the cubes of first n
# natural numbers
def findS (s):
    _sum = 0
    n = 1

    # Start adding cubes of
    # the numbers from 1
    while(_sum < s):
        _sum += n * n * n
        n += 1
    n-= 1

    # If sum becomes equal to s
    # return n
    if _sum == s:
        return n
    return -1

# Driver code
s = 9
n = findS (s)
if n == -1:
    print("-1")
else:
    print(n)
```

## C#

```
// C# program to check if a
// given number is sum of
// cubes of natural numbers.
using System;

class GFG
{

    // Function to find if the
    // given number is sum of
    // the cubes of first n
    // natural numbers
    public static int findS(int s)
    {
        int sum = 0;

        // Start adding cubes of
        // the numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n * n * n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

// Driver code
static public void Main (string []args)
{

    int s = 9;
    int n = findS(s);
    if (n == -1)
        Console.WriteLine("-1");
    else
        Console.WriteLine(n);
}
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a given number is sum of
// cubes of natural numbers.

// Function to find if the
// given number is sum of
// the cubes of first n
// natural numbers
function findS($s)
{
    $sum = 0;

    // Start adding cubes of
    // the numbers from 1
    for ($n = 1; $sum < $s; $n++)
    {
        $sum += $n * $n * $n;

        // If sum becomes equal to s
        // return n
        if ($sum == $s)
            return $n;
    }

    return -1;
}

// Driver code
$s = 9;
$n = findS($s);
if($n == -1)
    echo("-1");
else
    echo($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to check if a
// given number is sum of
// cubes of natural numbers.

// Function to find if
// the given number is
// sum of the cubes of
// first n natural numbers
function findS(s)
{
    let sum = 0;

    // Start adding cubes of
    // the numbers from 1
    for (let n = 1; sum < s; n++)
    {
        sum += n * n * n;

        // If sum becomes equal to s
        // return n
        if (sum == s)
            return n;
    }
    return -1;
}

// Driver code
    let s = 9;
    let n = findS(s);
    n == -1 ? document.write("-1") :document.write(n);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
2
```

一个**有效解**是基于公式【n(n+1)/2】<sup>2</sup>的前 n 个立方体的和。我们可以看到所有的数字都是正方形。
1) [检查给定的数字是否是完美的正方形。](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)
2)检查平方根是否为[三角形](https://www.geeksforgeeks.org/triangular-numbers/)(详见三角形数的方法 2)

## C++

```
// C++ program to check if a
// given number is sum of
// cubes of natural numbers.
#include <bits/stdc++.h>
using namespace std;

// Returns root of n(n+1)/2 = num
// if num is triangular (or integer
// root exists). Else returns -1.
int isTriangular(int num)
{
    if (num < 0)
        return false;

    // Considering the equation
    // n*(n+1)/2 = num. The equation
    // is : a(n^2) + bn + c = 0";
    int c = (-2 * num);
    int b = 1, a = 1;
    int d = (b * b) - (4 * a * c);

    if (d < 0)
        return -1;

    // Find roots of equation
    float root1 = ( -b + sqrt(d)) / (2 * a);
    float root2 = ( -b - sqrt(d)) / (2 * a);

    // checking if root1 is natural
    if (root1 > 0 && floor(root1) == root1)
        return root1;

    // checking if root2 is natural
    if (root2 > 0 && floor(root2) == root2)
        return root2;

    return -1;
}

// Returns square root of x if it is
// perfect square. Else returns -1.
int isPerfectSquare(long double x)
{
// Find floating point value of
// square root of x.
long double sr = sqrt(x);

// If square root is an integer
if ((sr - floor(sr)) == 0)
    return floor(sr);
else
    return -1;
}

// Function to find if the given number
// is sum of the cubes of first n
// natural numbers
int findS(int s)
{
    int sr = isPerfectSquare(s);
    if (sr == -1)
    return -1;
    return isTriangular(sr);
}

// Driver code
int main()
{
    int s = 9;
    int n = findS(s);
    n == -1 ? cout << "-1" : cout << n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if a given number is
// sum of cubes of natural
// numbers.
// import java.Math.*;
class GFG
{

// Returns root of n(n+1)/2 = num
// if num is triangular (or
// integer root exists). Else
// returns -1.
public static int isTriangular(int num)
{
    if (num < 0)
        return 0;

    // Considering the equation
    // n*(n+1)/2 = num. The equation
    // is : a(n^2) + bn + c = 0";
    int c = (-2 * num);
    int b = 1, a = 1;
    int d = (b * b) -
            (4 * a * c);

    if (d < 0)
        return -1;

    // Find roots of equation
    double root1 = (-b +
           Math.sqrt(d)) / (2 * a);
    double root2 = (-b -
           Math.sqrt(d)) / (2 * a);

    // checking if root1 is natural
    if ((int)(root1) > 0 &&
        (int)(Math.floor(root1)) ==
                   (int)(root1))
        return (int)(root1);

    // checking if
    // root2 is natural
    if ((int)(root2) > 0 &&
        (int)(Math.floor(root2)) ==
                   (int)(root2))
        return (int)(root2);

    return -1;
}

// Returns square root
// of x if it is perfect
// square. Else returns -1.
static int isPerfectSquare(double x)
{

// Find floating point
// value of square root of x.
double sr = Math.sqrt(x);

// If square root
// is an integer
if ((sr - Math.floor(sr)) == 0)
    return (int)(Math.floor(sr));
else
    return -1;
}

// Function to find if the
// given number is sum of
// the cubes of first n
// natural numbers
static int findS(int s)
{
    int sr = isPerfectSquare(s);
    if (sr == -1)
    return -1;
    return isTriangular(sr);
}

// Driver code
public static void main(String[] args)
{
    int s = 9;
    int n = findS(s);
    if(n == -1)
    System.out.println("-1");
    else
    System.out.println(n);
}
}

// This code is contributed
// by mits.
```

## 蟒蛇 3

```
# Python3 program to check
# if a given number is sum of
# cubes of natural numbers.
import math

# Returns root of n(n+1)/2 = num
# if num is triangular (or integer
# root exists). Else returns -1.
def isTriangular(num):
    if (num < 0):
        return False;

    # Considering the equation
    # n*(n+1)/2 = num. The equation
    # is : a(n^2) + bn + c = 0";
    c = (-2 * num);
    b = 1;
    a = 1;
    d = (b * b) - (4 * a * c);

    if (d < 0):
        return -1;

    # Find roots of equation
    root1 = (-b + math.sqrt(d)) // (2 * a);
    root2 = (-b - math.sqrt(d)) // (2 * a);

    # checking if root1 is natural
    if (root1 > 0 and
        math.floor(root1) == root1):
        return root1;

    # checking if root2 is natural
    if (root2 > 0 and
        math.floor(root2) == root2):
        return root2;

    return -1;

# Returns square root of
# x if it is perfect square.
# Else returns -1.
def isPerfectSquare(x):

    # Find floating point value
    # of square root of x.
    sr = math.sqrt(x);

    # If square root is an integer
    if ((sr - math.floor(sr)) == 0):
        return math.floor(sr);
    else:
        return -1;

# Function to find if the given
# number is sum of the cubes of
# first n natural numbers
def findS(s):
    sr = isPerfectSquare(s);
    if (sr == -1):
        return -1;
    return int(isTriangular(sr));

# Driver code
s = 9;
n = findS(s);
if(n == -1):
    print("-1");
else:
    print(n);

# This code is contributed by mits.
```

## C#

```
// C# program to check if a
// given number is sum of
// cubes of natural numbers.
using System;

class GFG
{

// Returns root of n(n+1)/2 = num
// if num is triangular (or integer
// root exists). Else returns -1.
static int isTriangular(int num)
{
    if (num < 0)
        return 0;

    // Considering the equation
    // n*(n+1)/2 = num. The equation
    // is : a(n^2) + bn + c = 0";
    int c = (-2 * num);
    int b = 1, a = 1;
    int d = (b * b) -
            (4 * a * c);

    if (d < 0)
        return -1;

    // Find roots of equation
    double root1 = (-b + Math.Sqrt(d)) / (2 * a);
    double root2 = (-b - Math.Sqrt(d)) / (2 * a);

    // checking if root1 is natural
    if ((int)(root1) > 0 &&
        (int)(Math.Floor(root1)) == (int)(root1))
        return (int)(root1);

    // checking if root2 is natural
    if ((int)(root2) > 0 &&
        (int)(Math.Floor(root2)) == (int)(root2))
        return (int)(root2);

    return -1;
}

// Returns square root of x
// if it is perfect square.
// Else returns -1.
static int isPerfectSquare(double x)
{

// Find floating point
// value of square root of x.
double sr = Math.Sqrt(x);

// If square root
// is an integer
if ((sr - Math.Floor(sr)) == 0)
    return (int)(Math.Floor(sr));
else
    return -1;
}

// Function to find if the
// given number is sum of
// the cubes of first n
// natural numbers
static int findS(int s)
{
    int sr = isPerfectSquare(s);
    if (sr == -1)
    return -1;
    return isTriangular(sr);
}

// Driver code
public static void Main()
{
    int s = 9;
    int n = findS(s);
    if(n == -1)
    Console.Write("-1");
    else
    Console.Write(n);
}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// given number is sum of
// cubes of natural numbers.

// Returns root of n(n+1)/2 = num
// if num is triangular (or integer
// root exists). Else returns -1.
function isTriangular($num)
{
    if ($num < 0)
        return false;

    // Considering the equation
    // n*(n+1)/2 = num. The equation
    // is : a(n^2) + bn + c = 0";
    $c = (-2 * $num);
    $b = 1;
    $a = 1;
    $d = ($b * $b) - (4 * $a * $c);

    if ($d < 0)
        return -1;

    // Find roots of equation
    $root1 = (-$b + sqrt($d)) /
                      (2 * $a);
    $root2 = (-$b - sqrt($d)) /
                      (2 * $a);

    // checking if root1 is natural
    if ($root1 > 0 &&
            floor($root1) == $root1)
        return $root1;

    // checking if root2 is natural
    if ($root2 > 0 &&
            floor($root2) == $root2)
        return $root2;

    return -1;
}

// Returns square root of 
// x if it is perfect square.
// Else returns -1.
function isPerfectSquare($x)
{

// Find floating point value
// of square root of x.
$sr = sqrt($x);

// If square root is an integer
if (($sr - floor($sr)) == 0)
    return floor($sr);
else
    return -1;
}

// Function to find if the given
// number is sum of the cubes of
// first n natural numbers
function findS($s)
{
    $sr = isPerfectSquare($s);
    if ($sr == -1)
    return -1;
    return isTriangular($sr);
}

// Driver code
$s = 9;
$n = findS($s);
if($n == -1)
echo "-1";
else
echo $n;

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// javascript program to check
// if a given number is
// sum of cubes of natural
// numbers.
// Returns root of n(n+1)/2 = num
    // if num is triangular (or
    // integer root exists). Else
    // returns -1.
    function isTriangular(num)
    {
        if (num < 0)
            return 0;

        // Considering the equation
        // n*(n+1)/2 = num. The equation
        // is : a(n^2) + bn + c = 0";
        var c = (-2 * num);
        var b = 1, a = 1;
        var d = (b * b) - (4 * a * c);

        if (d < 0)
            return -1;

        // Find roots of equation
        var root1 = (-b + Math.sqrt(d)) / (2 * a);
        var root2 = (-b - Math.sqrt(d)) / (2 * a);

        // checking if root1 is natural
        if (parseInt( (root1)) > 0 && parseInt( (Math.floor(root1))) == parseInt( (root1)))
            return parseInt(root1);

        // checking if
        // root2 is natural
        if (parseInt( (root2)) > 0 && parseInt( (Math.floor(root2))) == parseInt( (root2)))
            return parseInt( (root2));

        return -1;
    }

    // Returns square root
    // of x if it is perfect
    // square. Else returns -1.
    function isPerfectSquare(x)
    {

        // Find floating point
        // value of square root of x.
        var sr = Math.sqrt(x);

        // If square root
        // is an integer
        if ((sr - Math.floor(sr)) == 0)
            return parseInt( (Math.floor(sr)));
        else
            return -1;
    }

    // Function to find if the
    // given number is sum of
    // the cubes of first n
    // natural numbers
    function findS(s) {
        var sr = isPerfectSquare(s);
        if (sr == -1)
            return -1;
        return isTriangular(sr);
    }

    // Driver code

        var s = 9;
        var n = findS(s);
        if (n == -1)
            document.write("-1");
        else
            document.write(n);

// This code is contributed by Rajput-Ji.
</script>
```

**Output :** 

```
2
```