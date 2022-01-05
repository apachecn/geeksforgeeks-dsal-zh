# 给定点集合的凸包周长

> 原文:[https://www . geeksforgeeks . org/给定点集凸包周长/](https://www.geeksforgeeks.org/perimeter-of-convex-hull-for-a-given-set-of-points/)

给定 **n** 2-D 点**点【】**，任务是找到这组点的凸包周长。一组点的凸包是包含所有点的最小凸多边形。

**示例:**

> **输入:**点数[] = {{0，3}，{2，2}，{1，1}，{2，1}，{3，0}，{0，0}，{3，3}}
> **输出:** 12
> 
> **输入:**点数[] = {{0，2}，{2，1}，{3，1}，{3，7 } }
> T3】输出: 15.067

**逼近:** [单调链算法](https://en.wikibooks.org/wiki/Algorithm_Implementation/Geometry/Convex_hull/Monotone_chain)在 **O(n * log(n))** 时间构造凸包。我们必须先对点进行排序，然后在 **O(n)** 时间内计算上下船体。这些点将根据 x 坐标进行排序(在 x 坐标相同的情况下，根据 y 坐标)，然后我们将找到最左边的点，然后尝试顺时针旋转并找到下一个点，然后重复该步骤，直到我们到达最右边的点，然后再次顺时针旋转并找到下船体。
然后我们将使用凸包上的点来找到凸包的周长，这可以在 **O(n)** 时间内完成，因为点已经按顺时针顺序排序了。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define llu long long int
using namespace std;

struct Point {

    llu x, y;

    bool operator<(Point p)
    {
        return x < p.x || (x == p.x && y < p.y);
    }
};

// Cross product of two vectors OA and OB
// returns positive for counter clockwise
// turn and negative for clockwise turn
llu cross_product(Point O, Point A, Point B)
{
    return (A.x - O.x) * (B.y - O.y)
           - (A.y - O.y) * (B.x - O.x);
}

// Returns a list of points on the convex hull
// in counter-clockwise order
vector<Point> convex_hull(vector<Point> A)
{
    int n = A.size(), k = 0;

    if (n <= 3)
        return A;

    vector<Point> ans(2 * n);

    // Sort points lexicographically
    sort(A.begin(), A.end());

    // Build lower hull
    for (int i = 0; i < n; ++i) {

        // If the point at K-1 position is not a part
        // of hull as vector from ans[k-2] to ans[k-1]
        // and ans[k-2] to A[i] has a clockwise turn
        while (k >= 2
               && cross_product(ans[k - 2], 
                            ans[k - 1], A[i]) <= 0)
            k--;
        ans[k++] = A[i];
    }

    // Build upper hull
    for (size_t i = n - 1, t = k + 1; i > 0; --i) {

        // If the point at K-1 position is not a part
        // of hull as vector from ans[k-2] to ans[k-1]
        // and ans[k-2] to A[i] has a clockwise turn
        while (k >= t
               && cross_product(ans[k - 2], 
                          ans[k - 1], A[i - 1]) <= 0)
            k--;
        ans[k++] = A[i - 1];
    }

    // Resize the array to desired size
    ans.resize(k - 1);

    return ans;
}

// Function to return the distance between two points
double dist(Point a, Point b)
{
    return sqrt((a.x - b.x) * (a.x - b.x)
                + (a.y - b.y) * (a.y - b.y));
}

// Function to return the perimeter of the convex hull
double perimeter(vector<Point> ans)
{
    double perimeter = 0.0;

    // Find the distance between adjacent points
    for (int i = 0; i < ans.size() - 1; i++) {
        perimeter += dist(ans[i], ans[i + 1]);
    }

    // Add the distance between first and last point
    perimeter += dist(ans[0], ans[ans.size() - 1]);

    return perimeter;
}

// Driver code
int main()
{
    vector<Point> points;

    // Add points
    points.push_back({ 0, 3 });
    points.push_back({ 2, 2 });
    points.push_back({ 1, 1 });
    points.push_back({ 2, 1 });
    points.push_back({ 3, 0 });
    points.push_back({ 0, 0 });
    points.push_back({ 3, 3 });

    // Find the convex hull
    vector<Point> ans = convex_hull(points);

    // Find the perimeter of convex polygon
    cout << perimeter(ans);

    return 0;
}
```

**Output:**

```
12

```