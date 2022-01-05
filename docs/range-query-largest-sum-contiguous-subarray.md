# 最大和邻接子阵的范围查询

> 原文:[https://www . geesforgeks . org/range-query-maximum-sum-continuous-subarray/](https://www.geeksforgeeks.org/range-query-largest-sum-contiguous-subarray/)

给定一个数字，N 和 Q 两种类型的查询 1 和 2。任务是为给定的查询编写一个代码，其中在类型-1 中，给定 l 和 r，任务是打印[最大和连续子数组](https://www.geeksforgeeks.org/maximum-subarray-sum-given-range/)，对于类型 2，给定类型、索引和值，将值更新为 A <sub>索引</sub>。

**示例:**

```
Input : a = {-2, -3, 4, -1, -2, 1, 5, -3} 
        1st query : 1 5 8 
        2nd query : 2 1 10 
        3rd query : 1 1 3 
Output : Answer to 1st query : 6 
Answer to 3rd query : 11
```

**说明:**在第一次查询中，任务是打印 5-8 范围内连续子阵的最大和，由{-2，1，5，-3}组成。最大和为 6，由子阵列{1，5}组成。在第二个查询中，完成了一个更新操作，将[1]更新为 10，因此序列是{10，-3，4，-1，-2，1，5，-3}。在第三个查询中，任务是打印由{10，-3，4}组成的范围 1-3 中连续子阵列的最大和。最大的和是 11，由子阵列{10，-3，4}组成。

一种**天真的方法**是对每一个 type-1 查询使用[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。每个类型 1 查询的复杂度都是 O(n)。类型 2 查询在 O(1)中完成。

**高效方法:**
高效的方法是构建一个段树，其中每个节点存储四个值(sum、prefixsum、suffixsum、maxsum)，并对其进行范围查询，以找到每个查询的答案。如上所述，段树的节点存储四个值。父节点将存储左右子节点的合并。父节点存储如下所述的值:

> parent . sum = left . sum+right . sum
> parent . prefix sum = max(left . prefix sum，left . sum+right . prefix sum)
> parent . sufix sum = max(right . sufix sum，right . sum+left . sufix sum)
> parent . maxsum = max(parent . prefix sum，parent . sufix sum，left.maxsum，right . sufix sum+right . prefix sum)

父节点存储以下内容:

*   父节点的和是左右子节点和的和。
*   父节点的前缀和将等于左子节点前缀和或左子节点前缀和+右子节点前缀和的最大值。
*   父节点的后缀总和将等于右子后缀总和或右子总和+左子后缀总和
*   父节点的 maxsum 将是父节点的前缀 sum 或后缀 sum 的最大值，或者是左右子节点的 maxsum，或者是左右子节点的后缀 sum 和前缀 sum 的总和。

**段树的表示:**
1。叶节点是输入数组的元素。
2。每个内部节点代表叶节点的一些合并。对于不同的问题，合并可能会有所不同。对于这个问题，如上所述进行合并。
树的数组表示用于表示分段树。对于索引 I 处的每个节点，左子节点位于索引 **2 * i + 1** ，右子节点位于 **2 * i + 2** ，父节点位于**(I–1)/2**。

**从给定数组构建段树:**
从段 arr[0]开始。。。n-1]。并且每次将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，将值存储在上面公式中给出的所有四个变量中。

**更新数组和段树中的给定值:**
从提供给我们的数组的完整段开始。每次将数组分成两半，**忽略要更新的索引不存在的那一半**。继续在每一步忽略一半，直到到达叶节点，在那里更新给定索引的值。现在，根据给定的公式将更新后的值合并到我们遍历的路径中的所有节点。

**回答查询:**
对于每个查询，移动到树的左半部分和右半部分。只要给定的范围与树的任何一半完全重叠，就从该一半返回节点，而不在该区域中进一步遍历。当树的一半完全位于给定范围之外时，返回 INT_MIN。在部分范围重叠的情况下，穿过左右两半并相应返回。

下面是上述想法的实现:

## C++

```
// C++ program to find Largest Sum Contiguous
// Subarray in a given range with updates
#include <bits/stdc++.h>
using namespace std;

// Structure to store
// 4 values that are to be stored
// in the nodes
struct node {
    int sum, prefixsum, suffixsum, maxsum;
};

// array to store the segment tree
node tree[4 * 100];

// function to build the tree
void build(int arr[], int low, int high, int index)
{
    // the leaf node
    if (low == high) {
        tree[index].sum = arr[low];
        tree[index].prefixsum = arr[low];
        tree[index].suffixsum = arr[low];
        tree[index].maxsum = arr[low];
    }
    else {
        int mid = (low + high) / 2;

        // left subtree
        build(arr, low, mid, 2 * index + 1);

        // right subtree
        build(arr, mid + 1, high, 2 * index + 2);

        // parent node's sum is the summation
        // of left and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum =
                    max(tree[2 * index + 1].prefixsum,
                    tree[2 * index + 1].sum +
                    tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum =
                    max(tree[2 * index + 2].suffixsum,
                    tree[2 * index + 2].sum +
                    tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and right
        // child's prefix.
        tree[index].maxsum =
                    max(tree[index].prefixsum,
                    max(tree[index].suffixsum,
                    max(tree[2 * index + 1].maxsum,
                    max(tree[2 * index + 2].maxsum,
                    tree[2 * index + 1].suffixsum +
                    tree[2 * index + 2].prefixsum))));
    }
}

// function to update the tree
void update(int arr[], int index, int low, int high,
            int idx, int value)
{
    // the node to be updated
    if (low == high) {
        tree[index].sum = value;
        tree[index].prefixsum = value;
        tree[index].suffixsum = value;
        tree[index].maxsum = value;
    }
    else {

        int mid = (low + high) / 2;

        // if node to be updated is in left subtree
        if (idx <= mid)
            update(arr, 2 * index + 1, low, mid, idx, value);

        // if node to be updated is in right subtree
        else
            update(arr, 2 * index + 2, mid + 1,
                   high, idx, value);

        // parent node's sum is the summation of left
        // and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum =
                    max(tree[2 * index + 1].prefixsum,
                    tree[2 * index + 1].sum +
                    tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum =
                    max(tree[2 * index + 2].suffixsum,
                    tree[2 * index + 2].sum +
                    tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and
        // right child's prefix.
        tree[index].maxsum =
                    max(tree[index].prefixsum,
                    max(tree[index].suffixsum,
                    max(tree[2 * index + 1].maxsum,
                    max(tree[2 * index + 2].maxsum,
                    tree[2 * index + 1].suffixsum +
                    tree[2 * index + 2].prefixsum))));
    }
}

// function to return answer to  every type-1 query
node query(int arr[], int index, int low,
           int high, int l, int r)
{
    // initially all the values are INT_MIN
    node result;
    result.sum = result.prefixsum =
                 result.suffixsum =
                 result.maxsum = INT_MIN;

    // range does not lies in this subtree
    if (r < low || high < l)
        return result;

    // complete overlap of range
    if (l <= low && high <= r)
        return tree[index];

    int mid = (low + high) / 2;

    // right subtree
    if (l > mid)
        return query(arr, 2 * index + 2,
                     mid + 1, high, l, r);

    // left subtree   
    if (r <= mid)
        return query(arr, 2 * index + 1,
                     low, mid, l, r);

    node left = query(arr, 2 * index + 1,
                      low, mid, l, r);
    node right = query(arr, 2 * index + 2,
                        mid + 1, high, l, r);

    // finding the maximum and returning it
    result.sum = left.sum + right.sum;
    result.prefixsum = max(left.prefixsum, left.sum +
                           right.prefixsum);

    result.suffixsum = max(right.suffixsum,
                       right.sum + left.suffixsum);
    result.maxsum = max(result.prefixsum,
                    max(result.suffixsum,
                    max(left.maxsum,
                    max(right.maxsum,
                    left.suffixsum + right.prefixsum))));

    return result;
}

// Driver Code
int main()
{
    int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
    int n = sizeof(a) / sizeof(a[0]);

    // build the tree
    build(a, 0, n - 1, 0);

    // 1st query type-1
    int l = 5, r = 8;
    cout << query(a, 0, 0, n - 1, l - 1, r - 1).maxsum;
    cout << endl;

    // 2nd type-2 query
    int index = 1;
    int value = 10;
    a[index - 1] = value;
    update(a, 0, 0, n - 1, index - 1, value);

    // 3rd type-1 query
    l = 1, r = 3;
    cout << query(a, 0, 0, n - 1, l - 1, r - 1).maxsum;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Largest Sum Contiguous
// Subarray in a given range with updates
class GFG
{

// Structure to store 4 values that are
// to be stored in the nodes
static class node
{
    int sum, prefixsum, suffixsum, maxsum;
};

// array to store the segment tree
static node[] tree = new node[4 * 100];

// function to build the tree
static void build(int arr[], int low,
                  int high, int index)
{
    // the leaf node
    if (low == high)
    {
        tree[index].sum = arr[low];
        tree[index].prefixsum = arr[low];
        tree[index].suffixsum = arr[low];
        tree[index].maxsum = arr[low];
    }
    else
    {
        int mid = (low + high) / 2;

        // left subtree
        build(arr, low, mid, 2 * index + 1);

        // right subtree
        build(arr, mid + 1, high, 2 * index + 2);

        // parent node's sum is the summation
        // of left and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.max(tree[2 * index + 1].prefixsum,
                                         tree[2 * index + 1].sum +
                                         tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.max(tree[2 * index + 2].suffixsum,
                                         tree[2 * index + 2].sum +
                                         tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and right
        // child's prefix.
        tree[index].maxsum = Math.max(tree[index].prefixsum,
                             Math.max(tree[index].suffixsum,
                             Math.max(tree[2 * index + 1].maxsum,
                             Math.max(tree[2 * index + 2].maxsum,
                                      tree[2 * index + 1].suffixsum +
                                      tree[2 * index + 2].prefixsum))));
    }
}

// function to update the tree
static void update(int arr[], int index, int low,
                   int high, int idx, int value)
{
    // the node to be updated
    if (low == high)
    {
        tree[index].sum = value;
        tree[index].prefixsum = value;
        tree[index].suffixsum = value;
        tree[index].maxsum = value;
    }
    else
    {
        int mid = (low + high) / 2;

        // if node to be updated is in left subtree
        if (idx <= mid)
        {
            update(arr, 2 * index + 1, low,
                           mid, idx, value);
        }

        // if node to be updated is in right subtree
        else
        {
            update(arr, 2 * index + 2, mid + 1,
                             high, idx, value);
        }

        // parent node's sum is the summation of left
        // and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.max(tree[2 * index + 1].prefixsum,
                                         tree[2 * index + 1].sum +
                                         tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.max(tree[2 * index + 2].suffixsum,
                                         tree[2 * index + 2].sum +
                                         tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and
        // right child's prefix.
        tree[index].maxsum = Math.max(tree[index].prefixsum,
                             Math.max(tree[index].suffixsum,
                             Math.max(tree[2 * index + 1].maxsum,
                             Math.max(tree[2 * index + 2].maxsum,
                                      tree[2 * index + 1].suffixsum +
                                      tree[2 * index + 2].prefixsum))));
    }
}

// function to return answer to every type-1 query
static node query(int arr[], int index,
                  int low, int high, int l, int r)
{
    // initially all the values are Integer.MIN_VALUE
    node result = new node();
    result.sum = result.prefixsum
               = result.suffixsum
               = result.maxsum = Integer.MIN_VALUE;

    // range does not lies in this subtree
    if (r < low || high < l)
    {
        return result;
    }

    // complete overlap of range
    if (l <= low && high <= r)
    {
        return tree[index];
    }

    int mid = (low + high) / 2;

    // right subtree
    if (l > mid)
    {
        return query(arr, 2 * index + 2,
                     mid + 1, high, l, r);
    }

    // left subtree
    if (r <= mid)
    {
        return query(arr, 2 * index + 1,
                     low, mid, l, r);
    }

    node left = query(arr, 2 * index + 1,
                      low, mid, l, r);
    node right = query(arr, 2 * index + 2,
                       mid + 1, high, l, r);

    // finding the maximum and returning it
    result.sum = left.sum + right.sum;
    result.prefixsum = Math.max(left.prefixsum,
                                left.sum + right.prefixsum);

    result.suffixsum = Math.max(right.suffixsum,
                                right.sum + left.suffixsum);
    result.maxsum = Math.max(result.prefixsum,
                    Math.max(result.suffixsum,
                    Math.max(left.maxsum,
                    Math.max(right.maxsum, left.suffixsum +
                             right.prefixsum))));

    return result;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = {-2, -3, 4, -1, -2, 1, 5, -3};
    int n = a.length;
    for (int i = 0; i < 4 * 100; i++)
    {
        tree[i] = new node();
    }

    // build the tree
    build(a, 0, n - 1, 0);

    // 1st query type-1
    int l = 5, r = 8;
    System.out.print(query(a, 0, 0, n - 1,
                     l - 1, r - 1).maxsum);
    System.out.println();

    // 2nd type-2 query
    int index = 1;
    int value = 10;
    a[index - 1] = value;
    update(a, 0, 0, n - 1, index - 1, value);

    // 3rd type-1 query
    l = 1;
    r = 3;
    System.out.print(query(a, 0, 0, n - 1,
                             l - 1, r - 1).maxsum);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find Largest Sum Contiguous
# Subarray in a given range with updates
from sys import maxsize

INT_MIN = -maxsize

# Structure to store
# 4 values that are to be stored
# in the nodes
class node:
    def __init__(self):
        self.sum = 0
        self.prefixsum = 0
        self.suffixsum = 0
        self.maxsum = 0

# array to store the segment tree
tree = [0] * (4 * 100)
for i in range(4 * 100):
    tree[i] = node()

def build(arr: list, low: int, high: int, index: int):
    global tree

    # the leaf node
    if low == high:
        tree[index].sum = arr[low]
        tree[index].prefixsum = arr[low]
        tree[index].suffixsum = arr[low]
        tree[index].maxsum = arr[low]
    else:
        mid = (low + high) >> 1

        # left subtree
        build(arr, low, mid, 2 * index + 1)

        # right subtree
        build(arr, mid + 1, high, 2 * index + 2)

        # parent node's sum is the summation
        # of left and right child
        tree[index].sum = tree[2 * index + 1].sum + \
                            tree[2 * index + 2].sum

        # parent node's prefix sum will be equivalent
        # to maximum of left child's prefix sum or left
        # child sum + right child prefix sum.
        tree[index].prefixsum = max(
            tree[2 * index + 1].prefixsum,
            tree[2 * index + 1].sum + tree[2 * index + 2].prefixsum)

        # parent node's suffix sum will be equal to right
        # child suffix sum or right child sum + suffix
        # sum of left child
        tree[index].suffixsum = max(
            tree[2 * index + 2].suffixsum,
            tree[2 * index + 2].sum + tree[2 * index + 1].suffixsum)

        # maximum will be the maximum of prefix, suffix of
        # parent or maximum of left child or right child
        # and summation of left child's suffix and right
        # child's prefix.
        tree[index].maxsum = max(tree[index].prefixsum,
            max(tree[index].suffixsum,
                max(tree[2 * index + 1].maxsum,
                    max(tree[2 * index + 2].maxsum,
                        tree[2 * index + 1].suffixsum +
                        tree[2 * index + 2].prefixsum))))

# function to update the tree
def update(arr: list, index: int, low: int,
            high: int, idx: int, value: int):
    global tree

    # the node to be updated
    if low == high:
        tree[index].sum = value
        tree[index].prefixsum = value
        tree[index].suffixsum = value
        tree[index].maxsum = value
    else:
        mid = (low + high) >> 1

        # if node to be updated is in left subtree
        if idx <= mid:
            update(arr, 2 * index + 1,
                    low, mid, idx, value)

        # if node to be updated is in right subtree
        else:
            update(arr, 2 * index + 2,
                    mid + 1, high, idx, value)

        # parent node's sum is the summation of left
        # and right child
        tree[index].sum = tree[2 * index + 1].sum + \
                            tree[2 * index + 2].sum

        # parent node's prefix sum will be equivalent
        # to maximum of left child's prefix sum or left
        # child sum + right child prefix sum.
        tree[index].prefixsum = max(tree[2 * index + 1].prefixsum,
            tree[2 * index + 1].sum + tree[2 * index + 2].prefixsum)

        # parent node's suffix sum will be equal to right
        # child suffix sum or right child sum + suffix
        # sum of left child
        tree[index].suffixsum = max(tree[2 * index + 2].suffixsum,
            tree[2 * index + 2].sum + tree[2 * index + 1].suffixsum)

        # maximum will be the maximum of prefix, suffix of
        # parent or maximum of left child or right child
        # and summation of left child's suffix and
        # right child's prefix.
        tree[index].maxsum = max(tree[index].prefixsum,
            max(tree[index].suffixsum,
                max(tree[2 * index + 1].maxsum,
                    max(tree[2 * index + 2].maxsum,
                        tree[2 * index + 1].suffixsum +
                        tree[2 * index + 2].prefixsum))))

# function to return answer to every type-1 query
def query(arr: list, index: int, low: int,
        high: int, l: int, r: int) -> node:

    # initially all the values are INT_MIN
    result = node()
    result.sum = result.prefixsum = result.\
    suffixsum = result.maxsum = INT_MIN

    # range does not lies in this subtree
    if r < low or high < l:
        return result

    # complete overlap of range
    if l <= low and high <= r:
        return tree[index]

    mid = (low + high) >> 1

    # right subtree
    if l > mid:
        return query(arr, 2 * index + 2,
                        mid + 1, high, l, r)

    # left subtree
    if r <= mid:
        return query(arr, 2 * index + 1, low, mid, l, r)

    left = query(arr, 2 * index + 1, low, mid, l, r)
    right = query(arr, 2 * index + 2, mid + 1, high, l, r)

    # finding the maximum and returning it
    result.sum = left.sum + right.sum
    result.prefixsum = max(left.prefixsum,
                       left.sum + right.prefixsum)

    result.suffixsum = max(right.suffixsum,
                        right.sum + left.suffixsum)
    result.maxsum = max(result.prefixsum,
        max(result.suffixsum,
            max(left.maxsum, max(right.maxsum,
            left.suffixsum + right.prefixsum))))

    return result

# Driver Code
if __name__ == "__main__":

    a = [-2, -3, 4, -1, -2, 1, 5, -3]
    n = len(a)

    # build the tree
    build(a, 0, n - 1, 0)

    # 1st query type-1
    l = 5
    r = 8
    print(query(a, 0, 0, n - 1, l - 1, r - 1).maxsum)

    # 2nd type-2 query
    index = 1
    value = 10
    a[index - 1] = value
    update(a, 0, 0, n - 1, index - 1, value)

    # 3rd type-1 query
    l = 1
    r = 3
    print(query(a, 0, 0, n - 1, l - 1, r - 1).maxsum)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find Largest Sum Contiguous
// Subarray in a given range with updates
using System;
using System.Collections.Generic;

class GFG
{

// Structure to store 4 values that are
// to be stored in the nodes
public class node
{
    public int sum, prefixsum, suffixsum, maxsum;
};

// array to store the segment tree
static node[] tree = new node[4 * 100];

// function to build the tree
static void build(int []arr, int low,
                int high, int index)
{
    // the leaf node
    if (low == high)
    {
        tree[index].sum = arr[low];
        tree[index].prefixsum = arr[low];
        tree[index].suffixsum = arr[low];
        tree[index].maxsum = arr[low];
    }
    else
    {
        int mid = (low + high) / 2;

        // left subtree
        build(arr, low, mid, 2 * index + 1);

        // right subtree
        build(arr, mid + 1, high, 2 * index + 2);

        // parent node's sum is the summation
        // of left and right child
        tree[index].sum = tree[2 * index + 1].sum +
                        tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.Max(tree[2 * index + 1].prefixsum,
                                        tree[2 * index + 1].sum +
                                        tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.Max(tree[2 * index + 2].suffixsum,
                                        tree[2 * index + 2].sum +
                                        tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and right
        // child's prefix.
        tree[index].maxsum = Math.Max(tree[index].prefixsum,
                            Math.Max(tree[index].suffixsum,
                            Math.Max(tree[2 * index + 1].maxsum,
                            Math.Max(tree[2 * index + 2].maxsum,
                                    tree[2 * index + 1].suffixsum +
                                    tree[2 * index + 2].prefixsum))));
    }
}

// function to update the tree
static void update(int []arr, int index, int low,
                int high, int idx, int value)
{
    // the node to be updated
    if (low == high)
    {
        tree[index].sum = value;
        tree[index].prefixsum = value;
        tree[index].suffixsum = value;
        tree[index].maxsum = value;
    }
    else
    {
        int mid = (low + high) / 2;

        // if node to be updated is in left subtree
        if (idx <= mid)
        {
            update(arr, 2 * index + 1, low,
                        mid, idx, value);
        }

        // if node to be updated is in right subtree
        else
        {
            update(arr, 2 * index + 2, mid + 1,
                            high, idx, value);
        }

        // parent node's sum is the summation of left
        // and right child
        tree[index].sum = tree[2 * index + 1].sum +
                        tree[2 * index + 2].sum;

        // parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.Max(tree[2 * index + 1].prefixsum,
                                        tree[2 * index + 1].sum +
                                        tree[2 * index + 2].prefixsum);

        // parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.Max(tree[2 * index + 2].suffixsum,
                                        tree[2 * index + 2].sum +
                                        tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and
        // right child's prefix.
        tree[index].maxsum = Math.Max(tree[index].prefixsum,
                            Math.Max(tree[index].suffixsum,
                            Math.Max(tree[2 * index + 1].maxsum,
                            Math.Max(tree[2 * index + 2].maxsum,
                                    tree[2 * index + 1].suffixsum +
                                    tree[2 * index + 2].prefixsum))));
    }
}

// function to return answer to every type-1 query
static node query(int []arr, int index,
                int low, int high, int l, int r)
{
    // initially all the values are int.MinValue
    node result = new node();
    result.sum = result.prefixsum
            = result.suffixsum
            = result.maxsum = int.MinValue;

    // range does not lies in this subtree
    if (r < low || high < l)
    {
        return result;
    }

    // complete overlap of range
    if (l <= low && high <= r)
    {
        return tree[index];
    }

    int mid = (low + high) / 2;

    // right subtree
    if (l > mid)
    {
        return query(arr, 2 * index + 2,
                    mid + 1, high, l, r);
    }

    // left subtree
    if (r <= mid)
    {
        return query(arr, 2 * index + 1,
                    low, mid, l, r);
    }

    node left = query(arr, 2 * index + 1,
                    low, mid, l, r);
    node right = query(arr, 2 * index + 2,
                    mid + 1, high, l, r);

    // finding the maximum and returning it
    result.sum = left.sum + right.sum;
    result.prefixsum = Math.Max(left.prefixsum,
                                left.sum + right.prefixsum);

    result.suffixsum = Math.Max(right.suffixsum,
                                right.sum + left.suffixsum);
    result.maxsum = Math.Max(result.prefixsum,
                    Math.Max(result.suffixsum,
                    Math.Max(left.maxsum,
                    Math.Max(right.maxsum, left.suffixsum +
                            right.prefixsum))));

    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = {-2, -3, 4, -1, -2, 1, 5, -3};
    int n = a.Length;
    for (int i = 0; i < 4 * 100; i++)
    {
        tree[i] = new node();
    }

    // build the tree
    build(a, 0, n - 1, 0);

    // 1st query type-1
    int l = 5, r = 8;
    Console.Write(query(a, 0, 0, n - 1,
                    l - 1, r - 1).maxsum);
    Console.WriteLine();

    // 2nd type-2 query
    int index = 1;
    int value = 10;
    a[index - 1] = value;
    update(a, 0, 0, n - 1, index - 1, value);

    // 3rd type-1 query
    l = 1;
    r = 3;
    Console.Write(query(a, 0, 0, n - 1,
                            l - 1, r - 1).maxsum);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find Largest Sum
// Contiguous Subarray in a given range
// with updates

// Structure to store 4 values that are
// to be stored in the nodes
class node
{
    constructor()
    {
        this.sum = 0;
        this.prefixsum = 0;
        this.suffixsum = 0;
        this.maxsum = 0;
    }
};

// Array to store the segment tree
var tree = Array(4 * 100).fill(new node());

// Function to build the tree
function build(arr, low, high, index)
{

    // The leaf node
    if (low == high)
    {
        tree[index].sum = arr[low];
        tree[index].prefixsum = arr[low];
        tree[index].suffixsum = arr[low];
        tree[index].maxsum = arr[low];
    }
    else
    {
        var mid = parseInt((low + high) / 2);

        // Left subtree
        build(arr, low, mid, 2 * index + 1);

        // Right subtree
        build(arr, mid + 1, high, 2 * index + 2);

        // Parent node's sum is the summation
        // of left and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // Parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.max(tree[2 * index + 1].prefixsum,
                                         tree[2 * index + 1].sum +
                                         tree[2 * index + 2].prefixsum);

        // Parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.max(tree[2 * index + 2].suffixsum,
                                         tree[2 * index + 2].sum +
                                         tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and right
        // child's prefix.
        tree[index].maxsum = Math.max(tree[index].prefixsum,
                            Math.max(tree[index].suffixsum,
                            Math.max(tree[2 * index + 1].maxsum,
                            Math.max(tree[2 * index + 2].maxsum,
                                     tree[2 * index + 1].suffixsum +
                                     tree[2 * index + 2].prefixsum))));
    }
}

// Function to update the tree
function update(arr, index, low, high, idx, value)
{

    // The node to be updated
    if (low == high)
    {
        tree[index].sum = value;
        tree[index].prefixsum = value;
        tree[index].suffixsum = value;
        tree[index].maxsum = value;
    }
    else
    {
        var mid = parseInt((low + high) / 2);

        // If node to be updated is in left subtree
        if (idx <= mid)
        {
            update(arr, 2 * index + 1, low,
                   mid, idx, value);
        }

        // If node to be updated is in right subtree
        else
        {
            update(arr, 2 * index + 2, mid + 1,
                   high, idx, value);
        }

        // Parent node's sum is the summation of left
        // and right child
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // Parent node's prefix sum will be equivalent
        // to maximum of left child's prefix sum or left
        // child sum + right child prefix sum.
        tree[index].prefixsum = Math.max(tree[2 * index + 1].prefixsum,
                                         tree[2 * index + 1].sum +
                                         tree[2 * index + 2].prefixsum);

        // Parent node's suffix sum will be equal to right
        // child suffix sum or right child sum + suffix
        // sum of left child
        tree[index].suffixsum = Math.max(tree[2 * index + 2].suffixsum,
                                         tree[2 * index + 2].sum +
                                         tree[2 * index + 1].suffixsum);

        // maximum will be the maximum of prefix, suffix of
        // parent or maximum of left child or right child
        // and summation of left child's suffix and
        // right child's prefix.
        tree[index].maxsum = Math.max(tree[index].prefixsum,
                            Math.max(tree[index].suffixsum,
                            Math.max(tree[2 * index + 1].maxsum,
                            Math.max(tree[2 * index + 2].maxsum,
                                     tree[2 * index + 1].suffixsum +
                                     tree[2 * index + 2].prefixsum))));
    }
}

// Function to return answer to every type-1 query
function query(arr, index, low, high, l, r)
{

    // Initially all the values are int.MinValue
    var result = new node();
    result.sum = result.prefixsum = result.suffixsum =
                 result.maxsum = -1000000000;

    // Range does not lies in this subtree
    if (r < low || high < l)
    {
        return result;
    }

    // Complete overlap of range
    if (l <= low && high <= r)
    {
        return tree[index];
    }

    var mid = parseInt((low + high) / 2);

    // Right subtree
    if (l > mid)
    {
        return query(arr, 2 * index + 2,
                     mid + 1, high, l, r);
    }

    // Left subtree
    if (r <= mid)
    {
        return query(arr, 2 * index + 1,
                     low, mid, l, r);
    }

    var left = query(arr, 2 * index + 1,
                     low, mid, l, r);
    var right = query(arr, 2 * index + 2,
                      mid + 1, high, l, r);

    // Finding the maximum and returning it
    result.sum = left.sum + right.sum;
    result.prefixsum = Math.max(left.prefixsum,
                                left.sum + right.prefixsum);

    result.suffixsum = Math.max(right.suffixsum,
                                right.sum + left.suffixsum);
    result.maxsum = Math.max(result.prefixsum,
                    Math.max(result.suffixsum,
                    Math.max(left.maxsum,
                    Math.max(right.maxsum, left.suffixsum +
                             right.prefixsum))));

    return result;
}

// Driver Code
var a = [ -2, -3, 4, -1, -2, 1, 5, -3 ];
var n = a.length;

for(var i = 0; i < 4 * 100; i++)
{
    tree[i] = new node();
}

// Build the tree
build(a, 0, n - 1, 0);

// 1st query type-1
var l = 5, r = 8;
document.write(query(a, 0, 0, n - 1,
                       l - 1, r - 1).maxsum);
document.write("<br>");

// 2nd type-2 query
var index = 1;
var value = 10;
a[index - 1] = value;
update(a, 0, 0, n - 1, index - 1, value);

// 3rd type-1 query
l = 1;
r = 3;
document.write(query(a, 0, 0, n - 1,
                       l - 1, r - 1).maxsum);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
6
11
```

**时间复杂度:** O(n log n)用于构建树，O(log n)用于每个类型 1 查询，O(1)用于类型 2 查询。