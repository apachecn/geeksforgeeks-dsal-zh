# 找出一个矩形插入另一个矩形后剩下的最小矩形数

> 原文:[https://www . geeksforgeeks . org/find-最小矩形数-一个插入另一个后向左/](https://www.geeksforgeeks.org/find-the-minimum-number-of-rectangles-left-after-inserting-one-into-another/)

给定 **N** 矩形的**宽度**和**高度**。任务是找到将一个矩形插入另一个矩形后剩余的最小矩形数。
**注:**

1.  如果 W1 < W2 且 H1 < H2，则矩形 1 适合矩形 2。
2.  最小的矩形可以插入第二小的，这个矩形可以插入下一个，以此类推。

**例:**

```
Input : arr[] = {{20, 30}, {10, 10}, {30, 20}, {40, 50}};
Output : 2
Explanation : One of the possible way is to insert 
second rectangle in first and then insert 
first rectangle in fourth. 
Then finally, third and fourth rectangles left.

Input : arr[] = {{10, 30}, {20, 20}, {30, 10}};
Output : 3
Explanation : Can't place any rectangle in any other one. 
So, three rectangles left.
```

**接近** :

1.  首先对所有矩形进行排序，使高度按降序排列。我们将首先假设每个高度都是唯一的(稍后我们将把我们的方法扩展到有相同高度的情况)。
2.  我们维护嵌套的另一个数组[i]。从最高的矩形向下到最短的矩形，我们将尝试在嵌套[i]中找到一个宽度大于当前矩形宽度的嵌套矩形，从而使矩形适合嵌套[i]。不仅如此，我们想把它放在宽度最小的那一个。然后，我们将矩形放入嵌套的矩形中，并更新其新的高度和重量。为什么是最小的那个？因为如果我们将矩形放置在另一个宽度大于最小宽度的矩形上，我们可以应用以下交换参数:
    让我们假设存在一个最优排列，使得当前矩形[i]不放置在满足上述要求的最小宽度的嵌套[m]上。假设矩形[i]放在嵌套[n]上，而另一个矩形[j]放在嵌套[m]上。那么由于矩形[j]可以适合嵌套[n]，它也可以适合嵌套[m]，因此我们可以交换矩形[i]和矩形[j]。通过在所有阶段对所有这样的矩形执行交换，我们可以将这个最优排列转换为我们的贪婪排列。因此我们贪婪的安排也是最优的。
3.  归纳起来，我们可以证明嵌套[i]中的矩形总是按宽度递增排序的。
4.  最后，在有一个高度相同的矩形的情况下，我们按照递增的顺序对宽度进行排序，以保持嵌套[i]的排序顺序。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find the minimum number of rectangles
// left after inserting one into another

#include <bits/stdc++.h>
using namespace std;

// Function for comparison
bool comp(const pair<int, int>& L, const pair<int, int>& R)
{
    if (L.first == R.first)
        return L.second > R.second;

    return L.first < R.first;
}

// Function to find the minimum number of rectangles
// left after inserting one into another
int Rectangles(pair<int, int> rectangle[], int n)
{
    // Sort rectangles in increasing order of width
    // and decreasing order of height
    sort(rectangle, rectangle + n, comp);

    vector<pair<int, int> > nested;

    // Keep the largest rectangle
    nested.push_back(rectangle[n - 1]);

    // For all remaining rectangles
    for (int i = n - 2; i >= 0; --i) {
        int high = nested.size() - 1, low = 0;

        // Find the position of this rectangle in nested
        while (low <= high) {
            int mid = (high + low) / 2;
            if (nested[mid].first == rectangle[i].first
                || nested[mid].second <= rectangle[i].second)
                low = mid + 1;

            else
                high = mid - 1;
        }

        // If this rectangle not possible to insert in
        // any other rectangle
        if (low == nested.size())
            nested.push_back(rectangle[i]);

        // Replace with previous rectangle
        else {
            nested[low].second = rectangle[i].second;
            nested[low].first = rectangle[i].first;
        }
    }

    return ((int)nested.size());
}

// Driver code
int main()
{
    // list of Width, Height pair
    pair<int, int> arr[] = { { 20, 30 }, { 10, 10 }, { 30, 20 }, { 40, 50 } };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << Rectangles(arr, n);

    return 0;
}
```

**Output:** 

```
2
```