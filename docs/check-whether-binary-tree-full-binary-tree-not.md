# 检查二叉树是否为全二叉树

> 原文:[https://www . geesforgeks . org/check-when-二叉树-full-二叉树-not/](https://www.geeksforgeeks.org/check-whether-binary-tree-full-binary-tree-not/)

完全二叉树被定义为所有节点都有零个或两个子节点的二叉树。相反，完全二叉树中没有节点，只有一个子节点。关于全二叉树的更多信息可以在[这里](http://courses.cs.vt.edu/~cs3114/Fall09/wmcquain/Notes/T03a.BinaryTreeTheorems.pdf)找到。

例如:

![Full](img/ef5f584cbb9229f28c6d9971eb7718ef.png)

为了检查二叉树是否是完全二叉树，我们需要测试以下情况:-
1)如果二叉树节点为空，则它是完全二叉树。
2)如果一个二叉树节点确实有空的左右子树，那么按照定义它就是一个全二叉树。
3)如果一个二叉树节点有左右子树，那么从定义上来说，它就是一个完整二叉树的一部分。在这种情况下，递归检查左右子树本身是否也是二叉树。
4)在所有其他左右子树的组合中，二叉树不是完全二叉树。

下面是检查二叉树是否是完全二叉树的实现。

## C++

```
// C++ program to check whether a given Binary Tree is full or not
#include <bits/stdc++.h>

using namespace std;

/*  Tree node structure */
struct Node
{
    int key;
    struct Node *left, *right;
};

/* Helper function that allocates a new node with the
   given key and NULL left and right pointer. */
struct Node *newNode(char k)
{
    struct Node *node = new  Node;
    node->key = k;
    node->right = node->left = NULL;
    return node;
}

/* This function tests if a binary tree is a full binary tree. */
bool isFullTree (struct Node* root)
{
    // If empty tree
    if (root == NULL)
        return true;

    // If leaf node
    if (root->left == NULL && root->right == NULL)
        return true;

    // If both left and right are not NULL, and left & right subtrees
    // are full
    if ((root->left) && (root->right))
        return (isFullTree(root->left) && isFullTree(root->right));

    // We reach here when none of the above if conditions work
    return false;
}

// Driver Program
int main()
{
    struct Node* root = NULL;
    root = newNode(10);
    root->left = newNode(20);
    root->right = newNode(30);

    root->left->right = newNode(40);
    root->left->left = newNode(50);
    root->right->left = newNode(60);
    root->right->right = newNode(70);

    root->left->left->left = newNode(80);
    root->left->left->right = newNode(90);
    root->left->right->left = newNode(80);
    root->left->right->right = newNode(90);
    root->right->left->left = newNode(80);
    root->right->left->right = newNode(90);
    root->right->right->left = newNode(80);
    root->right->right->right = newNode(90);

    if (isFullTree(root))
        cout << "The Binary Tree is full\n";
    else
        cout << "The Binary Tree is not full\n";

    return(0);
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to check whether a given Binary Tree is full or not
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

/*  Tree node structure */
struct Node
{
    int key;
    struct Node *left, *right;
};

/* Helper function that allocates a new node with the
   given key and NULL left and right pointer. */
struct Node *newNode(char k)
{
    struct Node *node = (struct Node*)malloc(sizeof(struct Node));
    node->key = k;
    node->right = node->left = NULL;
    return node;
}

/* This function tests if a binary tree is a full binary tree. */
bool isFullTree (struct Node* root)
{
    // If empty tree
    if (root == NULL)
        return true;

    // If leaf node
    if (root->left == NULL && root->right == NULL)
        return true;

    // If both left and right are not NULL, and left & right subtrees
    // are full
    if ((root->left) && (root->right))
        return (isFullTree(root->left) && isFullTree(root->right));

    // We reach here when none of the above if conditions work
    return false;
}

// Driver Program
int main()
{
    struct Node* root = NULL;
    root = newNode(10);
    root->left = newNode(20);
    root->right = newNode(30);

    root->left->right = newNode(40);
    root->left->left = newNode(50);
    root->right->left = newNode(60);
    root->right->right = newNode(70);

    root->left->left->left = newNode(80);
    root->left->left->right = newNode(90);
    root->left->right->left = newNode(80);
    root->left->right->right = newNode(90);
    root->right->left->left = newNode(80);
    root->right->left->right = newNode(90);
    root->right->right->left = newNode(80);
    root->right->right->right = newNode(90);

    if (isFullTree(root))
        printf("The Binary Tree is full\n");
    else
        printf("The Binary Tree is not full\n");

    return(0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if binary tree is full or not

/*  Tree node structure */
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* this function checks if a binary tree is full or not */
    boolean isFullTree(Node node)
    {
        // if empty tree
        if(node == null)
        return true;

        // if leaf node
        if(node.left == null && node.right == null )
            return true;

        // if both left and right subtrees are not null
        // the are full
        if((node.left!=null) && (node.right!=null))
            return (isFullTree(node.left) && isFullTree(node.right));

        // if none work
        return false;
    }

    // Driver program
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(20);
        tree.root.right = new Node(30);
        tree.root.left.right = new Node(40);
        tree.root.left.left = new Node(50);
        tree.root.right.left = new Node(60);
        tree.root.left.left.left = new Node(80);
        tree.root.right.right = new Node(70);
        tree.root.left.left.right = new Node(90);
        tree.root.left.right.left = new Node(80);
        tree.root.left.right.right = new Node(90);
        tree.root.right.left.left = new Node(80);
        tree.root.right.left.right = new Node(90);
        tree.root.right.right.left = new Node(80);
        tree.root.right.right.right = new Node(90);

        if(tree.isFullTree(tree.root))
            System.out.print("The binary tree is full");
        else
            System.out.print("The binary tree is not full");
    }
}

// This code is contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to check whether given Binary tree is full or not

# Tree node structure
class Node:

    # Constructor of the node class for creating the node
    def __init__(self , key):
        self.key = key
        self.left = None
        self.right = None

# Checks if the binary tree is full or not
def isFullTree(root):

    # If empty tree
    if root is None:   
        return True

    # If leaf node
    if root.left is None and root.right is None:
        return True

    # If both left and right subtress are not None and
    # left and right subtress are full
    if root.left is not None and root.right is not None:
        return (isFullTree(root.left) and isFullTree(root.right))

    # We reach here when none of the above if conditions work
    return False

# Driver Program
root = Node(10);
root.left = Node(20);
root.right = Node(30);

root.left.right = Node(40);
root.left.left = Node(50);
root.right.left = Node(60);
root.right.right = Node(70);

root.left.left.left = Node(80);
root.left.left.right = Node(90);
root.left.right.left = Node(80);
root.left.right.right = Node(90);
root.right.left.left = Node(80);
root.right.left.right = Node(90);
root.right.right.left = Node(80);
root.right.right.right = Node(90);

if isFullTree(root):
    print "The Binary tree is full"
else:
    print "Binary tree is not full"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to check if binary tree
// is full or not
using System;

/* Tree node structure */
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG
{
public Node root;

/* This function checks if a binary
tree is full or not */
public virtual bool isFullTree(Node node)
{
    // if empty tree
    if (node == null)
    {
    return true;
    }

    // if leaf node
    if (node.left == null && node.right == null)
    {
        return true;
    }

    // if both left and right subtrees
    // are not null they are full
    if ((node.left != null) && (node.right != null))
    {
        return (isFullTree(node.left) &&
                isFullTree(node.right));
    }

    // if none work
    return false;
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(10);
    tree.root.left = new Node(20);
    tree.root.right = new Node(30);
    tree.root.left.right = new Node(40);
    tree.root.left.left = new Node(50);
    tree.root.right.left = new Node(60);
    tree.root.left.left.left = new Node(80);
    tree.root.right.right = new Node(70);
    tree.root.left.left.right = new Node(90);
    tree.root.left.right.left = new Node(80);
    tree.root.left.right.right = new Node(90);
    tree.root.right.left.left = new Node(80);
    tree.root.right.left.right = new Node(90);
    tree.root.right.right.left = new Node(80);
    tree.root.right.right.right = new Node(90);

    if (tree.isFullTree(tree.root))
    {
        Console.Write("The binary tree is full");
    }
    else
    {
        Console.Write("The binary tree is not full");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to check if binary tree is full or not

/*  Tree node structure */
class Node {
    constructor(item) {
        this.data = item;
        this.left = this.right = null;
    }
}

    var root;

    /* this function checks if a binary tree is full or not */
    function isFullTree( node) {
        // if empty tree
        if (node == null)
            return true;

        // if leaf node
        if (node.left == null && node.right == null)
            return true;

        // if both left and right subtrees are not null
        // the are full
        if ((node.left != null) && (node.right != null))
            return (isFullTree(node.left) && isFullTree(node.right));

        // if none work
        return false;
    }

    // Driver program

        root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.right = new Node(40);
        root.left.left = new Node(50);
        root.right.left = new Node(60);
        root.left.left.left = new Node(80);
        root.right.right = new Node(70);
        root.left.left.right = new Node(90);
        root.left.right.left = new Node(80);
        root.left.right.right = new Node(90);
        root.right.left.left = new Node(80);
        root.right.left.right = new Node(90);
        root.right.right.left = new Node(80);
        root.right.right.right = new Node(90);
         if(isFullTree(root))
            document.write("The binary tree is full");
        else
            document.write("The binary tree is not full");

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
The Binary Tree is full
```

上述代码的时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。

本文由**高拉夫·古普塔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息