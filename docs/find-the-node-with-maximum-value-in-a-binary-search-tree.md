# 在二叉查找树中找到最大值的节点

> 原文:[https://www . geesforgeks . org/find-二进制搜索树中具有最大值的节点/](https://www.geeksforgeeks.org/find-the-node-with-maximum-value-in-a-binary-search-tree/)

给定一个二叉查找树，任务是找到 BST 中具有最大值的节点。

![](img/8ae9fabdbc84861420368ee7e052a538.png)

对于上面的树，我们从 20 开始，然后向右移动到 22。我们继续向右移动，直到看到空值。由于 22 的右边为空，因此 22 是具有最大值的节点。

**进场:**这个挺简单的。只需递归地从根到右遍历节点，直到右侧为空。右边为空的节点是值最大的节点。

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child  
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// Function to create a new node
struct node* newNode(int data)
{
    struct node* newnode = new node();
    newnode->data = data;
    newnode->left = NULL;
    newnode->right = NULL;

    return (newnode);
}

// Function to insert a new node in BST
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

// Function to find the node with maximum value
// i.e. rightmost leaf node
int maxValue(struct node* node)
{   
    /* loop down to find the rightmost leaf */
    struct node* current = node;
    while (current->right != NULL) 
        current = current->right;

    return (current->data);
}

// Driver code
int main()
{
    struct node* root = NULL;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

    cout << "Maximum value in BST is " << maxValue(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of last
// 'n' nodes of the Linked List
import java.util.*;

class GFG
{

/* A binary tree node has data, pointer to left child 
and a pointer to right child */
static class node
{
    int data;
    node left;
    node right;
};

// Function to create a new node
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Function to insert a new node in BST
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

// Function to find the node with maximum value
// i.e. rightmost leaf node
static int maxValue(node node)
{ 
    /* loop down to find the rightmost leaf */
    node current = node;
    while (current.right != null) 
        current = current.right;

    return (current.data);
}

// Driver code
public static void main(String[] args) 
{
    node root = null;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

    System.out.println("Maximum value in BST is " + maxValue(root));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
import sys
import math

# A binary tree node has data, pointer to left child 
# and a pointer to right child 
class Node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Function to insert a new node in BST
def insert(root, data):

    # 1\. If the tree is empty, return a new,     
    # single node
    if not root:
        return Node(data)

    # 2\. Otherwise, recur down the tree
    if data < root.data:
        root.left = insert(root.left, data)
    if data > root.data:
        root.right = insert(root.right, data)

    # return the (unchanged) node pointer
    return root

# Function to find the node with maximum value 
# i.e. rightmost leaf node 
def maxValue(root):
    current = root

    #loop down to find the rightmost leaf
    while(current.right):
        current = current.right
    return current.data

# Driver code 
if __name__=='__main__':
    root=None
    root = insert(root,2)
    root = insert(root,1)
    root = insert(root,3)
    root = insert(root,6)
    root = insert(root,5)
    print("Maximum value in BST is {}".format(maxValue(root)))

# This code is contributed by Vikash Kumar 37
```

## C#

```
// C# implementation to find the sum of last 
// 'n' nodes of the Linked List 
using System;

class GFG 
{ 

/* A binary tree node has data, pointer to left child 
and a pointer to right child */
public class node 
{ 
    public int data; 
    public node left; 
    public node right; 
}; 

// Function to create a new node 
static node newNode(int data) 
{ 
    node node = new node(); 
    node.data = data; 
    node.left = null; 
    node.right = null; 

    return (node); 
} 

// Function to insert a new node in BST 
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

// Function to find the node with maximum value 
// i.e. rightmost leaf node 
static int maxValue(node node) 
{ 
    /* loop down to find the rightmost leaf */
    node current = node; 
    while (current.right != null) 
        current = current.right; 

    return (current.data); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    node root = null; 
    root = insert(root, 4); 
    insert(root, 2); 
    insert(root, 1); 
    insert(root, 3); 
    insert(root, 6); 
    insert(root, 5); 

    Console.WriteLine("Maximum value in BST is " + maxValue(root)); 
} 
} 

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // javascript implementation to find the sum of last
    // 'n' nodes of the Linked List

    /*
     * A binary tree node has data, pointer to left child and a pointer to right
     * child
     */
    class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

    // Function to create a new node
     function newNode(data) {
        var node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    // Function to insert a new node in BST
     function insert( node , data) {
        /*
         * 1\. If the tree is empty, return a new, single node
         */
        if (node == null)
            return (newNode(data));
        else {
            /* 2\. Otherwise, recur down the tree */
            if (data <= node.data)
                node.left = insert(node.left, data);
            else
                node.right = insert(node.right, data);

            /* return the (unchanged) node pointer */
            return node;
        }
    }

    // Function to find the node with maximum value
    // i.e. rightmost leaf node
    function maxValue( node) {
        /* loop down to find the rightmost leaf */
        var current = node;
        while (current.right != null)
            current = current.right;

        return (current.data);
    }

    // Driver code

        var root = null;
        root = insert(root, 4);
        insert(root, 2);
        insert(root, 1);
        insert(root, 3);
        insert(root, 6);
        insert(root, 5);

        document.write("Maximum value in BST is " + maxValue(root));

// This code contributed by Rajput-Ji 
</script>
```

**Output:** 

```
Maximum value in BST is 6
```

***时间复杂度** : O(N)*
***辅助空间** : O(1)*