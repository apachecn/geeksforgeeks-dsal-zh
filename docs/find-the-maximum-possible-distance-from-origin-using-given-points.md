# 使用给定点找到离原点的最大可能距离

> 原文:[https://www . geeksforgeeks . org/使用给定的点找到离原点的最大可能距离/](https://www.geeksforgeeks.org/find-the-maximum-possible-distance-from-origin-using-given-points/)

给定 **N** 个二维点。任务是使用给定点找到离原点的最大可能距离。使用**I<sup>th</sup>T5**(x<sub>I</sub>，y <sub>i</sub> )** 可以从 **(a，b)** 移动到 **(a + x <sub>i</sub> ，b + y <sub>i</sub> )** 。
**注:** **N** 位于 **1** 至 **1000** 之间，每个点最多可以使用一次。**

**示例:**

> **输入:** arr[][] = {{1，1}，{2，2}，{3，3}，{4，4}}
> **输出:** 14.14
> 我们能移动到的最远的点是(10，10)。
> 
> **输入:** arr[][] = {{0，10}，{5，-5}，{-5，-5 } }
> T3】输出: 10.00

**方法:**关键的观察是，当点按其向量与 x 轴的角度排序时，答案将包括一些连续范围内的向量。这个事实的证明可以从[这里](https://math.stackexchange.com/questions/730611/maximizing-the-magnitude-of-the-resultant-vector)阅读。那么，解决方案相当容易实现。迭代所有可能的范围，计算每个范围的答案，取最大值作为结果。如果实施得当，这是一种 O(N <sup>2</sup> )方法。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible
// distance from origin using given points.
void Max_Distance(vector<pair<int, int> >& xy, int n)
{
    // Sort the points with their tan angle
    sort(xy.begin(), xy.end(), [](const pair<int, int>& l,
                                  const pair<int, int>& r) {
        return atan2l(l.second, l.first)
               < atan2l(r.second, r.first);
    });

    // Push the whole vector
    for (int i = 0; i < n; i++)
        xy.push_back(xy[i]);

    // To store the required answer
    int res = 0;

    // Find the maximum possible answer
    for (int i = 0; i < n; i++) {
        int x = 0, y = 0;
        for (int j = i; j < i + n; j++) {
            x += xy[j].first;
            y += xy[j].second;
            res = max(res, x * x + y * y);
        }
    }

    // Print the required answer
    cout << fixed << setprecision(2) << sqrtl(res);
}

// Driver code
int main()
{
    vector<pair<int, int> > vec = { { 1, 1 },
                                    { 2, 2 },
                                    { 3, 3 },
                                    { 4, 4 } };

    int n = vec.size();

    // Function call
    Max_Distance(vec, n);

    return 0;
}
```

**Output:**

```
14.14

```