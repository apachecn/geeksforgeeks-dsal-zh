# 二叉查找树|第二集(删除)

> 原文:[https://www . geesforgeks . org/binary-search-tree-set-2-delete/](https://www.geeksforgeeks.org/binary-search-tree-set-2-delete/)

我们已经讨论了 [BST 搜索和插入操作](http://quiz.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。在这篇文章中，讨论了删除操作。当我们删除一个节点时，会出现三种可能性。
**1)** ***要删除的节点是*** ***叶:*** 简单地从树上移除。

```
              50                            50
           /     \         delete(20)      /   \
          30      70       --------->    30     70 
         /  \    /  \                     \    /  \ 
       20   40  60   80                   40  60   80
```

**2)** ***待删除节点只有一个子节点:*** 将该子节点复制到该节点并删除该子节点

```
              50                            50
           /     \         delete(30)      /   \
          30      70       --------->    40     70 
            \    /  \                          /  \ 
            40  60   80                       60   80
```

**3)** ***要删除的节点有两个子节点:*** 查找该节点的后续节点。将排序后的内容复制到节点，并删除排序后的内容。请注意，也可以使用更高级的前置任务。

```
              50                            60
           /     \         delete(50)      /   \
          40      70       --------->    40    70 
                 /  \                            \ 
                60   80                           80
```

需要注意的重要一点是，只有当合适的孩子不是空的时候，才需要更好的继任者。在这种特殊情况下，可以通过在节点的右子节点中找到最小值来获得更大的后继节点。

## C++

```
// C++ program to demonstrate
// delete operation in binary
// search tree
#include <bits/stdc++.h>
using namespace std;

struct node {
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node* newNode(int item)
{
    struct node* temp
        = (struct node*)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do
// inorder traversal of BST
void inorder(struct node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->key;
        inorder(root->right);
    }
}

/* A utility function to
insert a new node with given key in
 * BST */
struct node* insert(struct node* node, int key)
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

/* Given a non-empty binary search tree, return the node
with minimum key value found in that tree. Note that the
entire tree does not need to be searched. */
struct node* minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current && current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree and a key, this function
deletes the key and returns the new root */
struct node* deleteNode(struct node* root, int key)
{
    // base case
    if (root == NULL)
        return root;

    // If the key to be deleted is
    // smaller than the root's
    // key, then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is
    // greater than the root's
    // key, then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key, then This is the node
    // to be deleted
    else {
        // node has no child
        if (root->left==NULL and root->right==NULL)
            return NULL;

        // node with only one child or no child
        else if (root->left == NULL) {
            struct node* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct node* temp = root->left;
            free(root);
            return temp;
        }

        // node with two children: Get the inorder successor
        // (smallest in the right subtree)
        struct node* temp = minValueNode(root->right);

        // Copy the inorder successor's content to this node
        root->key = temp->key;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Driver Code
int main()
{
    /* Let us create following BST
            50
        /     \
        30     70
        / \ / \
    20 40 60 80 */
    struct node* root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    cout << "Inorder traversal of the given tree \n";
    inorder(root);

    cout << "\nDelete 20\n";
    root = deleteNode(root, 20);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    cout << "\nDelete 30\n";
    root = deleteNode(root, 30);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    cout << "\nDelete 50\n";
    root = deleteNode(root, 50);
    cout << "Inorder traversal of the modified tree \n";
    inorder(root);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to demonstrate
// delete operation in binary
// search tree
#include <stdio.h>
#include <stdlib.h>

struct node {
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node* newNode(int item)
{
    struct node* temp
        = (struct node*)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct node* root)
{
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

/* A utility function to
   insert a new node with given key in
 * BST */
struct node* insert(struct node* node, int key)
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

/* Given a non-empty binary search
   tree, return the node
   with minimum key value found in
   that tree. Note that the
   entire tree does not need to be searched. */
struct node* minValueNode(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current && current->left != NULL)
        current = current->left;

    return current;
}

/* Given a binary search tree
   and a key, this function
   deletes the key and
   returns the new root */
struct node* deleteNode(struct node* root, int key)
{
    // base case
    if (root == NULL)
        return root;

    // If the key to be deleted
    // is smaller than the root's
    // key, then it lies in left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted
    // is greater than the root's
    // key, then it lies in right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key,
    // then This is the node
    // to be deleted
    else {
        // node with only one child or no child
        if (root->left == NULL) {
            struct node* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct node* temp = root->left;
            free(root);
            return temp;
        }

        // node with two children:
        // Get the inorder successor
        // (smallest in the right subtree)
        struct node* temp = minValueNode(root->right);

        // Copy the inorder
        // successor's content to this node
        root->key = temp->key;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Driver Code
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct node* root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    printf("Inorder traversal of the given tree \n");
    inorder(root);

    printf("\nDelete 20\n");
    root = deleteNode(root, 20);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 30\n");
    root = deleteNode(root, 30);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 50\n");
    root = deleteNode(root, 50);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate
// delete operation in binary
// search tree
class BinarySearchTree {
    /* Class containing left
    and right child of current node
     * and key value*/
    class Node {
        int key;
        Node left, right;

        public Node(int item)
        {
            key = item;
            left = right = null;
        }
    }

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() { root = null; }

    // This method mainly calls deleteRec()
    void deleteKey(int key) { root = deleteRec(root, key); }

    /* A recursive function to
      delete an existing key in BST
     */
    Node deleteRec(Node root, int key)
    {
        /* Base Case: If the tree is empty */
        if (root == null)
            return root;

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = deleteRec(root.left, key);
        else if (key > root.key)
            root.right = deleteRec(root.right, key);

        // if key is same as root's
        // key, then This is the
        // node to be deleted
        else {
            // node with only one child or no child
            if (root.left == null)
                return root.right;
            else if (root.right == null)
                return root.left;

            // node with two children: Get the inorder
            // successor (smallest in the right subtree)
            root.key = minValue(root.right);

            // Delete the inorder successor
            root.right = deleteRec(root.right, root.key);
        }

        return root;
    }

    int minValue(Node root)
    {
        int minv = root.key;
        while (root.left != null)
        {
            minv = root.left.key;
            root = root.left;
        }
        return minv;
    }

    // This method mainly calls insertRec()
    void insert(int key) { root = insertRec(root, key); }

    /* A recursive function to
       insert a new key in BST */
    Node insertRec(Node root, int key)
    {

        /* If the tree is empty,
          return a new node */
        if (root == null) {
            root = new Node(key);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        /* return the (unchanged) node pointer */
        return root;
    }

    // This method mainly calls InorderRec()
    void inorder() { inorderRec(root); }

    // A utility function to do inorder traversal of BST
    void inorderRec(Node root)
    {
        if (root != null) {
            inorderRec(root.left);
            System.out.print(root.key + " ");
            inorderRec(root.right);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
        20   40  60   80 */
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        System.out.println(
            "Inorder traversal of the given tree");
        tree.inorder();

        System.out.println("\nDelete 20");
        tree.deleteKey(20);
        System.out.println(
            "Inorder traversal of the modified tree");
        tree.inorder();

        System.out.println("\nDelete 30");
        tree.deleteKey(30);
        System.out.println(
            "Inorder traversal of the modified tree");
        tree.inorder();

        System.out.println("\nDelete 50");
        tree.deleteKey(50);
        System.out.println(
            "Inorder traversal of the modified tree");
        tree.inorder();
    }
}
```

## 计算机编程语言

```
# Python program to demonstrate delete operation
# in binary search tree

# A Binary Tree Node

class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# A utility function to do inorder traversal of BST
def inorder(root):
    if root is not None:
        inorder(root.left)
        print root.key,
        inorder(root.right)

# A utility function to insert a
# new node with given key in BST
def insert(node, key):

    # If the tree is empty, return a new node
    if node is None:
        return Node(key)

    # Otherwise recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Given a non-empty binary
# search tree, return the node
# with minimum key value
# found in that tree. Note that the
# entire tree does not need to be searched

def minValueNode(node):
    current = node

    # loop down to find the leftmost leaf
    while(current.left is not None):
        current = current.left

    return current

# Given a binary search tree and a key, this function
# delete the key and returns the new root

def deleteNode(root, key):

    # Base Case
    if root is None:
        return root

    # If the key to be deleted
    # is smaller than the root's
    # key then it lies in  left subtree
    if key < root.key:
        root.left = deleteNode(root.left, key)

    # If the kye to be delete
    # is greater than the root's key
    # then it lies in right subtree
    elif(key > root.key):
        root.right = deleteNode(root.right, key)

    # If key is same as root's key, then this is the node
    # to be deleted
    else:

        # Node with only one child or no child
        if root.left is None:
            temp = root.right
            root = None
            return temp

        elif root.right is None:
            temp = root.left
            root = None
            return temp

        # Node with two children:
        # Get the inorder successor
        # (smallest in the right subtree)
        temp = minValueNode(root.right)

        # Copy the inorder successor's
        # content to this node
        root.key = temp.key

        # Delete the inorder successor
        root.right = deleteNode(root.right, temp.key)

    return root

# Driver code
""" Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 """

root = None
root = insert(root, 50)
root = insert(root, 30)
root = insert(root, 20)
root = insert(root, 40)
root = insert(root, 70)
root = insert(root, 60)
root = insert(root, 80)

print "Inorder traversal of the given tree"
inorder(root)

print "\nDelete 20"
root = deleteNode(root, 20)
print "Inorder traversal of the modified tree"
inorder(root)

print "\nDelete 30"
root = deleteNode(root, 30)
print "Inorder traversal of the modified tree"
inorder(root)

print "\nDelete 50"
root = deleteNode(root, 50)
print "Inorder traversal of the modified tree"
inorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to demonstrate delete
// operation in binary search tree
using System;

public class BinarySearchTree {
    /* Class containing left and right
    child of current node and key value*/
    class Node {
        public int key;
        public Node left, right;

        public Node(int item)
        {
            key = item;
            left = right = null;
        }
    }

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() { root = null; }

    // This method mainly calls deleteRec()
    void deleteKey(int key) { root = deleteRec(root, key); }

    /* A recursive function to
      delete an existing key in BST
     */
    Node deleteRec(Node root, int key)
    {
        /* Base Case: If the tree is empty */
        if (root == null)
            return root;

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = deleteRec(root.left, key);
        else if (key > root.key)
            root.right = deleteRec(root.right, key);

        // if key is same as root's key, then This is the
        // node to be deleted
        else {
            // node with only one child or no child
            if (root.left == null)
                return root.right;
            else if (root.right == null)
                return root.left;

            // node with two children: Get the
            // inorder successor (smallest
            // in the right subtree)
            root.key = minValue(root.right);

            // Delete the inorder successor
            root.right = deleteRec(root.right, root.key);
        }
        return root;
    }

    int minValue(Node root)
    {
        int minv = root.key;
        while (root.left != null) {
            minv = root.left.key;
            root = root.left;
        }
        return minv;
    }

    // This method mainly calls insertRec()
    void insert(int key) { root = insertRec(root, key); }

    /* A recursive function to insert a new key in BST */
    Node insertRec(Node root, int key)
    {

        /* If the tree is empty, return a new node */
        if (root == null) {
            root = new Node(key);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        /* return the (unchanged) node pointer */
        return root;
    }

    // This method mainly calls InorderRec()
    void inorder() { inorderRec(root); }

    // A utility function to do inorder traversal of BST
    void inorderRec(Node root)
    {
        if (root != null) {
            inorderRec(root.left);
            Console.Write(root.key + " ");
            inorderRec(root.right);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
            50
        / \
        30 70
        / \ / \
        20 40 60 80 */
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        Console.WriteLine(
            "Inorder traversal of the given tree");
        tree.inorder();

        Console.WriteLine("\nDelete 20");
        tree.deleteKey(20);
        Console.WriteLine(
            "Inorder traversal of the modified tree");
        tree.inorder();

        Console.WriteLine("\nDelete 30");
        tree.deleteKey(30);
        Console.WriteLine(
            "Inorder traversal of the modified tree");
        tree.inorder();

        Console.WriteLine("\nDelete 50");
        tree.deleteKey(50);
        Console.WriteLine(
            "Inorder traversal of the modified tree");
        tree.inorder();
    }
}

// This code has been contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to demonstrate
// delete operation in binary
// search tree
class Node
{
    constructor(item)
    {
        this.key = item;
        this.left = this.right = null;
    }
}

// Root of BST
let root=null;

// This method mainly calls deleteRec()
function deleteKey(key)
{
    root = deleteRec(root, key);
}

/* A recursive function to
      delete an existing key in BST
     */
function deleteRec(root,key)
{
    /* Base Case: If the tree is empty */
        if (root == null)
            return root;

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = deleteRec(root.left, key);
        else if (key > root.key)
            root.right = deleteRec(root.right, key);

        // if key is same as root's
        // key, then This is the
        // node to be deleted
        else {
            // node with only one child or no child
            if (root.left == null)
                return root.right;
            else if (root.right == null)
                return root.left;

            // node with two children: Get the inorder
            // successor (smallest in the right subtree)
            root.key = minValue(root.right);

            // Delete the inorder successor
            root.right = deleteRec(root.right, root.key);
        }

        return root;
}

function minValue(root)
{
    let minv = root.key;
        while (root.left != null)
        {
            minv = root.left.key;
            root = root.left;
        }
        return minv;
}

// This method mainly calls insertRec()
function insert(key)
{
    root = insertRec(root, key);
}

/* A recursive function to
       insert a new key in BST */
function insertRec(root,key)
{
    /* If the tree is empty,
          return a new node */
        if (root == null) {
            root = new Node(key);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        /* return the (unchanged) node pointer */
        return root;
}

 // This method mainly calls InorderRec()
function inorder()
{
    inorderRec(root);
}

// A utility function to do inorder traversal of BST
function inorderRec(root)
{
    if (root != null) {
            inorderRec(root.left);
            document.write(root.key + " ");
            inorderRec(root.right);
        }
}

// Driver Code
/* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
        20   40  60   80 */
insert(50);
insert(30);
insert(20);
insert(40);
insert(70);
insert(60);
insert(80);

document.write(
"Inorder traversal of the given tree<br>");
inorder();

document.write("<br>Delete 20<br>");
deleteKey(20);
document.write(
"Inorder traversal of the modified tree<br>");
inorder();

document.write("<br>Delete 30<br>");
deleteKey(30);
document.write(
"Inorder traversal of the modified tree<br>");
inorder();

document.write("<br>Delete 50<br>");
deleteKey(50);
document.write(
"Inorder traversal of the modified tree<br>");
inorder();

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Inorder traversal of the given tree
20 30 40 50 60 70 80
Delete 20
Inorder traversal of the modified tree
30 40 50 60 70 80
Delete 30
Inorder traversal of the modified tree
40 50 60 70 80
Delete 50
Inorder traversal of the modified tree
40 60 70 80
```

插图:

![bst-delete](img/871c4d8a6bf2257580c96a1db1511e81.png)

![bst-delete2](img/2a5f8789fc7f8ca3e78dcbaa0617c78e.png)

**时间复杂度:**删除操作的最坏情况时间复杂度为 O(h)，其中 h 为二叉查找树的高度。在最坏的情况下，我们可能不得不从根走到最深的叶节点。倾斜树的高度可能变成 n，删除操作的时间复杂度可能变成 O(n)

**优化到上面代码为两个子例:**
在上面的递归代码中，我们递归调用 delete()为后继者。我们可以通过跟踪后继节点的父节点来避免递归调用，这样我们就可以通过将父节点的子节点设置为空来移除后继节点。我们知道后继节点永远是叶节点。

## C++

```
// C++ program to implement optimized delete in BST.
#include <bits/stdc++.h>
using namespace std;

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

/* A utility function to insert a new node with given key in
 * BST */
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

/* Given a binary search tree and a key, this function
   deletes the key and returns the new root */
Node* deleteNode(Node* root, int k)
{
    // Base case
    if (root == NULL)
        return root;

    // Recursive calls for ancestors of
    // node to be deleted
    if (root->key > k) {
        root->left = deleteNode(root->left, k);
        return root;
    }
    else if (root->key < k) {
        root->right = deleteNode(root->right, k);
        return root;
    }

    // We reach here when root is the node
    // to be deleted.

    // If one of the children is empty
    if (root->left == NULL) {
        Node* temp = root->right;
        delete root;
        return temp;
    }
    else if (root->right == NULL) {
        Node* temp = root->left;
        delete root;
        return temp;
    }

    // If both children exist
    else {

        Node* succParent = root;

        // Find successor
        Node* succ = root->right;
        while (succ->left != NULL) {
            succParent = succ;
            succ = succ->left;
        }

        // Delete successor.  Since successor
        // is always left child of its parent
        // we can safely make successor's right
        // right child as left of its parent.
        // If there is no succ, then assign
        // succ->right to succParent->right
        if (succParent != root)
            succParent->left = succ->right;
        else
            succParent->right = succ->right;

        // Copy Successor Data to root
        root->key = succ->key;

        // Delete Successor and return root
        delete succ;
        return root;
    }
}

// Driver Code
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    Node* root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    printf("Inorder traversal of the given tree \n");
    inorder(root);

    printf("\nDelete 20\n");
    root = deleteNode(root, 20);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 30\n");
    root = deleteNode(root, 30);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    printf("\nDelete 50\n");
    root = deleteNode(root, 50);
    printf("Inorder traversal of the modified tree \n");
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement optimized delete in BST.
import java.util.*;

class GFG{

static class Node
{
    int key;
    Node left, right;
}

// A utility function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to do inorder traversal of BST
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print(root.key + " ");
        inorder(root.right);
    }
}

// A utility function to insert a new node
// with given key in BST
static Node insert(Node node, int key)
{

    // If the tree is empty, return a new node
    if (node == null)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    // Return the (unchanged) node pointer
    return node;
}

// Given a binary search tree and a key, this
// function deletes the key and returns the
// new root
static Node deleteNode(Node root, int k)
{

    // Base case
    if (root == null)
        return root;

    // Recursive calls for ancestors of
    // node to be deleted
    if (root.key > k)
    {
        root.left = deleteNode(root.left, k);
        return root;
    }
    else if (root.key < k)
    {
        root.right = deleteNode(root.right, k);
        return root;
    }

    // We reach here when root is the node
    // to be deleted.

    // If one of the children is empty
    if (root.left == null)
    {
        Node temp = root.right;
        return temp;
    }
    else if (root.right == null)
    {
        Node temp = root.left;
        return temp;
    }

    // If both children exist
    else
    {
        Node succParent = root;

        // Find successor
        Node succ = root.right;

        while (succ.left != null)
        {
            succParent = succ;
            succ = succ.left;
        }

        // Delete successor. Since successor
        // is always left child of its parent
        // we can safely make successor's right
        // right child as left of its parent.
        // If there is no succ, then assign
        // succ->right to succParent->right
        if (succParent != root)
            succParent.left = succ.right;
        else
            succParent.right = succ.right;

        // Copy Successor Data to root
        root.key = succ.key;

        return root;
    }
}

// Driver Code
public static void main(String args[])
{

    /* Let us create following BST
          50
        /     \
       30     70
      / \    / \
     20 40  60 80 */
    Node root = null;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    System.out.println("Inorder traversal of the " +
                       "given tree");
    inorder(root);

    System.out.println("\nDelete 20\n");
    root = deleteNode(root, 20);
    System.out.println("Inorder traversal of the " +
                       "modified tree");
    inorder(root);

    System.out.println("\nDelete 30\n");
    root = deleteNode(root, 30);
    System.out.println("Inorder traversal of the " +
                       "modified tree");
    inorder(root);

    System.out.println("\nDelete 50\n");
    root = deleteNode(root, 50);
    System.out.println("Inorder traversal of the " +
                       "modified tree");
    inorder(root);
}
}

// This code is contributed by adityapande88
```

## C#

```
// C# program to implement optimized delete in BST.
using System;

class GFG{

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
    temp.left = temp.right = null;
    return temp;
}

// A utility function to do inorder traversal of BST
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

// A utility function to insert a new node
// with given key in BST
static Node insert(Node node, int key)
{

    // If the tree is empty, return a new node
    if (node == null) return newNode(key);

    // Otherwise, recur down the tree
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);

    // Return the (unchanged) node pointer
    return node;
}

// Given a binary search tree and a key, this
// function deletes the key and returns the
// new root
static Node deleteNode(Node root, int k)
{

    // Base case
    if (root == null)
        return root;

    // Recursive calls for ancestors of
    // node to be deleted
    if (root.key > k)
    {
        root.left = deleteNode(root.left, k);
        return root;
    }
    else if (root.key < k)
    {
        root.right = deleteNode(root.right, k);
        return root;
    }

    // We reach here when root is the node
    // to be deleted.

    // If one of the children is empty
    if (root.left == null)
    {
        Node temp = root.right;
        return temp;
    }
    else if (root.right == null)
    {
        Node temp = root.left;
        return temp;
    }

    // If both children exist
    else
    {
        Node succParent = root;

        // Find successor
        Node succ = root.right;

        while (succ.left != null)
        {
            succParent = succ;
            succ = succ.left;
        }

        // Delete successor. Since successor
        // is always left child of its parent
        // we can safely make successor's right
        // right child as left of its parent.
        // If there is no succ, then assign
        // succ->right to succParent->right
        if (succParent != root)
            succParent.left = succ.right;
        else
            succParent.right = succ.right;

        // Copy Successor Data to root
        root.key = succ.key;

        return root;
    }
}

// Driver Code
public static void Main(String []args)
{

    /* Let us create following BST
          50
        /     \
       30     70
      / \    / \
     20 40  60 80 */
    Node root = null;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    Console.WriteLine("Inorder traversal of the " +
                       "given tree");
    inorder(root);

    Console.WriteLine("\nDelete 20\n");
    root = deleteNode(root, 20);
    Console.WriteLine("Inorder traversal of the " +
                       "modified tree");
    inorder(root);

    Console.WriteLine("\nDelete 30\n");
    root = deleteNode(root, 30);
    Console.WriteLine("Inorder traversal of the " +
                       "modified tree");
    inorder(root);

    Console.WriteLine("\nDelete 50\n");
    root = deleteNode(root, 50);
    Console.WriteLine("Inorder traversal of the " +
                       "modified tree");
    inorder(root);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to implement
# optimized delete in BST.

class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# A utility function to do
# inorder traversal of BST
def inorder(root):
    if root is not None:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

# A utility function to insert a
# new node with given key in BST
def insert(node, key):

    # If the tree is empty,
    # return a new node
    if node is None:
        return Node(key)

    # Otherwise recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Given a binary search tree
# and a key, this function
# delete the key and returns the new root
def deleteNode(root, key):

    # Base Case
    if root is None:
        return root

    # Recursive calls for ancestors of
    # node to be deleted
    if key < root.key:
        root.left = deleteNode(root.left, key)
        return root

    elif(key > root.key):
        root.right = deleteNode(root.right, key)
        return root

    # We reach here when root is the node
    # to be deleted.

    # If root node is a leaf node

    if root.left is None and root.right is None:
          return None

    # If one of the children is empty

    if root.left is None:
        temp = root.right
        root = None
        return temp

    elif root.right is None:
        temp = root.left
        root = None
        return temp

    # If both children exist

    succParent = root

    # Find Successor

    succ = root.right

    while succ.left != None:
        succParent = succ
        succ = succ.left

    # Delete successor.Since successor
    # is always left child of its parent
    # we can safely make successor's right
    # right child as left of its parent.
    # If there is no succ, then assign
    # succ->right to succParent->right
    if succParent != root:
        succParent.left = succ.right
    else:
        succParent.right = succ.right

    # Copy Successor Data to root

    root.key = succ.key

    return root

# Driver code
""" Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 """

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

print("\nDelete 20")
root = deleteNode(root, 20)
print("Inorder traversal of the modified tree")
inorder(root)

print("\nDelete 30")
root = deleteNode(root, 30)
print("Inorder traversal of the modified tree")
inorder(root)

print("\nDelete 50")
root = deleteNode(root, 50)
print("Inorder traversal of the modified tree")
inorder(root)

# This code is contributed by Shivam Bhat (shivambhat45)
```

**Output**

```
Inorder traversal of the given tree 
20 30 40 50 60 70 80 
Delete 20
Inorder traversal of the modified tree 
30 40 50 60 70 80 
Delete 30
Inorder traversal of the modified tree 
40 50 60 70 80 
Delete 50
Inorder traversal of the modified tree 
40 60 70 80 
```

感谢[Wolfgang 010](https://auth.geeksforgeeks.org/user/wolffgang010)提出上述优化建议。
**相关链接:**

*   [二叉查找树介绍、搜索和插入](http://quiz.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)
*   [二叉查找树小测验](http://quiz.geeksforgeeks.org/data-structure/binary-search-trees/)
*   [BST 上的编码练习](https://practice.geeksforgeeks.org/tag-page.php?tag=BST&isCmp=0)
*   [英国标准时间](https://www.geeksforgeeks.org/binary-search-tree/)上的所有文章

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息