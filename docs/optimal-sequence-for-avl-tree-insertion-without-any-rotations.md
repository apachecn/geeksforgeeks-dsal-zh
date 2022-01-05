# AVL 树插入的最佳顺序(无任何旋转)

> 原文:[https://www . geeksforgeeks . org/最优序列 for-AVL-tree-insert-not-any-rotations/](https://www.geeksforgeeks.org/optimal-sequence-for-avl-tree-insertion-without-any-rotations/)

给定一个整数数组，任务是找到将这些整数添加到 AVL 树中的顺序，这样就不需要旋转来平衡树。
**例:**

```
Input : array = {1, 2, 3}
Output : 2 1 3

Input : array = {2, 4, 1, 3, 5, 6, 7}
Output : 4 2 6 1 3 5 7
```

**进场:**

*   给定整数数组排序。
*   按照这里描述的方法，从排序的数组中创建 AVL 树。
*   现在，找到树的层次顺序遍历，这是所需的序列。
*   在上一步找到的序列中添加数字将始终保持树中所有节点的高度平衡属性。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

/* A Binary Tree node */
struct TNode {
    int data;
    struct TNode* left;
    struct TNode* right;
};

struct TNode* newNode(int data);

/* Function to construct AVL tree
   from a sorted array */
struct TNode* sortedArrayToBST(vector<int> arr, int start, int end)
{
    /* Base Case */
    if (start > end)
        return NULL;

    /* Get the middle element
       and make it root */
    int mid = (start + end) / 2;
    struct TNode* root = newNode(arr[mid]);

    /* Recursively construct the
       left subtree and make it
       left child of root */
    root->left = sortedArrayToBST(arr, start, mid - 1);

    /* Recursively construct the
       right subtree and make it
       right child of root */
    root->right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

/* Helper function that allocates
   a new node with the given data
   and NULL to the left and
   the right pointers. */
struct TNode* newNode(int data)
{
    struct TNode* node = new TNode();
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

// This function is used for testing purpose
void printLevelOrder(TNode *root)
{
    if (root == NULL)  return;

    queue<TNode *> q;
    q.push(root);

    while (q.empty() == false)
    {
        TNode *node = q.front();
        cout << node->data << " ";
        q.pop();
        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);
    }
}  

/* Driver program to
test above functions */
int main()
{

    // Assuming the array is sorted
    vector<int> arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.size();

    /* Convert List to AVL tree */
    struct TNode* root = sortedArrayToBST(arr, 0, n - 1);
    printLevelOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java implementation of the approach
import java.util.*;
class solution
{

/* A Binary Tree node */
 static  class TNode {
    int data;
     TNode left;
     TNode right;
}

/* Function to con AVL tree
   from a sorted array */
 static TNode sortedArrayToBST(int arr[], int start, int end)
{
    /* Base Case */
    if (start > end)
        return null;

    /* Get the middle element
       and make it root */
    int mid = (start + end) / 2;
     TNode root = newNode(arr[mid]);

    /* Recursively construct the
       left subtree and make it
       left child of root */
    root.left = sortedArrayToBST(arr, start, mid - 1);

    /* Recursively construct the
       right subtree and make it
       right child of root */
    root.right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

/* Helper function that allocates
   a new node with the given data
   and null to the left and
   the right pointers. */
static  TNode newNode(int data)
{
     TNode node = new TNode();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// This function is used for testing purpose
static void printLevelOrder(TNode root)
{
    if (root == null)  return;

    Queue<TNode > q= new LinkedList<TNode>();
    q.add(root);

    while (q.size()>0)
    {
        TNode node = q.element();
        System.out.print( node.data + " ");
        q.remove();
        if (node.left != null)
            q.add(node.left);
        if (node.right != null)
            q.add(node.right);
    }
}  

/* Driver program to
test above functions */
public static void main(String args[])
{

    // Assuming the array is sorted
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;

    /* Convert List to AVL tree */
     TNode root = sortedArrayToBST(arr, 0, n - 1);
    printLevelOrder(root);

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 code to print order of
# insertion into AVL tree to
# ensure no rotations

# Tree Node
class Node:
    def __init__(self, d):
        self.data = d
        self.left = None
        self.right = None

# Function to convert sorted array
# to a balanced AVL Tree/BST
# Input : sorted array of integers
# Output: root node of balanced AVL Tree/BST
def sortedArrayToBST(arr):

    if not arr:
        return None

    # Find middle and get its floor value
    mid = int((len(arr)) / 2)
    root = Node(arr[mid])

    # Recursively construct the left
    # and right subtree
    root.left = sortedArrayToBST(arr[:mid])
    root.right = sortedArrayToBST(arr[mid + 1:])

    # Return the root of the
    # constructed tree
    return root

# A utility function to print the
# Level Order Traversal of AVL Tree
# using a Queue
def printLevelOrder(root):
    if not root:
        return

    q = []
    q.append(root)

    # Keep printing the top element and
    # adding to queue while it is not empty
    while q != []:
        node = q.pop(0)
        print(node.data, end=" ")

        # If left node exists, enqueue it
        if node.left:
            q.append(node.left)

        # If right node exists, enqueue it
        if node.right:
            q.append(node.right)

# Driver Code
arr = [1, 2, 3, 4, 5, 6, 7]
root = sortedArrayToBST(arr)
printLevelOrder(root)

# This code is contributed
# by Adikar Bharath
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

/* A Binary Tree node */
public class TNode
{
    public int data;
    public TNode left;
    public TNode right;
}

/* Function to con AVL tree
from a sorted array */
static TNode sortedArrayToBST(int []arr,
                    int start, int end)
{
    /* Base Case */
    if (start > end)
        return null;

    /* Get the middle element
    and make it root */
    int mid = (start + end) / 2;
    TNode root = newNode(arr[mid]);

    /* Recursively construct the
    left subtree and make it
    left child of root */
    root.left = sortedArrayToBST(arr, start, mid - 1);

    /* Recursively construct  the
    right subtree and make it
    right child of root */
    root.right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

/* Helper function that allocates
a new node with the given data
and null to the left and
the right pointers. */
static TNode newNode(int data)
{
    TNode node = new TNode();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// This function is used for testing purpose
static void printLevelOrder(TNode root)
{
    if (root == null) return;

    Queue<TNode > q = new Queue<TNode>();
    q.Enqueue(root);

    while (q.Count > 0)
    {
        TNode node = q.Peek();
        Console.Write( node.data + " ");
        q.Dequeue();
        if (node.left != null)
            q.Enqueue(node.left);
        if (node.right != null)
            q.Enqueue(node.right);
    }
}

/* Driver code */
public static void Main()
{

    // Assuming the array is sorted
    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;

    /* Convert List to AVL tree */
    TNode root = sortedArrayToBST(arr, 0, n - 1);
    printLevelOrder(root);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

/* A Binary Tree node */
class TNode
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

/* Function to con AVL tree
from a sorted array */
function sortedArrayToBST(arr, start, end)
{
    /* Base Case */
    if (start > end)
        return null;

    /* Get the middle element
    and make it root */
    var mid = parseInt((start + end) / 2);
    var root = newNode(arr[mid]);

    /* Recursively construct the
    left subtree and make it
    left child of root */
    root.left = sortedArrayToBST(arr, start, mid - 1);

    /* Recursively construct the
    right subtree and make it
    right child of root */
    root.right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

/* Helper function that allocates
a new node with the given data
and null to the left and
the right pointers. */
function newNode(data)
{
    var node = new TNode();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// This function is used for testing purpose
function printLevelOrder(root)
{
    if (root == null) return;

    var q = [];
    q.push(root);

    while (q.length > 0)
    {
        var node = q[0];
        document.write( node.data + " ");
        q.shift();
        if (node.left != null)
            q.push(node.left);
        if (node.right != null)
            q.push(node.right);
    }
}

/* Driver code */
// Assuming the array is sorted
var arr = [1, 2, 3, 4, 5, 6, 7];
var n = arr.length;

/* Convert List to AVL tree */
var root = sortedArrayToBST(arr, 0, n - 1);
printLevelOrder(root);

// This code is contributed by itsok.

</script>
```

**Output:** 

```
4 2 6 1 3 5 7
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)