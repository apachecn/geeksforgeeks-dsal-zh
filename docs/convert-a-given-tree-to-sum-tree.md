# 将给定的树转换成它的和树

> 原文:[https://www . geesforgeks . org/convert-a-给定树到总和树/](https://www.geeksforgeeks.org/convert-a-given-tree-to-sum-tree/)

给定一个二叉树，其中每个节点都有正负值。将其转换为树，其中每个节点包含原始树中左右子树的总和。叶节点的值更改为 0。

例如，下面的树

```
                  10
               /      \
             -2        6
           /   \      /  \ 
         8     -4    7    5
```

应改为

```
                 20(4-2+12+6)
               /      \
         4(8-4)      12(7+5)
           /   \      /  \ 
         0      0    0    0
```

**解:**
遍历给定的树。在遍历中，存储当前节点的旧值，递归调用左右子树，并将当前节点的值更改为递归调用返回的值之和。最后返回新值和值的总和(即以此节点为根的子树中值的总和)。

## C++

```
// C++ program to convert a tree into its sum tree
#include <bits/stdc++.h>
using namespace std;

/* A tree node structure */
class node
{
    public:
int data;
node *left;
node *right;
};

// Convert a given tree to a tree where
// every node contains sum of values of
// nodes in left and right subtrees in the original tree
int toSumTree(node *Node)
{
    // Base case
    if(Node == NULL)
    return 0;

    // Store the old value
    int old_val = Node->data;

    // Recursively call for left and
    // right subtrees and store the sum as
    // old value of this node
    Node->data = toSumTree(Node->left) + toSumTree(Node->right);

    // Return the sum of values of nodes
    // in left and right subtrees and
    // old_value of this node
    return Node->data + old_val;
}

// A utility function to print
// inorder traversal of a Binary Tree
void printInorder(node* Node)
{
    if (Node == NULL)
        return;
    printInorder(Node->left);
    cout<<" "<<Node->data;
    printInorder(Node->right);
}

/* Utility function to create a new Binary Tree node */
node* newNode(int data)
{
    node *temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

/* Driver code */
int main()
{
    node *root = NULL;
    int x;

    /* Constructing tree given in the above figure */
    root = newNode(10);
    root->left = newNode(-2);
    root->right = newNode(6);
    root->left->left = newNode(8);
    root->left->right = newNode(-4);
    root->right->left = newNode(7);
    root->right->right = newNode(5);

    toSumTree(root);

    // Print inorder traversal of the converted
    // tree to test result of toSumTree()
    cout<<"Inorder Traversal of the resultant tree is: \n";
    printInorder(root);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>

/* A tree node structure */
struct node
{
  int data;
  struct node *left;
  struct node *right;
};

// Convert a given tree to a tree where every node contains sum of values of
// nodes in left and right subtrees in the original tree
int toSumTree(struct node *node)
{
    // Base case
    if(node == NULL)
      return 0;

    // Store the old value
    int old_val = node->data;

    // Recursively call for left and right subtrees and store the sum as
    // new value of this node
    node->data = toSumTree(node->left) + toSumTree(node->right);

    // Return the sum of values of nodes in left and right subtrees and
    // old_value of this node
    return node->data + old_val;
}

// A utility function to print inorder traversal of a Binary Tree
void printInorder(struct node* node)
{
     if (node == NULL)
          return;
     printInorder(node->left);
     printf("%d ", node->data);
     printInorder(node->right);
}

/* Utility function to create a new Binary Tree node */
struct node* newNode(int data)
{
  struct node *temp = new struct node;
  temp->data = data;
  temp->left = NULL;
  temp->right = NULL;

  return temp;
}

/* Driver function to test above functions */
int main()
{
  struct node *root = NULL;
  int x;

  /* Constructing tree given in the above figure */
  root = newNode(10);
  root->left = newNode(-2);
  root->right = newNode(6);
  root->left->left = newNode(8);
  root->left->right = newNode(-4);
  root->right->left = newNode(7);
  root->right->right = newNode(5);

  toSumTree(root);

  // Print inorder traversal of the converted tree to test result of toSumTree()
  printf("Inorder Traversal of the resultant tree is: \n");
  printInorder(root);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert a tree into its sum tree

// A binary tree node
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

    // Convert a given tree to a tree where every node contains sum of
    // values of nodes in left and right subtrees in the original tree
    int toSumTree(Node node)
    {
        // Base case
        if (node == null)
            return 0;

        // Store the old value
        int old_val = node.data;

        // Recursively call for left and right subtrees and store the sum
        // as new value of this node
        node.data = toSumTree(node.left) + toSumTree(node.right);

        // Return the sum of values of nodes in left and right subtrees
        // and old_value of this node
        return node.data + old_val;
    }

    // A utility function to print inorder traversal of a Binary Tree
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    /* Driver function to test above functions */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /* Constructing tree given in the above figure */
        tree.root = new Node(10);
        tree.root.left = new Node(-2);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(-4);
        tree.root.right.left = new Node(7);
        tree.root.right.right = new Node(5);

        tree.toSumTree(tree.root);

        // Print inorder traversal of the converted tree to test result
        // of toSumTree()
        System.out.println("Inorder Traversal of the resultant tree is:");
        tree.printInorder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to convert a tree
# into its sum tree

# Node definition
class node:

    def __init__(self, data):
        self.left = None
        self.right = None
        self.data = data

# Convert a given tree to a tree where
# every node contains sum of values of
# nodes in left and right subtrees
# in the original tree
def toSumTree(Node) :

    # Base case
    if(Node == None) :
        return 0

    # Store the old value
    old_val = Node.data

    # Recursively call for left and
    # right subtrees and store the sum as
    # new value of this node
    Node.data = toSumTree(Node.left) + \
                toSumTree(Node.right)

    # Return the sum of values of nodes
    # in left and right subtrees and
    # old_value of this node
    return Node.data + old_val

# A utility function to print
# inorder traversal of a Binary Tree
def printInorder(Node) :
    if (Node == None) :
        return
    printInorder(Node.left)
    print(Node.data, end = " ")
    printInorder(Node.right)

# Utility function to create a new Binary Tree node
def newNode(data) :
    temp = node(0)
    temp.data = data
    temp.left = None
    temp.right = None

    return temp

# Driver Code
if __name__ == "__main__":
    root = None
    x = 0

    # Constructing tree given in the above figure
    root = newNode(10)
    root.left = newNode(-2)
    root.right = newNode(6)
    root.left.left = newNode(8)
    root.left.right = newNode(-4)
    root.right.left = newNode(7)
    root.right.right = newNode(5)

    toSumTree(root)

    # Print inorder traversal of the converted
    # tree to test result of toSumTree()
    print("Inorder Traversal of the resultant tree is: ")
    printInorder(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to convert a tree
// into its sum tree
using System;

// A binary tree node
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

// Convert a given tree to a tree where
// every node contains sum of values of
// nodes in left and right subtrees in
// the original tree
public virtual int toSumTree(Node node)
{
    // Base case
    if (node == null)
    {
        return 0;
    }

    // Store the old value
    int old_val = node.data;

    // Recursively call for left and
    // right subtrees and store the sum
    // as new value of this node
    node.data = toSumTree(node.left) +
                toSumTree(node.right);

    // Return the sum of values of nodes
    // in left and right subtrees old_value
    // of this node
    return node.data + old_val;
}

// A utility function to print
// inorder traversal of a Binary Tree
public virtual void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    Console.Write(node.data + " ");
    printInorder(node.right);
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();

    /* Constructing tree given in
       the above figure */
    tree.root = new Node(10);
    tree.root.left = new Node(-2);
    tree.root.right = new Node(6);
    tree.root.left.left = new Node(8);
    tree.root.left.right = new Node(-4);
    tree.root.right.left = new Node(7);
    tree.root.right.right = new Node(5);

    tree.toSumTree(tree.root);

    // Print inorder traversal of the
    // converted tree to test result of toSumTree()
    Console.WriteLine("Inorder Traversal of " +
                     "the resultant tree is:");
    tree.printInorder(tree.root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to convert a tree
// into its sum tree

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

var root = null;

// Convert a given tree to a tree where
// every node contains sum of values of
// nodes in left and right subtrees in
// the original tree
function toSumTree(node)
{
    // Base case
    if (node == null)
    {
        return 0;
    }

    // Store the old value
    var old_val = node.data;

    // Recursively call for left and
    // right subtrees and store the sum
    // as new value of this node
    node.data = toSumTree(node.left) +
                toSumTree(node.right);

    // Return the sum of values of nodes
    // in left and right subtrees old_value
    // of this node
    return node.data + old_val;
}

// A utility function to print
// inorder traversal of a Binary Tree
function printInorder(node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}

// Driver Code

/* Constructing tree given in
   the above figure */
root = new Node(10);
root.left = new Node(-2);
root.right = new Node(6);
root.left.left = new Node(8);
root.left.right = new Node(-4);
root.right.left = new Node(7);
root.right.right = new Node(5);
toSumTree(root);
// Print inorder traversal of the
// converted tree to test result of toSumTree()
document.write("Inorder Traversal of " +
                 "the resultant tree is:<br>");
printInorder(root);

</script>
```

**输出:**

```
Inorder Traversal of the resultant tree is:
0 4 0 20 0 12 0
```

**时间复杂度:**该解决方案涉及给定树的简单遍历。所以时间复杂度是 O(n)，其中 n 是给定二叉树中的节点数。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。