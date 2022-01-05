# 覆盖无限网格上一系列点所需的最小步数

> 原文:[https://www . geesforgeks . org/覆盖无限网格上的点序列所需的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-needed-to-cover-a-sequence-of-points-on-an-infinite-grid/)

给定一个无限网格，初始单元位置(x，y)和一系列需要按照给定顺序覆盖的其他单元位置。任务是找到到达所有这些细胞所需的最小步数。
**注意:**移动可以在给定单元格的八个可能方向中的任何一个方向进行，即从单元格(x，y)开始，您可以移动到以下八个位置中的任何一个:(x-1，y+1)，(x-1，y)，(x-1，y-1)，(x，y-1)，(x+1，y)，(x+1，y)，(x+1，y+1)，(x，y+1)都是可能的。

**示例:**

> **输入:**点[] = [(0，0)，(1，1)，(1，2)]
> **输出:** 2
> 从(0，0)移动到(1，1)一步(对角线)然后
> 从(1，1)移动到(1，2)一步(向右)
> 
> **输入:**点[] = [{4，6}，{1，2}，{4，5}，{10，12}]
> **输出:** 14
> 从 **(4，6)** - > (3，5)-(T18)【2，4】->(1，3) - >
> **(1，2)** - > (2，3)-(T22)】

**方法:**因为所有给定点都要按照指定的顺序覆盖。找到从一个起点到达下一个点所需的最小步数，那么覆盖所有点的所有这些最小步数的总和就是答案。从点(x1，y1)到达(x2，y2)的一种方法是在水平方向移动 abs(x2-x1)步，在垂直方向移动 abs(y2-y1)步，但这不是到达(x2，y2)的最短路径。最好的方法是在对角线方向覆盖最大可能的距离，并保持在水平或垂直方向。
如果我们仔细观察，这只是减少到最大 **abs(x2-x1)** 和 **abs(y2-y1)** 。所有点的导线测量和所有对角线距离的总和将是答案。

下面是上述方法的实现:

## C++

```
// C++ program to cover a sequence of points
// in minimum steps in a given order.
#include <bits/stdc++.h>
using namespace std;

// cell structure denoted as point
struct point {
    int x, y;
};

// function to give minimum steps to
// move from point p1 to p2
int shortestPath(point p1, point p2)
{
    // dx is total horizontal
    // distance to be covered
    int dx = abs(p1.x - p2.x);

    // dy is total vertical
    // distance to be covered
    int dy = abs(p1.y - p2.y);

    // required answer is
    // maximum of these two
    return max(dx, dy);
}

// Function to return the minimum steps
int coverPoints(point sequence[], int size)
{
    int stepCount = 0;

    // finding steps for each
    // consecutive point in the sequence
    for (int i = 0; i < size - 1; i++) {
        stepCount += shortestPath(sequence[i],
                                  sequence[i + 1]);
    }

    return stepCount;
}

// Driver code
int main()
{
    // arr stores sequence of points
    // that are to be visited
    point arr[] = { { 4, 6 }, { 1, 2 }, { 4, 5 }, { 10, 12 } };

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << coverPoints(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to cover a 
// sequence of points in
// minimum steps in a given order.
import java.io.*;
import java.util.*;
import java.lang.*;

// class denoted as point
class point 
{
    int x, y;
    point(int a, int b)
    {
        x = a;
        y = b;

    }
}

class GFG
{
// function to give minimum 
// steps to move from point 
// p1 to p2
static int shortestPath(point p1, 
                        point p2)
{
    // dx is total horizontal
    // distance to be covered
    int dx = Math.abs(p1.x - p2.x);

    // dy is total vertical
    // distance to be covered
    int dy = Math.abs(p1.y - p2.y);

    // required answer is
    // maximum of these two
    return Math.max(dx, dy);
}

// Function to return
// the minimum steps
static int coverPoints(point sequence[], 
                       int size)
{
    int stepCount = 0;

    // finding steps for 
    // each consecutive
    // point in the sequence
    for (int i = 0; i < size - 1; i++)
    {
        stepCount += shortestPath(sequence[i],
                                  sequence[i + 1]);
    }

    return stepCount;
}

// Driver code
public static void main(String args[])
{
    // arr stores sequence of points
    // that are to be visited
    point arr[] = new point[4];
    arr[0] = new point(4, 6);
    arr[1] = new point(1, 2);
    arr[2] = new point(4, 5);
    arr[3] = new point(10, 12);

    int n = arr.length;
    System.out.print(coverPoints(arr, n));
}
}
```

## 蟒蛇 3

```
# Python program to cover a sequence of points
# in minimum steps in a given order.

# function to give minimum steps to
# move from pop1 to p2
def shortestPath(p1, p2):

    # dx is total horizontal
    # distance to be covered
    dx = abs(p1[0] - p2[0])

    # dy is total vertical
    # distance to be covered
    dy = abs(p1[1] - p2[1])

    # required answer is
    # maximum of these two
    return max(dx, dy)

# Function to return the minimum steps
def coverPoints(sequence, size):

    stepCount = 0

    # finding steps for each
    # consecutive poin the sequence
    for i in range(size-1):
        stepCount += shortestPath(sequence[i],sequence[i + 1])

    return stepCount

# Driver code
# arr stores sequence of points
# that are to be visited
arr =  [[4, 6] ,[ 1, 2 ], [ 4, 5] , [ 10, 12]]  

n = len(arr)
print(coverPoints(arr, n))

# This code is contributed by shivanisinghss2110.
```

## C#

```
// C# program to cover a 
// sequence of points in
// minimum steps in a given order.

using System; 
// class denoted as point
public class point 
{
    public int x, y;
    public point(int a, int b)
    {
        x = a;
        y = b;

    }
}

public class GFG
{
    // function to give minimum 
    // steps to move from point 
    // p1 to p2[]
    static int shortestPath(point p1, 
                            point p2)
    {
        // dx is total horizontal
        // distance to be covered
        int dx = Math.Abs(p1.x - p2.x);

        // dy is total vertical
        // distance to be covered
        int dy = Math.Abs(p1.y - p2.y);

        // required answer is
        // maximum of these two
        return Math.Max(dx, dy);
    }

    // Function to return
    // the minimum steps
    static int coverPoints(point []sequence, 
                           int size)
    {
        int stepCount = 0;

        // finding steps for 
        // each consecutive
        // point in the sequence
        for (int i = 0; i < size - 1; i++)
        {
            stepCount += shortestPath(sequence[i],
                                      sequence[i + 1]);
        }

        return stepCount;
    }

    // Driver code
    public static void Main()
    {
        // arr stores sequence of points
        // that are to be visited
        point []arr = new point[4];
        arr[0] = new point(4, 6);
        arr[1] = new point(1, 2);
        arr[2] = new point(4, 5);
        arr[3] = new point(10, 12);

        int n = arr.Length;
        Console.WriteLine(coverPoints(arr, n));
    }
}
// This code is contributed by Rajput-Ji
```

```
# Traversing from one point to another point
# storing the minimum number of steps
def traversal_steps(points):
    minSteps = 0
    for p in range(len(points)-1):

        # taking the manhattan distance between 
        # x and y-coordinates 
        d1 = abs(points[p][0] - points[p+1][0])
        d2 = abs(points[p][1] - points[p+1][1])

        # adding the maximum among the two to the 
        # running steps parameter
        minSteps += max(d1,d2)
    return (minSteps)

# Main Driver Code
if __name__ == '__main__':
    points = [(0,0),(1,1),(1,2)]
    print (traversal_steps(points))
    points = [(4,6),(1,2),(4,5),(10,12)]
    print (traversal_steps(points))
```

**Output:**

```
14

```

**时间复杂度:** O(N)