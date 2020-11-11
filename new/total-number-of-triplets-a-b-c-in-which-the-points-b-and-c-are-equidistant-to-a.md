# `B`和`C`点与`A`等距的三元组`(A, B, C)`总数

> 原文：[https://www.geeksforgeeks.org/total-number-of-triplets-a-b-c-in-which-the-points-b-and-c-are-equidistant-to-a/](https://www.geeksforgeeks.org/total-number-of-triplets-a-b-c-in-which-the-points-b-and-c-are-equidistant-to-a/)

给定包含`N`个点的数组`arr`，任务是找到点等距的三元组总数。

> 当`P1`和`P2`之间的距离与`P1`和`P2`之间的距离相同时，点`(P1, P2, P3)`的**三元组被认为是等距的**。

**注意**：点的顺序很重要，即`(P1, P2, P3)`与`(P2, P3, P1)`不同。

**示例**：

> **输入**：`arr = [[0, 0], [1, 0], [2, 0]]`
>
> **输出**：2
>
> **说明**：
>
> 由于点的顺序很重要，因此我们有两组不同的点`[[1, 0], [0, 0], [2, 0]]`和`[[1, 0], [2,  0], [0, 0]]`，其中点是等距的。
> 
> **输入**：`arr = [[1, 1], [1, 3], [2, 0]]`
>
> **输出**：0
>
> **说明**：
>
> 不可能获得点等距的任何三元组。

**方法**：为了解决上述问题，我们知道三元组的顺序很重要，因此可能存在**不止一个相同三元组的排列**，满足点的等距偶对的条件。

*   首先，我们将[计算其中具有等距点的三元组的所有排列](https://www.geeksforgeeks.org/python-all-possible-permutations-of-n-lists/)。

*   对列表中每个不同的三元组点重复相同的过程。 为了计算距离，我们将使用各个坐标之间的距离的[平方](https://www.geeksforgeeks.org/program-distance-two-points-earth/)。

*   使用[**哈希映射**](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)存储单个三元组的各种等距点对。

*   一旦我们计算了对的总数，就会计算出所需的排列。 我们对所有不同的三元组重复此过程，并将所有排列添加到结果中。

**以下是上述方法的实现**：

```
// C++ implementation to Find
// the total number of Triplets
// in which the points are Equidistant
#include <bits/stdc++.h>
using namespace std;
// function to count such triplets
int numTrip(vector<pair< int , int > >& points)
{
int res = 0;
// Iterate over all the points
for ( int i = 0; i < points.size(); ++i) {
unordered_map< long , int >
map(points.size());
// Iterate over all points other
// than the current point
for ( int j = 0; j < points.size(); ++j) {
if (j == i)
continue ; [HTG1 69]
int dy = points[i].second
- points[j].second;
int dx = points[i].first
- points[j].first;
// Compute squared euclidean distance
// for the current point
]              int key = dy * dy;
key += dx * dx;
map[key]++;
}
for ( auto & p : map)
// Compute nP2 that is n * (n - 1)
res += p.second * (p.second - 1);
}
// Return the final result
return res;
}
// Driver code
int [H TG103]
{
vector<pair< int , int > > mat
= { { 0, 0 }, { 1, 0 }, { 2, 0 } };
cout << numTrip(mat);
return 0;
} ]
```

**输出**：

```
2

```

**时间复杂度**：`O(N ^ 2)`



* * *

* * *



