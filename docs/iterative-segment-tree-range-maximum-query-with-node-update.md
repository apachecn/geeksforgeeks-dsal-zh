# 迭代段树(带节点更新的范围最大查询)

> 原文:[https://www . geesforgeks . org/iterative-segment-tree-range-maximum-query-with-node-update/](https://www.geeksforgeeks.org/iterative-segment-tree-range-maximum-query-with-node-update/)

给定数组 arr[0。。。n-1]。任务是执行以下操作:

*   求从索引 l 到 r 的元素的最大值，其中 0 <= l <= r <= n-1。
*   将数组中指定元素的值更改为新值 x。给定 I 和 x，将 A[i]更改为 x，0 <= i <= n-1。

**示例:**

> 输入:a[] = {2，6，7，5，18，86，54，2}
> 查询 1:最大值(2，7)
> 查询 2:更新(3，90)
> 查询 3:最大值(2，6)
> **输出:**
> 范围 2 到 7 的最大值为 86。
> 范围 2 到 6 的最大值为 90。

我们已经讨论了[递归段树实现](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)。本文讨论[迭代实现](https://www.geeksforgeeks.org/segment-tree-efficient-implementation/)。分段树的迭代版本基本上使用了这样一个事实，对于索引 I，树中的左子级= 2 * i，右子级= 2 * i + 1。段树数组中索引 I 的父级可以通过 parent = i / 2 找到。因此，我们可以很容易地一个接一个地在树的各个层次上下移动。首先，我们计算范围内的最大值，同时从叶节点开始构建树，并一个接一个地向上爬。我们在处理查询以寻找某个范围内的最大值时使用了相同的概念。因为在最坏的情况下有(log n)个级别，所以查询需要 log n 个时间。为了将特定索引更新为给定值，我们从叶节点开始更新段树，并通过在每次迭代中逐渐向上移动级别来更新受当前节点更新影响的所有节点。更新也需要 log n 时间，因为在那里我们必须从叶节点开始更新所有级别，在那里我们在用户给出的精确索引处更新精确值。

下面是上述方法的实现。

## C++

```
// C++ Program to implement
// iterative segment tree.
#include <bits/stdc++.h>
using namespace std;

void construct_segment_tree(vector<int>& segtree,
                            vector<int>& a, int n)
{
    // assign values to leaves of the segment tree
    for (int i = 0; i < n; i++)
        segtree[n + i] = a[i];

    /* assign values to internal nodes
    to compute maximum in a given range */
    for (int i = n - 1; i >= 1; i--)
        segtree[i] = max(segtree[2 * i],
                         segtree[2 * i + 1]);
}

void update(vector<int>& segtree, int pos, int value,
            int n)
{
    // change the index to leaf node first
    pos += n;

    // update the value at the leaf node
    // at the exact index
    segtree[pos] = value;

    while (pos > 1) {

        // move up one level at a time in the tree
        pos >>= 1;

        // update the values in the nodes in
        // the next higher level
        segtree[pos] = max(segtree[2 * pos],
                           segtree[2 * pos + 1]);
    }
}

int range_query(vector<int>& segtree, int left, int
                                                    right,
                int n)
{
    /* Basically the left and right indices will move
        towards right and left respectively and with
        every each next higher level and compute the
        maximum at each height. */
    // change the index to leaf node first
    left += n;
    right += n;

    // initialize maximum to a very low value
    int ma = INT_MIN;

    while (left < right) {

        // if left index in odd
        if (left & 1) {
            ma = max(ma, segtree[left]);

            // make left index even
            left++;
        }

        // if right index in odd
        if (right & 1) {

            // make right index even
            right--;

            ma = max(ma, segtree[right]);
        }

        // move to the next higher level
        left /= 2;
        right /= 2;
    }
    return ma;
}

// Driver code
int main()
{
    vector<int> a = { 2, 6, 10, 4, 7, 28, 9, 11, 6, 33 };
    int n = a.size();

    /* Construct the segment tree by assigning
    the values to the internal nodes*/
    vector<int> segtree(2 * n);
    construct_segment_tree(segtree, a, n);

    // compute maximum in the range left to right
    int left = 1, right = 5;
    cout << "Maximum in range " << left << " to "
         << right << " is " << range_query(segtree, left,
                                           right + 1, n)
         << "\n";

    // update the value of index 5 to 32
    int index = 5, value = 32;

    // a[5] = 32;
    // Contents of array : {2, 6, 10, 4, 7, 32, 9, 11, 6, 33}
    update(segtree, index, value, n);

    // compute maximum in the range left to right
    left = 2, right = 8;
    cout << "Maximum in range " << left << " to "
         << right << " is " << range_query(segtree,
                                           left, right + 1, n)
         << "\n";

    return 0;
}
```

## 蟒蛇 3

```
# Python Program to implement
# iterative segment tree.

from sys import maxsize
INT_MIN = -maxsize

def construct_segment_tree(a: list, n: int):
    global segtree

    # assign values to leaves of the segment tree
    for i in range(n):
        segtree[n + i] = a[i]

    # assign values to internal nodes
    # to compute maximum in a given range */
    for i in range(n - 1, 0, -1):
        segtree[i] = max(segtree[2 * i], segtree[2 * i + 1])

def update(pos: int, value: int, n: int):
    global segtree

    # change the index to leaf node first
    pos += n

    # update the value at the leaf node
    # at the exact index
    segtree[pos] = value

    while pos > 1:

        # move up one level at a time in the tree
        pos //= 2

        # update the values in the nodes in
        # the next higher level
        segtree[pos] = max(segtree[2 * pos], segtree[2 * pos + 1])

def range_query(left: int, right: int, n: int) -> int:
    global segtree

    # Basically the left and right indices will move
    # towards right and left respectively and with
    # every each next higher level and compute the
    # maximum at each height.
    # change the index to leaf node first
    left += n
    right += n

    # initialize maximum to a very low value
    ma = INT_MIN
    while left < right:

        # if left index in odd
        if left & 1:
            ma = max(ma, segtree[left])

            # make left index even
            left += 1

        # if right index in odd
        if right & 1:

            # make right index even
            right -= 1

            ma = max(ma, segtree[right])

        # move to the next higher level
        left //= 2
        right //= 2
    return ma

# Driver Code
if __name__ == "__main__":
    a = [2, 6, 10, 4, 7, 28, 9, 11, 6, 33]
    n = len(a)

    # Construct the segment tree by assigning
    # the values to the internal nodes
    segtree = [0] * (2 * n)
    construct_segment_tree(a, n)

    # compute maximum in the range left to right
    left = 1
    right = 5
    print("Maximum in range %d to %d is %d" %
        (left, right, range_query(left, right + 1, n)))

    # update the value of index 5 to 32
    index = 5
    value = 32

    # a[5] = 32;
    # Contents of array : {2, 6, 10, 4, 7, 32, 9, 11, 6, 33}
    update(index, value, n)

    # compute maximum in the range left to right
    left = 2
    right = 8
    print("Maximum in range %d to %d is %d" %
        (left, right, range_query(left, right + 1, n)))

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to implement
// iterative segment tree.
function construct_segment_tree(segtree, a, n)
{

    // Assign values to leaves of the segment tree
    for(let i = 0; i < n; i++)
        segtree[n + i] = a[i];

    // Assign values to internal nodes
    // to compute maximum in a given range
    for(let i = n - 1; i >= 1; i--)
        segtree[i] = Math.max(segtree[2 * i],
                              segtree[2 * i + 1]);
}

function update(segtree, pos, value, n)
{

    // Change the index to leaf node first
    pos += n;

    // Update the value at the leaf node
    // at the exact index
    segtree[pos] = value;

    while (pos > 1)
    {

        // Move up one level at a time in the tree
        pos >>= 1;

        // Update the values in the nodes in
        // the next higher level
        segtree[pos] = Math.max(segtree[2 * pos],
                                segtree[2 * pos + 1]);
    }
}

function range_query(segtree, left, right, n)
{

    /* Basically the left and right indices will move
        towards right and left respectively and with
        every each next higher level and compute the
        maximum at each height. */
    // change the index to leaf node first
    left += n;
    right += n;

    // Initialize maximum to a very low value
    let ma = Number.MIN_VALUE;

    while (left < right)
    {

        // If left index in odd
        if ((left & 1) != 0)
        {
            ma = Math.max(ma, segtree[left]);

            // Make left index even
            left++;
        }

        // If right index in odd
        if ((right & 1) > 0)
        {

            // Make right index even
            right--;

            ma = Math.max(ma, segtree[right]);
        }

        // Move to the next higher level
        left = parseInt(left / 2, 10);
        right = parseInt(right / 2, 10);
    }
    return ma;
}

// Driver code
let a = [ 2, 6, 10, 4, 7, 28, 9, 11, 6, 33 ];
let n = a.length;

// Construct the segment tree by assigning
// the values to the internal nodes
let segtree = new Array(2 * n);
construct_segment_tree(segtree, a, n);

// Compute maximum in the range left to right
let left = 1, right = 5;
document.write("Maximum in range " + left +
               " to " + right + " is " +
               range_query(segtree, left, right + 1, n) + "</br>");

// Update the value of index 5 to 32
let index = 5, value = 32;

// a[5] = 32;
// Contents of array : {2, 6, 10, 4, 7, 32, 9, 11, 6, 33}
update(segtree, index, value, n);

// Compute maximum in the range left to right
left = 2, right = 8;
document.write("Maximum in range " + left +
               " to " + right + " is " +
               range_query(segtree, left, right + 1, n) + "</br>");

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
Maximum in range 1 to 5 is 28
Maximum in range 2 to 8 is 32
```

**时间复杂度:**(N * log N)
T3】辅助空间: O(N)