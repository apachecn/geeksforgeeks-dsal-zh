# 二进制数组中与 1 异或的范围更新查询。

> 原文:[https://www . geesforgeks . org/range-update-query-to-xor-with-in-1-in-a-binary-array/](https://www.geeksforgeeks.org/range-update-queries-to-xor-with-1-in-a-binary-array/)

给定大小为 **N** 的二进制数组 **arr[]** 。任务是回答 **Q** 的查询，可以是下面的任何一种类型:
**类型 1–1l r:**用 1 对从 l 到 r 的所有数组元素执行按位异或运算。
**类型 2–2l r:**返回子数组[l，r]中值为 1 的两个元素之间的最小距离。
**类型 3–3l r:**返回子数组[l，r]中值为 1 的两个元素之间的最大距离。
**类型 4–4l r:**返回子数组[l，r]中值为 0 的两个元素之间的最小距离。
**类型 5–5l r:**返回子数组[l，r]中值为 0 的两个元素之间的最大距离。
**例:**

> **输入:** arr[] = {1，1，0，1，0，1，0，1，0，1，0}，q=5
> **输出:** 2 2 3 2
> **解释:**
> **查询 1 :** 类型 2，l=3，r=7
> 范围 3 到 7 包含{1，0，1，0，1 }。
> 所以，值为 1 的两个元素之间的最小距离为 2。
> **查询 2 :** 类型 3，l=2，r=5
> 范围 2 到 5 包含{ 0，1，0，1 }。
> 所以，值为 1 的两个元素之间的最大距离为 2。
> **查询 3 :** 类型 1，l=1，r=4
> 更新后数组变为{1，0，1，0，1，1，0，1，0，1，0，0，0，0，1，1，1，1，1，0}
> **查询 4 :** 类型 4，l=3，r=7
> 更新后数组中的范围 3 到 7 包含{ 0，1，1，0，1 }。
> 所以，值为 0 的两个元素之间的最小距离为 3。
> **查询 5 :** 类型 5，l=4，r=9
> 范围 4 到 9 包含{ 1，1，0，1，0，1 }。
> 所以，值为 0 的两个元素之间的最大距离为 2。

**方法:**
我们将创建一个[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)并使用范围更新配合[惰性传播](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)来解决这个问题。

*   段树中的每个节点将具有最左 1 和最右 1 的索引，最左 0 和最右 0 以及整数，包含子阵列{l，r}中值为 1 的任何元素之间的最大和最小距离，以及子阵列[中值为 0 的任何元素之间的最大和最小距离。](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) 
*   现在，在这个段树中，我们可以合并左节点和右节点，如下所示:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// l1 = leftmost index of 1, l0 = leftmost index of 0.
// r1 = rightmost index of 1, r0 = rightmost index of 0.
// max1 = maximum distance between two 1’s.
// max0 = maximum distance between two 0’s.
// min1 = minimum distance between two 1’s.
// min0 = minimum distance between two 0’s.
node Merge(node left, node right)
{
    node cur;

    if left.l0 is valid
        cur.l0 = left.l0
    else
        cur.l0 = r.l0
    // We will do this for all values
    // i.e. cur.r0, cur.l1, cur.r1, cur.l0

    // To find the min and max difference between two 1's and 0's
    // we will take min/max value of left side, right side and
    // difference between rightmost index of 1/0 in right node
    // and leftmost index of 1/0 in left node respectively.

     cur.min0 = minimum of left.min0 and right.min0

     if left.r0 is valid and right.l0 is valid
        cur.min0 = minimum of cur.min0 and (right.l0 - left.r0)
    // We will do this for all max/min values
    // i.e. cur.min0, cur.min1, cur.max1, cur.max0

    return cur;
}
```

*   为了处理范围更新查询，我们将使用惰性传播。更新查询要求我们将从 l 到 r 范围内的所有元素与 1 进行异或运算，根据观察，我们知道:

```
       0 xor 1 = 1
       1 xor 1 = 0
```

*   因此，我们可以观察到，在这次更新之后，所有的 0 将变为 1，所有的 1 将变为 0。因此，在我们的段树节点中，0 和 1 的所有对应值也将被交换，即

```
       l0 and l1 will get swapped
       r0 and r1 will get swapped
       min0 and min1 will get swapped
       max0 and max1 will get swapped
```

*   然后，最后为了找到任务 2、3、4 和 5 的答案，我们只需要调用给定范围{l，r}的查询函数，为了找到任务 1 的答案，我们需要调用范围更新函数。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the given problem
#include <bits/stdc++.h>
using namespace std;

int lazy[100001];

// Class for each node
// in the segment tree
class node {
public:
    int l1, r1, l0, r0;
    int min0, max0, min1, max1;

    node()
    {
        l1 = r1 = l0 = r0 = -1;

        max1 = max0 = INT_MIN;
        min1 = min0 = INT_MAX;
    }

} seg[100001];

// A utility function for
// merging two nodes
node MergeUtil(node l, node r)
{
    node x;

    x.l0 = (l.l0 != -1) ? l.l0 : r.l0;
    x.r0 = (r.r0 != -1) ? r.r0 : l.r0;

    x.l1 = (l.l1 != -1) ? l.l1 : r.l1;
    x.r1 = (r.r1 != -1) ? r.r1 : l.r1;

    x.min0 = min(l.min0, r.min0);
    if (l.r0 != -1 && r.l0 != -1)
        x.min0 = min(x.min0, r.l0 - l.r0);

    x.min1 = min(l.min1, r.min1);
    if (l.r1 != -1 && r.l1 != -1)
        x.min1 = min(x.min1, r.l1 - l.r1);

    x.max0 = max(l.max0, r.max0);
    if (l.l0 != -1 && r.r0 != -1)
        x.max0 = max(x.max0, r.r0 - l.l0);

    x.max1 = max(l.max1, r.max1);
    if (l.l1 != -1 && r.r1 != -1)
        x.max1 = max(x.max1, r.r1 - l.l1);

    return x;
}

// utility function
// for updating a node
node UpdateUtil(node x)
{
    swap(x.l0, x.l1);
    swap(x.r0, x.r1);
    swap(x.min1, x.min0);
    swap(x.max0, x.max1);

    return x;
}

// A recursive function that constructs
// Segment Tree for given string
void Build(int qs, int qe, int ind, int arr[])
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {
        if (arr[qs] == 1) {
            seg[ind].l1 = seg[ind].r1 = qs;
        }
        else {
            seg[ind].l0 = seg[ind].r0 = qs;
        }

        lazy[ind] = 0;
        return;
    }
    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    Build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    Build(mid + 1, qe, ind << 1 | 1, arr);

    // merge the two child nodes
    // to obtain the parent node
    seg[ind] = MergeUtil(
        seg[ind << 1],
        seg[ind << 1 | 1]);
}

// Query in a range qs to qe
node Query(int qs, int qe,
           int ns, int ne, int ind)
{
    if (lazy[ind] != 0) {
        seg[ind] = UpdateUtil(seg[ind]);
        if (ns != ne) {
            lazy[ind * 2] ^= lazy[ind];
            lazy[ind * 2 + 1] ^= lazy[ind];
        }
        lazy[ind] = 0;
    }

    node x;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;

    node l = Query(qs, qe, ns,
                   mid, ind << 1);
    node r = Query(qs, qe,
                   mid + 1, ne,
                   ind << 1 | 1);

    x = MergeUtil(l, r);
    return x;
}

// range update using lazy propagation
void RangeUpdate(int us, int ue,
                 int ns, int ne, int ind)
{
    if (lazy[ind] != 0) {
        seg[ind] = UpdateUtil(seg[ind]);
        if (ns != ne) {
            lazy[ind * 2] ^= lazy[ind];
            lazy[ind * 2 + 1] ^= lazy[ind];
        }
        lazy[ind] = 0;
    }

    // If the range is out of the bounds
    // of this segment
    if (ns > ne || ns > ue || ne < us)
        return;

    // If the range lies in this segment
    if (ns >= us && ne <= ue) {
        seg[ind] = UpdateUtil(seg[ind]);
        if (ns != ne) {
            lazy[ind * 2] ^= 1;
            lazy[ind * 2 + 1] ^= 1;
        }
        return;
    }

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;
    RangeUpdate(us, ue, ns, mid, ind << 1);
    RangeUpdate(us, ue, mid + 1, ne, ind << 1 | 1);

    node l = seg[ind << 1], r = seg[ind << 1 | 1];
    seg[ind] = MergeUtil(l, r);
}

// Driver code
int main()
{

    int arr[] = { 1, 1, 0,
                  1, 0, 1,
                  0, 1, 0,
                  1, 0, 1,
                  1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build the segment tree
    Build(0, n - 1, 1, arr);

    // Query of Type 2 in the range 3 to 7
    node ans = Query(3, 7, 0, n - 1, 1);
    cout << ans.min1 << "\n";

    // Query of Type 3 in the range 2 to 5
    ans = Query(2, 5, 0, n - 1, 1);
    cout << ans.max1 << "\n";

    // Query of Type 1 in the range 1 to 4
    RangeUpdate(1, 4, 0, n - 1, 1);

    // Query of Type 4 in the range 3 to 7
    ans = Query(3, 7, 0, n - 1, 1);
    cout << ans.min0 << "\n";

    // Query of Type 5 in the range 4 to 9
    ans = Query(4, 9, 0, n - 1, 1);
    cout << ans.max0 << "\n";

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the given problem
from sys import maxsize
from typing import List
INT_MAX = maxsize
INT_MIN = -maxsize
lazy = [0 for _ in range(100001)]

# Class for each node
# in the segment tree
class node:
    def __init__(self) -> None:
        self.l1 = self.r1 = self.l0 = self.r0 = -1
        self.max0 = self.max1 = INT_MIN
        self.min0 = self.min1 = INT_MAX

seg = [node() for _ in range(100001)]

# A utility function for
# merging two nodes
def MergeUtil(l: node, r: node) -> node:
    x = node()

    x.l0 = l.l0 if (l.l0 != -1) else r.l0
    x.r0 = r.r0 if (r.r0 != -1) else l.r0

    x.l1 = l.l1 if (l.l1 != -1) else r.l1
    x.r1 = r.r1 if (r.r1 != -1) else l.r1

    x.min0 = min(l.min0, r.min0)
    if (l.r0 != -1 and r.l0 != -1):
        x.min0 = min(x.min0, r.l0 - l.r0)

    x.min1 = min(l.min1, r.min1)
    if (l.r1 != -1 and r.l1 != -1):
        x.min1 = min(x.min1, r.l1 - l.r1)

    x.max0 = max(l.max0, r.max0)
    if (l.l0 != -1 and r.r0 != -1):
        x.max0 = max(x.max0, r.r0 - l.l0)

    x.max1 = max(l.max1, r.max1)
    if (l.l1 != -1 and r.r1 != -1):
        x.max1 = max(x.max1, r.r1 - l.l1)

    return x

# utility function
# for updating a node
def UpdateUtil(x: node) -> node:
    x.l0, x.l1 = x.l1, x.l0
    x.r0, x.r1 = x.r1, x.r0
    x.min1, x.min0 = x.min0, x.min1
    x.max0, x.max1 = x.max1, x.max0

    return x

# A recursive function that constructs
# Segment Tree for given string
def Build(qs: int, qe: int, ind: int, arr: List[int]) -> None:

  # If start is equal to end then
    # insert the array element
    if (qs == qe):
        if (arr[qs] == 1):
            seg[ind].l1 = seg[ind].r1 = qs
        else:
            seg[ind].l0 = seg[ind].r0 = qs

        lazy[ind] = 0
        return

    mid = (qs + qe) >> 1

    # Build the segment tree
    # for range qs to mid
    Build(qs, mid, ind << 1, arr)

    # Build the segment tree
    # for range mid+1 to qe
    Build(mid + 1, qe, ind << 1 | 1, arr)

    # merge the two child nodes
    # to obtain the parent node
    seg[ind] = MergeUtil(seg[ind << 1], seg[ind << 1 | 1])

# Query in a range qs to qe
def Query(qs: int, qe: int, ns: int, ne: int, ind: int) -> node:
    if (lazy[ind] != 0):
        seg[ind] = UpdateUtil(seg[ind])
        if (ns != ne):
            lazy[ind * 2] ^= lazy[ind]
            lazy[ind * 2 + 1] ^= lazy[ind]
        lazy[ind] = 0
    x = node()

    # If the range lies in this segment
    if (qs <= ns and qe >= ne):
        return seg[ind]

    # If the range is out of the bounds
    # of this segment
    if (ne < qs or ns > qe or ns > ne):
        return x

    # Else query for the right and left
    # child node of this subtree
    # and merge them
    mid = (ns + ne) >> 1
    l = Query(qs, qe, ns, mid, ind << 1)
    r = Query(qs, qe, mid + 1, ne, ind << 1 | 1)
    x = MergeUtil(l, r)
    return x

# range update using lazy prpagation
def RangeUpdate(us: int, ue: int, ns: int, ne: int, ind: int) -> None:
    if (lazy[ind] != 0):
        seg[ind] = UpdateUtil(seg[ind])
        if (ns != ne):
            lazy[ind * 2] ^= lazy[ind]
            lazy[ind * 2 + 1] ^= lazy[ind]
        lazy[ind] = 0

    # If the range is out of the bounds
    # of this segment
    if (ns > ne or ns > ue or ne < us):
        return

    # If the range lies in this segment
    if (ns >= us and ne <= ue):
        seg[ind] = UpdateUtil(seg[ind])
        if (ns != ne):
            lazy[ind * 2] ^= 1
            lazy[ind * 2 + 1] ^= 1
        return

    # Else query for the right and left
    # child node of this subtree
    # and merge them
    mid = (ns + ne) >> 1
    RangeUpdate(us, ue, ns, mid, ind << 1)
    RangeUpdate(us, ue, mid + 1, ne, ind << 1 | 1)
    l = seg[ind << 1]
    r = seg[ind << 1 | 1]
    seg[ind] = MergeUtil(l, r)

# Driver code
if __name__ == "__main__":
    arr = [1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0]
    n = len(arr)

    # Build the segment tree
    Build(0, n - 1, 1, arr)

    # Query of Type 2 in the range 3 to 7
    ans = Query(3, 7, 0, n - 1, 1)
    print(ans.min1)

    # Query of Type 3 in the range 2 to 5
    ans = Query(2, 5, 0, n - 1, 1)
    print(ans.max1)

    # Query of Type 1 in the range 1 to 4
    RangeUpdate(1, 4, 0, n - 1, 1)

    # Query of Type 4 in the range 3 to 7
    ans = Query(3, 7, 0, n - 1, 1)
    print(ans.min0)

    # Query of Type 5 in the range 4 to 9
    ans = Query(4, 9, 0, n - 1, 1)
    print(ans.max0)

# This code is contributed by sanjeev2552
```

**Output:** 

```
2
2
3
2
```