# 从两个给定的二叉树构建最大二叉树

> 原文:[https://www . geeksforgeeks . org/construct-a-max-二叉树-from-two-给定的二叉树/](https://www.geeksforgeeks.org/construct-a-maximum-binary-tree-from-two-given-binary-trees/)

给定两个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是从两个给定的二叉树创建一个**最大二叉树**，并打印该树的[有序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

**什么是最大二叉树？**

> **最大二进制**以如下方式构造:
> 在两个二叉树都具有两个对应节点的情况下，这两个值的最大值被认为是最大二叉树的节点值。
> 如果两个节点中的任何一个为*空*，并且如果另一个节点不为空，则在最大二叉树的该节点上插入该值。

**示例:**

```
Input:
Tree 1                Tree 2
   3                    5 
  / \                  / \
 2   6                1   8 
/                      \   \ 
20                      2   8 
Output: 20 2 2 5 8 8
Explanation:
          5
         / \
        2   8
       / \   \
      20   2   8

To construct the required Binary Tree,
Root Node value: Max(3, 5) = 5
Root->left value: Max(2, 1) = 2
Root->right value: Max(6, 8) = 8
Root->left->left value: 20
Root->left->right value: 2
Root->right->right value: 8

Input:
       Tree 1            Tree 2 
         9                 5
        / \               / \
       2   6             1   8
      / \                 \   \
     20  3                 2   8
Output:  20 2 3 9 8 8
Explanation:
          9
         / \
        2   8
       / \   \
      20  3   8
```

**方法:**
按照下面给出的步骤解决问题:

*   使用 [**前序遍历**](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) 遍历两棵树。
*   如果两个节点都为**空**，返回。否则，检查以下情况:
    *   如果两个节点都不是**空**，那么将它们之间的**最大值**存储为**最大二叉树**的节点值。
    *   如果只有一个节点为**空**，则将**非空**节点的值存储为**最大二叉树**的节点值。
*   递归遍历左子树。
*   递归遍历右子树
*   最后，返回**最大二叉树**的**根**。

下面是上述方法的实现:

## C++

```
// C++ program to find the Maximum
// Binary Tree from two Binary Trees
#include<bits/stdc++.h>
using namespace std;

// A binary tree node has data,
// pointer to left child
// and a pointer to right child
class Node{

public:
int data;
Node *left, *right;

Node(int data, Node *left,
               Node *right)
{
    this->data = data;
    this->left = left;
    this->right = right;
}
};

// Helper method that allocates
// a new node with the given data
// and NULL left and right pointers.
Node* newNode(int data)
{
    Node *tmp = new Node(data, NULL, NULL);
    return tmp;
}

// Given a binary tree, print
// its nodes in inorder
void inorder(Node *node)
{
    if (node == NULL)
        return;

    // First recur on left child
    inorder(node->left);

    // Then print the data of node
    cout << node->data << " ";

    // Now recur on right child
    inorder(node->right);
}

// Method to find the maximum
// binary tree from two binary trees
Node* MaximumBinaryTree(Node *t1, Node *t2)
{
    if (t1 == NULL)
        return t2;
    if (t2 == NULL)
        return t1;

    t1->data = max(t1->data, t2->data);
    t1->left = MaximumBinaryTree(t1->left,
                                 t2->left);
    t1->right = MaximumBinaryTree(t1->right,
                                  t2->right);
    return t1;
}

// Driver Code
int main()
{

    /* First Binary Tree
             3
            / \
           2   6
         /
        20
    */

    Node *root1 = newNode(3);
    root1->left = newNode(2);
    root1->right = newNode(6);
    root1->left->left = newNode(20);

    /* Second Binary Tree
            5
           / \
          1   8
           \   \
            2   8
            */
    Node *root2 = newNode(5);
    root2->left = newNode(1);
    root2->right = newNode(8);
    root2->left->right = newNode(2);
    root2->right->right = newNode(8);

    Node *root3 = MaximumBinaryTree(root1, root2);
    inorder(root3);
}

// This code is contributed by pratham76
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Maximum
// Binary Tree from two Binary Trees

/* A binary tree node has data,
 pointer to left child
and a pointer to right child */
class Node {
    int data;
    Node left, right;

    public Node(int data, Node left,
                Node right)
    {
        this.data = data;
        this.left = left;
        this.right = right;
    }

    /* Helper method that allocates
       a new node with the given data
       and NULL left and right pointers. */
    static Node newNode(int data)
    {
        return new Node(data, null, null);
    }

    /* Given a binary tree, print
       its nodes in inorder*/
    static void inorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        inorder(node.left);

        /* then print the data of node */
        System.out.printf("%d ", node.data);

        /* now recur on right child */
        inorder(node.right);
    }

    /* Method to find the maximum
       binary tree from
       two binary trees*/
    static Node MaximumBinaryTree(Node t1, Node t2)
    {
        if (t1 == null)
            return t2;
        if (t2 == null)
            return t1;
        t1.data = Math.max(t1.data, t2.data);
        t1.left = MaximumBinaryTree(t1.left,
                                    t2.left);
        t1.right = MaximumBinaryTree(t1.right,
                                     t2.right);
        return t1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        /* First Binary Tree
                 3
                / \
               2   6
              /
             20
        */

        Node root1 = newNode(3);
        root1.left = newNode(2);
        root1.right = newNode(6);
        root1.left.left = newNode(20);

        /* Second Binary Tree
                 5
                / \
                1  8
                \   \
                  2   8
                  */
        Node root2 = newNode(5);
        root2.left = newNode(1);
        root2.right = newNode(8);
        root2.left.right = newNode(2);
        root2.right.right = newNode(8);

        Node root3
            = MaximumBinaryTree(root1, root2);
        inorder(root3);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the Maximum
# Binary Tree from two Binary Trees

''' A binary tree node has data,
 pointer to left child
and a pointer to right child '''
class Node:

    def __init__(self, data, left, right):

        self.data = data
        self.left = left
        self.right = right

''' Helper method that allocates
   a new node with the given data
   and None left and right pointers. '''
def newNode(data):

    return Node(data, None, None);

''' Given a binary tree, print
   its nodes in inorder'''
def inorder(node):

    if (node == None):
        return;

    ''' first recur on left child '''
    inorder(node.left);

    ''' then print the data of node '''
    print(node.data, end=' ');

    ''' now recur on right child '''
    inorder(node.right);

''' Method to find the maximum
   binary tree from
   two binary trees'''
def MaximumBinaryTree(t1, t2):

    if (t1 == None):
        return t2;
    if (t2 == None):
        return t1;
    t1.data = max(t1.data, t2.data);
    t1.left = MaximumBinaryTree(t1.left,
                                t2.left);
    t1.right = MaximumBinaryTree(t1.right,
                                 t2.right);
    return t1;

# Driver Code
if __name__=='__main__':

    ''' First Binary Tree
             3
            / \
           2   6
          /
         20
    '''

    root1 = newNode(3);
    root1.left = newNode(2);
    root1.right = newNode(6);
    root1.left.left = newNode(20);

    ''' Second Binary Tree
             5
            / \
            1  8
            \   \
              2   8
              '''
    root2 = newNode(5);
    root2.left = newNode(1);
    root2.right = newNode(8);
    root2.left.right = newNode(2);
    root2.right.right = newNode(8);

    root3 = MaximumBinaryTree(root1, root2);
    inorder(root3);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the Maximum
// Binary Tree from two Binary Trees
using System;

// A binary tree node has data,
// pointer to left child
// and a pointer to right child
class Node{

public int data;
public Node left, right;

public Node(int data, Node left,
                      Node right)
{
    this.data = data;
    this.left = left;
    this.right = right;
}

// Helper method that allocates
// a new node with the given data
// and NULL left and right pointers.
static Node newNode(int data)
{
    return new Node(data, null, null);
}

// Given a binary tree, print
// its nodes in inorder
static void inorder(Node node)
{
    if (node == null)
        return;

    // first recur on left child
    inorder(node.left);

    // then print the data of node
    Console.Write("{0} ", node.data);

    // now recur on right child
    inorder(node.right);
}

// Method to find the maximum
// binary tree from
// two binary trees
static Node MaximumBinaryTree(Node t1, Node t2)
{
    if (t1 == null)
        return t2;
    if (t2 == null)
        return t1;

    t1.data = Math.Max(t1.data, t2.data);
    t1.left = MaximumBinaryTree(t1.left,
                                t2.left);
    t1.right = MaximumBinaryTree(t1.right,
                                 t2.right);
    return t1;
}

// Driver Code
public static void Main(String[] args)
{

    /* First Binary Tree
             3
            / \
           2   6
         /
        20
    */

    Node root1 = newNode(3);
    root1.left = newNode(2);
    root1.right = newNode(6);
    root1.left.left = newNode(20);

    /* Second Binary Tree
            5
           / \
          1   8
           \   \
            2   8
            */
    Node root2 = newNode(5);
    root2.left = newNode(1);
    root2.right = newNode(8);
    root2.left.right = newNode(2);
    root2.right.right = newNode(8);

    Node root3 = MaximumBinaryTree(root1, root2);
    inorder(root3);
}
}

// This code is contributed by Amal Kumar Choubey
```

## java 描述语言

```
<script>

// Javascript program to find the Maximum
// Binary Tree from two Binary Trees

// A binary tree node has data,
// pointer to left child
// and a pointer to right child
class Node{

    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Helper method that allocates
// a new node with the given data
// and NULL left and right pointers.
function newNode(data)
{
    return new Node(data, null, null);
}

// Given a binary tree, print
// its nodes in inorder
function inorder(node)
{
    if (node == null)
        return;

    // first recur on left child
    inorder(node.left);

    // then print the data of node
    document.write(node.data + " ");

    // now recur on right child
    inorder(node.right);
}

// Method to find the maximum
// binary tree from
// two binary trees
function MaximumBinaryTree(t1, t2)
{
    if (t1 == null)
        return t2;
    if (t2 == null)
        return t1;

    t1.data = Math.max(t1.data, t2.data);
    t1.left = MaximumBinaryTree(t1.left,
                                t2.left);
    t1.right = MaximumBinaryTree(t1.right,
                                 t2.right);
    return t1;
}

// Driver Code

/* First Binary Tree
         3
        / \
       2   6
     /
    20
*/
var root1 = newNode(3);
root1.left = newNode(2);
root1.right = newNode(6);
root1.left.left = newNode(20);
/* Second Binary Tree
        5
       / \
      1   8
       \   \
        2   8
        */
var root2 = newNode(5);
root2.left = newNode(1);
root2.right = newNode(8);
root2.left.right = newNode(2);
root2.right.right = newNode(8);
var root3 = MaximumBinaryTree(root1, root2);
inorder(root3);

</script>
```

**Output:** 

```
20 2 2 5 8 8
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*