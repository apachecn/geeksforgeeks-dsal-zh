# 给定 N 个点可以形成的三角形数量

> 原文:[https://www . geeksforgeeks . org/给定 n 点可以形成的三角形数量/](https://www.geeksforgeeks.org/number-of-triangles-that-can-be-formed-with-given-n-points/)

给定笛卡尔平面上 N 个点的 X 和 Y 坐标。任务是找到非零面积的可能三角形的数量，这些三角形可以通过将每个点连接到其他点而形成。

**示例:**

```
Input: P[] = {{0, 0}, {2, 0}, {1, 1}, {2, 2}}
Output: 3
Possible triangles can be [(0, 0}, (2, 0), (1, 1)], 
[(0, 0), (2, 0), (2, 2)] and [(1, 1), (2, 2), (2, 0)]

Input : P[] = {{0, 0}, {2, 0}, {1, 1}}
Output : 1

```

在[笛卡尔坐标系中可能三角形的数量](https://www.geeksforgeeks.org/number-possible-triangles-cartesian-coordinate-system/)中已经讨论过一个**天真的方法**

**高效逼近**:考虑一个点 Z，求其与其他点的斜率。现在，如果两个点与 Z 点具有相同的斜率，这意味着这三个点是共线的，它们不能形成三角形。因此，将 Z 作为其一个点的三角形的数量是从剩余的点中选择 2 个点，然后从与 Z 具有相同斜率的点中减去选择 2 个点的方式的数量。由于 Z 可以是 N 个点中的任何一个点，所以我们必须再迭代一个循环。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// This function returns the required number
// of triangles
int countTriangles(pair<int, int> P[], int N)
{
    // Hash Map to store the frequency of
    // slope corresponding to a point (X, Y)
    map<pair<int, int>, int> mp;
    int ans = 0;

    // Iterate over all possible points
    for (int i = 0; i < N; i++) {
        mp.clear();

        // Calculate slope of all elements
        // with current element
        for (int j = i + 1; j < N; j++) {
            int X = P[i].first - P[j].first;
            int Y = P[i].second - P[j].second;

            // find the slope with reduced
            // fraction
            int g = __gcd(X, Y);
            X /= g;
            Y /= g;
            mp[{ X, Y }]++;
        }
        int num = N - (i + 1);

        // Total number of ways to form a triangle
        // having one point as current element
        ans += (num * (num - 1)) / 2;

        // Subtracting the total number of ways to
        // form a triangle having the same slope or are
        // collinear
        for (auto j : mp)
            ans -= (j.second * (j.second - 1)) / 2;
    }
    return ans;
}

// Driver Code to test above function
int main()
{
    pair<int, int> P[] = { { 0, 0 }, { 2, 0 }, { 1, 1 }, { 2, 2 } };
    int N = sizeof(P) / sizeof(P[0]);
    cout << countTriangles(P, N) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach 
from collections import defaultdict
from math import gcd

# This function returns the 
# required number of triangles 
def countTriangles(P, N): 

    # Hash Map to store the frequency of 
    # slope corresponding to a point (X, Y) 
    mp = defaultdict(lambda:0) 
    ans = 0

    # Iterate over all possible points 
    for i in range(0, N): 
        mp.clear() 

        # Calculate slope of all elements 
        # with current element 
        for j in range(i + 1, N): 
            X = P[i][0] - P[j][0] 
            Y = P[i][1] - P[j][1] 

            # find the slope with reduced 
            # fraction 
            g = gcd(X, Y) 
            X //= g 
            Y //= g 
            mp[(X, Y)] += 1

        num = N - (i + 1) 

        # Total number of ways to form a triangle 
        # having one point as current element 
        ans += (num * (num - 1)) // 2

        # Subtracting the total number of 
        # ways to form a triangle having 
        # the same slope or are collinear 
        for j in mp: 
            ans -= (mp[j] * (mp[j] - 1)) // 2

    return ans 

# Driver Code
if __name__ == "__main__": 

    P = [[0, 0], [2, 0], [1, 1], [2, 2]] 
    N = len(P) 
    print(countTriangles(P, N))

# This code is contributed by Rituraj Jain
```

**Output:**

```
3

```