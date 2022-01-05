# 将二叉树的左右表示转换为右下

> 原文:[https://www . geesforgeks . org/convert-left-right-presentation-bianry-tree-right/](https://www.geeksforgeeks.org/convert-left-right-representation-bianry-tree-right/)

**二叉树的左右表示**是标准表示，其中每个节点都有一个指向左子节点的指针和另一个指向右子节点的指针。
**右下表示法**是一种替代表示法，其中每个节点都有一个指向左(或第一)子节点的指针和另一个指向下一个兄弟节点的指针。所以每一层的兄弟姐妹都是从左到右相连的。
给定一个二叉树的左右表示如下

```
                               1
                    /    \
                   2      3
                   /    \
                   4      5
                     /     /   \
                    6    7      8 
```

将树的结构转换为右下表示，如下图所示。

```
            1
            |
            2 – 3
                |
                4 — 5
                |   |
                6   7 – 8 
```

转换应该就地进行，即左子指针应该用作向下指针，右子指针应该用作右同级指针。
**我们强烈建议尽量减少你的浏览器，自己试试这个。**
思路是先转换左右子，再转换根。下面是 C++实现的思路。

## C++

```
/* C++ program to convert left-right to down-right
   representation of binary tree */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct node
{
    int key;
    struct node *left, *right;
};

// An Iterative level order traversal based function to
// convert left-right to down-right representation.
void convert(node *root)
{
    // Base Case
    if (root == NULL)  return;

    // Recursively convert left an right subtrees
    convert(root->left);
    convert(root->right);

    // If left child is NULL, make right child as left
    // as it is the first child.
    if (root->left == NULL)
       root->left = root->right;

    // If left child is NOT NULL, then make right child
    // as right of left child
    else
       root->left->right = root->right;

    // Set root's right as NULL
    root->right = NULL;
}

// A utility function to traverse a tree stored in
// down-right form.
void downRightTraversal(node *root)
{
    if (root != NULL)
    {
        cout << root->key << " ";
        downRightTraversal(root->right);
        downRightTraversal(root->left);
    }
}

// Utility function to create a new tree node
node* newNode(int key)
{
    node *temp = new node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in above diagram
    /*
           1
         /   \
        2     3
             / \
            4   5
           /   /  \
          6   7    8
    */
    node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->right->left = newNode(4);
    root->right->right = newNode(5);
    root->right->left->left = newNode(6);
    root->right->right->left = newNode(7);
    root->right->right->right = newNode(8);

    convert(root);

    cout << "Traversal of the tree converted to down-right form\n";
    downRightTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to convert left-right to
down-right representation of binary tree */
class GFG
{

// A Binary Tree Node
static class node
{
    int key;
    node left, right;
    node(int key)
    {
        this.key = key;
        this.left = null;
        this.right = null;
    }
}

// An Iterative level order traversal
// based function to convert left-right
// to down-right representation.
static void convert(node root)
{
    // Base Case
    if (root == null) return;

    // Recursively convert left
    // an right subtrees
    convert(root.left);
    convert(root.right);

    // If left child is NULL, make right
    // child as left as it is the first child.
    if (root.left == null)
    root.left = root.right;

    // If left child is NOT NULL, then make
    // right child as right of left child
    else
    root.left.right = root.right;

    // Set root's right as NULL
    root.right = null;
}

// A utility function to traverse a
// tree stored in down-right form.
static void downRightTraversal(node root)
{
    if (root != null)
    {
        System.out.print(root.key + " ");
        downRightTraversal(root.right);
        downRightTraversal(root.left);
    }
}

// Utility function to create
// a new tree node
static node newNode(int key)
{
    node temp = new node(0);
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver Code
public static void main(String[] args)
{
    // Let us create binary tree
    // shown in above diagram
    /*
        1
        / \
        2 3
            / \
            4 5
        / / \
        6 7 8
    */
    node root = new node(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.right.left = newNode(4);
    root.right.right = newNode(5);
    root.right.left.left = newNode(6);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(8);

    convert(root);

    System.out.println("Traversal of the tree " +
                 "converted to down-right form");
    downRightTraversal(root);
}
}

// This code is contributed
// by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to convert left-right to
# down-right representation of binary tree

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# An Iterative level order traversal based
# function to convert left-right to down-right
# representation.
def convert(root):

    # Base Case
    if (root == None):
        return

    # Recursively convert left an
    # right subtrees
    convert(root.left)
    convert(root.right)

    # If left child is None, make right
    # child as left as it is the first child.
    if (root.left == None):
        root.left = root.right

    # If left child is NOT None, then make
    # right child as right of left child
    else:
        root.left.right = root.right

    # Set root's right as None
    root.right = None

# A utility function to traverse a
# tree stored in down-right form.
def downRightTraversal(root):

    if (root != None):

        print( root.key, end = " ")
        downRightTraversal(root.right)
        downRightTraversal(root.left)

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree shown
    # in above diagram
    """
        1
        / \
        2     3
            / \
            4 5
        / / \
        6 7 8
    """
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.right.left = newNode(4)
    root.right.right = newNode(5)
    root.right.left.left = newNode(6)
    root.right.right.left = newNode(7)
    root.right.right.right = newNode(8)

    convert(root)

    print("Traversal of the tree converted",
                       "to down-right form")
    downRightTraversal(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to convert left-right to
// down-right representation of binary tree
using System;

class GFG
{

// A Binary Tree Node
public class node
{
    public int key;
    public node left, right;
    public node(int key)
    {
        this.key = key;
        this.left = null;
        this.right = null;
    }
}

// An Iterative level order traversal
// based function to convert left-right
// to down-right representation.
public static void convert(node root)
{
    // Base Case
    if (root == null)
    {
        return;
    }

    // Recursively convert left
    // an right subtrees
    convert(root.left);
    convert(root.right);

    // If left child is NULL, make right
    // child as left as it is the first child.
    if (root.left == null)
    {
        root.left = root.right;
    }

    // If left child is NOT NULL, then make
    // right child as right of left child
    else
    {
        root.left.right = root.right;
    }

    // Set root's right as NULL
    root.right = null;
}

// A utility function to traverse a
// tree stored in down-right form.
public static void downRightTraversal(node root)
{
    if (root != null)
    {
        Console.Write(root.key + " ");
        downRightTraversal(root.right);
        downRightTraversal(root.left);
    }
}

// Utility function to create
// a new tree node
public static node newNode(int key)
{
    node temp = new node(0);
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver Code
public static void Main(string[] args)
{
    // Let us create binary tree
    // shown in above diagram
    /*
        1
        / \
        2 3
            / \
            4 5
        / / \
        6 7 8
    */
    node root = new node(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.right.left = newNode(4);
    root.right.right = newNode(5);
    root.right.left.left = newNode(6);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(8);

    convert(root);

    Console.WriteLine("Traversal of the tree " +
                      "converted to down-right form");
    downRightTraversal(root);
}
}

// This code is contributed
// by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to convert left-right to
// down-right representation of binary tree

// A Binary Tree Node
class node
{
  constructor(key)
  {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}

// An Iterative level order traversal
// based function to convert left-right
// to down-right representation.
function convert(root)
{
    // Base Case
    if (root == null)
    {
        return;
    }

    // Recursively convert left
    // an right subtrees
    convert(root.left);
    convert(root.right);

    // If left child is NULL, make right
    // child as left as it is the first child.
    if (root.left == null)
    {
        root.left = root.right;
    }

    // If left child is NOT NULL, then make
    // right child as right of left child
    else
    {
        root.left.right = root.right;
    }

    // Set root's right as NULL
    root.right = null;
}

// A utility function to traverse a
// tree stored in down-right form.
function downRightTraversal(root)
{
    if (root != null)
    {
        document.write(root.key + " ");
        downRightTraversal(root.right);
        downRightTraversal(root.left);
    }
}

// Utility function to create
// a new tree node
function newNode(key)
{
    var temp = new node(0);
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver Code
// Let us create binary tree
// shown in above diagram
/*
    1
    / \
    2 3
        / \
        4 5
    / / \
    6 7 8
*/
var root = new node(1);
root.left = newNode(2);
root.right = newNode(3);
root.right.left = newNode(4);
root.right.right = newNode(5);
root.right.left.left = newNode(6);
root.right.right.left = newNode(7);
root.right.right.right = newNode(8);
convert(root);
document.write("Traversal of the tree " +
                  "converted to down-right form<br>");
downRightTraversal(root);

</script>
```

**输出:**

```
Traversal of the tree converted to down-right form
1 2 3 4 5 7 8 6
```

上述程序的时间复杂度为 O(n)。

本文由 **Abhishek** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。