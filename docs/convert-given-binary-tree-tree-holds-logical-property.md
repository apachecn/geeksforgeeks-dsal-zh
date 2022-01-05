# 将给定的二叉树转换为持有逻辑与属性的树

> 原文:[https://www . geesforgeks . org/convert-given-二叉树-tree-holds-logic-property/](https://www.geeksforgeeks.org/convert-given-binary-tree-tree-holds-logical-property/)

给定一棵二叉树(每个节点最多有 2 个子节点)，其中每个节点的值为 0 或 1。将给定的二叉树转换为持有逻辑与属性的树，即每个节点值应该是其子节点之间的逻辑与。

**示例:**

```
Input : The below tree doesn’t hold the logical AND property
        convert it to a tree that holds the property.
             1
           /   \
          1     0
         / \   / \
        0   1 1   1 
Output :
             0
           /   \
          0     1
         / \   / \
        0   1 1   1 
```

其思想是以后序方式遍历给定的二叉树。对于每个节点，检查(递归地)如果该节点有一个子节点，那么我们不需要检查其他任何东西，如果该节点有它的两个子节点，那么简单地用它的子数据的逻辑“与”来更新节点数据。

## C++

```
// C++ code to convert a given binary tree
// to a tree that holds logical AND property.
#include<bits/stdc++.h>
using namespace std;

// Structure of binary tree
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

// function to create a new node
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->data= key;
    node->left = node->right = NULL;
    return node;
}

// Convert the given tree to a tree where
// each node is logical AND of its children
// The main idea is to do Postorder traversal
void convertTree(Node *root)
{
    if (root == NULL)
        return;

    /* first recur on left child */
    convertTree(root->left);

    /* then recur on right child */
    convertTree(root->right);

    if (root->left != NULL && root->right != NULL)
        root->data = (root->left->data) &
                     (root->right->data);
}

void printInorder(Node* root)
{
    if (root == NULL)
        return;

    /* first recur on left child */
    printInorder(root->left);

    /* then print the data of node */
    printf("%d ", root->data);

    /* now recur on right child */
    printInorder(root->right);
}

// main function
int main()
{
    /* Create following Binary Tree
             1
           /   \
          1     0
         / \   / \
        0   1 1   1
             */

    Node *root=newNode(0);
    root->left=newNode(1);
    root->right=newNode(0);
    root->left->left=newNode(0);
    root->left->right=newNode(1);
    root->right->left=newNode(1);
    root->right->right=newNode(1);
    printf("\n Inorder traversal before conversion ");
    printInorder(root);

    convertTree(root);

    printf("\n Inorder traversal after conversion ");
    printInorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert a given binary tree
// to a tree that holds logical AND property.
class GfG {

// Structure of binary tree
static class Node
{
    int data;
     Node left;
     Node right;
}

// function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.data= key;
    node.left = null;
    node.right = null;
    return node;
}

// Convert the given tree to a tree where
// each node is logical AND of its children
// The main idea is to do Postorder traversal
static void convertTree(Node root)
{
    if (root == null)
        return;

    /* first recur on left child */
    convertTree(root.left);

    /* then recur on right child */
    convertTree(root.right);

    if (root.left != null && root.right != null)
        root.data = (root.left.data) & (root.right.data);
}

static void printInorder(Node root)
{
    if (root == null)
        return;

    /* first recur on left child */
    printInorder(root.left);

    /* then print the data of node */
    System.out.print(root.data + " ");

    /* now recur on right child */
    printInorder(root.right);
}

// main function
public static void main(String[] args)
{
    /* Create following Binary Tree
            1
        / \
        1     0
        / \ / \
        0 1 1 1
            */

    Node root=newNode(0);
    root.left=newNode(1);
    root.right=newNode(0);
    root.left.left=newNode(0);
    root.left.right=newNode(1);
    root.right.left=newNode(1);
    root.right.right=newNode(1);
    System.out.print("Inorder traversal before conversion ");
    printInorder(root);

    convertTree(root);
    System.out.println();
    System.out.print("Inorder traversal after conversion ");
    printInorder(root);
}}
```

## 蟒蛇 3

```
# Program to convert an aribitary binary tree
# to a tree that holds children sum property

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Convert the given tree to a tree where
# each node is logical AND of its children
# The main idea is to do Postorder traversal
def convertTree(root) :

    if (root == None) :
        return

    """ first recur on left child """
    convertTree(root.left)

    """ then recur on right child """
    convertTree(root.right)

    if (root.left != None and root.right != None):
        root.data = ((root.left.data) &
                     (root.right.data))

def printInorder(root) :

    if (root == None) :
        return

    """ first recur on left child """
    printInorder(root.left)

    """ then print the data of node """
    print( root.data, end = " ")

    """ now recur on right child """
    printInorder(root.right)

# Driver Code
if __name__ == '__main__':

    """ Create following Binary Tree
            1
        / \
        1     0
        / \ / \
        0 1 1 1
            """

    root = newNode(0)
    root.left = newNode(1)
    root.right = newNode(0)
    root.left.left = newNode(0)
    root.left.right = newNode(1)
    root.right.left = newNode(1)
    root.right.right = newNode(1)

    print("Inorder traversal before conversion",
                                      end = " ")
    printInorder(root)

    convertTree(root)

    print("\nInorder traversal after conversion ",
                                        end = " ")
    printInorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# code to convert a given binary tree
// to a tree that holds logical AND property.
using System;

class GfG
{

// Structure of binary tree
class Node
{
    public int data;
    public Node left;
    public Node right;
}

// function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.data= key;
    node.left = null;
    node.right = null;
    return node;
}

// Convert the given tree to a tree where
// each node is logical AND of its children
// The main idea is to do Postorder traversal
static void convertTree(Node root)
{
    if (root == null)
        return;

    /* first recur on left child */
    convertTree(root.left);

    /* then recur on right child */
    convertTree(root.right);

    if (root.left != null && root.right != null)
        root.data = (root.left.data) & (root.right.data);
}

static void printInorder(Node root)
{
    if (root == null)
        return;

    /* first recur on left child */
    printInorder(root.left);

    /* then print the data of node */
    Console.Write(root.data + " ");

    /* now recur on right child */
    printInorder(root.right);
}

// Driver code
public static void Main()
{
    /* Create following Binary Tree
            1
        / \
        1 0
        / \ / \
        0 1 1 1
            */

    Node root=newNode(0);
    root.left=newNode(1);
    root.right=newNode(0);
    root.left.left=newNode(0);
    root.left.right=newNode(1);
    root.right.left=newNode(1);
    root.right.right=newNode(1);
    Console.Write("Inorder traversal before conversion ");
    printInorder(root);

    convertTree(root);
    Console.WriteLine();
    Console.Write("Inorder traversal after conversion ");
    printInorder(root);
}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

// Javascript code to convert a given binary tree
// to a tree that holds logical AND property.

// Structure of binary tree
class Node
{
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

// Convert the given tree to a tree where
// each node is logical AND of its children
// The main idea is to do Postorder traversal
function convertTree(root)
{
    if (root == null)
        return;

    /* First recur on left child */
    convertTree(root.left);

    /* Then recur on right child */
    convertTree(root.right);

    if (root.left != null && root.right != null)
        root.data = (root.left.data) & (root.right.data);
}

function printInorder(root)
{
    if (root == null)
        return;

    /* First recur on left child */
    printInorder(root.left);

    /* then print the data of node */
    document.write(root.data + " ");

    /* Now recur on right child */
    printInorder(root.right);
}

// Driver code
/* Create following Binary Tree
        1
    / \
    1 0
    / \ / \
    0 1 1 1
        */
var root = newNode(0);
root.left = newNode(1);
root.right = newNode(0);
root.left.left = newNode(0);
root.left.right = newNode(1);
root.right.left = newNode(1);
root.right.right = newNode(1);

document.write("Inorder traversal before conversion ");
printInorder(root);
convertTree(root);

document.write("<br>");
document.write("Inorder traversal after conversion ");

printInorder(root);

// This code is contributed by noob2000

</script>
```

**输出:**

```
 Inorder traversal before conversion 0 1 1 0 1 0 1 
 Inorder traversal after conversion 0 0 1 0 1 1 1 

```

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。