# 检查一个点是否位于球体内部

> 原文:[https://www . geesforgeks . org/check-a-point-lie-in-a-sphere-or-not/](https://www.geeksforgeeks.org/check-whether-a-point-lies-inside-a-sphere-or-not/)

给定球体中心 **(cx，cy，cz)** 及其半径 **r** 的坐标。我们的任务是检查一个点 **(x，y，z)** 是在这个球体的内部，外部还是上面。
**举例:**

```
Input : Centre(0, 0, 0) Radius 3
        Point(1, 1, 1)
Output :Point is inside the sphere

Input :Centre(0, 0, 0) Radius 3
       Point(2, 1, 2)
Output :Point lies on the sphere

Input :Centre(0, 0, 0) Radius 3
       Point(10, 10, 10)
Output :Point is outside the sphere
```

**方法:**
一个点是否位于球体内部，取决于它与中心的距离。
一个点(x，y，z)在球体内部，中心(cx，cy，cz)和半径为 r，如果

```
( x-cx ) ^2 + (y-cy) ^2 + (z-cz) ^ 2 < r^2 
```

如果
，一个点(x，y，z)位于具有中心(cx，cy，cz)和半径 r 的球体上

```
( x-cx ) ^2 + (y-cy) ^2 + (z-cz) ^ 2 = r^2 
```

如果
，一个点(x，y，z)在具有中心(cx，cy，cz)和半径 r 的球体之外

```
( x-cx ) ^2 + (y-cy) ^2 + (z-cz) ^ 2 > r^2 
```

## C++

```
// CPP code to illustrate above approach
#include <bits/stdc++.h>
using namespace std;
// function to calculate the distance between centre and the point
int check(int cx, int cy, int cz, int x, int y, int z)
{
    int x1 = pow((x - cx), 2);
    int y1 = pow((y - cy), 2);
    int z1 = pow((z - cz), 2);

    // distance between the centre
    // and given point
    return (x1 + y1 + z1);
}

// Driver program to test above function
int main()
{
    // coordinates of centre
    int cx = 1, cy = 2, cz = 3;

    int r = 5; // radius of the sphere
    int x = 4, y = 5, z = 2; // coordinates of point

    int ans = check(cx, cy, cz, x, y, z);

    // distance btw centre and point is less
    // than radius
    if (ans < (r * r))
        cout << "Point is inside the sphere";

    // distance btw centre and point is
    // equal to radius
    else if (ans == (r * r))
        cout << "Point lies on the sphere";

    // distance btw center and point is
    // greater than radius
    else
        cout << "Point is outside the sphere";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to illustrate above approach
import java.io.*;
import java.util.*;
import java.lang.*;

class GfG {

    // function to calculate the distance
    // between centre and the point
    public static int check(int cx, int cy,
                 int cz, int x, int y, int z)
    {
        int x1 = (int)Math.pow((x - cx), 2);
        int y1 = (int)Math.pow((y - cy), 2);
        int z1 = (int)Math.pow((z - cz), 2);

        // distance between the centre
        // and given point
        return (x1 + y1 + z1);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        // coordinates of centre
        int cx = 1, cy = 2, cz = 3;

        int r = 5; // radius of the sphere

        // coordinates of point
        int x = 4, y = 5, z = 2;

        int ans = check(cx, cy, cz, x, y, z);

        // distance btw centre and point is less
        // than radius
        if (ans < (r * r))
            System.out.println("Point is inside"
                       + " the sphere");

        // distance btw centre and point is
        // equal to radius
        else if (ans == (r * r))
            System.out.println("Point lies on"
                        + " the sphere");

        // distance btw center and point is
        // greater than radius
        else
            System.out.println("Point is outside"
                             + " the sphere");
    }
}

// This code is contributed by Sagar Shukla.
```

## 计算机编程语言

```
# Python3 code to illustrate above approach

import math
# function to calculate distance btw center and given point
def check(cx, cy, cz, x, y, z, ):

    x1 = math.pow((x-cx), 2)
    y1 = math.pow((y-cy), 2)
    z1 = math.pow((z-cz), 2)
    return (x1 + y1 + z1) # distance between the centre and given point

# driver code   
cx = 1
cy = 2 # coordinates of centre
cz = 3

r = 5 # radius of sphere

x = 4
y = 5 # coordinates of the given point
z = 2
# function call to calculate distance btw centre and given point
ans = check(cx, cy, cz, x, y, z);

# distance btw centre and point is less than radius
if ans<(r**2):
    print("Point is inside the sphere")

# distance btw centre and point is equal to radius
elif ans ==(r**2):
    print("Point lies on the sphere")

# distance btw centre and point is greater than radius
else:
    print("Point is outside the sphere")
```

## C#

```
// C# code to illustrate
// above approach
using System;

class GFG
{

    // function to calculate
    // the distance between
    // centre and the point
    public static int check(int cx, int cy,
                            int cz, int x,
                            int y, int z)
    {
        int x1 = (int)Math.Pow((x - cx), 2);
        int y1 = (int)Math.Pow((y - cy), 2);
        int z1 = (int)Math.Pow((z - cz), 2);

        // distance between the
        // centre and given point
        return (x1 + y1 + z1);
    }

    // Driver Code
    public static void Main()
    {
        // coordinates of centre
        int cx = 1, cy = 2, cz = 3;

        int r = 5; // radius of the sphere

        // coordinates of point
        int x = 4, y = 5, z = 2;

        int ans = check(cx, cy, cz,
                        x, y, z);

        // distance btw centre
        // and point is less
        // than radius
        if (ans < (r * r))
            Console.WriteLine("Point is inside" +
                                  " the sphere");

        // distance btw centre
        // and point is
        // equal to radius
        else if (ans == (r * r))
            Console.WriteLine("Point lies on" +
                                " the sphere");

        // distance btw center
        // and point is greater
        // than radius
        else
            Console.WriteLine("Point is outside" +
                                   " the sphere");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// function to calculate 
// the distance between
// centre and the point
function check($cx, $cy, $cz,
               $x, $y, $z)
{
    $x1 = pow(($x - $cx), 2);
    $y1 = pow(($y - $cy), 2);
    $z1 = pow(($z - $cz), 2);

    // distance between the
    // centre and given point
    return ($x1 + $y1 + $z1);
}

// Driver Code

// coordinates of centre
$cx = 1;
$cy = 2;
$cz = 3;

$r = 5; // radius of the sphere
$x = 4;
$y = 5;
$z = 2; // coordinates of point

$ans = check($cx, $cy, $cz,
             $x, $y, $z);

// distance btw centre and
// point is less than radius
if ($ans < ($r * $r))
    echo "Point is inside " .  
                "the sphere";

// distance btw centre and
// point is equal to radius
else if ($ans == ($r * $r))
    echo "Point lies on the sphere";

// distance btw center and point
// is greater than radius
else
    echo "Point is outside " .
                 "the sphere";

// This code is contributed
// by shiv_bhakt
?>
```

## java 描述语言

```
<script>

// Javascript code to illustrate above approach

// function to calculate the distance between centre and the point
function check(cx, cy, cz, x, y, z)
{
    let x1 = Math.pow((x - cx), 2);
    let y1 = Math.pow((y - cy), 2);
    let z1 = Math.pow((z - cz), 2);

    // distance between the centre
    // and given point
    return (x1 + y1 + z1);
}

// Driver program to test above function

    // coordinates of centre
    let cx = 1, cy = 2, cz = 3;

    let r = 5; // radius of the sphere
    let x = 4, y = 5, z = 2; // coordinates of point

    let ans = check(cx, cy, cz, x, y, z);

    // distance btw centre and point is less
    // than radius
    if (ans < (r * r))
        document.write("Point is inside the sphere");

    // distance btw centre and point is
    // equal to radius
    else if (ans == (r * r))
        document.write("Point lies on the sphere");

    // distance btw center and point is
    // greater than radius
    else
        document.write("Point is outside the sphere");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Point is inside the sphere
```

**时间复杂度:** O(1)