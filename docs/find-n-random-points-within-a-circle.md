# 在一个圆内找到 N 个随机点

> 原文:[https://www . geesforgeks . org/find-n-random-points-in-a-circle/](https://www.geeksforgeeks.org/find-n-random-points-within-a-circle/)

给定四个整数 **N、R、X 和 Y** ，使其代表一个以**【X、Y】**为圆心坐标的半径为 **R** 的圆。任务是在圆内或圆上随机找 **N** 点。
**示例:**

> **输入:** R = 12，X = 3，Y = 3，N = 5
> **输出:** (7.05，-3.36) (5.21，-7.49) (7.53，0.19) (-2.37，12.05) (1.45，11.80)
> **输入:** R = 5，X = 1，Y = 1，N = 3
> **输出:**

**方法:**要在圆内或圆上找到一个随机点，我们需要两个分量，一个**角(θ)**和**距中心的距离(D)**。之后现在，点(x <sub>i</sub> ，y <sub>i</sub> )可以表示为:

```
xi = X + D * cos(theta)
yi = Y + D * sin(theta)
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define PI 3.141592653589

// Return a random double between 0 & 1
double uniform()
{
    return (double)rand() / RAND_MAX;
}

// Function to find the N random points on
// the given circle
vector<pair<double, double> > randPoint(
    int r, int x, int y, int n)
{
    // Result vector
    vector<pair<double, double> > res;

    for (int i = 0; i < n; i++) {

        // Get Angle in radians
        double theta = 2 * PI * uniform();

        // Get length from center
        double len = sqrt(uniform()) * r;

        // Add point to results.
        res.push_back({ x + len * cos(theta),
                        y + len * sin(theta) });
    }

    // Return the N points
    return res;
}

// Function to display the content of
// the vector A
void printVector(
    vector<pair<double, double> > A)
{

    // Iterate over A
    for (pair<double, double> P : A) {

        // Print the N random points stored
        printf("(%.2lf, %.2lf)\n",
               P.first, P.second);
    }
}

// Driver Code
int main()
{
    // Given dimensions
    int R = 12;
    int X = 3;
    int Y = 3;
    int N = 5;

    // Function Call
    printVector(randPoint(R, X, Y, N));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static final double PI = 3.141592653589;
static class pair
{
    double first, second;

    public pair(double first,
                double second)
    {
        super();
        this.first = first;
        this.second = second;
    }
}

// Return a random double between 0 & 1
static double uniform(){return Math.random();}

// Function to find the N random points on
// the given circle
static Vector<pair> randPoint(int r, int x,
                              int y, int n)
{

    // Result vector
    Vector<pair> res = new Vector<pair>();

    for(int i = 0; i < n; i++)
    {

        // Get Angle in radians
        double theta = 2 * PI * uniform();

        // Get length from center
        double len = Math.sqrt(uniform()) * r;

        // Add point to results.
        res.add(new pair(x + len * Math.cos(theta),
                         y + len * Math.sin(theta)));
    }

    // Return the N points
    return res;
}

// Function to display the content of
// the vector A
static void printVector(Vector<pair> A)
{

    // Iterate over A
    for(pair P : A)
    {

        // Print the N random points stored
        System.out.printf("(%.2f, %.2f)\n",
                          P.first, P.second);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given dimensions
    int R = 12;
    int X = 3;
    int Y = 3;
    int N = 5;

    // Function call
    printVector(randPoint(R, X, Y, N));
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

static readonly double PI = 3.141592653589;
class pair
{
    public double first, second;

    public pair(double first,
                double second)
    {
        this.first = first;
        this.second = second;
    }
}

// Return a random double between 0 & 1
static double uniform()
{
    return new Random().NextDouble();
}

// Function to find the N random points on
// the given circle
static List<pair> randPoint(int r, int x,
                              int y, int n)
{

    // Result vector
    List<pair> res = new List<pair>();
    for(int i = 0; i < n; i++)
    {

        // Get Angle in radians
        double theta = 2 * PI * uniform();

        // Get length from center
        double len = Math.Sqrt(uniform()) * r;

        // Add point to results.
        res.Add(new pair(x + len * Math.Cos(theta),
                         y + len * Math.Sin(theta)));
    }

    // Return the N points
    return res;
}

// Function to display the content of
// the vector A
static void printList(List<pair> A)
{

    // Iterate over A
    foreach(pair P in A)
    {

        // Print the N random points stored
        Console.Write("({0:F2}, {1:F2})\n",
                          P.first, P.second);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given dimensions
    int R = 12;
    int X = 3;
    int Y = 3;
    int N = 5;

    // Function call
    printList(randPoint(R, X, Y, N));
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
(7.05, -3.36)
(5.21, -7.49)
(7.53, 0.19)
(-2.37, 12.05)
(1.45, 11.80)
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(N)*