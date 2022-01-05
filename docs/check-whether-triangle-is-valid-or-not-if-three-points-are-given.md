# 给三个点检查三角形是否有效

> 原文:[https://www . geesforgeks . org/check-如果给出三个点，三角形是否有效/](https://www.geeksforgeeks.org/check-whether-triangle-is-valid-or-not-if-three-points-are-given/)

给定一个平面内三个点的坐标**P1****P2**和 **P3** ，任务是检查三个点是否形成三角形
**示例:**

> **输入:** P1 = (1，5)，P2 = (2，5)，P3 = (4，6)
> **输出:**是
> T6】输入: P1 = (1，1)，P2 = (1，4)，P3 = (1，5)
> T9】输出:否

**逼近:**问题中的关键观察点是三个点不在直线上时才形成三角形，也就是这三个点的三角形不等于零形成的面积。
![\text{Area of Triangle }= \frac{1}{2}*(x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2))   ](img/346b4cdc845c73d06f019a049379a591.png "Rendered by QuickLaTeX.com")
以上公式来源于[鞋带公式](https://www.geeksforgeeks.org/area-of-a-polygon-with-given-n-ordered-vertices/)。
所以我们来检查三角形形成的面积是否为零。
以下是上述方法的实施:

## C++

```
// C++ implementation to check
// if three points form a triangle

#include <bits/stdc++.h>
using namespace std;

// Function to check if three
// points make a triangle
void checkTriangle(int x1, int y1, int x2,
                   int y2, int x3, int y3)
{

    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    int a = x1 * (y2 - y3)
            + x2 * (y3 - y1)
            + x3 * (y1 - y2);

    // Condition to check if
    // area is not equal to 0
    if (a == 0)
        cout << "No";
    else
        cout << "Yes";
}

// Driver Code
int main()
{
    int x1 = 1, x2 = 2, x3 = 3,
        y1 = 1, y2 = 2, y3 = 3;
    checkTriangle(x1, y1, x2,
                  y2, x3, y3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if three points form a triangle
import java.io.*;
import java.util.*;

class GFG {

// Function to check if three
// points make a triangle
static void checkTriangle(int x1, int y1,
                          int x2, int y2,
                          int x3, int y3)
{

    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    int a = x1 * (y2 - y3) +
            x2 * (y3 - y1) +
            x3 * (y1 - y2);

    // Condition to check if
    // area is not equal to 0
    if (a == 0)
        System.out.println("No");
    else
        System.out.println("Yes");
}

// Driver code
public static void main(String[] args)
{
    int x1 = 1, y1 = 1,
        x2 = 2, y2 = 2,
        x3 = 3, y3 = 3;
    checkTriangle(x1, y1, x2, y2, x3, y3);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation to check
# if three points form a triangle

# Function to check if three
# points make a triangle
def checkTriangle(x1, y1, x2, y2, x3, y3):

    # Calculation the area of
    # triangle. We have skipped
    # multiplication with 0.5
    # to avoid floating point
    # computations
    a = (x1 * (y2 - y3) +
         x2 * (y3 - y1) +
         x3 * (y1 - y2))

    # Condition to check if
    # area is not equal to 0
    if a == 0:
        print('No')
    else:
        print('Yes')

# Driver code
if __name__=='__main__':

    (x1, x2, x3) = (1, 2, 3)
    (y1, y2, y3) = (1, 2, 3)

    checkTriangle(x1, y1, x2, y2, x3, y3)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to check
// if three points form a triangle
using System;

class GFG {

// Function to check if three
// points make a triangle
static void checkTriangle(int x1, int y1,
                          int x2, int y2,
                          int x3, int y3)
{
    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    int a = x1 * (y2 - y3) +
            x2 * (y3 - y1) +
            x3 * (y1 - y2);

    // Condition to check if
    // area is not equal to 0
    if (a == 0)
        Console.WriteLine("No");
    else
        Console.WriteLine("Yes");
}

// Driver code
public static void Main()
{
    int x1 = 1, y1 = 1,
        x2 = 2, y2 = 2,
        x3 = 3, y3 = 3;

    checkTriangle(x1, y1, x2, y2, x3, y3);
}
}

//This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>
// Javascript implementation to check
// if three points form a triangle

// Function to check if three
// points make a triangle
function checkTriangle(x1, y1, x2,
                y2, x3, y3)
{

    // Calculation the area of
    // triangle. We have skipped
    // multiplication with 0.5
    // to avoid floating point
    // computations
    let a = x1 * (y2 - y3)
            + x2 * (y3 - y1)
            + x3 * (y1 - y2);

    // Condition to check if
    // area is not equal to 0
    if (a == 0)
        document.write("No");
    else
        document.write("Yes");
}

// Driver Code
    let x1 = 1, x2 = 2, x3 = 3,
        y1 = 1, y2 = 2, y3 = 3;
    checkTriangle(x1, y1, x2,
                y2, x3, y3);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
No
```