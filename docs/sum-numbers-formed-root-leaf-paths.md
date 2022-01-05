# 从根到叶路径形成的所有数字的总和

> 原文:[https://www . geesforgeks . org/sum-numbers-formed-root-leaf-path/](https://www.geeksforgeeks.org/sum-numbers-formed-root-leaf-paths/)

给定一个二叉树，其中每个节点值都是 1-9 的数字。求从根到叶路径形成的所有数字的和。

例如，考虑下面的二叉树。

```
           6
       /      \
     3          5
   /   \          \
  2     5          4  
      /   \
     7     4
  There are 4 leaves, hence 4 root to leaf paths:
   Path                    Number
  6->3->2                   632
  6->3->5->7               6357
  6->3->5->4               6354
  6->5>4                    654   
Answer = 632 + 6357 + 6354 + 654 = 13997 
```

这个想法是对树进行一次前序遍历。在前序遍历中，跟踪计算值直到当前节点，让这个值为*值*。对于每个节点，我们将 *val* 更新为 *val*10* plus 节点的数据。

## C++

```
// C++ program to find sum of
// all paths from root to leaves 
#include <bits/stdc++.h>
using namespace std;

class node 
{ 
    public:
    int data; 
    node *left, *right; 
}; 

// function to allocate new node with given data 
node* newNode(int data) 
{ 
    node* Node = new node();
    Node->data = data; 
    Node->left = Node->right = NULL; 
    return (Node); 
} 

// Returns sum of all root to leaf paths.
// The first parameter is root 
// of current subtree, the second 
// parameter is value of the number formed 
// by nodes from root to this node 
int treePathsSumUtil(node *root, int val) 
{ 
    // Base case 
    if (root == NULL) return 0; 

    // Update val 
    val = (val*10 + root->data); 

    // if current node is leaf, return the current value of val 
    if (root->left==NULL && root->right==NULL) 
    return val; 

    // recur sum of values for left and right subtree 
    return treePathsSumUtil(root->left, val) + 
        treePathsSumUtil(root->right, val); 
} 

// A wrapper function over treePathsSumUtil() 
int treePathsSum(node *root) 
{ 
    // Pass the initial value as 0
    // as there is nothing above root 
    return treePathsSumUtil(root, 0); 
} 

// Driver code
int main() 
{ 
    node *root = newNode(6); 
    root->left = newNode(3); 
    root->right = newNode(5); 
    root->left->left = newNode(2); 
    root->left->right = newNode(5); 
    root->right->right = newNode(4); 
    root->left->right->left = newNode(7); 
    root->left->right->right = newNode(4); 
    cout<<"Sum of all paths is "<<treePathsSum(root); 
    return 0; 
} 

// This code is contributed by rathbhupendra
```

## C

```
// C program to find sum of all paths from root to leaves
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *left, *right;
};

// function to allocate new node with given data
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Returns sum of all root to leaf paths. The first parameter is root
// of current subtree, the second parameter is value of the number formed
// by nodes from root to this node
int treePathsSumUtil(struct node *root, int val)
{
    // Base case
    if (root == NULL)  return 0;

    // Update val
    val = (val*10 + root->data);

    // if current node is leaf, return the current value of val
    if (root->left==NULL && root->right==NULL)
       return val;

    // recur sum of values for left and right subtree
    return treePathsSumUtil(root->left, val) +
           treePathsSumUtil(root->right, val);
}

// A wrapper function over treePathsSumUtil()
int treePathsSum(struct node *root)
{
    // Pass the initial value as 0 as there is nothing above root
    return treePathsSumUtil(root, 0);
}

// Driver function to test the above functions
int main()
{
    struct node *root = newNode(6);
    root->left        = newNode(3);
    root->right       = newNode(5);
    root->left->left  = newNode(2);
    root->left->right = newNode(5);
    root->right->right = newNode(4);
    root->left->right->left = newNode(7);
    root->left->right->right = newNode(4);
    printf("Sum of all paths is %d", treePathsSum(root));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all numbers that are formed from root
// to leaf paths

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

    // Returns sum of all root to leaf paths. The first parameter is 
    // root of current subtree, the second parameter is value of the  
    // number formed by nodes from root to this node
    int treePathsSumUtil(Node node, int val) 
    {
        // Base case
        if (node == null)
            return 0;

        // Update val
        val = (val * 10 + node.data);

        // if current node is leaf, return the current value of val
        if (node.left == null && node.right == null)
            return val;

        // recur sum of values for left and right subtree
        return treePathsSumUtil(node.left, val)
                + treePathsSumUtil(node.right, val);
    }

    // A wrapper function over treePathsSumUtil()
    int treePathsSum(Node node) 
    {
        // Pass the initial value as 0 as there is nothing above root
        return treePathsSumUtil(node, 0);
    }

    // Driver program to test above functions
    public static void main(String args[]) 
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(6);
        tree.root.left = new Node(3);
        tree.root.right = new Node(5);
        tree.root.right.right = new Node(4);
        tree.root.left.left = new Node(2);
        tree.root.left.right = new Node(5);
        tree.root.left.right.right = new Node(4);
        tree.root.left.right.left = new Node(7);

        System.out.print("Sum of all paths is " + 
                                 tree.treePathsSum(tree.root));   
    }    
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find sum of all paths from root to leaves

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returs sums of all root to leaf paths. The first parameter is root
# of current subtree, the second paramete"r is value of the number
# formed by nodes from root to this node
def treePathsSumUtil(root, val):

    # Base Case
    if root is None:
        return 0

    # Update val
    val = (val*10 + root.data)

    # If current node is leaf, return the current value of val
    if root.left is None and root.right is None:
        return val

    # Recur sum of values for left and right subtree
    return (treePathsSumUtil(root.left, val) + 
            treePathsSumUtil(root.right, val))

# A wrapper function over treePathSumUtil()
def treePathsSum(root):

    # Pass the initial value as 0 as ther is nothing above root
    return treePathsSumUtil(root, 0)

# Driver function to test above function
root = Node(6)
root.left = Node(3)
root.right = Node(5)
root.left.left = Node(2)
root.left.right = Node(5)
root.right.right = Node(4)
root.left.right.left = Node(7)
root.left.right.right = Node(4)
print "Sum of all paths is", treePathsSum(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// c# program to find sum of all numbers 
// that are formed from root to leaf paths 
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

// Returns sum of all root to leaf paths. 
// The first parameter is root of current 
// subtree, the second parameter is value 
// of the number formed by nodes from root
// to this node 
public virtual int treePathsSumUtil(Node node,
                                    int val)
{
    // Base case 
    if (node == null)
    {
        return 0;
    }

    // Update val 
    val = (val * 10 + node.data);

    // if current node is leaf, return 
    // the current value of val 
    if (node.left == null && node.right == null)
    {
        return val;
    }

    // recur sum of values for left and right subtree 
    return treePathsSumUtil(node.left, val) +
           treePathsSumUtil(node.right, val);
}

// A wrapper function over treePathsSumUtil() 
public virtual int treePathsSum(Node node)
{
    // Pass the initial value as 0 as 
    // there is nothing above root 
    return treePathsSumUtil(node, 0);
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(6);
    tree.root.left = new Node(3);
    tree.root.right = new Node(5);
    tree.root.right.right = new Node(4);
    tree.root.left.left = new Node(2);
    tree.root.left.right = new Node(5);
    tree.root.left.right.right = new Node(4);
    tree.root.left.right.left = new Node(7);

    Console.Write("Sum of all paths is " + 
                   tree.treePathsSum(tree.root));
}
}

// This code is contributed by Shrikant13
```

**Output:**

```
Sum of all paths is 13997
```

**时间复杂度:**上面的代码是一个简单的前序遍历代码，每隔恰好一次访问。因此，时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。

本文由**拉姆昌德 R** 供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论