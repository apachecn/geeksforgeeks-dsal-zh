# 打印二叉查找树所有奇数节点

> 原文:[https://www . geeksforgeeks . org/print-二进制搜索树的所有奇数节点/](https://www.geeksforgeeks.org/print-all-odd-nodes-of-binary-search-tree/)

给一个二叉查找树。任务是打印二叉查找树的所有奇数节点。
**例** :

```
Input : 
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8 
Output : 3 5 7

Input :
          14 
        /   \ 
       12    17 
      / \   / \ 
     8  13 16   19 
Output : 13 17 19
```

**接近**:使用任意一个[树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历二叉查找树，检查当前节点的值是否为奇数。如果是，则打印，否则跳过该节点。
以下是上述办法的实施情况:

## C++

```
// C++ program to print all odd node of BST
#include <bits/stdc++.h>
using namespace std;

// create Tree
struct Node {
    int key;
    struct Node *left, *right;
};

// A utility function to create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

/* A utility function to insert a new node
   with given key in BST */
Node* insert(Node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to print all odd nodes
void oddNode(Node* root)
{
    if (root != NULL) {
        oddNode(root->left);

        // if node is odd then print it
        if (root->key % 2 != 0)
            printf("%d ", root->key);

        oddNode(root->right);
    }
}

// Driver Code
int main()
{
    /* Let us create following BST 
        5 
      /  \ 
     3    7 
    / \  / \ 
    2 4  6 8 */
    Node* root = NULL;
    root = insert(root, 5);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 4);
    root = insert(root, 7);
    root = insert(root, 6);
    root = insert(root, 8);

    oddNode(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all odd node of BST
class GfG {

// create Tree
static class Node {
    int key;
    Node left, right;
}

// A utility function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to do inorder traversal of BST
static void inorder(Node root)
{
    if (root != null) {
        inorder(root.left);
        System.out.print(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert a new node
with given key in BST */
static Node insert(Node node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to print all odd nodes
static void oddNode(Node root)
{
    if (root != null) {
        oddNode(root.left);

        // if node is odd then print it
        if (root.key % 2 != 0)
            System.out.print(root.key + " ");

        oddNode(root.right);
    }
}

// Driver Code
public static void main(String[] args)
{
    /* Let us create following BST
        5
    / \
    3 7
    / \ / \
    2 4 6 8 */
    Node root = null;
    root = insert(root, 5);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 4);
    root = insert(root, 7);
    root = insert(root, 6);
    root = insert(root, 8);

    oddNode(root);

}
}
```

## 蟒蛇 3

```
# Python3 program to print all odd
# node of BST

# create Tree
# to create a new BST node
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# A utility function to do inorder
# traversal of BST
def inorder( root) :

    if (root != None):
        inorder(root.left)
        print(root.key, end = " ")
        inorder(root.right)

""" A utility function to insert a
new node with given key in BST """
def insert(node, key):

    """ If the tree is empty,
    return a new node """
    if (node == None):
        return newNode(key)

    """ Otherwise, recur down the tree """
    if (key < node.key):
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    """ return the (unchanged) node pointer """
    return node

# Function to print all even nodes
def oddNode(root) :

    if (root != None):
        oddNode(root.left)

        # if node is even then print it
        if (root.key % 2 != 0):
            print(root.key, end = " ")
        oddNode(root.right)

# Driver Code
if __name__ == '__main__':

    """ Let us create following BST
    5
    / \
    3 7
    / \ / \
    2 4 6 8 """
    root = None
    root = insert(root, 5)
    root = insert(root, 3)
    root = insert(root, 2)
    root = insert(root, 4)
    root = insert(root, 7)
    root = insert(root, 6)
    root = insert(root, 8)

    oddNode(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to print all odd node of BST
using System;

public class GfG
{

// create Tree
class Node
{
    public int key;
    public Node left, right;
}

// A utility function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to do
// inorder traversal of BST
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert a new node
with given key in BST */
static Node insert(Node node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to print all odd nodes
static void oddNode(Node root)
{
    if (root != null)
    {
        oddNode(root.left);

        // if node is odd then print it
        if (root.key % 2 != 0)
            Console.Write(root.key + " ");

        oddNode(root.right);
    }
}

// Driver Code
public static void Main(String[] args)
{
    /* Let us create following BST
        5
    / \
    3 7
    / \ / \
    2 4 6 8 */
    Node root = null;
    root = insert(root, 5);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 4);
    root = insert(root, 7);
    root = insert(root, 6);
    root = insert(root, 8);

    oddNode(root);

}
}

// This code has been contributed
// by PrinciRaj1992
```

**Output:** 

```
3 5 7
```

**时间复杂度:** O(n)，其中 n 为二叉查找树的节点数。
***辅助空间** : O(n)*