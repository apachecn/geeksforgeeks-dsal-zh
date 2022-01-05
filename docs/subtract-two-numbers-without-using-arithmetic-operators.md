# 不使用算术运算符减去两个数

> 原文:[https://www . geesforgeks . org/减法-不使用算术运算符的二进制数/](https://www.geeksforgeeks.org/subtract-two-numbers-without-using-arithmetic-operators/)

编写一个减法函数(x，y)，返回 x-y，其中 x 和 y 是整数。该函数不应使用任何算术运算符(+、++、–、-..等等)。
想法是使用按位运算符。[两个数的相加已经使用按位运算符](https://www.geeksforgeeks.org/add-two-numbers-without-using-arithmetic-operators/)进行了讨论。像加法一样，思路是用[减法器](http://en.wikipedia.org/wiki/Subtractor)逻辑。

下面给出了半减法器的真值表。

```
X     Y     Diff     Borrow
0     0     0     0
0     1     1     1
1     0     1     0
1     1     0     0
```

从上表可以画出“差”和“借”的卡诺图。
所以，逻辑方程是:

```
    Diff   = y ⊕ x
    Borrow = x' . y 
```

来源:[减法器维基百科页面](http://en.wikipedia.org/wiki/Subtractor)

以下是基于上述等式的实现。

## C++

```
// C++ program to Subtract two numbers
// without using arithmetic operators
#include <iostream>
using namespace std;

int subtract(int x, int y)
{
    // Iterate till there
    // is no carry
    while (y != 0)
    {
        // borrow contains common
        // set bits of y and unset
        // bits of x
        int borrow = (~x) & y;

        // Subtraction of bits of x
        // and y where at least one
        // of the bits is not set
        x = x ^ y;

        // Borrow is shifted by one
        // so that subtracting it from
        // x gives the required sum
        y = borrow << 1;
    }
    return x;
}

// Driver Code
int main()
{
    int x = 29, y = 13;
    cout << "x - y is " << subtract(x, y);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to Subtract two numbers
// without using arithmetic operators
#include<stdio.h>

int subtract(int x, int y)
{
    // Iterate till there
    // is no carry
    while (y != 0)
    {
        // borrow contains common
        // set bits of y and unset
        // bits of x
        int borrow = (~x) & y;

        // Subtraction of bits of x
        // and y where at least one
        // of the bits is not set
        x = x ^ y;

        // Borrow is shifted by one
        // so that subtracting it from
        // x gives the required sum
        y = borrow << 1;
    }
    return x;
}

// Driver Code
int main()
{
    int x = 29, y = 13;
    printf("x - y is %d", subtract(x, y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to subtract two Number
// without using arithmetic operator
import java.io.*;

class GFG
{
    static int subtract(int x, int y)
    {

    // Iterate till there
    // is no carry
    while (y != 0)
    {
        // borrow contains common
        // set bits of y and unset
        // bits of x
        int borrow = (~x) & y;

        // Subtraction of bits of x
        // and y where at least one
        // of the bits is not set
        x = x ^ y;

        // Borrow is shifted by one
        // so that subtracting it from
        // x gives the required sum
        y = borrow << 1;
    }

    return x;
}

    // Driver Code
    public static void main (String[] args)
    {
        int x = 29, y = 13;

        System.out.println("x - y is " +
                        subtract(x, y));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
def subtract(x, y):

    # Iterate till there
    # is no carry
    while (y != 0):

        # borrow contains common
        # set bits of y and unset
        # bits of x
        borrow = (~x) & y

        # Subtraction of bits of x
        # and y where at least one
        # of the bits is not set
        x = x ^ y

        # Borrow is shifted by one
        # so that subtracting it from
        # x gives the required sum
        y = borrow << 1

    return x

# Driver Code
x = 29
y = 13
print("x - y is",subtract(x, y))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to subtract two Number
// without using arithmetic operator
using System;

class GFG {

    static int subtract(int x, int y)
    {

        // Iterate till there
        // is no carry
        while (y != 0)
        {

            // borrow contains common
            // set bits of y and unset
            // bits of x
            int borrow = (~x) & y;

            // Subtraction of bits of x
            // and y where at least one
            // of the bits is not set
            x = x ^ y;

            // Borrow is shifted by one
            // so that subtracting it from
            // x gives the required sum
            y = borrow << 1;
        }

        return x;
    }

    // Driver Code
    public static void Main ()
    {
        int x = 29, y = 13;

        Console.WriteLine("x - y is " +
                        subtract(x, y));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to subtract two Number
// without using arithmetic operator

function subtract($x, $y)
{

    // Iterate till there is no carry
    while ($y != 0)
    {

        // borrow contains common set
        // bits of y and unset
        // bits of x
        $borrow = (~$x) & $y;

        // Subtraction of bits of x
        // and y where at least
        // one of the bits is not set

        $x = $x ^ $y;

        // Borrow is shifted by one so
        // that subtracting it from
        // x gives the required sum

        $y = $borrow << 1;
    }
    return $x;
}

        // Driver Code
        $x = 29; $y = 13;
        echo "x - y is ", subtract($x,$y);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to Subtract two numbers
// without using arithmetic operators

function subtract(x, y)
{
    // Iterate till there
    // is no carry
    while (y != 0)
    {
        // borrow contains common
        // set bits of y and unset
        // bits of x
        let borrow = (~x) & y;

        // Subtraction of bits of x
        // and y where at least one
        // of the bits is not set
        x = x ^ y;

        // Borrow is shifted by one
        // so that subtracting it from
        // x gives the required sum
        y = borrow << 1;
    }
    return x;
}

// Driver Code

let x = 29, y = 13;
document.write("x - y is " + subtract(x, y));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
x - y is 16
```

时间复杂度:0(对数 y)

辅助空间:0(1)

下面是相同方法的递归实现。

## C++

```
#include <iostream>
using namespace std;

int subtract(int x, int y)
{
    if (y == 0)
        return x;
    return subtract(x ^ y, (~x & y) << 1);
}

// Driver program
int main()
{
    int x = 29, y = 13;
    cout << "x - y is "<< subtract(x, y);
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include<stdio.h>

int subtract(int x, int y)
{
    if (y == 0)
        return x;
    return subtract(x ^ y, (~x & y) << 1);
}

// Driver program
int main()
{
    int x = 29, y = 13;
    printf("x - y is %d", subtract(x, y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  Program to subtract two Number
// without using arithmetic operator
// Recursive implementation.
class GFG {

    static int subtract(int x, int y)
    {

        if (y == 0)
            return x;

        return subtract(x ^ y, (~x & y) << 1);
    }

    // Driver program
    public static void main(String[] args)
    {
        int x = 29, y = 13;
        System.out.printf("x - y is %d",
                            subtract(x, y));
    }
}

// This code is contributed by 
// Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python  Program to
# subtract two Number
# without using arithmetic operator
# Recursive implementation.

def subtract(x, y):

    if (y == 0):
        return x
    return subtract(x ^ y, (~x & y) << 1)

# Driver program
x = 29
y = 13
print("x - y is", subtract(x, y))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to subtract two Number
// without using arithmetic operator
// Recursive implementation.
using System;

class GFG {

    static int subtract(int x, int y)
    {
        if (y == 0)
            return x;

        return subtract(x ^ y, (~x & y) << 1);
    }

    // Driver program
    public static void Main()
    {
        int x = 29, y = 13;
        Console.WriteLine("x - y is "+
                            subtract(x, y));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

function subtract($x, $y)
{
    if ($y == 0)
        return $x;
    return subtract($x ^ $y,
                   (~$x & $y) << 1);
}

// Driver Code
$x = 29; $y = 13;
echo "x - y is ", subtract($x, $y);

# This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript  Program to subtract two Number
// without using arithmetic operator
// Recursive implementation.  
function subtract(x , y)
{

    if (y == 0)
        return x;

    return subtract(x ^ y, (~x & y) << 1);
}

// Driver program
var x = 29, y = 13;
document.write("x - y is "+
                    subtract(x, y));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
x - y is 16
```

时间复杂度:0(对数 y)

辅助空间:0(对数 y)

本文由**Dheraj**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息