# 检查给定的二叉树是否为 SumTree

> 原文:[https://www . geesforgeks . org/check-if-a-给定-二叉树-is-sumtree/](https://www.geeksforgeeks.org/check-if-a-given-binary-tree-is-sumtree/)

写一个函数，如果给定的二叉树是 SumTree，则返回 true，否则返回 false。SumTree 是一种二叉树，其中一个节点的值等于其左子树和右子树中存在的节点的总和。空树是 SumTree，空树的和可以认为是 0。叶节点也被认为是 SumTree。

下面是 SumTree 的一个例子。

```
          26
        /   \
      10     3
    /    \     \
  4      6      3
```

**方法 1(简单)**
求左子树和右子树的节点之和。检查计算的总和是否等于根的数据。此外，递归检查左右子树是否是 SumTrees。

## C++

```
// C++ program to check if Binary tree
// is sum tree or not
#include <iostream>
using namespace std;

// A binary tree node has data,
// left child and right child
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

// A utility function to get the sum
// of values in tree with root as root
int sum(struct node *root)
{
    if (root == NULL)
        return 0;

    return sum(root->left) + root->data +
           sum(root->right);
}

// Returns 1 if sum property holds for
// the given node and both of its children
int isSumTree(struct node* node)
{
    int ls, rs;

    // If node is NULL or it's a leaf
    // node then return true
    if (node == NULL ||
       (node->left == NULL &&
        node->right == NULL))
        return 1;

   // Get sum of nodes in left and
   // right subtrees
   ls = sum(node->left);
   rs = sum(node->right);

   // If the node and both of its
   // children satisfy the property
   // return 1 else 0
    if ((node->data == ls + rs) &&
          isSumTree(node->left) &&
          isSumTree(node->right))
        return 1;

   return 0;
}

// Helper function that allocates a new node
// with the given data and NULL left and right
// pointers.
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(
        sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

// Driver code
int main()
{
    struct node *root = newNode(26);
    root->left = newNode(10);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(6);
    root->right->right = newNode(3);

    if (isSumTree(root))
        cout << "The given tree is a SumTree ";
    else
        cout << "The given tree is not a SumTree ";

    getchar();
    return 0;
}

// This code is contributed by khushboogoyal499
```

## C

```
// C program to check if Binary tree
// is sum tree or not
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, left child and right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* A utility function to get the sum of values in tree with root
  as root */
int sum(struct node *root)
{
   if(root == NULL)
     return 0;
   return sum(root->left) + root->data + sum(root->right);
}

/* returns 1 if sum property holds for the given
    node and both of its children */
int isSumTree(struct node* node)
{
    int ls, rs;

    /* If node is NULL or it's a leaf node then
       return true */
    if(node == NULL ||
            (node->left == NULL && node->right == NULL))
        return 1;

   /* Get sum of nodes in left and right subtrees */
   ls = sum(node->left);
   rs = sum(node->right);

   /* if the node and both of its children satisfy the
       property return 1 else 0*/
    if((node->data == ls + rs)&&
            isSumTree(node->left) &&
            isSumTree(node->right))
        return 1;

   return 0;
}

/*
 Helper function that allocates a new node
 with the given data and NULL left and right
 pointers.
*/
struct node* newNode(int data)
{
    struct node* node =
        (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

/* Driver program to test above function */
int main()
{
    struct node *root  = newNode(26);
    root->left         = newNode(10);
    root->right        = newNode(3);
    root->left->left   = newNode(4);
    root->left->right  = newNode(6);
    root->right->right = newNode(3);
    if(isSumTree(root))
        printf("The given tree is a SumTree.");
    else
        printf("The given tree is not a SumTree.");

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if Binary tree
// is sum tree or not
import java.io.*;

// A binary tree node has data,
// left child and right child
class Node
{
    int data;
    Node left, right, nextRight;

    // Helper function that allocates a new node
    // with the given data and NULL left and right
    // pointers.
    Node(int item)
    {
        data = item;
        left = right = null;
    }
}
class BinaryTree {
    public static Node root;

    // A utility function to get the sum
    // of values in tree with root as root
    static int sum(Node node)
    {
        if(node == null)
        {
            return 0;
        }
        return (sum(node.left) + node.data+sum(node.right));
    }

    // Returns 1 if sum property holds for
    // the given node and both of its children
    static int isSumTree(Node node)
    {
        int ls,rs;

        // If node is NULL or it's a leaf
        // node then return true
        if(node == null || (node.left == null && node.right == null))
        {
            return 1;
        }

        // Get sum of nodes in left and
        // right subtrees
        ls = sum(node.left);
        rs = sum(node.right);

        // If the node and both of its
        // children satisfy the property
        // return 1 else 0
        if((node.data == ls + rs) && isSumTree(node.left) != 0 && isSumTree(node.right) != 0)
        {
            return 1;
        }
        return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        BinaryTree tree=new BinaryTree();
        tree.root=new Node(26);
        tree.root.left=new Node(10);
        tree.root.right=new Node(3);
        tree.root.left.left=new Node(4);
        tree.root.left.right=new Node(6);
        tree.root.right.right=new Node(3);
        if(isSumTree(root) != 0)
        {
            System.out.println("The given tree is a SumTree");
        }
        else
        {
            System.out.println("The given tree is not a SumTree");
        }
    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# A binary tree node has data,
# left child and right child
class node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# A utility function to get the sum
# of values in tree with root as root
def sum(root):

    if(root == None):
        return 0
    return (sum(root.left) +
            root.data +
            sum(root.right))

# returns 1 if sum property holds
# for the given node and both of
# its children
def isSumTree(node):

    # ls, rs

    # If node is None or it's a leaf
    # node then return true
    if(node == None or
      (node.left == None and
       node.right == None)):
        return 1

    # Get sum of nodes in left and
    # right subtrees
    ls = sum(node.left)
    rs = sum(node.right)

    # if the node and both of its children
    # satisfy the property return 1 else 0
    if((node.data == ls + rs) and
        isSumTree(node.left) and
        isSumTree(node.right)):
        return 1

    return 0

# Driver code
if __name__ == '__main__':

    root = node(26)
    root.left= node(10)
    root.right = node(3)
    root.left.left = node(4)
    root.left.right = node(6)
    root.right.right = node(3)

    if(isSumTree(root)):
        print("The given tree is a SumTree ")
    else:
        print("The given tree is not a SumTree ")

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to check if Binary tree
// is sum tree or not
using System;

// A binary tree node has data,
// left child and right child
public class Node
{
    public int data;
    public Node left, right, nextRight;

    // Helper function that allocates a new node
    // with the given data and NULL left and right
    // pointers.
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {

    public Node root;

    // A utility function to get the sum
    // of values in tree with root as root
    int sum(Node node)
    {
        if(node == null)
        {
            return 0;
        }
        return (sum(node.left) + node.data+sum(node.right));
    }

    // Returns 1 if sum property holds for
    // the given node and both of its children
    int isSumTree(Node node)
    {
        int ls,rs;

        // If node is NULL or it's a leaf
        // node then return true
        if(node == null || (node.left == null && node.right == null))
        {
            return 1;
        }

        // Get sum of nodes in left and
        // right subtrees
        ls = sum(node.left);
        rs = sum(node.right);

        // If the node and both of its
        // children satisfy the property
        // return 1 else 0
        if((node.data == ls + rs) && isSumTree(node.left) != 0 && isSumTree(node.right) != 0)
        {
            return 1;
        }
        return 0;
    }

    // Driver code
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(26);
        tree.root.left = new Node(10);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(6);
        tree.root.right.right = new Node(3);
        if(tree.isSumTree(tree.root) != 0)
        {
            Console.WriteLine("The given tree is a SumTree");
        }
        else
        {
            Console.WriteLine("The given tree is not a SumTree");
        }
    }
}

// This code is contributed by Pratham76
```

## java 描述语言

```
<script>
// Javascript program to check if Binary tree
// is sum tree or not

    // A binary tree node has data,
    // left child and right child
    class Node
    {
    // Helper function that allocates a new node
    // with the given data and NULL left and right
    // pointers.
        constructor(x) {
            this.data = x;
            this.left = null;
            this.right = null;
          }
    }

    let root;

    // A utility function to get the sum
    // of values in tree with root as root
    function sum(node)
    {
        if(node == null)
        {
            return 0;
        }
        return (sum(node.left) + node.data+sum(node.right));
    }

    // Returns 1 if sum property holds for
    // the given node and both of its children
    function isSumTree(node)
    {
        let ls,rs;

        // If node is NULL or it's a leaf
        // node then return true
        if(node == null || (node.left == null && node.right == null))
        {
            return 1;
        }

        // Get sum of nodes in left and
        // right subtrees
        ls = sum(node.left);
        rs = sum(node.right);

        // If the node and both of its
        // children satisfy the property
        // return 1 else 0
        if((node.data == ls + rs) && isSumTree(node.left) != 0 && isSumTree(node.right) != 0)
        {
            return 1;
        }
        return 0;
    }

    // Driver code
    root = new Node(26)
    root.left= new Node(10)
    root.right = new Node(3)
    root.left.left = new Node(4)
    root.left.right = new Node(6)
    root.right.right = new Node(3)

    if(isSumTree(root) != 0)
    {
        document.write("The given tree is a SumTree");
    }
    else
    {
        document.write("The given tree is not a SumTree");
    }

    // This code is contributed by unknown2108
</script>
```

**Output**

```
The given tree is a SumTree
```