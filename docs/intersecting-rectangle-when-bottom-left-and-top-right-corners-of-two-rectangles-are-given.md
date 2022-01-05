# 给定两个矩形的左下角和右上角时相交的矩形

> 原文:[https://www . geesforgeks . org/相交矩形-当给出两个矩形的左下角和右上角时/](https://www.geeksforgeeks.org/intersecting-rectangle-when-bottom-left-and-top-right-corners-of-two-rectangles-are-given/)

给定 4 个点的坐标，两个矩形的左下角和右上角。任务是找到由给定的两个矩形形成的相交矩形的坐标。

![](img/9a13f2f95d79b95e3abb9e1aaf8fe1b2.png)

**例:**

> **输入:**
> rec1:左下(0，0)，右上(10，8)
> rec 2:左下(2，3)，右上(7，9)
> **输出:** (2，3) (7，8) (2，8) (7，3)
> **输入:**
> rec1:左下(0，0)，右上(3，3)
> rec 2:左下(1，3)

**逼近:**
因为两个给定点是矩形的对角线。所以，x1 < x2，y1 < y2。同样 x3 < x4，y3 < y4。
所以，利用公式可以找到相交矩形的左下角点和右上角点。

```
x5 = max(x1, x3);
y5 = max(y1, y3);
x6 = min(x2, x4);
y6 = min(y2, y4);  
```

在没有交叉的情况下，x5 和 y5 总是会分别超过 x6 和 y5。矩形的另外两个点可以通过简单的几何图形找到。
以下是上述方法的实现:

## C++

```
// CPP program to find intersection
// rectangle of given two rectangles.
#include <bits/stdc++.h>
using namespace std;

// function to find intersection rectangle of given two rectangles.
void FindPoints(int x1, int y1, int x2, int y2,
                int x3, int y3, int x4, int y4)
{
    // gives bottom-left point
    // of intersection rectangle
    int x5 = max(x1, x3);
    int y5 = max(y1, y3);

    // gives top-right point
    // of intersection rectangle
    int x6 = min(x2, x4);
    int y6 = min(y2, y4);

    // no intersection
    if (x5 > x6 || y5 > y6) {
        cout << "No intersection";
        return;
    }

    cout << "(" << x5 << ", " << y5 << ") ";

    cout << "(" << x6 << ", " << y6 << ") ";

    // gives top-left point
    // of intersection rectangle
    int x7 = x5;
    int y7 = y6;

    cout << "(" << x7 << ", " << y7 << ") ";

    // gives bottom-right point
    // of intersection rectangle
    int x8 = x6;
    int y8 = y5;

    cout << "(" << x8 << ", " << y8 << ") ";
}

// Driver code
int main()
{
    // bottom-left and top-right
    // corners of first rectangle
    int x1 = 0, y1 = 0, x2 = 10, y2 = 8;

    // bottom-left and top-right
    // corners of first rectangle
    int x3 = 2, y3 = 3, x4 = 7, y4 = 9;

    // function call
    FindPoints(x1, y1, x2, y2, x3, y3, x4, y4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find intersection
// rectangle of given two rectangles.
class GFG
{

// function to find intersection
// rectangle of given two rectangles.
static void FindPoints(int x1, int y1,
                       int x2, int y2,
                       int x3, int y3,
                       int x4, int y4)
{
    // gives bottom-left point
    // of intersection rectangle
    int x5 = Math.max(x1, x3);
    int y5 = Math.max(y1, y3);

    // gives top-right point
    // of intersection rectangle
    int x6 = Math.min(x2, x4);
    int y6 = Math.min(y2, y4);

    // no intersection
    if (x5 > x6 || y5 > y6)
    {
        System.out.println("No intersection");
        return;
    }

    System.out.print("(" + x5 + ", " +
                           y5 + ") ");

    System.out.print("(" + x6 + ", " +
                           y6 + ") ");

    // gives top-left point
    // of intersection rectangle
    int x7 = x5;
    int y7 = y6;

    System.out.print("(" + x7 + ", " +
                           y7 + ") ");

    // gives bottom-right point
    // of intersection rectangle
    int x8 = x6;
    int y8 = y5;

    System.out.print("(" + x8 + ", " +
                           y8 + ") ");
}

// Driver code
public static void main(String args[])
{
    // bottom-left and top-right
    // corners of first rectangle
    int x1 = 0, y1 = 0,
        x2 = 10, y2 = 8;

    // bottom-left and top-right
    // corners of first rectangle
    int x3 = 2, y3 = 3,
        x4 = 7, y4 = 9;

    // function call
    FindPoints(x1, y1, x2, y2,
               x3, y3, x4, y4);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find intersection
# rectangle of given two rectangles.

# function to find intersection
# rectangle of given two rectangles.
def FindPoints(x1, y1, x2, y2,
               x3, y3, x4, y4):

    # gives bottom-left point
    # of intersection rectangle
    x5 = max(x1, x3)
    y5 = max(y1, y3)

    # gives top-right point
    # of intersection rectangle
    x6 = min(x2, x4)
    y6 = min(y2, y4)

    # no intersection
    if (x5 > x6 or y5 > y6) :
        print("No intersection")
        return

    print( "(", x5, ", ", y5, ") ", end = " ")

    print( "(", x6, ", ", y6, ") ", end = " ")

    # gives top-left point
    # of intersection rectangle
    x7 = x5
    y7 = y6

    print( "(", x7, ", ", y7, ") ", end = " ")

    # gives bottom-right point
    # of intersection rectangle
    x8 = x6
    y8 = y5

    print( "(", x8, ", ", y8, ") ")

# Driver code
if __name__ == "__main__":

    # bottom-left and top-right
    # corners of first rectangle
    x1 = 0
    y1 = 0
    x2 = 10
    y2 = 8

    # bottom-left and top-right
    # corners of first rectangle
    x3 = 2
    y3 = 3
    x4 = 7
    y4 = 9

    # function call
    FindPoints(x1, y1, x2, y2, x3, y3, x4, y4)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find intersection
// rectangle of given two rectangles.
using System;

class GFG
{

// function to find intersection
// rectangle of given two rectangles.
static void FindPoints(int x1, int y1,
                       int x2, int y2,
                       int x3, int y3,
                       int x4, int y4)
{
    // gives bottom-left point
    // of intersection rectangle
    int x5 = Math.Max(x1, x3);
    int y5 = Math.Max(y1, y3);

    // gives top-right point
    // of intersection rectangle
    int x6 = Math.Min(x2, x4);
    int y6 = Math.Min(y2, y4);

    // no intersection
    if (x5 > x6 || y5 > y6)
    {
        Console.WriteLine("No intersection");
        return;
    }

    Console.Write("(" + x5 + ", " +
                        y5 + ") ");

    Console.Write("(" + x6 + ", " +
                        y6 + ") ");

    // gives top-left point
    // of intersection rectangle
    int x7 = x5;
    int y7 = y6;

    Console.Write("(" + x7 + ", " +
                        y7 + ") ");

    // gives bottom-right point
    // of intersection rectangle
    int x8 = x6;
    int y8 = y5;

    Console.Write("(" + x8 + ", " +
                        y8 + ") ");
}

// Driver code
public static void Main()
{
    // bottom-left and top-right
    // corners of first rectangle
    int x1 = 0, y1 = 0,
        x2 = 10, y2 = 8;

    // bottom-left and top-right
    // corners of first rectangle
    int x3 = 2, y3 = 3,
        x4 = 7, y4 = 9;

    // function call
    FindPoints(x1, y1, x2, y2,
               x3, y3, x4, y4);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find intersection
// rectangle of given two rectangles.

// function to find intersection rectangle
// of given two rectangles.
function FindPoints($x1, $y1, $x2, $y2,
                    $x3, $y3, $x4, $y4)
{
    // gives bottom-left point
    // of intersection rectangle
    $x5 = max($x1, $x3);
    $y5 = max($y1, $y3);

    // gives top-right point
    // of intersection rectangle
    $x6 = min($x2, $x4);
    $y6 = min($y2, $y4);

    // no intersection
    if ($x5 > $x6 || $y5 > $y6)
    {
        echo "No intersection";
        return;
    }

    echo "(" . $x5 . ", " . $y5 . ") ";

    echo "(" . $x6 . ", " . $y6 . ") ";

    // gives top-left point
    // of intersection rectangle
    $x7 = $x5;
    $y7 = $y6;

    echo "(" . $x7 . ", " . $y7 . ") ";

    // gives bottom-right point
    // of intersection rectangle
    $x8 = $x6;
    $y8 = $y5;

    echo "(" . $x8 . ", " . $y8 . ") ";
}

// Driver code

// bottom-left and top-right
// corners of first rectangle
$x1 = 0; $y1 = 0; $x2 = 10; $y2 = 8;

// bottom-left and top-right
// corners of first rectangle
$x3 = 2; $y3 = 3; $x4 = 7; $y4 = 9;

// function call
FindPoints($x1, $y1, $x2, $y2,
           $x3, $y3, $x4, $y4);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find intersection
// rectangle of given two rectangles.

// Function to find intersection
// rectangle of given two rectangles.
function FindPoints(x1, y1, x2, y2,
                    x3, y3, x4, y4)
{

    // Gives bottom-left point
    // of intersection rectangle
    var x5 = Math.max(x1, x3);
    var y5 = Math.max(y1, y3);

    // Gives top-right point
    // of intersection rectangle
    var x6 = Math.min(x2, x4);
    var y6 = Math.min(y2, y4);

    // No intersection
    if (x5 > x6 || y5 > y6)
    {
        document.write("No intersection");
        return;
    }
    document.write("(" + x5 + ", " +
                         y5 + ") ");

    document.write("(" + x6 + ", " +
                         y6 + ") ");

    // Gives top-left point
    // of intersection rectangle
    var x7 = x5;
    var y7 = y6;

    document.write("(" + x7 + ", " +
                         y7 + ") ");

    // Gives bottom-right point
    // of intersection rectangle
    var x8 = x6;
    var y8 = y5;

    document.write("(" + x8 + ", " +
                         y8 + ") ");
}

// Driver Code

// bottom-left and top-right
// corners of first rectangle
var x1 = 0, y1 = 0,
    x2 = 10, y2 = 8;

// bottom-left and top-right
// corners of first rectangle
var x3 = 2, y3 = 3,
    x4 = 7, y4 = 9;

// Function call
FindPoints(x1, y1, x2, y2,
           x3, y3, x4, y4);

// This code is contributed by kirti

</script>
```

**Output:** 

```
(2, 3) (7, 8) (2, 8) (7, 3)
```

**时间复杂度:** O(1)

**辅助空间:** O(1)