# 带复制键的 AVL

> 原文:[https://www.geeksforgeeks.org/avl-with-duplicate-keys/](https://www.geeksforgeeks.org/avl-with-duplicate-keys/)

在阅读关于 AVL 树处理重复之前，请参考下面的帖子。
[在二叉查找树如何处理重复？](https://www.geeksforgeeks.org/how-to-handle-duplicates-in-binary-search-tree/)
这是为了扩充 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)节点，将计数与常规字段(如键、左指针和右指针)存储在一起。
在空二叉查找树中插入按键 12、10、20、9、11、10、12、12 将创建以下内容。

```
          12(3)
       /        \
     10(2)      20(1)
    /    \       
 9(1)   11(1)   
```

括号
中显示了一个键的计数，下面是普通 AVL 树的实现，每个键都有计数。该代码基本取自 AVL 树中的[插入删除代码。为处理重复项所做的更改被突出显示，其余代码相同。
需要注意的重要一点是，变化非常类似于简单的二叉查找树变化。](https://www.geeksforgeeks.org/avl-tree-set-2-deletion/) 

## C++

```
// C++ program of AVL tree that
// handles duplicates
#include <bits/stdc++.h>
using namespace std;

// An AVL tree node
struct node {
    int key;
    struct node* left;
    struct node* right;
    int height;
    int count;
};

// A utility function to get maximum of two integers
int max(int a, int b);

// A utility function to get height of the tree
int height(struct node* N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// A utility function to get maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

/* Helper function that allocates a new node with the given key and
    NULL left and right pointers. */
struct node* newNode(int key)
{
    struct node* node = (struct node*)
        malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    node->height = 1; // new node is initially added at leaf
    node->count = 1;
    return (node);
}

// A utility function to right rotate subtree rooted with y
// See the diagram given above.
struct node* rightRotate(struct node* y)
{
    struct node* x = y->left;
    struct node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// A utility function to left rotate subtree rooted with x
// See the diagram given above.
struct node* leftRotate(struct node* x)
{
    struct node* y = x->right;
    struct node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(struct node* N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

struct node* insert(struct node* node, int key)
{
    /* 1.  Perform the normal BST rotation */
    if (node == NULL)
        return (newNode(key));

    // If key already exists in BST, increment count and return
    if (key == node->key) {
        (node->count)++;
        return node;
    }

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* 2\. Update height of this ancestor node */
    node->height = max(height(node->left), height(node->right)) + 1;

    /* 3\. Get the balance factor of this ancestor node to check whether
       this node became unbalanced */
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return the node with minimum
   key value found in that tree. Note that the entire tree does not
   need to be searched. */
struct node* minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

struct node* deleteNode(struct node* root, int key)
{
    // STEP 1: PERFORM STANDARD BST DELETE

    if (root == NULL)
        return root;

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
    else {
        // If key is present more than once, simply decrement
        // count and return
        if (root->count > 1) {
            (root->count)--;
            return NULL;
        }
        // Else, delete the node

        // node with only one child or no child
        if ((root->left == NULL) || (root->right == NULL)) {
            struct node* temp = root->left ? root->left : root->right;

            // No child case
            if (temp == NULL) {
                temp = root;
                root = NULL;
            }
            else // One child case
                *root = *temp; // Copy the contents of the non-empty child

            free(temp);
        }
        else {
            // node with two children: Get the inorder successor (smallest
            // in the right subtree)
            struct node* temp = minValueNode(root->right);

            // Copy the inorder successor's data to this node and update the count
            root->key = temp->key;
            root->count = temp->count;
            temp->count = 1;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == NULL)
        return root;

    // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
    root->height = max(height(root->left), height(root->right)) + 1;

    // STEP 3: GET THE BALANCE FACTOR OF THIS NODE (to check whether
    // this node became unbalanced)
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// A utility function to print preorder traversal of the tree.
// The function also prints height of every node
void preOrder(struct node* root)
{
    if (root != NULL) {
        cout << root->key << "("<<root->count << ")"<< " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

/* Driver program to test above function*/
int main()
{
    struct node* root = NULL;

    /* Constructing tree given in the above figure */
    root = insert(root, 9);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 5);
    root = insert(root, 9);
    root = insert(root, 7);
    root = insert(root, 17);

    cout <<"Pre order traversal of the constructed AVL tree is \n";
    preOrder(root);

    cout <<"\nPre order traversal after deletion of 9 \n";
    preOrder(root);

    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// C++ program of AVL tree that
// handles duplicates
#include <stdio.h>
#include <stdlib.h>

// An AVL tree node
struct node {
    int key;
    struct node* left;
    struct node* right;
    int height;
    int count;
};

// A utility function to get maximum of two integers
int max(int a, int b);

// A utility function to get height of the tree
int height(struct node* N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// A utility function to get maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

/* Helper function that allocates a new node with the given key and
    NULL left and right pointers. */
struct node* newNode(int key)
{
    struct node* node = (struct node*)
        malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    node->height = 1; // new node is initially added at leaf
    node->count = 1;
    return (node);
}

// A utility function to right rotate subtree rooted with y
// See the diagram given above.
struct node* rightRotate(struct node* y)
{
    struct node* x = y->left;
    struct node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// A utility function to left rotate subtree rooted with x
// See the diagram given above.
struct node* leftRotate(struct node* x)
{
    struct node* y = x->right;
    struct node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(struct node* N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

struct node* insert(struct node* node, int key)
{
    /* 1.  Perform the normal BST rotation */
    if (node == NULL)
        return (newNode(key));

    // If key already exists in BST, increment count and return
    if (key == node->key) {
        (node->count)++;
        return node;
    }

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* 2\. Update height of this ancestor node */
    node->height = max(height(node->left), height(node->right)) + 1;

    /* 3\. Get the balance factor of this ancestor node to check whether
       this node became unbalanced */
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return the node with minimum
   key value found in that tree. Note that the entire tree does not
   need to be searched. */
struct node* minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

struct node* deleteNode(struct node* root, int key)
{
    // STEP 1: PERFORM STANDARD BST DELETE

    if (root == NULL)
        return root;

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
    else {
        // If key is present more than once, simply decrement
        // count and return
        if (root->count > 1) {
            (root->count)--;
            return NULL;
        }
        // Else, delete the node

        // node with only one child or no child
        if ((root->left == NULL) || (root->right == NULL)) {
            struct node* temp = root->left ? root->left : root->right;

            // No child case
            if (temp == NULL) {
                temp = root;
                root = NULL;
            }
            else // One child case
                *root = *temp; // Copy the contents of the non-empty child

            free(temp);
        }
        else {
            // node with two children: Get the inorder successor (smallest
            // in the right subtree)
            struct node* temp = minValueNode(root->right);

            // Copy the inorder successor's data to this node and update the count
            root->key = temp->key;
            root->count = temp->count;
            temp->count = 1;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == NULL)
        return root;

    // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
    root->height = max(height(root->left), height(root->right)) + 1;

    // STEP 3: GET THE BALANCE FACTOR OF THIS NODE (to check whether
    // this node became unbalanced)
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// A utility function to print preorder traversal of the tree.
// The function also prints height of every node
void preOrder(struct node* root)
{
    if (root != NULL) {
        printf("%d(%d) ", root->key, root->count);
        preOrder(root->left);
        preOrder(root->right);
    }
}

/* Driver program to test above function*/
int main()
{
    struct node* root = NULL;

    /* Constructing tree given in the above figure */
    root = insert(root, 9);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 5);
    root = insert(root, 9);
    root = insert(root, 7);
    root = insert(root, 17);

    printf("Pre order traversal of the constructed AVL tree is \n");
    preOrder(root);

    root = deleteNode(root, 9);

    printf("\nPre order traversal after deletion of 9 \n");
    preOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of AVL tree that handles duplicates
import java.util.*;

class solution {

    // An AVL tree node
    static class node {
        int key;
        node left;
        node right;
        int height;
        int count;
    }

    // A utility function to get height of the tree
    static int height(node N)
    {
        if (N == null)
            return 0;
        return N.height;
    }

    // A utility function to get maximum of two integers
    static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    /* Helper function that allocates a new node with the given key and 
    null left and right pointers. */
    static node newNode(int key)
    {
        node node = new node();
        node.key = key;
        node.left = null;
        node.right = null;
        node.height = 1; // new node is initially added at leaf
        node.count = 1;
        return (node);
    }

    // A utility function to right rotate subtree rooted with y
    // See the diagram given above.
    static node rightRotate(node y)
    {
        node x = y.left;
        node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = max(height(y.left), height(y.right)) + 1;
        x.height = max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // A utility function to left rotate subtree rooted with x
    // See the diagram given above.
    static node leftRotate(node x)
    {
        node y = x.right;
        node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = max(height(x.left), height(x.right)) + 1;
        y.height = max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Get Balance factor of node N
    static int getBalance(node N)
    {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    static node insert(node node, int key)
    {
        /*1.  Perform the normal BST rotation */
        if (node == null)
            return (newNode(key));

        // If key already exists in BST, increment count and return
        if (key == node.key) {
            (node.count)++;
            return node;
        }

        /* Otherwise, recur down the tree */
        if (key < node.key)
            node.left = insert(node.left, key);
        else
            node.right = insert(node.right, key);

        /* 2\. Update height of this ancestor node */
        node.height = max(height(node.left), height(node.right)) + 1;

        /* 3\. Get the balance factor of this ancestor node to check whether 
       this node became unbalanced */
        int balance = getBalance(node);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    /* Given a non-empty binary search tree, return the node with minimum 
   key value found in that tree. Note that the entire tree does not 
   need to be searched. */
    static node minValueNode(node node)
    {
        node current = node;

        /* loop down to find the leftmost leaf */
        while (current.left != null)
            current = current.left;

        return current;
    }

    static node deleteNode(node root, int key)
    {
        // STEP 1: PERFORM STANDARD BST DELETE

        if (root == null)
            return root;

        // If the key to be deleted is smaller than the root's key,
        // then it lies in left subtree
        if (key < root.key)
            root.left = deleteNode(root.left, key);

        // If the key to be deleted is greater than the root's key,
        // then it lies in right subtree
        else if (key > root.key)
            root.right = deleteNode(root.right, key);

        // if key is same as root's key, then This is the node
        // to be deleted
        else {
            // If key is present more than once, simply decrement
            // count and return
            if (root.count > 1) {
                (root.count)--;
                return null;
            }
            // ElSE, delete the node

            // node with only one child or no child
            if ((root.left == null) || (root.right == null)) {
                node temp = root.left != null ? root.left : root.right;

                // No child case
                if (temp == null) {
                    temp = root;
                    root = null;
                }
                else // One child case
                    root = temp; // Copy the contents of the non-empty child
            }
            else {
                // node with two children: Get the inorder successor (smallest
                // in the right subtree)
                node temp = minValueNode(root.right);

                // Copy the inorder successor's data to this node and update the count
                root.key = temp.key;
                root.count = temp.count;
                temp.count = 1;

                // Delete the inorder successor
                root.right = deleteNode(root.right, temp.key);
            }
        }

        // If the tree had only one node then return
        if (root == null)
            return root;

        // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
        root.height = max(height(root.left), height(root.right)) + 1;

        // STEP 3: GET THE BALANCE FACTOR OF THIS NODE (to check whether
        // this node became unbalanced)
        int balance = getBalance(root);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && getBalance(root.left) >= 0)
            return rightRotate(root);

        // Left Right Case
        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        // Right Right Case
        if (balance < -1 && getBalance(root.right) <= 0)
            return leftRotate(root);

        // Right Left Case
        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    // A utility function to print preorder traversal of the tree.
    // The function also prints height of every node
    static void preOrder(node root)
    {
        if (root != null) {
            System.out.printf("%d(%d) ", root.key, root.count);
            preOrder(root.left);
            preOrder(root.right);
        }
    }

    /* Driver program to test above function*/
    public static void main(String args[])
    {
        node root = null;

        /* Coning tree given in the above figure */
        root = insert(root, 9);
        root = insert(root, 5);
        root = insert(root, 10);
        root = insert(root, 5);
        root = insert(root, 9);
        root = insert(root, 7);
        root = insert(root, 17);

        System.out.printf("Pre order traversal of the constructed AVL tree is \n");
        preOrder(root);

        deleteNode(root, 9);

        System.out.printf("\nPre order traversal after deletion of 9 \n");
        preOrder(root);
    }
}
// contributed by Arnab Kundu
```

## C#

```
// C# program of AVL tree that
// handles duplicates
using System;

class GFG {

    // An AVL tree node
    class node {
        public int key;
        public node left;
        public node right;
        public int height;
        public int count;
    }

    // A utility function to get
    // height of the tree
    static int height(node N)
    {
        if (N == null)
            return 0;
        return N.height;
    }

    // A utility function to get
    // maximum of two integers
    static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    /* Helper function that allocates a 
    new node with the given key and 
    null left and right pointers. */
    static node newNode(int key)
    {
        node node = new node();
        node.key = key;
        node.left = null;
        node.right = null;
        node.height = 1; // new node is initially
        // added at leaf
        node.count = 1;
        return (node);
    }

    // A utility function to right
    // rotate subtree rooted with y
    // See the diagram given above.
    static node rightRotate(node y)
    {
        node x = y.left;
        node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = max(height(y.left),
                       height(y.right))
                   + 1;
        x.height = max(height(x.left),
                       height(x.right))
                   + 1;

        // Return new root
        return x;
    }

    // A utility function to left
    // rotate subtree rooted with x
    // See the diagram given above.
    static node leftRotate(node x)
    {
        node y = x.right;
        node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = max(height(x.left),
                       height(x.right))
                   + 1;
        y.height = max(height(y.left),
                       height(y.right))
                   + 1;

        // Return new root
        return y;
    }

    // Get Balance factor of node N
    static int getBalance(node N)
    {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    static node insert(node node, int key)
    {
        /*1\. Perform the normal BST rotation */
        if (node == null)
            return (newNode(key));

        // If key already exists in BST,
        // increment count and return
        if (key == node.key) {
            (node.count)++;
            return node;
        }

        /* Otherwise, recur down the tree */
        if (key < node.key)
            node.left = insert(node.left, key);
        else
            node.right = insert(node.right, key);

        /* 2\. Update height of this 
          ancestor node */
        node.height = max(height(node.left),
                          height(node.right))
                      + 1;

        /* 3\. Get the balance factor of 
    this ancestor node to check whether 
    this node became unbalanced */
        int balance = getBalance(node);

        // If this node becomes unbalanced,
        // then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        /* return the (unchanged)
       node pointer */
        return node;
    }

    /* Given a non-empty binary search 
   tree, return the node with minimum 
   key value found in that tree. Note 
   that the entire tree does not 
   need to be searched. */
    static node minValueNode(node node)
    {
        node current = node;

        /* loop down to find the
       leftmost leaf */
        while (current.left != null)
            current = current.left;

        return current;
    }

    static node deleteNode(node root, int key)
    {
        // STEP 1: PERFORM STANDARD BST DELETE
        if (root == null)
            return root;

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

        // if key is same as root's key,
        // then this is the node to be deleted
        else {
            // If key is present more than
            // once, simply decrement
            // count and return
            if (root.count > 1) {
                (root.count)--;
                return null;
            }

            // ElSE, delete the node

            // node with only one child
            // or no child
            if ((root.left == null) || (root.right == null)) {
                node temp = root.left != null ? root.left : root.right;

                // No child case
                if (temp == null) {
                    temp = root;
                    root = null;
                }
                else // One child case
                    root = temp; // Copy the contents of
                // the non-empty child
            }
            else {
                // node with two children: Get
                // the inorder successor (smallest
                // in the right subtree)
                node temp = minValueNode(root.right);

                // Copy the inorder successor's
                // data to this node and update the count
                root.key = temp.key;
                root.count = temp.count;
                temp.count = 1;

                // Delete the inorder successor
                root.right = deleteNode(root.right,
                                        temp.key);
            }
        }

        // If the tree had only one
        // node then return
        if (root == null)
            return root;

        // STEP 2: UPDATE HEIGHT OF
        // THE CURRENT NODE
        root.height = max(height(root.left),
                          height(root.right))
                      + 1;

        // STEP 3: GET THE BALANCE FACTOR
        // OF THIS NODE (to check whether
        // this node became unbalanced)
        int balance = getBalance(root);

        // If this node becomes unbalanced,
        // then there are 4 cases

        // Left Left Case
        if (balance > 1 && getBalance(root.left) >= 0)
            return rightRotate(root);

        // Left Right Case
        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        // Right Right Case
        if (balance < -1 && getBalance(root.right) <= 0)
            return leftRotate(root);

        // Right Left Case
        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    // A utility function to print
    // preorder traversal of the tree.
    // The function also prints height
    // of every node
    static void preOrder(node root)
    {
        if (root != null) {
            Console.Write(root.key + "(" + root.count + ") ");
            preOrder(root.left);
            preOrder(root.right);
        }
    }

    // Driver Code
    static public void Main(String[] args)
    {
        node root = null;

        /* Coning tree given in 
       the above figure */
        root = insert(root, 9);
        root = insert(root, 5);
        root = insert(root, 10);
        root = insert(root, 5);
        root = insert(root, 9);
        root = insert(root, 7);
        root = insert(root, 17);

        Console.Write("Pre order traversal of "
                      + "the constructed AVL tree is \n");
        preOrder(root);

        deleteNode(root, 9);

        Console.Write("\nPre order traversal after "
                      + "deletion of 9 \n");
        preOrder(root);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python code to delete a node in AVL tree
# Generic tree node class

class TreeNode():
    def __init__(self, val):
        self.count = 1    # assigning count variable so that during insertion in will be incremented for duplicate values
        # and during deletion, it will be decremented if has multiple copies.
        self.height = 1
        self.val = val
        self.left = None
        self.right = None
# only insertion and deletion will be affected. if multiple copies are there, entry(count) will be printed during traversal.

# AVL tree class which supports insertion,
# deletion operations

class AVL_Tree(object):

    def insert(self, root, key):

        # Step 1 - Perform normal BST
        if not root:
            return TreeNode(key)
        elif key < root.val:
            root.left = self.insert(root.left, key)
        elif key > root.val:
            root.right = self.insert(root.right, key)
        else:
            root.count += 1  # incrementing count if same entry is inserted.

        # Step 2 - Update the height of the
        # ancestor node
        root.height = 1 + max(self.getHeight(root.left),
                              self.getHeight(root.right))

        # Step 3 - Get the balance factor
        balance = self.getBalance(root)

        # Step 4 - If the node is unbalanced,
        # then try out the 4 cases
        # Case 1 - Left Left
        if balance > 1 and key < root.left.val:
            return self.rightRotate(root)

        # Case 2 - Right Right
        if balance < -1 and key > root.right.val:
            return self.leftRotate(root)

        # Case 3 - Left Right
        if balance > 1 and key > root.left.val:
            root.left = self.leftRotate(root.left)
            return self.rightRotate(root)

        # Case 4 - Right Left
        if balance < -1 and key < root.right.val:
            root.right = self.rightRotate(root.right)
            return self.leftRotate(root)

        return root

    # Recursive function to delete a node with
    # given key from subtree with given root.
    # It returns root of the modified subtree.
    def delete(self, root, key):

        # Step 1 - Perform standard BST delete
        if not root:
            return root

        elif key < root.val:
            root.left = self.delete(root.left, key)

        elif key > root.val:
            root.right = self.delete(root.right, key)

        else:
            if root.count > 1:  # if count is more than one i.e multiple copies are there
                root.count -= 1  # just decrement count
                return root   # so that one copy will be deleted and return

            if root.left is None:
                temp = root.right
                root = None
                return temp

            elif root.right is None:
                temp = root.left
                root = None
                return temp

            temp = self.getMinValueNode(root.right)
            root.val = temp.val
            root.right = self.delete(root.right,
                                     temp.val)

        # If the tree has only one node,
        # simply return it
        if root is None:
            return root

        # Step 2 - Update the height of the
        # ancestor node
        root.height = 1 + max(self.getHeight(root.left),
                              self.getHeight(root.right))

        # Step 3 - Get the balance factor
        balance = self.getBalance(root)

        # Step 4 - If the node is unbalanced,
        # then try out the 4 cases
        # Case 1 - Left Left
        if balance > 1 and self.getBalance(root.left) >= 0:
            return self.rightRotate(root)

        # Case 2 - Right Right
        if balance < -1 and self.getBalance(root.right) <= 0:
            return self.leftRotate(root)

        # Case 3 - Left Right
        if balance > 1 and self.getBalance(root.left) < 0:
            root.left = self.leftRotate(root.left)
            return self.rightRotate(root)

        # Case 4 - Right Left
        if balance < -1 and self.getBalance(root.right) > 0:
            root.right = self.rightRotate(root.right)
            return self.leftRotate(root)

        return root

    def leftRotate(self, z):

        y = z.right
        T2 = y.left

        # Perform rotation
        y.left = z
        z.right = T2

        # Update heights
        z.height = 1 + max(self.getHeight(z.left),
                           self.getHeight(z.right))
        y.height = 1 + max(self.getHeight(y.left),
                           self.getHeight(y.right))

        # Return the new root
        return y

    def rightRotate(self, z):

        y = z.left
        T3 = y.right

        # Perform rotation
        y.right = z
        z.left = T3

        # Update heights
        z.height = 1 + max(self.getHeight(z.left),
                           self.getHeight(z.right))
        y.height = 1 + max(self.getHeight(y.left),
                           self.getHeight(y.right))

        # Return the new root
        return y

    def getHeight(self, root):
        if not root:
            return 0

        return root.height

    def getBalance(self, root):
        if not root:
            return 0

        return self.getHeight(root.left) - self.getHeight(root.right)

    def getMinValueNode(self, root):
        if root is None or root.left is None:
            return root

        return self.getMinValueNode(root.left)

    def preOrder(self, root):

        if not root:
            return

        print("{}({}) ".format(root.val, root.count), end="")
        self.preOrder(root.left)
        self.preOrder(root.right)

myTree = AVL_Tree()
root = None
nums = [9, 5, 10, 5, 9, 7, 17]

for num in nums:
    root = myTree.insert(root, num)

# Preorder Traversal
print("Preorder Traversal after insertion -")
myTree.preOrder(root)
print()

# Delete
key = 10
root = myTree.delete(root, key)
key = 10
root = myTree.delete(root, key)
key = -1
root = myTree.delete(root, key)
key = 0
root = myTree.delete(root, key)

# Preorder Traversal
print("Preorder Traversal after deletion -")
myTree.preOrder(root)
print()

# This code is contributed by Ajitesh Pathak
```

## java 描述语言

```
<script>

    // JavaScript program of AVL tree that handles duplicates

    class Node
    {
        constructor() {
           this.left;
           this.right;
           this.key;
           this.height;
           this.count;
        }
    }

    // A utility function to get height of the tree
    function height(N)
    {
        if (N == null)
            return 0;
        return N.height;
    }

    // A utility function to get maximum of two integers
    function max(a, b)
    {
        return (a > b) ? a : b;
    }

    /* Helper function that allocates a new 
    node with the given key and
    null left and right pointers. */
    function newNode(key)
    {
        let node = new Node();
        node.key = key;
        node.left = null;
        node.right = null;
        node.height = 1; // new node is initially added at leaf
        node.count = 1;
        return (node);
    }

    // A utility function to right rotate
    // subtree rooted with y
    // See the diagram given above.
    function rightRotate(y)
    {
        let x = y.left;
        let T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = max(height(y.left), height(y.right)) + 1;
        x.height = max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // A utility function to left rotate subtree rooted with x
    // See the diagram given above.
    function leftRotate(x)
    {
        let y = x.right;
        let T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = max(height(x.left), height(x.right)) + 1;
        y.height = max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Get Balance factor of node N
    function getBalance(N)
    {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    function insert(node, key)
    {
        /*1.  Perform the normal BST rotation */
        if (node == null)
            return (newNode(key));

        // If key already exists in BST, increment count and return
        if (key == node.key) {
            (node.count)++;
            return node;
        }

        /* Otherwise, recur down the tree */
        if (key < node.key)
            node.left = insert(node.left, key);
        else
            node.right = insert(node.right, key);

        /* 2\. Update height of this ancestor node */
        node.height = max(height(node.left), height(node.right)) + 1;

        /* 3\. Get the balance factor of this 
        ancestor node to check whether
        this node became unbalanced */
        let balance = getBalance(node);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    /* Given a non-empty binary search tree,
       return the node with minimum
       key value found in that tree. Note that 
       the entire tree does not
       need to be searched. */
    function minValueNode(node)
    {
        let current = node;

        /* loop down to find the leftmost leaf */
        while (current.left != null)
            current = current.left;

        return current;
    }

    function deleteNode(root, key)
    {
        // STEP 1: PERFORM STANDARD BST DELETE

        if (root == null)
            return root;

        // If the key to be deleted is smaller than the root's key,
        // then it lies in left subtree
        if (key < root.key)
            root.left = deleteNode(root.left, key);

        // If the key to be deleted is greater than the root's key,
        // then it lies in right subtree
        else if (key > root.key)
            root.right = deleteNode(root.right, key);

        // if key is same as root's key, then This is the node
        // to be deleted
        else {
            // If key is present more than once, simply decrement
            // count and return
            if (root.count > 1) {
                (root.count)--;
                return null;
            }
            // ElSE, delete the node

            // node with only one child or no child
            if ((root.left == null) || (root.right == null)) {
                let temp = root.left != null ? root.left : root.right;

                // No child case
                if (temp == null) {
                    temp = root;
                    root = null;
                }
                else // One child case
                // Copy the contents of the non-empty child
                    root = temp; 
            }
            else {
                // node with two children: Get the
                // inorder successor (smallest
                // in the right subtree)
                let temp = minValueNode(root.right);

                // Copy the inorder successor's data to
                // this node and update the count
                root.key = temp.key;
                root.count = temp.count;
                temp.count = 1;

                // Delete the inorder successor
                root.right = deleteNode(root.right, temp.key);
            }
        }

        // If the tree had only one node then return
        if (root == null)
            return root;

        // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
        root.height = max(height(root.left), height(root.right)) + 1;

        // STEP 3: GET THE BALANCE FACTOR 
        // OF THIS NODE (to check whether
        // this node became unbalanced)
        let balance = getBalance(root);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && getBalance(root.left) >= 0)
            return rightRotate(root);

        // Left Right Case
        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        // Right Right Case
        if (balance < -1 && getBalance(root.right) <= 0)
            return leftRotate(root);

        // Right Left Case
        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    // A utility function to print preorder traversal of the tree.
    // The function also prints height of every node
    function preOrder(root)
    {
        if (root != null) {
            document.write(root.key + "(" + root.count + ") ");
            preOrder(root.left);
            preOrder(root.right);
        }
    }

    let root = null;

    /* Coning tree given in the above figure */
    root = insert(root, 9);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 5);
    root = insert(root, 9);
    root = insert(root, 7);
    root = insert(root, 17);

    document.write(
    "Pre order traversal of the constructed AVL tree is " + 
    "</br>");
    preOrder(root);

    deleteNode(root, 9);

    document.write(
    "</br>" + "Pre order traversal after deletion of 9 " + 
    "</br>");
    preOrder(root);

</script>
```

**输出:**

```
Pre order traversal of the constructed AVL tree is
9(2) 5(2) 7(1) 10(1) 17(1)
Pre order traversal after deletion of 9
9(1) 5(2) 7(1) 10(1) 17(1) 
```

感谢**Rounaq jhunchunu Wala**分享初始代码。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息