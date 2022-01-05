# 检查是否可以用给定的方向余弦画一条直线

> 原文:[https://www . geeksforgeeks . org/check-如果有可能画一条给定方向的直线-余弦/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-draw-a-straight-line-with-the-given-direction-cosines/)

给定三维平面的三个方向余弦 **l** 、 **m** 和 **n** ，任务是检查是否有可能用它们画一条直线。如果可能，打印**是**否则打印**否**。
**举例:**

> **输入:** l = 0.258，m = 0.80，n = 0.23
> **输出:**否
> **输入:** l = 0.70710678，m = 0.5，n = 0.5
> **输出:**是

**逼近:**如果一条直线与正的 **X 轴**形成角度 **a** ，与正的 **Y 轴**形成角度 **b** ，与正的 **Z 轴**形成角度 **c** ，则它的方向余弦为 **cos(a)** 、 **cos(b)** 和 **cos(c)** 。
直线，**cos<sup>2</sup>(a)+cos<sup>2</sup>(b)+cos<sup>2</sup>(c)= 1**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if a straight line is possible
bool isPossible(float x, float y, float z)
{
    float a = x * x + y * y + z * z;
    if (ceil(a) == 1 && floor(a) == 1)
        return true;
    return false;
}

// Driver code
int main()
{
    float l = 0.70710678, m = 0.5, n = 0.5;

    if (isPossible(l, m, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true
// if a straight line is possible
static boolean isPossible(float x, float y, float z)
{
    float a = x * x + y * y + z * z;
    if (Math.ceil(a) == 1 && Math.floor(a) == 1)
        return true;
    return false;
}

// Driver code
public static void main(String args[])
{
    float l = 0.70710678f, m = 0.5f, n = 0.5f;

    if (isPossible(l, m, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil, floor

# Function that returns true
# if a straight line is possible
def isPossible(x, y, z) :

    a = x * x + y * y + z * z
    a = round(a, 8)

    if (ceil(a) == 1 & floor(a) == 1) :
        return True
    return False

# Driver code
if __name__ == "__main__" :

    l = 0.70710678
    m = 0.5
    n = 0.5

    if (isPossible(l, m, n)):
        print("Yes")
    else :
        print("No")

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true
// if a straight line is possible
static bool isPossible(float x, float y, float z)
{
    float a = x * x + y * y + z * z;
    if (Math.Ceiling(a) == 1 && Math.Floor(a) == 1)
        return true;
    return false;
}

// Driver code
public static void Main()
{
    float l = 0.70710678f, m = 0.5f, n = 0.5f;
    if (isPossible(l, m, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true
// if a straight line is possible
function isPossible($x, $y, $z)
{
    $a = round($x * $x + $y * $y + $z * $z);
    if (ceil($a) == 1 && floor($a) == 1)
        return true;
    return false;
}

// Driver code
$l = 0.70710678; $m = 0.5; $n = 0.5;

if (isPossible($l, $m, $n))
    echo("Yes");
else
    echo("No");
// This code is contributed by mukul singh.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true
// if a straight line is possible
function isPossible(x,y,z)
{
    let a = Math.round(x * x + y * y + z * z);

    if (Math.ceil(a) == 1 && Math.floor(a) == 1)
        return true;
    return false;
}

// Driver code
let l = 0.70710678, m = 0.5, n = 0.5;
if (isPossible(l, m, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Yes
```