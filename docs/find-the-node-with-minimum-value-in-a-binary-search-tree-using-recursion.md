# 使用递归找到二叉查找树中具有最小值的节点

> 原文:[https://www . geesforgeks . org/find-二进制搜索树中具有最小值的节点-使用递归/](https://www.geeksforgeeks.org/find-the-node-with-minimum-value-in-a-binary-search-tree-using-recursion/)

给定一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，任务是找到具有最小值的节点。

**示例:**

> **输入:**
> 
> ![BST_LCA](img/80a529084597eec7023083269684bcbe.png)
> 
> **输出:** 4

**方法:**只需递归地从根向左遍历节点，直到 left 为 NULL。左边为空的节点是最小值的节点。

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
int minValue(struct node* node)
{
    if (node->left == NULL)
        return node->data;
    return minValue(node->left);
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

    cout << minValue(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach

class GFG
{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int data;
    Node left;
    Node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static Node newNode(int data)
{
    Node node = new Node();
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
static Node insert(Node node, int data)
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
static int minValue(Node node)
{
    if (node.left == null)
        return node.data;
    return minValue(node.left);
}

// Driver code
public static void main(String args[])
{
    // Create the BST
    Node root = null;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

    System.out.println(minValue(root));

}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Implementation of
# the above approach
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates 
# a new node with the given data
# and null left and right pointers.
def insert(node, data):
    if node is None :
        return Node(data)
    else:
        if data <= node.data:
            node.left = insert(node.left, data)
        else:
            node.right = insert(node.right, data)

        return node

# Function to return the minimum node
# in the given binary search tree
def minValue(node):
    if node.left == None:
        return node.data
    return minValue(node.left)

# Driver code
if __name__ == "__main__" :

    # Create the BST
    root = None
    root = insert(root, 4)
    insert(root, 2)
    insert(root, 1)
    insert(root, 3)
    insert(root, 6)
    insert(root, 5)

    print(minValue(root))

# This code is contributed by vinayak
```

## C#

```
// C# Implementation of the above approach
using System;

class GFG
{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static Node newNode(int data)
{
    Node node = new Node();
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
static Node insert(Node node, int data)
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
static int minValue(Node node)
{
    if (node.left == null)
        return node.data;
    return minValue(node.left);
}

// Driver code
public static void Main(String []args)
{
    // Create the BST
    Node root = null;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

    Console.WriteLine(minValue(root));

}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// A binary tree node has data, pointer to
// left child and a pointer to right child
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Helper function that allocates a new node
// with the given data and null left and right
// pointers.
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Give a binary search tree and a number,
// inserts a new node with the given number in
// the correct place in the tree. Returns the new
// root pointer which the caller should then use
// (the standard trick to avoid using reference
// parameters).
function insert(node, data)
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
function minValue(node)
{
    if (node.left == null)
        return node.data;

    return minValue(node.left);
}

// Driver code

// Create the BST
var root = null;
root = insert(root, 4);
insert(root, 2);
insert(root, 1);
insert(root, 3);
insert(root, 6);
insert(root, 5);

document.write(minValue(root));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n)，最差情况发生在左斜树。