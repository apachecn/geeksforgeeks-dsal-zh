# 八面体表面积程序

> 原文:[https://www . geesforgeks . org/八面体表面积程序/](https://www.geeksforgeeks.org/program-for-surface-area-of-octahedron/)

给定八面体的边，然后计算表面积。

示例:

```
Input  : 7
Output : 169.741

Input  : 9
Output : 280.59
```

正八面体有八个面，都是等边三角形。八面体的面积是 2 乘以边长的平方乘以 3 的平方根。

> 公式:
> 表面积= 2*(sqrt(3))*(边*边)

## C++

```
// CPP Program to calculate
// surface area of Octahedron
#include <bits/stdc++.h>
using namespace std;

// utility Function
double surface_area_octahedron(double side)
{
    return (2*(sqrt(3))*(side*side));
}

// Driver Function
int main()
{
    double side = 7;
    cout << "Surface area of octahedron ="
        << surface_area_octahedron(side)
        << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to calculate
// surface area of Octahedron.

import java.io.*;
import java.util.*;

class GFG {

// utility Function
static double surface_area_octahedron(double side)
{
    return (2*(Math.sqrt(3))*(side*side));
}
    public static void main (String[] args) {
    double side = 7;
    System.out.println("Surface area of octahedron ="
                    + surface_area_octahedron(side));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python Program to calculate
# surface area of Octahedron.
import math

# utility Function
def surface_area_octahedron( side):

    return (2*(math.sqrt(3))*(side*side))

# driver code
side = 7
print("Surface area of octahedron =" ,
      surface_area_octahedron(side))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to calculate
// surface area of Octahedron.
using System;

class GFG {

    // utility Function
    static double surface_area_octahedron(double side)
    {
        return (2 * (Math.Sqrt(3)) * (side * side));
    }

    // Driver code
    public static void Main()
    {
        double side = 7;
        Console.WriteLine("Surface area of octahedron ="
                        + surface_area_octahedron(side));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to calculate
// surface area of Octahedron

// utility Function
function surface_area_octahedron($side)
{
    return (2 * (sqrt(3)) *
           ($side * $side));
}

// Driver Code
$side = 7;
echo("Surface area of octahedron =");
echo( surface_area_octahedron($side));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// JavaScript program to calculate
// surface area of Octahedron.

// Utility Function
function surface_area_octahedron(side)
{
    return (2 * (Math.sqrt(3)) * (side*side));
}

// Driver Code
let side = 7;

document.write("Surface area of octahedron =" +
               surface_area_octahedron(side));

// This code is contributed by avijitmondal1998

</script>
```

**输出:**

```
Surface area of octahedron =169.741
```