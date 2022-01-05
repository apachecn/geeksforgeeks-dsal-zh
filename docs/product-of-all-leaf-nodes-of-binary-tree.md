# 二叉树所有叶节点的乘积

> 原文:[https://www . geesforgeks . org/二叉树全叶节点积/](https://www.geeksforgeeks.org/product-of-all-leaf-nodes-of-binary-tree/)

给定一棵二叉树，求所有叶节点的乘积。
示例:

```
Input : 
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
          \
           8
Output :
product = 4 * 5 * 8 * 7 = 1120
```

其思想是以任何方式遍历树，并检查该节点是否是叶节点。如果节点是叶节点，将节点数据乘以一个变量 *prod* ，用于存储叶节点的乘积。
以下是上述办法的实施情况。

## C++

```
// CPP program to find product of
// all leaf nodes of binary tree
#include <bits/stdc++.h>
using namespace std;

// struct binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// return new node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// utility function which calculates
// product of all leaf nodes
void leafProduct(Node* root, int& prod)
{
    if (!root)
        return;

    // product root data to prod if
    // root is a leaf node
    if (!root->left && !root->right)
        prod *= root->data;

    // propagate recursively in left
    // and right subtree
    leafProduct(root->left, prod);
    leafProduct(root->right, prod);
}

// Driver program
int main()
{

    // construct binary tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right = newNode(3);
    root->right->right = newNode(7);
    root->right->left = newNode(6);
    root->right->left->right = newNode(8);

    // variable to store product of leaf nodes
    int prod = 1;
    leafProduct(root, prod);
    cout << prod << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of
// all leaf nodes of binary tree
class GFG
{

// struct binary tree node
static class Node
{
    int data;
    Node left, right;
};

// return new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// product
static int prod = 1;

// utility function which calculates
// product of all leaf nodes
static void leafProduct(Node root )
{
    if (root == null)
        return;

    // product root data to prod if
    // root is a leaf node
    if (root.left == null && root.right == null)
        prod *= root.data;

    // propagate recursively in left
    // and right subtree
    leafProduct(root.left);
    leafProduct(root.right);
}

// Driver program
public static void main(String args[])
{

    // construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);
    root.right.left.right = newNode(8);

    // variable to store product of leaf nodes
    prod = 1;
    leafProduct(root);
    System.out.println(prod );
}
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program to find product of
# all leaf nodes of binary tree

# Node class
class Node:

    # Function to initialise the node object
    def __init__(self, data):
        self.data = data # Assign data
        self.next =None

# return new node
def newNode( data) :

    temp = Node(0)
    temp.data = data
    temp.left = temp.right = None
    return temp

# product
prod = 1

# utility function which calculates
# product of all leaf nodes
def leafProduct( root ) :

    global prod
    if (root == None) :
        return

    # product root data to prod if
    # root is a leaf node
    if (root.left == None and root.right == None):
        prod *= root.data

    # propagate recursively in left
    # and right subtree
    leafProduct(root.left)
    leafProduct(root.right)

# Driver program

# construct binary tree
root = newNode(1)
root.left = newNode(2)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right = newNode(3)
root.right.right = newNode(7)
root.right.left = newNode(6)
root.right.left.right = newNode(8)

# variable to store product of leaf nodes
prod = 1
leafProduct(root)
print(prod )

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to find product of
// all leaf nodes of binary tree
using System;

class GFG
{

// struct binary tree node
public class Node
{
    public int data;
    public Node left, right;
};

// return new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// product
static int prod = 1;

// utility function which calculates
// product of all leaf nodes
static void leafProduct(Node root )
{
    if (root == null)
        return;

    // product root data to prod if
    // root is a leaf node
    if (root.left == null && root.right == null)
        prod *= root.data;

    // propagate recursively in left
    // and right subtree
    leafProduct(root.left);
    leafProduct(root.right);
}

// Driver code
public static void Main(String []args)
{

    // construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);
    root.right.left.right = newNode(8);

    // variable to store product of leaf nodes
    prod = 1;
    leafProduct(root);
    Console.WriteLine(prod );
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find product of
// all leaf nodes of binary tree
// struct binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    // return new node
    function newNode(data) {
var temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
    }

    // product
    var prod = 1;

    // utility function which calculates
    // product of all leaf nodes
    function leafProduct(root) {
        if (root == null)
            return;

        // product root data to prod if
        // root is a leaf node
        if (root.left == null && root.right == null)
            prod *= root.data;

        // propagate recursively in left
        // and right subtree
        leafProduct(root.left);
        leafProduct(root.right);
    }

    // Driver program

        // construct binary tree
var root = newNode(1);
        root.left = newNode(2);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right = newNode(3);
        root.right.right = newNode(7);
        root.right.left = newNode(6);
        root.right.left.right = newNode(8);

        // variable to store product of leaf nodes
        prod = 1;
        leafProduct(root);
        document.write(prod);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
1120
```

**时间复杂度:** O(n)，其中 n 为树中节点总数。