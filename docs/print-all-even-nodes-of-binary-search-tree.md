# 打印二叉查找树所有偶数节点

> 原文:[https://www . geesforgeks . org/print-all-even-nodes-of-binary-search-tree/](https://www.geeksforgeeks.org/print-all-even-nodes-of-binary-search-tree/)

给一个二叉查找树。任务是打印二叉查找树的所有偶数节点。
**例:**

```
Input : 
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8 
Output : 2 4 6 8

Input :
          14 
        /   \ 
       12    17 
      / \   / \ 
     8  13 16   19 
Output : 8 12 14 16
```

**方法:**遍历二叉查找树，检查当前节点的值是否为偶数。如果是，则打印，否则跳过该节点。
以下是上述办法的实施情况:

## C++

```
// C++ program to print all even node of BST
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
        printf(root->key,end=" ");
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

// Function to print all even nodes
void evenNode(Node* root)
{
    if (root != NULL) {
        evenNode(root->left);
        // if node is even then print it
        if (root->key % 2 == 0)
            printf("%d ", root->key);
        evenNode(root->right);
    }
}

// Driver Code
int main()
{
    /* Let us create following BST
       5
      / \
     3     7
    / \ / \
    2 4 6 8 */
    Node* root = NULL;
    root = insert(root, 5);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 4);
    root = insert(root, 7);
    root = insert(root, 6);
    root = insert(root, 8);

    evenNode(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all even node of BST
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

// Function to print all even nodes
static void evenNode(Node root)
{
    if (root != null) {
        evenNode(root.left);
        // if node is even then print it
        if (root.key % 2 == 0)
            System.out.print(root.key + " ");
        evenNode(root.right);
    }
}

// Driver Code
public static void main(String[] args)
{
    /* Let us create following BST
    5
    / \
    3     7
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

    evenNode(root);

}
}
```

## 蟒蛇 3

```
# Python3 program to print all even node of BST

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
def inorder(root) :

    if (root != None):
        inorder(root.left)
        printf("%d ", root.key)
        inorder(root.right)

""" A utility function to insert a new
node with given key in BST """
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

    """ return the (unchanged)
        node pointer """
    return node

# Function to print all even nodes
def evenNode(root) :

    if (root != None):
        evenNode(root.left)

        # if node is even then print it
        if (root.key % 2 == 0):
            print(root.key, end = " ")
        evenNode(root.right)

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

    evenNode(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to print all even node of BST
using System;

class GfG
{

    // create Tree
    class Node
    {
        public int key;
        public Node left, right;
    }

    // A utility function to
    // create a new BST node
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

    // Function to print all even nodes
    static void evenNode(Node root)
    {
        if (root != null)
        {
            evenNode(root.left);

            // if node is even then print it
            if (root.key % 2 == 0)
                Console.Write(root.key + " ");
            evenNode(root.right);
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

        evenNode(root);
    }
}

// This code has been contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to print all even node of BST

// create Tree
     class Node {
            constructor() {
                this.key = 0;
                this.left = null;
                this.right = null;
            }
        }

// A utility function to create a new BST node
function newNode(item)
{
    var temp = new Node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to do inorder traversal of BST
function inorder(root)
{
    if (root != null) {
        inorder(root.left);
        document.write(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert a new node
with given key in BST */
function insert(node , key)
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

// Function to print all even nodes
function evenNode(root)
{
    if (root != null) {
        evenNode(root.left);
        // if node is even then print it
        if (root.key % 2 == 0)
            document.write(root.key + " ");
        evenNode(root.right);
    }
}

// Driver Code
    /* Let us create following BST
    5
    / \
    3     7
    / \ / \
    2 4 6 8 */
    var root = null;
    root = insert(root, 5);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 4);
    root = insert(root, 7);
    root = insert(root, 6);
    root = insert(root, 8);

    evenNode(root);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
2 4 6 8
```