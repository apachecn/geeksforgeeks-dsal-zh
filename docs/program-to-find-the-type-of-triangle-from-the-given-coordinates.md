# 从给定坐标中找出三角形类型的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-type-of-of-triangle-from-给定坐标/](https://www.geeksforgeeks.org/program-to-find-the-type-of-triangle-from-the-given-coordinates/)

给我们一个三角形的坐标。任务是根据边和角度对这个三角形进行分类。
**例:**

```
Input: p1 = (3, 0), p2 = (0, 4), p3 = (4, 7)
Output: Right Angle triangle and Isosceles

Input: p1 = (0, 0), p2 = (1, 1), p3 = (1, 2);
Output: Triangle is obtuse and Scalene
```

**进场:**

*   我们可以通过首先计算边长，然后根据边长的比较进行分类来解决这个问题。按边分类很简单，如果所有边都相等，三角形就是**等边**，如果任意两条边相等，三角形就是**等腰**，否则就是**不等边**。
*   现在角度可以用勾股定理来分类，如果两边的平方之和等于三边的平方，三角形就是**直角**，如果少了三角形就是**锐角**否则就是**钝角**三角形。

下面是三角形分类的简单代码:

## C++

```
// C/C++ program to classify a given triangle

#include <bits/stdc++.h>
using namespace std;

struct point {
    int x, y;
    point() {}
    point(int x, int y)
        : x(x), y(y)
    {
    }
};

// Utility method to return square of x
int square(int x)
{
    return x * x;
}

// Utility method to sort a, b, c; after this
// method a <= b <= c
void order(int& a, int& b, int& c)
{
    int copy[3];
    copy[0] = a;
    copy[1] = b;
    copy[2] = c;
    sort(copy, copy + 3);
    a = copy[0];
    b = copy[1];
    c = copy[2];
}

// Utility method to return Square of distance
// between two points
int euclidDistSquare(point p1, point p2)
{
    return square(p1.x - p2.x) + square(p1.y - p2.y);
}

// Method to classify side
string getSideClassification(int a, int b, int c)
{
    // if all sides are equal
    if (a == b && b == c)
        return "Equilateral";

    // if any two sides are equal
    else if (a == b || b == c)
        return "Isosceles";

    else
        return "Scalene";
}

// Method to classify angle
string getAngleClassification(int a, int b, int c)
{
    // If addition of sum of square of two side
    // is less, then acute
    if (a + b > c)
        return "acute";

    // by pythagoras theorem
    else if (a + b == c)
        return "right";

    else
        return "obtuse";
}

// Method to classify the triangle by sides and angles
void classifyTriangle(point p1, point p2, point p3)
{
    // Find squares of distances between points
    int a = euclidDistSquare(p1, p2);
    int b = euclidDistSquare(p1, p3);
    int c = euclidDistSquare(p2, p3);

    // Sort all squares of distances in increasing order
    order(a, b, c);

    cout << "Triangle is "
                + getAngleClassification(a, b, c)
                + " and "
                + getSideClassification(a, b, c)
         << endl;
}

// Driver code
int main()
{
    point p1, p2, p3;
    p1 = point(3, 0);
    p2 = point(0, 4);
    p3 = point(4, 7);
    classifyTriangle(p1, p2, p3);

    p1 = point(0, 0);
    p2 = point(1, 1);
    p3 = point(1, 2);
    classifyTriangle(p1, p2, p3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to classify a given triangle
import java.util.*;
class GFG
{

static class point
{
    int x, y;
    point() {}

    public point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// Utility method to return square of x
static int square(int x)
{
    return x * x;
}
static int a, b, c;

// Utility method to sort a, b, c; after this
// method a <= b <= c
static void order()
{
    int []copy = new int[3];
    copy[0] = a;
    copy[1] = b;
    copy[2] = c;
    Arrays.sort(copy);
    a = copy[0];
    b = copy[1];
    c = copy[2];
}

// Utility method to return Square of distance
// between two points
static int euclidDistSquare(point p1, point p2)
{
    return square(p1.x - p2.x) + square(p1.y - p2.y);
}

// Method to classify side
static String getSideClassification(int a,
                                    int b, int c)
{
    // if all sides are equal
    if (a == b && b == c)
        return "Equilateral";

    // if any two sides are equal
    else if (a == b || b == c)
        return "Isosceles";

    else
        return "Scalene";
}

// Method to classify angle
static String getAngleClassification(int a,
                                     int b, int c)
{
    // If addition of sum of square of two side
    // is less, then acute
    if (a + b > c)
        return "acute";

    // by pythagoras theorem
    else if (a + b == c)
        return "right";

    else
        return "obtuse";
}

// Method to classify the triangle
// by sides and angles
static void classifyTriangle(point p1,
                             point p2, point p3)
{
    // Find squares of distances between points
    a = euclidDistSquare(p1, p2);
    b = euclidDistSquare(p1, p3);
    c = euclidDistSquare(p2, p3);

    // Sort all squares of distances in increasing order
    order();

    System.out.println( "Triangle is "
                + getAngleClassification(a, b, c)
                + " and "
                + getSideClassification(a, b, c));
}

// Driver code
public static void main(String[] args)
{
    point p1, p2, p3;
    p1 = new point(3, 0);
    p2 = new point(0, 4);
    p3 = new point(4, 7);
    classifyTriangle(p1, p2, p3);

    p1 = new point(0, 0);
    p2 = new point(1, 1);
    p3 = new point(1, 2);
    classifyTriangle(p1, p2, p3);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to classify a given triangle
using System;

class GFG
{
public class point
{
    public int x, y;
    public point() {}

    public point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// Utility method to return square of x
static int square(int x)
{
    return x * x;
}
static int a, b, c;

// Utility method to sort a, b, c;
// after this method a <= b <= c
static void order()
{
    int []copy = new int[3];
    copy[0] = a;
    copy[1] = b;
    copy[2] = c;
    Array.Sort(copy);
    a = copy[0];
    b = copy[1];
    c = copy[2];
}

// Utility method to return
// Square of distance between two points
static int euclidDistSquare(point p1,
                            point p2)
{
    return square(p1.x - p2.x) +
           square(p1.y - p2.y);
}

// Method to classify side
static String getSideClassification(int a,
                                    int b, int c)
{
    // if all sides are equal
    if (a == b && b == c)
        return "Equilateral";

    // if any two sides are equal
    else if (a == b || b == c)
        return "Isosceles";

    else
        return "Scalene";
}

// Method to classify angle
static String getAngleClassification(int a,
                                     int b, int c)
{
    // If addition of sum of square of
    // two side is less, then acute
    if (a + b > c)
        return "acute";

    // by pythagoras theorem
    else if (a + b == c)
        return "right";

    else
        return "obtuse";
}

// Method to classify the triangle
// by sides and angles
static void classifyTriangle(point p1,
                              point p2,
                              point p3)
{
    // Find squares of distances between points
    a = euclidDistSquare(p1, p2);
    b = euclidDistSquare(p1, p3);
    c = euclidDistSquare(p2, p3);

    // Sort all squares of distances
    // in increasing order
    order();

    Console.WriteLine( "Triangle is "
                + getAngleClassification(a, b, c)
                + " and "
                + getSideClassification(a, b, c));
}

// Driver code
public static void Main(String[] args)
{
    point p1, p2, p3;
    p1 = new point(3, 0);
    p2 = new point(0, 4);
    p3 = new point(4, 7);
    classifyTriangle(p1, p2, p3);

    p1 = new point(0, 0);
    p2 = new point(1, 1);
    p3 = new point(1, 2);
    classifyTriangle(p1, p2, p3);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to classify a given triangle

class point
{
    constructor(x,y)
    {
        this.x = x;
        this.y = y;
    }
}

// Utility method to return square of x
function square(x)
{
    return x * x;
}
let a, b, c;

// Utility method to sort a, b, c; after this
// method a <= b <= c
function order()
{
    let copy = new Array(3);
    copy[0] = a;
    copy[1] = b;
    copy[2] = c;
    (copy).sort(function(a,b){return a-b;});
    a = copy[0];
    b = copy[1];
    c = copy[2];
}

// Utility method to return Square of distance
// between two points
function euclidDistSquare(p1,p2)
{
    return square(p1.x - p2.x) + square(p1.y - p2.y);
}

// Method to classify side
function getSideClassification(a,b,c)
{
    // if all sides are equal
    if (a == b && b == c)
        return "Equilateral";

    // if any two sides are equal
    else if (a == b || b == c)
        return "Isosceles";

    else
        return "Scalene";
}

// Method to classify angle
function getAngleClassification(a, b, c)
{

    // If addition of sum of square of two side
    // is less, then acute
    if (a + b > c)
        return "acute";

    // by pythagoras theorem
    else if (a + b == c)
        return "right";

    else
        return "obtuse";
}

// Method to classify the triangle
// by sides and angles
function classifyTriangle(p1, p2, p3)
{

    // Find squares of distances between points
    a = euclidDistSquare(p1, p2);
    b = euclidDistSquare(p1, p3);
    c = euclidDistSquare(p2, p3);

    // Sort all squares of distances in increasing order
    order();

    document.write( "Triangle is "
                + getAngleClassification(a, b, c)
                + " and "
                + getSideClassification(a, b, c)+"<br>");
}

// Driver code
let p1, p2, p3;
p1 = new point(3, 0);
p2 = new point(0, 4);
p3 = new point(4, 7);
classifyTriangle(p1, p2, p3);

p1 = new point(0, 0);
p2 = new point(1, 1);
p3 = new point(1, 2);
classifyTriangle(p1, p2, p3);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Triangle is right and Isosceles
Triangle is obtuse and Scalene
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。