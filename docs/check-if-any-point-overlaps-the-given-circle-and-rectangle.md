# 检查是否有任何点与给定的圆形和矩形重叠

> 原文:[https://www . geeksforgeeks . org/check-如果任意点与给定的圆形和矩形重叠/](https://www.geeksforgeeks.org/check-if-any-point-overlaps-the-given-circle-and-rectangle/)

给定矩形 **(X1，Y1)、(X2，Y2)** 的两个相对的**对角点**和圆的中心，半径 **R，(Xc，Yc)** ，任务是检查是否存在既属于圆又属于矩形的点 **P** 。
**举例:**

> **输入:** R = 2，Xc = 0，Yc = 0，X1 = 1，Y1 = 0，X2 = 3，Y2 = 3
> **输出:**真
> **解释:**
> 很明显，从下图来看，圆和矩形相交。
> 
> ![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200507140414/Circle-Page-3-1.png)
> 
> **输入:** R = 1，Xc = 1，Yc = 1，X1 = 3，Y1 = 3，X2 = 5，Y2 = 6
> T3】输出:假

**做法:**思路就是简单检查一下圆和矩形是否相交。当交叉发生时，基本上有两种可能的情况。

1.  **情况 1:** 矩形的边与圆接触或相交。为了检查形状是否相交，我们需要在矩形上或矩形内找到一个最靠近圆心的点。如果该点位于圆上或圆内，则保证两个形状相交。让最近的点用 **(Xn，Yn)** 表示。然后使用**sqrt((Xc-Xn)<sup>2</sup>+(Yc-Yn)<sup>2</sup>)**可以找到最近点与圆心的距离。如果该距离≤圆的半径，则两个形状相交。
2.  **情况 2:** 圆心位于矩形内。由于圆心位于矩形内，最近的点将是(Xc，Yc)。

仔细观察，可以观察到感兴趣点仅取决于(X1，Y1)和(X2，Y2)相对于(Xc，Yc)的位置。因此，上述两种情况下的最近点可以计算为:

1.  Xn=最大值(X1，最小值(Xc，X2))
2.  Yn= max（Y1， min（Yc， Y2））

以下是上述方法的实现:

## C++

```
// C++ implementation to check if any
// point overlaps the given circle
// and rectangle
#include<bits/stdc++.h>
using namespace std;

// Function to check if any point
// overlaps the given circle
// and rectangle
bool checkOverlap(int R, int Xc, int Yc,
                         int X1, int Y1,
                         int X2, int Y2)
{

    // Find the nearest point on the
    // rectangle to the center of
    // the circle
    int Xn = max(X1, min(Xc, X2));
    int Yn = max(Y1, min(Yc, Y2));

    // Find the distance between the
    // nearest point and the center
    // of the circle
    // Distance between 2 points,
    // (x1, y1) & (x2, y2) in
    // 2D Euclidean space is
    // ((x1-x2)**2 + (y1-y2)**2)**0.5
    int Dx = Xn - Xc;
    int Dy = Yn - Yc;
    return (Dx * Dx + Dy * Dy) <= R * R;
}

// Driver code
int main()
{
    int R = 1;
    int Xc = 0, Yc = 0;
    int X1 = 1, Y1 = -1;
    int X2 = 3, Y2 = 1;

    if(checkOverlap(R, Xc, Yc,
                       X1, Y1,
                       X2, Y2))
    {
        cout << "True" << endl;
    }
    else
    {
        cout << "False";
    }
}

// This code is contributed by BhupendraSingh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if any
// point overlaps the given circle
// and rectangle
class GFG{

// Function to check if any point
// overlaps the given circle
// and rectangle
static boolean checkOverlap(int R, int Xc, int Yc,
                                   int X1, int Y1,
                                   int X2, int Y2)
{

    // Find the nearest point on the
    // rectangle to the center of
    // the circle
    int Xn = Math.max(X1, Math.min(Xc, X2));
    int Yn = Math.max(Y1, Math.min(Yc, Y2));

    // Find the distance between the
    // nearest point and the center
    // of the circle
    // Distance between 2 points,
    // (x1, y1) & (x2, y2) in
    // 2D Euclidean space is
    // ((x1-x2)**2 + (y1-y2)**2)**0.5
    int Dx = Xn - Xc;
    int Dy = Yn - Yc;
    return (Dx * Dx + Dy * Dy) <= R * R;
}

// Driver code
public static void main(String[] args)
{
    int R = 1;
    int Xc = 0, Yc = 0;
    int X1 = 1, Y1 = -1;
    int X2 = 3, Y2 = 1;

    if(checkOverlap(R, Xc, Yc,
                       X1, Y1,
                       X2, Y2))
    {
        System.out.print("True" + "\n");
    }
    else
    {
        System.out.print("False");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to check if any
# point overlaps the given Circle
# and Rectangle

# Function to check if any point
# overlaps the given Circle
# and Rectangle
def checkOverlap(R, Xc, Yc, X1, Y1, X2, Y2):

    # Find the nearest point on the
    # rectangle to the center of
    # the circle
    Xn = max(X1, min(Xc, X2))
    Yn = max(Y1, min(Yc, Y2))

    # Find the distance between the
    # nearest point and the center
    # of the circle
    # Distance between 2 points,
    # (x1, y1) & (x2, y2) in
    # 2D Euclidean space is
    # ((x1-x2)**2 + (y1-y2)**2)**0.5
    Dx = Xn - Xc
    Dy = Yn - Yc
    return (Dx**2 + Dy**2) <= R**2

# Driver code
if(__name__ == "__main__"):
    R = 1
    Xc, Yc = 0, 0
    X1, Y1 = 1, -1
    X2, Y2 = 3, 1

    print(checkOverlap(R, Xc, Yc, X1, Y1, X2, Y2))
```

## C#

```
// C# implementation to check if any
// point overlaps the given circle
// and rectangle
using System;
class GFG{

// Function to check if any point
// overlaps the given circle
// and rectangle
static bool checkOverlap(int R, int Xc, int Yc,
                                int X1, int Y1,
                                int X2, int Y2)
{

    // Find the nearest point on the
    // rectangle to the center of
    // the circle
    int Xn = Math.Max(X1,
             Math.Min(Xc, X2));
    int Yn = Math.Max(Y1,
             Math.Min(Yc, Y2));

    // Find the distance between the
    // nearest point and the center
    // of the circle
    // Distance between 2 points,
    // (x1, y1) & (x2, y2) in
    // 2D Euclidean space is
    // ((x1-x2)**2 + (y1-y2)**2)**0.5
    int Dx = Xn - Xc;
    int Dy = Yn - Yc;
    return (Dx * Dx + Dy * Dy) <= R * R;
}

// Driver code
public static void Main()
{
    int R = 1;
    int Xc = 0, Yc = 0;
    int X1 = 1, Y1 = -1;
    int X2 = 3, Y2 = 1;

    if(checkOverlap(R, Xc, Yc,
                       X1, Y1,
                       X2, Y2))
    {
        Console.Write("True" + "\n");
    }
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript implementation to check if any
// point overlaps the given circle
// and rectangle

// Function to check if any point
// overlaps the given circle
// and rectangle
function checkOverlap(R, Xc, Yc, X1, Y1, X2, Y2)
{

    // Find the nearest point on the
    // rectangle to the center of
    // the circle
    let Xn = Math.max(X1, Math.min(Xc, X2));
    let Yn = Math.max(Y1, Math.min(Yc, Y2));

    // Find the distance between the
    // nearest point and the center
    // of the circle
    // Distance between 2 points,
    // (x1, y1) & (x2, y2) in
    // 2D Euclidean space is
    // ((x1-x2)**2 + (y1-y2)**2)**0.5
    let Dx = Xn - Xc;
    let Dy = Yn - Yc;
    return (Dx * Dx + Dy * Dy) <= R * R;
}

// Driver Code

    let R = 1;
    let Xc = 0, Yc = 0;
    let X1 = 1, Y1 = -1;
    let X2 = 3, Y2 = 1;

    if(checkOverlap(R, Xc, Yc,
                       X1, Y1,
                       X2, Y2))
    {
        document.write("True" + "\n");
    }
    else
    {
        document.write("False");
    }

</script>
```

**Output:** 

```
True
```

时间复杂度:0(1)

辅助空间:0(1)