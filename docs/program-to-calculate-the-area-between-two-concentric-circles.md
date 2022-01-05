# 计算两个同心圆之间面积的程序

> 原文:[https://www . geeksforgeeks . org/计算两个同心圆之间面积的程序/](https://www.geeksforgeeks.org/program-to-calculate-the-area-between-two-concentric-circles/)

给定半径为 **X** 和 **Y** 的两个同心圆，其中( **X > Y** )。找到它们之间的区域。
你需要找到绿色区域的区域，如下图所示:

![](img/b17f11d72a6a759ead385151eef4dbaf.png)

**示例:**

```
Input : X = 2, Y = 1
Output : 9.42478

Input : X = 4, Y = 2
Output : 37.6991
```

**方法:**
两个给定同心圆之间的面积可以通过外圆面积减去内圆面积来计算。自 **X > Y** 起。 **X** 是外圆的半径。
因此，两个给定同心圆之间的面积将为:

```
π*X2 - π*Y2
```

下面是上述方法的实现:

## C++

```
// C++ program to find area between the
// two given concentric circles

#include <bits/stdc++.h>
using namespace std;

// Function to find area between the
// two given concentric circles
double calculateArea(int x, int y)
{
    // Declare value of pi
    double pi = 3.1415926536;

    // Calculate area of outer circle
    double arx = pi * x * x;

    // Calculate area of inner circle
    double ary = pi * y * y;

    // Difference in areas
    return arx - ary;
}

// Driver Program
int main()
{
    int x = 2;
    int y = 1;

    cout << calculateArea(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find area between the
// two given concentric circles
import java.io.*;

class GFG
{

// Function to find area between the
// two given concentric circles
static double calculateArea(int x, int y)
{
    // Declare value of pi
    double pi = 3.1415926536;

    // Calculate area of outer circle
    double arx = pi * x * x;

    // Calculate area of inner circle
    double ary = pi * y * y;

    // Difference in areas
    return arx - ary;
}

// Driver code
public static void main (String[] args)
{
    int x = 2;
    int y = 1;
    System.out.println (calculateArea(x, y));
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python3 program to find area between 
# the two given concentric circles

# Function to find area between the
# two given concentric circles
def calculateArea(x, y):

    # Declare value of pi
    pi = 3.1415926536

    # Calculate area of outer circle
    arx = pi * x * x

    # Calculate area of inner circle
    ary = pi * y * y

    # Difference in areas
    return arx - ary

# Driver Code
x = 2
y = 1

print(calculateArea(x, y))

# This code is contributed
# by shashank_sharma
```

## C#

```
// C# program to find area between the
// two given concentric circles
using System;

class GFG
{

// Function to find area between the
// two given concentric circles
static double calculateArea(int x, int y)
{
    // Declare value of pi
    double pi = 3.1415926536;

    // Calculate area of outer circle
    double arx = pi * x * x;

    // Calculate area of inner circle
    double ary = pi * y * y;

    // Difference in areas
    return arx - ary;
}

// Driver code
public static void Main ()
{
    int x = 2;
    int y = 1;
    Console.WriteLine(calculateArea(x, y));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find area between the
// two given concentric circles

// Function to find area between the
// two given concentric circles
function calculateArea($x, $y)
{
    // Declare value of pi
    $pi = 3.1415926536;

    // Calculate area of outer circle
    $arx = $pi * $x * $x;

    // Calculate area of inner circle
    $ary = $pi * $y * $y;

    // Difference in areas
    return ($arx - $ary);
}

// Driver Code
$x = 2;
$y = 1;

echo calculateArea($x, $y);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to find area between
// the two given concentric circles

// Function to find
// nth concentric hexagon number
function calculateArea(x, y)
{

    // Declare value of pi
    var pi = 3.1415926536;

    // Calculate area of outer circle
    var arx = pi * x * x;

    // Calculate area of inner circle
    var ary = pi * y * y;

    // Difference in areas
    return arx - ary;
}

// Driver code
var x = 2;
var y = 1;

// Function call
document.write(calculateArea(x, y));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
9.42478
```

**时间复杂度:** O(1)