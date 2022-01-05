# 计算给定直线在(I，0)和(j，1)之间的交点数量

> 原文:[https://www . geeksforgeeks . org/count-交叉数-i-0 和-j-1 之间给定线的点数/](https://www.geeksforgeeks.org/count-number-of-intersections-points-for-given-lines-between-i-0-and-j-1/)

给定形式为 **(i，j)** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)、**线【】**对，其中 **(i，j)** 表示从坐标 **(i，0)** 到 **(j，1)** 的线段，任务是找到给定线的交点的计数。

**示例:**

> **输入:**线[] = {{1，2}，{2，1}}
> **输出:** 1
> **解释:**对于给定的两对线，线的形式(1，0)到(2，1)在点(1.5，0.5)与从(2，0)到(1，1)的线相交。因此交叉点的总数是 1。
> 
> **输入:**行[] = {{1，5}，{2，1}，{3，7}，{4，1}，{8，2}}
> **输出:** 5

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)使用[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)来解决。可以观察到，对于 b 表示的线，两对 **(a，b)** 和 **(c，d)** 相交的 **(a > c 和 b < d)** 或 **(a < c 和 b > d)** 必须成立。

因此，使用这种观察，给定的对的[阵列可以按照**1<sup>ST</sup>T5】元素的降序排序**](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。遍历数组时，将第二个元素的值插入到基于策略的数据结构中，并使用 [order_of_key 函数](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)找到小于插入对的第二个元素的元素计数，并将计数的总和保存在变量中。同样，对给定的成对数组按其第 2 个<sup>和第 2 个</sup>元素的降序排序后的情况进行计算。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
using namespace __gnu_pbds;
using namespace std;

// Defining Policy Based Data Structure
typedef tree<int, null_type,
             less_equal<int>, rb_tree_tag,
             tree_order_statistics_node_update>
    ordered_multiset;

// Function to count points
// of intersection of pairs
// (a, b) and (c, d)
// such that a > c and b < d
int cntIntersections(
    vector<pair<int, int> > lines,
    int N)
{
    // Stores the count
    // of intersection points
    int cnt = 0;

    // Initializing Ordered Multiset
    ordered_multiset s;

    // Loop to iterate the array
    for (int i = 0; i < N; i++) {

        // Add the count of integers
        // smaller than lines[i].second
        // in the total count
        cnt += s.order_of_key(lines[i].second);

        // Insert lines[i].second into s
        s.insert(lines[i].second);
    }

    // Return Count
    return cnt;
}

// Function to find the
// total count of points of
// intersections of all the given lines
int cntAllIntersections(
    vector<pair<int, int> > lines,
    int N)
{
    // Sort the array in decreasing
    // order of 1st element
    sort(lines.begin(), lines.end(),
         greater<pair<int, int> >());

    // Stores the total count
    int totalCnt = 0;

    // Function call for cases
    // with a > c and b < d
    totalCnt += cntIntersections(lines, N);

    // Swap all the pairs of the array in order
    // to calculate cases with a < c and b > d
    for (int i = 0; i < N; i++) {
        swap(lines[i].first, lines[i].second);
    }

    // Function call for cases
    // with a < c and b > d
    totalCnt += cntIntersections(lines, N);

    // Return Answer
    return totalCnt;
}

// Driver Code
int main()
{
    vector<pair<int, int> > lines{
        {1, 5}, {2, 1}, {3, 7}, {4, 1}, {8, 2}
    };

    cout << cntAllIntersections(lines,
                                lines.size());

    return 0;
}
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*