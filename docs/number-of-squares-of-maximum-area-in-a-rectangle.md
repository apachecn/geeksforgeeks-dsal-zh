# 矩形中最大面积的平方数

> 原文:[https://www . geesforgeks . org/矩形最大面积平方数/](https://www.geeksforgeeks.org/number-of-squares-of-maximum-area-in-a-rectangle/)

给定一个边长为 m 和 n 的矩形。将矩形切割成相同的小块，使每个小块都是一个正方形，具有最大可能的边长，没有矩形的剩余部分。打印形成的此类正方形的数量。
**例:**

```
Input: 9 6
Output: 6
Rectangle can be cut into squares of size 3.

Input: 4 2
Output: 2
Rectangle can be cut into squares of size 2.
```

**方法:**任务是将矩形切割成边长为 s 的正方形，矩形没有剩余的部分，因此 **s** 必须将 **m** 和 **n** 分开。同样，正方形的边应该是最大可能的，因此，s 应该是 m 和 n 的最大公约数。
所以， **s = gcd(m，n)** 。
要找到矩形被切割成的方块数，需要做的任务是将矩形的面积除以大小为 s 的正方形的面积。

## C++

```
// C++ code for calculating the
// number of squares
#include <bits/stdc++.h>
using namespace std;

// Function to find number of squares
int NumberOfSquares(int x, int y)
{
    // Here in built c++ gcd function is used
    int s = __gcd(x, y);

    int ans = (x * y) / (s * s);

    return ans;
}

// Driver code
int main()
{
    int m = 385, n = 60;

    // Call the function NumberOfSquares
    cout << NumberOfSquares(m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for calculating
// the number of squares
import java.io.*;

class GFG
{
    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

// Function to find
// number of squares
static int NumberOfSquares(int x,
                           int y)
{
    // Here in built c++
    // gcd function is used
    int s = __gcd(x, y);

    int ans = (x * y) / (s * s);

    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int m = 385, n = 60;

    // Call the function
    // NumberOfSquares
    System.out.println(NumberOfSquares(m, n));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 code for calculating
# the number of squares

# Recursive function to
# return gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0;

    # base case
    if (a == b):
        return a;

    # a is greater
    if (a > b):
        return __gcd(a - b, b);
    return __gcd(a, b - a);

# Function to find
# number of squares
def NumberOfSquares(x, y):

    # Here in built PHP
    # gcd function is used
    s = __gcd(x, y);

    ans = (x * y) / (s * s);

    return int(ans);

# Driver Code
m = 385;
n = 60;

# Call the function
# NumberOfSquares
print(NumberOfSquares(m, n));

# This code is contributed
# by mit
```

## C#

```
// C# code for calculating
// the number of squares
using System;

class GFG
{

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

// Function to find
// number of squares
static int NumberOfSquares(int x,
                           int y)
{
    // Here in built c++
    // gcd function is used
    int s = __gcd(x, y);

    int ans = (x * y) /
              (s * s);

    return ans;
}

// Driver Code
static public void Main ()
{
int m = 385, n = 60;

// Call the function
// NumberOfSquares
Console.WriteLine(NumberOfSquares(m, n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for calculating
// the number of squares

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0 || $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// Function to find
// number of squares
function NumberOfSquares($x, $y)
{
    // Here in built PHP
    // gcd function is used
    $s = __gcd($x, $y);

    $ans = ($x * $y) /
           ($s * $s);

    return $ans;
}

// Driver Code
$m = 385;
$n = 60;

// Call the function
// NumberOfSquares
echo (NumberOfSquares($m, $n));

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript code for calculating the
// number of squares

function __gcd(a, b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Function to find number of squares
function NumberOfSquares(x, y)
{
    // Here in built c++ gcd function is used
    let s = __gcd(x, y);

    let ans = parseInt((x * y) / (s * s));

    return ans;
}

// Driver code
    let m = 385, n = 60;

    // Call the function NumberOfSquares
    document.write(NumberOfSquares(m, n));

</script>
```

**Output:** 

```
924
```