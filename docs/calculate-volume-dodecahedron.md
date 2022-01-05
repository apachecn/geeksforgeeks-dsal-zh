# 计算十二面体的体积

> 原文:[https://www . geesforgeks . org/calculate-volume-十二面体/](https://www.geeksforgeeks.org/calculate-volume-dodecahedron/)

给定十二面体的边，计算它的体积。体积是形状占据的空间量。
A [**十二面体**](https://en.wikipedia.org/wiki/Dodecahedron) 是一个由 12 个面或平边组成的三维图形。所有的面都是同样大小的五角星。“十二面体”一词来源于希腊语中的“十二面体”和“面”。
**公式:**
体积= (15 + 7√5)*e <sup>3</sup> /4
其中 e 为一条边的长度。
示例:

```
Input : side = 4
Output : 490.44

Input : side = 9
Output : 5586.41
```

## C++

```
// CPP program to calculate
// Volume of dodecahedron
#include <bits/stdc++.h>
using namespace std;

// utility Function
double vol_of_dodecahedron(int side)
{
    return (((15 + (7 * (sqrt(5)))) / 4)
                       * (pow(side, 3))) ;
}
// Driver Function
int main()
{
    int side = 4;

    cout << "Volume of dodecahedron = "
         << vol_of_dodecahedron(side);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// Volume of dodecahedron

import java.io.*;

class GFG
{
        // driver function
    public static void main (String[] args)
       {
           int side = 4;
           System.out.print("Volume of dodecahedron = ");
           System.out.println(vol_of_dodecahedron(side));
       }

     static double vol_of_dodecahedron(int side)
        {
             return (((15 + (7 * (Math.sqrt(5)))) / 4)
                       * (Math.pow(side, 3)));
        }
}

// This code is contributed
// by Azkia Anam.
```

## 蟒蛇 3

```
# Python3 program to calculate
# Volume of dodecahedron
import math

# utility Function
def vol_of_dodecahedron(side) :

    return (((15 + (7 * (math.sqrt(5)))) / 4)
                    * (math.pow(side, 3)))

# Driver Function
side = 4
print("Volume of dodecahedron =",
       round(vol_of_dodecahedron(side), 2))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to calculate
// Volume of dodecahedron
using System;

public class GFG
{

    // utility Function
    static float vol_of_dodecahedron(int side)
    {
        return (float)(((15 + (7 * (Math.Sqrt(5)))) / 4)
                        * (Math.Pow(side, 3))) ;
    }

    // Driver Function
    static public void Main ()
    {
        int side = 4;

        Console.WriteLine("Volume of dodecahedron = "
            + vol_of_dodecahedron(side));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// Volume of dodecahedron

// utility Function
function vol_of_dodecahedron($side)
{
    return (((15 + (7 * (sqrt(5)))) / 4)
                      * (pow($side, 3))) ;
}

    // Driver Function
    $side = 4;
    echo ("Volume of dodecahedron = ");
    echo(vol_of_dodecahedron($side));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to calculate
// Volume of dodecahedron

// utility Function
function vol_of_dodecahedron( side)
{
    return (((15 + (7 * (Math.sqrt(5)))) / 4)
                       * (Math.pow(side, 3))) ;
}

// Driver Function
    let side = 4;
    document.write("Volume of dodecahedron = " +
    vol_of_dodecahedron(side).toFixed(2));

    // This code contributed by gauravrajput1
</script>
```

输出:

```

Volume of dodecahedron = 490.44
```