# 使用段树

查询给定索引范围内值在 A 到 B 范围内的元素

> 原文:[https://www . geeksforgeeks . org/查询具有给定索引范围内的值的元素使用段树/](https://www.geeksforgeeks.org/queries-for-elements-having-values-within-the-range-a-to-b-in-the-given-index-range-using-segment-tree/)

给定一个由 **N** 元素和两个整数 **A** 到 **B** 组成的数组 **arr[]** ，任务是回答 Q 个查询，每个查询都有两个整数 **L** 和 **R** 。对于每个查询，任务是在子阵列**arr【L…R】**中找到位于范围 **A** 到 **B** 内的元素数量(两者都包括在内)。

**示例:**

> **输入:** arr[] = {7，3，9，13，5，4}，A=4，B=7
> 查询= { 1，5 }
> **输出:** 2
> **解释:**
> 在子阵列{3，9，13，5，4}中只有 5 和 4 位于 4 到 7
> 之间。
> 
> **输入:** arr[] = {0，1，2，3，4，5，6，7}，A=1，B=5
> 查询= { 3，5 }
> **输出:** 3
> **解释:**
> 所有元素 3，4，5 都位于子阵列{ 3，4，5 }中的 1 到 5
> 内。

**先决条件:** [段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)
**天真方法:**通过简单地遍历数组从索引 **L** 直到 **R** 并在数组元素位于范围 **A** 至 **B** 内时不断将 **1** 添加到计数中来找到每个查询的答案。该方法的时间复杂度为 **O(n * q)** 。

**高效方法:**
构建[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。
段树的表示
**1。**叶节点是输入数组的元素。
**2。**每个内部节点包含位于其下所有叶的 **A** 到 **B** 范围内的叶数。

**从给定数组**
构建线段树我们从线段 arr【0】开始。。。n-1]。并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们存储位于其下所有节点的范围 **A** 到 **B** 内的元素的数量。
该方法的时间复杂度为 **O(q * log(n))**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Procedure to build the segment tree
void buildTree(vector<int>& tree, int* arr,
               int index, int s, int e, int A, int B)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e) {
        if (arr[s] >= A && arr[s] <= B)
            tree[index] = 1;
        else
            tree[index] = 0;
        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index, s, mid, A, B);
    buildTree(tree, arr, 2 * index + 1, mid + 1, e, A, B);

    tree[index] = tree[2 * index] + tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are query range
int query(vector<int> tree, int index, int s,
          int e, int l, int r)
{

    // out of bound or no overlap
    if (r < s || l > e)
        return 0;

    // Complete overlap
    // Query range completely lies in
    // the segment tree node range
    if (s >= l && e <= r) {
        return tree[index];
    }

    // Partially overlap
    // Query range partially lies in
    // the segment tree node range
    int mid = (s + e) / 2;
    return (query(tree, 2 * index, s, mid, l, r)
            + query(tree, 2 * index + 1, mid + 1, e, l, r));
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 9, 13, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    vector<int> tree(4 * n + 1);

    int L = 1, R = 5, A = 4, B = 7;

    buildTree(tree, arr, 1, 0, n - 1, A, B);

    cout << query(tree, 1, 0, n - 1, L, R)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Procedure to build the segment tree
static void buildTree(int tree[] , int arr[] ,
                      int index, int s, int e,
                      int A, int B)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e)
    {
        if (arr[s] >= A && arr[s] <= B)
            tree[index] = 1;
        else
            tree[index] = 0;

        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index,
              s, mid, A, B);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e, A, B);

    tree[index] = tree[2 * index] +
                  tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are query range
static int query(int tree[], int index, int s,
                 int e, int l, int r)
{

    // Out of bound or no overlap
    if (r < s || l > e)
        return 0;

    // Complete overlap
    // Query range completely lies in
    // the segment tree node range
    if (s >= l && e <= r)
    {
        return tree[index];
    }

    // Partially overlap
    // Query range partially lies in
    // the segment tree node range
    int mid = (s + e) / 2;
    return (query(tree, 2 * index,
                  s, mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r));
}

// Driver code
public static void main (String []args)
{
    int arr[] = { 7, 3, 9, 13, 5, 4 };
    int n = arr.length;
    int tree[] = new int [(4 * n + 1)];

    int L = 1, R = 5, A = 4, B = 7;

    buildTree(tree, arr, 1, 0, n - 1, A, B);

    System.out.print(query(tree, 1, 0, n - 1, L, R));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Procedure to build the segment tree
def buildTree(tree,arr,index, s, e, A, B):

    # Reached the leaf node
    # of the segment tree
    if (s == e):
        if (arr[s] >= A and arr[s] <= B):
            tree[index] = 1
        else:
            tree[index] = 0
        return

    # Recursively call the buildTree
    # on both the nodes of the tree
    mid = (s + e) // 2
    buildTree(tree, arr, 2 * index, s, mid, A, B)
    buildTree(tree, arr, 2 * index + 1, mid + 1, e, A, B)

    tree[index] = tree[2 * index] + tree[2 * index + 1]

# Query procedure to get the answer
# for each query l and r are query range
def query(tree, index, s, e, l, r):

    # out of bound or no overlap
    if (r < s or l > e):
        return 0

    # Complete overlap
    # Query range completely lies in
    # the segment tree node range
    if (s >= l and e <= r):
        return tree[index]

    # Partially overlap
    # Query range partially lies in
    # the segment tree node range
    mid = (s + e) // 2
    return (query(tree, 2 * index, s, mid, l, r)
            + query(tree, 2 * index + 1, mid + 1, e, l, r))

# Driver code
if __name__ == '__main__':
    arr=[7, 3, 9, 13, 5, 4]
    n = len(arr)
    tree=[0]*(4 * n + 1)

    L = 1
    R = 5
    A = 4
    B = 7

    buildTree(tree, arr, 1, 0, n - 1, A, B)

    print(query(tree, 1, 0, n - 1, L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Procedure to build the segment tree
static void buildTree(int[] tree, int[] arr,
                      int index, int s, int e,
                      int A, int B)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e)
    {
        if (arr[s] >= A && arr[s] <= B)
            tree[index] = 1;
        else
            tree[index] = 0;

        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index,
              s, mid, A, B);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e, A, B);

    tree[index] = tree[2 * index] +
                  tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are query range
static int query(int[] tree, int index, int s,
                 int e, int l, int r)
{

    // Out of bound or no overlap
    if (r < s || l > e)
        return 0;

    // Complete overlap
    // Query range completely lies in
    // the segment tree node range
    if (s >= l && e <= r)
    {
        return tree[index];
    }

    // Partially overlap
    // Query range partially lies in
    // the segment tree node range
    int mid = (s + e) / 2;
    return (query(tree, 2 * index,
                  s, mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r));
}

// Driver code
public static void Main ()
{
    int[] arr = new int[] { 7, 3, 9, 13, 5, 4 };
    int n = arr.Length;
    int[] tree = new int [(4 * n + 1)];

    int L = 1, R = 5, A = 4, B = 7;

    buildTree(tree, arr, 1, 0, n - 1, A, B);

    Console.Write(query(tree, 1, 0, n - 1, L, R));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Procedure to build the segment tree
function buildTree(tree, arr, index, s, e, A, B)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e)
    {
        if (arr[s] >= A && arr[s] <= B)
            tree[index] = 1;
        else
            tree[index] = 0;

        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    let mid = Math.floor((s + e) / 2);
    buildTree(tree, arr, 2 * index,
              s, mid, A, B);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e, A, B);

    tree[index] = tree[2 * index] +
                  tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are query range
function query(tree, index, s, e, l, r)
{

    // Out of bound or no overlap
    if (r < s || l > e)
        return 0;

    // Complete overlap
    // Query range completely lies in
    // the segment tree node range
    if (s >= l && e <= r)
    {
        return tree[index];
    }

    // Partially overlap
    // Query range partially lies in
    // the segment tree node range
    let mid = Math.floor((s + e) / 2);
    return (query(tree, 2 * index,
                  s, mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r));
}

// Driver code
let arr = [ 7, 3, 9, 13, 5, 4 ];
let n = arr.length;
let tree = new Array(4 * n + 1);
let L = 1, R = 5, A = 4, B = 7;
buildTree(tree, arr, 1, 0, n - 1, A, B);

document.write(query(tree, 1, 0, n - 1, L, R));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```