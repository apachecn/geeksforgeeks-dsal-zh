# 使用段树查询给定范围内的偶数和元素的计数。

> 原文:[https://www . geeksforgeeks . org/使用段树查询给定范围内的偶数元素总数/](https://www.geeksforgeeks.org/queries-for-the-count-of-even-digit-sum-elements-in-the-given-range-using-segment-tree/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是回答 Q 个查询，每个查询有两个整数 **L** 和 **R** 。对于每个查询，任务是在数字和为偶数的子阵列**arr【L…R】**中找到元素的数量。
**举例:**

> **输入:** arr[] = {7，3，19，13，5，4}
> 查询= { 1，5 }
> **输出:** 3
> **解释:**
> 元素 19，13 和 4 在子阵列{3，9，13，5，4}中有偶数位和
> 。
> **输入:** arr[] = {0，1，2，3，4，5，6，7}
> 查询= { 3，5 }
> **输出:** 1
> **解释:**
> 在子阵{ 3，4，5 }中只有 4 有偶数位和
> 。

**天真的做法:**

*   通过简单地遍历数组从索引 **L** 到 **R** 找到每个查询的答案，并且只要数组元素有偶数和，就不断地将 **1** 加到计数中。该方法的时间复杂度为 **O(n * q)** 。

**高效方法:**
想法是建立[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。

1.  **段树的表示:**
    *   叶节点是输入数组的元素。

    *   每个内部节点包含叶的数量，其下所有叶的偶数和。

2.  **从给定数组构建段树:**
    *   我们从片段 arr[0]开始。。。n-1]。每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，对于每个这样的段，我们存储其下所有节点的偶数和的元素数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the digit sum
// for a number
int digitSum(int num)
{
    int sum = 0;
    while (num) {
        sum += (num % 10);
        num /= 10;
    }

    return sum;
}

// Procedure to build the segment tree
void buildTree(vector<int>& tree, int* arr,
               int index, int s, int e)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e) {
        if (digitSum(arr[s]) & 1)
            tree[index] = 0;
        else
            tree[index] = 1;
        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index,
              s, mid);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e);

    tree[index] = tree[2 * index]
                + tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are
// query range
int query(vector<int> tree, int index,
          int s, int e, int l, int r)
{

    // Out of bound or no overlap
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
    return (query(tree, 2 * index, s,
                  mid, l, r)
            + query(tree, 2 * index + 1,
                    mid + 1, e, l, r));
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 19, 13, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    vector<int> tree(4 * n + 1);

    int L = 1, R = 5;

    buildTree(tree, arr, 1, 0, n - 1);

    cout << query(tree, 1, 0, n - 1, L, R)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG{

// Function to find the digit sum
// for a number
static int digitSum(int num)
{
    int sum = 0;
    while (num > 0)
    {
        sum += (num % 10);
        num /= 10;
    }
    return sum;
}

// Procedure to build the segment tree
static void buildTree(int []tree, int []arr,
                int index, int s, int e)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e)
    {
        if (digitSum(arr[s]) % 2 == 1)
            tree[index] = 0;
        else
            tree[index] = 1;
        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index,
              s, mid);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e);

    tree[index] = tree[2 * index] +
                    tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are
// query range
static int query(int []tree, int index,
                 int s, int e,
                 int l, int r)
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
    return (query(tree, 2 * index, s,
                  mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r));
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 7, 3, 19, 13, 5, 4 };
    int n = arr.length;
    int []tree = new int[4 * n + 1];

    int L = 1, R = 5;

    buildTree(tree, arr, 1, 0, n - 1);

    System.out.print(query(tree, 1, 0,
                           n - 1, L, R) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the digit sum
# for a number
def digitSum(num):

    sum = 0;
    while (num):
        sum += (num % 10)
        num //= 10

    return sum

# Procedure to build the segment tree
def buildTree(tree, arr, index, s, e):

    # Reached the leaf node
    # of the segment tree
    if (s == e):
        if (digitSum(arr[s]) & 1):
            tree[index] = 0
        else:
            tree[index] = 1
        return

    # Recursively call the buildTree
    # on both the nodes of the tree
    mid = (s + e) // 2
    buildTree(tree, arr, 2 * index,
              s, mid)
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e)

    tree[index] = (tree[2 * index] +
                   tree[2 * index + 1])

# Query procedure to get the answer
# for each query l and r are
# query range
def query(tree, index, s, e, l, r):

    # Out of bound or no overlap
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
    return (query(tree, 2 * index,
                  s, mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r))

# Driver code
arr = [ 7, 3, 19, 13, 5, 4 ]
n = len(arr)

tree = [0] * (4 * n + 1)

L = 1
R = 5

buildTree(tree, arr, 1, 0, n - 1);

print(query(tree, 1, 0, n - 1, L, R))

# This code is contributed by Apurvaraj
```

## C#

```
// C# implementation of the approach
using System;
class GFG{

// Function to find the digit sum
// for a number
static int digitSum(int num)
{
    int sum = 0;
    while (num > 0)
    {
        sum += (num % 10);
        num /= 10;
    }
    return sum;
}

// Procedure to build the segment tree
static void buildTree(int []tree, int []arr,
                      int index, int s, int e)
{

    // Reached the leaf node
    // of the segment tree
    if (s == e)
    {
        if (digitSum(arr[s]) % 2 == 1)
            tree[index] = 0;
        else
            tree[index] = 1;
        return;
    }

    // Recursively call the buildTree
    // on both the nodes of the tree
    int mid = (s + e) / 2;
    buildTree(tree, arr, 2 * index,
              s, mid);
    buildTree(tree, arr, 2 * index + 1,
              mid + 1, e);

    tree[index] = tree[2 * index] +
                  tree[2 * index + 1];
}

// Query procedure to get the answer
// for each query l and r are
// query range
static int query(int []tree, int index,
                 int s, int e,
                 int l, int r)
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
    return (query(tree, 2 * index, s,
                  mid, l, r) +
            query(tree, 2 * index + 1,
                  mid + 1, e, l, r));
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 7, 3, 19, 13, 5, 4 };
    int n = arr.Length;
    int []tree = new int[4 * n + 1];

    int L = 1, R = 5;

    buildTree(tree, arr, 1, 0, n - 1);

    Console.Write(query(tree, 1, 0,
                        n - 1, L, R) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach

      // Function to find the digit sum
      // for a number
      function digitSum(num) {
        var sum = 0;
        while (num > 0) {
          sum += parseInt(num % 10);
          num = parseInt(num / 10);
        }
        return sum;
      }

      // Procedure to build the segment tree
      function buildTree(tree, arr, index, s, e) {
        // Reached the leaf node
        // of the segment tree
        if (s === e) {
          if (digitSum(arr[s]) % 2 === 1) tree[index] = 0;
          else tree[index] = 1;
          return;
        }

        // Recursively call the buildTree
        // on both the nodes of the tree
        var mid = parseInt((s + e) / 2);
        buildTree(tree, arr, 2 * index, s, mid);
        buildTree(tree, arr, 2 * index + 1, mid + 1, e);

        tree[index] = tree[2 * index] + tree[2 * index + 1];
      }

      // Query procedure to get the answer
      // for each query l and r are
      // query range
      function query(tree, index, s, e, l, r) {
        // Out of bound or no overlap
        if (r < s || l > e) return 0;

        // Complete overlap
        // Query range completely lies in
        // the segment tree node range
        if (s >= l && e <= r) {
          return tree[index];
        }

        // Partially overlap
        // Query range partially lies in
        // the segment tree node range
        var mid = (s + e) / 2;
        return (
          query(tree, 2 * index, s, mid, l, r) +
          query(tree, 2 * index + 1, mid + 1, e, l, r)
        );
      }

      // Driver code
      var arr = [7, 3, 19, 13, 5, 4];
      var n = arr.length;
      var tree = new Array(4 * n + 1).fill(0);

      var L = 1,
        R = 5;

      buildTree(tree, arr, 1, 0, n - 1);

      document.write(query(tree, 1, 0, n - 1, L, R) + "<br>");

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(Q * log(N))