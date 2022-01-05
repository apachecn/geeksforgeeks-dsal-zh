# 根据给定的前序遍历构建一个特殊的树

> 原文:[https://www . geeksforgeeks . org/construct-a-special-tree-from-给定-preorder-traversation/](https://www.geeksforgeeks.org/construct-a-special-tree-from-given-preorder-traversal/)

给定一个数组“pre[]”，它表示一个特殊二叉树的 Preorder 遍历，其中每个节点都有 0 或 2 个子节点。又给出了一个数组“PRlen[]”，它只有两个可能的值“L”和“N”。“preLN[]”中的值“L”表示二叉树中对应的节点是叶节点，“N”表示对应的节点是非叶节点。编写一个函数，根据给定的两个数组构造树。

**示例:**

```
Input:  pre[] = {10, 30, 20, 5, 15},  preLN[] = {'N', 'N', 'L', 'L', 'L'}
Output: Root of following tree
          10
         /  \
        30   15
       /  \
      20   5
```

pre[]中的第一个元素将始终是 root。所以我们可以很容易地找出根源。如果左边的子树为空，右边的子树也必须为空，根的 preLN[]条目必须为‘L’。我们可以简单地创建一个节点并返回它。如果左右子树不为空，则递归调用左右子树，并将返回的节点链接到根。

## C++

```
/* A program to construct Binary Tree from preorder traversal */
#include<bits/stdc++.h>

/* A binary tree node structure */
struct node
{
    int data;
    struct node *left;
    struct node *right;
};

/* Utility function to create a new Binary Tree node */
struct node* newNode (int data)
{
    struct node *temp = new struct node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* A recursive function to create a Binary Tree from given pre[]
   preLN[] arrays. The function returns root of tree. index_ptr is used
   to update index values in recursive calls. index must be initially
   passed as 0 */
struct node *constructTreeUtil(int pre[], char preLN[], int *index_ptr, int n)
{
    int index = *index_ptr; // store the current value of index in pre[]

    // Base Case: All nodes are constructed
    if (index == n)
        return NULL;

    // Allocate memory for this node and increment index for
    // subsequent recursive calls
    struct node *temp = newNode ( pre[index] );
    (*index_ptr)++;

    // If this is an internal node, construct left and right subtrees and link the subtrees
    if (preLN[index] == 'N')
    {
      temp->left  = constructTreeUtil(pre, preLN, index_ptr, n);
      temp->right = constructTreeUtil(pre, preLN, index_ptr, n);
    }

    return temp;
}

// A wrapper over constructTreeUtil()
struct node *constructTree(int pre[], char preLN[], int n)
{
    // Initialize index as 0\. Value of index is used in recursion to maintain
    // the current index in pre[] and preLN[] arrays.
    int index = 0;

    return constructTreeUtil (pre, preLN, &index, n);
}

/* This function is used only for testing */
void printInorder (struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder (node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    printInorder (node->right);
}

/* Driver function to test above functions */
int main()
{
    struct node *root = NULL;

    /* Constructing tree given in the above figure
          10
         /  \
        30   15
       /  \
      20   5 */
    int pre[] = {10, 30, 20, 5, 15};
    char preLN[] = {'N', 'N', 'L', 'L', 'L'};
    int n = sizeof(pre)/sizeof(pre[0]);

    // construct the above tree
    root = constructTree (pre, preLN, n);

    // Test the constructed tree
    printf("Following is Inorder Traversal of the Constructed Binary Tree: \n");
    printInorder (root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct a binary tree from preorder traversal

// A Binary Tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class Index
{
    int index = 0;
}

class BinaryTree
{
    Node root;
    Index myindex = new Index();

    /* A recursive function to create a Binary Tree from given pre[]
       preLN[] arrays. The function returns root of tree. index_ptr is used
       to update index values in recursive calls. index must be initially
       passed as 0 */
    Node constructTreeUtil(int pre[], char preLN[], Index index_ptr,
                                                     int n, Node temp)
    {
        // store the current value of index in pre[]
        int index = index_ptr.index;

        // Base Case: All nodes are constructed
        if (index == n)
            return null;

        // Allocate memory for this node and increment index for
        // subsequent recursive calls
        temp = new Node(pre[index]);
        (index_ptr.index)++;

        // If this is an internal node, construct left and right subtrees
        // and link the subtrees
        if (preLN[index] == 'N')
        {
            temp.left = constructTreeUtil(pre, preLN, index_ptr, n,
                                                               temp.left);
            temp.right = constructTreeUtil(pre, preLN, index_ptr, n,
                                                               temp.right);
        }

        return temp;
    }

    // A wrapper over constructTreeUtil()
    Node constructTree(int pre[], char preLN[], int n, Node node)
    {
        // Initialize index as 0\. Value of index is used in recursion to
        // maintain the current index in pre[] and preLN[] arrays.
        int index = 0;

        return constructTreeUtil(pre, preLN, myindex, n, node);
    }

    /* This function is used only for testing */
    void printInorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        System.out.print(node.data + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    // driver function to test the above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[]{10, 30, 20, 5, 15};
        char preLN[] = new char[]{'N', 'N', 'L', 'L', 'L'};
        int n = pre.length;

        // construct the above tree
        Node mynode = tree.constructTree(pre, preLN, n, tree.root);

        // Test the constructed tree
        System.out.println("Following is Inorder Traversal of the" 
                                      + "Constructed Binary Tree: ");
        tree.printInorder(mynode);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# A program to construct Binary
# Tree from preorder traversal

# Utility function to create a
# new Binary Tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A recursive function to create a
# Binary Tree from given pre[] preLN[]
# arrays. The function returns root of 
# tree. index_ptr is used to update
# index values in recursive calls. index
# must be initially passed as 0
def constructTreeUtil(pre, preLN, index_ptr, n):

    index = index_ptr[0] # store the current value
                         # of index in pre[]

    # Base Case: All nodes are constructed
    if index == n:
        return None

    # Allocate memory for this node and
    # increment index for subsequent
    # recursive calls
    temp = newNode(pre[index])
    index_ptr[0] += 1

    # If this is an internal node, construct left
    # and right subtrees and link the subtrees
    if preLN[index] == 'N':
        temp.left = constructTreeUtil(pre, preLN,
                                      index_ptr, n)
        temp.right = constructTreeUtil(pre, preLN,
                                       index_ptr, n)

    return temp

# A wrapper over constructTreeUtil()
def constructTree(pre, preLN, n):

    # Initialize index as 0\. Value of index is
    # used in recursion to maintain the current
    # index in pre[] and preLN[] arrays.
    index = [0]

    return constructTreeUtil(pre, preLN, index, n)

# This function is used only for testing
def printInorder (node):
    if node == None:
        return

    # first recur on left child
    printInorder (node.left)

    # then print the data of node
    print(node.data,end=" ")

    # now recur on right child
    printInorder (node.right)

# Driver Code
if __name__ == '__main__':
    root = None

    # Constructing tree given in
    # the above figure
    #     10
    #     / \
    # 30 15
    # / \
    # 20 5
    pre = [10, 30, 20, 5, 15]
    preLN = ['N', 'N', 'L', 'L', 'L']
    n = len(pre)

    # construct the above tree
    root = constructTree (pre, preLN, n)

    # Test the constructed tree
    print("Following is Inorder Traversal of",
          "the Constructed Binary Tree:")
    printInorder (root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to construct a binary
// tree from preorder traversal
using System;

// A Binary Tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class Index
{
    public int index = 0;
}

class GFG
{
public Node root;
public Index myindex = new Index();

/* A recursive function to create a
Binary Tree from given pre[] preLN[] arrays.
The function returns root of tree. index_ptr
is used to update index values in recursive
calls. index must be initially passed as 0 */
public virtual Node constructTreeUtil(int[] pre, char[] preLN,
                                      Index index_ptr, int n,
                                      Node temp)
{
    // store the current value of index in pre[]
    int index = index_ptr.index;

    // Base Case: All nodes are constructed
    if (index == n)
    {
        return null;
    }

    // Allocate memory for this node
    // and increment index for
    // subsequent recursive calls
    temp = new Node(pre[index]);
    (index_ptr.index)++;

    // If this is an internal node,
    // construct left and right subtrees
    // and link the subtrees
    if (preLN[index] == 'N')
    {
        temp.left = constructTreeUtil(pre, preLN, index_ptr,
                                      n, temp.left);
        temp.right = constructTreeUtil(pre, preLN, index_ptr,
                                       n, temp.right);
    }

    return temp;
}

// A wrapper over constructTreeUtil()
public virtual Node constructTree(int[] pre, char[] preLN,
                                  int n, Node node)
{
    // Initialize index as 0\. Value of
    // index is used in recursion to
    // maintain the current index in
    // pre[] and preLN[] arrays.
    int index = 0;

    return constructTreeUtil(pre, preLN,
                             myindex, n, node);
}

/* This function is used only for testing */
public virtual void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }

    /* first recur on left child */
    printInorder(node.left);

    /* then print the data of node */
    Console.Write(node.data + " ");

    /* now recur on right child */
    printInorder(node.right);
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    int[] pre = new int[]{10, 30, 20, 5, 15};
    char[] preLN = new char[]{'N', 'N', 'L', 'L', 'L'};
    int n = pre.Length;

    // construct the above tree
    Node mynode = tree.constructTree(pre, preLN,
                                     n, tree.root);

    // Test the constructed tree
    Console.WriteLine("Following is Inorder Traversal of the" +
                                  "Constructed Binary Tree: ");
    tree.printInorder(mynode);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to construct a binary
// tree from preorder traversal

// A Binary Tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

class Index
{
    constructor()
    {
        this.index = 0;
    }
}

var root = null;
var myindex = new Index();

/* A recursive function to create a
Binary Tree from given pre[] preLN[] arrays.
The function returns root of tree. index_ptr
is used to update index values in recursive
calls. index must be initially passed as 0 */
function constructTreeUtil(pre, preLN, index_ptr, n, temp)
{
    // store the current value of index in pre[]
    var index = index_ptr.index;

    // Base Case: All nodes are constructed
    if (index == n)
    {
        return null;
    }

    // Allocate memory for this node
    // and increment index for
    // subsequent recursive calls
    temp = new Node(pre[index]);
    (index_ptr.index)++;

    // If this is an internal node,
    // construct left and right subtrees
    // and link the subtrees
    if (preLN[index] == 'N')
    {
        temp.left = constructTreeUtil(pre, preLN, index_ptr,
                                      n, temp.left);
        temp.right = constructTreeUtil(pre, preLN, index_ptr,
                                       n, temp.right);
    }

    return temp;
}

// A wrapper over constructTreeUtil()
function constructTree(pre, preLN, n, node)
{
    // Initialize index as 0\. Value of
    // index is used in recursion to
    // maintain the current index in
    // pre[] and preLN[] arrays.
    var index = 0;

    return constructTreeUtil(pre, preLN,
                             myindex, n, node);
}

/* This function is used only for testing */
function printInorder( node)
{
    if (node == null)
    {
        return;
    }

    /* first recur on left child */
    printInorder(node.left);

    /* then print the data of node */
    document.write(node.data + " ");

    /* now recur on right child */
    printInorder(node.right);
}

// Driver Code
var pre = [10, 30, 20, 5, 15];
var preLN = ['N', 'N', 'L', 'L', 'L'];
var n = pre.length;
// construct the above tree
var mynode = constructTree(pre, preLN,
                                 n, root);
// Test the constructed tree
document.write("Following is Inorder Traversal of the" +
                              "Constructed Binary Tree:<br>");
printInorder(mynode);

</script>
```

**输出:**

```
Following is Inorder Traversal of the Constructed Binary Tree:
20 30 5 10 15
```

**时间复杂度:** O(n)
[根据全 k 元树的前序遍历](https://www.geeksforgeeks.org/construct-full-k-ary-tree-preorder-traversal/)
构建全 k 元树如果发现有不正确的地方请写评论，或者想分享更多关于以上讨论话题的信息