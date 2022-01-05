# 球体内部可内切的最大立方体

> 原文:[https://www . geeksforgeeks . org/最大的球内可刻立方体/](https://www.geeksforgeeks.org/largest-cube-that-can-be-inscribed-within-the-sphere/)

这里给定的是一个半径为 **r** 的球体，任务是找到最大立方体的可以放入其中的一边。
**例:**

```
Input: r = 8
Output: 9.2376

Input: r = 5
Output: 5.7735
```

![](img/eff621ba031e2aaabda979dd12bd2c53.png)

**接近** :

> 立方体的边= **a**
> 球体的半径= **r**
> 从对角线上看，很明显，立方体的对角线=球体的直径，
> **a√3 = 2r** 或者， **a = 2r/√3**

下面是实现:

## C++

```
// C++ Program to find the biggest cube
// inscribed within a sphere
#include <bits/stdc++.h>
using namespace std;

// Function to find the side of the cube
float largestCube(float r)
{

    // radius cannot be negative
    if (r < 0)
        return -1;

    // side of the cube
    float a = (2 * r) / sqrt(3);
    return a;
}

// Driver code
int main()
{
    float r = 5;
    cout << largestCube(r) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the biggest cube
// inscribed within a sphere
import java.util.*;
class Solution{
// Function to find the side of the cube
static float largestCube(float r)
{

    // radius cannot be negative
    if (r < 0)
        return -1;

    // side of the cube
    float a = (2 * r) / (float)Math.sqrt(3);
    return a;
}

// Driver code
public static void main(String args[])
{
    float r = 5;
    System.out.println( largestCube(r));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 Program to find the biggest
# cube inscribed within a sphere
from math import sqrt

# Function to find the side of the cube
def largestCube(r):

    # radius cannot be negative
    if (r < 0):
        return -1

    # side of the cube
    a = (2 * r) / sqrt(3)
    return a

# Driver code
if __name__ == '__main__':
    r = 5
    print("{0:.6}".format(largestCube(r)))

# This code is contributed
# by SURENDRA_GANGWAR
```

## C#

```
// C# Program to find the biggest cube
// inscribed within a sphere
using System;
class Solution{
// Function to find the side of the cube
static float largestCube(float r)
{

    // radius cannot be negative
    if (r < 0)
        return -1;

    // side of the cube
    float a = (2 * r) / (float)Math.Sqrt(3);
    return a;
}

// Driver code
static void Main()
{
    float r = 5;
    Console.WriteLine( largestCube(r));

}

}
//This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the biggest
// cube inscribed within a sphere

// Function to find the side
// of the cube
function largestCube($r)
{

    // radius cannot be negative
    if ($r < 0)
        return -1;

    // side of the cube
    $a = (float)((2 * $r) / sqrt(3));
    return $a;
}

// Driver code
$r = 5;
echo largestCube($r);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// javascript Program to find the biggest cube
// inscribed within a sphere

// Function to find the side of the cube
function largestCube(r)
{

    // radius cannot be negative
    if (r < 0)
        return -1;

    // side of the cube
    var a = (2 * r) / Math.sqrt(3);
    return a;
}

// Driver code 
var r = 5;
document.write( largestCube(r).toFixed(5));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
5.7735
```