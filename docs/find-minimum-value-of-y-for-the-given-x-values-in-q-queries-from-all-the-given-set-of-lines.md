# 从所有给定的行集合中找出 Q 查询中给定 x 值的 y 的最小值

> 原文:[https://www . geeksforgeeks . org/find-给定行集中所有给定查询的最小 y 值/](https://www.geeksforgeeks.org/find-minimum-value-of-y-for-the-given-x-values-in-q-queries-from-all-the-given-set-of-lines/)

给定由**斜率(m)** 和**截距(c)** 组成的二维数组 **arr[][]** ，用于大量行的形式 **y = mx + c** 和 **Q** 查询，使得每个查询包含值 **x** 。任务是从所有给定的线组中为给定的 **x** 值找到 **y** 的最小值。

**示例:**

> **输入:** arr[][] ={ {1，1}，{0，0}，{-3，3} }，Q = {-2，2，0}
> **输出:** -1，-3，0
> **解释:**
> 对于查询 x = -2，等式中的 y 值为-1，0，9。所以最小值为-1
> 同样，对于 x = 2，y 值为 3，0，-3。所以最小值是-3
> 对于 x = 0，y = 1，0，3 的值，所以最小值是 0。
> 
> **输入:** arr[][] ={ {5，6}，{3，2}，{7，3} }，Q = { 1，2，30 }
> **输出:** 5，8，92

**天真法:**天真法是将每一行的 x 值代入，计算所有行的最小值。对于每个查询，将花费 O(N)个时间，因此解决方案的复杂性变为 **O(Q * N)** ，其中 N 是行数，Q 是查询数。

**高效方法:**思路是用[凸包](https://www.geeksforgeeks.org/convex-hull-using-divide-and-conquer-algorithm/)的招数:

*   从给定的行集合中，可以找到并删除没有意义的行(对于任何 x 值，它们都不会给出最小值 y)，从而减少集合。
*   现在，如果可以找到每一行给出最小值的范围(l，r)，那么可以使用[二分搜索法来回答每个查询。](https://www.geeksforgeeks.org/binary-search/)
*   因此，创建了具有递减斜率顺序的排序的线向量，并且以递减斜率顺序插入线。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

struct Line {
    int m, c;

public:
    // Sort the line in decreasing
    // order of their slopes
    bool operator<(Line l)
    {

        // If slopes arent equal
        if (m != l.m)
            return m > l.m;

        // If the slopes are equal
        else
            return c > l.c;
    }

    // Checks if line L3 or L1 is better than L2
    // Intersection of Line 1 and
    // Line 2 has x-coordinate (b1-b2)/(m2-m1)
    // Similarly for Line 1 and
    // Line 3 has x-coordinate (b1-b3)/(m3-m1)
    // Cross multiplication will give the below result
    bool check(Line L1, Line L2, Line L3)
    {
        return (L3.c - L1.c) * (L1.m - L2.m)
               < (L2.c - L1.c) * (L1.m - L3.m);
    }
};

struct Convex_HULL_Trick {

    // To store the lines
    vector<Line> l;

    // Add the line to the set of lines
    void add(Line newLine)
    {

        int n = l.size();

        // To check if after adding the new line
        // whether old lines are
        // losing significance or not
        while (n >= 2
               && newLine.check(l[n - 2],
                                l[n - 1],
                                newLine)) {
            n--;
        }

        l.resize(n);

        // Add the present line
        l.push_back(newLine);
    }

    // Function to return the y coordinate
    // of the specified line for the given coordinate
    int value(int in, int x)
    {
        return l[in].m * x + l[in].c;
    }

    // Function to Return the minimum value
    // of y for the given x coordinate
    int minQuery(int x)
    {
        // if there is no lines
        if (l.empty())
            return INT_MAX;

        int low = 0, high = (int)l.size() - 2;

        // Binary search
        while (low <= high) {
            int mid = (low + high) / 2;

            if (value(mid, x) > value(mid + 1, x))
                low = mid + 1;
            else
                high = mid - 1;
        }

        return value(low, x);
    }
};

// Driver code
int main()
{
    Line lines[] = { { 1, 1 },
                     { 0, 0 },
                     { -3, 3 } };
    int Q[] = { -2, 2, 0 };
    int n = 3, q = 3;
    Convex_HULL_Trick cht;

    // Sort the lines
    sort(lines, lines + n);

    // Add the lines
    for (int i = 0; i < n; i++)
        cht.add(lines[i]);

    // For each query in Q
    for (int i = 0; i < q; i++) {
        int x = Q[i];
        cout << cht.minQuery(x) << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.ArrayList;
import java.util.Arrays;

class GFG{

static class Line implements Comparable<Line>
{
    int m, c;

    public Line(int m, int c)
    {
        this.m = m;
        this.c = c;
    }

    // Sort the line in decreasing
    // order of their slopes
    @Override
    public int compareTo(Line l)
    {

        // If slopes arent equal
        if (m != l.m)
            return l.m - this.m;

        // If the slopes are equal
        else
            return l.c - this.c;
    }

    // Checks if line L3 or L1 is better than L2
    // Intersection of Line 1 and
    // Line 2 has x-coordinate (b1-b2)/(m2-m1)
    // Similarly for Line 1 and
    // Line 3 has x-coordinate (b1-b3)/(m3-m1)
    // Cross multiplication will give the below result
    boolean check(Line L1, Line L2, Line L3)
    {
        return (L3.c - L1.c) * (L1.m - L2.m) <
               (L2.c - L1.c) * (L1.m - L3.m);
    }
}

static class Convex_HULL_Trick
{

    // To store the lines
    ArrayList<Line> l = new ArrayList<>();

    // Add the line to the set of lines
    void add(Line newLine)
    {
        int n = l.size();

        // To check if after adding the new
        // line whether old lines are
        // losing significance or not
        while (n >= 2 &&
               newLine.check(l.get(n - 2),
                             l.get(n - 1), newLine))
        {
            n--;
        }

        // l = new Line[n];

        // Add the present line
        l.add(newLine);
    }

    // Function to return the y coordinate
    // of the specified line for the given
    // coordinate
    int value(int in, int x)
    {
        return l.get(in).m * x + l.get(in).c;
    }

    // Function to Return the minimum value
    // of y for the given x coordinate
    int minQuery(int x)
    {

        // If there is no lines
        if (l.isEmpty())
            return Integer.MAX_VALUE;

        int low = 0, high = (int)l.size() - 2;

        // Binary search
        while (low <= high)
        {
            int mid = (low + high) / 2;

            if (value(mid, x) > value(mid + 1, x))
                low = mid + 1;
            else
                high = mid - 1;
        }
        return value(low, x);
    }
};

// Driver code
public static void main(String[] args)
{
    Line[] lines = { new Line(1, 1),
                     new Line(0, 0),
                     new Line(-3, 3) };
    int Q[] = { -2, 2, 0 };
    int n = 3, q = 3;

    Convex_HULL_Trick cht = new Convex_HULL_Trick();

    // Sort the lines
    Arrays.sort(lines);

    // Add the lines
    for(int i = 0; i < n; i++)
        cht.add(lines[i]);

    // For each query in Q
    for(int i = 0; i < q; i++)
    {
        int x = Q[i];
        System.out.println(cht.minQuery(x));
    }
}
}

// This code is contributed by sanjeev2552
```

**Output:** 

```
-1
-3
0
```