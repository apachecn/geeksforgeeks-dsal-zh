# 获取二叉树中最大左节点

> 原文:[https://www . geesforgeks . org/get-maximum-left-node-二叉树/](https://www.geeksforgeeks.org/get-maximum-left-node-binary-tree/)

给定一棵树，任务是在二叉树的唯一左边节点中找到最大值。
**例:**

```
Input : 
           7
         /    \
        6       5
       / \     / \
      4  3     2  1 
Output :
6

Input :
            1
         /    \
        2       3
       /       / \
      4       5   6
        \    /  \ 
         7  8   9 
Output :
8
```

按顺序遍历，只对左节点应用条件，得到左节点的最大值。
我们试着用代码来理解。

## C++

```
// CPP program to print maximum element
// in left node.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Get max of left element using
// Inorder traversal
int maxOfLeftElement(Node* root)
{
    int res = INT_MIN;
    if (root == NULL)
        return res;

    if (root->left != NULL)
        res = root->left->data;

    // Return maximum of three values
    // 1) Recursive max in left subtree
    // 2) Value in left node
    // 3) Recursive max in right subtree
    return max({ maxOfLeftElement(root->left),
                 res,
                 maxOfLeftElement(root->right) });
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in above diagram
    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    /*     7
         /    \
        6       5
       / \     / \
      4  3     2  1          */
    cout << maxOfLeftElement(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print maximum element
// in left node.
import java.util.*;
class GfG {

// A Binary Tree Node
static class Node {
    int data;
    Node left, right;
}

// Get max of left element using
// Inorder traversal
static int maxOfLeftElement(Node root)
{
    int res = Integer.MIN_VALUE;
    if (root == null)
        return res;

    if (root.left != null)
        res = root.left.data;

    // Return maximum of three values
    // 1) Recursive max in left subtree
    // 2) Value in left node
    // 3) Recursive max in right subtree
    return Math.max(maxOfLeftElement(root.left),
       Math.max(res, maxOfLeftElement(root.right)));
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver program to test above functions
public static void main(String[] args)
{
    // Let us create binary tree shown in above diagram
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /* 7
        / \
        6 5
    / \ / \
    4 3 2 1         */
    System.out.println(maxOfLeftElement(root));
}
}
```

## 蟒蛇 3

```
# Python program to prmaximum element
# in left node.

# Utility class to create a
# new tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Get max of left element using
# Inorder traversal
def maxOfLeftElement(root):
    res = -999999999999
    if (root == None):
        return res

    if (root.left != None):
        res = root.left.data

    # Return maximum of three values
    # 1) Recursive max in left subtree
    # 2) Value in left node
    # 3) Recursive max in right subtree
    return max({ maxOfLeftElement(root.left), res,
                 maxOfLeftElement(root.right) })

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree shown
    # in above diagram
    root = newNode(7)
    root.left = newNode(6)
    root.right = newNode(5)
    root.left.left = newNode(4)
    root.left.right = newNode(3)
    root.right.left = newNode(2)
    root.right.right = newNode(1)

    #     7
    #     / \
    # 6     5
    # / \     / \
    # 4 3     2 1        
    print(maxOfLeftElement(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to print maximum element
// in left node.
using System;

class GfG
{

    // A Binary Tree Node
    class Node
    {
        public int data;
        public Node left, right;
    }

    // Get max of left element using
    // Inorder traversal
    static int maxOfLeftElement(Node root)
    {
        int res = int.MinValue;
        if (root == null)
            return res;

        if (root.left != null)
            res = root.left.data;

        // Return maximum of three values
        // 1) Recursive max in left subtree
        // 2) Value in left node
        // 3) Recursive max in right subtree
        return Math.Max(maxOfLeftElement(root.left),
        Math.Max(res, maxOfLeftElement(root.right)));
    }

    // Utility function to create a new tree node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Let us create binary tree
        // shown in above diagram
        Node root = newNode(7);
        root.left = newNode(6);
        root.right = newNode(5);
        root.left.left = newNode(4);
        root.left.right = newNode(3);
        root.right.left = newNode(2);
        root.right.right = newNode(1);

        /* 7
            / \
            6 5
        / \ / \
        4 3 2 1         */
        Console.WriteLine(maxOfLeftElement(root));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to print maximum element
// in left node.
// A Binary Tree Node
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
}
// Get max of left element using
// Inorder traversal
function maxOfLeftElement(root)
{
    var res = -1000000000;
    if (root == null)
        return res;
    if (root.left != null)
        res = root.left.data;
    // Return maximum of three values
    // 1) Recursive max in left subtree
    // 2) Value in left node
    // 3) Recursive max in right subtree
    return Math.max(maxOfLeftElement(root.left),
    Math.max(res, maxOfLeftElement(root.right)));
}
// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}
// Driver code
// Let us create binary tree
// shown in above diagram
var root = newNode(7);
root.left = newNode(6);
root.right = newNode(5);
root.left.left = newNode(4);
root.left.right = newNode(3);
root.right.left = newNode(2);
root.right.right = newNode(1);
/* 7
    / \
    6 5
/ \ / \
4 3 2 1         */
document.write(maxOfLeftElement(root));

</script>
```

**Output:** 

```
6
```