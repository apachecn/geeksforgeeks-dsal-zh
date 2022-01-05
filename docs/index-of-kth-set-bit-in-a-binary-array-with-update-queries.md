# 带有更新查询的二进制数组中第 kth 组位的索引

> 原文:[https://www . geeksforgeeks . org/index-of-kth-set-bit-in-a-a-array-with-update-query/](https://www.geeksforgeeks.org/index-of-kth-set-bit-in-a-binary-array-with-update-queries/)

给定二进制数组 **arr[]** 和 **q** 以下类型的查询:

1.  **k:** 求数组中 **k <sup>第</sup>组位**即 **k <sup>第</sup> 1** 的索引。
2.  **(x，y):** 更新 **arr[x] = y** ，其中 **y** 可以是 **0** 或 **1** 。

**例:**

> **输入:** arr[] = {1，0，1，0，0，1，1}，q = 2
> k = 4
> (x，y) = (5，1)
> **输出:**
> 第 4 组位的索引:6
> 数组更新后:
> 1 0 1 0 0 1

**方法:**一个简单的解决方案是运行从 **0** 到**n–1**的循环，并找到 **k <sup>th</sup>** **1** 。要更新一个值，只需执行 **arr[i] = x** 。第一次操作需要 **O(n)** 时间，第二次操作需要 **O(1)** 时间。
**另一种解决方案**是创建另一个数组，并将每个 1 的索引存储在该数组中的第 1 个索引处。**K<sup>th</sup>****1**的索引现在可以在 **O(1)** 时间计算，但是更新操作现在需要 **O(n)** 时间。如果查询操作的数量很大，并且更新很少，这种方法就能很好地工作。
但是，如果查询和更新的次数相等呢？我们可以使用 [**段树**](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/) 在 **O(Logn)** 时间执行这两个操作。

> 线段树的表示:
> 
> 1.  叶节点是输入数组的元素。
> 2.  每个内部节点代表叶节点的总和合并。
> 
> 树的数组表示用于表示段树。对于索引 I 处的每个节点，左子节点位于索引 2*i+1 处，右子节点位于索引 2*i+2 处，父节点位于(i-1)/2 处。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to build the tree
void buildTree(int* tree, int* a, int s, int e, int idx)
{
    // s = starting index
    // e = ending index
    // a = array storing binary string of numbers
    // idx = starting index = 1, for recurring the tree
    if (s == e) {

        // store each element value at the
        // leaf node
        tree[idx] = a[s];
        return;
    }

    int mid = (s + e) / 2;

    // Recurring in two sub portions (left, right)
    // to build the segment tree

    // Calling for the left sub portion
    buildTree(tree, a, s, mid, 2 * idx);

    // Calling for the right sub portion
    buildTree(tree, a, mid + 1, e, 2 * idx + 1);

    // Summing up the number of one's
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1];

    return;
}

// Function to return the index of the query
int queryTree(int* tree, int s, int e, int k, int idx)
{
    // s = starting index
    // e = ending index
    // k = searching for kth bit
    // idx = starting index = 1, for recurring the tree

    // k > number of 1's in a binary string
    if (k > tree[idx])
        return -1;

    // leaf node at which kth 1 is stored
    if (s == e)
        return s;
    int mid = (s + e) / 2;

    // If left sub-tree contains more or equal 1's
    // than required kth 1
    if (tree[2 * idx] >= k)
        return queryTree(tree, s, mid, k, 2 * idx);

    // If left sub-tree contains less 1's than
    // required kth 1 then recur in the right sub-tree
    else
        return queryTree(tree, mid + 1, e, k - tree[2 * idx], 2 * idx + 1);
}

// Function to perform the update query
void updateTree(int* tree, int s, int e, int i, int change, int idx)
{
    // s = starting index
    // e = ending index
    // i = index at which change is to be done
    // change = new changed bit
    // idx = starting index = 1, for recurring the tree

    // Out of bounds request
    if (i < s || i > e) {
        cout << "error";
        return;
    }

    // Leaf node of the required index i
    if (s == e) {

        // Replacing the node value with
        // the new changed value
        tree[idx] = change;
        return;
    }

    int mid = (s + e) / 2;

    // If the index i lies in the left sub-tree
    if (i >= s && i <= mid)
        updateTree(tree, s, mid, i, change, 2 * idx);

    // If the index i lies in the right sub-tree
    else
        updateTree(tree, mid + 1, e, i, change, 2 * idx + 1);

    // Merging both left and right sub-trees
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
    return;
}

// Function to perform queries
void queries(int* tree, int* a, int q, int p, int k, int change, int n)
{
    int s = 0, e = n - 1, idx = 1;
    if (q == 1) {
        // q = 1 update, p = index at which change
        // is to be done, change = new bit
        a[p] = change;
        updateTree(tree, s, e, p, change, idx);
        cout << "Array after updation:\n";
        for (int i = 0; i < n; i++)
            cout << a[i] << " ";
        cout << "\n";
    }
    else {
        // q = 0, print kth bit
        cout << "Index of " << k << "th set bit: "
             << queryTree(tree, s, e, k, idx) << "\n";
    }
}

// Driver code
int main()
{
    int a[] = { 1, 0, 1, 0, 0, 1, 1, 1 };
    int n = sizeof(a) / sizeof(int);

    // Declaring & initializing the tree with
    // maximum possible size of the segment tree
    // and each value initially as 0
    int* tree = new int[4 * n + 1];
    for (int i = 0; i < 4 * n + 1; ++i) {
        tree[i] = 0;
    }

    // s and e are the starting and ending
    // indices respectively
    int s = 0, e = n - 1, idx = 1;

    // Build the segment tree
    buildTree(tree, a, s, e, idx);

    // Find index of kth set bit
    int q = 0, p = 0, change = 0, k = 4;
    queries(tree, a, q, p, k, change, n);

    // Update query
    q = 1, p = 5, change = 0;
    queries(tree, a, q, p, k, change, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function to build the tree
    static void buildTree(int[] tree, int[] a,
                       int s, int e, int idx)
    {

        // s = starting index
        // e = ending index
        // a = array storing binary string of numbers
        // idx = starting index = 1, for recurring the tree
        if (s == e)
        {

            // store each element value at the
            // leaf node
            tree[idx] = a[s];
            return;
        }

        int mid = (s + e) / 2;

        // Recurring in two sub portions (left, right)
        // to build the segment tree

        // Calling for the left sub portion
        buildTree(tree, a, s, mid, 2 * idx);

        // Calling for the right sub portion
        buildTree(tree, a, mid + 1, e, 2 * idx + 1);

        // Summing up the number of one's
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];

        return;
    }

    // Function to return the index of the query
    static int queryTree(int[] tree, int s,
                        int e, int k, int idx)
    {

        // s = starting index
        // e = ending index
        // k = searching for kth bit
        // idx = starting index = 1, for recurring the tree

        // k > number of 1's in a binary string
        if (k > tree[idx])
            return -1;

        // leaf node at which kth 1 is stored
        if (s == e)
            return s;
        int mid = (s + e) / 2;

        // If left sub-tree contains more or equal 1's
        // than required kth 1
        if (tree[2 * idx] >= k)
            return queryTree(tree, s, mid, k, 2 * idx);

        // If left sub-tree contains less 1's than
        // required kth 1 then recur in the right sub-tree
        else
            return queryTree(tree, mid + 1, e, k - tree[2 * idx],
                                                    2 * idx + 1);
    }

    // Function to perform the update query
    static void updateTree(int[] tree, int s, int e,
                            int i, int change, int idx)
    {

        // s = starting index
        // e = ending index
        // i = index at which change is to be done
        // change = new changed bit
        // idx = starting index = 1, for recurring the tree

        // Out of bounds request
        if (i < s || i > e)
        {
            System.out.println("Error");
            return;
        }

        // Leaf node of the required index i
        if (s == e)
        {

            // Replacing the node value with
            // the new changed value
            tree[idx] = change;
            return;
        }

        int mid = (s + e) / 2;

        // If the index i lies in the left sub-tree
        if (i >= s && i <= mid)
            updateTree(tree, s, mid, i, change, 2 * idx);

        // If the index i lies in the right sub-tree
        else
            updateTree(tree, mid + 1, e, i, change, 2 * idx + 1);

        // Merging both left and right sub-trees
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
        return;
    }

    // Function to perform queries
    static void queries(int[] tree, int[] a, int q, int p,
                                int k, int change, int n)
    {
        int s = 0, e = n - 1, idx = 1;
        if (q == 1)
        {

            // q = 1 update, p = index at which change
            // is to be done, change = new bit
            a[p] = change;
            updateTree(tree, s, e, p, change, idx);
            System.out.println("Array after updation:");
            for (int i = 0; i < n; i++)
                System.out.print(a[i] + " ");
            System.out.println();
        }
        else
        {

            // q = 0, print kth bit
            System.out.printf("Index of %dth set bit: %d\n",
                                k, queryTree(tree, s, e, k, idx));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 1, 0, 1, 0, 0, 1, 1, 1 };
        int n = a.length;

        // Declaring & initializing the tree with
        // maximum possible size of the segment tree
        // and each value initially as 0
        int[] tree = new int[4 * n + 1];
        for (int i = 0; i < 4 * n + 1; ++i)
        {
            tree[i] = 0;
        }

        // s and e are the starting and ending
        // indices respectively
        int s = 0, e = n - 1, idx = 1;

        // Build the segment tree
        buildTree(tree, a, s, e, idx);

        // Find index of kth set bit
        int q = 0, p = 0, change = 0, k = 4;
        queries(tree, a, q, p, k, change, n);

        // Update query
        q = 1;
        p = 5;
        change = 0;
        queries(tree, a, q, p, k, change, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to build the tree
def buildTree(tree: list, a: list,
                s: int, e: int, idx: int):

    # s = starting index
    # e = ending index
    # a = array storing binary string of numbers
    # idx = starting index = 1, for recurring the tree
    if s == e:

        # store each element value at the
        # leaf node
        tree[idx] = a[s]
        return

    mid = (s + e) // 2

    # Recurring in two sub portions (left, right)
    # to build the segment tree

    # Calling for the left sub portion
    buildTree(tree, a, s, mid, 2 * idx)

    # Calling for the right sub portion
    buildTree(tree, a, mid + 1, e, 2 * idx + 1)

    # Summing up the number of one's
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1]

    return

# Function to return the index of the query
def queryTree(tree: list, s: int, e: int,
            k: int, idx: int) -> int:

    # s = starting index
    # e = ending index
    # k = searching for kth bit
    # idx = starting index = 1, for recurring the tree

    # k > number of 1's in a binary string
    if k > tree[idx]:
        return -1

    # leaf node at which kth 1 is stored
    if s == e:
        return s
    mid = (s + e) // 2

    # If left sub-tree contains more or equal 1's
    # than required kth 1
    if tree[2 * idx] >= k:
        return queryTree(tree, s, mid, k, 2 * idx)

    # If left sub-tree contains less 1's than
    # required kth 1 then recur in the right sub-tree
    else:
        return queryTree(tree, mid + 1, e,
                    k - tree[2 * idx], 2 * idx + 1)

# Function to perform the update query
def updateTree(tree: list, s: int, e: int,
                i: int, change: int, idx: int):

    # s = starting index
    # e = ending index
    # i = index at which change is to be done
    # change = new changed bit
    # idx = starting index = 1, for recurring the tree

    # Out of bounds request
    if i < s or i > e:
        print("error")
        return

    # Leaf node of the required index i
    if s == e:

        # Replacing the node value with
        # the new changed value
        tree[idx] = change
        return

    mid = (s + e) // 2

    # If the index i lies in the left sub-tree
    if i >= s and i <= mid:
        updateTree(tree, s, mid, i, change, 2 * idx)

    # If the index i lies in the right sub-tree
    else:
        updateTree(tree, mid + 1, e, i, change, 2 * idx + 1)

    # Merging both left and right sub-trees
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1]
    return

# Function to perform queries
def queries(tree: list, a: list, q: int, p: int,
            k: int, change: int, n: int):
    s = 0
    e = n - 1
    idx = 1
    if q == 1:

        # q = 1 update, p = index at which change
        # is to be done, change = new bit
        a[p] = change
        updateTree(tree, s, e, p, change, idx)
        print("Array after updation:")
        for i in range(n):
            print(a[i], end=" ")
        print()
    else:

        # q = 0, print kth bit
        print("Index of %dth set bit: %d" % (k,
                queryTree(tree, s, e, k, idx)))

# Driver Code
if __name__ == "__main__":
    a = [1, 0, 1, 0, 0, 1, 1, 1]
    n = len(a)

    # Declaring & initializing the tree with
    # maximum possible size of the segment tree
    # and each value initially as 0
    tree = [0] * (4 * n + 1)

    # s and e are the starting and ending
    # indices respectively
    s = 0
    e = n - 1
    idx = 1

    # Build the segment tree
    buildTree(tree, a, s, e, idx)

    # Find index of kth set bit
    q = 0
    p = 0
    change = 0
    k = 4
    queries(tree, a, q, p, k, change, n)

    # Update query
    q = 1
    p = 5
    change = 0
    queries(tree, a, q, p, k, change, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to build the tree
    static void buildTree(int[] tree, int[] a,
                        int s, int e, int idx)
    {

        // s = starting index
        // e = ending index
        // a = array storing binary string of numbers
        // idx = starting index = 1, for recurring the tree
        if (s == e)
        {

            // store each element value at the
            // leaf node
            tree[idx] = a[s];
            return;
        }

        int mid = (s + e) / 2;

        // Recurring in two sub portions (left, right)
        // to build the segment tree

        // Calling for the left sub portion
        buildTree(tree, a, s, mid, 2 * idx);

        // Calling for the right sub portion
        buildTree(tree, a, mid + 1, e, 2 * idx + 1);

        // Summing up the number of one's
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];

        return;
    }

    // Function to return the index of the query
    static int queryTree(int[] tree, int s,
                        int e, int k, int idx)
    {

        // s = starting index
        // e = ending index
        // k = searching for kth bit
        // idx = starting index = 1, for recurring the tree

        // k > number of 1's in a binary string
        if (k > tree[idx])
            return -1;

        // leaf node at which kth 1 is stored
        if (s == e)
            return s;
        int mid = (s + e) / 2;

        // If left sub-tree contains more or equal 1's
        // than required kth 1
        if (tree[2 * idx] >= k)
            return queryTree(tree, s, mid, k, 2 * idx);

        // If left sub-tree contains less 1's than
        // required kth 1 then recur in the right sub-tree
        else
            return queryTree(tree, mid + 1,
                            e, k - tree[2 * idx],
                            2 * idx + 1);
    }

    // Function to perform the update query
    static void updateTree(int[] tree, int s, int e,
                            int i, int change, int idx)
    {

        // s = starting index
        // e = ending index
        // i = index at which change is to be done
        // change = new changed bit
        // idx = starting index = 1, for recurring the tree

        // Out of bounds request
        if (i < s || i > e)
        {
            Console.WriteLine("Error");
            return;
        }

        // Leaf node of the required index i
        if (s == e)
        {

            // Replacing the node value with
            // the new changed value
            tree[idx] = change;
            return;
        }

        int mid = (s + e) / 2;

        // If the index i lies in the left sub-tree
        if (i >= s && i <= mid)
            updateTree(tree, s, mid, i,
                        change, 2 * idx);

        // If the index i lies in the right sub-tree
        else
            updateTree(tree, mid + 1, e, i,
                       change, 2 * idx + 1);

        // Merging both left and right sub-trees
        tree[idx] = tree[2 * idx] +
                    tree[2 * idx + 1];
        return;
    }

    // Function to perform queries
    static void queries(int[] tree, int[] a, int q, int p,
                                int k, int change, int n)
    {
        int s = 0, e = n - 1, idx = 1;
        if (q == 1)
        {

            // q = 1 update, p = index at which change
            // is to be done, change = new bit
            a[p] = change;
            updateTree(tree, s, e, p, change, idx);
            Console.WriteLine("Array after updation:");
            for (int i = 0; i < n; i++)
                Console.Write(a[i] + " ");
            Console.WriteLine();
        }
        else
        {

            // q = 0, print kth bit
            Console.Write("Index of {0}th set bit: {1}\n",
                            k, queryTree(tree, s, e, k, idx));
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 1, 0, 1, 0, 0, 1, 1, 1 };
        int n = a.Length;

        // Declaring & initializing the tree with
        // maximum possible size of the segment tree
        // and each value initially as 0
        int[] tree = new int[4 * n + 1];
        for (int i = 0; i < 4 * n + 1; ++i)
        {
            tree[i] = 0;
        }

        // s and e are the starting and ending
        // indices respectively
        int s = 0, e = n - 1, idx = 1;

        // Build the segment tree
        buildTree(tree, a, s, e, idx);

        // Find index of kth set bit
        int q = 0, p = 0, change = 0, k = 4;
        queries(tree, a, q, p, k, change, n);

        // Update query
        q = 1;
        p = 5;
        change = 0;
        queries(tree, a, q, p, k, change, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to build the tree
function buildTree(tree, a, s, e, idx)
{
    // s = starting index
    // e = ending index
    // a = array storing binary string of numbers
    // idx = starting index = 1, for recurring the tree
    if (s == e) {

        // store each element value at the
        // leaf node
        tree[idx] = a[s];
        return;
    }

    let mid = Math.floor((s + e) / 2);

    // Recurring in two sub portions (left, right)
    // to build the segment tree

    // Calling for the left sub portion
    buildTree(tree, a, s, mid, 2 * idx);

    // Calling for the right sub portion
    buildTree(tree, a, mid + 1, e, 2 * idx + 1);

    // Summing up the number of one's
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1];

    return;
}

// Function to return the index of the query
function queryTree(tree, s, e, k, idx)
{
    // s = starting index
    // e = ending index
    // k = searching for kth bit
    // idx = starting index = 1, for recurring the tree

    // k > number of 1's in a binary string
    if (k > tree[idx])
        return -1;

    // leaf node at which kth 1 is stored
    if (s == e)
        return s;
    let mid = Math.floor((s + e) / 2);

    // If left sub-tree contains more or equal 1's
    // than required kth 1
    if (tree[2 * idx] >= k)
        return queryTree(tree, s, mid, k, 2 * idx);

    // If left sub-tree contains less 1's than
    // required kth 1 then recur in the right sub-tree
    else
        return queryTree(tree, mid + 1, e, k -
        tree[2 * idx], 2 * idx + 1);
}

// Function to perform the update query
function updateTree(tree, s, e, i, change, idx)
{
    // s = starting index
    // e = ending index
    // i = index at which change is to be done
    // change = new changed bit
    // idx = starting index = 1, for recurring the tree

    // Out of bounds request
    if (i < s || i > e) {
        document.write("error");
        return;
    }

    // Leaf node of the required index i
    if (s == e) {

        // Replacing the node value with
        // the new changed value
        tree[idx] = change;
        return;
    }

    let mid = Math.floor((s + e) / 2);

    // If the index i lies in the left sub-tree
    if (i >= s && i <= mid)
        updateTree(tree, s, mid, i, change, 2 * idx);

    // If the index i lies in the right sub-tree
    else
        updateTree(tree, mid + 1, e, i, change, 2 * idx + 1);

    // Merging both left and right sub-trees
    tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
    return;
}

// Function to perform queries
function queries(tree, a, q, p, k, change, n)
{
    let s = 0, e = n - 1, idx = 1;
    if (q == 1) {
        // q = 1 update, p = index at which change
        // is to be done, change = new bit
        a[p] = change;
        updateTree(tree, s, e, p, change, idx);
        document.write("Array after updation:<br>");
        for (let i = 0; i < n; i++)
            document.write(a[i] + " ");
        document.write("<br>");
    }
    else {
        // q = 0, prlet kth bit
        document.write("Index of " + k +
        "th set bit: " + queryTree(tree, s, e, k, idx) + "<br>");
    }
}

// Driver code

    let a = [ 1, 0, 1, 0, 0, 1, 1, 1 ];
    let n = a.length;

    // Declaring & initializing the tree with
    // maximum possible size of the segment tree
    // and each value initially as 0
    let tree = new Array(4 * n + 1);
    for (let i = 0; i < 4 * n + 1; ++i) {
        tree[i] = 0;
    }

    // s and e are the starting and ending
    // indices respectively
    let s = 0, e = n - 1, idx = 1;

    // Build the segment tree
    buildTree(tree, a, s, e, idx);

    // Find index of kth set bit
    let q = 0, p = 0, change = 0, k = 4;
    queries(tree, a, q, p, k, change, n);

    // Update query
    q = 1, p = 5, change = 0;
    queries(tree, a, q, p, k, change, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Index of 4th set bit: 6
Array after updation:
1 0 1 0 0 0 1 1
```

**时间复杂度:**每个查询 O(logN)，构建段树 O(NlogN)。
**辅助空间:** O(N)