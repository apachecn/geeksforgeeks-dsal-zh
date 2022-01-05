# 找出上面、下面、左边或右边至少有 1 个点的点数

> 原文:[https://www . geeksforgeeks . org/find-在它的左下方或右上方至少有 1 个点的点数/](https://www.geeksforgeeks.org/find-the-number-of-points-that-have-atleast-1-point-above-below-left-or-right-of-it/)

给定二维平面中的 **N** 点。如果两个点的 X 坐标相同，并且第一个点的 Y 坐标大于第二个点的 Y 坐标，则称一个点在另一个点之上。同样，我们定义如下，左和右。任务是计算上面、下面、左边或右边至少有一个点的点数。
**例:**

> **输入:** arr[] = {{0，0}、{0，1}、{1，0}、{0，-1}、{-1，0}}
> **输出:** 1
> 唯一满足条件的点是点(0，0)。
> **输入:** arr[] = {{0，0}，{1，0}，{0，-2}，{5，0}}
> **输出:** 0

**逼近:**对于每一个 **X** 坐标，在所有有这个 **X** 坐标的点中找出 2 个值，最小值和最大值 **Y** 坐标。对每个 **Y** 坐标做同样的事情。现在，对于满足约束的点，其 **Y** 坐标必须位于该 **X** 坐标的两个计算值之间。同样检查其 **X** 坐标。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MX 2001
#define OFF 1000

// Represents a point in 2-D space
struct point {
    int x, y;
};

// Function to return the count of
// required points
int countPoints(int n, struct point points[])
{
    int minx[MX];
    int miny[MX];

    // Initialize minimum values to infinity
    fill(minx, minx + MX, INT_MAX);
    fill(miny, miny + MX, INT_MAX);

    // Initialize maximum values to zero
    int maxx[MX] = { 0 };
    int maxy[MX] = { 0 };
    int x, y;
    for (int i = 0; i < n; i++) {

        // Add offset to deal with negative
        // values
        points[i].x += OFF;
        points[i].y += OFF;
        x = points[i].x;
        y = points[i].y;

        // Update the minimum and maximum
        // values
        minx[y] = min(minx[y], x);
        maxx[y] = max(maxx[y], x);
        miny[x] = min(miny[x], y);
        maxy[x] = max(maxy[x], y);
    }

    int count = 0;
    for (int i = 0; i < n; i++) {
        x = points[i].x;
        y = points[i].y;

        // Check if condition is satisfied
        // for X coordinate
        if (x > minx[y] && x < maxx[y])

            // Check if condition is satisfied
            // for Y coordinate
            if (y > miny[x] && y < maxy[x])
                count++;
    }
    return count;
}

// Driver code
int main()
{
    struct point points[] = { { 0, 0 },
                              { 0, 1 },
                              { 1, 0 },
                              { 0, -1 },
                              { -1, 0 } };
    int n = sizeof(points) / sizeof(points[0]);
    cout << countPoints(n, points);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MX = 2001;
static int OFF = 1000;

// Represents a point in 2-D space
static class point
{
    int x, y;

    public point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

};

// Function to return the count of
// required points
static int countPoints(int n, point points[])
{
    int []minx = new int[MX];
    int []miny = new int[MX];

    // Initialize minimum values to infinity
    for (int i = 0; i < n; i++)
    {
        minx[i]=Integer.MAX_VALUE;
        miny[i]=Integer.MAX_VALUE;
    }

    // Initialize maximum values to zero
    int []maxx = new int[MX];
    int []maxy = new int[MX];

    int x, y;
    for (int i = 0; i < n; i++)
    {

        // Add offset to deal with negative
        // values
        points[i].x += OFF;
        points[i].y += OFF;
        x = points[i].x;
        y = points[i].y;

        // Update the minimum and maximum
        // values
        minx[y] = Math.min(minx[y], x);
        maxx[y] = Math.max(maxx[y], x);
        miny[x] = Math.min(miny[x], y);
        maxy[x] = Math.max(maxy[x], y);
    }

    int count = 0;
    for (int i = 0; i < n; i++)
    {
        x = points[i].x;
        y = points[i].y;

        // Check if condition is satisfied
        // for X coordinate
        if (x > minx[y] && x < maxx[y])

            // Check if condition is satisfied
            // for Y coordinate
            if (y > miny[x] && y < maxy[x])
                count++;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    point points[] = {new point(0, 0),
                      new point(0, 1),
                      new point(1, 0),
                      new point(0, -1),
                      new point(-1, 0)};
    int n = points.length;
    System.out.println(countPoints(n, points));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from sys import maxsize as INT_MAX

MX = 2001
OFF = 1000

# Represents a point in 2-D space
class point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

# Function to return the count of
# required points
def countPoints(n: int, points: list) -> int:

    # Initialize minimum values to infinity
    minx = [INT_MAX] * MX
    miny = [INT_MAX] * MX

    # Initialize maximum values to zero
    maxx = [0] * MX
    maxy = [0] * MX
    x, y = 0, 0
    for i in range(n):

        # Add offset to deal with negative
        # values
        points[i].x += OFF
        points[i].y += OFF
        x = points[i].x
        y = points[i].y

        # Update the minimum and maximum
        # values
        minx[y] = min(minx[y], x)
        maxx[y] = max(maxx[y], x)
        miny[x] = min(miny[x], y)
        maxy[x] = max(maxy[x], y)

    count = 0
    for i in range(n):
        x = points[i].x
        y = points[i].y

        # Check if condition is satisfied
        # for X coordinate
        if (x > minx[y] and x < maxx[y]):

            # Check if condition is satisfied
            # for Y coordinate
            if (y > miny[x] and y < maxy[x]):
                count += 1

    return count

# Driver Code
if __name__ == "__main__":

    points = [point(0, 0),
              point(0, 1),
              point(1, 0),
              point(0, -1),
              point(-1, 0)]
    n = len(points)

    print(countPoints(n, points))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int MX = 2001;
static int OFF = 1000;

// Represents a point in 2-D space
public class point
{
    public int x, y;

    public point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// Function to return the count of
// required points
static int countPoints(int n, point []points)
{
    int []minx = new int[MX];
    int []miny = new int[MX];

    // Initialize minimum values to infinity
    for (int i = 0; i < n; i++)
    {
        minx[i]=int.MaxValue;
        miny[i]=int.MaxValue;
    }

    // Initialize maximum values to zero
    int []maxx = new int[MX];
    int []maxy = new int[MX];

    int x, y;
    for (int i = 0; i < n; i++)
    {

        // Add offset to deal with negative
        // values
        points[i].x += OFF;
        points[i].y += OFF;
        x = points[i].x;
        y = points[i].y;

        // Update the minimum and maximum
        // values
        minx[y] = Math.Min(minx[y], x);
        maxx[y] = Math.Max(maxx[y], x);
        miny[x] = Math.Min(miny[x], y);
        maxy[x] = Math.Max(maxy[x], y);
    }

    int count = 0;
    for (int i = 0; i < n; i++)
    {
        x = points[i].x;
        y = points[i].y;

        // Check if condition is satisfied
        // for X coordinate
        if (x > minx[y] && x < maxx[y])

            // Check if condition is satisfied
            // for Y coordinate
            if (y > miny[x] && y < maxy[x])
                count++;
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    point []points = {new point(0, 0),
                      new point(0, 1),
                      new point(1, 0),
                      new point(0, -1),
                      new point(-1, 0)};
    int n = points.Length;
    Console.WriteLine(countPoints(n, points));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MX = 2001;
var OFF = 1000;

// Function to return the count of
// required points
function countPoints( n, points)
{
    var minx = Array(MX).fill(1000000000);
    var miny = Array(MX).fill(1000000000);

    // Initialize maximum values to zero
    var maxx = Array(MX).fill(0);
    var maxy = Array(MX).fill(0);
    var x, y;
    for (var i = 0; i < n; i++) {

        // Add offset to deal with negative
        // values
        points[i][0] += OFF;
        points[i][1] += OFF;
        x = points[i][0];
        y = points[i][1];

        // Update the minimum and maximum
        // values
        minx[y] = Math.min(minx[y], x);
        maxx[y] = Math.max(maxx[y], x);
        miny[x] = Math.min(miny[x], y);
        maxy[x] = Math.max(maxy[x], y);
    }

    var count = 0;
    for (var i = 0; i < n; i++) {
        x = points[i][0];
        y = points[i][1];

        // Check if condition is satisfied
        // for X coordinate
        if (x > minx[y] && x < maxx[y])

            // Check if condition is satisfied
            // for Y coordinate
            if (y > miny[x] && y < maxy[x])
                count++;
    }
    return count;
}

// Driver code
var points = [ [ 0, 0 ],
                          [ 0, 1 ],
                          [ 1, 0 ],
                          [ 0, -1 ],
                          [ -1, 0 ] ];
var n = points.length;
document.write( countPoints(n, points));

// This code is contributed by famously.
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)