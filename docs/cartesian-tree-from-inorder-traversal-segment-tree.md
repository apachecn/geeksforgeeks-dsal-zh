# 笛卡尔树从有序遍历|线段树

> 原文:[https://www . geesforgeks . org/cartesian-tree-from-order-traversation-segment-tree/](https://www.geeksforgeeks.org/cartesian-tree-from-inorder-traversal-segment-tree/)

给定笛卡儿树的有序遍历，任务是从它构建整棵树。

**示例:**

```
Input: arr[] = {1, 5, 3}
Output: 1 5 3
  5
 / \
1   3

Input: arr[] = {3, 7, 4, 8}
Output: 3 7 4 8
     8
    /
   7
  / \
 3   4
```

**方法:**我们已经在这里看到了一个算法，平均花费 O(NlogN)时间，但在最坏的情况下可以到达 O(N <sup>2</sup> )。
在本文中，我们将看到如何构建 **O(Nlog(N))** 最坏情况运行时间下的笛卡尔坐标。为此，我们将使用[段树](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)来回答最大范围查询。

下面将是我们在范围{L，R}上的递归算法:

1.  使用段树上的范围-最大值查询找到该范围{L，R}中的最大值。假设‘M’是该范围内的最大索引。
2.  选择“arr[M]”作为当前节点的值，并使用该值创建一个节点。
3.  求解范围{L，M-1}和{M+1，R}。
4.  将{L，M-1}返回的节点设置为当前节点的左子节点，{M+1，R}设置为右子节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define maxLen 30

// Node of the BST
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        left = NULL;
        right = NULL;
        this->data = data;
    }
};

// Array to store segment tree
int segtree[maxLen * 4];

// Function to create segment-tree to answer
// range-max query
int buildTree(int l, int r, int i, int* arr)
{
    // Base case
    if (l == r) {
        segtree[i] = l;
        return l;
    }

    // Maximum index in left range
    int l1 = buildTree(l, (l + r) / 2,
                       2 * i + 1, arr);

    // Maximum index in right range
    int r1 = buildTree((l + r) / 2 + 1,
                       r, 2 * i + 2, arr);

    // If value at l1 > r1
    if (arr[l1] > arr[r1])
        segtree[i] = l1;

    // Else
    else
        segtree[i] = r1;

    // Returning the maximum in range
    return segtree[i];
}

// Function to answer range max query
int rangeMax(int l, int r, int rl,
             int rr, int i, int* arr)
{

    // Base cases
    if (r < rl || l > rr)
        return -1;
    if (l >= rl and r <= rr)
        return segtree[i];

    // Maximum in left range
    int l1 = rangeMax(l, (l + r) / 2, rl,
                      rr, 2 * i + 1, arr);

    // Maximum in right range
    int r1 = rangeMax((l + r) / 2 + 1, r,
                      rl, rr, 2 * i + 2, arr);

    // l1 = -1 means left range
    // was out-side required range
    if (l1 == -1)
        return r1;
    if (r1 == -1)
        return l1;

    // Returning the maximum
    // among two ranges
    if (arr[l1] > arr[r1])
        return l1;
    else
        return r1;
}

// Function to print the inorder
// traversal of the binary tree
void inorder(node* curr)
{

    // Base case
    if (curr == NULL)
        return;

    // Traversing the left sub-tree
    inorder(curr->left);

    // Printing current node
    cout << curr->data << " ";

    // Traversing the right sub-tree
    inorder(curr->right);
}

// Function to build cartesian tree
node* createCartesianTree(int l, int r, int* arr, int n)
{
    // Base case
    if (r < l)
        return NULL;

    // Maximum in the range
    int m = rangeMax(0, n - 1, l, r, 0, arr);

    // Creating current node
    node* curr = new node(arr[m]);

    // Creating left sub-tree
    curr->left = createCartesianTree(l, m - 1, arr, n);

    // Creating right sub-tree
    curr->right = createCartesianTree(m + 1, r, arr, n);

    // Returning current node
    return curr;
}

// Driver code
int main()
{
    // In-order traversal of cartesian tree
    int arr[] = { 8, 11, 21, 100, 5, 70, 55 };

    // Size of the array
    int n = sizeof(arr) / sizeof(int);

    // Building the segment tree
    buildTree(0, n - 1, 0, arr);

    // Building and printing cartesian tree
    inorder(createCartesianTree(0, n - 1, arr, n));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int maxLen = 30;

// Node of the BST
static class node
{
    int data;
    node left;
    node right;
    node(int data)
    {
        left = null;
        right = null;
        this.data = data;
    }
};

// Array to store segment tree
static int segtree[] = new int[maxLen * 4];

// Function to create segment-tree to answer
// range-max query
static int buildTree(int l, int r,
                     int i, int[] arr)
{
    // Base case
    if (l == r)
    {
        segtree[i] = l;
        return l;
    }

    // Maximum index in left range
    int l1 = buildTree(l, (l + r) / 2,
                       2 * i + 1, arr);

    // Maximum index in right range
    int r1 = buildTree((l + r) / 2 + 1,
                        r, 2 * i + 2, arr);

    // If value at l1 > r1
    if (arr[l1] > arr[r1])
        segtree[i] = l1;

    // Else
    else
        segtree[i] = r1;

    // Returning the maximum in range
    return segtree[i];
}

// Function to answer range max query
static int rangeMax(int l, int r, int rl,
                    int rr, int i, int[] arr)
{

    // Base cases
    if (r < rl || l > rr)
        return -1;
    if (l >= rl && r <= rr)
        return segtree[i];

    // Maximum in left range
    int l1 = rangeMax(l, (l + r) / 2, rl,
                      rr, 2 * i + 1, arr);

    // Maximum in right range
    int r1 = rangeMax((l + r) / 2 + 1, r,
                       rl, rr, 2 * i + 2, arr);

    // l1 = -1 means left range
    // was out-side required range
    if (l1 == -1)
        return r1;
    if (r1 == -1)
        return l1;

    // Returning the maximum
    // among two ranges
    if (arr[l1] > arr[r1])
        return l1;
    else
        return r1;
}

// Function to print the inorder
// traversal of the binary tree
static void inorder(node curr)
{

    // Base case
    if (curr == null)
        return;

    // Traversing the left sub-tree
    inorder(curr.left);

    // Printing current node
    System.out.print(curr.data + " ");

    // Traversing the right sub-tree
    inorder(curr.right);
}

// Function to build cartesian tree
static node createCartesianTree(int l, int r,
                                int[] arr, int n)
{
    // Base case
    if (r < l)
        return null;

    // Maximum in the range
    int m = rangeMax(0, n - 1, l, r, 0, arr);

    // Creating current node
    node curr = new node(arr[m]);

    // Creating left sub-tree
    curr.left = createCartesianTree(l, m - 1, arr, n);

    // Creating right sub-tree
    curr.right = createCartesianTree(m + 1, r, arr, n);

    // Returning current node
    return curr;
}

// Driver code
public static void main(String args[])
{
    // In-order traversal of cartesian tree
    int arr[] = { 8, 11, 21, 100, 5, 70, 55 };

    // Size of the array
    int n = arr.length;

    // Building the segment tree
    buildTree(0, n - 1, 0, arr);

    // Building && printing cartesian tree
    inorder(createCartesianTree(0, n - 1, arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Node of a linked list
class Node:
    def __init__(self, data = None, left = None,
                right = None ):
        self.data = data
        self.right = right
        self.left = left

maxLen = 30

# Array to store segment tree
segtree = [0]*(maxLen * 4)

# Function to create segment-tree to answer
# range-max query
def buildTree(l , r ,i , arr):

    global segtree
    global maxLen

    # Base case
    if (l == r) :

        segtree[i] = l
        return l

    # Maximum index in left range
    l1 = buildTree(l, int((l + r) / 2),
                   2 * i + 1, arr)

    # Maximum index in right range
    r1 = buildTree(int((l + r) / 2) + 1,r,
                   2 * i + 2, arr)

    # If value at l1 > r1
    if (arr[l1] > arr[r1]):
        segtree[i] = l1

    # Else
    else:
        segtree[i] = r1

    # Returning the maximum in range
    return segtree[i]

# Function to answer range max query
def rangeMax(l, r, rl, rr, i, arr):

    global segtree
    global maxLen

    # Base cases
    if (r < rl or l > rr):
        return -1
    if (l >= rl and r <= rr):
        return segtree[i]

    # Maximum in left range
    l1 = rangeMax(l, int((l + r) / 2), rl,
                            rr, 2 * i + 1, arr)

    # Maximum in right range
    r1 = rangeMax(int((l + r) / 2) + 1, r, rl,
                    rr, 2 * i + 2, arr)

    # l1 = -1 means left range
    # was out-side required range
    if (l1 == -1):
        return r1
    if (r1 == -1):
        return l1

    # Returning the maximum
    # among two ranges
    if (arr[l1] > arr[r1]):
        return l1
    else:
        return r1

# Function to print the inorder
# traversal of the binary tree
def inorder(curr):

    # Base case
    if (curr == None):
        return

    # Traversing the left sub-tree
    inorder(curr.left)

    # Printing current node
    print(curr.data, end= " ")

    # Traversing the right sub-tree
    inorder(curr.right)

# Function to build cartesian tree
def createCartesianTree(l , r , arr, n):

    # Base case
    if (r < l):
        return None

    # Maximum in the range
    m = rangeMax(0, n - 1, l, r, 0, arr)

    # Creating current node
    curr = Node(arr[m])

    # Creating left sub-tree
    curr.left = createCartesianTree(l, m - 1, arr, n)

    # Creating right sub-tree
    curr.right = createCartesianTree(m + 1, r, arr, n)

    # Returning current node
    return curr

# Driver code

# In-order traversal of cartesian tree
arr = [ 8, 11, 21, 100, 5, 70, 55 ]

# Size of the array
n = len(arr)

# Building the segment tree
buildTree(0, n - 1, 0, arr)

# Building && printing cartesian tree
inorder(createCartesianTree(0, n - 1, arr, n))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int maxLen = 30;

    // Node of the BST
    public class node
    {
        public int data;
        public node left;
        public node right;
        public node(int data)
        {
            left = null;
            right = null;
            this.data = data;
        }
    };

    // Array to store segment tree
    static int []segtree = new int[maxLen * 4];

    // Function to create segment-tree to answer
    // range-max query
    static int buildTree(int l, int r,
                         int i, int[] arr)
    {
        // Base case
        if (l == r)
        {
            segtree[i] = l;
            return l;
        }

        // Maximum index in left range
        int l1 = buildTree(l, (l + r) / 2,
                           2 * i + 1, arr);

        // Maximum index in right range
        int r1 = buildTree((l + r) / 2 + 1,
                            r, 2 * i + 2, arr);

        // If value at l1 > r1
        if (arr[l1] > arr[r1])
            segtree[i] = l1;

        // Else
        else
            segtree[i] = r1;

        // Returning the maximum in range
        return segtree[i];
    }

    // Function to answer range max query
    static int rangeMax(int l, int r, int rl,
                        int rr, int i, int[] arr)
    {

        // Base cases
        if (r < rl || l > rr)
            return -1;
        if (l >= rl && r <= rr)
            return segtree[i];

        // Maximum in left range
        int l1 = rangeMax(l, (l + r) / 2, rl,
                          rr, 2 * i + 1, arr);

        // Maximum in right range
        int r1 = rangeMax((l + r) / 2 + 1, r,
                           rl, rr, 2 * i + 2, arr);

        // l1 = -1 means left range
        // was out-side required range
        if (l1 == -1)
            return r1;
        if (r1 == -1)
            return l1;

        // Returning the maximum
        // among two ranges
        if (arr[l1] > arr[r1])
            return l1;
        else
            return r1;
    }

    // Function to print the inorder
    // traversal of the binary tree
    static void inorder(node curr)
    {

        // Base case
        if (curr == null)
            return;

        // Traversing the left sub-tree
        inorder(curr.left);

        // Printing current node
        Console.Write(curr.data + " ");

        // Traversing the right sub-tree
        inorder(curr.right);
    }

    // Function to build cartesian tree
    static node createCartesianTree(int l, int r,
                                    int[] arr, int n)
    {
        // Base case
        if (r < l)
            return null;

        // Maximum in the range
        int m = rangeMax(0, n - 1, l, r, 0, arr);

        // Creating current node
        node curr = new node(arr[m]);

        // Creating left sub-tree
        curr.left = createCartesianTree(l, m - 1,
                                         arr, n);

        // Creating right sub-tree
        curr.right = createCartesianTree(m + 1, r,
                                          arr, n);

        // Returning current node
        return curr;
    }

    // Driver code
    public static void Main()
    {
        // In-order traversal of cartesian tree
        int []arr = { 8, 11, 21, 100, 5, 70, 55 };

        // Size of the array
        int n = arr.Length;

        // Building the segment tree
        buildTree(0, n - 1, 0, arr);

        // Building && printing cartesian tree
        inorder(createCartesianTree(0, n - 1, arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxLen = 30;

// Node of the BST
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Array to store segment tree
var segtree = Array(maxLen * 4).fill(0);

// Function to create segment-tree to answer
// range-max query
function buildTree(l, r, i, arr)
{

    // Base case
    if (l == r)
    {
        segtree[i] = l;
        return l;
    }

    // Maximum index in left range
    var l1 = buildTree(l, parseInt((l + r) / 2),
                                2 * i + 1, arr);

    // Maximum index in right range
    var r1 = buildTree(parseInt((l + r) / 2) + 1,
                              r, 2 * i + 2, arr);

    // If value at l1 > r1
    if (arr[l1] > arr[r1])
        segtree[i] = l1;

    // Else
    else
        segtree[i] = r1;

    // Returning the maximum in range
    return segtree[i];
}

// Function to answer range max query
function rangeMax(l, r, rl, rr, i, arr)
{

    // Base cases
    if (r < rl || l > rr)
        return -1;
    if (l >= rl && r <= rr)
        return segtree[i];

    // Maximum in left range
    var l1 = rangeMax(l, parseInt((l + r) / 2), rl,
                               rr, 2 * i + 1, arr);

    // Maximum in right range
    var r1 = rangeMax(parseInt((l + r) / 2) + 1, r,
                        rl, rr, 2 * i + 2, arr);

    // l1 = -1 means left range
    // was out-side required range
    if (l1 == -1)
        return r1;
    if (r1 == -1)
        return l1;

    // Returning the maximum
    // among two ranges
    if (arr[l1] > arr[r1])
        return l1;
    else
        return r1;
}

// Function to print the inorder
// traversal of the binary tree
function inorder(curr)
{

    // Base case
    if (curr == null)
        return;

    // Traversing the left sub-tree
    inorder(curr.left);

    // Printing current node
    document.write(curr.data + " ");

    // Traversing the right sub-tree
    inorder(curr.right);
}

// Function to build cartesian tree
function createCartesianTree(l, r, arr, n)
{

    // Base case
    if (r < l)
        return null;

    // Maximum in the range
    var m = rangeMax(0, n - 1, l, r, 0, arr);

    // Creating current node
    var curr = new node(arr[m]);

    // Creating left sub-tree
    curr.left = createCartesianTree(l, m - 1,
                                     arr, n);

    // Creating right sub-tree
    curr.right = createCartesianTree(m + 1, r,
                                      arr, n);

    // Returning current node
    return curr;
}

// Driver code

// In-order traversal of cartesian tree
var arr = [ 8, 11, 21, 100, 5, 70, 55 ];

// Size of the array
var n = arr.length;

// Building the segment tree
buildTree(0, n - 1, 0, arr);

// Building && printing cartesian tree
inorder(createCartesianTree(0, n - 1, arr, n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
8 11 21 100 5 70 55
```

**时间复杂度:**O(N+logN)
T3】辅助空间 : O(N)。