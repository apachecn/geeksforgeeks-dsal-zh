# 二叉查找树某节点的后置前置

> 原文:[https://www . geesforgeks . org/post order-preference-node-binary-search-tree/](https://www.geeksforgeeks.org/postorder-predecessor-node-binary-search-tree/)

给定一棵二叉树和二叉树中的一个节点，找到给定节点的后置前置。

**示例:**

```
Consider the following binary tree
              20            
           /      \         
          10       26       
         /  \     /   \     
       4     18  24    27   
            /  \
           14   19
          /  \
         13  15
Input :  4
Output : 10
Postorder traversal of given tree is 4, 13, 15, 
14, 19, 18, 10, 24, 27, 26, 20.

Input :  24
Output : 10
```

一个**简单的解决方案**是首先将给定树的后序遍历存储在一个数组中，然后线性搜索给定的节点并打印它旁边的节点。
时间复杂度:O(n)
辅助空间:O(n)
一个**高效解**基于以下观察。

1.  如果给定节点的右边的子节点存在，那么右边的子节点就是后置前置。
2.  如果右边的子节点不存在，并且给定的节点是其父节点的左边的子节点，那么它的同级节点就是它的后置前置节点。
3.  如果以上条件都不满足(左子节点不存在，并且给定节点不是其父节点的右子节点)，那么我们使用父指针向上移动，直到发生以下情况之一。
    *   我们到达了根。在这种情况下，后置前置任务不存在。
    *   当前节点(给定节点的祖先之一)是其父节点的右子节点，在这种情况下，后置前置节点是当前节点的同级节点。

## C++

```
// C++ program to find postorder predecessor of
// a node in Binary Tree.
#include <iostream>
using namespace std;

struct Node {
    struct Node *left, *right, *parent;
    int key;
};

Node* newNode(int key)
{
    Node* temp = new Node;
    temp->left = temp->right = temp->parent = NULL;
    temp->key = key;
    return temp;
}

Node* postorderPredecessor(Node* root, Node* n)
{
    // If right child exists, then it is postorder
    // predecessor.
    if (n->right)
        return n->right;

    // If right child does not exist, then
    // travel up (using parent pointers)
    // until we reach a node which is right
    // child of its parent.
    Node *curr = n, *parent = curr->parent;
    while (parent != NULL && parent->left == curr) {
        curr = curr->parent;
        parent = parent->parent;
    }

    // If we reached root, then the given
    // node has no postorder predecessor
    if (parent == NULL)
        return NULL;

    return parent->left;
}

int main()
{
    Node* root = newNode(20);
    root->parent = NULL;
    root->left = newNode(10);
    root->left->parent = root;
    root->left->left = newNode(4);
    root->left->left->parent = root->left;
    root->left->right = newNode(18);
    root->left->right->parent = root->left;
    root->right = newNode(26);
    root->right->parent = root;
    root->right->left = newNode(24);
    root->right->left->parent = root->right;
    root->right->right = newNode(27);
    root->right->right->parent = root->right;
    root->left->right->left = newNode(14);
    root->left->right->left->parent = root->left->right;
    root->left->right->left->left = newNode(13);
    root->left->right->left->left->parent = root->left->right->left;
    root->left->right->left->right = newNode(15);
    root->left->right->left->right->parent = root->left->right->left;
    root->left->right->right = newNode(19);
    root->left->right->right->parent = root->left->right;

    Node* nodeToCheck = root->left->right;

    Node* res = postorderPredecessor(root, nodeToCheck);

    if (res) {
        printf("Postorder predecessor of %d is %d\n",
               nodeToCheck->key, res->key);
    }
    else {
        printf("Postorder predecessor of %d is NULL\n",
               nodeToCheck->key);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find postorder predecessor
// of a node in Binary Tree.
import java.util.*;

class GFG{

static class Node
{
    Node left, right, parent;
    int key;
};

static Node newNode(int key)
{
    Node temp = new Node();
    temp.left = temp.right = temp.parent = null;
    temp.key = key;
    return temp;
}

static Node postorderPredecessor(Node root, Node n)
{

    // If right child exists, then it is
    // postorder predecessor.
    if (n.right != null)
        return n.right;

    // If right child does not exist, then
    // travel up (using parent pointers)
    // until we reach a node which is right
    // child of its parent.
    Node curr = n, parent = curr.parent;
    while (parent != null && parent.left == curr)
    {
        curr = curr.parent;
        parent = parent.parent;
    }

    // If we reached root, then the given
    // node has no postorder predecessor
    if (parent == null)
        return null;

    return parent.left;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(20);
    root.parent = null;
    root.left = newNode(10);
    root.left.parent = root;
    root.left.left = newNode(4);
    root.left.left.parent = root.left;
    root.left.right = newNode(18);
    root.left.right.parent = root.left;
    root.right = newNode(26);
    root.right.parent = root;
    root.right.left = newNode(24);
    root.right.left.parent = root.right;
    root.right.right = newNode(27);
    root.right.right.parent = root.right;
    root.left.right.left = newNode(14);
    root.left.right.left.parent = root.left.right;
    root.left.right.left.left = newNode(13);
    root.left.right.left.left.parent = root.left.right.left;
    root.left.right.left.right = newNode(15);
    root.left.right.left.right.parent = root.left.right.left;
    root.left.right.right = newNode(19);
    root.left.right.right.parent = root.left.right;

    Node nodeToCheck = root.left.right;

    Node res = postorderPredecessor(root, nodeToCheck);

    if (res != null)
    {
        System.out.printf("Postorder predecessor " +
                          "of %d is %d\n",
                          nodeToCheck.key, res.key);
    }
    else
    {
        System.out.printf("Postorder predecessor " +
                          "of %d is null\n",
                          nodeToCheck.key);
    }
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
"""Python3 program to find postorder
predecessor of given node."""

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = self.parent = None

def postorderPredecessor(root, n):

    # If right child exists, then it
    # is postorder predecessor.
    if (n.right) :
        return n.right

    # If right child does not exist, then
    # travel up (using parent pointers)
    # until we reach a node which is right
    # child of its parent.
    curr = n
    parent = curr.parent
    while (parent != None and
           parent.left == curr):
        curr = curr.parent
        parent = parent.parent

    # If we reached root, then the given
    # node has no postorder predecessor
    if (parent == None) :
        return None

    return parent.left

# Driver Code
if __name__ == '__main__':

    root = newNode(20)
    root.parent = None
    root.left = newNode(10)
    root.left.parent = root
    root.left.left = newNode(4)
    root.left.left.parent = root.left
    root.left.right = newNode(18)
    root.left.right.parent = root.left
    root.right = newNode(26)
    root.right.parent = root
    root.right.left = newNode(24)
    root.right.left.parent = root.right
    root.right.right = newNode(27)
    root.right.right.parent = root.right
    root.left.right.left = newNode(14)
    root.left.right.left.parent = root.left.right
    root.left.right.left.left = newNode(13)
    root.left.right.left.left.parent = root.left.right.left
    root.left.right.left.right = newNode(15)
    root.left.right.left.right.parent = root.left.right.left
    root.left.right.right = newNode(19)
    root.left.right.right.parent = root.left.right

    nodeToCheck = root.left.right

    res = postorderPredecessor(root, nodeToCheck)

    if (res) :
        print("Postorder predecessor of",
               nodeToCheck.key, "is", res.key)

    else:
        print("Postorder predecessor of",
               nodeToCheck.key, "is None")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find postorder
// predecessor of a node
// in Binary Tree.
using System;
class GFG{

class Node
{
  public Node left, right, parent;
  public int key;
};

static Node newNode(int key)
{
  Node temp = new Node();
  temp.left = temp.right =
              temp.parent = null;
  temp.key = key;
  return temp;
}

static Node postorderPredecessor(Node root,
                                 Node n)
{   
  // If right child exists,
  // then it is postorder
  // predecessor.
  if (n.right != null)
    return n.right;

  // If right child does not exist, then
  // travel up (using parent pointers)
  // until we reach a node which is right
  // child of its parent.
  Node curr = n, parent = curr.parent;
  while (parent != null &&
         parent.left == curr)
  {
    curr = curr.parent;
    parent = parent.parent;
  }

  // If we reached root, then the given
  // node has no postorder predecessor
  if (parent == null)
    return null;

  return parent.left;
}

// Driver code
public static void Main(String[] args)
{
  Node root = newNode(20);
  root.parent = null;
  root.left = newNode(10);
  root.left.parent = root;
  root.left.left = newNode(4);
  root.left.left.parent = root.left;
  root.left.right = newNode(18);
  root.left.right.parent = root.left;
  root.right = newNode(26);
  root.right.parent = root;
  root.right.left = newNode(24);
  root.right.left.parent = root.right;
  root.right.right = newNode(27);
  root.right.right.parent = root.right;
  root.left.right.left = newNode(14);
  root.left.right.left.parent = root.left.right;
  root.left.right.left.left = newNode(13);
  root.left.right.left.left.parent = root.left.right.left;
  root.left.right.left.right = newNode(15);
  root.left.right.left.right.parent = root.left.right.left;
  root.left.right.right = newNode(19);
  root.left.right.right.parent = root.left.right;
  Node nodeToCheck = root.left.right;

  Node res = postorderPredecessor(root, nodeToCheck);

  if (res != null)
  {
    Console.Write("Postorder predecessor " +
                  "of {0} is {1}\n",
                  nodeToCheck.key, res.key);
  }
  else
  {
    Console.Write("Postorder predecessor " +
                  "of {0} is null\n",
                  nodeToCheck.key);
  }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to find postorder
// predecessor of a node
// in Binary Tree.

class Node
{
    constructor()
    {
        this.left = null;
        this.right = null;
        this.parent = null;
        this.key = 0;
    }
};

function newNode(key)
{
  var temp = new Node();
  temp.left = temp.right =
              temp.parent = null;
  temp.key = key;
  return temp;
}

function postorderPredecessor(root, n)
{   
  // If right child exists,
  // then it is postorder
  // predecessor.
  if (n.right != null)
    return n.right;

  // If right child does not exist, then
  // travel up (using parent pointers)
  // until we reach a node which is right
  // child of its parent.
  var curr = n, parent = curr.parent;
  while (parent != null &&
         parent.left == curr)
  {
    curr = curr.parent;
    parent = parent.parent;
  }

  // If we reached root, then the given
  // node has no postorder predecessor
  if (parent == null)
    return null;

  return parent.left;
}

// Driver code
var root = newNode(20);
root.parent = null;
root.left = newNode(10);
root.left.parent = root;
root.left.left = newNode(4);
root.left.left.parent = root.left;
root.left.right = newNode(18);
root.left.right.parent = root.left;
root.right = newNode(26);
root.right.parent = root;
root.right.left = newNode(24);
root.right.left.parent = root.right;
root.right.right = newNode(27);
root.right.right.parent = root.right;
root.left.right.left = newNode(14);
root.left.right.left.parent = root.left.right;
root.left.right.left.left = newNode(13);
root.left.right.left.left.parent = root.left.right.left;
root.left.right.left.right = newNode(15);
root.left.right.left.right.parent = root.left.right.left;
root.left.right.right = newNode(19);
root.left.right.right.parent = root.left.right;
var nodeToCheck = root.left.right;
var res = postorderPredecessor(root, nodeToCheck);
if (res != null)
{
  document.write(`Postorder predecessor ` +
                `of ${nodeToCheck.key} is ${res.key}<br>`);
}
else
{
  document.write(`Postorder predecessor ` +
                `of ${nodeToCheck.key} is null<br>`);
}

// This code is contributed by famously.
</script>
```

**Output:** 

```
Postorder predecessor of 18 is 19
```

**时间复杂度:** O(h)其中 h 是给定二叉树的高度
T3】辅助空间: O(1)