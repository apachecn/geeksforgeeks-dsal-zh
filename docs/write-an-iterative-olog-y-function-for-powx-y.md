# 为幂(x，y)

写一个迭代 O(Log y)函数

> 原文:[https://www . geesforgeks . org/write-an-iterative-olog-y-function-for-powx-y/](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/)

给定一个整数 x 和一个正数 y，编写一个函数，在以下条件下计算 x <sup>y</sup> 。
a)函数的时间复杂度应为 O(Log y)
b)额外空间为 O(1)

**示例:**

```
Input: x = 3, y = 5
Output: 243

Input: x = 2, y = 5
Output: 32

```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/abset-25327/1)

我们已经讨论了[幂](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)的递归 O(Log y)解。递归解决方案通常不是首选，因为它们需要调用堆栈上的空间，并且涉及函数调用开销。

以下是计算 x <sup>y</sup> 的实现。

## C++

```
// Iterative C program to implement pow(x, n)
#include <iostream>
using namespace std;

/* Iterative Function to calculate (x^y) in O(logy) */
int power(int x, unsigned int y)
{
    int res = 1; // Initialize result

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x; // Change x to x^2
    }
    return res;
}

// Driver program to test above functions
int main()
{
    int x = 3;
    unsigned int y = 5;

    cout<<"Power is "<<power(x, y);

    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// Iterative C++ program to implement pow(x, n)
#include <stdio.h>

/* Iterative Function to calculate (x^y) in O(logy) */
int power(int x, unsigned int y)
{
    int res = 1; // Initialize result

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x; // Change x to x^2
    }
    return res;
}

// Driver program to test above functions
int main()
{
    int x = 3;
    unsigned int y = 5;

    printf("Power is %d", power(x, y));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program
// to implement pow(x, n)
import java.io.*;

class GFG
{

/* Iterative Function to
calculate (x^y) in O(logy) */
static int power(int x, int y)
{
    // Initialize result
    int res = 1;

    while (y > 0)
    {
        // If y is odd,
        // multiply
        // x with result
        if ((y & 1) == 1)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x; // Change x to x^2
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int x = 3;
    int y = 5;

    System.out.println("Power is " +
                        power(x, y));
}
}

// This code is contributed
// by aj_36
```

## 蟒蛇 3

```
# Iterative Python3 program
# to implement pow(x, n)

# Iterative Function to
# calculate (x^y) in O(logy)
def power(x, y):

    # Initialize result
    res = 1

    while (y > 0):

        # If y is odd, multiply
        # x with result
        if ((y & 1) == 1) :
            res = res * x

        # y must be even
        # now y = y/2
        y = y >> 1

        # Change x to x^2
        x = x * x

    return res

# Driver Code
x = 3
y = 5

print("Power is ",
       power(x, y))

# This code is contributed
# by ihritik
```

## C#

```
// Iterative C# program
// to implement pow(x, n)
using System;

class GFG
{

/* Iterative Function to
calculate (x^y) in O(logy) */
static int power(int x, int y)
{
    int res = 1; // Initialize result

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) == 1)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x; // Change x to x^2
    }
    return res;
}

// Driver Code
static public void Main ()
{
int x = 3;
int y = 5;

Console.WriteLine("Power is "+
                   power(x, y));
}
}

// This code is contributed
// by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative php program
// to implement pow(x, n)>

// Iterative Function to
// calculate (x^y) in O(logy)

function power($x, $y)
{

    // Initialize result
    $res = 1;    

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = $res * $x;

        // y must be even now

        // y = y/2
        $y = $y >> 1;

        // Change x to x^2
        $x = $x * $x;
    }
    return $res;
}

    // Driver Code
    $x = 3;
    $y = 5;

    echo "Power is ", power($x, $y);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Iterative Javascript program to implement pow(x, n)

/* Iterative Function to calculate (x^y) in O(logy) */
function power(x, y)
{
// Initialize result
    let res = 1;

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x; // Change x to x^2
    }
    return res;
}

// Driver program to test above functions

    let x = 3;
    y = 5;

    document.write("Power is " + power(x, y));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Power is 243
```

***时间复杂度:** O(对数 y)*

***辅助空间:** O(1)*

本文由 **Udit Gupta** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息