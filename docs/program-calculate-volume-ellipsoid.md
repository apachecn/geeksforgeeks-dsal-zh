# 椭球体积计算程序

> 原文:[https://www . geesforgeks . org/program-calculate-volume-椭球/](https://www.geeksforgeeks.org/program-calculate-volume-ellipsoid/)

**椭球**，其封闭面的所有平面截面要么是椭圆要么是圆。椭球体关于三个在中心相交的互相垂直的轴是对称的。它是一个三维的、封闭的几何形状，所有平面部分都是椭圆或圆。
椭球体有三个独立的轴，通常由三个半轴的长度 a、b、c 指定。如果一个椭圆体是由一个椭圆围绕它的一个轴旋转而成的，那么这个椭圆体的两个轴是相同的，它被称为旋转椭圆体。如果它的三个轴的长度都相同，它就是一个球体。

```
Standard equation of Ellipsoid :
x<sup>2 / a2 + y2 / b2 + z2 / c2 = 1</sup>

<sup>where a, b, c are positive real numbers.</sup>
Volume of Ellipsoid :  (4/3) * pi * r1 * r2 * r3 
```

以下是计算椭球体体积的代码:

## C++

```
// CPP program to find the
// volume of Ellipsoid.
#include <bits/stdc++.h>
using namespace std;

// Function to find the volume
float volumeOfEllipsoid(float r1,
                        float r2,
                        float r3)
{
    float pi = 3.14;
    return 1.33 * pi * r1 *
                  r2 * r3;
}

// Driver Code
int main()
{
    float r1 = 2.3, r2 = 3.4, r3 = 5.7;
    cout << "volume of ellipsoid is : "
         << volumeOfEllipsoid(r1, r2, r3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// volume of Ellipsoid.
import java.util.*;
import java.lang.*;

class GfG
{

    // Function to find the volume
    public static float volumeOfEllipsoid(float r1,
                                          float r2,
                                          float r3)
    {
        float pi = (float)3.14;
        return (float) 1.33 * pi * r1 * r2 * r3;
    }

    // Driver Code
    public static void main(String args[])
    {
        float r1 = (float) 2.3,
              r2 = (float) 3.4,
              r3 = (float) 5.7;
        System.out.println("volume of ellipsoid is : "
                    + volumeOfEllipsoid(r1, r2, r3));
    }
}

// This code is contributed by Sagar Shukla
```

## 计算机编程语言

```
''' Python3 program to Volume of ellipsoid'''
import math

# Function To calculate Volume
def volumeOfEllipsoid(r1, r2, r3):
    return 1.33 * math.pi * r1 * r2 * r3

# Driver Code
r1 = float(2.3)
r2 = float(3.4)
r3 = float(5.7)
print( "Volume of ellipsoid is : ",
        volumeOfEllipsoid(r1, r2, r3) )
```

## C#

```
// C# program to find the
// volume of Ellipsoid.
using System;

class GfG
{

    // Function to find the volume
    public static float volumeOfEllipsoid(float r1,
                                            float r2,
                                            float r3)
    {
        float pi = (float)3.14;
        return (float) 1.33 * pi * r1 * r2 * r3;
    }

    // Driver Code
    public static void Main()
    {
        float r1 = (float)2.3,
            r2 =(float) 3.4,
            r3 = (float)5.7;
        Console.WriteLine("volume of ellipsoid is : " +
                        volumeOfEllipsoid(r1, r2, r3));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// volume of Ellipsoid.

// Function to find the volume
function volumeOfEllipsoid( $r1,
                            $r2,
                            $r3)
{
    $pi = 3.14;
    return 1.33 * $pi * $r1 *
                  $r2 * $r3;
}

// Driver Code

    $r1 = 2.3; $r2 = 3.4;
    $r3 = 5.7;
    echo ( "volume of ellipsoid is : ");
    echo( volumeOfEllipsoid($r1, $r2, $r3));

// This code is contributed by vt_m .
?>
```

## java 描述语言

```
<script>
// javascript program to find the
// volume of Ellipsoid.

// Function to find the volume
function volumeOfEllipsoid( r1, r2, r3)
{
    let pi = 3.14;
    return 1.33 * pi * r1 *
                  r2 * r3;
}

// Driver Code
   let r1 = 2.3, r2 = 3.4, r3 = 5.7;
    document.write( "volume of ellipsoid is : "
         + volumeOfEllipsoid(r1, r2, r3).toFixed(2));

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
Volume of ellipsoid is : 186.15
```