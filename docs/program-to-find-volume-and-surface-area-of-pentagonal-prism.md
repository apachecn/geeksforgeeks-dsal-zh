# 求五角棱镜体积和表面积的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-volume-and-surface-area-of-五边形棱镜/](https://www.geeksforgeeks.org/program-to-find-volume-and-surface-area-of-pentagonal-prism/)

有 5 个矩形面和 2 个平行的五边形底面的棱镜就是五边形棱镜。所以给你五角棱镜的[顶点](https://en.wikipedia.org/wiki/Apothem)长度 **(a)** 、基长 **(b)** 和高度 **(h)** 。你要找到**五角棱镜的表面积和体积。**
**例:**

```
Input : a=3, b=5, h=6
Output :surface area=225, volume=225

Input : a=2, b=3, h=5
Output :surface area=105, volume=75
```

![](https://media.geeksforgeeks.org/wp-content/uploads/prism-3.png)

**在这个图中，**
**一**——五角棱镜的一个长度。
**b**–五角棱镜的基本长度。
**h**–五角棱镜的高度。
**公式:**下面是计算皮达戈纳尔棱镜表面积和体积的公式。

![$ surface\ Area(A)= 5\times a\times b + 5\times b\times h $  ](img/6b06a61881bccfd2b9bd4403b23de768.png "Rendered by QuickLaTeX.com")

![$ Volume(v)= \frac{5}{2}\times b\times h $  ](img/98a1407219bef575ead0c2b50c2666cd.png "Rendered by QuickLaTeX.com")

## C++

```
// CPP program to find
// surface area and volume of the
// Pentagonal Prism
#include <bits/stdc++.h>
using namespace std;

// function for surface area
float surfaceArea(float a, float b, float h)
{
    return 5 * a * b + 5 * b * h;
}

// function for VOlume
float volume(float b, float h)
{
    return (5 * b * h) / 2;
}

// Driver function
int main()
{
    float a = 5;
    float b = 3;
    float h = 7;

    cout << "surface area= " << surfaceArea(a, b, h) << ", ";

    cout << "volume= " << volume(b, h);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// surface area and volume of the
// Pentagonal Prism
import java.util.*;

class solution
{

// function for surface area
static float surfaceArea(float a, float b, float h)
{

    return 5 * a * b + 5 * b * h;

}

// function for VOlume
static float volume(float b, float h)
{

    return (5 * b * h) / 2;

}

// Driver function
public static void main(String arr[])
{
    float a = 5;
    float b = 3;
    float h = 7;

    System.out.println( "surface area= "+surfaceArea(a, b, h)+", ");

    System.out.println("volume= "+volume(b, h));
}
}
```

## 蟒蛇 3

```
# Python 3 program to find surface area
# and volume of the Pentagonal Prism

# function for surface area
def surfaceArea(a, b, h):
    return 5 * a * b + 5 * b * h

# function for VOlume
def volume(b, h):
    return (5 * b * h) / 2

# Driver Code
if __name__ == '__main__':
    a = 5
    b = 3
    h = 7

    print("surface area =", surfaceArea(a, b, h),
                   ",", "volume =", volume(b, h))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find surface
// area and volume of the
// Pentagonal Prism
using System;

class GFG
{

// function for surface area
static float surfaceArea(float a,
                         float b, float h)
{
    return 5 * a * b + 5 * b * h;
}

// function for VOlume
static float volume(float b, float h)
{
    return (5 * b * h) / 2;
}

// Driver Code
public static void Main()
{
    float a = 5;
    float b = 3;
    float h = 7;

    Console.WriteLine("surface area = " +
            surfaceArea(a, b, h) + ", ");

    Console.WriteLine("volume = " +
                     volume(b, h));
}
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// surface area and volume
// of the Pentagonal Prism

// function for surface area
function surfaceArea($a, $b, $h)
{
    return 5 * $a * $b +
           5 * $b * $h;
}

// function for VOlume
function volume($b, $h)
{
    return (5 * $b * $h) / 2;
}

// Driver Code
$a = 5;
$b = 3;
$h = 7;

echo "surface area = " ,
      surfaceArea($a, $b, $h) , ", ";

echo "volume = " , volume($b, $h);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>
// javascript program to find
// surface area and volume of the
// Pentagonal Prism

// function for surface area
function surfaceArea( a,  b,  h)
{
    return 5 * a * b + 5 * b * h;
}

// function for VOlume
function volume( b,  h)
{
    return (5 * b * h) / 2;
}

// Driver function
    let a = 5;
    let b = 3;
    let h = 7;

    document.write( "surface area= " + surfaceArea(a, b, h) + ", ");

    document.write( "volume= " + volume(b, h));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
surface area= 180, volume= 52.5
```