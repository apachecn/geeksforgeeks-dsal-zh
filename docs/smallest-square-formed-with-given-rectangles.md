# 由给定矩形形成的最小正方形

> 原文:[https://www . geeksforgeeks . org/最小方形带给定矩形/](https://www.geeksforgeeks.org/smallest-square-formed-with-given-rectangles/)

给定一个长度为 **l** 和宽度为 **b** 的矩形，我们需要找到由这些给定尺寸的矩形所能形成的最小正方形的面积。
**例:**

```
Input : 1 2
Output : 4
We can form a 2 x 2 square
using two rectangles of size
1 x 2.

Input : 7 10
Output :4900
```

假设我们想用长度为 **l** & **b** 的矩形制作一个边长为 **a** 的正方形。这意味着 **a** 是 **l** & **b** 的倍数。既然我们想要最小的正方形，那就必须是 **l** & **b** 的**最低公倍数** (LCM)。
**程序 1** :

## C++

```
// C++ Program to find the area
// of the smallest square which
// can be formed with rectangles
// of given dimensions
#include <bits/stdc++.h>
using namespace std;
// Recursive function to return gcd of a and b
int gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to find the area
// of the smallest square
int squarearea(int l, int b)
{

    // the length or breadth or side
    // cannot be negative
    if (l < 0 || b < 0)
        return -1;

        // LCM of length and breadth
        int n = (l * b) / gcd(l, b);

        // squaring to get the area
        return n * n;

}

// Driver code
int main()
{
    int l = 6, b = 4;
    cout << squarearea(l, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JavaProgram to find the area
// of the smallest square which
// can be formed with rectangles
// of given dimensions
class GFG
{

// Recursive function to
// return gcd of a and b
static int gcd(int a, int b)
{
// Everything divides 0
if (a == 0 || b == 0)
    return 0;

// Base case
if (a == b)
    return a;

// a is greater
if (a > b)
    return gcd(a - b, b);
return gcd(a, b - a);
}

// Function to find the area
// of the smallest square
static int squarearea(int l, int b)
{

// the length or breadth or side
// cannot be negative
if (l < 0 || b < 0)
    return -1;

    // LCM of length and breadth
    int n = (l * b) / gcd(l, b);

    // squaring to get the area
    return n * n;

}

// Driver code
public static void main(String[] args)
{
    int l = 6, b = 4;
    System.out.println(squarearea(l, b));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 Program to find the area
# of the smallest square which
# can be formed with rectangles
# of given dimensions

# Recursive function to return gcd of a and b
def gcd( a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # Base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return gcd(a - b, b)
    return gcd(a, b - a)

# Function to find the area
# of the smallest square
def squarearea( l, b):

    # the length or breadth or side
    # cannot be negative
    if (l < 0 or b < 0):
        return -1

        # LCM of length and breadth
    n = (l * b) / gcd(l, b)

        # squaring to get the area
    return n * n

# Driver code
if __name__=='__main__':
    l = 6
    b = 4
    print(int(squarearea(l, b)))

#This code is contributed by ash264
```

## C#

```
// C# Program to find the area
// of the smallest square which
// can be formed with rectangles
// of given dimensions
using System;

class GFG
{

// Recursive function to
// return gcd of a and b
static int gcd(int a, int b)
{
// Everything divides 0
if (a == 0 || b == 0)
    return 0;

// Base case
if (a == b)
    return a;

// a is greater
if (a > b)
    return gcd(a - b, b);
return gcd(a, b - a);
}

// Function to find the area
// of the smallest square
static int squarearea(int l, int b)
{

// the length or breadth or side
// cannot be negative
if (l < 0 || b < 0)
    return -1;

    // LCM of length and breadth
    int n = (l * b) / gcd(l, b);

    // squaring to get the area
    return n * n;

}

// Driver code
public static void Main()
{
    int l = 6, b = 4;
    Console.Write(squarearea(l, b));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the area
// of the smallest square which
// can be formed with rectangles
// of given dimensions

// Recursive function to
// return gcd of a and b
function gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // Base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return gcd($a - $b, $b);
    return gcd($a, $b - $a);
}

// Function to find the area
// of the smallest square
function squarearea($l, $b)
{

    // the length or breadth or side
    // cannot be negative
    if ($l < 0 || $b < 0)
        return -1;

        // LCM of length and breadth
        $n = ($l * $b) / gcd($l, $b);

        // squaring to get the area
        return $n * $n;

}

// Driver code
$l = 6;
$b = 4;
echo squarearea($l, $b)."\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the area
// of the smallest square which
// can be formed with rectangles
// of given dimensions

// Recursive function to
// return gcd of a and b
function gcd(a , b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to find the area
// of the smallest square
function squarearea(l , b)
{

// the length or breadth or side
// cannot be negative
if (l < 0 || b < 0)
    return -1;

    // LCM of length and breadth
    var n = (l * b) / gcd(l, b);

    // squaring to get the area
    return n * n;

}

// Driver code

    var l = 6, b = 4;
    document.write(squarearea(l, b));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
144
```