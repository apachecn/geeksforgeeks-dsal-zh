# 使用段树

查询给定索引范围内的最大对和

> 原文:[https://www . geesforgeks . org/查询给定索引范围内最大对和使用段树/](https://www.geeksforgeeks.org/queries-for-greatest-pair-sum-in-the-given-index-range-using-segment-tree/)

给定一个包含 **N** 整数的数组**arr【】**和一个代表范围**【L，R】**的数组**Q【】**，任务是找到范围**【L，R】**中最大的对和值，其中 0≤L≤R≤N–1。

**示例:**

> **输入:** arr[] = {1，3，2，7，9，11}，Q[] = {1，4}
> **输出:** 16
> **解释:**
> 1 到 4 范围内最大的对和为 7 + 9 = 16。
> 
> **输入:** arr[] = {0，1，2，3，4，5，6，7}，Q[] = {5，7}
> **输出:** 13
> **解释:**
> 5 到 7 范围内最大的对和为 6 + 7 = 13。

**天真法:**这个问题的天真法是从[L，R]开始运行一个循环，找出给定范围内最大的两个元素。它们的和总是给定指数范围内最大的对和。这种方法的时间复杂度是每个查询的 **O(N)** 。

**高效方法:**想法是使用 [**段树**](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/ "Segment Tree") 来执行一些预处理，并在对数时间内找到每个查询的值。

**段树的表示:**

1.  叶节点是输入数组的元素。
2.  每个内部节点包含最大对和以及其下所有叶子的最大元素。

树的数组表示用于表示[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。对于索引“I”处的每个节点，左边的子节点位于索引 **((2 * i) + 1)** ，右边的子节点位于索引 **((2 * i) + 2)** ，父节点位于索引**((I–1)/2)**。

**从给定数组构建段树:**

*   我们从给定数组 arr[]的一个段开始。
*   在每一步，我们将当前片段分成两半(如果它还没有变成长度为 1 的片段)。
*   对获得的数组的一半递归地执行上述步骤。
*   对于每个段，我们在段树节点中存储最大值和最大对和。
*   The maximum pair sum and the maximum value for every node can be found as:

    > maximum pair sum-> maximum value (left child maximum pair sum, right child maximum pair sum, left child maximum plus right child maximum)
    > 
    > maximum value-> maximum value (left child

下面是上述方法的实现:

```
// C++ program for range greatest
// pair sum query using segment tree

#include <bits/stdc++.h>
using namespace std;

// Defining the node
struct node {
    int maxVal, greatestPSum;
} st[100009];

// A utility function
node util(node x, node y)
{
    node ans;

    // Find the maximum pair sum
    ans.greatestPSum
        = max(x.maxVal + y.maxVal,
              max(x.greatestPSum,
                  y.greatestPSum));
    // Find the maximum value
    ans.maxVal = max(x.maxVal, y.maxVal);
    return ans;
}

// A utility function to get the
// middle index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* A recursive function to get the
greatest pair sum value in a given range 
of array indexes. Here:

index --> Index of current node in the 
          segment tree. Initially 0 is 
          passed as root is always at index 0 
ss & se --> Starting and ending indexes 
            of the segment represented 
            by current node, i.e., st[index] 
qs & qe --> Starting and ending indexes
            of query range */
node query(int ss, int se, int qs,
           int qe, int index)
{
    // If segment of this node is a part
    // of given range, then return
    // the min of the segment
    if (qs <= ss && qe >= se)
        return st[index];

    node temp;
    temp.maxVal = -1,
    temp.greatestPSum = -1;

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return temp;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return util(query(ss, mid, qs,
                      qe, 2 * index + 1),

                query(mid + 1, se, qs,
                      qe, 2 * index + 2));
}

// Function to return the greatest pair
// sum in the range from index
// qs (query start) to qe (query end)
node checkQuery(int n, int qs, int qe)
{
    node temp;
    temp.maxVal = -1, temp.greatestPSum = -1;

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe) {
        cout << "Invalid Input";
        return temp;
    }

    return query(0, n - 1, qs, qe, 0);
}

// A recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node in segment tree
node constructST(int arr[], int ss,
                 int se, int si)
{
    // If there is one element in array,
    // store it in current node of
    // segment tree and return
    if (ss == se) {
        st[si].maxVal = arr[ss];
        st[si].greatestPSum = 0;
        return st[si];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    int mid = getMid(ss, se);
    st[si] = util(constructST(arr, ss, mid,
                              si * 2 + 1),

                  constructST(arr, mid + 1, se,
                              si * 2 + 2));
    return st[si];
}

// Utility function to find the
// greatest pair sum for the given
// queries
void operation(int arr[], int n,
               int qs, int qe)
{
    // Build segment tree from given array
    constructST(arr, 0, n - 1, 0);

    node ans = checkQuery(n, qs, qe);

    // Print minimum value in arr[qs..qe]
    cout << ans.greatestPSum << endl;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 7, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int L = 1;
    int R = 4;

    operation(arr, n, L, R);

    return 0;
}
```

**Output:**

```
16

```

**时间复杂度:**

*   树构造的时间复杂度是 *O(N)* ，其中 N 是数组的大小。
*   每个查询的时间复杂度为 *O(log(N))* ，其中 N 是数组的大小。