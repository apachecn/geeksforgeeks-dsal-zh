# 二叉树到二叉查找树的转换

> 原文:[https://www . geesforgeks . org/二叉树到二叉树的搜索树转换/](https://www.geeksforgeeks.org/binary-tree-to-binary-search-tree-conversion/)

给定一棵二叉树，将其转换为二叉查找树树。转换必须以保持二叉树原始结构的方式进行。

**示例**

```
Example 1
Input:
          10
         /  \
        2    7
       / \
      8   4
Output:
          8
         /  \
        4    10
       / \
      2   7

Example 2
Input:
          10
         /  \
        30   15
       /      \
      20       5
Output:
          15
         /  \
       10    20
       /      \
      5        30
```

**解决方案**

以下是将二叉树转换为二叉查找树的三步解决方案。

1)创建一个临时数组 arr[]来存储树的有序遍历。这一步需要 O(n)个时间。

2)对临时数组 arr[]进行排序。这一步的时间复杂度取决于排序算法。在下面的实现中，使用了快速排序，这需要(n^2)时间。这可以使用堆排序或合并排序在 O(nLogn)时间内完成。

3)再次遍历树，将数组元素逐个复制到树节点。这一步需要 O(n)个时间。

以下是上述方法的 C 实现。要转换的主要函数在下面的代码中突出显示。

## c++

```
/* A program to convert Binary Tree to Binary Search Tree */
#include <iostream>
using namespace std;

/* A binary tree node structure */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* A helper function that stores inorder traversal of a tree rooted
with node */
void storeInorder(struct node* node, int inorder[], int* index_ptr)
{
    // Base Case
    if (node == NULL)
        return;

    /* first store the left subtree */
    storeInorder(node->left, inorder, index_ptr);

    /* Copy the root's data */
    inorder[*index_ptr] = node->data;
    (*index_ptr)++; // increase index for next entry

    /* finally store the right subtree */
    storeInorder(node->right, inorder, index_ptr);
}

/* A helper function to count nodes in a Binary Tree */
int countNodes(struct node* root)
{
    if (root == NULL)
        return 0;
    return countNodes(root->left) + countNodes(root->right) + 1;
}

// Following function is needed for library function qsort()
int compare(const void* a, const void* b)
{
    return (*(int*)a - *(int*)b);
}

/* A helper function that copies contents of arr[] to Binary Tree.
This function basically does Inorder traversal of Binary Tree and
one by one copy arr[] elements to Binary Tree nodes */
void arrayToBST(int* arr, struct node* root, int* index_ptr)
{
    // Base Case
    if (root == NULL)
        return;

    /* first update the left subtree */
    arrayToBST(arr, root->left, index_ptr);

    /* Now update root's data and increment index */
    root->data = arr[*index_ptr];
    (*index_ptr)++;

    /* finally update the right subtree */
    arrayToBST(arr, root->right, index_ptr);
}

// This function converts a given Binary Tree to BST
void binaryTreeToBST(struct node* root)
{
    // base case: tree is empty
    if (root == NULL)
        return;

    /* Count the number of nodes in Binary Tree so that
    we know the size of temporary array to be created */
    int n = countNodes(root);

    // Create a temp array arr[] and store inorder traversal of tree in arr[]
    int* arr = new int[n];
    int i = 0;
    storeInorder(root, arr, &i);

    // Sort the array using library function for quick sort
    qsort(arr, n, sizeof(arr[0]), compare);

    // Copy array elements back to Binary Tree
    i = 0;
    arrayToBST(arr, root, &i);

    // delete dynamically allocated memory to avoid memory leak
    delete[] arr;
}

/* Utility function to create a new Binary Tree node */
struct node* newNode(int data)
{
    struct node* temp = new struct node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* Utility function to print inorder traversal of Binary Tree */
void printInorder(struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    cout <<" "<< node->data;

    /* now recur on right child */
    printInorder(node->right);
}

/* Driver function to test above functions */
int main()
{
    struct node* root = NULL;

    /* Constructing tree given in the above figure
        10
        / \
        30 15
    /     \
    20     5 */
    root = newNode(10);
    root->left = newNode(30);
    root->right = newNode(15);
    root->left->left = newNode(20);
    root->right->right = newNode(5);

    // convert Binary Tree to BST
    binaryTreeToBST(root);

    cout <<"Following is Inorder Traversal of the converted BST:" << endl ;
    printInorder(root);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
/* A program to convert Binary Tree to Binary Search Tree */
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node structure */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* A helper function that stores inorder traversal of a tree rooted
with node */
void storeInorder(struct node* node, int inorder[], int* index_ptr)
{
    // Base Case
    if (node == NULL)
        return;

    /* first store the left subtree */
    storeInorder(node->left, inorder, index_ptr);

    /* Copy the root's data */
    inorder[*index_ptr] = node->data;
    (*index_ptr)++; // increase index for next entry

    /* finally store the right subtree */
    storeInorder(node->right, inorder, index_ptr);
}

/* A helper function to count nodes in a Binary Tree */
int countNodes(struct node* root)
{
    if (root == NULL)
        return 0;
    return countNodes(root->left) + countNodes(root->right) + 1;
}

// Following function is needed for library function qsort()
int compare(const void* a, const void* b)
{
    return (*(int*)a - *(int*)b);
}

/* A helper function that copies contents of arr[] to Binary Tree.
This function basically does Inorder traversal of Binary Tree and
one by one copy arr[] elements to Binary Tree nodes */
void arrayToBST(int* arr, struct node* root, int* index_ptr)
{
    // Base Case
    if (root == NULL)
        return;

    /* first update the left subtree */
    arrayToBST(arr, root->left, index_ptr);

    /* Now update root's data and increment index */
    root->data = arr[*index_ptr];
    (*index_ptr)++;

    /* finally update the right subtree */
    arrayToBST(arr, root->right, index_ptr);
}

// This function converts a given Binary Tree to BST
void binaryTreeToBST(struct node* root)
{
    // base case: tree is empty
    if (root == NULL)
        return;

    /* Count the number of nodes in Binary Tree so that
    we know the size of temporary array to be created */
    int n = countNodes(root);

    // Create a temp array arr[] and store inorder traversal of tree in arr[]
    int* arr = new int[n];
    int i = 0;
    storeInorder(root, arr, &i);

    // Sort the array using library function for quick sort
    qsort(arr, n, sizeof(arr[0]), compare);

    // Copy array elements back to Binary Tree
    i = 0;
    arrayToBST(arr, root, &i);

    // delete dynamically allocated memory to avoid memory leak
    delete[] arr;
}

/* Utility function to create a new Binary Tree node */
struct node* newNode(int data)
{
    struct node* temp = new struct node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* Utility function to print inorder traversal of Binary Tree */
void printInorder(struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    printInorder(node->right);
}

/* Driver function to test above functions */
int main()
{
    struct node* root = NULL;

    /* Constructing tree given in the above figure
        10
        / \
        30 15
    /     \
    20     5 */
    root = newNode(10);
    root->left = newNode(30);
    root->right = newNode(15);
    root->left->left = newNode(20);
    root->right->right = newNode(5);

    // convert Binary Tree to BST
    binaryTreeToBST(root);

    printf("Following is Inorder Traversal of the converted BST: \n");
    printInorder(root);

    return 0;
}
```

## Java

```
/* A program to convert Binary Tree to Binary Search Tree */
import java.util.*;

public class GFG{

    /* A binary tree node structure */
    static class Node {
        int data;
        Node left;
        Node right;
    };

    // index pointer to pointer to the array index
    static int index;

    /* A helper function that stores inorder traversal of a tree rooted
    with node */
    static void storeInorder(Node node, int inorder[])
    {
        // Base Case
        if (node == null)
            return;

        /* first store the left subtree */
        storeInorder(node.left, inorder);

        /* Copy the root's data */
        inorder[index] = node.data;
        index++; // increase index for next entry

        /* finally store the right subtree */
        storeInorder(node.right, inorder);
    }

    /* A helper function to count nodes in a Binary Tree */
    static int countNodes(Node root)
    {
        if (root == null)
            return 0;
        return countNodes(root.left) + countNodes(root.right) + 1;
    }

    /* A helper function that copies contents of arr[] to Binary Tree.
    This function basically does Inorder traversal of Binary Tree and
    one by one copy arr[] elements to Binary Tree nodes */
    static void arrayToBST(int[] arr, Node root)
    {
        // Base Case
        if (root == null)
            return;

        /* first update the left subtree */
        arrayToBST(arr, root.left);

        /* Now update root's data and increment index */
        root.data = arr[index];
        index++;

        /* finally update the right subtree */
        arrayToBST(arr, root.right);
    }

    // This function converts a given Binary Tree to BST
    static void binaryTreeToBST(Node root)
    {
        // base case: tree is empty
        if (root == null)
            return;

        /* Count the number of nodes in Binary Tree so that
        we know the size of temporary array to be created */
        int n = countNodes(root);

        // Create a temp array arr[] and store inorder traversal of tree in arr[]
        int arr[] = new int[n];

        storeInorder(root, arr);

        // Sort the array using library function for quick sort
        Arrays.sort(arr);

        // Copy array elements back to Binary Tree
        index = 0;
        arrayToBST(arr, root);
    }

    /* Utility function to create a new Binary Tree node */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    /* Utility function to print inorder traversal of Binary Tree */
    static void printInorder(Node node)
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

    /* Driver function to test above functions */
    public static void main(String args[])
    {
        Node root = null;

        /* Constructing tree given in the above figure
            10
            / \
            30 15
        /     \
        20     5 */
        root = newNode(10);
        root.left = newNode(30);
        root.right = newNode(15);
        root.left.left = newNode(20);
        root.right.right = newNode(5);

        // convert Binary Tree to BST
        binaryTreeToBST(root);

        System.out.println("Following is Inorder Traversal of the converted BST: ");
        printInorder(root);

    }
}

// This code is contributed by adityapande88.
```

## Python

```
# Program to convert binary tree to BST

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function to store the inorder traversal of a tree
def storeInorder(root, inorder):

    # Base Case
    if root is None:
        return

    # First store the left subtree
    storeInorder(root.left, inorder)

    # Copy the root's data
    inorder.append(root.data)

    # Finally store the right subtree
    storeInorder(root.right, inorder)

# A helper function to count nodes in a binary tree
def countNodes(root):
    if root is None:
        return 0

    return countNodes(root.left) + countNodes(root.right) + 1

# Helper function that copies contents of sorted array
# to Binary tree
def arrayToBST(arr, root):

    # Base Case
    if root is None:
        return

    # First update the left subtree
    arrayToBST(arr, root.left)

    # now update root's data delete the value from array
    root.data = arr[0]
    arr.pop(0)

    # Finally update the right subtree
    arrayToBST(arr, root.right)

# This function converts a given binary tree to BST
def binaryTreeToBST(root):

    # Base Case: Tree is empty
    if root is None:
        return

    # Count the number of nodes in Binary Tree so that
    # we know the size of temporary array to be created
    n = countNodes(root)

    # Create the temp array and store the inorder traversal
    # of tree
    arr = []
    storeInorder(root, arr)

    # Sort the array
    arr.sort()

    # copy array elements back to binary tree
    arrayToBST(arr, root)

# Print the inorder traversal of the tree
def printInorder(root):
    if root is None:
        return
    printInorder(root.left)
    print root.data,
    printInorder(root.right)

# Driver program to test above function
root = Node(10)
root.left = Node(30)
root.right = Node(15)
root.left.left = Node(20)
root.right.right = Node(5)

# Convert binary tree to BST
binaryTreeToBST(root)

print "Following is the inorder traversal of the converted BST"
printInorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## c#

```
using System;

public class Node
{
    public int data;
    public Node left;
    public Node right;
}

public class GFG{

    // index pointer to pointer to the array index
    static int index;

    /* A helper function that stores inorder traversal of a tree rooted
    with node */
    static void storeInorder(Node node, int[] inorder)
    {
        // Base Case
        if (node == null)
            return;

        /* first store the left subtree */
        storeInorder(node.left, inorder);

        /* Copy the root's data */
        inorder[index] = node.data;
        index++; // increase index for next entry

        /* finally store the right subtree */
        storeInorder(node.right, inorder);
    }

    /* A helper function to count nodes in a Binary Tree */
    static int countNodes(Node root)
    {
        if (root == null)
            return 0;
        return countNodes(root.left) + countNodes(root.right) + 1;
    }

    /* A helper function that copies contents of arr[] to Binary Tree.
    This function basically does Inorder traversal of Binary Tree and
    one by one copy arr[] elements to Binary Tree nodes */
    static void arrayToBST(int[] arr, Node root)
    {
        // Base Case
        if (root == null)
            return;

        /* first update the left subtree */
        arrayToBST(arr, root.left);

        /* Now update root's data and increment index */
        root.data = arr[index];
        index++;

        /* finally update the right subtree */
        arrayToBST(arr, root.right);
    }

    // This function converts a given Binary Tree to BST
    static void binaryTreeToBST(Node root)
    {
        // base case: tree is empty
        if (root == null)
            return;

        /* Count the number of nodes in Binary Tree so that
        we know the size of temporary array to be created */
        int n = countNodes(root);

        // Create a temp array arr[] and store inorder traversal of tree in arr[]
        int[] arr = new int[n];

        storeInorder(root, arr);

        // Sort the array using library function for quick sort
        Array.Sort(arr);

        // Copy array elements back to Binary Tree
        index = 0;
        arrayToBST(arr, root);
    }

    /* Utility function to create a new Binary Tree node */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    /* Utility function to print inorder traversal of Binary Tree */
    static void printInorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        Console.Write(node.data + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    /* Driver function to test above functions */

    static public void Main (){

        Node root = null;

        /* Constructing tree given in the above figure
            10
            / \
            30 15
        /     \
        20     5 */
        root = newNode(10);
        root.left = newNode(30);
        root.right = newNode(15);
        root.left.left = newNode(20);
        root.right.right = newNode(5);

        // convert Binary Tree to BST
        binaryTreeToBST(root);

        Console.WriteLine("Following is Inorder Traversal of the converted BST: ");
        printInorder(root);

    }
}

// This code is contributed by avanitrachhadiya2155
```

## Javascript

```
<script>

    /* A program to convert Binary Tree
    to Binary Search Tree */

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // index pointer to pointer to the array index
    let index = 0;

    /* Utility function to create a new Binary Tree node */
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    /* Utility function to print inorder
       traversal of Binary Tree */
    function printInorder(node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        document.write(node.data + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    /* A helper function that copies
       contents of arr[] to Binary Tree.
       This function basically does Inorder
       traversal of Binary Tree and
       one by one copy arr[] elements to Binary Tree nodes */
    function arrayToBST(arr, root)
    {
        // Base Case
        if (root == null)
            return;

        /* first update the left subtree */
        arrayToBST(arr, root.left);

        /* Now update root's data and increment index */
        root.data = arr[index];
        index++;

        /* finally update the right subtree */
        arrayToBST(arr, root.right);
    }

    /* A helper function that stores inorder
    traversal of a tree rooted with node */
    function storeInorder(node, inorder)
    {
        // Base Case
        if (node == null)
            return inorder;

        /* first store the left subtree */
        storeInorder(node.left, inorder);

        /* Copy the root's data */
        inorder[index] = node.data;
        index++; // increase index for next entry

        /* finally store the right subtree */
        storeInorder(node.right, inorder);
    }

    /* A helper function to count nodes in a Binary Tree */
    function countNodes(root)
    {
        if (root == null)
            return 0;
        return countNodes(root.left) + countNodes(root.right) + 1;
    }

    // This function converts a given Binary Tree to BST
    function binaryTreeToBST(root)
    {
        // base case: tree is empty
        if (root == null)
            return;

        /* Count the number of nodes in Binary Tree so that
        we know the size of temporary array to be created */
        let n = countNodes(root);

        // Create a temp array arr[] and store
        // inorder traversal of tree in arr[]
        let arr = new Array(n);
        arr.fill(0);

        storeInorder(root, arr);

        // Sort the array using library function for quick sort
        arr.sort(function(a, b){return a - b});

        // Copy array elements back to Binary Tree
        index = 0;
        arrayToBST(arr, root);
    }

    let root = null;

    /* Constructing tree given in the above figure
              10
              / \
              30 15
          /     \
          20     5 */
    root = newNode(10);
    root.left = newNode(30);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.right.right = newNode(5);

    // convert Binary Tree to BST
    binaryTreeToBST(root);

    document.write(
    "Following is Inorder Traversal of the converted BST: "+
    "</br>");
    printInorder(root);

</script>
```

**输出**

```
Following is the inorder traversal of the converted BST
5 10 15 20 30
```

**复杂度分析:**

*   **Time complexity:** o (nlogn). This is the complexity of the sorting algorithm we are using. After the first sequential traversal, the remaining operations are performed in linear time.
*   **auxiliary space:** o (n). Use the data structure "array" to store ordered traversal.

我们将介绍解决这个问题的另一种方法，即使用 0(树的高度)额外空间来转换树。

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论