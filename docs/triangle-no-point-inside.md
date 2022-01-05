# 内部没有点的三角形

> 原文:[https://www.geeksforgeeks.org/triangle-no-point-inside/](https://www.geeksforgeeks.org/triangle-no-point-inside/)

给定二维空间中的 N 个点，我们需要找到三个点，使得通过选择这些点而制成的三角形不应包含任何其他内部点。所有给定的点不会位于同一条线上，因此解将一直存在。
示例:

```
In above diagram possible triangle with no point 
inside can be formed by choosing these triplets,
[(0, 0), (2, 0), (1, 1)]
[(0, 0), (1, 1), (0, 2)]
[(1, 1), (2, 0), (2, 2)]
[(1, 1), (0, 2), (2, 2)]

So any of the above triplets can be the final answer.
```

解决方法是基于这样一个事实:如果存在一个三角形，里面没有点，那么我们可以在所有点之间形成一个任意点的三角形。
我们可以通过逐一搜索所有三个点来解决这个问题。第一点可以随机选择。选择第一个点后，我们需要两个点，这样它们的斜率应该不同，并且没有一个点应该位于这三个点的三角形内。我们可以这样做，选择第二个点作为第一个点的最近点，选择第三个点作为第二个最近点，斜率不同。为此，我们首先遍历所有的点，选择离第一个点最近的点，并将其指定为所需三角形的第二个点。然后我们再迭代一次，找到斜率不同且距离最小的点，这将是我们三角形的第三个点。

## C++

```
// C/C++ program to find triangle with no point inside
#include <bits/stdc++.h>
using namespace std;

// method to get square of distance between
// (x1, y1) and (x2, y2)
int getDistance(int x1, int y1, int x2, int y2)
{
    return (x2 - x1)*(x2 - x1) +
           (y2 - y1)*(y2 - y1);
}

// Method prints points which make triangle with no
// point inside
void triangleWithNoPointInside(int points[][2], int N)
{
    //    any point can be chosen as first point of triangle
    int first = 0;
    int second, third;
    int minD = INT_MAX;

    // choose nearest point as second point of triangle
    for (int i = 0; i < N; i++)
    {
        if (i == first)
            continue;

        // Get distance from first point and choose
        // nearest one
        int d = getDistance(points[i][0], points[i][1],
                    points[first][0], points[first][1]);
        if (minD > d)
        {
            minD = d;
            second = i;
        }
    }

    // Pick third point by finding the second closest
    // point with different slope.
    minD = INT_MAX;
    for (int i = 0; i < N; i++)
    {
        // if already chosen point then skip them
        if (i == first || i == second)
            continue;

        // get distance from first point
        int d = getDistance(points[i][0], points[i][1],
                     points[first][0], points[first][1]);

        /*  the slope of the third point with the first
            point should not be equal to the slope of
            second point with first point (otherwise
            they'll be collinear)     and among all such
            points, we choose point with the smallest
            distance  */
        // here cross multiplication is compared instead
        // of division comparison
        if ((points[i][0] - points[first][0]) *
            (points[second][1] - points[first][1]) !=
            (points[second][0] - points[first][0]) *
            (points[i][1] - points[first][1]) &&
            minD > d)
        {
            minD = d;
            third = i;
        }
    }

    cout << points[first][0] << ", "
         << points[first][1] << endl;
    cout << points[second][0] << ", "
         << points[second][1] << endl;
    cout << points[third][0] << ", "
         << points[third][1] << endl;
}

// Driver code to test above methods
int main()
{
    int points[][2] = {{0, 0}, {0, 2}, {2, 0},
                       {2, 2}, {1, 1}};
    int N = sizeof(points) / sizeof(points[0]);
    triangleWithNoPointInside(points, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find triangle
// with no point inside
import java.io.*;

class GFG
{
    // method to get square of distance between
    // (x1, y1) and (x2, y2)
    static int getDistance(int x1, int y1, int x2, int y2)
    {
        return (x2 - x1)*(x2 - x1) +
                  (y2 - y1)*(y2 - y1);
    }

    // Method prints points which make triangle with no
    // point inside
    static void triangleWithNoPointInside(int points[][], int N)
    {
        // any point can be chosen as first point of triangle
        int first = 0;
        int second =0;
        int third =0;
        int minD = Integer.MAX_VALUE;

        // choose nearest point as second point of triangle
        for (int i = 0; i < N; i++)
        {
            if (i == first)
                continue;

            // Get distance from first point and choose
            // nearest one
            int d = getDistance(points[i][0], points[i][1],
                        points[first][0], points[first][1]);
            if (minD > d)
            {
                minD = d;
                second = i;
            }
        }

        // Pick third point by finding the second closest
        // point with different slope.
        minD = Integer.MAX_VALUE;
        for (int i = 0; i < N; i++)
        {
            // if already chosen point then skip them
            if (i == first || i == second)
                continue;

            // get distance from first point
            int d = getDistance(points[i][0], points[i][1],
                        points[first][0], points[first][1]);

            /* the slope of the third point with the first
                point should not be equal to the slope of
                second point with first point (otherwise
                they'll be collinear) and among all such
                points, we choose point with the smallest
                distance */
            // here cross multiplication is compared instead
            // of division comparison
            if ((points[i][0] - points[first][0]) *
                (points[second][1] - points[first][1]) !=
                (points[second][0] - points[first][0]) *
                (points[i][1] - points[first][1]) &&
                minD > d)
            {
                minD = d;
                third = i;
            }
        }

        System.out.println(points[first][0] + ", "
            + points[first][1]);
        System.out.println(points[second][0]+ ", "
            + points[second][1]) ;
        System.out.println(points[third][0] +", "
            + points[third][1]);
    }

    // Driver code
    public static void main (String[] args)
    {
        int points[][] = {{0, 0}, {0, 2}, {2, 0},
                         {2, 2}, {1, 1}};
        int N = points.length;
        triangleWithNoPointInside(points, N);
    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find triangle
# with no point inside
import sys

# method to get square of distance between
# (x1, y1) and (x2, y2)
def getDistance(x1, y1, x2, y2):
    return (x2 - x1) * (x2 - x1) + \
           (y2 - y1) * (y2 - y1)

# Method prints points which make triangle
# with no point inside
def triangleWithNoPointInside(points, N):

    # any point can be chosen as
    # first point of triangle
    first = 0
    second = 0
    third = 0
    minD = sys.maxsize

    # choose nearest point as
    # second point of triangle
    for i in range(0, N):
        if i == first:
            continue

        # Get distance from first point and choose
        # nearest one
        d = getDistance(points[i][0], points[i][1],
                        points[first][0],
                        points[first][1])
        if minD > d:
            minD = d
            second = i

    # Pick third point by finding the second closest
    # point with different slope.
    minD = sys.maxsize
    for i in range (0, N):

        # if already chosen point then skip them
        if i == first or i == second:
            continue

        # get distance from first point
        d = getDistance(points[i][0], points[i][1],
                        points[first][0],
                        points[first][1])

        """ the slope of the third point with the first
            point should not be equal to the slope of
            second point with first point (otherwise
            they'll be collinear) and among all such
            points, we choose point with the smallest
            distance """

        # here cross multiplication is compared instead
        # of division comparison
        if ((points[i][0] - points[first][0]) *
            (points[second][1] - points[first][1]) !=
            (points[second][0] - points[first][0]) *
            (points[i][1] - points[first][1])
            and minD > d) :
            minD = d
            third = i

    print(points[first][0], ', ', points[first][1])
    print(points[second][0], ', ', points[second][1])
    print(points[third][0], ', ', points[third][1])

# Driver code
points = [[0, 0], [0, 2],
          [2, 0], [2, 2], [1, 1]]
N = len(points)
triangleWithNoPointInside(points, N)

# This code is contributed by Gowtham Yuvaraj
```

## C#

```
using System;

// C# program to find triangle
// with no point inside

public class GFG
{
    // method to get square of distance between
    // (x1, y1) and (x2, y2)
    public static int getDistance(int x1, int y1, int x2, int y2)
    {
        return (x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1);
    }

    // Method prints points which make triangle with no
    // point inside
    public static void triangleWithNoPointInside(int[][] points, int N)
    {
        // any point can be chosen as first point of triangle
        int first = 0;
        int second = 0;
        int third = 0;
        int minD = int.MaxValue;

        // choose nearest point as second point of triangle
        for (int i = 0; i < N; i++)
        {
            if (i == first)
            {
                continue;
            }

            // Get distance from first point and choose
            // nearest one
            int d = getDistance(points[i][0], points[i][1], points[first][0], points[first][1]);
            if (minD > d)
            {
                minD = d;
                second = i;
            }
        }

        // Pick third point by finding the second closest
        // point with different slope.
        minD = int.MaxValue;
        for (int i = 0; i < N; i++)
        {
            // if already chosen point then skip them
            if (i == first || i == second)
            {
                continue;
            }

            // get distance from first point
            int d = getDistance(points[i][0], points[i][1], points[first][0], points[first][1]);

            /* the slope of the third point with the first
                point should not be equal to the slope of
                second point with first point (otherwise
                they'll be collinear) and among all such
                points, we choose point with the smallest
                distance */
            // here cross multiplication is compared instead
            // of division comparison
            if ((points[i][0] - points[first][0]) * (points[second][1] - points[first][1]) != (points[second][0] - points[first][0]) * (points[i][1] - points[first][1]) && minD > d)
            {
                minD = d;
                third = i;
            }
        }

        Console.WriteLine(points[first][0] + ", " + points[first][1]);
        Console.WriteLine(points[second][0] + ", " + points[second][1]);
        Console.WriteLine(points[third][0] + ", " + points[third][1]);
    }

    // Driver code 
    public static void Main(string[] args)
    {
        int[][] points = new int[][]
        {
            new int[] {0, 0},
            new int[] {0, 2},
            new int[] {2, 0},
            new int[] {2, 2},
            new int[] {1, 1}
        };
        int N = points.Length;
        triangleWithNoPointInside(points, N);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find triangle
// with no point inside
    // method to get square of distance between
    // (x1, y1) and (x2, y2)
    function getDistance(x1 , y1 , x2 , y2) {
        return (x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1);
    }

    // Method prints points which make triangle with no
    // point inside
    function triangleWithNoPointInside(points , N) {
        // any point can be chosen as first point of triangle
        var first = 0;
        var second = 0;
        var third = 0;
        var minD = Number.MAX_VALUE;

        // choose nearest point as second point of triangle
        for (i = 0; i < N; i++) {
            if (i == first)
                continue;

            // Get distance from first point and choose
            // nearest one
            var d = getDistance(points[i][0], points[i][1], points[first][0], points[first][1]);
            if (minD > d) {
                minD = d;
                second = i;
            }
        }

        // Pick third point by finding the second closest
        // point with different slope.
        minD = Number.MAX_VALUE;
        for (i = 0; i < N; i++) {
            // if already chosen point then skip them
            if (i == first || i == second)
                continue;

            // get distance from first point
            var d = getDistance(points[i][0], points[i][1], points[first][0], points[first][1]);

            /*
             * the slope of the third point with the first point should not be equal to the
             * slope of second point with first point (otherwise they'll be collinear) and
             * among all such points, we choose point with the smallest distance
             */
            // here cross multiplication is compared instead
            // of division comparison
            if ((points[i][0] - points[first][0])
                    * (points[second][1] - points[first][1]) != (points[second][0] - points[first][0])
                            * (points[i][1] - points[first][1])
                    && minD > d) {
                minD = d;
                third = i;
            }
        }

        document.write(points[first][0] + ", " + points[first][1]+"<br/>");
        document.write(points[second][0] + ", " + points[second][1]+"<br/>");
        document.write(points[third][0] + ", " + points[third][1]+"<br/>");
    }

    // Driver code

        var points = [ [ 0, 0 ], [ 0, 2 ], [ 2, 0 ], [ 2, 2 ], [ 1, 1 ] ];
        var N = points.length;
        triangleWithNoPointInside(points, N);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
0, 0
1, 1
0, 2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。