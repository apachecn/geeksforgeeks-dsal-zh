# 检查给定点是否位于三角形内

> 原文:[https://www . geesforgeks . org/check-给定点是否位于三角形内/](https://www.geeksforgeeks.org/check-whether-a-given-point-lies-inside-a-triangle-or-not/)

给定一个三角形的三个角点，还有一个点 P。编写一个函数来检查 P 是否位于三角形内。
例如，考虑下面的程序，对于 P(10，15)函数应该返回 true，对于 P’(30，15)函数应该返回 false

```
              B(10,30)
                / \
               /   \
              /     \
             /   P   \      P'
            /         \
     A(0,0) ----------- C(20,0) 
```

**解:**
设三个角的坐标为(x1，y1)、(x2，y2)和(x3，y3)。且给定点 P 的坐标为(x，y)
1)计算给定三角形的面积，即上图中三角形 ABC 的面积。面积 A =[x1(y2–y3)+x2(y3–y1)+x3(y1-y2)]/2
2)计算三角形 PAB 的面积。我们可以用同样的公式。让这个区域为 A1。
3)计算三角形 PBC 的面积。让这个区域为 A2。
4)计算三角形 PAC 的面积。让这个区域为 A3。
5)如果 P 位于三角形内部，那么 A1 + A2 + A3 必须等于 a。

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* A utility function to calculate area of triangle formed by (x1, y1),
   (x2, y2) and (x3, y3) */
float area(int x1, int y1, int x2, int y2, int x3, int y3)
{
   return abs((x1*(y2-y3) + x2*(y3-y1)+ x3*(y1-y2))/2.0);
}

/* A function to check whether point P(x, y) lies inside the triangle formed
   by A(x1, y1), B(x2, y2) and C(x3, y3) */
bool isInside(int x1, int y1, int x2, int y2, int x3, int y3, int x, int y)
{  
   /* Calculate area of triangle ABC */
   float A = area (x1, y1, x2, y2, x3, y3);

   /* Calculate area of triangle PBC */ 
   float A1 = area (x, y, x2, y2, x3, y3);

   /* Calculate area of triangle PAC */ 
   float A2 = area (x1, y1, x, y, x3, y3);

   /* Calculate area of triangle PAB */  
   float A3 = area (x1, y1, x2, y2, x, y);

   /* Check if sum of A1, A2 and A3 is same as A */
   return (A == A1 + A2 + A3);
}

/* Driver program to test above function */
int main()
{
   /* Let us check whether the point P(10, 15) lies inside the triangle
      formed by A(0, 0), B(20, 0) and C(10, 30) */
   if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
     cout <<"Inside";
   else
     cout <<"Not Inside";

   return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>
#include <math.h>
#include <stdbool.h>
#include <stdlib.h>
/* A utility function to calculate area of triangle formed by (x1, y1),
   (x2, y2) and (x3, y3) */
float area(int x1, int y1, int x2, int y2, int x3, int y3)
{
   return abs((x1*(y2-y3) + x2*(y3-y1)+ x3*(y1-y2))/2.0);
}

/* A function to check whether point P(x, y) lies inside the triangle formed
   by A(x1, y1), B(x2, y2) and C(x3, y3) */
bool isInside(int x1, int y1, int x2, int y2, int x3, int y3, int x, int y)
{  
   /* Calculate area of triangle ABC */
   float A = area (x1, y1, x2, y2, x3, y3);

   /* Calculate area of triangle PBC */ 
   float A1 = area (x, y, x2, y2, x3, y3);

   /* Calculate area of triangle PAC */ 
   float A2 = area (x1, y1, x, y, x3, y3);

   /* Calculate area of triangle PAB */  
   float A3 = area (x1, y1, x2, y2, x, y);

   /* Check if sum of A1, A2 and A3 is same as A */
   return (A == A1 + A2 + A3);
}

/* Driver program to test above function */
int main()
{
   /* Let us check whether the point P(10, 15) lies inside the triangle
      formed by A(0, 0), B(20, 0) and C(10, 30) */
   if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
     printf ("Inside");
   else
     printf ("Not Inside");

   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Check whether a given point
// lies inside a triangle or not
import java.util.*;

class GFG {

    /* A utility function to calculate area of triangle
       formed by (x1, y1) (x2, y2) and (x3, y3) */
    static double area(int x1, int y1, int x2, int y2,
                                        int x3, int y3)
    {
       return Math.abs((x1*(y2-y3) + x2*(y3-y1)+
                                    x3*(y1-y2))/2.0);
    }

    /* A function to check whether point P(x, y) lies
       inside the triangle formed by A(x1, y1),
       B(x2, y2) and C(x3, y3) */
    static boolean isInside(int x1, int y1, int x2,
                int y2, int x3, int y3, int x, int y)
    {  
       /* Calculate area of triangle ABC */
        double A = area (x1, y1, x2, y2, x3, y3);

       /* Calculate area of triangle PBC */ 
        double A1 = area (x, y, x2, y2, x3, y3);

       /* Calculate area of triangle PAC */ 
        double A2 = area (x1, y1, x, y, x3, y3);

       /* Calculate area of triangle PAB */  
        double A3 = area (x1, y1, x2, y2, x, y);

       /* Check if sum of A1, A2 and A3 is same as A */
        return (A == A1 + A2 + A3);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        /* Let us check whether the point P(10, 15)
           lies inside the triangle formed by
           A(0, 0), B(20, 0) and C(10, 30) */
       if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
           System.out.println("Inside");
       else
           System.out.println("Not Inside");

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
# A utility function to calculate area
# of triangle formed by (x1, y1),
# (x2, y2) and (x3, y3)

def area(x1, y1, x2, y2, x3, y3):

    return abs((x1 * (y2 - y3) + x2 * (y3 - y1)
                + x3 * (y1 - y2)) / 2.0)

# A function to check whether point P(x, y)
# lies inside the triangle formed by
# A(x1, y1), B(x2, y2) and C(x3, y3)
def isInside(x1, y1, x2, y2, x3, y3, x, y):

    # Calculate area of triangle ABC
    A = area (x1, y1, x2, y2, x3, y3)

    # Calculate area of triangle PBC
    A1 = area (x, y, x2, y2, x3, y3)

    # Calculate area of triangle PAC
    A2 = area (x1, y1, x, y, x3, y3)

    # Calculate area of triangle PAB
    A3 = area (x1, y1, x2, y2, x, y)

    # Check if sum of A1, A2 and A3
    # is same as A
    if(A == A1 + A2 + A3):
        return True
    else:
        return False

# Driver program to test above function
# Let us check whether the point P(10, 15)
# lies inside the triangle formed by
# A(0, 0), B(20, 0) and C(10, 30)
if (isInside(0, 0, 20, 0, 10, 30, 10, 15)):
    print('Inside')
else:
    print('Not Inside')

# This code is contributed by Danish Raza
```

## C#

```
// C# Code to Check whether a given point
// lies inside a triangle or not
using System;

class GFG {

    /* A utility function to calculate area of triangle
    formed by (x1, y1) (x2, y2) and (x3, y3) */
    static double area(int x1, int y1, int x2,
                       int y2, int x3, int y3)
    {
        return Math.Abs((x1 * (y2 - y3) +
                         x2 * (y3 - y1) +
                         x3 * (y1 - y2)) / 2.0);
    }

    /* A function to check whether point P(x, y) lies
    inside the triangle formed by A(x1, y1),
    B(x2, y2) and C(x3, y3) */
    static bool isInside(int x1, int y1, int x2,
                         int y2, int x3, int y3,
                         int x, int y)
    {
        /* Calculate area of triangle ABC */
        double A = area(x1, y1, x2, y2, x3, y3);

        /* Calculate area of triangle PBC */
        double A1 = area(x, y, x2, y2, x3, y3);

        /* Calculate area of triangle PAC */
        double A2 = area(x1, y1, x, y, x3, y3);

        /* Calculate area of triangle PAB */
        double A3 = area(x1, y1, x2, y2, x, y);

        /* Check if sum of A1, A2 and A3 is same as A */
        return (A == A1 + A2 + A3);
    }

/* Driver program to test above function */
public static void Main()
{
    /* Let us check whether the point P(10, 15)
    lies inside the triangle formed by
    A(0, 0), B(20, 0) and C(10, 30) */
    if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
        Console.WriteLine("Inside");
    else
        Console.WriteLine("Not Inside");
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

/* A utility function to calculate
  area of triangle formed by (x1, y1),
  (x2, y2) and (x3, y3) */
function area($x1, $y1, $x2,
              $y2, $x3, $y3)
{
    return abs(($x1 * ($y2 - $y3) +
                $x2 * ($y3 - $y1) + 
                $x3 * ($y1 - $y2)) / 2.0);
}

/* A function to check whether
   P(x, y) lies inside the
   triangle formed by A(x1, y1),
   B(x2, y2) and C(x3, y3) */
function isInside($x1, $y1, $x2, $y2,
                  $x3, $y3, $x, $y)
{

    /* Calculate area of triangle ABC */
    $A = area ($x1, $y1, $x2, $y2, $x3, $y3);

    /* Calculate area of triangle PBC */
    $A1 = area ($x, $y, $x2, $y2, $x3, $y3);

    /* Calculate area of triangle PAC */
    $A2 = area ($x1, $y1, $x, $y, $x3, $y3);

    /* Calculate area of triangle PAB */
    $A3 = area ($x1, $y1, $x2, $y2, $x, $y);

    /* Check if sum of A1, A2
    and A3 is same as A */
    return ($A == $A1 + $A2 + $A3);
}

    // Driver Code
    /* Let us check whether the
       P(10, 15) lies inside the
       triangle formed by A(0, 0),
       B(20, 0) and C(10, 30) */
    if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
        echo "Inside";
    else
        echo "Not Inside";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

/* A utility function to calculate area of triangle formed by (x1, y1),
(x2, y2) and (x3, y3) */
function area(x1, y1, x2, y2, x3, y3)
{
return Math.abs((x1*(y2-y3) + x2*(y3-y1)+ x3*(y1-y2))/2.0);
}

/* A function to check whether point P(x, y) lies inside the triangle formed
by A(x1, y1), B(x2, y2) and C(x3, y3) */
function isInside(x1, y1, x2, y2, x3, y3, x, y)
{
/* Calculate area of triangle ABC */
let A = area (x1, y1, x2, y2, x3, y3);

/* Calculate area of triangle PBC */
let A1 = area (x, y, x2, y2, x3, y3);

/* Calculate area of triangle PAC */
let A2 = area (x1, y1, x, y, x3, y3);

/* Calculate area of triangle PAB */   
let A3 = area (x1, y1, x2, y2, x, y);

/* Check if sum of A1, A2 and A3 is same as A */
return (A == A1 + A2 + A3);
}

/* Driver program to test above function */

/* Let us check whether the point P(10, 15) lies inside the triangle
    formed by A(0, 0), B(20, 0) and C(10, 30) */
if (isInside(0, 0, 20, 0, 10, 30, 10, 15))
    document.write("Inside");
else
    document.write("Not Inside");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
 Inside 
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

https://www.youtube.com/watch?v=H9qu9Xptf

-w
**练习:**给定一个矩形的四个角的坐标，和一个点 P，写一个函数检查 P 是否位于给定的矩形内。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。