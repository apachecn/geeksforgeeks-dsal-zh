# 使用递归找到二叉查找树中具有最大值的节点

> 原文:[https://www . geesforgeks . org/find-二进制搜索树中具有最大值的节点-使用递归/](https://www.geeksforgeeks.org/find-the-node-with-maximum-value-in-a-binary-search-tree-using-recursion/)

给定一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，任务是找到具有最大值的节点。

**示例:**

> **输入:**
> 
> ![BST_LCA](img/80a529084597eec7023083269684bcbe.png)
> 
> **输出:** 22

**方法:**只需递归地从根到右遍历节点，直到 right 为 NULL。右边为空的节点是值最大的节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node
with the given data and NULL left and right
pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)
        malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

/* Give a binary search tree and a number,
inserts a new node with the given number in
the correct place in the tree. Returns the new
root pointer which the caller should then use
(the standard trick to avoid using reference
parameters). */
struct node* insert(struct node* node, int data)
{

    /* 1\. If the tree is empty, return a new,
    single node */
    if (node == NULL)
        return (newNode(data));
    else {

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data)
            node->left = insert(node->left, data);
        else
            node->right = insert(node->right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to return the minimum node
// in the given binary search tree
int maxValue(struct node* node)
{
    if (node->right == NULL)
        return node->data;
    return maxValue(node->right);
}

// Driver code
int main()
{

    // Create the BST
    struct node* root = NULL;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

    cout << maxValue(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

/* A binary tree node has data,
   pointer to left child and a
   pointer to right child */
static class node
{
    int data;
    node left;
    node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Give a binary search tree and a number,
inserts a new node with the given number in
the correct place in the tree. Returns the new
root pointer which the caller should then use
(the standard trick to avoid using reference
parameters). */
static node insert(node node, int data)
{

    /* 1\. If the tree is empty, return a new,
    single node */
    if (node == null)
        return (newNode(data));
    else
    {

        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
            node.left = insert(node.left, data);
        else
            node.right = insert(node.right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to return the minimum node
// in the given binary search tree
static int maxValue(node node)
{
    if (node.right == null)
        return node.data;
    return maxValue(node.right);
}

// Driver code
public static void main(String args[])
{

    // Create the BST
    node root = null;
    root = insert(root, 4);
    root = insert(root, 2);
    root = insert(root, 1);
    root = insert(root, 3);
    root = insert(root, 6);
    root = insert(root, 5);

    System.out.println(maxValue(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# A binary tree node has data,
# pointer to left child and
# a pointer to right child
# Linked list node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates
# a new node with the given data
# and None left and right pointers.
def newNode(data):
    node = Node(0)
    node.data = data
    node.left = None
    node.right = None

    return (node)

# Give a binary search tree and a number,
# inserts a new node with the given number in
# the correct place in the tree. Returns the new
# root pointer which the caller should then use
# (the standard trick to avoid using reference
# parameters).
def insert(node,data):

    # 1\. If the tree is empty, 
    # return a new, single node
    if (node == None):
        return (newNode(data))
    else :

        # 2\. Otherwise, recur down the tree
        if (data <= node.data):
            node.left = insert(node.left, data)
        else:
            node.right = insert(node.right, data)

        # return the (unchanged) node pointer */
        return node

# Function to return the minimum node
# in the given binary search tree
def maxValue(node):

    if (node.right == None):
        return node.data
    return maxValue(node.right)

# Driver Code
if __name__=='__main__':

    # Create the BST
    root = None
    root = insert(root, 4)
    root = insert(root, 2)
    root = insert(root, 1)
    root = insert(root, 3)
    root = insert(root, 6)
    root = insert(root, 5)

    print (maxValue(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
public class node
{
    public int data;
    public node left;
    public node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Give a binary search tree and a number,
inserts a new node with the given number in
the correct place in the tree. Returns the new
root pointer which the caller should then use
(the standard trick to avoid using reference
parameters). */
static node insert(node node, int data)
{

    /* 1\. If the tree is empty, return a new,
    single node */
    if (node == null)
        return (newNode(data));
    else
    {

        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
            node.left = insert(node.left, data);
        else
            node.right = insert(node.right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to return the minimum node
// in the given binary search tree
static int maxValue(node node)
{
    if (node.right == null)
        return node.data;
    return maxValue(node.right);
}

// Driver code
public static void Main(String []args)
{

    // Create the BST
    node root = null;
    root = insert(root, 4);
    root = insert(root, 2);
    root = insert(root, 1);
    root = insert(root, 3);
    root = insert(root, 6);
    root = insert(root, 5);

    Console.WriteLine(maxValue(root));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
class node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
function newNode(data)
{
    let Node = new node(data);
    return (Node);
}

/* Give a binary search tree and a number,
inserts a new node with the given number in
the correct place in the tree. Returns the new
root pointer which the caller should then use
(the standard trick to avoid using reference
parameters). */
function insert(Node, data)
{

    /* 1\. If the tree is empty, return a new,
    single node */
    if (Node == null)
        return (newNode(data));
    else
    {

        /* 2\. Otherwise, recur down the tree */
        if (data <= Node.data)
            Node.left = insert(Node.left, data);
        else
            Node.right = insert(Node.right, data);

        /* Return the (unchanged) node pointer */
        return Node;
    }
}

// Function to return the minimum node
// in the given binary search tree
function maxValue(Node)
{
    if (Node.right == null)
        return Node.data;

    return maxValue(Node.right);
}

// Driver code

// Create the BST
let root = null;
root = insert(root, 4);
root = insert(root, 2);
root = insert(root, 1);
root = insert(root, 3);
root = insert(root, 6);
root = insert(root, 5);

document.write(maxValue(root));

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(n)，右偏斜树出现最坏情况。