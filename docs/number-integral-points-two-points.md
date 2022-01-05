# 两点间积分点数

> 原文:[https://www . geesforgeks . org/number-integral-points-two-points/](https://www.geeksforgeeks.org/number-integral-points-two-points/)

给定两点 **p** (x1，y1)和 **q** (x2，y2)，计算位于连接它们的线上的积分点数。
**例:**如果点数为(0，2)和(4，0)，那么其上的积分点数只有一个，即(2，1)。
同样，如果点是(1，9)和(8，16)，则位于其上的积分点是 6，它们是(2，10)、(3，11)、(4，12)、(5，13)、(6，14)和(7，15)。

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/count-integral-points5445/1)

 **从任意给定点开始，使用循环到达另一个终点。对于循环中的每个点，检查它是否位于连接给定两点的线上。如果是，则将计数增加 1。该方法的时间复杂度为 0(最小值(x2-x1，y2-y1))。

**最优进场****

```
1\. If the edge formed by joining **p** and **q** is parallel 
   to the X-axis, then the number of integral points 
   between the vertices is : 
        abs(p.y - q.y)-1

2\. Similarly if edge is parallel to the Y-axis, then 
   the number of integral points in between is :
    abs(p.x - q.x)-1

3\. Else, we can find the integral points between the
   vertices using below formula:
     GCD(abs(p.x - q.x), abs(p.y - q.y)) - 1
```

****GCD 公式是如何工作的？**
思路是用最简单的形式求直线的方程，即在方程 ax + by +c 中，系数 a、b、c 成为同素。我们可以通过计算 a、b 和 c 的 GCD(最大公约数)来实现，并以最简单的形式转换 a、b 和 c。
那么，答案就是(y 坐标差)除以(a)–1。这是因为在计算 ax + by + c = 0 之后，对于不同的 y 值，x 将是可以被 a 整除的 y 值的个数。
下面是上述思想的实现。** 

## **C++**

```
// C++ code to find the number of integral points
// lying on the line joining the two given points
#include <iostream>
#include <cmath>
using namespace std;

// Class to represent an Integral point on XY plane.
class Point
{
public:
    int x, y;
    Point(int a=0, int b=0):x(a),y(b) {}
};

// Utility function to find GCD of two numbers
// GCD of a and b
int gcd(int a, int b)
{
    if (b == 0)
       return a;
    return gcd(b, a%b);
}

// Finds the no. of Integral points between
// two given points.
int getCount(Point p, Point q)
{
    // If line joining p and q is parallel to
    // x axis, then count is difference of y
    // values
    if (p.x==q.x)
        return abs(p.y - q.y) - 1;

    // If line joining p and q is parallel to
    // y axis, then count is difference of x
    // values
    if (p.y == q.y)
        return abs(p.x-q.x) - 1;

    return gcd(abs(p.x-q.x), abs(p.y-q.y))-1;
}

// Driver program to test above
int main()
{
    Point p(1, 9);
    Point q(8, 16);

    cout << "The number of integral points between "
         << "(" << p.x << ", " << p.y << ") and ("
         << q.x << ", " << q.y << ") is "
         << getCount(p, q);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to find the number of integral points
// lying on the line joining the two given points

class GFG
{

// Class to represent an Integral point on XY plane.
static class Point
{
    int x, y;
    Point(int a, int b)
    {
        this.x = a;
        this.y = b;
    }
};

// Utility function to find GCD of two numbers
// GCD of a and b
static int gcd(int a, int b)
{
    if (b == 0)
    return a;
    return gcd(b, a % b);
}

// Finds the no. of Integral points between
// two given points.
static int getCount(Point p, Point q)
{
    // If line joining p and q is parallel to
    // x axis, then count is difference of y
    // values
    if (p.x == q.x)
        return Math.abs(p.y - q.y) - 1;

    // If line joining p and q is parallel to
    // y axis, then count is difference of x
    // values
    if (p.y == q.y)
        return Math.abs(p.x - q.x) - 1;

    return gcd(Math.abs(p.x - q.x), Math.abs(p.y - q.y)) - 1;
}

// Driver program to test above
public static void main(String[] args)
{
    Point p = new Point(1, 9);
    Point q = new Point(8, 16);

    System.out.println("The number of integral points between "
        + "(" + p.x + ", " + p.y + ") and ("
        + q.x + ", " + q.y + ") is "
        + getCount(p, q));
}
}

// This code contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 code to find the number of
# integral points lying on the line
# joining the two given points

# Class to represent an Integral point
# on XY plane.
class Point:

    def __init__(self, a, b):
        self.x = a
        self.y = b

# Utility function to find GCD
# of two numbers GCD of a and b
def gcd(a, b):

    if b == 0:
        return a
    return gcd(b, a % b)

# Finds the no. of Integral points
# between two given points.
def getCount(p, q):

    # If line joining p and q is parallel
    # to x axis, then count is difference
    # of y values
    if p.x == q.x:
        return abs(p.y - q.y) - 1

    # If line joining p and q is parallel
    # to y axis, then count is difference
    # of x values
    if p.y == q.y:
        return abs(p.x - q.x) - 1

    return gcd(abs(p.x - q.x),
               abs(p.y - q.y)) - 1

# Driver Code
if __name__ == "__main__":

    p = Point(1, 9)
    q = Point(8, 16)

    print("The number of integral points",
          "between ({}, {}) and ({}, {}) is {}" .
           format(p.x, p.y, q.x, q.y, getCount(p, q)))

# This code is contributed by Rituraj Jain
```

## **C#**

```
// C# code to find the number of integral points
// lying on the line joining the two given points
using System;

class GFG
{

// Class to represent an Integral point on XY plane.
public class Point
{
    public int x, y;
    public Point(int a, int b)
    {
        this.x = a;
        this.y = b;
    }
};

// Utility function to find GCD of two numbers
// GCD of a and b
static int gcd(int a, int b)
{
    if (b == 0)
    return a;
    return gcd(b, a % b);
}

// Finds the no. of Integral points between
// two given points.
static int getCount(Point p, Point q)
{
    // If line joining p and q is parallel to
    // x axis, then count is difference of y
    // values
    if (p.x == q.x)
        return Math.Abs(p.y - q.y) - 1;

    // If line joining p and q is parallel to
    // y axis, then count is difference of x
    // values
    if (p.y == q.y)
        return Math.Abs(p.x - q.x) - 1;

    return gcd(Math.Abs(p.x - q.x), Math.Abs(p.y - q.y)) - 1;
}

// Driver code
public static void Main(String[] args)
{
    Point p = new Point(1, 9);
    Point q = new Point(8, 16);

    Console.WriteLine("The number of integral points between "
        + "(" + p.x + ", " + p.y + ") and ("
        + q.x + ", " + q.y + ") is "
        + getCount(p, q));
}
}

/* This code contributed by PrinciRaj1992 */
```

## **java 描述语言**

```
<script>
// javascript code to find the number of integral points
// lying on the line joining the two given points
    // Class to represent an Integral point on XY plane.
     class Point {

        constructor(a , b) {
            this.x = a;
            this.y = b;
        }
    }

    // Utility function to find GCD of two numbers
    // GCD of a and b
    function gcd(a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Finds the no. of Integral points between
    // two given points.
    function getCount( p,  q)
    {

        // If line joining p and q is parallel to
        // x axis, then count is difference of y
        // values
        if (p.x == q.x)
            return Math.abs(p.y - q.y) - 1;

        // If line joining p and q is parallel to
        // y axis, then count is difference of x
        // values
        if (p.y == q.y)
            return Math.abs(p.x - q.x) - 1;

        return gcd(Math.abs(p.x - q.x), Math.abs(p.y - q.y)) - 1;
    }

    // Driver program to test above   
         p = new Point(1, 9);
         q = new Point(8, 16);

        document.write("The number of integral points between " + "(" + p.x + ", " + p.y + ") and (" + q.x + ", "
                + q.y + ") is " + getCount(p, q));

// This code is contributed by gauravrajput1
</script>
```

****输出:**** 

```
The number of integral points between (1, 9) and (8, 16) is 6
```

****参考:**
[https://www . geeksforgeeks . org/count-integral-points-in-a-a-triangle/](https://www.geeksforgeeks.org/count-integral-points-inside-a-triangle/)
本文由 Paridhi Johari 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息**