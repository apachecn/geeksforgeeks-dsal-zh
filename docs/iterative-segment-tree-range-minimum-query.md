# 迭代段树(范围最小查询)

> 原文:[https://www . geesforgeks . org/iterative-segment-tree-range-minimum-query/](https://www.geeksforgeeks.org/iterative-segment-tree-range-minimum-query/)

我们已经讨论了[递归段树实现](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。在这篇文章中，将讨论迭代实现。
让我们考虑以下问题了解段树。
我们有一个数组 arr[0。。。n-1]。我们应该能够
1 找到从索引 l 到 r 的元素的最小值，其中 0 < = l < = r < = n-1
2 将数组中指定元素的值更改为新值 x。我们需要进行 arr[i] = x，其中 0 < = i < = n-1。
**举例:**

```
Input : 2, 6, 7, 5, 18, 86, 54, 2
        minimum(2, 7)  
        update(3, 4)
        minimum(2, 6) 
Output : Minimum in range 2 to 7 is 2.
         Minimum in range 2 to 6 is 4.
```

分段树的迭代版本基本上使用了这样一个事实，对于索引 I，树中的左子级= 2 * i，右子级= 2 * i + 1。段树数组中索引 I 的父级可以通过 parent = i / 2 找到。因此，我们可以很容易地一个接一个地在树的各个层次上下移动。首先，我们计算范围内的最小值，同时从叶节点开始构建树，并一个接一个地向上爬。我们在处理查询以寻找范围内的最小值时使用相同的概念。因为在最坏的情况下有(log n)个级别，所以查询需要 log n 个时间。为了将特定索引更新为给定值，我们从叶节点开始更新段树，并通过在每次迭代中逐渐向上移动级别来更新受当前节点更新影响的所有节点。更新也需要 log n 时间，因为在那里我们必须从叶节点开始更新所有级别，在那里我们在用户给出的精确索引处更新精确值。

## C++

```
// CPP Program to implement iterative segment
// tree.
#include <bits/stdc++.h>
#define ll long long

using namespace std;

void construct_segment_tree(vector<int>& segtree,
                           vector<int> &a, int n)
{
    // assign values to leaves of the segment tree
    for (int i = 0; i < n; i++)
        segtree[n + i] = a[i];   

    /* assign values to internal nodes
      to compute minimum in a given range */
    for (int i = n - 1; i >= 1; i--)
        segtree[i] = min(segtree[2 * i],
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
        segtree[pos] = min(segtree[2 * pos],
                           segtree[2 * pos + 1]);
    }
}

int range_query(vector<int>& segtree, int left, int
                                      right, int n)
{
    /*  Basically the left and right indices will move
        towards right and left respectively and with
        every each next higher level and compute the
        minimum at each height. */
    // change the index to leaf node first
    left += n;
    right += n;

    // initialize minimum to a very high value
    int mi = (int)1e9;

    while (left < right) {

        // if left index in odd
        if (left & 1) {
            mi = min(mi, segtree[left]);

            // make left index even
            left++;
        }

        // if right index in odd
        if (right & 1) {

            // make right index even
            right--;

            mi = min(mi, segtree[right]);
        }

        // move to the next higher level
        left /= 2;
        right /= 2;
    }
    return mi;
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

    // compute minimum in the range left to right
    int left = 0, right = 5;
    cout << "Minimum in range " << left << " to "
         << right << " is "<< range_query(segtree, left,
                                  right + 1, n) << "\n";

    // update the value of index 3 to 1
    int index = 3, value = 1;

    // a[3] = 1;
    // Contents of array : {2, 6, 10, 1, 7, 28, 9, 11, 6, 33}
    update(segtree, index, value, n); // point update

    // compute minimum in the range left to right
    left = 2, right = 6;
    cout << "Minimum in range " << left << " to "
         << right << " is " << range_query(segtree,
                      left, right + 1, n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement iterative segment
// tree.
import java.io.*;
import java.util.*;

class GFG
{

    static void construct_segment_tree(int[] segtree,
                                        int[] a, int n)
    {

        // assign values to leaves of the segment tree
        for (int i = 0; i < n; i++)
            segtree[n + i] = a[i];

        /*
        * assign values to internal nodes
        * to compute minimum in a given range
        */
        for (int i = n - 1; i >= 1; i--)
            segtree[i] = Math.min(segtree[2 * i], segtree[2 * i + 1]);
    }

    static void update(int[] segtree, int pos, int value, int n)
    {

        // change the index to leaf node first
        pos += n;

        // update the value at the leaf node
        // at the exact index
        segtree[pos] = value;

        while (pos > 1)
        {

            // move up one level at a time in the tree
            pos >>= 1;

            // update the values in the nodes in
            // the next higher level
            segtree[pos] = Math.min(segtree[2 * pos],
                                segtree[2 * pos + 1]);
        }
    }

    static int range_query(int[] segtree, int left,
                           int right, int n)
    {

        /*
        * Basically the left and right indices will move
        * towards right and left respectively and with
        * every each next higher level and compute the
        * minimum at each height. */
        // change the index to leaf node first
        left += n;
        right += n;

        // initialize minimum to a very high value
        int mi = (int) 1e9;

        while (left < right)
        {

            // if left index in odd
            if ((left & 1) == 1)
            {
                mi = Math.min(mi, segtree[left]);

                // make left index even
                left++;
            }

            // if right index in odd
            if ((right & 1) == 1)
            {

                // make right index even
                right--;

                mi = Math.min(mi, segtree[right]);
            }

            // move to the next higher level
            left /= 2;
            right /= 2;
        }
        return mi;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = {2, 6, 10, 4, 7, 28, 9, 11, 6, 33};
        int n = a.length;

        /*
        * Construct the segment tree by assigning
        * the values to the internal nodes
        */
        int[] segtree = new int[2 * n];
        construct_segment_tree(segtree, a, n);

        // compute minimum in the range left to right
        int left = 0, right = 5;
        System.out.printf("Minimum in range %d to %d is %d\n",
                           left, right, range_query(segtree,
                           left, right + 1, n));

        // update the value of index 3 to 1
        int index = 3, value = 1;

        // a[3] = 1;
        // Contents of array : {2, 6, 10, 1, 7, 28, 9, 11, 6, 33}
        update(segtree, index, value, n); // point update

        // compute minimum in the range left to right
        left = 2;
        right = 6;
        System.out.printf("Minimum in range %d to %d is %d\n",
                           left, right, range_query(segtree,
                           left, right + 1, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to implement
# iterative segment tree.
def construct_segment_tree(segtree, a, n):

    # assign values to leaves of
    # the segment tree
    for i in range(n):
        segtree[n + i] = a[i];

    # assign values to remaining nodes
    # to compute minimum in a given range
    for i in range(n - 1, 0, -1):
        segtree[i] = min(segtree[2 * i],
                         segtree[2 * i + 1])

def range_query(segtree, left, right, n):
    left += n
    right += n

    """ Basically the left and right indices
        will move towards right and left respectively
        and with every each next higher level and
        compute the minimum at each height change
        the index to leaf node first """
    mi = 1e9 # initialize minimum to a very high value
    while (left < right):
        if (left & 1): # if left index in odd
                mi = min(mi, segtree[left])
                left = left + 1
        if (right & 1): # if right index in odd
                right -= 1
                mi = min(mi, segtree[right])

        # move to the next higher level
        left = left // 2
        right = right // 2
    return mi

def update(segtree, pos, value, n):

    # change the index to leaf node first
    pos += n

    # update the value at the leaf node
    # at the exact index
    segtree[pos] = value
    while (pos > 1):

        # move up one level at a time in the tree
        pos >>= 1;

        # update the values in the nodes
        # in the next higher level
        segtree[pos] = min(segtree[2 * pos],
                           segtree[2 * pos + 1])

# Driver Code    

# Elements in list
a = [2, 6, 10, 4, 7, 28, 9, 11, 6, 33]
n = len(a)

# Construct the segment tree by assigning
# the values to the internal nodes
segtree = [0 for i in range(2 * n)]
construct_segment_tree(segtree, a, n);
left = 0
right = 5 #compute minimum in the range left to right
print ("Minimum in range", left, "to", right, "is",
        range_query(segtree, left, right + 1, n))

# update the value of index 3 to 1
index = 3
value = 1

# a[3] = 1;
# Contents of array : {2, 6, 10, 1, 7, 28, 9, 11, 6, 33}
update(segtree, index, value, n); # point update
left = 2
right = 6 # compute minimum in the range left to right
print("Minimum in range", left, "to", right, "is",
       range_query(segtree, left, right + 1, n))

# This code is contributed by sarthak Raghuwanshi
```

## C#

```
// C# Program to implement iterative segment
// tree.
using System;

class GFG
{

    static void construct_segment_tree(int[] segtree,
                                        int[] a, int n)
    {

        // assign values to leaves of the segment tree
        for (int i = 0; i < n; i++)
            segtree[n + i] = a[i];

        /*
        * assign values to internal nodes
        * to compute minimum in a given range
        */
        for (int i = n - 1; i >= 1; i--)
            segtree[i] = Math.Min(segtree[2 * i],
                            segtree[2 * i + 1]);
    }

    static void update(int[] segtree, int pos,
                        int value, int n)
    {

        // change the index to leaf node first
        pos += n;

        // update the value at the leaf node
        // at the exact index
        segtree[pos] = value;

        while (pos > 1)
        {

            // move up one level at a time in the tree
            pos >>= 1;

            // update the values in the nodes in
            // the next higher level
            segtree[pos] = Math.Min(segtree[2 * pos],
                                segtree[2 * pos + 1]);
        }
    }

    static int range_query(int[] segtree, int left,
                        int right, int n)
    {

        /*
        * Basically the left and right indices will move
        * towards right and left respectively and with
        * every each next higher level and compute the
        * minimum at each height. */
        // change the index to leaf node first
        left += n;
        right += n;

        // initialize minimum to a very high value
        int mi = (int) 1e9;

        while (left < right)
        {

            // if left index in odd
            if ((left & 1) == 1)
            {
                mi = Math.Min(mi, segtree[left]);

                // make left index even
                left++;
            }

            // if right index in odd
            if ((right & 1) == 1)
            {

                // make right index even
                right--;

                mi = Math.Min(mi, segtree[right]);
            }

            // move to the next higher level
            left /= 2;
            right /= 2;
        }
        return mi;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = {2, 6, 10, 4, 7, 28, 9, 11, 6, 33};
        int n = a.Length;

        /*
        * Construct the segment tree by assigning
        * the values to the internal nodes
        */
        int[] segtree = new int[2 * n];
        construct_segment_tree(segtree, a, n);

        // compute minimum in the range left to right
        int left = 0, right = 5;
        Console.Write("Minimum in range {0} to {1} is {2}\n",
                        left, right, range_query(segtree,
                        left, right + 1, n));

        // update the value of index 3 to 1
        int index = 3, value = 1;

        // a[3] = 1;
        // Contents of array : {2, 6, 10, 1, 7, 28, 9, 11, 6, 33}
        update(segtree, index, value, n); // point update

        // compute minimum in the range left to right
        left = 2;
        right = 6;
        Console.Write("Minimum in range {0} to {1} is {2}\n",
                        left, right, range_query(segtree,
                        left, right + 1, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript Program to implement iterative segment
// tree.
function construct_segment_tree(segtree, a, n)
{

    // assign values to leaves of the segment tree
    for (var i = 0; i < n; i++)
        segtree[n + i] = a[i];
    /*
    * assign values to internal nodes
    * to compute minimum in a given range
    */
    for (var i = n - 1; i >= 1; i--)
        segtree[i] = Math.min(segtree[2 * i],
                        segtree[2 * i + 1]);
}
function update(segtree, pos, value, n)
{
    // change the index to leaf node first
    pos += n;

    // update the value at the leaf node
    // at the exact index
    segtree[pos] = value;
    while (pos > 1)
    {
        // move up one level at a time in the tree
        pos >>= 1;

        // update the values in the nodes in
        // the next higher level
        segtree[pos] = Math.min(segtree[2 * pos],
                            segtree[2 * pos + 1]);
    }
}
function range_query(segtree, left, right, n)
{

    /*
    * Basically the left and right indices will move
    * towards right and left respectively and with
    * every each next higher level and compute the
    * minimum at each height. */
    // change the index to leaf node first
    left += n;
    right += n;
    // initialize minimum to a very high value
    var mi = 1000000000;
    while (left < right)
    {

        // if left index in odd
        if ((left & 1) == 1)
        {
            mi = Math.min(mi, segtree[left]);
            // make left index even
            left++;
        }
        // if right index in odd
        if ((right & 1) == 1)
        {
            // make right index even
            right--;
            mi = Math.min(mi, segtree[right]);
        }
        // move to the next higher level
        left /= 2;
        right /= 2;
    }
    return mi;
}

// Driver Code
var a = [2, 6, 10, 4, 7, 28, 9, 11, 6, 33];
var n = a.length;
/*
* Construct the segment tree by assigning
* the values to the internal nodes
*/
var segtree = Array(2*n).fill(0);
construct_segment_tree(segtree, a, n);

// compute minimum in the range left to right
var left = 0, right = 5;
document.write(`Minimum in range ${left} to ${right} is ${range_query(segtree,left, right + 1, n)}<br>`)

// update the value of index 3 to 1
var index = 3, value = 1;

// a[3] = 1;
// Contents of array : {2, 6, 10, 1, 7, 28, 9, 11, 6, 33}
update(segtree, index, value, n); // point update

// compute minimum in the range left to right
left = 2;
right = 6;
document.write(`Minimum in range ${left} to ${right} is ${range_query(segtree, left, right + 1, n)}<br>`);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Minimum in range 0 to 5 is 2
Minimum in range 2 to 6 is 1
```

**时间复杂度:**(n log n)
T3】辅助空间: (n)