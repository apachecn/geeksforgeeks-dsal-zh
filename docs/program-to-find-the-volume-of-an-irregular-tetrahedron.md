# 求不规则四面体体积的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-volume-of-a-rule-tetrahedron/](https://www.geeksforgeeks.org/program-to-find-the-volume-of-an-irregular-tetrahedron/)

给定不规则四面体的边长。任务是确定四面体的体积。
**让金字塔的边长为 U、U、V、V、w、**

![](img/4dff83eb1d3688e6b8a80e19f50cf886.png)

**示例:**

```
Input: u = 1000, v = 1000, w = 1000, U = 3, V = 4, W = 5
Output: 1999.9947

Input: u = 2000, v = 2000, w = 2000, U = 3, V = 4, W = 5
Output: 3999.9858
```

根据边长计算不规则四面体体积的公式为:
A =
![\begin{vmatrix} 0 & u*u & v*v & w*w & 1 \\ u*u & 0 & W*W & V*V & 1 \\ v*v & W*W & 0 & U*U & 1 \\ w*w & V*V & W*W & 0 & 1 \\ 1 & 1 & 1 & 1 & 0 \end{vmatrix}   ](img/3263a80145ea32904b7f7ea24c3d0dc0.png "Rendered by QuickLaTeX.com")

> 体积= sqrt(a/288)=
> t1]sqrt(4 * u * u * v * v * w * w–u * u *(v * v+w * w–u * u)^ 2–v * v(w * w+u * u–v)^ 2–w * w(u * u+v * v–w)^ 2+(u * u+v * v–w)*(w * w+u * u–v * v)*(w * v)

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define db double
// Function to find the volume
void findVolume(db u, db v, db w, db U, db V, db W, db b)
{

    // Steps to calculate volume of a
    // Tetrahedron using formula
    db uPow = pow(u, 2);
    db vPow = pow(v, 2);
    db wPow = pow(w, 2);
    db UPow = pow(U, 2);
    db VPow = pow(V, 2);
    db WPow = pow(W, 2);

    db a = 4 * (uPow * vPow * wPow)
        - uPow * pow((vPow + wPow - UPow), 2)
        - vPow * pow((wPow + uPow - VPow), 2)
        - wPow * pow((uPow + vPow - WPow), 2)
        + (vPow + wPow - UPow) * (wPow + uPow - VPow)
        * (uPow + vPow - WPow);
    db vol = sqrt(a);
    vol /= b;

    cout << fixed << setprecision(4) << vol;
}

// Driver code
int main()
{

    // edge lengths
    db u = 1000, v = 1000, w = 1000;
    db U = 3, V = 4, W = 5;
    db b = 12;

    findVolume(u, v, w, U, V, W, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the volume
static void findVolume(double u, double v, double w, double U,
                      double V, double W, double b)
{

    // Steps to calculate volume of a
    // Tetrahedron using formula
    double uPow = Math.pow(u, 2);
    double vPow = Math.pow(v, 2);
    double wPow = Math.pow(w, 2);
    double UPow = Math.pow(U, 2);
    double VPow = Math.pow(V, 2);
    double WPow = Math.pow(W, 2);

    double a = 4 * (uPow * vPow * wPow)
        - uPow * Math.pow((vPow + wPow - UPow), 2)
        - vPow * Math.pow((wPow + uPow - VPow), 2)
        - wPow * Math.pow((uPow + vPow - WPow), 2)
        + (vPow + wPow - UPow) * (wPow + uPow - VPow)
        * (uPow + vPow - WPow);
    double vol = Math.sqrt(a);
    vol /= b;

    System.out.printf("%.4f",vol);
}

// Driver code
public static void main(String args[])
{

    // edge lengths
    double u = 1000, v = 1000, w = 1000;
    double U = 3, V = 4, W = 5;
    double b = 12;

    findVolume(u, v, w, U, V, W, b);
}

}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# from math lib import everything
from math import *

# Function to find the volume
def findVolume(u, v, w, U, V, W, b) :

    # Steps to calculate volume of a
    # Tetrahedron using formula
    uPow = pow(u, 2)
    vPow = pow(v, 2)
    wPow = pow(w, 2)
    UPow = pow(U, 2)
    VPow = pow(V, 2)
    WPow = pow(W, 2)

    a = (4 * (uPow * vPow * wPow)
        - uPow * pow((vPow + wPow - UPow), 2)
        - vPow * pow((wPow + uPow - VPow), 2)
        - wPow * pow((uPow + vPow - WPow), 2)
        + (vPow + wPow - UPow) * (wPow + uPow - VPow)
        * (uPow + vPow - WPow))

    vol = sqrt(a)
    vol /= b

    print(round(vol,4))

# Driver code    
if __name__ == "__main__" :

    # edge lengths
    u, v, w = 1000, 1000, 1000
    U, V, W = 3, 4, 5
    b = 12

    findVolume(u, v, w, U, V, W, b)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the volume
static void findVolume(double u, double v,
                       double w, double U,
                       double V, double W,
                       double b)
{

    // Steps to calculate volume of a
    // Tetrahedron using formula
    double uPow = Math.Pow(u, 2);
    double vPow = Math.Pow(v, 2);
    double wPow = Math.Pow(w, 2);
    double UPow = Math.Pow(U, 2);
    double VPow = Math.Pow(V, 2);
    double WPow = Math.Pow(W, 2);

    double a = 4 * (uPow * vPow * wPow) -
                    uPow * Math.Pow((vPow + wPow - UPow), 2) -
                    vPow * Math.Pow((wPow + uPow - VPow), 2) -
                    wPow * Math.Pow((uPow + vPow - WPow), 2) +
                    (vPow + wPow - UPow) *
                    (wPow + uPow - VPow) * (uPow + vPow - WPow);
    double vol = Math.Sqrt(a);
    vol /= b;

    Console.Write(System.Math.Round(vol, 4));
}

// Driver code
public static void Main()
{

    // edge lengths
    double u = 1000, v = 1000, w = 1000;
    double U = 3, V = 4, W = 5;
    double b = 12;

    findVolume(u, v, w, U, V, W, b);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the volume
function findVolume($u, $v, $w,
                    $U, $V, $W, $b)
{

    // Steps to calculate volume of
    // a Tetrahedron using formula
    $uPow = pow($u, 2);
    $vPow = pow($v, 2);
    $wPow = pow($w, 2);
    $UPow = pow($U, 2);
    $VPow = pow($V, 2);
    $WPow = pow($W, 2);

    $a = 4 * ($uPow * $vPow * $wPow) -
              $uPow * pow(($vPow + $wPow - $UPow), 2) -
              $vPow * pow(($wPow + $uPow - $VPow), 2) -
              $wPow * pow(($uPow + $vPow - $WPow), 2) +
              ($vPow + $wPow - $UPow) *
              ($wPow + $uPow - $VPow) *
              ($uPow + $vPow - $WPow);
    $vol = sqrt($a);
    $vol /= $b;

    echo $vol;
}

// Driver code

// edge lengths
$u = 1000;
$v = 1000;
$w = 1000;
$U = 3;
$V = 4;
$W = 5;
$b = 12;

findVolume($u, $v, $w, $U, $V, $W, $b);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find the volume
function findVolume(u, v, w, U, V, W, b)
{

    // Steps to calculate volume of a
    // Tetrahedron using formula
    let uPow = Math.pow(u, 2);
    let vPow = Math.pow(v, 2);
    let wPow = Math.pow(w, 2);
    let UPow = Math.pow(U, 2);
    let VPow = Math.pow(V, 2);
    let WPow = Math.pow(W, 2);

    let a = 4 * (uPow * vPow * wPow) -
          uPow * Math.pow((vPow + wPow - UPow), 2) -
          vPow * Math.pow((wPow + uPow - VPow), 2) -
          wPow * Math.pow((uPow + vPow - WPow), 2) +
          (vPow + wPow - UPow) * (wPow + uPow - VPow) *
          (uPow + vPow - WPow);

    let vol = Math.sqrt(a);
    vol /= b;

    document.write(vol.toFixed(4));
}

// Driver code

// Edge lengths
let u = 1000, v = 1000, w = 1000;
let U = 3, V = 4, W = 5;
let b = 12;

findVolume(u, v, w, U, V, W, b);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1999.9947
```