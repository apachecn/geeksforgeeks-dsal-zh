# 在二叉查找树如何处理重复？

> 原文:[https://www . geesforgeks . org/如何处理二进制搜索树中的重复项/](https://www.geeksforgeeks.org/how-to-handle-duplicates-in-binary-search-tree/)

在二叉查找树树中，一个键的左子树中的所有键必须更小，右子树中的所有键必须更大。因此，根据定义，二叉查找树有不同的键。
如何允许重复，每次插入插入一个有值的键，每次删除删除一个匹配项？
一个**简单的解决方案**是允许右侧有相同的按键(我们也可以选择左侧)。例如，考虑在空二叉查找树中插入键 12、10、20、9、11、10、12、12

```
          12
       /     \
     10      20
    /  \     /
   9   11   12 
      /      \
    10       12
```

一个**更好的解决方案**是增加每个树节点，将计数与常规字段(如键、左指针和右指针)存储在一起。
在一个空的二叉查找树中插入 12、10、20、9、11、10、12、12 号键将创建以下内容。

```
          12(3)
       /        \
     10(2)      20(1)
    /    \       
 9(1)   11(1)   

Count of a key is shown in bracket
```

与上述简单方法相比，该方法具有以下优点。
**1)** 树高小，不考虑重复数。请注意，大多数 BST 操作(搜索、插入和删除)的时间复杂度为 O(h)，其中 h 是 BST 的高度。因此，如果我们能够保持较小的高度，我们就可以减少关键比较的次数。
**2)** 搜索、插入和删除变得更加容易。我们可以使用相同的插入、搜索和删除算法，只需稍加修改(见下面的代码)。
**3)** 这种方法也适用于自平衡 BST([AVL 树](https://www.geeksforgeeks.org/archives/17679)、[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)等)。这些树涉及旋转，并且旋转可能违反简单解的 BST 属性，因为旋转后相同的键可以在左侧或右侧。
下面是普通二叉查找树的实现，每个按键都有计数。该代码基本取自[代码，用于在](http://geeksquiz.com/binary-search-tree-set-2-delete/)中插入和删除。为处理重复项所做的更改被突出显示，其余代码相同。

## C++

```
// C++ program to implement basic operations
// (search, insert and delete) on a BST that
// handles duplicates by storing count with
// every node
#include<bits/stdc++.h>
using namespace std;

struct node
{
    int key;
    int count;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node *newNode(int item)
{
    struct node *temp = (struct node *)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    temp->count = 1;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        cout << root->key << "("
             << root->count << ") ";
        inorder(root->right);
    }
}

/* A utility function to insert a new
node with given key in BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    // If key already exists in BST,
    // increment count and return
    if (key == node->key)
    {
    (node->count)++;
        return node;
    }

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return
the node with minimum key value found in that
tree. Note that the entire tree does not need
to be searched. */
struct node * minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree and a key,
this function deletes a given key and
returns root of modified tree */
struct node* deleteNode(struct node* root,
                                 int key)
{
    // base case
    if (root == NULL) return root;

    // If the key to be deleted is smaller than the
    // root's key, then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is greater than
    // the root's key, then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key
    else
    {
        // If key is present more than once,
        // simply decrement count and return
        if (root->count > 1)
        {
            (root->count)--;
            return root;
        }

        // ElSE, delete the node

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

        // node with two children: Get the inorder
        // successor (smallest in the right subtree)
        struct node* temp = minValueNode(root->right);

        // Copy the inorder successor's
        // content to this node
        root->key = temp->key;
        root->count = temp->count;

          // To ensure successor gets deleted by
          // deleteNode call, set count to 0.
          temp->count = 0;

        // Delete the inorder successor
        root->right = deleteNode(root->right,
                                  temp->key);
    }
    return root;
}

// Driver Code
int main()
{
    /* Let us create following BST
            12(3)
        /     \
    10(2)     20(1)
    / \
    9(1) 11(1) */
    struct node *root = NULL;
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 9);
    root = insert(root, 11);
    root = insert(root, 10);
    root = insert(root, 12);
    root = insert(root, 12);

    cout << "Inorder traversal of the given tree "
         << endl;
    inorder(root);

    cout << "\nDelete 20\n";
    root = deleteNode(root, 20);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    cout << "\nDelete 12\n" ;
    root = deleteNode(root, 12);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    cout << "\nDelete 9\n";
    root = deleteNode(root, 9);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    return 0;
}

// This code is contributed by Akanksha Rai
```

## C

```
// C program to implement basic operations (search, insert and delete)
// on a BST that handles duplicates by storing count with every node
#include<stdio.h>
#include<stdlib.h>

struct node
{
    int key;
    int count;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node *newNode(int item)
{
    struct node *temp =  (struct node *)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    temp->count = 1;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d(%d) ", root->key, root->count);
        inorder(root->right);
    }
}

/* A utility function to insert a new node with given key in BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    // If key already exists in BST, increment count and return
    if (key == node->key)
    {
       (node->count)++;
        return node;
    }

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left  = insert(node->left, key);
    else
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return the node with
   minimum key value found in that tree. Note that the entire
   tree does not need to be searched. */
struct node * minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree and a key, this function
   deletes a given key and returns root of modified tree */
struct node* deleteNode(struct node* root, int key)
{
    // base case
    if (root == NULL) return root;

    // If the key to be deleted is smaller than the
    // root's key, then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is greater than the root's key,
    // then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key
    else
    {
        // If key is present more than once, simply decrement
        // count and return
        if (root->count > 1)
        {
           (root->count)--;
           return root;
        }

        // ElSE, delete the node

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
        root->count = temp->count;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
             12(3)
          /        \
       10(2)      20(1)
       /   \
    9(1)  11(1)   */
    struct node *root = NULL;
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 9);
    root = insert(root, 11);
    root = insert(root, 10);
    root = insert(root, 12);
    root = insert(root, 12);

    printf("Inorder traversal of the given tree \n");
    inorder(root);

    printf("\nDelete 20\n");
    root = deleteNode(root, 20);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 12\n");
    root = deleteNode(root, 12);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 9\n");
    root = deleteNode(root, 9);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement basic operations
// (search, insert and delete) on a BST that
// handles duplicates by storing count with
// every node
class GFG
{
static class node
{
    int key;
    int count;
    node left, right;
};

// A utility function to create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    temp.count = 1;
    return temp;
}

// A utility function to do inorder traversal of BST
static void inorder(node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print(root.key + "(" +
                         root.count + ") ");
        inorder(root.right);
    }
}

/* A utility function to insert a new
node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == null) return newNode(key);

    // If key already exists in BST,
    // increment count and return
    if (key == node.key)
    {
    (node.count)++;
        return node;
    }

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return
the node with minimum key value found in that
tree. Note that the entire tree does not need
to be searched. */
static node minValueNode(node node)
{
    node current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
        current = current.left;

    return current;
}

/* Given a binary search tree and a key,
this function deletes a given key and
returns root of modified tree */
static node deleteNode(node root, int key)
{
    // base case
    if (root == null) return root;

    // If the key to be deleted is smaller than the
    // root's key, then it lies in left subtree
    if (key < root.key)
        root.left = deleteNode(root.left, key);

    // If the key to be deleted is greater than
    // the root's key, then it lies in right subtree
    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    // if key is same as root's key
    else
    {
        // If key is present more than once,
        // simply decrement count and return
        if (root.count > 1)
        {
            (root.count)--;
            return root;
        }

        // ElSE, delete the node

        // node with only one child or no child
        if (root.left == null)
        {
            node temp = root.right;
            root=null;
            return temp;
        }
        else if (root.right == null)
        {
            node temp = root.left;
            root = null;
            return temp;
        }

        // node with two children: Get the inorder
        // successor (smallest in the right subtree)
        node temp = minValueNode(root.right);

        // Copy the inorder successor's
        // content to this node
        root.key = temp.key;
        root.count = temp.count;

        // Delete the inorder successor
        root.right = deleteNode(root.right,
                                temp.key);
    }
    return root;
}

// Driver Code
public static void main(String[] args)
{
    /* Let us create following BST
            12(3)
        /     \
    10(2)     20(1)
    / \
    9(1) 11(1) */
    node root = null;
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 9);
    root = insert(root, 11);
    root = insert(root, 10);
    root = insert(root, 12);
    root = insert(root, 12);

    System.out.print("Inorder traversal of " +
                     "the given tree " + "\n");
    inorder(root);

    System.out.print("\nDelete 20\n");
    root = deleteNode(root, 20);
    System.out.print("Inorder traversal of " +
                     "the modified tree \n");
    inorder(root);

    System.out.print("\nDelete 12\n");
    root = deleteNode(root, 12);
    System.out.print("Inorder traversal of " +
                     "the modified tree \n");
    inorder(root);

    System.out.print("\nDelete 9\n");
    root = deleteNode(root, 9);
    System.out.print("Inorder traversal of " +
                     "the modified tree \n");
    inorder(root);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement basic operations
# (search, insert and delete) on a BST that handles
# duplicates by storing count with every node

# A utility function to create a new BST node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.count = 1
        self.left = None
        self.right = None

# A utility function to do inorder
# traversal of BST
def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.key,"(", root.count,")",
                                 end = " ")
        inorder(root.right)

# A utility function to insert a new node
# with given key in BST
def insert(node, key):

    # If the tree is empty, return a new node
    if node == None:
        k = newNode(key)
        return k

    # If key already exists in BST, increment
    # count and return
    if key == node.key:
        (node.count) += 1
        return node

    # Otherwise, recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Given a non-empty binary search tree, return
# the node with minimum key value found in that
# tree. Note that the entire tree does not need
# to be searched.
def minValueNode(node):
    current = node

    # loop down to find the leftmost leaf
    while current.left != None:
        current = current.left

    return current

# Given a binary search tree and a key,
# this function deletes a given key and
# returns root of modified tree
def deleteNode(root, key):

    # base case
    if root == None:
        return root

    # If the key to be deleted is smaller than the
    # root's key, then it lies in left subtree
    if key < root.key:
        root.left = deleteNode(root.left, key)

    # If the key to be deleted is greater than
    # the root's key, then it lies in right subtree
    elif key > root.key:
        root.right = deleteNode(root.right, key)

    # if key is same as root's key
    else:

        # If key is present more than once,
        # simply decrement count and return
        if root.count > 1:
            root.count -= 1
            return root

        # ElSE, delete the node node with
        # only one child or no child
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
        root.count = temp.count

        # Delete the inorder successor
        root.right = deleteNode(root.right, temp.key)
    return root

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    # 12(3)
    # / \
    # 10(2) 20(1)
    # / \
    # 9(1) 11(1)
    root = None
    root = insert(root, 12)
    root = insert(root, 10)
    root = insert(root, 20)
    root = insert(root, 9)
    root = insert(root, 11)
    root = insert(root, 10)
    root = insert(root, 12)
    root = insert(root, 12)

    print("Inorder traversal of the given tree")
    inorder(root)
    print()

    print("Delete 20")
    root = deleteNode(root, 20)
    print("Inorder traversal of the modified tree")
    inorder(root)
    print()

    print("Delete 12")
    root = deleteNode(root, 12)
    print("Inorder traversal of the modified tree")
    inorder(root)
    print()

    print("Delete 9")
    root = deleteNode(root, 9)
    print("Inorder traversal of the modified tree")
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to implement basic operations
// (search, insert and delete) on a BST that
// handles duplicates by storing count with
// every node
using System;

class GFG
{
public class node
{
    public int key;
    public int count;
    public node left, right;
};

// A utility function to create
// a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    temp.count = 1;
    return temp;
}

// A utility function to do inorder
// traversal of BST
static void inorder(node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + "(" +
                      root.count + ") ");
        inorder(root.right);
    }
}

/* A utility function to insert a new
node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty,
    return a new node */
    if (node == null) return newNode(key);

    // If key already exists in BST,
    // increment count and return
    if (key == node.key)
    {
        (node.count)++;
        return node;
    }

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
found in that tree. Note that the entire tree
does not need to be searched. */
static node minValueNode(node node)
{
    node current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
        current = current.left;

    return current;
}

/* Given a binary search tree and a key,
this function deletes a given key and
returns root of modified tree */
static node deleteNode(node root, int key)
{
    // base case
    if (root == null) return root;

    // If the key to be deleted is smaller than the
    // root's key, then it lies in left subtree
    if (key < root.key)
        root.left = deleteNode(root.left, key);

    // If the key to be deleted is greater than
    // the root's key, then it lies in right subtree
    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    // if key is same as root's key
    else
    {
        // If key is present more than once,
        // simply decrement count and return
        if (root.count > 1)
        {
            (root.count)--;
            return root;
        }

        // ElSE, delete the node
        node temp = null;

        // node with only one child or no child
        if (root.left == null)
        {
            temp = root.right;
            root = null;
            return temp;
        }
        else if (root.right == null)
        {
            temp = root.left;
            root = null;
            return temp;
        }

        // node with two children: Get the inorder
        // successor (smallest in the right subtree)
        temp = minValueNode(root.right);

        // Copy the inorder successor's
        // content to this node
        root.key = temp.key;
        root.count = temp.count;

        // Delete the inorder successor
        root.right = deleteNode(root.right,
                                temp.key);
    }
    return root;
}

// Driver Code
public static void Main(String[] args)
{
    /* Let us create following BST
            12(3)
        /     \
    10(2)     20(1)
    / \
    9(1) 11(1) */
    node root = null;
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 9);
    root = insert(root, 11);
    root = insert(root, 10);
    root = insert(root, 12);
    root = insert(root, 12);

    Console.Write("Inorder traversal of " +
                  "the given tree " + "\n");
    inorder(root);

    Console.Write("\nDelete 20\n");
    root = deleteNode(root, 20);
    Console.Write("Inorder traversal of " +
                  "the modified tree \n");
    inorder(root);

    Console.Write("\nDelete 12\n");
    root = deleteNode(root, 12);
    Console.Write("Inorder traversal of " +
                  "the modified tree \n");
    inorder(root);

    Console.Write("\nDelete 9\n");
    root = deleteNode(root, 9);
    Console.Write("Inorder traversal of " +
                  "the modified tree \n");
    inorder(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to implement basic operations
// (search, insert and delete) on a BST that
// handles duplicates by storing count with
// every node

class node {
        constructor() {
            this.key = 0;
            this.count = 0;
            this.left = null;
            this.right = null;
        }
    }

    // A utility function to create a new BST node
     function newNode(item) {
        var temp = new node();
        temp.key = item;
        temp.left = temp.right = null;
        temp.count = 1;
        return temp;
    }

    // A utility function to do inorder
    // traversal of BST
    function inorder( root) {
        if (root != null) {
            inorder(root.left);
            document.write(root.key +
            "(" + root.count + ") ");
            inorder(root.right);
        }
    }

    /*
     * A utility function to insert a new
     node with given key in BST
     */
     function insert( node , key) {
        /* If the tree is empty, return a new node */
        if (node == null)
            return newNode(key);

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

        /* return the (unchanged) node pointer */
        return node;
    }

    /*
     * Given a non-empty binary search tree,
     return the node with minimum key value
     * found in that tree. Note that the
     entire tree does not need to be searched.
     */
     function minValueNode( node) {
        var current = node;

        /* loop down to find the leftmost leaf */
        while (current.left != null)
            current = current.left;

        return current;
    }

    /*
     * Given a binary search tree and a key,
     this function deletes a given key and
     * returns root of modified tree
     */
     function deleteNode( root , key) {
        // base case
        if (root == null)
            return root;

        // If the key to be deleted is smaller than the
        // root's key, then it lies in left subtree
        if (key < root.key)
            root.left = deleteNode(root.left, key);

        // If the key to be deleted is greater than
        // the root's key, then it lies in right subtree
        else if (key > root.key)
            root.right = deleteNode(root.right, key);

        // if key is same as root's key
        else {
            // If key is present more than once,
            // simply decrement count and return
            if (root.count > 1) {
                (root.count)--;
                return root;
            }

            // ElSE, delete the node

            // node with only one child or no child
            if (root.left == null) {
                var temp = root.right;
                root = null;
                return temp;
            } else if (root.right == null) {
                var temp = root.left;
                root = null;
                return temp;
            }

            // node with two children: Get the inorder
            // successor (smallest in the right subtree)
            var temp = minValueNode(root.right);

            // Copy the inorder successor's
            // content to this node
            root.key = temp.key;
            root.count = temp.count;

            // Delete the inorder successor
            root.right = deleteNode(root.right, temp.key);
        }
        return root;
    }

    // Driver Code

        /*
         * Let us create following BST
         12(3) / \ 10(2) 20(1) / \ 9(1) 11(1)
         */
        var root = null;
        root = insert(root, 12);
        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 9);
        root = insert(root, 11);
        root = insert(root, 10);
        root = insert(root, 12);
        root = insert(root, 12);

        document.write("Inorder traversal of "
        + "the given tree " + "<br/>");
        inorder(root);

        document.write("<br/>Delete 20<br/>");
        root = deleteNode(root, 20);
        document.write("Inorder traversal of "
        + "the modified tree <br/>");
        inorder(root);

        document.write("<br/>Delete 12<br/>");
        root = deleteNode(root, 12);
        document.write("Inorder traversal of "
        + "the modified tree <br/>");
        inorder(root);

        document.write("<br/>Delete 9<br/>");
        root = deleteNode(root, 9);
        document.write("Inorder traversal of "
        + "the modified tree <br/>");
        inorder(root);

// This code contributed by aashish1995

</script>
```

**输出:**

```
Inorder traversal of the given tree
9(1) 10(2) 11(1) 12(3) 20(1)
Delete 20
Inorder traversal of the modified tree
9(1) 10(2) 11(1) 12(3)
Delete 12
Inorder traversal of the modified tree
9(1) 10(2) 11(1) 12(2)
Delete 9
Inorder traversal of the modified tree
10(2) 11(1) 12(2)
```

我们将很快讨论允许复制的 AVL 和红黑树。
本文由**奇拉**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息