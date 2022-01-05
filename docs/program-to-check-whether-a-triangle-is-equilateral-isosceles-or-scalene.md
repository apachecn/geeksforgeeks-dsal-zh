# 检查三角形是等边三角形、等腰三角形还是不等边三角形的程序

> 原文:[https://www . geesforgeks . org/program-to-check-a-三角形是等边等腰三角形还是不等边三角形/](https://www.geeksforgeeks.org/program-to-check-whether-a-triangle-is-equilateral-isosceles-or-scalene/)

给定代表三角形三条边的 **X** 、 **Y** 、 **Z** 三个整数，任务是检查给定边形成的三角形是[等边](https://en.wikipedia.org/wiki/Equilateral_triangle)、[等腰](https://en.wikipedia.org/wiki/Isosceles_triangle)还是[不等边](https://en.wikipedia.org/wiki/Scalene)。

> **等边三角形:**如果一个三角形的所有边都相等，那么这个三角形就是等边三角形。如果 X，Y，Z 是三角形的三条边。那么，只有当 X = Y = Z 时，三角形才是等边的。
> 
> **等腰三角形:**如果一个三角形的任意两条边相等，则称它为等腰三角形。如果 X，Y，Z 是三角形的三条边。那么，如果 X = Y 或 X = Z 或 Y = Z，三角形就是等腰三角形。
> 
> **不等边三角形:**一个三角形如果没有一条边是相等的，则称之为不等边三角形。

**示例:**

> **输入:** X = 6，Y = 8，Z = 10
> **输出:**不等边三角形
> **解释:**
> 由于给定三角形的所有边都是不等边的，所以三角形是不等边的。
> 
> **输入:** X = 10，Y = 10，Z = 10
> **输出:**等边三角形
> **解释:**
> 因为给定三角形的所有边都相等。

**方法:**按照以下步骤解决问题:

1.  检查 **X = Y** 和 **Y = Z** 是否一致。如果发现是真的，打印“等边三角形”。
2.  如果不是等边三角形，则检查 **X = Y** 或 **X = Z** 或 **Y = Z** 。如果发现是真的，打印“等腰三角形”。
3.  如果以上步骤都不满足，则打印“不等边三角形”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the triangle
// is equilateral or isosceles or scalene
void checkTriangle(int x, int y, int z)
{

    // Check for equilateral triangle
    if (x == y && y == z)
        cout << "Equilateral Triangle";

    // Check for isosceles triangle
    else if (x == y || y == z || z == x)
        cout << "Isosceles Triangle";

    // Otherwise scalene triangle
    else
        cout << "Scalene Triangle";
}

// Driver Code
int main()
{

    // Given sides of triangle
    int x = 8, y = 7, z = 9;

    // Function call
    checkTriangle(x, y, z);
}

// This code is contributed by jana_sayantan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the triangle
// is equilateral or isosceles or scalene
static void checkTriangle(int x, int y, int z)
{

    // Check for equilateral triangle
    if (x == y && y == z )
        System.out.println("Equilateral Triangle");

    // Check for isosceles triangle
    else if (x == y || y == z || z == x )
        System.out.println("Isosceles Triangle");

    // Otherwise scalene triangle
    else
        System.out.println("Scalene Triangle");
}

// Driver Code
public static void main(String[] args)
{

    // Given sides of triangle
    int x = 8, y = 7, z = 9;

    // Function call
    checkTriangle(x, y, z);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the triangle
# is equilateral or isosceles or scalene
def checkTriangle(x, y, z):

    # _Check for equilateral triangle
    if x == y == z:
        print("Equilateral Triangle")

    # Check for isosceles triangle
    elif x == y or y == z or z == x:
        print("Isosceles Triangle")

    # Otherwise scalene triangle
    else:
        print("Scalene Triangle")

# Driver Code

# Given sides of triangle
x = 8
y = 7
z = 9

# Function Call
checkTriangle(x, y, z)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the triangle
// is equilateral or isosceles or scalene
static void checkTriangle(int x, int y, int z)
{

    // Check for equilateral triangle
    if (x == y && y == z )
        Console.WriteLine("Equilateral Triangle");

    // Check for isosceles triangle
    else if (x == y || y == z || z == x )
        Console.WriteLine("Isosceles Triangle");

    // Otherwise scalene triangle
    else
        Console.WriteLine("Scalene Triangle");
}

// Driver Code
public static void Main()
{

    // Given sides of triangle
    int x = 8, y = 7, z = 9;

    // Function call
    checkTriangle(x, y, z);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// JavaScript program for the above approach 

// Function to check if the triangle
// is equilateral or isosceles or scalene
function checkTriangle(x, y, z)
{

    // Check for equilateral triangle
    if (x == y && y == z)
        document.write("Equilateral Triangle");

    // Check for isosceles triangle
    else if (x == y || y == z || z == x)
        document.write("Isosceles Triangle");

    // Otherwise scalene triangle
    else
        document.write("Scalene Triangle");
}

// Driver Code

    // Given sides of triangle
    let x = 8, y = 7, z = 9;

    // Function call
    checkTriangle(x, y, z);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Scalene Triangle
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)