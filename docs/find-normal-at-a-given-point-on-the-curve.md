# 在曲线上给定点找到法线

> 原文:[https://www . geeksforgeeks . org/find-曲线上给定点的法线/](https://www.geeksforgeeks.org/find-normal-at-a-given-point-on-the-curve/)

给定一条曲线**[y = x(A–x)]**，任务是在该曲线上给定点(x，y)寻找法线，其中 A 是整数，x，y 也是任意整数。

**示例:**

```
Input: A = 2, x = 2, y = 0
Output: 2y = x - 2
Since y = x(2 - x)
      y = 2x - x^2 differentiate it with respect to x
      dy/dx = 2 - 2x  put x = 2, y = 0 in this equation
      dy/dx = 2 - 2* 2 = -2
      equation  => (Y - 0 ) = ((-1/-2))*( Y - 2)
                => 2y = x -2

Input: A = 3, x = 4, y = 5
Output: Not possible
Point is not on that curve 
```

**方法:**首先我们需要找到给定点是否在那条曲线上，如果点在那条曲线上，那么:

1.  我们需要微分这个方程，如果你分析，你会发现 dy/dx 总是变成 A–2x。
2.  在 dy/dx 中输入 x，y。
3.  正规方程为 Y–Y =-(1/(dy/dx))*(X–X)。

以下是上述方法的实现:

## C++

```
// C++ program for find curve
// at given point
#include <bits/stdc++.h>
using namespace std;

// function for find normal
void findNormal(int A, int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            cout << 0 - dif << "y = "
                 << "x" << (0 - x) + (y * dif);

        else if (dif > 0)

            // differentiate is positive
            cout << dif << "y = "
                 << "-x+" << x + dif * y;

        // differentiate  is zero
        else
            cout << "x = " << x;
    }

    // other wise normal not found
    else
        cout << "Not possible";
}

// Driver code
int main()
{
    // declare variable
    int A = 2, x = 2, y = 0;

    // call function findNormal
    findNormal(A, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for find curve
// at given point

import java.io.*;

class GFG {

// function for find normal
static void findNormal(int A, int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on the curve or not
    if (y == (2 * x - x * x)) {

        // if differentiate is negative
        if (dif < 0)
            System.out.print( (0 - dif) + "y = "
                + "x" +((0 - x) + (y * dif)));

        else if (dif > 0)

            // differentiate is positive
            System.out.print( dif + "y = "
                + "-x+" + (x + dif * y));

        // differentiate is zero
        else
            System.out.print( "x = " +x);
    }

    // other wise normal not found
    else
        System.out.println( "Not possible");
}

       // Driver code
    public static void main (String[] args) {
        // declare variable
    int A = 2, x = 2, y = 0;

    // call function findNormal
    findNormal(A, x, y);;
    }
}
// This Code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 program for find curve
# at given point

# function for find normal
def findNormal(A, x, y):

    # differentiate given equation
    dif = A - x * 2

    # check that point on the curve or not
    if (y == (2 * x - x * x)):

        # if differentiate is negative
        if (dif < 0):
            print(0 - dif, "y =", "x",
                 (0 - x) + (y * dif))

        elif (dif > 0):

            # differentiate is positive
            print(dif, "y =", "- x +",
                        x + dif * y)

        # differentiate is zero
        else:
            print("x =", x)

    # other wise normal not found
    else:
        print("Not possible")

# Driver code
if __name__ == '__main__':

    # declare variable
    A = 2
    x = 2
    y = 0

    # call function findNormal
    findNormal(A, x, y)

# This code is contributed By
# Surendra_Gangwar
```

## C#

```
// C# program for find curve
// at given point
using System;

class GFG
{

// function for find normal
static void findNormal(int A,
                       int x, int y)
{
    // differentiate given equation
    int dif = A - x * 2;

    // check that point on
    // the curve or not
    if (y == (2 * x - x * x))
    {

        // if differentiate is negative
        if (dif < 0)
            Console.Write((0 - dif) + "y = " +
                   "x" + ((0 - x) + (y * dif)));

        else if (dif > 0)

            // differentiate is positive
            Console.Write(dif + "y = " +
                          "-x + " + (x + dif * y));

        // differentiate is zero
        else
            Console.Write("x = " + x);
    }

    // other wise normal not found
    else
        Console.WriteLine("Not possible");
}

// Driver code
static public void Main ()
{
    // declare variable
    int A = 2, x = 2, y = 0;

    // call function findNormal
    findNormal(A, x, y);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for find curve
// at given point

// function for find normal
function findNormal($A, $x, $y)
{
    // differentiate given equation
    $dif = $A - $x * 2;

    // check that point on the
    // curve or not
    if ($y == (2 * $x - $x * $x))
    {

        // if differentiate is negative
        if ($dif < 0)
            echo (0 - $dif), "y = ",
                 "x" , (0 - $x) + ($y * $dif);

        else if ($dif > 0)

            // differentiate is positive
            echo $dif , "y = ",
                 "-x+" ,( $x + $dif * $y);

        // differentiate is zero
        else
            echo "x = " , $x;
    }

    // other wise normal not found
    else
        echo "Not possible";
}

// Driver code

// declare variable
$A = 2;
$x = 2;
$y = 0;

// call function findNormal
findNormal($A, $x, $y);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program for find curve at given point

    // function for find normal
    function findNormal(A, x, y)
    {
        // differentiate given equation
        let dif = A - x * 2;

        // check that point on
        // the curve or not
        if (y == (2 * x - x * x))
        {

            // if differentiate is negative
            if (dif < 0)
                document.write((0 - dif) + "y = " +
                       "x" + ((0 - x) + (y * dif)));

            else if (dif > 0)

                // differentiate is positive
                document.write(dif + "y = " +
                              "-x + " + (x + dif * y));

            // differentiate is zero
            else
                document.write("x = " + x);
        }

        // other wise normal not found
        else
            document.write("Not possible");
    }

    // declare variable
    let A = 2, x = 2, y = 0;

    // call function findNormal
    findNormal(A, x, y);

</script>
```

**Output:** 

```
2y = x-2
```