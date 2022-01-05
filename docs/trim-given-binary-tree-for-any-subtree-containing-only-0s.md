# 为任何只包含 0 的子树修剪给定的二叉树

> 原文:[https://www . geesforgeks . org/trim-given-二叉树-for-any-subtree-only-contained-0s/](https://www.geeksforgeeks.org/trim-given-binary-tree-for-any-subtree-containing-only-0s/)

给定一棵 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是为任何只包含 0 的子树修剪这棵树。

**示例:**

```
Input:
             1  
              \
               0
              / \
             0   1

Output: 
             1  
              \
               0
                \
                 1    
Explanation: 
The subtree shown as bold below 
does not contain any 1\. 
Hence it can be trimmed.
             1  
              \
               0
              / \
             0   1

Input: 
               1  
             /   \
            1     0
           / \   / \
          1   1 0   1
         /
        0
Output:
             1  
           /   \
          1     0
         / \     \
        1   1     1

Input: 
              1  
            /   \
           0     1
          / \   / \
         0   0 0   1
Output:
            1  
              \
                1
                  \
                   1
```

**方法:**给定的问题可以使用 [**后序遍历**](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) 来解决。其思想是，如果左右子树都为空，并且当前节点的值为 0，则将空节点返回给父节点。这将删除甚至不包含单个 1 的子树。按照以下步骤解决问题:

*   如果根为空，我们只需返回空。
*   在左右子树上递归调用该函数
*   如果左子树和右子树返回 null，并且当前节点的值为 0，则返回 null
*   否则返回当前节点本身

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <iostream>
using namespace std;

class TreeNode {

public:
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val)
    {
        data = val;
        left = NULL;
        right = NULL;
    }
};

// Inorder function to print the tree
void inorderPrint(TreeNode* root)
{
    if (root == NULL)
        return;
    inorderPrint(root->left);
    cout << root->data << " ";
    inorderPrint(root->right);
}

// Postorder traversal
TreeNode* TrimTree(TreeNode* root)
{
    if (!root)
        return nullptr;

    // Traverse from leaf to node
    root->left = TrimTree(root->left);
    root->right = TrimTree(root->right);

    // We only trim if the node's value is 0
    // and children are null
    if (root->data == 0 && root->left == nullptr
        && root->right == nullptr) {

        // We trim the subtree by returning nullptr
        return nullptr;
    }

    // Otherwise we leave the node the way it is
    return root;
}

// Driver code
int main()
{
    /*
           1
         /   \
       0      1
      / \    /  \
    0    0  0    1
    */

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(0);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(0);
    root->left->right = new TreeNode(0);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(1);

    TreeNode* ReceivedRoot = TrimTree(root);
    cout << endl;
    inorderPrint(ReceivedRoot);
    /*
              1
                \
                  1
                    \
                     1
    */
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

static class TreeNode {

    int data;
    TreeNode left;
    TreeNode right;
    TreeNode(int val)
    {
        data = val;
        left = null;
        right = null;
    }
};

// Inorder function to print the tree
static void inorderPrint(TreeNode root)
{
    if (root == null)
        return;
    inorderPrint(root.left);
    System.out.print(root.data+ " ");
    inorderPrint(root.right);
}

// Postorder traversal
static TreeNode TrimTree(TreeNode root)
{
    if (root==null)
        return null;

    // Traverse from leaf to node
    root.left = TrimTree(root.left);
    root.right = TrimTree(root.right);

    // We only trim if the node's value is 0
    // and children are null
    if (root.data == 0 && root.left == null
        && root.right == null) {

        // We trim the subtree by returning null
        return null;
    }

    // Otherwise we leave the node the way it is
    return root;
}

// Driver code
public static void main(String[] args)
{
    /*
           1
         /   \
       0      1
      / \    /  \
    0    0  0    1
    */

    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(0);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(0);
    root.left.right = new TreeNode(0);
    root.right.left = new TreeNode(0);
    root.right.right = new TreeNode(1);

    TreeNode ReceivedRoot = TrimTree(root);
    System.out.println();
    inorderPrint(ReceivedRoot);
    /*
              1
                \
                  1
                    \
                     1
    */
}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program for above approach
using System;
public class GFG{

class TreeNode {

    public int data;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int val)
    {
        data = val;
        left = null;
        right = null;
    }
};

// Inorder function to print the tree
static void inorderPrint(TreeNode root)
{
    if (root == null)
        return;
    inorderPrint(root.left);
    Console.Write(root.data+ " ");
    inorderPrint(root.right);
}

// Postorder traversal
static TreeNode TrimTree(TreeNode root)
{
    if (root==null)
        return null;

    // Traverse from leaf to node
    root.left = TrimTree(root.left);
    root.right = TrimTree(root.right);

    // We only trim if the node's value is 0
    // and children are null
    if (root.data == 0 && root.left == null
        && root.right == null) {

        // We trim the subtree by returning null
        return null;
    }

    // Otherwise we leave the node the way it is
    return root;
}

// Driver code
public static void Main(String[] args)
{
    /*
           1
         /   \
       0      1
      / \    /  \
    0    0  0    1
    */

    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(0);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(0);
    root.left.right = new TreeNode(0);
    root.right.left = new TreeNode(0);
    root.right.right = new TreeNode(1);

    TreeNode ReceivedRoot = TrimTree(root);
    Console.WriteLine();
    inorderPrint(ReceivedRoot);
    /*
              1
                \
                  1
                    \
                     1
    */
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// JavaScript Program to implement
// the above approach

class TreeNode {

    constructor( val)
    {
        this.data = val;
        this.left = null;
        this.right = null;
    }
};

// Inorder function to print the tree
function inorderPrint( root)
{
    if (root == null)
        return;
    inorderPrint(root.left);
    document.write(root.data + " ");
    inorderPrint(root.right);
}

// Postorder traversal
function TrimTree( root)
{
    if (!root)
        return null;

    // Traverse from leaf to node
    root.left = TrimTree(root.left);
    root.right = TrimTree(root.right);

    // We only trim if the node's value is 0
    // and children are null
    if (root.data == 0 && root.left == null
        && root.right == null) {

        // We trim the subtree by returning nullptr
        return null;
    }

    // Otherwise we leave the node the way it is
    return root;
}

// Driver code

    /*
           1
         /   \
       0      1
      / \    /  \
    0    0  0    1
    */

    let root = new TreeNode(1);
    root.left = new TreeNode(0);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(0);
    root.left.right = new TreeNode(0);
    root.right.left = new TreeNode(0);
    root.right.right = new TreeNode(1);

    let ReceivedRoot = TrimTree(root);
    document.write('<br>')
    inorderPrint(ReceivedRoot);
    /*
              1
                \
                  1
                    \
                     1
    */

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
1 1 1
```

**时间复杂度:** O(N)，其中 N 为树中节点数。
**辅助空间:** O(H)，递归调用栈可以和树的高度 H 一样大。在**最坏的情况**下，当树**倾斜时，H = N。**