# 求曲线上给定点的切线

> 原文:[https://www . geesforgeks . org/find-曲线上给定点的切线/](https://www.geeksforgeeks.org/find-tangent-at-a-given-point-on-the-curve/)

给定一条曲线**[y = x(A–x)]，**任务是找到该曲线上给定点(x，y)的切线，其中 A，x，y 为整数。
**例:**

```
Input: A = 2, x = 2, y = 0
Output: y = -2x - 4
Since y = x(2 - x)
      y = 2x - x^2 differentiate it with respect to x
      dy/dx = 2 - 2x  put x = 2, y = 0 in this equation
      dy/dx = 2 - 2* 2 = -2
      equation  => (Y - 0 ) = ((-2))*( Y - 2)
                => y = -2x -4

Input: A = 3, x = 4, y = 5
Output: Not possible
    Point is not on that curve
```

![](img/3ff7a90e9ff08da2102fc82bc2f5b7a7.png)

**进场:**

1.  首先找出给定点是否在那条曲线上。
2.  如果点在那条曲线上，那么求导数
3.  通过将 x，y 放入 dy/dx 计算切线的坡度。
4.  通过将切线的梯度和给定点的坐标代入直线方程的梯度点形式来确定切线的方程，其中法向方程为 Y–Y =(dy/dx)*(X–X)。

以下是上述方法的实现:

## C++

```
// C++ program for find Tangent
// on a curve at given point

#include <bits/stdc++.h>
using namespace std;

// function for find Tangent
void findTangent(int A, int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            cout << "y = "
                 << dif << "x" << (x * dif) + (y);

        else if (dif > 0)

            // differentiate is positive
            cout << "y = "
                 << dif << "x+" << -x * dif + y;

        // differentiate is zero
        else
            cout << "Not possible";
    }
}

// Driver code
int main()
{
    // declare variable
    int A = 2, x = 2, y = 0;

    // call function findTangent
    findTangent(A, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for find Tangent
// on a curve at given point
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// function for find Tangent
static void findTangent(int A, int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            System.out.println( "y = "
                 + dif + "x" + (x * dif + y));

        else if (dif > 0)

            // differentiate is positive
            System.out.println( "y = "
                 + dif + "x+" + -x * dif + y);

        // differentiate is zero
        else
            System.out.println("Not possible");
    }
}

// Driver code
public static void main(String args[])
{
    // declare variable
    int A = 2, x = 2, y = 0;

    // call function findTangent
    findTangent(A, x, y);

} 
}
```

## 蟒蛇 3

```
# Python3 program for find Tangent
# on a curve at given point

# function for find Tangent
def findTangent(A, x, y) :

    #  differentiate given equation
    dif = A - x * 2

    #  check that point on the curve or not
    if y == (2 * x - x * x) :

        # if differentiate is negative
        if dif < 0 :

            print("y =",dif,"x",(x * dif) + (y))

        # differentiate is positive
        elif dif > 0 :

            print("y =",dif,"x+",-x * dif + y)

        # differentiate is zero
        else :

            print("Not Possible")

   # Driver code    
if __name__ == "__main__" :

    # declare variable
    A, x, y = 2, 2, 0

    # call function findTangent
    findTangent(A, x, y)

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program for find Tangent
// on a curve at given point

using System;
class GFG
{

// function for find Tangent
static void findTangent(int A, int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            Console.Write( "y = "
                 + dif + "x" + (x * dif + y)+"\n");

        else if (dif > 0)

            // differentiate is positive
            Console.Write( "y = "
                 + dif + "x+" + -x * dif + y+"\n");

        // differentiate is zero
        else
            Console.Write("Not possible"+"\n");
    }
}

// Driver code
public static void Main()
{
    // declare variable
    int A = 2, x = 2, y = 0;

    // call function findTangent
    findTangent(A, x, y);

}  
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for find Tangent
// on a curve at given point

// function for find Tangent
function findTangent($A, $x, $y)
{
    // differentiate given equation
    $dif = $A - $x * 2;

    // check that point on the
    // curve or not
    if ($y == (2 * $x - $x * $x))
    {

        // if differentiate is negative
        if ($dif < 0)
            echo "y = ", $dif , "x" ,
                  ($x * $dif) + ($y);

        else if ($dif > 0)

            // differentiate is positive
            echo "y = ",
                $dif , "x+" , -$x * $dif + $y;

        // differentiate is zero
        else
            echo "Not possible";
    }
}

// Driver code

// declare variable
$A = 2;
$x = 2;
$y = 0;

// call function findTangent
findTangent($A, $x, $y);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// javascript program for find Tangent
// on a curve at given point

// function for find Tangent
function findTangent( A,  x,  y)
{
    // differentiate given equation
    var dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            document.write( "y = "
                 + dif + "x" + (x * dif + y)+"\n");

        else if (dif > 0)

            // differentiate is positive
            document.write( "y = "
                 + dif + "x+" + -x * dif + y+"\n");

        // differentiate is zero
        else
            document.write("Not possible"+"\n");
    }
}

// Driver code

    // declare variable
    var A = 2, x = 2, y = 0;

    // call function findTangent
    findTangent(A, x, y);

// This code is contributed by bunnyram19.
</script>
```

**输出:**

```
y = -2x-4
```