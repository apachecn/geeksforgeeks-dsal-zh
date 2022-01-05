# 金字塔体积程序

> 原文:[https://www . geesforgeks . org/program-for-volume-of-pyramid/](https://www.geeksforgeeks.org/program-for-volume-of-pyramid/)

金字塔是一种三维几何形状，由多边形的所有角连接到中心顶点而形成。
金字塔有很多种类型。大多数情况下，它们是以它们拥有的碱基类型命名的。让我们看看下面一些常见类型的金字塔。

> 正方形金字塔的体积[金字塔的底部是正方形] = (1/3) * (b^2) * h
> 三角形金字塔的体积[金字塔的底部是三角形] = (1/6) * a * b * h
> 五边形金字塔的体积[金字塔的底部是五边形] = (5/6) * a * b * h
> 六边形金字塔的体积[金字塔的底部是六边形] = a * b * h

下面是计算金字塔体积的代码:

## C++

```
// CPP program to find the volume.
#include <bits/stdc++.h>
using namespace std;

// Function to find the volume
// of triangular pyramid
float volumeTriangular(int a,
                       int b,
                       int h)
{
    float vol = (0.1666) * a *
                       b * h;
    return vol;
}

// Function to find the
// volume of square pyramid
float volumeSquare(int b, int h)
{
    float vol = (0.33) * b *
                     b * h;
    return vol;
}

// Function to find the volume
// of pentagonal pyramid
float volumePentagonal(int a,
                       int b,
                       int h)
{
    float vol = (0.83) * a * b * h;
    return vol;
}

// Function to find the volume
// of hexagonal pyramid
float volumeHexagonal(int a,
                      int b,
                      int h)
{
    float vol = a * b * h;
    return vol;
}

// Driver Code
int main()
{
    int b = 4, h = 9, a = 4;
    cout << "Volume of triangular"
         << " base pyramid is "
         << volumeTriangular(a, b, h)
         << endl;

    cout << "Volume of square "
         << " base pyramid is "
         << volumeSquare(b, h)
         << endl;

    cout << "Volume of pentagonal"
         << " base pyramid is "
         << volumePentagonal(a, b, h)
         << endl;

    cout << "Volume of Hexagonal"
         << " base pyramid is "
         << volumeHexagonal(a, b, h);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for volume
// of Pyramid.
import java.util.*;
import java.lang.*;

class GfG
{

    // Function to find the volume of
    // triangular pyramid
    public static float volumeTriangular(int a,
                                         int b,
                                         int h)
    {
        float vol = (float)(0.1666) * a * b * h;
        return vol;
    }

    // Function to find the volume
    // of square pyramid
    public static float volumeSquare(int b,
                                     int h)
    {
        float vol = (float)(0.33) * b * b * h;
        return vol;
    }

    // Function to find the volume of
    // pentagonal pyramid
    public static float volumePentagonal(int a,
                                         int b,
                                         int h)
    {
        float vol = (float)(0.83) * a * b * h;
        return vol;
    }

    // Function to find the volume of hexagonal
    // pyramid
    public static float volumeHexagonal(int a,
                                        int b,
                                        int h)
    {
        float vol = (float)a * b * h;
        return vol;
    }

    // Driver Code
    public static void main(String argc[])
    {
        int b = 4, h = 9, a = 4;
        System.out.println("Volume of triangular"+
                             " base pyramid is " +
                       volumeTriangular(a, b, h));

        System.out.println("Volume of square base" +
                                    " pyramid is " +
                                volumeSquare(b, h));

        System.out.println("Volume of pentagonal"+
                             " base pyramid is " +
                       volumePentagonal(a, b, h));

        System.out.println("Volume of Hexagonal"+
                              " base pyramid is " +
                         volumeHexagonal(a, b, h));
    }
}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Python3 program to Volume of Pyramid

# Function to calculate
# Volume of Triangular Pyramid
def volumeTriangular(a, b, h):
    return (0.1666) * a * b * h

# Function To calculate
# Volume of Square Pyramid
def volumeSquare(b, h):
    return (0.33) * b * b * h

# Function To calculate Volume
# of Pentagonal Pyramid
def volumePentagonal(a, b, h):
    return (0.83) * a * b * h

# Function To calculate Volume
# of Hexagonal Pyramid
def volumeHexagonal(a, b, h):
    return a * b * h

# Driver Code
b = float(4)
h = float(9)
a = float(4)
print( "Volume of triangular base pyramid is ",
                    volumeTriangular(a, b, h) )
print( "Volume of square base pyramid is ",
                    volumeSquare(b, h) )
print( "Volume of pentagonal base pyramid is ",
                    volumePentagonal(a,b, h) )
print( "Volume of Hexagonal base pyramid is ",
                    volumeHexagonal(a, b, h))

# This code is contributed by rishabh_jain
```

## C#

```
// C# Program for volume of Pyramid.
using System;

class GFG
{

    // Function to find the volume of
    // triangular pyramid
    public static float volumeTriangular(int a,
                                         int b,
                                         int h)
    {
        float vol = (float)(0.1666) * a * b * h;
        return vol;
    }

    // Function to find the volume
    // of square pyramid
    public static float volumeSquare(int b,
                                     int h)
    {
        float vol = (float)(0.33) * b * b * h;
        return vol;
    }

    // Function to find the volume 
    // of pentagonal pyramid
    public static float volumePentagonal(int a,
                                         int b,
                                         int h)
    {
        float vol = (float)(0.83) * a * b * h;
        return vol;
    }

    // Function to find the volume
    // of hexagonal pyramid
    public static float volumeHexagonal(int a,
                                        int b,
                                        int h)
    {
        float vol = (float)a * b * h;
        return vol;
    }

    // Driver Code
    public static void Main()
    {
        int b = 4, h = 9, a = 4;
        Console.WriteLine("Volume of triangular"+
                            " base pyramid is " +
                      volumeTriangular(a, b, h));

        Console.WriteLine("Volume of square "+
                          "base pyramid is " +
                          volumeSquare(b, h));

        Console.WriteLine("Volume of pentagonal"+
                            " base pyramid is " +
                      volumePentagonal(a, b, h));

        Console.WriteLine("Volume of Hexagonal"+
                           " base pyramid is " +
                      volumeHexagonal(a, b, h));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the volume.

// Function to find the volume
// of triangular pyramid
function volumeTriangular($a, $b, $h)
{
    $vol = (0.1666) * $a * $b * $h;
    return $vol;
}

// Function to find the
// volume of square pyramid
function volumeSquare($b, $h)
{
    $vol = (0.33) * $b * $b * $h;
    return $vol;
}

// Function to find the volume
// of pentagonal pyramid
function volumePentagonal($a, $b, $h)
{
    $vol = (0.83) * $a * $b * $h;
    return $vol;
}

// Function to find the volume
// of hexagonal pyramid
function volumeHexagonal($a, $b, $h)
{
    $vol = $a * $b * $h;
    return $vol;
}

// Driver Code
$b = 4; $h = 9; $a = 4;
echo ("Volume of triangular base pyramid is ");
echo( volumeTriangular($a, $b, $h));
echo("\n");
echo ("Volume of square base pyramid is ");
echo( volumeSquare($b, $h));
echo("\n");
echo ("Volume of pentagonal base pyramid is ");
echo(volumePentagonal($a, $b, $h));
echo("\n");
echo("Volume of Hexagonal base pyramid is ");
echo(volumeHexagonal($a, $b, $h));

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>
// javascript program to find the volume.

// Function to find the volume
// of triangular pyramid
function volumeTriangular( a,
                        b,
                        h)
{
    let vol = (0.1666) * a *
                       b * h;
    return vol;
}

// Function to find the
// volume of square pyramid
function volumeSquare( b,  h)
{
    let vol = (0.33) * b *
                     b * h;
    return vol;
}

// Function to find the volume
// of pentagonal pyramid
function volumePentagonal( a,  b,   h)
{
    let vol = (0.83) * a * b * h;
    return vol;
}

// Function to find the volume
// of hexagonal pyramid
function volumeHexagonal( a,   b, h)
{
    let vol = a * b * h;
    return vol;
}

// Driver Code

    let b = 4, h = 9, a = 4;
    document.write( "Volume of triangular"
         + " base pyramid is "
         + volumeTriangular(a, b, h)
         +"<br/>");

   document.write( "Volume of square "
         + " base pyramid is "
         + volumeSquare(b, h)
         +"<br/>");

    document.write( "Volume of pentagonal"
         + " base pyramid is "
         + volumePentagonal(a, b, h)
         +"<br/>");

    document.write("Volume of Hexagonal"
         + " base pyramid is "
         + volumeHexagonal(a, b, h));

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
Volume of triangular base pyramid is 23.9904
Volume of square base pyramid is 47.52
Volume of pentagonal base pyramid is 119.52
Volume of Hexagonal base pyramid is 144
```