# 以最小最大方式打印二叉查找树

> 原文:[https://www . geesforgeks . org/print-binary-search-tree-in-min-max-fashion/](https://www.geeksforgeeks.org/print-binary-search-tree-in-min-max-fashion/)

给定一个二叉查找树(BST)，任务是以最小-最大方式打印 BST。
**什么是 min-max 时尚？**
最小-最大方式意味着你必须先打印最大节点，然后最小节点，然后第二个最大节点，然后第二个最小节点，以此类推。

**示例:**

```
Input:                
         100                            
        /   \    
      20     500     
     /  \                      
    10   30 
          \   
           40
Output: 10 500 20 100 30 40

Input:
         40                            
        /   \    
      20     50     
     /  \      \               
    10   35     60
        /      /   
      25      55
Output: 10 60 20 55 25 50 35 40 
```

**进场:**

1.  创建一个有序数组**【】**并存储给定二叉查找树的有序遍历。
2.  由于二叉查找树的有序遍历是按升序排序的，初始化 **i = 0** 和**j = n–1**。
3.  打印**以便【I】**并更新 **i = i + 1** 。
4.  打印**以便【j】**并更新**j = j–1**。
5.  重复步骤 3 和 4，直到所有柠檬都被打印出来。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Structure of each node of BST
struct node {
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
node* newNode(int item)
{
    node* temp = new node();
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* A utility function to insert a new
node with given key in BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
int sizeOfTree(node* root)
{
    if (root == NULL) {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root->left);

    // Calculate right size recursively
    int right = sizeOfTree(root->right);

    // Return total size recursively
    return (left + right + 1);
}

// Utility function to print the
// Min max order of BST
void printMinMaxOrderUtil(node* root, int inOrder[],
                          int& index)
{

    // Base condition
    if (root == NULL) {
        return;
    }

    // Left recursive call
    printMinMaxOrderUtil(root->left, inOrder, index);

    // Store elements in inorder array
    inOrder[index++] = root->key;

    // Right recursive call
    printMinMaxOrderUtil(root->right, inOrder, index);
}

// Function to print the
// Min max order of BST
void printMinMaxOrder(node* root)
{
    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Take auxiliary array for storing
    // The inorder traversal of BST
    int inOrder[numNode + 1];
    int index = 0;

    // Function call for printing
    // element in min max order
    printMinMaxOrderUtil(root, inOrder, index);
    int i = 0;
    index--;

    // While loop for printing elements
    // In front last order
    while (i < index) {
        cout << inOrder[i++] << " "
             << inOrder[index--] << " ";
    }
    if (i == index) {
        cout << inOrder[i] << endl;
    }
}

// Driver code
int main()
{
    struct node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    printMinMaxOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Structure of each node of BST
static class node
{
    int key;
    node left, right;
};
static int index;

// A utility function to create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

/* A utility function to insert a new
node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty,
    return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
static int sizeOfTree(node root)
{
    if (root == null)
    {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Utility function to print the
// Min max order of BST
static void printMinMaxOrderUtil(node root,
                                 int inOrder[])
{

    // Base condition
    if (root == null)
    {
        return;
    }

    // Left recursive call
    printMinMaxOrderUtil(root.left, inOrder);

    // Store elements in inorder array
    inOrder[index++] = root.key;

    // Right recursive call
    printMinMaxOrderUtil(root.right, inOrder);
}

// Function to print the
// Min max order of BST
static void printMinMaxOrder(node root)
{
    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Take auxiliary array for storing
    // The inorder traversal of BST
    int []inOrder = new int[numNode + 1];

    // Function call for printing
    // element in min max order
    printMinMaxOrderUtil(root, inOrder);
    int i = 0;
    index--;

    // While loop for printing elements
    // In front last order
    while (i < index)
    {
        System.out.print(inOrder[i++] + " " +
                         inOrder[index--] + " ");
    }
    if (i == index)
    {
        System.out.println(inOrder[i]);
    }
}

// Driver code
public static void main(String[] args)
{
    node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    printMinMaxOrder(root);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Structure of each node of BST
class Node:
    def __init__(self,key):
        self.left = None
        self.right = None
        self.val = key

def insert(root,node):
    if root is None:
        root = Node(node)
    else:
        if root.val < node:
            if root.right is None:
                root.right = Node(node)
            else:
                insert(root.right, node)
        else:
            if root.left is None:
                root.left = Node(node)
            else:
                insert(root.left, node)

# Function to return the size of the tree
def sizeOfTree(root):

    if root == None:
        return 0

    # Calculate left size recursively
    left = sizeOfTree(root.left)

    # Calculate right size recursively
    right = sizeOfTree(root.right);

    # Return total size recursively
    return (left + right + 1)

# Utility function to print the
# Min max order of BST
def printMinMaxOrderUtil(root, inOrder, index):

    # Base condition
    if root == None:
        return

    # Left recursive call
    printMinMaxOrderUtil(root.left, inOrder, index)

    # Store elements in inorder array
    inOrder[index[0]] = root.val
    index[0] += 1

    # Right recursive call
    printMinMaxOrderUtil(root.right, inOrder, index)

# Function to print the
# Min max order of BST
def printMinMaxOrder(root):

    # Store the size of BST
    numNode = sizeOfTree(root);

    # Take auxiliary array for storing
    # The inorder traversal of BST
    inOrder = [0] * (numNode + 1)
    index = 0

    # Function call for printing
    # element in min max order
    ref = [index]
    printMinMaxOrderUtil(root, inOrder, ref)
    index = ref[0]
    i = 0;
    index -= 1

    # While loop for printing elements
    # In front last order
    while (i < index):

        print (inOrder[i], inOrder[index], end = ' ')
        i += 1
        index -= 1

    if i == index:
        print(inOrder[i])

# Driver Code
root = Node(50)
insert(root, 30)
insert(root, 20)
insert(root, 40)
insert(root, 70)
insert(root, 60)
insert(root, 80)

printMinMaxOrder(root)

# This code is contributed by Sadik Ali
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Structure of each node of BST
class node
{
    public int key;
    public node left, right;
};
static int index;

// A utility function to create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

/* A utility function to insert a new
node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty,
    return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
static int sizeOfTree(node root)
{
    if (root == null)
    {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Utility function to print the
// Min max order of BST
static void printMinMaxOrderUtil(node root,
                                  int []inOrder)
{

    // Base condition
    if (root == null)
    {
        return;
    }

    // Left recursive call
    printMinMaxOrderUtil(root.left, inOrder);

    // Store elements in inorder array
    inOrder[index++] = root.key;

    // Right recursive call
    printMinMaxOrderUtil(root.right, inOrder);
}

// Function to print the
// Min max order of BST
static void printMinMaxOrder(node root)
{
    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Take auxiliary array for storing
    // The inorder traversal of BST
    int []inOrder = new int[numNode + 1];

    // Function call for printing
    // element in min max order
    printMinMaxOrderUtil(root, inOrder);
    int i = 0;
    index--;

    // While loop for printing elements
    // In front last order
    while (i < index)
    {
        Console.Write(inOrder[i++] + " " +
                      inOrder[index--] + " ");
    }
    if (i == index)
    {
        Console.WriteLine(inOrder[i]);
    }
}

// Driver code
public static void Main(String[] args)
{
    node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    printMinMaxOrder(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Structure of each node of BST
class node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

var index = 0;

// A utility function to create a new BST node
function newNode(item)
{
    var temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a new
// node with given key in BST
function insert(node, key)
{

    /* If the tree is empty,
    return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
function sizeOfTree(root)
{
    if (root == null)
    {
        return 0;
    }

    // Calculate left size recursively
    var left = sizeOfTree(root.left);

    // Calculate right size recursively
    var right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Utility function to print the
// Min max order of BST
function printMinMaxOrderUtil(root, inOrder)
{

    // Base condition
    if (root == null)
    {
        return;
    }

    // Left recursive call
    printMinMaxOrderUtil(root.left, inOrder);

    // Store elements in inorder array
    inOrder[index++] = root.key;

    // Right recursive call
    printMinMaxOrderUtil(root.right, inOrder);
}

// Function to print the
// Min max order of BST
function printMinMaxOrder(root)
{

    // Store the size of BST
    var numNode = sizeOfTree(root);

    // Take auxiliary array for storing
    // The inorder traversal of BST
    var inOrder = Array(numNode+1);

    // Function call for printing
    // element in min max order
    printMinMaxOrderUtil(root, inOrder);
    var i = 0;
    index--;

    // While loop for printing elements
    // In front last order
    while (i < index)
    {
        document.write(inOrder[i++] + " " +
                       inOrder[index--] + " ");
    }
    if (i == index)
    {
        document.write(inOrder[i]);
    }
}

// Driver code
var root = null;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);

printMinMaxOrder(root);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
20 80 30 70 40 60 50
```