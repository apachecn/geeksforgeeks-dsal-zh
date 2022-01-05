# 确定轴向平面八分之一的程序

> 原文:[https://www . geesforgeks . org/确定轴面八分之一的程序/](https://www.geeksforgeeks.org/program-to-determine-the-octant-of-the-axial-plane/)

给定 3 个坐标 x，y 和 z，任务是确定轴向平面的八分之一。
**例:**

> **输入:** 2、3、4
> **输出:**点位于第一个八分点
> **输入:** -4、2、-8
> **输出:**点位于第六个八分点
> **输入:** -6、-2、8
> **输出:**点位于第三个八分点

**方法:**下面给出的是为了确定轴向平面的八分之一需要检查的条件。

*   检查 x >= 0 和 y >= 0 和 z >= 0，那么点位于第一个八分点。
*   检查 x < 0 and y > = 0 和 z >= 0，那么点位于第二个八分点。
*   检查 x < 0 and y < 0 and z > = 0，则点位于第三个八分点。
*   检查 x >= 0，y < 0 and z > = 0，那么点位于第四个八分点。
*   检查 x >= 0 和 y >= 0 和 z < 0，那么点位于第五个八分点。
*   检查 x < 0 and y > = 0 且 z < 0，则点位于第六个八分点。
*   检查 x < 0 和 y < 0 和 z < 0，那么点位于第七个八分点。
*   检查 x >= 0 和 y < 0 和 z < 0，那么点位于第八个八分点。

以下是上述方法的实现:

## C++

```
// C++ program to print octant
// of a given point.
#include <bits/stdc++.h>
#include<math.h>

using namespace std;

// Function to print octant
void octant(float x, float y,
                     float z)
{
    if (x >= 0 && y >= 0 && z >= 0)
        cout << "Point lies in 1st octant\n";

    else if (x < 0 && y >= 0 && z >= 0)
        cout << "Point lies in 2nd octant\n";

    else if (x < 0 && y < 0 && z >= 0)
        cout << "Point lies in 3rd octant\n";

    else if (x >= 0 && y < 0 && z >= 0)
        cout << "Point lies in 4th octant\n";

    else if (x >= 0 && y >= 0 && z < 0)
        cout << "Point lies in 5th octant\n";

    else if (x < 0 && y >= 0 && z < 0)
        cout << "Point lies in 6th octant\n";

    else if (x < 0 && y < 0 && z < 0)
        cout << "Point lies in 7th octant\n";

    else if (x >= 0 && y < 0 && z < 0)
        cout << "Point lies in 8th octant\n";
}

// Driver Code
int main()
{
    float x = 2, y = 3, z = 4;
    octant(x, y, z) ;

    x = -4, y = 2, z = -8;
    octant(x, y, z);

    x = -6, y = -2, z = 8;
    octant(x, y, z);
    return 0;
}
// This code is contributed
// by Amber_Saxena.
```

## C

```
// C program to print octant
// of a given point.
#include <stdio.h>

// Function to print octant
void octant(float x, float y,
                     float z)
{
    if (x >= 0 && y >= 0 && z >= 0)
        printf("Point lies in 1st octant\n");

    else if (x < 0 && y >= 0 && z >= 0)
        printf("Point lies in 2nd octant\n");

    else if (x < 0 && y < 0 && z >= 0)
        printf("Point lies in 3rd octant\n");

    else if (x >= 0 && y < 0 && z >= 0)
        printf("Point lies in 4th octant\n");

    else if (x >= 0 && y >= 0 && z < 0)
        printf("Point lies in 5th octant\n");

    else if (x < 0 && y >= 0 && z < 0)
        printf("Point lies in 6th octant\n");

    else if (x < 0 && y < 0 && z < 0)
        printf("Point lies in 7th octant\n");

    else if (x >= 0 && y < 0 && z < 0)
        printf("Point lies in 8th octant\n");
}

// Driver Code
int main()
{
    float x = 2, y = 3, z = 4;
    octant(x, y, z) ;

    x = -4, y = 2, z = -8;
    octant(x, y, z);

    x = -6, y = -2, z = 8;
    octant(x, y, z);
}

// This code is contributed
// by Amber_Saxena.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print octant
// of a given point.
import java.util.*;

class solution
{

// Function to print octant
static void octant(float x, float y,
                    float z)
{
    if (x >= 0 && y >= 0 && z >= 0)
        System.out.println("Point lies in 1st octant");

    else if (x < 0 && y >= 0 && z >= 0)
        System.out.println("Point lies in 2nd octant");

    else if (x < 0 && y < 0 && z >= 0)
    System.out.println("Point lies in 3rd octant");

    else if (x >= 0 && y < 0 && z >= 0)
        System.out.println("Point lies in 4th octant");

    else if (x >= 0 && y >= 0 && z < 0)
        System.out.println("Point lies in 5th octant");

    else if (x < 0 && y >= 0 && z < 0)
        System.out.println("Point lies in 6th octant");

    else if (x < 0 && y < 0 && z < 0)
        System.out.println("Point lies in 7th octant");

    else if (x >= 0 && y < 0 && z < 0)
    System.out.println("Point lies in 8th octant");
}

// Driver Code
public static void main(String args[])
{
    float x = 2, y = 3, z = 4;
    octant(x, y, z) ;

    x = -4; y = 2; z = -8;
    octant(x, y, z);

    x = -6; y = -2; z = 8;
    octant(x, y, z);

}
}
//This code is contributed by Surendra_Gangwar
```

## 计算机编程语言

```
# Python program to print octant of a
# given point.

# Function to print octant
def octant(x, y, z):

    if x >= 0 and y >= 0 and z >= 0:
        print "Point lies in 1st octant"

    elif x < 0 and y >= 0 and z >= 0:
        print "Point lies in 2nd octant"

    elif x < 0 and y < 0 and z >= 0:
        print "Point lies in 3rd octant"

    elif x >= 0 and y < 0 and z >= 0:
        print "Point lies in 4th octant"

    elif x >= 0 and y >= 0 and z < 0:
        print "Point lies in 5th octant"

    elif x < 0 and y >= 0 and z < 0:
        print "Point lies in 6th octant"

    elif x < 0 and y < 0 and z < 0:
        print "Point lies in 7th octant"

    elif x >= 0 and y < 0 and z < 0:
        print "Point lies in 8th octant"

# Driver Code
x, y, z = 2, 3, 4
octant(x, y, z)

x, y, z = -4, 2, -8
octant(x, y, z)

x, y, z = -6, -2, 8
octant(x, y, z)
```

## C#

```
// C# program to print octant
// of a given point.
using System;

class GFG
{

// Function to print octant
static void octant(float x, float y,
                   float z)
{
    if (x >= 0 && y >= 0 && z >= 0)
        Console.WriteLine("Point lies in 1st octant");

    else if (x < 0 && y >= 0 && z >= 0)
        Console.WriteLine("Point lies in 2nd octant");

    else if (x < 0 && y < 0 && z >= 0)
        Console.WriteLine("Point lies in 3rd octant");

    else if (x >= 0 && y < 0 && z >= 0)
        Console.WriteLine("Point lies in 4th octant");

    else if (x >= 0 && y >= 0 && z < 0)
        Console.WriteLine("Point lies in 5th octant");

    else if (x < 0 && y >= 0 && z < 0)
        Console.WriteLine("Point lies in 6th octant");

    else if (x < 0 && y < 0 && z < 0)
        Console.WriteLine("Point lies in 7th octant");

    else if (x >= 0 && y < 0 && z < 0)
    Console.WriteLine("Point lies in 8th octant");
}

// Driver Code
static public void Main ()
{
    float x = 2, y = 3, z = 4;
    octant(x, y, z) ;

    x = -4; y = 2; z = -8;
    octant(x, y, z);

    x = -6; y = -2; z = 8;
    octant(x, y, z);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print octant
// of a given point.

// Function to print octant
function octant($x, $y, $z)
{
    if ($x >= 0 && $y >= 0 && $z >= 0)
        echo "Point lies in 1st octant\n";

    else if ($x < 0 && $y >= 0 && $z >= 0)
        echo "Point lies in 2nd octant\n";

    else if ($x < 0 && $y < 0 && $z >= 0)
        echo "Point lies in 3rd octant\n";

    else if ($x >= 0 && $y < 0 && $z >= 0)
        echo "Point lies in 4th octant\n";

    else if ($x >= 0 && $y >= 0 && $z < 0)
        echo "Point lies in 5th octant\n";

    else if ($x < 0 && $y >= 0 && $z < 0)
        echo "Point lies in 6th octant\n";

    else if ($x < 0 && $y < 0 && $z < 0)
        echo "Point lies in 7th octant\n";

    else if ($x >= 0 && $y < 0 && $z < 0)
        echo "Point lies in 8th octant\n";
}

// Driver Code
$x = 2;
$y = 3;
$z = 4;
octant($x, $y, $z) ;

$x = -4;
$y = 2;
$z = -8;
octant($x, $y, $z);

$x = -6;
$y = -2;
$z = 8;
octant($x, $y, $z);

// This code is contributed
// by Amber_Saxena.
?>
```

## java 描述语言

```
<script>

// Javascript program to print octant
// of a given point.

// Function to print octant
function octant( x,  y, z)
{
    if (x >= 0 && y >= 0 && z >= 0)
        document.write("Point lies in 1st octant"+"</br>");

    else if (x < 0 && y >= 0 && z >= 0)
        document.write( "Point lies in 2nd octant"+"</br>");

    else if (x < 0 && y < 0 && z >= 0)
        document.write("Point lies in 3rd octant"+"</br>");

    else if (x >= 0 && y < 0 && z >= 0)
        document.write("Point lies in 4th octant"+"</br>");

    else if (x >= 0 && y >= 0 && z < 0)
        document.write("Point lies in 5th octant"+"</br>");

    else if (x < 0 && y >= 0 && z < 0)
        document.write("Point lies in 6th octant"+"</br>");

    else if (x < 0 && y < 0 && z < 0)
        document.write("Point lies in 7th octant"+"</br>");

    else if (x >= 0 && y < 0 && z < 0)
        document.write("Point lies in 8th octant"+"</br>");
}

    // driver code 
    let x = 2, y = 3, z = 4;
    octant(x, y, z) ;

    x = -4, y = 2, z = -8;
    octant(x, y, z);

    x = -6, y = -2, z = 8;
    octant(x, y, z);

   // This code is contributed by jana_sayantan.
</script>
```

**Output:** 

```
Point lies in 1st octant
Point lies in 6th octant
Point lies in 3rd octant
```