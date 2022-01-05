# 将给定的二叉树转换为持有逻辑或属性的树

> 原文:[https://www . geeksforgeeks . org/convert-a-给定-二叉树-a-tree-a-hold-logic-or-property/](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-a-tree-that-holds-logical-or-property/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)(每个节点最多有 2 个子节点)，其中每个节点都有值 **0** 或 **1** 。任务是将给定的二叉树转换为持有逻辑或属性的树，即每个节点值应该是其子节点之间的逻辑或。

**示例:**

```
Input: 
       1
     /   \
    1      0
  /  \    /  \
 0    1  1    1

Output: 0 1 1 1 1 1 1
```

```
Explanation: 
Given Tree
       1
     /   \
    1      0
  /  \    /  \
 0    1  1    1

After Processing
       1
     /   \
    1      1
  /  \    /  \
 0    1  1    1
```

**方法:**
想法是以[后序方式](https://www.geeksforgeeks.org/print-postorder-from-given-inorder-and-preorder-traversals/)遍历给定的二叉树，因为在后序遍历中，根的两个子树都已经在根本身之前被访问过。
对于每个节点，检查(递归地)如果节点有一个子节点，那么我们不需要检查其他任何东西，如果节点有它的两个子节点，那么简单地用它的子数据的逻辑或更新节点数据。

下面是上述方法的实现:

## C++

```
// C++ code to convert a
// given binary tree to
// a tree that holds
// logical OR property.
#include <bits/stdc++.h>
using namespace std;

// Structure of the binary tree
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to create a new node
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->data = key;
    node->left = node->right = NULL;
    return node;
}

// Convert the given tree to a
// tree where each node is logical
// OR of its children The main idea
// is to do Postorder traversal
void convertTree(Node* root)
{
    if (root == NULL)
        return;

    // First recur on left child
    convertTree(root->left);

    // Then recur on right child
    convertTree(root->right);

    if (root->left != NULL
        && root->right != NULL)
        root->data
            = (root->left->data)
            | (root->right->data);
}

void printInorder(Node* root)
{
    if (root == NULL)
        return;

    // First recurr on left child
    printInorder(root->left);

    // Then print the data of node
    printf("%d ", root->data);

    // Now recur on right child
    printInorder(root->right);
}

// Main function
int main()
{

    Node* root = newNode(1);
    root->left = newNode(1);
    root->right = newNode(0);
    root->left->left = newNode(0);
    root->left->right = newNode(1);
    root->right->left = newNode(1);
    root->right->right = newNode(1);

    convertTree(root);
    printInorder(root);
    return 0;
}
```

## 计算机编程语言

```
# Python program to convert a
# given binary tree to
# a tree that holds
# logical OR property.

# Function that allocates a new
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Convert the given tree
# to a tree where each node
# is logical or of its children
# The main idea is to do
# Postorder traversal
def convertTree(root) :

    if (root == None) :
        return

    # First recur on left child
    convertTree(root.left)

    # Then recur on right child
    convertTree(root.right)

    if (root.left and root.right):
        root.data \
        = ((root.left.data) |
                    (root.right.data))

def printInorder(root) :

    if (root == None) :
        return

    # First recur on left child
    printInorder(root.left)

    # Then print the data of node
    print( root.data, end = " ")

    # Now recur on right child
    printInorder(root.right)

# Driver Code
if __name__ == '__main__':

    root = newNode(0)
    root.left = newNode(1)
    root.right = newNode(0)
    root.left.left = newNode(0)
    root.left.right = newNode(1)
    root.right.left = newNode(1)
    root.right.right = newNode(1)

    convertTree(root)
    printInorder(root)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert a
// given binary tree to a
// tree that holds logical
// OR property.
class GfG {

    // Structure of the binary tree
    static class Node {
        int data;
        Node left;
        Node right;
    }

    // Function to create a new node
    static Node newNode(int key)
    {
        Node node = new Node();
        node.data = key;
        node.left = null;
        node.right = null;
        return node;
    }

    // Convert the given tree to
    // a tree where each node is
    // logical AND of its children
    // The main idea is to do
    // Postorder traversal
    static void convertTree(Node root)
    {
        if (root == null)
            return;

        // First recur on left child
        convertTree(root.left);

        // Then recur on right child
        convertTree(root.right);

        if (root.left != null
            && root.right != null)
            root.data
                = (root.left.data)
                  | (root.right.data);
    }

    // Function to print inorder traversal
    // of the tree
    static void printInorder(Node root)
    {
        if (root == null)
            return;

        // First recur on left child
        printInorder(root.left);

        // Then print the data of node
        System.out.print(root.data + " ");

        // Now recur on right child
        printInorder(root.right);
    }

    // Driver Code
    public static void main(String[] args)
    {
        Node root = newNode(0);
        root.left = newNode(1);
        root.right = newNode(0);
        root.left.left = newNode(0);
        root.left.right = newNode(1);
        root.right.left = newNode(1);
        root.right.right = newNode(1);

        convertTree(root);
        printInorder(root);
    }
}
```

## C#

```
// C# code to convert a given
// binary tree to a tree that
// holds logical AND property.
using System;

class GfG {

    // Structure of binary tree
    class Node {
        public int data;
        public Node left;
        public Node right;
    }

    // Function to create a new node
    static Node newNode(int key)
    {
        Node node = new Node();
        node.data = key;
        node.left = null;
        node.right = null;
        return node;
    }

    // Convert the given tree to a
    // tree where each node is logical
    // AND of its children The main
    // idea is to do Postorder traversal
    static void convertTree(Node root)
    {
        if (root == null)
            return;

        // First recur on left child
        convertTree(root.left);

        // Then recur on right child
        convertTree(root.right);

        if (root.left != null
            && root.right != null)
            root.data
                = (root.left.data)
                  | (root.right.data);
    }

    // Function to perform the inorder
    // traversal
    static void printInorder(Node root)
    {
        if (root == null)
            return;

        // First recur on left child
        printInorder(root.left);

        // then print the data of node
        Console.Write(root.data + " ");

        // now recur on right child
        printInorder(root.right);
    }

    // Driver code
    public static void Main()
    {

        Node root = newNode(0);
        root.left = newNode(1);
        root.right = newNode(0);
        root.left.left = newNode(0);
        root.left.right = newNode(1);
        root.right.left = newNode(1);
        root.right.right = newNode(1);

        convertTree(root);
        printInorder(root);
    }
}
// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript code to convert a given
// binary tree to a tree that
// holds logical AND property.
// Structure of binary tree
class Node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

// Function to create a new node
function newNode(key)
{
    var node = new Node();
    node.data = key;
    node.left = null;
    node.right = null;
    return node;
}

// Convert the given tree to a
// tree where each node is logical
// AND of its children The main
// idea is to do Postorder traversal
function convertTree(root)
{
    if (root == null)
        return;

    // First recur on left child
    convertTree(root.left);

    // Then recur on right child
    convertTree(root.right);
    if (root.left != null
        && root.right != null)
        root.data
            = (root.left.data)
              | (root.right.data);
}

// Function to perform the inorder
// traversal
function printInorder(root)
{
    if (root == null)
        return;

    // First recur on left child
    printInorder(root.left);

    // then print the data of node
    document.write(root.data + " ");

    // now recur on right child
    printInorder(root.right);
}

// Driver code
var root = newNode(0);
root.left = newNode(1);
root.right = newNode(0);
root.left.left = newNode(0);
root.left.right = newNode(1);
root.right.left = newNode(1);
root.right.right = newNode(1);
convertTree(root);
printInorder(root);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
0 1 1 1 1 1 1
```