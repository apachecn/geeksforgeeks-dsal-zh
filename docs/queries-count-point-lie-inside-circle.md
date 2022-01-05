# 关于点数的查询位于一个圆内

> 原文:[https://www . geesforgeks . org/query-count-point-lie-inside-circle/](https://www.geeksforgeeks.org/queries-count-point-lie-inside-circle/)

给定 2D 平面上的点的坐标(x，y)和 Q 查询。每个查询包含一个整数 **r** ，任务是统计位于半径为 r 且以原点为中心的圆的内部或圆周上的点数。
**例:**

```
Input : n = 5
Coordinates: 
1 1
2 2
3 3
-1 -1
4 4

Query 1: 3
Query 2: 32

Output :
3
5
For first query radius = 3, number of points lie
inside or on the circumference are (1, 1), (-1, -1),
(2, 2). There are only 3 points lie inside or on 
the circumference of the circle.
For second query radius = 32, all five points are
inside the circle. 
```

以半径为 r，x<sup>2</sup>+y<sup>2</sup>= r<sup>2</sup>的原点(0，0)为中心的圆的方程。以及(x <sub>1</sub> 、y <sub>1</sub> )点位于圆周内部或圆周上的条件，x<sub>1</sub><sup>2</sup>+y<sub>1</sub><sup>2</sup><= r<sup>2</sup>。
一种**天真的方法**可以针对每个查询，遍历所有点并检查条件。这需要 0(n * Q)时间复杂度。
一种**有效的方法**是预先计算每个点坐标的 x <sup>2</sup> + y <sup>2</sup> ，并将它们存储在数组 p[]中。现在，对数组 p[]进行排序。然后对数组应用二分搜索法，为每个查询找到最后一个条件为 p[i] < = r <sup>2</sup> 的索引。
以下是本办法的实施情况:

## C++

```
// C++ program to find number of points lie inside or
// on the circumference of circle for Q queries.
#include <bits/stdc++.h>
using namespace std;

// Computing the x^2 + y^2 for each given points
// and sorting them.
void preprocess(int p[], int x[], int y[], int n)
{
    for (int i = 0; i < n; i++)
        p[i] = x[i] * x[i] + y[i] * y[i];

    sort(p, p + n);
}

// Return count of points lie inside or on circumference
// of circle using binary search on p[0..n-1]
int query(int p[], int n, int rad)
{
    int start = 0, end = n - 1;
    while ((end - start) > 1) {
        int mid = (start + end) / 2;
        double tp = sqrt(p[mid]);

        if (tp > (rad * 1.0))
            end = mid - 1;
        else
            start = mid;
    }

    double tp1 = sqrt(p[start]), tp2 = sqrt(p[end]);

    if (tp1 > (rad * 1.0))
        return 0;
    else if (tp2 <= (rad * 1.0))
        return end + 1;
    else
        return start + 1;
}

// Driven Program
int main()
{
    int x[] = { 1, 2, 3, -1, 4 };
    int y[] = { 1, 2, 3, -1, 4 };
    int n = sizeof(x) / sizeof(x[0]);

    // Compute distances of all points and keep
    // the distances sorted so that query can
    // work in O(logn) using Binary Search.
    int p[n];
    preprocess(p, x, y, n);

    // Print number of points in a circle of radius 3.
    cout << query(p, n, 3) << endl;

    // Print number of points in a circle of radius 32.
    cout << query(p, n, 32) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Queries on count of
// points lie inside a circle
import java.util.*;

class GFG {

    // Computing the x^2 + y^2 for each given points
    // and sorting them.
    public static void preprocess(int p[], int x[],
                                  int y[], int n)
    {
        for (int i = 0; i < n; i++)
            p[i] = x[i] * x[i] + y[i] * y[i];

        Arrays.sort(p);
    }

    // Return count of points lie inside or on
    // circumference of circle using binary
    // search on p[0..n-1]
    public static int query(int p[], int n, int rad)
    {
        int start = 0, end = n - 1;
        while ((end - start) > 1) {
            int mid = (start + end) / 2;
            double tp = Math.sqrt(p[mid]);

            if (tp > (rad * 1.0))
                end = mid - 1;
            else
                start = mid;
        }

        double tp1 = Math.sqrt(p[start]);
        double tp2 = Math.sqrt(p[end]);

        if (tp1 > (rad * 1.0))
            return 0;
        else if (tp2 <= (rad * 1.0))
            return end + 1;
        else
            return start + 1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int x[] = { 1, 2, 3, -1, 4 };
        int y[] = { 1, 2, 3, -1, 4 };
        int n = x.length;

        // Compute distances of all points and keep
        // the distances sorted so that query can
        // work in O(logn) using Binary Search.
        int p[] = new int[n];
        preprocess(p, x, y, n);

        // Print number of points in a circle of
        // radius 3.
        System.out.println(query(p, n, 3));

        // Print number of points in a circle of
        // radius 32.
        System.out.println(query(p, n, 32));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 program to find number of
# points lie inside or on the circumference
# of circle for Q queries.
import math

# Computing the x^2 + y^2 for each
# given points and sorting them.
def preprocess(p, x, y, n):
    for i in range(n):
        p[i] = x[i] * x[i] + y[i] * y[i]

    p.sort()

# Return count of points lie inside
# or on circumference of circle using
# binary search on p[0..n-1]
def query(p, n, rad):

    start = 0
    end = n - 1
    while ((end - start) > 1):
        mid = (start + end) // 2
        tp = math.sqrt(p[mid])

        if (tp > (rad * 1.0)):
            end = mid - 1
        else:
            start = mid

    tp1 = math.sqrt(p[start])
    tp2 = math.sqrt(p[end])

    if (tp1 > (rad * 1.0)):
        return 0
    elif (tp2 <= (rad * 1.0)):
        return end + 1
    else:
        return start + 1

# Driver Code
if __name__ == "__main__":

    x = [ 1, 2, 3, -1, 4 ]
    y = [ 1, 2, 3, -1, 4 ]
    n = len(x)

    # Compute distances of all points and keep
    # the distances sorted so that query can
    # work in O(logn) using Binary Search.
    p = [0] * n
    preprocess(p, x, y, n)

    # Print number of points in a
    # circle of radius 3.
    print(query(p, n, 3))

    # Print number of points in a
    # circle of radius 32.
    print(query(p, n, 32))

# This code is contributed by ita_c
```

## C#

```
// C# Code for Queries on count of
// points lie inside a circle
using System;

class GFG {

    // Computing the x^2 + y^2 for each
    // given points and sorting them.
    public static void preprocess(int[] p, int[] x,
                                    int[] y, int n)
    {
        for (int i = 0; i < n; i++)
            p[i] = x[i] * x[i] + y[i] * y[i];

        Array.Sort(p);
    }

    // Return count of points lie inside or on
    // circumference of circle using binary
    // search on p[0..n-1]
    public static int query(int[] p, int n, int rad)
    {
        int start = 0, end = n - 1;
        while ((end - start) > 1) {
            int mid = (start + end) / 2;
            double tp = Math.Sqrt(p[mid]);

            if (tp > (rad * 1.0))
                end = mid - 1;
            else
                start = mid;
        }

        double tp1 = Math.Sqrt(p[start]);
        double tp2 = Math.Sqrt(p[end]);

        if (tp1 > (rad * 1.0))
            return 0;
        else if (tp2 <= (rad * 1.0))
            return end + 1;
        else
            return start + 1;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] x = { 1, 2, 3, -1, 4 };
        int[] y = { 1, 2, 3, -1, 4 };
        int n = x.Length;

        // Compute distances of all points and keep
        // the distances sorted so that query can
        // work in O(logn) using Binary Search.
        int[] p = new int[n];
        preprocess(p, x, y, n);

        // Print number of points in a circle of
        // radius 3.
        Console.WriteLine(query(p, n, 3));

        // Print number of points in a circle of
        // radius 32.
        Console.WriteLine(query(p, n, 32));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// Javascript Code for Queries on count of
// points lie inside a circle

    // Computing the x^2 + y^2 for each given points
    // and sorting them.
    function preprocess(p,x,y,n)
    {
        for (let i = 0; i < n; i++)
            p[i] = x[i] * x[i] + y[i] * y[i];

        p.sort(function(a,b){return a-b;});

    }

    // Return count of points lie inside or on
    // circumference of circle using binary
    // search on p[0..n-1]
    function query(p,n,rad)
    {
        let start = 0, end = n - 1;
        while ((end - start) > 1) {
            let mid = Math.floor((start + end) / 2);
            let tp = Math.sqrt(p[mid]);

            if (tp > (rad * 1.0))
                end = mid - 1;
            else
                start = mid;
        }

        let tp1 = Math.sqrt(p[start]);
        let tp2 = Math.sqrt(p[end]);

        if (tp1 > (rad * 1.0))
            return 0;
        else if (tp2 <= (rad * 1.0))
            return end + 1;
        else
            return start + 1;
    }

    /* Driver program to test above function */
    let x=[1, 2, 3, -1, 4 ];
    let y=[1, 2, 3, -1, 4];
    let n = x.length;

    // Compute distances of all points and keep
    // the distances sorted so that query can
    // work in O(logn) using Binary Search.
    let p=new Array(n);
    for(let i=0;i<n;i++)
    {
        p[i]=0;
    }
    preprocess(p, x, y, n);

    // Print number of points in a circle of
    // radius 3.
    document.write(query(p, n, 3)+"<br>");

    // Print number of points in a circle of
    // radius 32.
    document.write(query(p, n, 32)+"<br>");

    // This code is contributed by rag2127

</script>
```

**输出:**

```
3
5
```

**时间复杂度:** O(n log n)用于预处理，O(Q Log n)用于 Q 查询。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。