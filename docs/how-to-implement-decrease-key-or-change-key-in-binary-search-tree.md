# 二叉查找树如何实施降调或改调？

> 原文:[https://www . geesforgeks . org/如何在二进制搜索树中实现减少键或更改键/](https://www.geeksforgeeks.org/how-to-implement-decrease-key-or-change-key-in-binary-search-tree/)

给定一个二叉查找树，编写一个以下面三个为参数的函数:
1)树根
2)旧键值
3)新键值
函数应该将旧键值改为新键值。该函数可能假设旧的键值始终存在于二叉查找树。
**例:**

```
Input: Root of below tree
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 
     Old key value:  40
     New key value:  10

Output: BST should be modified to following
              50
           /     \
          30      70
         /       /  \
       20      60   80  
       /
     10
```

**我们强烈建议您最小化浏览器，先自己试试**
想法是对旧键值调用 delete，然后对新键值调用 insert。下面是 C++实现的思路。

## C++

```
// C++ program to demonstrate decrease
// key operation on binary search tree
#include<bits/stdc++.h>

using namespace std;

class node
{
    public:
    int key;
    node *left, *right;
};

// A utility function to
// create a new BST node
node *newNode(int item)
{
    node *temp = new node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to
// do inorder traversal of BST
void inorder(node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

/* A utility function to insert
a new node with given key in BST */
node* insert(node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree,
return the node with minimum key value
found in that tree. Note that the entire
tree does not need to be searched. */
node * minValueNode(node* Node)
{
    node* current = Node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree and
a key, this function deletes the key
and returns the new root */
node* deleteNode(node* root, int key)
{
    // base case
    if (root == NULL) return root;

    // If the key to be deleted is
    // smaller than the root's key,
    // then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is
    // greater than the root's key,
    // then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's
    // key, then This is the node
    // to be deleted
    else
    {
        // node with only one child or no child
        if (root->left == NULL)
        {
            node *temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL)
        {
            node *temp = root->left;
            free(root);
            return temp;
        }

        // node with two children: Get
        // the inorder successor (smallest
        // in the right subtree)
        node* temp = minValueNode(root->right);

        // Copy the inorder successor's
        // content to this node
        root->key = temp->key;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Function to decrease a key
// value in Binary Search Tree
node *changeKey(node *root, int oldVal, int newVal)
{
    // First delete old key value
    root = deleteNode(root, oldVal);

    // Then insert new key value
    root = insert(root, newVal);

    // Return new root
    return root;
}

// Driver code
int main()
{
    /* Let us create following BST
            50
        / \
        30 70
        / \ / \
    20 40 60 80 */
    node *root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    cout << "Inorder traversal of the given tree \n";
    inorder(root);

    root = changeKey(root, 40, 10);

    /* BST is modified to
            50
        / \
        30 70
        / / \
    20 60 80
    /
    10 */
    cout << "\nInorder traversal of the modified tree \n";
    inorder(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to demonstrate decrease  key operation on binary search tree
#include<stdio.h>
#include<stdlib.h>

struct node
{
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node *newNode(int item)
{
    struct node *temp =  (struct node *)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

/* A utility function to insert a new node with given key in BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left  = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return the node with minimum
   key value found in that tree. Note that the entire tree does not
   need to be searched. */
struct node * minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree and a key, this function deletes the key
   and returns the new root */
struct node* deleteNode(struct node* root, int key)
{
    // base case
    if (root == NULL) return root;

    // If the key to be deleted is smaller than the root's key,
    // then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is greater than the root's key,
    // then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key, then This is the node
    // to be deleted
    else
    {
        // node with only one child or no child
        if (root->left == NULL)
        {
            struct node *temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL)
        {
            struct node *temp = root->left;
            free(root);
            return temp;
        }

        // node with two children: Get the inorder successor (smallest
        // in the right subtree)
        struct node* temp = minValueNode(root->right);

        // Copy the inorder successor's content to this node
        root->key = temp->key;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Function to decrease a key value in Binary Search Tree
struct node *changeKey(struct node *root, int oldVal, int newVal)
{
    //  First delete old key value
    root = deleteNode(root, oldVal);

    // Then insert new key value
    root = insert(root, newVal);

    // Return new root
    return root;
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct node *root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    printf("Inorder traversal of the given tree \n");
    inorder(root);

    root = changeKey(root, 40, 10);

    /* BST is modified to
              50
           /     \
          30      70
         /       /  \
       20      60   80
       /
     10     */
    printf("\nInorder traversal of the modified tree \n");
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate decrease
// key operation on binary search tree
class GfG
{

static class node
{
    int key;
    node left, right;
}
static node root = null;

// A utility function to
// create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to
// do inorder traversal of BST
static void inorder(node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert
a new node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == null) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree,
return the node with minimum key value
found in that tree. Note that the entire
tree does not need to be searched. */
static node minValueNode(node Node)
{
    node current = Node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
        current = current.left;

    return current;
}

/* Given a binary search tree and
a key, this function deletes the key
and returns the new root */
static node deleteNode(node root, int key)
{
    // base case
    if (root == null) return root;

    // If the key to be deleted is
    // smaller than the root's key,
    // then it lies in left subtree
    if (key < root.key)
        root.left = deleteNode(root.left, key);

    // If the key to be deleted is
    // greater than the root's key,
    // then it lies in right subtree
    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    // if key is same as root's
    // key, then This is the node
    // to be deleted
    else
    {
        // node with only one child or no child
        if (root.left == null)
        {
            node temp = root.right;
            return temp;
        }
        else if (root.right == null)
        {
            node temp = root.left;
            return temp;
        }

        // node with two children: Get
        // the inorder successor (smallest
        // in the right subtree)
        node temp = minValueNode(root.right);

        // Copy the inorder successor's
        // content to this node
        root.key = temp.key;

        // Delete the inorder successor
        root.right = deleteNode(root.right, temp.key);
    }
    return root;
}

// Function to decrease a key
// value in Binary Search Tree
static node changeKey(node root, int oldVal, int newVal)
{
    // First delete old key value
    root = deleteNode(root, oldVal);

    // Then insert new key value
    root = insert(root, newVal);

    // Return new root
    return root;
}

// Driver code
public static void main(String[] args)
{
    /* Let us create following BST
            50
        / \
        30 70
        / \ / \
    20 40 60 80 */
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    System.out.println("Inorder traversal of the given tree");
    inorder(root);

    root = changeKey(root, 40, 10);

    /* BST is modified to
            50
        / \
        30 70
        / / \
    20 60 80
    /
    10 */
    System.out.println("\nInorder traversal of the modified tree ");
    inorder(root);
}
}

// This code is contributed by Prerna saini
```

## 蟒蛇 3

```
# Python3 program to demonstrate decrease key
# operation on binary search tree

# A utility function to create a new BST node
class newNode:

    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# A utility function to do inorder
# traversal of BST
def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.key,end=" ")
        inorder(root.right)

# A utility function to insert a new
# node with given key in BST
def insert(node, key):

    # If the tree is empty, return a new node
    if node == None:
        return newNode(key)

    # Otherwise, recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Given a non-empty binary search tree, return
# the node with minimum key value found in that
# tree. Note that the entire tree does not
# need to be searched.
def minValueNode(node):
    current = node

    # loop down to find the leftmost leaf
    while current.left != None:
        current = current.left
    return current

# Given a binary search tree and a key, this
# function deletes the key and returns the new root
def deleteNode(root, key):

    # base case
    if root == None:
        return root

    # If the key to be deleted is smaller than
    # the root's key, then it lies in left subtree
    if key < root.key:
        root.left = deleteNode(root.left, key)

    # If the key to be deleted is greater than
    # the root's key, then it lies in right subtree
    elif key > root.key:
        root.right = deleteNode(root.right, key)

    # if key is same as root's key, then
    # this is the node to be deleted
    else:

        # node with only one child or no child
        if root.left == None:
            temp = root.right
            return temp
        elif root.right == None:
            temp = root.left
            return temp

        # node with two children: Get the inorder
        # successor (smallest in the right subtree)
        temp = minValueNode(root.right)

        # Copy the inorder successor's content
        # to this node
        root.key = temp.key

        # Delete the inorder successor
        root.right = deleteNode(root.right, temp.key)
    return root

# Function to decrease a key value in
# Binary Search Tree
def changeKey(root, oldVal, newVal):

    # First delete old key value
    root = deleteNode(root, oldVal)

    # Then insert new key value
    root = insert(root, newVal)

    # Return new root
    return root

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    #         50
    #     /     \
    #     30     70
    #     / \ / \
    # 20 40 60 80
    root = None
    root = insert(root, 50)
    root = insert(root, 30)
    root = insert(root, 20)
    root = insert(root, 40)
    root = insert(root, 70)
    root = insert(root, 60)
    root = insert(root, 80)

    print("Inorder traversal of the given tree")
    inorder(root)

    root = changeKey(root, 40, 10)
    print()

    # BST is modified to
    #         50
    #     /     \
    #     30     70
    #     /     / \
    # 20     60 80
    # /
    # 10    
    print("Inorder traversal of the modified tree")
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to demonstrate decrease
// key operation on binary search tree
using System;

class GFG
{
public class node
{
    public int key;
    public node left, right;
}
static node root = null;

// A utility function to
// create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to
// do inorder traversal of BST
static void inorder(node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert
a new node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == null) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree,
return the node with minimum key value
found in that tree. Note that the entire
tree does not need to be searched. */
static node minValueNode(node Node)
{
    node current = Node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
        current = current.left;

    return current;
}

/* Given a binary search tree and
a key, this function deletes the key
and returns the new root */
static node deleteNode(node root, int key)
{
    node temp = null;

    // base case
    if (root == null) return root;

    // If the key to be deleted is
    // smaller than the root's key,
    // then it lies in left subtree
    if (key < root.key)
        root.left = deleteNode(root.left, key);

    // If the key to be deleted is
    // greater than the root's key,
    // then it lies in right subtree
    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    // if key is same as root's
    // key, then This is the node
    // to be deleted
    else
    {

        // node with only one child or no child
        if (root.left == null)
        {
            temp = root.right;
            return temp;
        }
        else if (root.right == null)
        {
            temp = root.left;
            return temp;
        }

        // node with two children: Get
        // the inorder successor (smallest
        // in the right subtree)
        temp = minValueNode(root.right);

        // Copy the inorder successor's
        // content to this node
        root.key = temp.key;

        // Delete the inorder successor
        root.right = deleteNode(root.right,
                                 temp.key);
    }
    return root;
}

// Function to decrease a key
// value in Binary Search Tree
static node changeKey(node root, int oldVal,
                                 int newVal)
{
    // First delete old key value
    root = deleteNode(root, oldVal);

    // Then insert new key value
    root = insert(root, newVal);

    // Return new root
    return root;
}

// Driver code
public static void Main(String[] args)
{
    /* Let us create following BST
            50
        / \
        30 70
        / \ / \
    20 40 60 80 */
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    Console.WriteLine("Inorder traversal " +
                      "of the given tree ");
    inorder(root);

    root = changeKey(root, 40, 10);

    /* BST is modified to
            50
        / \
        30 70
        / / \
    20 60 80
    /
    10 */
    Console.WriteLine("\nInorder traversal " +
                      "of the modified tree");
    inorder(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to demonstrate decrease
// key operation on binary search tree

 class node
{
        constructor() {
            this.key = 0;
            this.left = null;
            this.right = null;
        }
    }
 var root = null;

// A utility function to
// create a new BST node
 function newNode(item)
{
    var temp = new node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// A utility function to
// do inorder traversal of BST
function inorder( root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.key + " ");
        inorder(root.right);
    }
}

/* A utility function to insert
a new node with given key in BST */
 function insert( node , key)
{
    /* If the tree is empty, return a new node */
    if (node == null) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree,
return the node with minimum key value
found in that tree. Note that the entire
tree does not need to be searched. */
 function minValueNode( Node)
{
    var current = Node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
        current = current.left;

    return current;
}

/* Given a binary search tree and
a key, this function deletes the key
and returns the new root */
 function deleteNode( root , key)
{
    // base case
    if (root == null) return root;

    // If the key to be deleted is
    // smaller than the root's key,
    // then it lies in left subtree
    if (key < root.key)
        root.left = deleteNode(root.left, key);

    // If the key to be deleted is
    // greater than the root's key,
    // then it lies in right subtree
    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    // if key is same as root's
    // key, then This is the node
    // to be deleted
    else
    {
        // node with only one child or no child
        if (root.left == null)
        {
             temp = root.right;
            return temp;
        }
        else if (root.right == null)
        {
             temp = root.left;
            return temp;
        }

        // node with two children: Get
        // the inorder successor (smallest
        // in the right subtree)
        var temp = minValueNode(root.right);

        // Copy the inorder successor's
        // content to this node
        root.key = temp.key;

        // Delete the inorder successor
        root.right = deleteNode(root.right, temp.key);
    }
    return root;
}

// Function to decrease a key
// value in Binary Search Tree
 function changeKey( root , oldVal , newVal)
{
    // First delete old key value
    root = deleteNode(root, oldVal);

    // Then insert new key value
    root = insert(root, newVal);

    // Return new root
    return root;
}

// Driver code

    /* Let us create following BST
            50
        / \
        30 70
        / \ / \
    20 40 60 80 */
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);   

    document.write(
    "Inorder traversal of the given tree<br/>"
    );
    inorder(root);

    root = changeKey(root, 40, 10);

    /* BST is modified to
            50
        / \
        30 70
        / / \
    20 60 80
    /
    10 */

    document.write(
    "<br/>Inorder traversal of the modified tree <br/>"
    );
    inorder(root);

// This code contributed by aashish1995

</script>
```

**输出:**

```
Inorder traversal of the given tree 
20 30 40 50 60 70 80 
Inorder traversal of the modified tree 
10 20 30 50 60 70 80 
```

上述变化的时间复杂度是 O(h)，其中 h 是 BST 的高度。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息