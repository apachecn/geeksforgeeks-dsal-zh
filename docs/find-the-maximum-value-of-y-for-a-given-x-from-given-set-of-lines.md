# 从给定的一组线中找出给定 X 的最大 Y 值

> 原文:[https://www . geeksforgeeks . org/从给定的行集中找到给定 x 的最大 y 值/](https://www.geeksforgeeks.org/find-the-maximum-value-of-y-for-a-given-x-from-given-set-of-lines/)

给定一组由二维数组**表示的线，数组**分别由**斜率(m)** 和**截距(c)** 和 **Q** 查询组成，使得每个查询包含一个值 **x** 。任务是从所有给定的一组线中为 **x** 的每个值找到 **y** 的最大值。

> 给定的线由等式 **y = m*x + c** 表示。

**示例:**

> **输入:** arr[][2] ={ {1，1}，{0，0}，{-3，3} }，Q = {-2，2，1}
> **输出:** 9，3，2
> 对于查询 x = -2，等式中的 y 值为-1，0，9。所以最大值为 9
> 同样，对于 x = 2，y 值为 3，0，-3。所以最大值是 3
> 对于 x = 1，y = 2，0，0 的值。所以最大值是 2。
> 
> **输入:** arr[][] ={ {5，6}，{3，2}，{7，3} }，Q = { 1，2，30 }
> **输出:** 10，17，213

**天真法:**天真法是在每一行中代入 **x** 的值，计算所有行的最大值。对于每个查询，将花费 **O(N)** 时间，因此解决方案的复杂性变为 **O(Q * N)** ，其中 **N** 是行数， **Q** 是查询数。

**高效方法:**思路是使用[凸包绝招:](https://www.geeksforgeeks.org/convex-hull-set-1-jarviss-algorithm-or-wrapping/)

*   从给定的行集合中，可以找到并删除没有意义的行(对于 **x** 的任何值，它们从不给出最大值 **y** ，从而减少集合。
*   现在，如果可以找到每一行给出最大值的范围 **(l，r)** ，那么可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来回答每个查询。
*   因此，创建具有递减斜率顺序的线的[排序向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)，并且以递减斜率顺序插入线。

下面是上述方法的实现:

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

struct Line {
    int m, c;

public:
    // Sort the line in decreasing
    // order of their slopes
    bool operator<(Line l)
    {

        // If slopes aren't equal
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
    // Cross multiplication will
    // give the below result
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
    // of the specified line
    // for the given coordinate
    int value(int in, int x)
    {
        return l[in].m * x + l[in].c;
    }

    // Function to Return the maximum value
    // of y for the given x coordinate
    int maxQuery(int x)
    {
        // if there is no lines
        if (l.empty())
            return INT_MAX;

        int low = 0,
            high = (int)l.size() - 2;

        // Binary search
        while (low <= high) {
            int mid = (low + high) / 2;

            if (value(mid, x)
                < value(mid + 1, x))
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
    int Q[] = { -2, 2, 1 };
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
        cout << cht.maxQuery(x) << endl;
    }

    return 0;
}
```

**Output:**

```
9
3
2

```