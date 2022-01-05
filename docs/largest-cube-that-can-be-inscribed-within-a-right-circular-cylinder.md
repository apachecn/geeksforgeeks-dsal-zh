# 可内接在正圆柱体内的最大立方体

> 原文:[https://www . geeksforgeeks . org/可在右圆柱体内刻制的最大立方体/](https://www.geeksforgeeks.org/largest-cube-that-can-be-inscribed-within-a-right-circular-cylinder/)

这里给出的是一个高度为 **h** 半径为 **r** 的右圆柱体。任务是找到最大立方体的**体积**，可以在里面刻字。
**示例** :

```
Input: h = 3, r = 2
Output: volume = 27

Input: h = 5, r = 4
Output: volume = 125
```

![](img/3da9908b2010e4d014ad45d8ec4c4bd3.png)

**接近**:从图中可以清楚的了解到**立方体的边=圆柱体的高度**。
所以，**卷= (height)^3**
以下是上述方法的实施:

## C++

```
// C++ Program to find the biggest cube
// inscribed within a right circular cylinder
#include <bits/stdc++.h>
using namespace std;

// Function to find the volume of the cube
float cube(float h, float r)
{

    // height and radius cannot be negative
    if (h < 0 && r < 0)
        return -1;

    // volume of the cube
    float a = pow(h, 3);

    return a;
}

// Driver code
int main()
{
    float h = 5, r = 4;
    cout << cube(h, r) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the biggest cube
// inscribed within a right circular cylinder
class Solution
{

// Function to find the volume of the cube
static float cube(float h, float r)
{

    // height and radius cannot be negative
    if (h < 0 && r < 0)
        return -1;

    // volume of the cube
    float a = (float)Math.pow(h, 3);

    return a;
}

// Driver code
public static void main(String args[])
{
    float h = 5, r = 4;
    System.out.println( cube(h, r) );
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 Program to find the biggest cube
# inscribed within a right circular cylinder
import math

# Function to find the volume of the cube
def cube(h, r):

    # height and radius cannot be negative
    if (h < 0 and r < 0):
        return -1

    # volume of the cube
    a = math.pow(h, 3)

    return a

# Driver code
h = 5; r = 4;
print(cube(h, r));

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# Program to find the biggest
// cube inscribed within a right
// circular cylinder
using System;

class GFG
{

// Function to find the volume
// of the cube
static float cube(float h, float r)
{

    // height and radius cannot
    // be negative
    if (h < 0 && r < 0)
        return -1;

    // volume of the cube
    float a = (float)Math.Pow(h, 3);

    return a;
}

// Driver code
public static void Main()
{
    float h = 5, r = 4;
    Console.Write( cube(h, r) );
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the biggest 
// cube inscribed within a right
// circular cylinder

// Function to find the volume
// of the cube
function cube($h, $r)
{

    // height and radius cannot
    // be negative
    if ($h < 0 && $r < 0)
        return -1;

    // volume of the cube
    $a = pow($h, 3);

    return $a;
}

// Driver code
$h = 5;
$r = 4;
echo cube($h, $r);

// This code is contributed by @Tushil.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the biggest cube
// inscribed within a right circular cylinder

// Function to find the volume of the cube
function cube(h , r)
{

    // height and radius cannot be negative
    if (h < 0 && r < 0)
        return -1;

    // volume of the cube
    var a = Math.pow(h, 3);

    return a;
}

// Driver code

var h = 5, r = 4;
document.write( cube(h, r) );

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
125
```