# 二进制数组范围查询寻找两个零之间的最小距离

> 原文:[https://www . geeksforgeeks . org/二进制数组范围查询查找两个零之间的最小距离/](https://www.geeksforgeeks.org/binary-array-range-queries-to-find-the-minimum-distance-between-two-zeros/)

**先决条件:** [分割树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
给定仅由 0 和 1 组成的二进制数组**arr【】**和由 K 个查询组成的 2D 数组**Q【】【】**，任务是为每个查询{L，R}在数组的范围【L，R】内找到两个 0 之间的最小距离。

**示例:**

> **输入:** arr[] = {1，0，0，1}，Q[][] = {{0，2}}
> **输出:** 1
> **解释:**
> 显然，在[0，2]范围内，第一个 0 位于索引 1，最后一个位于索引 2。
> 最小距离= 2–1 = 1。
> 
> **输入:** arr[] = {1，1，0，1，0，1，0，1，0，1，0，0，1，0}，Q[][] = {{3，9}，{10，13 } }
> T3】输出:2 3
> T6】说明:T8】在范围【3，9】内，0 之间的最小距离为 2(索引 4 和 6)。
> 在[10，13]范围内，0 之间的最小距离为 3(索引 10 和 13)。

**方法:**思路是用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)解决这个问题:

1.  段树中的每个节点将具有最左边的 0 和最右边的 0 的索引，以及包含子阵列{ 1，R}中 0 之间的最小距离的整数。
2.  设 min 为两个零之间的最小距离。然后，在形成段树后可以找到 min 的值为:
    min =最小值(左节点 min 的值，右节点 min 的值，右节点最左边索引 0 和左节点最右边索引 0 的差)。
3.  在计算并存储每个节点的最小距离后，所有查询都可以在对数时间内得到回答。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum
// distance between two elements
// with value 0 within a subarray (l, r)

#include <bits/stdc++.h>
using namespace std;

// Structure for each node
// in the segment tree
struct node {
    int l0, r0;
    int min0;
} seg[100001];

// A utility function for
// merging two nodes
node task(node l, node r)
{
    node x;

    x.l0 = (l.l0 != -1) ? l.l0 : r.l0;

    x.r0 = (r.r0 != -1) ? r.r0 : l.r0;

    x.min0 = min(l.min0, r.min0);

    // If both the nodes are valid
    if (l.r0 != -1 && r.l0 != -1)

        // Computing the minimum distance to store
        // in the segment tree
        x.min0 = min(x.min0, r.l0 - l.r0);

    return x;
}

// A recursive function that constructs
// Segment Tree for given string
void build(int qs, int qe, int ind, int arr[])
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {

        if (arr[qs] == 0) {
            seg[ind].l0 = seg[ind].r0 = qs;
            seg[ind].min0 = INT_MAX;
        }

        else {
            seg[ind].l0 = seg[ind].r0 = -1;
            seg[ind].min0 = INT_MAX;
        }

        return;
    }

    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // Merge the two child nodes
    // to obtain the parent node
    seg[ind] = task(seg[ind << 1],
                    seg[ind << 1 | 1]);
}

// Query in a range qs to qe
node query(int qs, int qe, int ns, int ne, int ind)
{
    node x;
    x.l0 = x.r0 = -1;
    x.min0 = INT_MAX;

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

    node l = query(qs, qe, ns, mid, ind << 1);
    node r = query(qs, qe, mid + 1, ne, ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
int main()
{

    int arr[] = { 1, 1, 0, 1, 0, 1,
                0, 1, 0, 1, 0, 1, 1, 0 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Build the segment tree
    build(0, n - 1, 1, arr);

    // Queries
    int Q[][2] = { { 3, 9 }, { 10, 13 } };

    for (int i = 0; i < 2; i++) {

// Finding the answer for every query
// and printing it
        node ans = query(Q[i][0], Q[i][1],
                        0, n - 1, 1);

        cout << ans.min0 << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// distance between two elements
// with value 0 within a subarray (l, r)
class GFG{

// Structure for each Node
// in the segment tree
static class Node
{
    int l0, r0;
    int min0;
};

static Node[] seg = new Node[100001];

// A utility function for
// merging two Nodes
static Node task(Node l, Node r)
{
    Node x = new Node();

    x.l0 = (l.l0 != -1) ? l.l0 : r.l0;

    x.r0 = (r.r0 != -1) ? r.r0 : l.r0;

    x.min0 = Math.min(l.min0, r.min0);

    // If both the Nodes are valid
    if (l.r0 != -1 && r.l0 != -1)

        // Computing the minimum distance to store
        // in the segment tree
        x.min0 = Math.min(x.min0, r.l0 - l.r0);

    return x;
}

// A recursive function that constructs
// Segment Tree for given string
static void build(int qs, int qe,
                  int ind, int arr[])
{

    // If start is equal to end then
    // insert the array element
    if (qs == qe)
    {
        if (arr[qs] == 0)
        {
            seg[ind].l0 = seg[ind].r0 = qs;
            seg[ind].min0 = Integer.MAX_VALUE;
        }

        else
        {
            seg[ind].l0 = seg[ind].r0 = -1;
            seg[ind].min0 = Integer.MAX_VALUE;
        }
        return;
    }

    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // Merge the two child Nodes
    // to obtain the parent Node
    seg[ind] = task(seg[ind << 1],
                    seg[ind << 1 | 1]);
}

// Query in a range qs to qe
static Node query(int qs, int qe, int ns,
                  int ne, int ind)
{
    Node x = new Node();
    x.l0 = x.r0 = -1;
    x.min0 = Integer.MAX_VALUE;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child Node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;

    Node l = query(qs, qe, ns, mid,
                          ind << 1);
    Node r = query(qs, qe, mid + 1,
                  ne, ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < 100001; i++)
    {
        seg[i] = new Node();
    }

    int arr[] = { 1, 1, 0, 1, 0, 1, 0,
                  1, 0, 1, 0, 1, 1, 0 };

    int n = arr.length;

    // Build the segment tree
    build(0, n - 1, 1, arr);

    // Queries
    int[][] Q = { { 3, 9 }, { 10, 13 } };

    for(int i = 0; i < 2; i++)
    {

        // Finding the answer for every query
        // and printing it
        Node ans = query(Q[i][0], Q[i][1],
                         0, n - 1, 1);

        System.out.println(ans.min0);
    }
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# distance between two elements with
# value 0 within a subarray (l, r)
import sys

# Structure for each node
# in the segment tree
class node():

    def __init__(self):

        self.l0 = 0
        self.r0 = 0
        min0 = 0

seg = [node() for i in range(100001)]

# A utility function for
# merging two nodes
def task(l, r):

    x = node()

    x.l0 = l.l0 if (l.l0 != -1) else r.l0
    x.r0 = r.r0 if (r.r0 != -1)  else l.r0

    x.min0 = min(l.min0, r.min0)

    # If both the nodes are valid
    if (l.r0 != -1 and r.l0 != -1):

        # Computing the minimum distance to
        # store in the segment tree
        x.min0 = min(x.min0, r.l0 - l.r0)

    return x

# A recursive function that constructs
# Segment Tree for given string
def build(qs, qe, ind, arr):

    # If start is equal to end then
    # insert the array element
    if (qs == qe):

        if (arr[qs] == 0):
            seg[ind].l0 = seg[ind].r0 = qs
            seg[ind].min0 = sys.maxsize

        else:
            seg[ind].l0 = seg[ind].r0 = -1
            seg[ind].min0 = sys.maxsize

        return

    mid = (qs + qe) >> 1

    # Build the segment tree
    # for range qs to mid
    build(qs, mid, ind << 1, arr)

    # Build the segment tree
    # for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr)

    # Merge the two child nodes
    # to obtain the parent node
    seg[ind] = task(seg[ind << 1],
                    seg[ind << 1 | 1])

# Query in a range qs to qe
def query(qs, qe, ns, ne, ind):

    x = node()
    x.l0 = x.r0 = -1
    x.min0 = sys.maxsize

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

    l = query(qs, qe, ns, mid, ind << 1)
    r = query(qs, qe, mid + 1, ne, ind << 1 | 1)

    x = task(l, r)

    return x

# Driver code 
if __name__=="__main__":

    arr = [ 1, 1, 0, 1, 0, 1, 0,
            1, 0, 1, 0, 1, 1, 0 ]

    n = len(arr)

    # Build the segment tree
    build(0, n - 1, 1, arr)

    # Queries
    Q = [ [ 3, 9 ], [ 10, 13 ] ]

    for i in range(2):

        # Finding the answer for every query
        # and printing it
        ans = query(Q[i][0], Q[i][1], 0,
                    n - 1, 1)

        print(ans.min0)

# This code is contributed by rutvik_56
```

**输出:**

```
2
3
```