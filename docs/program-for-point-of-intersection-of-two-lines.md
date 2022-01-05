# 两条直线交点程序

> 原文:[https://www . geeksforgeeks . org/双线交点程序/](https://www.geeksforgeeks.org/program-for-point-of-intersection-of-two-lines/)

给定 AB 线对应的 A 点和 B 点，PQ 线对应的 P 点和 Q 点，求这些线的交点。这些点在 2D 平面上给出了它们的 X 和 Y 坐标。

示例:

```
Input : A = (1, 1), B = (4, 4)
        C = (1, 8), D = (2, 4)
Output : The intersection of the given lines 
         AB and CD is: (2.4, 2.4)

Input : A = (0, 1), B = (0, 4)
        C = (1, 8), D = (1, 4)
Output : The given lines AB and CD are parallel.

```

首先假设我们有两点(x <sub>1</sub> ，y <sub>1</sub> )和(x <sub>2</sub> ，y <sub>2</sub> )。现在，我们找到这些点形成的线的方程。

假设给定的行是:

1.  a<sub>1</sub>x+b<sub>1</sub>y = c<sub>1</sub>
2.  a<sub>2</sub>x+b<sub>2</sub>y = c<sub>2</sub>

我们现在必须解这两个方程来找到交点。为了求解，我们乘以 1。由 b <sub>2</sub> 和 2 由 b<sub>1</sub>T4【这就给了我们，
a<sub>1</sub>b<sub>2</sub>x+b<sub>1</sub>b<sub>2</sub>y = c<sub>1</sub>b<sub>2</sub>T18】a<sub>2</sub>b<sub>1</sub>x+b<sub>2</sub>b

减去这些我们得到，
(a<sub>1</sub>b<sub>2</sub>–a<sub>2</sub>b<sub>1</sub>)x = c<sub>1</sub>b<sub>2</sub>–c<sub>2</sub>b<sub>1</sub>

这就给了我们 x 的值，同样，我们可以找到 y 的值(x，y)给了我们交点。

**注意:**这给出了两条线的交点，但是如果给我们的是线段而不是直线，我们还必须重新检查如此计算的点实际上位于两条线段上。
如果线段由点(x <sub>1</sub> 、y <sub>1</sub> )和(x <sub>2</sub> 、y <sub>2</sub> 指定，那么为了检查(x，y)是否在线段上，我们只需检查

*   min (x <sub>1</sub> ，x<sub>2</sub>)<= x<= max(x<sub>1</sub>，x <sub>2</sub>
*   min (y <sub>1</sub> ，y<sub>2</sub>)<= y<= max(y<sub>1</sub>，y <sub>2</sub>

上述实现的伪代码:

```
determinant = a1 b2 - a2 b1
if (determinant == 0)
{
    // Lines are parallel
}
else
{
    x = (c1b2 - c2b1)/determinant
    y = (a1c2 - a2c1)/determinant
}

```

这些可以通过首先直接获得斜率，然后找到直线的截距来导出。

## C++

```
// C++ Implementation. To find the point of
// intersection of two lines
#include <bits/stdc++.h>
using namespace std;

// This pair is used to store the X and Y
// coordinates of a point respectively
#define pdd pair<double, double>

// Function used to display X and Y coordinates
// of a point
void displayPoint(pdd P)
{
    cout << "(" << P.first << ", " << P.second
         << ")" << endl;
}

pdd lineLineIntersection(pdd A, pdd B, pdd C, pdd D)
{
    // Line AB represented as a1x + b1y = c1
    double a1 = B.second - A.second;
    double b1 = A.first - B.first;
    double c1 = a1*(A.first) + b1*(A.second);

    // Line CD represented as a2x + b2y = c2
    double a2 = D.second - C.second;
    double b2 = C.first - D.first;
    double c2 = a2*(C.first)+ b2*(C.second);

    double determinant = a1*b2 - a2*b1;

    if (determinant == 0)
    {
        // The lines are parallel. This is simplified
        // by returning a pair of FLT_MAX
        return make_pair(FLT_MAX, FLT_MAX);
    }
    else
    {
        double x = (b2*c1 - b1*c2)/determinant;
        double y = (a1*c2 - a2*c1)/determinant;
        return make_pair(x, y);
    }
}

// Driver code
int main()
{
    pdd A = make_pair(1, 1);
    pdd B = make_pair(4, 4);
    pdd C = make_pair(1, 8);
    pdd D = make_pair(2, 4);

    pdd intersection = lineLineIntersection(A, B, C, D);

    if (intersection.first == FLT_MAX &&
        intersection.second==FLT_MAX)
    {
        cout << "The given lines AB and CD are parallel.\n";
    }

    else
    {
        // NOTE: Further check can be applied in case
        // of line segments. Here, we have considered AB
        // and CD as lines
        cout << "The intersection of the given lines AB "
                "and CD is: ";
        displayPoint(intersection);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation. To find the point of
// intersection of two lines

// Class used to  used to store the X and Y
// coordinates of a point respectively
class Point
{
    double x,y;

    public Point(double x, double y) 
    {
        this.x = x;
        this.y = y;
    }

    // Method used to display X and Y coordinates
    // of a point
    static void displayPoint(Point p)
    {
        System.out.println("(" + p.x + ", " + p.y + ")");
    }
}

class Test
{     
    static Point lineLineIntersection(Point A, Point B, Point C, Point D)
    {
        // Line AB represented as a1x + b1y = c1
        double a1 = B.y - A.y;
        double b1 = A.x - B.x;
        double c1 = a1*(A.x) + b1*(A.y);

        // Line CD represented as a2x + b2y = c2
        double a2 = D.y - C.y;
        double b2 = C.x - D.x;
        double c2 = a2*(C.x)+ b2*(C.y);

        double determinant = a1*b2 - a2*b1;

        if (determinant == 0)
        {
            // The lines are parallel. This is simplified
            // by returning a pair of FLT_MAX
            return new Point(Double.MAX_VALUE, Double.MAX_VALUE);
        }
        else
        {
            double x = (b2*c1 - b1*c2)/determinant;
            double y = (a1*c2 - a2*c1)/determinant;
            return new Point(x, y);
        }
    }

    // Driver method
    public static void main(String args[])
    {
        Point A = new Point(1, 1);
        Point B = new Point(4, 4);
        Point C = new Point(1, 8);
        Point D = new Point(2, 4);

        Point intersection = lineLineIntersection(A, B, C, D);

        if (intersection.x == Double.MAX_VALUE &&
            intersection.y == Double.MAX_VALUE)
        {
            System.out.println("The given lines AB and CD are parallel.");
        }

        else
        {
            // NOTE: Further check can be applied in case
            // of line segments. Here, we have considered AB
            // and CD as lines
           System.out.print("The intersection of the given lines AB " + 
                               "and CD is: ");
           Point.displayPoint(intersection);
        }
    }
}
```

## C#

```
using System;

// C# Implementation. To find the point of 
// intersection of two lines 

// Class used to  used to store the X and Y 
// coordinates of a point respectively 
public class Point
{
    public double x, y;

    public Point(double x, double y)
    {
        this.x = x;
        this.y = y;
    }

    // Method used to display X and Y coordinates 
    // of a point 
    public static void displayPoint(Point p)
    {
        Console.WriteLine("(" + p.x + ", " + p.y + ")");
    }
}

public class Test
{
    public static Point lineLineIntersection(Point A, Point B, Point C, Point D)
    {
        // Line AB represented as a1x + b1y = c1 
        double a1 = B.y - A.y;
        double b1 = A.x - B.x;
        double c1 = a1 * (A.x) + b1 * (A.y);

        // Line CD represented as a2x + b2y = c2 
        double a2 = D.y - C.y;
        double b2 = C.x - D.x;
        double c2 = a2 * (C.x) + b2 * (C.y);

        double determinant = a1 * b2 - a2 * b1;

        if (determinant == 0)
        {
            // The lines are parallel. This is simplified 
            // by returning a pair of FLT_MAX 
            return new Point(double.MaxValue, double.MaxValue);
        }
        else
        {
            double x = (b2 * c1 - b1 * c2) / determinant;
            double y = (a1 * c2 - a2 * c1) / determinant;
            return new Point(x, y);
        }
    }

    // Driver method 
    public static void Main(string[] args)
    {
        Point A = new Point(1, 1);
        Point B = new Point(4, 4);
        Point C = new Point(1, 8);
        Point D = new Point(2, 4);

        Point intersection = lineLineIntersection(A, B, C, D);

        if (intersection.x == double.MaxValue && intersection.y == double.MaxValue)
        {
            Console.WriteLine("The given lines AB and CD are parallel.");
        }

        else
        {
            // NOTE: Further check can be applied in case 
            // of line segments. Here, we have considered AB 
            // and CD as lines 
           Console.Write("The intersection of the given lines AB " + "and CD is: ");
           Point.displayPoint(intersection);
        }
    }
}

  // This code is contributed by Shrikant13
```

**Output:**

```
The intersection of the given lines AB and 
CD is: (2.4, 2.4)

```

本文由**安雅金达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。