# 将正常 BST 转换为平衡 BST

> 原文:[https://www . geesforgeks . org/convert-normal-BST-balanced-BST/](https://www.geeksforgeeks.org/convert-normal-bst-balanced-bst/)

给定一个可能不平衡的 BST(**B**in arial**S**search**T**REE)，将其转换为具有最小可能高度的平衡 BST。
示例:

```
Input:
       30
      /
     20
    /
   10
Output:
     20
   /   \
 10     30

Input:
         4
        /
       3
      /
     2
    /
   1
Output:
      3            3           2
    /  \         /  \        /  \
   1    4   OR  2    4  OR  1    3   OR ..
    \          /                   \
     2        1                     4 

Input:
          4
        /   \
       3     5
      /       \
     2         6 
    /           \
   1             7
Output:
       4
    /    \
   2      6
 /  \    /  \
1    3  5    7 
```

一个**简单的解决方案**是按顺序遍历节点，然后一个接一个地插入到像 AVL 树这样的自平衡 BST 中。该解决方案的时间复杂度为 O(n Log n)，并且该解决方案不能保证
An **高效解决方案**能够在 O(n)时间内以最小可能高度构建平衡的 BST。以下是步骤。

1.  按顺序遍历给定的 BST，并将结果存储在数组中。这一步需要 O(n)个时间。请注意，这个数组将被排序，因为有序遍历 BST 总是会产生排序的序列。
2.  使用这里讨论的递归方法从上面创建的排序数组构建一个平衡的 BST。这个步骤也需要 O(n)个时间，因为我们遍历每个元素正好一次，处理一个元素需要 O(1)个时间。

下面是以上步骤的实现。

## C++

```
// C++ program to convert a left unbalanced BST to
// a balanced BST
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node* left,  *right;
};

/* This function traverse the skewed binary tree and
   stores its nodes pointers in vector nodes[] */
void storeBSTNodes(Node* root, vector<Node*> &nodes)
{
    // Base case
    if (root==NULL)
        return;

    // Store nodes in Inorder (which is sorted
    // order for BST)
    storeBSTNodes(root->left, nodes);
    nodes.push_back(root);
    storeBSTNodes(root->right, nodes);
}

/* Recursive function to construct binary tree */
Node* buildTreeUtil(vector<Node*> &nodes, int start,
                   int end)
{
    // base case
    if (start > end)
        return NULL;

    /* Get the middle element and make it root */
    int mid = (start + end)/2;
    Node *root = nodes[mid];

    /* Using index in Inorder traversal, construct
       left and right subtress */
    root->left  = buildTreeUtil(nodes, start, mid-1);
    root->right = buildTreeUtil(nodes, mid+1, end);

    return root;
}

// This functions converts an unbalanced BST to
// a balanced BST
Node* buildTree(Node* root)
{
    // Store nodes of given BST in sorted order
    vector<Node *> nodes;
    storeBSTNodes(root, nodes);

    // Constructs BST from nodes[]
    int n = nodes.size();
    return buildTreeUtil(nodes, 0, n-1);
}

// Utility function to create a new node
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

/* Function to do preorder traversal of tree */
void preOrder(Node* node)
{
    if (node == NULL)
        return;
    printf("%d ", node->data);
    preOrder(node->left);
    preOrder(node->right);
}

// Driver program
int main()
{
    /* Constructed skewed binary tree is
                10
               /
              8
             /
            7
           /
          6
         /
        5   */

    Node* root = newNode(10);
    root->left = newNode(8);
    root->left->left = newNode(7);
    root->left->left->left = newNode(6);
    root->left->left->left->left = newNode(5);

    root = buildTree(root);

    printf("Preorder traversal of balanced "
            "BST is : \n");
    preOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert a left unbalanced BST to a balanced BST

import java.util.*;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* This function traverse the skewed binary tree and
       stores its nodes pointers in vector nodes[] */
    void storeBSTNodes(Node root, Vector<Node> nodes)
    {
        // Base case
        if (root == null)
            return;

        // Store nodes in Inorder (which is sorted
        // order for BST)
        storeBSTNodes(root.left, nodes);
        nodes.add(root);
        storeBSTNodes(root.right, nodes);
    }

    /* Recursive function to construct binary tree */
    Node buildTreeUtil(Vector<Node> nodes, int start,
            int end)
    {
        // base case
        if (start > end)
            return null;

        /* Get the middle element and make it root */
        int mid = (start + end) / 2;
        Node node = nodes.get(mid);

        /* Using index in Inorder traversal, construct
           left and right subtress */
        node.left = buildTreeUtil(nodes, start, mid - 1);
        node.right = buildTreeUtil(nodes, mid + 1, end);

        return node;
    }

    // This functions converts an unbalanced BST to
    // a balanced BST
    Node buildTree(Node root)
    {
        // Store nodes of given BST in sorted order
        Vector<Node> nodes = new Vector<Node>();
        storeBSTNodes(root, nodes);

        // Constructs BST from nodes[]
        int n = nodes.size();
        return buildTreeUtil(nodes, 0, n - 1);
    }

    /* Function to do preorder traversal of tree */
    void preOrder(Node node)
    {
        if (node == null)
            return;
        System.out.print(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    // Driver program to test the above functions
    public static void main(String[] args)
    {
         /* Constructed skewed binary tree is
                10
               /
              8
             /
            7
           /
          6
         /
        5   */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.left.left = new Node(7);
        tree.root.left.left.left = new Node(6);
        tree.root.left.left.left.left = new Node(5);

        tree.root = tree.buildTree(tree.root);
        System.out.println("Preorder traversal of balanced BST is :");
        tree.preOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to convert a left
# unbalanced BST to a balanced BST
import sys
import math

# A binary tree node has data, pointer to left child
# and a pointer to right child
class Node:
    def __init__(self,data):
        self.data=data
        self.left=None
        self.right=None

# This function traverse the skewed binary tree and
# stores its nodes pointers in vector nodes[]
def storeBSTNodes(root,nodes):

    # Base case
    if not root:
        return

    # Store nodes in Inorder (which is sorted
    # order for BST)
    storeBSTNodes(root.left,nodes)
    nodes.append(root)
    storeBSTNodes(root.right,nodes)

# Recursive function to construct binary tree
def buildTreeUtil(nodes,start,end):

    # base case
    if start>end:
        return None

    # Get the middle element and make it root
    mid=(start+end)//2
    node=nodes[mid]

    # Using index in Inorder traversal, construct
    # left and right subtress
    node.left=buildTreeUtil(nodes,start,mid-1)
    node.right=buildTreeUtil(nodes,mid+1,end)
    return node

# This functions converts an unbalanced BST to
# a balanced BST
def buildTree(root):

    # Store nodes of given BST in sorted order
    nodes=[]
    storeBSTNodes(root,nodes)

    # Constructs BST from nodes[]
    n=len(nodes)
    return buildTreeUtil(nodes,0,n-1)

# Function to do preorder traversal of tree
def preOrder(root):
    if not root:
        return
    print("{} ".format(root.data),end="")
    preOrder(root.left)
    preOrder(root.right)

# Driver code
if __name__=='__main__':
    # Constructed skewed binary tree is
    #         10
    #         /
    #         8
    #         /
    #     7
    #     /
    #     6
    #     /
    # 5
    root = Node(10)
    root.left = Node(8)
    root.left.left = Node(7)
    root.left.left.left = Node(6)
    root.left.left.left.left = Node(5)
    root = buildTree(root)
    print("Preorder traversal of balanced BST is :")
    preOrder(root)

# This code has been contributed by Vikash Kumar 37
```

## C#

```
using System;
using System.Collections.Generic;

// C# program to convert a left unbalanced BST to a balanced BST

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
public class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

public class BinaryTree
{
    public Node root;

    /* This function traverse the skewed binary tree and
       stores its nodes pointers in vector nodes[] */
    public virtual void storeBSTNodes(Node root, List<Node> nodes)
    {
        // Base case
        if (root == null)
        {
            return;
        }

        // Store nodes in Inorder (which is sorted
        // order for BST)
        storeBSTNodes(root.left, nodes);
        nodes.Add(root);
        storeBSTNodes(root.right, nodes);
    }

    /* Recursive function to construct binary tree */
    public virtual Node buildTreeUtil(List<Node> nodes, int start, int end)
    {
        // base case
        if (start > end)
        {
            return null;
        }

        /* Get the middle element and make it root */
        int mid = (start + end) / 2;
        Node node = nodes[mid];

        /* Using index in Inorder traversal, construct
           left and right subtress */
        node.left = buildTreeUtil(nodes, start, mid - 1);
        node.right = buildTreeUtil(nodes, mid + 1, end);

        return node;
    }

    // This functions converts an unbalanced BST to
    // a balanced BST
    public virtual Node buildTree(Node root)
    {
        // Store nodes of given BST in sorted order
        List<Node> nodes = new List<Node>();
        storeBSTNodes(root, nodes);

        // Constructs BST from nodes[]
        int n = nodes.Count;
        return buildTreeUtil(nodes, 0, n - 1);
    }

    /* Function to do preorder traversal of tree */
    public virtual void preOrder(Node node)
    {
        if (node == null)
        {
            return;
        }
        Console.Write(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    // Driver program to test the above functions
    public static void Main(string[] args)
    {
         /* Constructed skewed binary tree is
                10
               /
              8
             /
            7
           /
          6
         /
        5   */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.left.left = new Node(7);
        tree.root.left.left.left = new Node(6);
        tree.root.left.left.left.left = new Node(5);

        tree.root = tree.buildTree(tree.root);
        Console.WriteLine("Preorder traversal of balanced BST is :");
        tree.preOrder(tree.root);
    }
}

  //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program to convert a left
    // unbalanced BST to a balanced BST

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let root;

    /* This function traverse the skewed binary tree and
       stores its nodes pointers in vector nodes[] */
    function storeBSTNodes(root, nodes)
    {
        // Base case
        if (root == null)
            return;

        // Store nodes in Inorder (which is sorted
        // order for BST)
        storeBSTNodes(root.left, nodes);
        nodes.push(root);
        storeBSTNodes(root.right, nodes);
    }

    /* Recursive function to construct binary tree */
    function buildTreeUtil(nodes, start, end)
    {
        // base case
        if (start > end)
            return null;

        /* Get the middle element and make it root */
        let mid = parseInt((start + end) / 2, 10);
        let node = nodes[mid];

        /* Using index in Inorder traversal, construct
           left and right subtress */
        node.left = buildTreeUtil(nodes, start, mid - 1);
        node.right = buildTreeUtil(nodes, mid + 1, end);

        return node;
    }

    // This functions converts an unbalanced BST to
    // a balanced BST
    function buildTree(root)
    {
        // Store nodes of given BST in sorted order
        let nodes = [];
        storeBSTNodes(root, nodes);

        // Constructs BST from nodes[]
        let n = nodes.length;
        return buildTreeUtil(nodes, 0, n - 1);
    }

    /* Function to do preorder traversal of tree */
    function preOrder(node)
    {
        if (node == null)
            return;
        document.write(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    /* Constructed skewed binary tree is
                  10
                 /
                8
               /
              7
             /
            6
           /
          5   */
    root = new Node(10);
    root.left = new Node(8);
    root.left.left = new Node(7);
    root.left.left.left = new Node(6);
    root.left.left.left.left = new Node(5);

    root = buildTree(root);
    document.write("Preorder traversal of balanced BST is :" + "</br>");
    preOrder(root);

</script>
```

**输出:**

```
Preorder traversal of balanced BST is : 
7 5 6 8 10 
```

本文由 **Aditya Goel** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并将你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息