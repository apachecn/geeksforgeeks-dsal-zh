# 检查三点是否共线的程序

> 原文:[https://www . geesforgeks . org/program-check-三点-共线/](https://www.geeksforgeeks.org/program-check-three-points-collinear/)

给定三个点，检查它们是否位于直线上
**例:**

```
Input : (1, 1), (1, 4), (1, 5)
Output : Yes 
The points lie on a straight line

Input : (1, 5), (2, 5), (4, 6)
Output : No 
The points do not lie on a straight line
```

**首先逼近**
如果这三个点的三角形面积为零，则这三个点位于直线上。所以我们会检查三角形形成的面积是否为零

```
Formula for area of triangle is : 
0.5 * [x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)]

The formula is basically half of determinant
value of following.
x1 x2 x3
y1 y2 y3
1   1  1

The above formula is derived from shoelace formula.

If this equals zero then points lie on a straight line 
```

## C++

```
// C++ program to check if three
// points are collinear or not
// using area of triangle.
#include <bits/stdc++.h>
#include <math.h>
#include <stdlib.h>

using namespace std;
// function to check if point
// collinear or not
void collinear(int x1, int y1, int x2,
               int y2, int x3, int y3)
{
    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    int a = x1 * (y2 - y3) +
            x2 * (y3 - y1) +
            x3 * (y1 - y2);

    if (a == 0)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int x1 = 1, x2 = 1, x3 = 1,
        y1 = 1, y2 = 4, y3 = 5;
    collinear(x1, y1, x2, y2, x3, y3);
    return 0;
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## C

```
// C program to check if three
// points are collinear or not
// using area of triangle.
#include <stdio.h>
#include <math.h>
#include <stdlib.h>

// function to check if point
// collinear or not
void collinear(int x1, int y1, int x2,
               int y2, int x3, int y3)
{
    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    int a = x1 * (y2 - y3) +
            x2 * (y3 - y1) +
            x3 * (y1 - y2);

    if (a == 0)
        printf("Yes");
    else
        printf("No");
}

// Driver Code
int main()
{
    int x1 = 1, x2 = 1, x3 = 1,
        y1 = 1, y2 = 4, y3 = 5;
    collinear(x1, y1, x2, y2, x3, y3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// three points are collinear
// or not using area of triangle.
class GFG
{

    // function to check if
    // point collinear or not
    static void collinear(int x1, int y1, int x2,
                          int y2, int x3, int y3)
    {

        /* Calculation the area of
        triangle. We have skipped
        multiplication with 0.5
        to avoid floating point
        computations */
        int a = x1 * (y2 - y3) +
                x2 * (y3 - y1) +
                x3 * (y1 - y2);

        if (a == 0)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        int x1 = 1, x2 = 1, x3 = 1,
            y1 = 1, y2 = 4, y3 = 5;

        collinear(x1, y1, x2, y2, x3, y3);

    }
}

// This code is contributed by Sam007.
```

## 计算机编程语言

```
# Python program to check
# if three points are collinear
# or not using area of triangle.

# function to check if
# point collinear or not
def collinear(x1, y1, x2, y2, x3, y3):

    """ Calculation the area of 
        triangle. We have skipped
        multiplication with 0.5 to
        avoid floating point computations """
    a = x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)

    if (a == 0):
        print "Yes"
    else:
        print "No"

# Driver Code
x1, x2, x3, y1, y2, y3 = 1, 1, 1, 1, 4, 5
collinear(x1, y1, x2, y2, x3, y3)

# This code is contributed
# by Sachin Bisht
```

## C#

```
// C# program to check if
// three points are collinear
// or not using area of triangle.
using System;

class GFG
{

    /* function to check if
    point collinear or not */
    static void collinear(int x1, int y1, int x2,
                          int y2, int x3, int y3)
    {

        /* Calculation the area of 
        triangle. We have skipped
        multiplication with 0.5 to
        avoid floating point computations */
        int a = x1 * (y2 - y3) +
                x2 * (y3 - y1) +
                x3 * (y1 - y2);

        if (a == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }

    // Driver code
    public static void Main ()
    {
        int x1 = 1, x2 = 1, x3 = 1,
            y1 = 1, y2 = 4, y3 = 5;

        collinear(x1, y1, x2, y2, x3, y3);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP or not using area of triangle.

/* function to check if
point collinear or not */
function collinear($x1, $y1, $x2,
                   $y2, $x3, $y3)
{
    /* Calculation the area of
    triangle. We have skipped
    multiplication with 0.5 to
    avoid floating point computations */
    $a = $x1 * ($y2 - $y3) +
         $x2 * ($y3 - $y1) +
         $x3 * ($y1 - $y2);

    if ($a == 0)
        printf("Yes");
    else
        printf("No");
}

// Driver Code
$x1 = 1; $x2 = 1; $x3 = 1;
$y1 = 1; $y2 = 4; $y3 = 5;
collinear($x1, $y1, $x2, $y2, $x3, $y3);

// This code is contributed by Sam007.
?>
```

## java 描述语言

```
<script>
// Javascript program to check if three
// points are collinear or not
// using area of triangle.

function collinear(x1,  y1,  x2, y2,  x3,  y3)
{

    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    var a = x1 * (y2 - y3) +
            x2 * (y3 - y1) +
            x3 * (y1 - y2);

    if (a == 0)
        document.write("Yes");
    else
        document.write( "No");
}

var x1 = 1, x2 = 1, x3 = 1,y1 = 1, y2 = 4, y3 = 5;
    collinear(x1, y1, x2, y2, x3, y3);

// This code is contributed by akshitsaxenaa09.
</script>
```

**输出:**

```
Yes
```

**第二次进场**

```
For three points, slope of any pair of points
must be same as other pair.

For example, slope of line joining (x2, y2)
and (x3, y3), and line joining (x1, y1) and
(x2, y2) must be same.

(y3 - y2)/(x3 - x2) = (y2 - y1)/(x2 - x1)

In other words, 
(y3 - y2)(x2 - x1) = (y2 - y1)(x3 - x2) 
```

## C

```
// Slope based solution to check
// if three points are collinear.
#include <stdio.h>
#include <math.h>

/* function to check if
point collinear or not*/
void collinear(int x1, int y1, int x2,
               int y2, int x3, int y3)
{
    if ((y3 - y2) * (x2 - x1) ==
        (y2 - y1) * (x3 - x2))
        printf("Yes");
    else
        printf("No");
}

// Driver Code
int main()
{
    int x1 = 1, x2 = 1, x3 = 0,
        y1 = 1, y2 = 6, y3 = 9;
    collinear(x1, y1, x2, y2, x3, y3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Slope based solution to check
// if three points are collinear.

import java.io.*;

class GFG {

/* function to check if
point collinear or not*/
static void cool_line(int x1, int y1, int x2,
            int y2, int x3, int y3)
{
    if ((y3 - y2) * (x2 - x1) ==
        (y2 - y1) * (x3 - x2))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code

    public static void main (String[] args) {
        int a1 = 1, a2 = 1, a3 = 0,
        b1 = 1, b2 = 6, b3 = 9;
       cool_line(a1, b1, a2, b2, a3, b3);

    }
}
//This Code is Contributed by ajit
```

## 计算机编程语言

```
# Slope based solution to check if three
# points are collinear.

# function to check if
# point collinear or not
def collinear(x1, y1, x2, y2, x3, y3):

    if ((y3 - y2)*(x2 - x1) == (y2 - y1)*(x3 - x2)):
        print ("Yes")
    else:
        print ("No")

# Driver Code
x1, x2, x3, y1, y2, y3 = 1, 1, 0, 1, 6, 9
collinear(x1, y1, x2, y2, x3, y3);

# This code is contributed
# by Sachin Bisht
```

## C#

```
// Slope based solution to check
// if three points are collinear.
using System;

class GFG
{

/* function to check if
point collinear or not*/
static void cool_line(int x1, int y1, int x2,
                      int y2, int x3, int y3)
{
    if ((y3 - y2) * (x2 - x1) ==
        (y2 - y1) * (x3 - x2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
static public void Main ()
{
    int a1 = 1, a2 = 1, a3 = 0,
    b1 = 1, b2 = 6, b3 = 9;
    cool_line(a1, b1, a2, b2, a3, b3);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Slope based solution to check
// if three points are collinear.

/* function to check if
point collinear or not*/
function collinear($x1, $y1, $x2,
                   $y2, $x3, $y3)
{
    if (($y3 - $y2) * ($x2 - $x1) ==
        ($y2 - $y1) * ($x3 - $x2))
        echo ("Yes");
    else
        echo ("No");
}

// Driver Code
$x1 = 1;
$x2 = 1;
$x3 = 0;
$y1 = 1;
$y2 = 6;
$y3 = 9;
collinear($x1, $y1, $x2,
          $y2, $x3, $y3);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Slope based solution to check
// if three points are collinear.
/*
     * function to check if point collinear or not
     */
    function cool_line(x1 , y1 , x2 , y2 , x3 , y3)
    {
        if ((y3 - y2) * (x2 - x1) == (y2 - y1) * (x3 - x2))
            document.write("Yes");
        else
            document.write("No");
    }

    // Driver Code
        var a1 = 1, a2 = 1, a3 = 0, b1 = 1, b2 = 6, b3 = 9;
        cool_line(a1, b1, a2, b2, a3, b3);

// This code is contributed by aashish1995
</script>
```

**输出:**

```
No 
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。