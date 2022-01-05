# 在给定的范围内找到具有最大设置位的元素进行查询

> 原文:[https://www . geeksforgeeks . org/find-the-element-having-to-q-query 给定范围内的最大设置位/](https://www.geeksforgeeks.org/find-the-element-having-maximum-set-bits-in-the-given-range-for-q-queries/)

给定一个由 **N** 整数和 **Q** 查询组成的数组**arr【】**，每个查询有两个整数 **L** 和 **R** ，任务是找到在 L 到 R 范围内具有最大设置位的元素

**注意:**如果有多个元素具有最大设置位，则打印其中的最大值。

**示例:**

> **输入:** arr[] = {18，9，8，15，14，5}，Q = {{1，4}}
> **输出:** 15
> **解释:**
> 斯巴瑞–{ 9，8，15，14}
> 这些整数的二进制表示–
> 9 =>1001 =>Set bit = 2
> 8 =>1000 =
> 
> **输入:** arr[] = {18，9，8，15，14，5}，Q = {{0，2}}
> **输出:** 18
> **解释:**
> Subarray –{ 18，9，8}
> 这些整数的二进制表示–
> 18 =>10010 =>Set bit = 2
> 9 =>1001 =>

**天真方法:**一个简单的解决方案是运行一个从 L 到 R 的循环，计算每个元素的设置位数，并为每个查询找到从 L 到 R 的最大设置位数元素。

***时间复杂度** : O(Q * N)*
***辅助空间复杂度** : O(1)*

**高效方法:**思路是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中每个节点包含两个值，最大集合位元素和最大集合位计数。

*   **段树的表示:**
    1.  叶节点是给定数组的元素。
    2.  每个内部节点代表叶节点的一些合并。对于不同的问题，合并可能会有所不同。对于这个问题，合并是一个节点下叶子的最大集合位数。
    3.  树的数组表示用于表示段树。对于索引 I 处的每个节点，左子节点位于索引 ***2*i+1*** ，右子节点位于 ***2*i+2*** ，父节点位于 ***(i-1)/2*** 。
*   **从给定数组构建段树:**
    1.  我们从片段 arr[0]开始。。。n-1]。并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们将 max_set_bits 和值存储在相应的节点中。
    2.  任何两个范围组合的最大设置位要么是左侧的最大设置位，要么是右侧的最大设置位，以最大值为准。
    3.  最后，在线段树上计算[范围查询。](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// maximum set bits value in a range

#include <bits/stdc++.h>

using namespace std;

// Structure to store two
// values in one node
struct Node {
    int value;
    int max_set_bits;
};

Node tree[4 * 10000];

// Function that returns the count
// of set bits in a number
int setBits(int x)
{
    // Parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }
    return parity;
}

// Function to build the segment tree
void buildSegmentTree(int a[], int index,
                      int beg, int end)
{

    // Condition to check if there is
    // only one element in the array
    if (beg == end) {
        tree[index].value = a[beg];
        tree[index].max_set_bits
            = setBits(a[beg]);
    }

    else {

        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        buildSegmentTree(a, 2 * index + 1,
                         beg, mid);
        buildSegmentTree(a, 2 * index + 2,
                         mid + 1, end);

        // Condition to check the maximum set
        // bits is greater in two subtrees
        if (tree[2 * index + 1].max_set_bits
            > tree[2 * index + 2].max_set_bits) {

            tree[index].max_set_bits
                = tree[2 * index + 1]
                      .max_set_bits;
            tree[index].value
                = tree[2 * index + 1]
                      .value;
        }

        else if (tree[2 * index + 2].max_set_bits
                 > tree[2 * index + 1].max_set_bits) {

            tree[index].max_set_bits
                = tree[2 * index + 2]
                      .max_set_bits;
            tree[index].value
                = tree[2 * index + 2].value;
        }

        // Condition when maximum set bits
        // are equal in both subtrees
        else {
            tree[index].max_set_bits
                = tree[2 * index + 2]
                      .max_set_bits;
            tree[index].value = max(
                tree[2 * index + 2].value,
                tree[2 * index + 1].value);
        }
    }
}

// Function to do the range query
// in the segment tree
Node query(int index, int beg,
           int end, int l, int r)
{
    Node result;
    result.value
        = result.max_set_bits = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // If left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1,
                     end, l, r);

    // If right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg,
                     mid, l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg,
                      mid, l, r);
    Node right = query(2 * index + 2, mid + 1,
                       end, l, r);

    if (left.max_set_bits > right.max_set_bits) {
        result.max_set_bits = left.max_set_bits;
        result.value = left.value;
    }
    else if (right.max_set_bits > left.max_set_bits) {
        result.max_set_bits = right.max_set_bits;
        result.value = right.value;
    }
    else {
        result.max_set_bits = left.max_set_bits;
        result.value = max(right.value, left.value);
    }

    // Returns the value
    return result;
}

// Driver code
int main()
{

    int a[] = { 18, 9, 8, 15, 14, 5 };

    // Calculates the length of array
    int N = sizeof(a) / sizeof(a[0]);

    // Build Segment Tree
    buildSegmentTree(a, 0, 0, N - 1);

    // Find the max set bits value between
    // 1st and 4th index of array
    cout << query(0, 0, N - 1, 1, 4).value
         << endl;

    // Find the max set bits value between
    // 0th and 2nd index of array
    cout << query(0, 0, N - 1, 0, 2).value
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// maximum set bits value in a range
import java.util.*;

class GFG{

// Structure to store two
// values in one node
static class Node
{
    int value;
    int max_set_bits;
};

static Node []tree = new Node[4 * 10000];

// Function that returns the count
// of set bits in a number
static int setBits(int x)
{

    // Parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0)
    {
        if (x % 2 == 1)
            parity++;
        x = x >> 1;
    }
    return parity;
}

// Function to build the segment tree
static void buildSegmentTree(int a[], int index,
                             int beg, int end)
{

    // Condition to check if there is
    // only one element in the array
    if (beg == end)
    {
        tree[index].value = a[beg];
        tree[index].max_set_bits = setBits(a[beg]);
    }
    else
    {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        buildSegmentTree(a, 2 * index + 1,
                         beg, mid);
        buildSegmentTree(a, 2 * index + 2,
                          mid + 1, end);

        // Condition to check the maximum set
        // bits is greater in two subtrees
        if (tree[2 * index + 1].max_set_bits >
            tree[2 * index + 2].max_set_bits)
        {
            tree[index].max_set_bits =
            tree[2 * index + 1].max_set_bits;
            tree[index].value =
            tree[2 * index + 1].value;
        }
        else if (tree[2 * index + 2].max_set_bits >
                 tree[2 * index + 1].max_set_bits)
        {
            tree[index].max_set_bits =
            tree[2 * index + 2].max_set_bits;
            tree[index].value =
            tree[2 * index + 2].value;
        }

        // Condition when maximum set bits
        // are equal in both subtrees
        else
        {
            tree[index].max_set_bits =
            tree[2 * index + 2].max_set_bits;
            tree[index].value = Math.max(
            tree[2 * index + 2].value,
            tree[2 * index + 1].value);
        }
    }
}

// Function to do the range query
// in the segment tree
static Node query(int index, int beg,
                  int end, int l, int r)
{
    Node result = new Node();
    result.value = result.max_set_bits = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // If left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1,
                         end, l, r);

    // If right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg,
                     mid, l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg,
                          mid, l, r);
    Node right = query(2 * index + 2, mid + 1,
                           end, l, r);

    if (left.max_set_bits > right.max_set_bits)
    {
        result.max_set_bits = left.max_set_bits;
        result.value = left.value;
    }
    else if (right.max_set_bits > left.max_set_bits)
    {
        result.max_set_bits = right.max_set_bits;
        result.value = right.value;
    }
    else
    {
        result.max_set_bits = left.max_set_bits;
        result.value = Math.max(right.value,
                                left.value);
    }

    // Returns the value
    return result;
}

// Driver code
public static void main(String[] args)
{

    int a[] = { 18, 9, 8, 15, 14, 5 };

    // Calculates the length of array
    int N = a.length;

    for(int i = 0; i < tree.length; i++)
        tree[i] = new Node();

    // Build Segment Tree
    buildSegmentTree(a, 0, 0, N - 1);

    // Find the max set bits value between
    // 1st and 4th index of array
    System.out.print(query(0, 0, N - 1, 1, 4).value +"\n");

    // Find the max set bits value between
    // 0th and 2nd index of array
    System.out.print(query(0, 0, N - 1, 0, 2).value +"\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to find
# maximum set bits value in a range

# Structure to store two
# values in one node
from typing import List

class Node:

    def __init__(self) -> None:

        self.value = 0
        self.max_set_bits = 0

tree = [Node() for _ in range(4 * 10000)]

# Function that returns the count
# of set bits in a number
def setBits(x: int) -> int:

    # Parity will store the
    # count of set bits
    parity = 0

    while (x != 0):
        if (x & 1):
            parity += 1

        x = x >> 1

    return parity

# Function to build the segment tree
def buildSegmentTree(a: List[int], index: int,
                     beg: int, end: int) -> None:

    # Condition to check if there is
    # only one element in the array
    if (beg == end):
        tree[index].value = a[beg]
        tree[index].max_set_bits = setBits(a[beg])

    else:
        mid = (beg + end) // 2

        # If there are more than one elements,
        # then recur for left and right subtrees
        buildSegmentTree(a, 2 * index + 1, beg, mid)
        buildSegmentTree(a, 2 * index + 2, mid + 1, end)

        # Condition to check the maximum set
        # bits is greater in two subtrees
        if (tree[2 * index + 1].max_set_bits >
            tree[2 * index + 2].max_set_bits):
            tree[index].max_set_bits = tree[2 * index + 1].max_set_bits
            tree[index].value = tree[2 * index + 1].value

        elif (tree[2 * index + 2].max_set_bits >
              tree[2 * index + 1].max_set_bits):

            tree[index].max_set_bits = tree[2 * index + 2].max_set_bits
            tree[index].value = tree[2 * index + 2].value

        # Condition when maximum set bits
        # are equal in both subtrees
        else:
            tree[index].max_set_bits = tree[2 * index + 2].max_set_bits
            tree[index].value = max(tree[2 * index + 2].value,
                                    tree[2 * index + 1].value)

# Function to do the range query
# in the segment tree
def query(index: int, beg: int,
          end: int, l: int, r: int) -> Node:

    result = Node()
    result.value = result.max_set_bits = -1

    # If segment of this node is outside the given
    # range, then return the minimum value.
    if (beg > r or end < l):
        return result

    # If segment of this node is a part of given
    # range, then return the node of the segment
    if (beg >= l and end <= r):
        return tree[index]

    mid = (beg + end) // 2

    # If left segment of this node falls out of
    # range, then recur in the right side of
    # the tree
    if (l > mid):
        return query(2 * index + 2, mid + 1,
                     end, l, r)

    # If right segment of this node falls out of
    # range, then recur in the left side of
    # the tree
    if (r <= mid):
        return query(2 * index + 1, beg,
                     mid, l, r)

    # If a part of this segment overlaps with
    # the given range
    left = query(2 * index + 1, beg, mid, l, r)
    right = query(2 * index + 2, mid + 1, end, l, r)

    if (left.max_set_bits > right.max_set_bits):
        result.max_set_bits = left.max_set_bits
        result.value = left.value

    elif (right.max_set_bits > left.max_set_bits):
        result.max_set_bits = right.max_set_bits
        result.value = right.value

    else:
        result.max_set_bits = left.max_set_bits
        result.value = max(right.value, left.value)

    # Returns the value
    return result

# Driver code
if __name__ == "__main__":

    a = [ 18, 9, 8, 15, 14, 5 ]

    # Calculates the length of array
    N = len(a)

    # Build Segment Tree
    buildSegmentTree(a, 0, 0, N - 1)

    # Find the max set bits value between
    # 1st and 4th index of array
    print(query(0, 0, N - 1, 1, 4).value)

    # Find the max set bits value between
    # 0th and 2nd index of array
    print(query(0, 0, N - 1, 0, 2).value)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation to find maximum
// set bits value in a range
using System;

class GFG{

// Structure to store two
// values in one node
class Node
{
    public int value;
    public int max_set_bits;
};

static Node []tree = new Node[4 * 10000];

// Function that returns the count
// of set bits in a number
static int setBits(int x)
{

    // Parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0)
    {
        if (x % 2 == 1)
            parity++;
        x = x >> 1;
    }
    return parity;
}

// Function to build the segment tree
static void buildSegmentTree(int []a, int index,
                             int beg, int end)
{

    // Condition to check if there is
    // only one element in the array
    if (beg == end)
    {
        tree[index].value = a[beg];
        tree[index].max_set_bits = setBits(a[beg]);
    }
    else
    {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        buildSegmentTree(a, 2 * index + 1,
                         beg, mid);
        buildSegmentTree(a, 2 * index + 2,
                         mid + 1, end);

        // Condition to check the maximum set
        // bits is greater in two subtrees
        if (tree[2 * index + 1].max_set_bits >
            tree[2 * index + 2].max_set_bits)
        {
            tree[index].max_set_bits =
            tree[2 * index + 1].max_set_bits;
            tree[index].value =
            tree[2 * index + 1].value;
        }
        else if (tree[2 * index + 2].max_set_bits >
                 tree[2 * index + 1].max_set_bits)
        {
            tree[index].max_set_bits =
            tree[2 * index + 2].max_set_bits;
            tree[index].value =
            tree[2 * index + 2].value;
        }

        // Condition when maximum set bits
        // are equal in both subtrees
        else
        {
            tree[index].max_set_bits =
            tree[2 * index + 2].max_set_bits;
            tree[index].value = Math.Max(
            tree[2 * index + 2].value,
            tree[2 * index + 1].value);
        }
    }
}

// Function to do the range query
// in the segment tree
static Node query(int index, int beg,
                  int end, int l, int r)
{
    Node result = new Node();
    result.value = result.max_set_bits = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // If left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1,
                         end, l, r);

    // If right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg,
                         mid, l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg,
                          mid, l, r);
    Node right = query(2 * index + 2, mid + 1,
                           end, l, r);

    if (left.max_set_bits > right.max_set_bits)
    {
        result.max_set_bits = left.max_set_bits;
        result.value = left.value;
    }
    else if (right.max_set_bits > left.max_set_bits)
    {
        result.max_set_bits = right.max_set_bits;
        result.value = right.value;
    }
    else
    {
        result.max_set_bits = left.max_set_bits;
        result.value = Math.Max(right.value,
                                 left.value);
    }

    // Returns the value
    return result;
}

// Driver code
public static void Main(String[] args)
{

    int []a = { 18, 9, 8, 15, 14, 5 };

    // Calculates the length of array
    int N = a.Length;

    for(int i = 0; i < tree.Length; i++)
        tree[i] = new Node();

    // Build Segment Tree
    buildSegmentTree(a, 0, 0, N - 1);

    // Find the max set bits value between
    // 1st and 4th index of array
    Console.Write(query(0, 0, N - 1, 1, 4).value + "\n");

    // Find the max set bits value between
    // 0th and 2nd index of array
    Console.Write(query(0, 0, N - 1, 0, 2).value + "\n");
}
}

// This code is contributed by amal kumar choubey
```

**Output:** 

```
15
18
```

***时间复杂度:**O(Q * logN)*T4】