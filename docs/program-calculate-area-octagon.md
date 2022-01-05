# 计算八边形面积的程序

> 原文:[https://www . geesforgeks . org/program-calculate-area-八角形/](https://www.geeksforgeeks.org/program-calculate-area-octagon/)

正八边形是边长相同、内角大小相同的封闭图形。它有八条反射对称线和八阶旋转对称线。正八边形每个顶点的内角是 135°。中心角是 45 度。
**属性:**

> 凸多边形，等边多边形，等边图形，等轴图形，环形。

![](img/53488c525583d7011393ab065174943d.png)

**公式:**

```
Area : 2 × (side length)² × (1+sqrt(2))
```

**例:**

```
Input : side = 3
Output : Area of Regular Octagon = 43.4558

Input : side = 4
Output : Area of Regular Octagon = 77.2548
```

## C++

```
// CPP program to find area of octagon
#include <bits/stdc++.h>
using namespace std;

// Utility function
double areaOctagon(double side)
{
    return (float)(2 * (1 + sqrt(2)) *
                   side * side);
}

// Driver Code
int main()
{
    double side = 4;
    cout << "Area of Regular Octagon = "
         << areaOctagon(side) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// area of Octagon.
import java.io.*;

class GFG
{  
    // utility function
    static double areaOctagon(double side)
    {
    return (float)(2 * (1 + Math.sqrt(2))
                          * side * side);
    }

    // driver code
    public static void main(String arg[])
    {
        double side = 4;
        System.out.print("Area of Regular Octagon = " 
                          + areaOctagon(side));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to
# find area of octagon

import math

# Utility function
def areaOctagon(side):
    return (2 * (1 + (math.sqrt(2))) * side * side)

# Driver function
side = 4
print("Area of Regular Octagon =",
       round(areaOctagon(side), 4))

# This code is contributed
# by Azkia Anam.
```

## C#

```
// C# Program to find
// area of Octagon.
using System;

class GFG
{
    // utility function
    static double areaOctagon(double side)
    {
    return (float)(2 * (1 + Math.Sqrt(2))
                        * side * side);
    }

    // Driver code
    public static void Main()
    {
        double side = 4;
        Console.WriteLine("Area of Regular Octagon = "
                          + areaOctagon(side));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find area of octagon

// Utility function
function areaOctagon( $side)
{
    return (2 * (1 + sqrt(2)) *
            $side * $side);
}

// Driver Code

$side = 4;
echo("Area of Regular Octagon = ");
echo(areaOctagon($side));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to find area of octagon

// Utility function
function areaOctagon(side)
{
    return (2 * (1 + Math.sqrt(2)) *
                side * side);
}

// Driver Code
    let side = 4;
    document.write("Area of Regular Octagon = "
        + areaOctagon(side) + "<br>");

// This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
Area of Regular Octagon = 77.2548
```