# 转换一棵二叉树，使得每个节点在其右子树中存储所有节点的总和

> 原文:[https://www . geesforgeks . org/convert-a-二叉树，这样每个节点都在其右子树中存储所有节点的总和/](https://www.geeksforgeeks.org/convert-a-binary-tree-such-that-every-node-stores-the-sum-of-all-nodes-in-its-right-subtree/)

给定一棵二叉树，将每个节点中的值更改为右子树中节点的所有值的总和，包括它自己的值。
**例:**

```
Input : 
     1
   /   \
 2      3
Output : 
    4
  /   \
 2     3

Input : 
       1
      / \
     2   3
    / \   \
   4   5   6
Output :
       10
      / \
     7   9
    / \   \
   4   5   6
```

**逼近**:思路是以**自下而上**的方式遍历给定的二叉树。递归计算左右子树中节点的总和。将右子树中的节点总和累加到当前节点，并返回当前子树下的节点总和。
以下是上述办法的实施情况。

## C++

```
// C++ program to store sum of nodes in
// right subtree in every node
#include <bits/stdc++.h>
using namespace std;

// Node of tree
struct Node {
    int data;
    Node *left, *right;
};

// Function to create a new node
struct Node* createNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// Function to build new tree with
// all nodes having the sum of all
// nodes in its right subtree
int updateBTree(Node* root)
{
    // Base cases
    if (!root)
        return 0;
    if (root->left == NULL && root->right == NULL)
        return root->data;

    // Update right and left subtrees
    int rightsum = updateBTree(root->right);
    int leftsum = updateBTree(root->left);

    // Add rightsum to current node
    root->data += rightsum;

    // Return sum of values under root
    return root->data + leftsum;
}

// Function to traverse tree in inorder way
void inorder(struct Node* node)
{
    if (node == NULL)
        return;
    inorder(node->left);
    cout << node->data << " ";
    inorder(node->right);
}

// Driver code
int main()
{
    /* Let us construct a binary tree
            1
           / \
          2   3
         / \   \
        4   5   6       */
    struct Node* root = NULL;
    root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->right = createNode(6);

    // new tree construction
    updateBTree(root);

    cout << "Inorder traversal of the modified tree is \n";
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to store sum of nodes in
// right subtree in every node
class GFG
{

// Node of tree
static class Node
{
    int data;
    Node left, right;
};

// Function to create a new node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Function to build new tree with
// all nodes having the sum of all
// nodes in its right subtree
static int updateBTree(Node root)
{
    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update right and left subtrees
    int rightsum = updateBTree(root.right);
    int leftsum = updateBTree(root.left);

    // Add rightsum to current node
    root.data += rightsum;

    // Return sum of values under root
    return root.data + leftsum;
}

// Function to traverse tree in inorder way
static void inorder( Node node)
{
    if (node == null)
        return;
    inorder(node.left);
    System.out.print( node.data + " ");
    inorder(node.right);
}

// Driver code
public static void main(String args[])
{
    /* Let us construct a binary tree
        1
        / \
        2 3
        / \ \
        4 5 6 */
    Node root = null;
    root = createNode(1);
    root.left = createNode(2);
    root.right = createNode(3);
    root.left.left = createNode(4);
    root.left.right = createNode(5);
    root.right.right = createNode(6);

    // new tree conion
    updateBTree(root);

    System.out.print( "Inorder traversal of the modified tree is \n");
    inorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Program to convert expression tree
# from prefix expression

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                
class createNode:

    # Conto create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to build new tree with
# all nodes having the sum of all
# nodes in its right subtree
def updateBTree( root):

    # Base cases
    if (not root):
        return 0
    if (root.left == None and
        root.right == None):
        return root.data

    # Update right and left subtrees
    rightsum = updateBTree(root.right)
    leftsum = updateBTree(root.left)

    # Add rightsum to current node
    root.data += rightsum

    # Return sum of values under root
    return root.data + leftsum

# Function to traverse tree in inorder way
def inorder(node):

    if (node == None):
        return
    inorder(node.left)
    print(node.data, end = " ")
    inorder(node.right)

# Driver Code
if __name__ == '__main__':

    """ Let us convert binary tree
        1
    / \
    2 3
    / \ \
    4 5 6 """
    root = None
    root = createNode(1)
    root.left = createNode(2)
    root.right = createNode(3)
    root.left.left = createNode(4)
    root.left.right = createNode(5)
    root.right.right = createNode(6)

    # new tree construction
    updateBTree(root)

    print("Inorder traversal of the",
          "modified tree is")
    inorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to store sum of nodes in
// right subtree in every node
using System;

class GFG
{

// Node of tree
public class Node
{
    public int data;
    public Node left, right;
};

// Function to create a new node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Function to build new tree with
// all nodes having the sum of all
// nodes in its right subtree
static int updateBTree(Node root)
{
    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update right and left subtrees
    int rightsum = updateBTree(root.right);
    int leftsum = updateBTree(root.left);

    // Add rightsum to current node
    root.data += rightsum;

    // Return sum of values under root
    return root.data + leftsum;
}

// Function to traverse tree in inorder way
static void inorder( Node node)
{
    if (node == null)
        return;
    inorder(node.left);
    Console.Write( node.data + " ");
    inorder(node.right);
}

// Driver code
public static void Main(String[] args)
{
    /* Let us construct a binary tree
        1
        / \
        2 3
        / \ \
        4 5 6 */
    Node root = null;
    root = createNode(1);
    root.left = createNode(2);
    root.right = createNode(3);
    root.left.left = createNode(4);
    root.left.right = createNode(5);
    root.right.right = createNode(6);

    // new tree conion
    updateBTree(root);

    Console.Write( "Inorder traversal of the modified tree is \n");
    inorder(root);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to store sum of nodes in
// right subtree in every node

// Node of tree
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to create a new node
function createNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Function to build new tree with
// all nodes having the sum of all
// nodes in its right subtree
function updateBTree(root)
{

    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update right and left subtrees
    var rightsum = updateBTree(root.right);
    var leftsum = updateBTree(root.left);

    // Add rightsum to current node
    root.data += rightsum;

    // Return sum of values under root
    return root.data + leftsum;
}

// Function to traverse tree in inorder way
function inorder(node)
{
    if (node == null)
        return;
    inorder(node.left);
    document.write( node.data + " ");
    inorder(node.right);
}

// Driver code
/* Let us construct a binary tree
    1
    / \
    2 3
    / \ \
    4 5 6 */
var root = null;
root = createNode(1);
root.left = createNode(2);
root.right = createNode(3);
root.left.left = createNode(4);
root.left.right = createNode(5);
root.right.right = createNode(6);

// new tree conion
updateBTree(root);
document.write( "Inorder traversal of the modified tree is <br>");
inorder(root);

// This code is contributed by famously.
</script>
```

**Output:** 

```
Inorder traversal of the modified tree is 
4 7 5 10 9 6
```

**时间复杂度** : O(n)