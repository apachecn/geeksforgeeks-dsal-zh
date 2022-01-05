# 翻转符号问题|惰性传播段树

> 原文:[https://www . geesforgeks . org/fling-sign-problem-lazy-propagation-segment-tree/](https://www.geeksforgeeks.org/flipping-sign-problem-lazy-propagation-segment-tree/)

给定大小为 **N** 的数组。可以有以下类型的多个查询。

1.  **更新(l，r)** :更新时，翻转(将 a[i]乘以-1)a[i]的值，其中 l < = i < = r。简单来说，更改给定范围内 a[I]的符号。
2.  **查询(l，r)** :查询时，打印给定范围(包括 l 和 r)内数组的和。

**例:**

> **输入:** arr[] = { 1，2，3，4，5 }
> 更新(0，2)
> 查询(0，4)
> T5】输出: 3
> 应用更新操作后数组变为{ -1，-2，-3，4，5 }。
> 所以和为 3
> **输入:** arr[] = { 1，2，3，4，5 }
> 更新(0，4)
> 查询(0，4)
> **输出:** -15
> 应用更新操作后数组变成{ -1，-2，-3，-4，-5 }。
> 所以总和是-15

**先决条件:**

1.  [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
2.  [段树中的懒惰繁殖](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)

**方法:**
创建一个段树，其中每个节点存储其左右子节点的和，除非它是存储数组的叶节点。
对于**更新**操作:
创建一个名为 lazy 的树，大小与上面的段树相同，其中树存储其子树和 lazy 存储的总和，无论它们是否被要求翻转。如果某个范围的 lazy 设置为 1，则该范围下的所有值都需要翻转。对于更新，使用以下操作–

*   如果当前段树的 lazy 设置为 1，那么通过改变符号来更新当前段树节点，因为值需要翻转，同时翻转其子节点的 lazy 值，并将其自身的 lazy 重置为 0。
*   如果当前节点的范围完全位于更新查询范围内，则通过更改其符号来更新当前节点，如果不是叶节点，还会翻转其子节点的 lazy 值。
*   如果当前节点的范围与更新范围重叠，则对其子节点进行递归，并使用其子节点的总和更新当前节点。

对于**查询**操作:
如果 lazy 设置为 1，那么改变当前节点的符号，将当前节点 lazy 重置为 0，如果不是叶节点，也翻转其子节点 lazy 的值。然后像在段树中一样进行简单的查询。
以下是上述办法的实施:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 15

int tree[MAX] = { 0 };
int lazy[MAX] = { 0 };

// Function to build the segment tree
void build(int arr[],int node, int a, int b)
{
    if (a == b) {
        tree[node] = arr[a];
        return;
    }

    // left child
    build(arr,2 * node, a, (a + b) / 2);

    // right child
    build(arr,2 * node + 1, 1 + (a + b) / 2, b);

    tree[node] = tree[node * 2] +
                         tree[node * 2 + 1];
}

void update_tree(int node, int a,
                int b, int i, int j)
{

    // If lazy of node is 1 then
    // value in current node
    // needs to be flipped
    if (lazy[node] != 0) {

        // Update it
        tree[node] = tree[node] * (-1);

        if (a != b) {

            // flip value in lazy
            lazy[node * 2] =
                        !(lazy[node * 2]);

             // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        // Reset the node lazy value
        lazy[node] = 0;
    }

    // Current segment is not
    // within range [i, j]
    if (a > b || a > j || b < i)
        return;

    // Segment is fully
    // within range
    if (a >= i && b <= j) {
        tree[node] = tree[node] * (-1);

        // Not leaf node
        if (a != b) {

            // Flip the value as if lazy is
            // 1 and again asked to flip
            // value then without flipping
            // value two times
            lazy[node * 2] =
                         !(lazy[node * 2]);
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        return;
    }

    // Updating left child
    update_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Updating right child
    update_tree(1 + node * 2, 1 +
                     (a + b) / 2, b, i, j);

    // Updating root with
    // sum of its child
    tree[node] = tree[node * 2] +
                     tree[node * 2 + 1];
}

int query_tree(int node, int a,
                      int b, int i, int j)
{
    // Out of range
    if (a > b || a > j || b < i)
        return 0;

    // If lazy of node is 1 then value
    // in current node needs to be flipped
    if (lazy[node] != 0) {

        tree[node] = tree[node] * (-1);
        if (a != b) {
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        lazy[node] = 0;
    }

    // Current segment is totally
    // within range [i, j]
    if (a >= i && b <= j)
        return tree[node];

    // Query left child
    int q1 = query_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Query right child
    int q2 = query_tree(1 + node * 2,
                 1 + (a + b) / 2, b, i, j);

    // Return final result
    return q1 + q2;
}

int main()
{

    int arr[]={1,2,3,4,5};

    int n=sizeof(arr)/sizeof(arr[0]);

    // Building segment tree
    build(arr,1, 0, n - 1);

    // Array is { 1, 2, 3, 4, 5 }
    cout << query_tree(1, 0, n - 1, 0, 4) << endl;

    // Flip range 0 to 4
    update_tree(1, 0, n - 1, 0, 4);

    // Array becomes { -1, -2, -3, -4, -5 }
    cout << query_tree(1, 0, n - 1, 0, 4) << endl;

    // Flip range 0 t0 2
    update_tree(1, 0, n - 1, 0, 2);

    // Array becomes { 1, 2, 3, -4, -5 }
    cout << query_tree(1, 0, n - 1, 0, 4) << endl;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static final int MAX = 15;

static int tree[] = new int[MAX];
static boolean lazy[] = new boolean[MAX];

// Function to build the segment tree
static void build(int arr[],int node, int a, int b)
{
    if (a == b)
    {
        tree[node] = arr[a];
        return;
    }

    // left child
    build(arr,2 * node, a, (a + b) / 2);

    // right child
    build(arr,2 * node + 1, 1 + (a + b) / 2, b);

    tree[node] = tree[node * 2] +
                        tree[node * 2 + 1];
}

static void update_tree(int node, int a,
                int b, int i, int j)
{

    // If lazy of node is 1 then
    // value in current node
    // needs to be flipped
    if (lazy[node] != false)
    {

        // Update it
        tree[node] = tree[node] * (-1);

        if (a != b)
        {

            // flip value in lazy
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        // Reset the node lazy value
        lazy[node] = false;
    }

    // Current segment is not
    // within range [i, j]
    if (a > b || a > j || b < i)
        return;

    // Segment is fully
    // within range
    if (a >= i && b <= j)
    {
        tree[node] = tree[node] * (-1);

        // Not leaf node
        if (a != b)
        {

            // Flip the value as if lazy is
            // 1 and again asked to flip
            // value then without flipping
            // value two times
            lazy[node * 2] =
                        !(lazy[node * 2]);
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        return;
    }

    // Updating left child
    update_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Updating right child
    update_tree(1 + node * 2, 1 +
                    (a + b) / 2, b, i, j);

    // Updating root with
    // sum of its child
    tree[node] = tree[node * 2] +
                    tree[node * 2 + 1];
}

static int query_tree(int node, int a,
                    int b, int i, int j)
{
    // Out of range
    if (a > b || a > j || b < i)
        return 0;

    // If lazy of node is 1 then value
    // in current node needs to be flipped
    if (lazy[node] != false)
    {

        tree[node] = tree[node] * (-1);
        if (a != b)
        {
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        lazy[node] = false;
    }

    // Current segment is totally
    // within range [i, j]
    if (a >= i && b <= j)
        return tree[node];

    // Query left child
    int q1 = query_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Query right child
    int q2 = query_tree(1 + node * 2,
                1 + (a + b) / 2, b, i, j);

    // Return final result
    return q1 + q2;
}

// Driver code
public static void main(String[] args)
{

    int arr[]={1, 2, 3, 4, 5};

    int n=arr.length;

    // Building segment tree
    build(arr,1, 0, n - 1);

    // Array is { 1, 2, 3, 4, 5 }
    System.out.print(query_tree(1, 0, n - 1, 0, 4) +"\n");

    // Flip range 0 to 4
    update_tree(1, 0, n - 1, 0, 4);

    // Array becomes { -1, -2, -3, -4, -5 }
    System.out.print(query_tree(1, 0, n - 1, 0, 4) +"\n");

    // Flip range 0 t0 2
    update_tree(1, 0, n - 1, 0, 2);

    // Array becomes { 1, 2, 3, -4, -5 }
    System.out.print(query_tree(1, 0, n - 1, 0, 4) +"\n");
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 15

tree = [0]*MAX
lazy = [0]*MAX

# Function to build the segment tree
def build(arr,node, a, b):
    if (a == b):
        tree[node] = arr[a]
        return

    # left child
    build(arr,2 * node, a, (a + b) // 2)

    # right child
    build(arr,2 * node + 1, 1 + (a + b) // 2, b)

    tree[node] = tree[node * 2] +tree[node * 2 + 1]

def update_tree(node, a,b, i, j):

    # If lazy of node is 1 then
    # value in current node
    # needs to be flipped
    if (lazy[node] != 0):

        # Update it
        tree[node] = tree[node] * (-1)

        if (a != b):

            # flip value in lazy
            lazy[node * 2] =not (lazy[node * 2])

            # flip value in lazy
            lazy[node * 2 + 1] =not (lazy[node * 2 + 1])

        # Reset the node lazy value
        lazy[node] = 0

    # Current segment is not
    # within range [i, j]
    if (a > b or a > j or b < i):
        return

    # Segment is fully
    # within range
    if (a >= i and b <= j):
        tree[node] = tree[node] * (-1)

        # Not leaf node
        if (a != b):

            # Flip the value as if lazy is
            # 1 and again asked to flip
            # value then without flipping
            # value two times
            lazy[node * 2] = not (lazy[node * 2])
            lazy[node * 2 + 1] = not (lazy[node * 2 + 1])

        return

    # Updating left child
    update_tree(node * 2, a,(a + b) // 2, i, j)

    # Updating right child
    update_tree(1 + node * 2, 1 +(a + b) // 2, b, i, j)

    # Updating root with
    # sum of its child
    tree[node] = tree[node * 2] +tree[node * 2 + 1]

def query_tree(node, a,b, i, j):
    # Out of range
    if (a > b or a > j or b < i):
        return 0

    # If lazy of node is 1 then value
    # in current node needs to be flipped
    if (lazy[node] != 0):

        tree[node] = tree[node] * (-1)
        if (a != b):
            lazy[node * 2] =not (lazy[node * 2])

            # flip value in lazy
            lazy[node * 2 + 1] = not (lazy[node * 2 + 1])

        lazy[node] = 0

    # Current segment is totally
    # within range [i, j]
    if (a >= i and b <= j):
        return tree[node]

    # Query left child
    q1 = query_tree(node * 2, a,(a + b) // 2, i, j)

    # Query right child
    q2 = query_tree(1 + node * 2,1 + (a + b) // 2, b, i, j)

    # Return final result
    return q1 + q2

# Driver code
if __name__ == '__main__':

    arr=[1,2,3,4,5]

    n=len(arr)

    # Building segment tree
    build(arr,1, 0, n - 1)

    # Array is { 1, 2, 3, 4, 5
    print(query_tree(1, 0, n - 1, 0, 4))

    # Flip range 0 to 4
    update_tree(1, 0, n - 1, 0, 4)

    # Array becomes { -1, -2, -3, -4, -5
    print(query_tree(1, 0, n - 1, 0, 4))

    # Flip range 0 t0 2
    update_tree(1, 0, n - 1, 0, 2)

    # Array becomes { 1, 2, 3, -4, -5
    print(query_tree(1, 0, n - 1, 0, 4))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static readonly int MAX = 15;

static int []tree = new int[MAX];
static bool []lazy = new bool[MAX];

// Function to build the segment tree
static void build(int []arr,int node, int a, int b)
{
    if (a == b)
    {
        tree[node] = arr[a];
        return;
    }

    // left child
    build(arr, 2 * node, a, (a + b) / 2);

    // right child
    build(arr, 2 * node + 1, 1 + (a + b) / 2, b);

    tree[node] = tree[node * 2] +
                        tree[node * 2 + 1];
}

static void update_tree(int node, int a,
                int b, int i, int j)
{

    // If lazy of node is 1 then
    // value in current node
    // needs to be flipped
    if (lazy[node] != false)
    {

        // Update it
        tree[node] = tree[node] * (-1);

        if (a != b)
        {

            // flip value in lazy
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        // Reset the node lazy value
        lazy[node] = false;
    }

    // Current segment is not
    // within range [i, j]
    if (a > b || a > j || b < i)
        return;

    // Segment is fully
    // within range
    if (a >= i && b <= j)
    {
        tree[node] = tree[node] * (-1);

        // Not leaf node
        if (a != b)
        {

            // Flip the value as if lazy is
            // 1 and again asked to flip
            // value then without flipping
            // value two times
            lazy[node * 2] =
                        !(lazy[node * 2]);
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        return;
    }

    // Updating left child
    update_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Updating right child
    update_tree(1 + node * 2, 1 +
                    (a + b) / 2, b, i, j);

    // Updating root with
    // sum of its child
    tree[node] = tree[node * 2] +
                    tree[node * 2 + 1];
}

static int query_tree(int node, int a,
                    int b, int i, int j)
{
    // Out of range
    if (a > b || a > j || b < i)
        return 0;

    // If lazy of node is 1 then value
    // in current node needs to be flipped
    if (lazy[node] != false)
    {
        tree[node] = tree[node] * (-1);
        if (a != b)
        {
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        lazy[node] = false;
    }

    // Current segment is totally
    // within range [i, j]
    if (a >= i && b <= j)
        return tree[node];

    // Query left child
    int q1 = query_tree(node * 2, a,
                        (a + b) / 2, i, j);

    // Query right child
    int q2 = query_tree(1 + node * 2,
                1 + (a + b) / 2, b, i, j);

    // Return readonly result
    return q1 + q2;
}

// Driver code
public static void Main(String[] args)
{

    int []arr = {1, 2, 3, 4, 5};

    int n = arr.Length;

    // Building segment tree
    build(arr, 1, 0, n - 1);

    // Array is { 1, 2, 3, 4, 5 }
    Console.Write(query_tree(1, 0, n - 1, 0, 4) +"\n");

    // Flip range 0 to 4
    update_tree(1, 0, n - 1, 0, 4);

    // Array becomes { -1, -2, -3, -4, -5 }
    Console.Write(query_tree(1, 0, n - 1, 0, 4) +"\n");

    // Flip range 0 t0 2
    update_tree(1, 0, n - 1, 0, 2);

    // Array becomes { 1, 2, 3, -4, -5 }
    Console.Write(query_tree(1, 0, n - 1, 0, 4) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let MAX = 15;

let tree = new Array(MAX).fill(0);
let lazy = new Array(MAX).fill(0);

// Function to build the segment tree
function build(arr,node, a, b)
{
    if (a == b) {
        tree[node] = arr[a];
        return;
    }

    // left child
    build(arr,2 * node, a, Math.floor((a + b) / 2));

    // right child
    build(arr,2 * node + 1, 1 + Math.floor((a + b) / 2), b);

    tree[node] = tree[node * 2] +
                        tree[node * 2 + 1];
}

function update_tree(node, a, b, i, j)
{

    // If lazy of node is 1 then
    // value in current node
    // needs to be flipped
    if (lazy[node] != 0) {

        // Update it
        tree[node] = tree[node] * (-1);

        if (a != b) {

            // flip value in lazy
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        // Reset the node lazy value
        lazy[node] = 0;
    }

    // Current segment is not
    // within range [i, j]
    if (a > b || a > j || b < i)
        return;

    // Segment is fully
    // within range
    if (a >= i && b <= j) {
        tree[node] = tree[node] * (-1);

        // Not leaf node
        if (a != b) {

            // Flip the value as if lazy is
            // 1 and again asked to flip
            // value then without flipping
            // value two times
            lazy[node * 2] =
                        !(lazy[node * 2]);
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        return;
    }

    // Updating left child
    update_tree(node * 2, a,
                        Math.floor((a + b) / 2), i, j);

    // Updating right child
    update_tree(1 + node * 2, 1 +
                    Math.floor((a + b) / 2), b, i, j);

    // Updating root with
    // sum of its child
    tree[node] = tree[node * 2] +
                    tree[node * 2 + 1];
}

function query_tree(node, a, b, i, j)
{
    // Out of range
    if (a > b || a > j || b < i)
        return 0;

    // If lazy of node is 1 then value
    // in current node needs to be flipped
    if (lazy[node] != 0) {

        tree[node] = tree[node] * (-1);
        if (a != b) {
            lazy[node * 2] =
                        !(lazy[node * 2]);

            // flip value in lazy
            lazy[node * 2 + 1] =
                    !(lazy[node * 2 + 1]);
        }

        lazy[node] = 0;
    }

    // Current segment is totally
    // within range [i, j]
    if (a >= i && b <= j)
        return tree[node];

    // Query left child
    let q1 = query_tree(node * 2, a,
                        Math.floor((a + b) / 2), i, j);

    // Query right child
    let q2 = query_tree(1 + node * 2,
                1 + Math.floor((a + b) / 2), b, i, j);

    // Return final result
    return q1 + q2;
}

    let arr = [ 1,2,3,4,5];

    let n = arr.length;

    // Building segment tree
    build(arr,1, 0, n - 1);

    // Array is { 1, 2, 3, 4, 5 }
    document.write(query_tree(1, 0, n - 1, 0, 4) + "<br>");

    // Flip range 0 to 4
    update_tree(1, 0, n - 1, 0, 4);

    // Array becomes { -1, -2, -3, -4, -5 }
    document.write(query_tree(1, 0, n - 1, 0, 4) + "<br>");

    // Flip range 0 t0 2
    update_tree(1, 0, n - 1, 0, 2);

    // Array becomes { 1, 2, 3, -4, -5 }
    document.write(query_tree(1, 0, n - 1, 0, 4) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
15
-15
-3
```

**时间复杂度:** O(log(N))