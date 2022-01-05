# 二叉查找树的有序接班人

> 原文:[https://www . geesforgeks . org/in order-后继二进制搜索树/](https://www.geeksforgeeks.org/inorder-successor-in-binary-search-tree/)

在二叉树中，节点的有序后继是二叉树有序遍历中的下一个节点。对于有序遍历中的最后一个节点，有序后继节点为空。

在二叉查找树，输入节点的有序后继节点也可以定义为键最小的节点大于输入节点的键。因此，有时按排序顺序查找下一个节点很重要。

[![](img/80a529084597eec7023083269684bcbe.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/2009/09/BST_LCA.gif)

在上图中， **8** 的顺序继承人为 **10** ， **10** 的顺序继承人为 **12** ， **14** 的顺序继承人为 **20** 。

**方法 1(使用父指针)**
在这个方法中，我们假设每个节点都有一个父指针。
算法根据输入节点的右子树是否为空分为两种情况。

**输入:** *节点，根* // *节点*是需要 Inorder 后继的节点。
**输出:** *成功* // *成功*是*节点*的后续节点。

1.  如果*节点*的右子树不是*空*，那么成功位于右子树中。请执行以下操作。
    转到右子树，返回右子树中键值最小的节点。
2.  如果*节点*的右子树为空，那么*成功*就是祖先之一。请执行以下操作。
    使用父指针向上移动，直到看到其父节点的左子节点。这样一个节点的父节点是*成功*。

**实现:**
请注意，在下面的代码中，查找无机后继者的功能是高亮显示的(灰色背景)。

## C++

```
#include <iostream>
using namespace std;

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
    struct node* parent;
};

struct node* minValue(struct node* node);

struct node* inOrderSuccessor(
    struct node* root,
    struct node* n)
{
    // step 1 of the above algorithm
    if (n->right != NULL)
        return minValue(n->right);

    // step 2 of the above algorithm
    struct node* p = n->parent;
    while (p != NULL && n == p->right) {
        n = p;
        p = p->parent;
    }
    return p;
}

/* Given a non-empty binary search tree,
    return the minimum data 
    value found in that tree. Note that
    the entire tree does not need
    to be searched. */
struct node* minValue(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL) {
        current = current->left;
    }
    return current;
}

/* Helper function that allocates a new
    node with the given data and
    NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)
        malloc(sizeof(
            struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->parent = NULL;

    return (node);
}

/* Give a binary search tree and
   a number, inserts a new node with   
    the given number in the correct
    place in the tree. Returns the new
    root pointer which the caller should
    then use (the standard trick to
    avoid using reference parameters). */
struct node* insert(struct node* node,
                    int data)
{
    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == NULL)
        return (newNode(data));
    else {
        struct node* temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data) {
            temp = insert(node->left, data);
            node->left = temp;
            temp->parent = node;
        }
        else {
            temp = insert(node->right, data);
            node->right = temp;
            temp->parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }
}

/* Driver program to test above functions*/
int main()
{
    struct node *root = NULL, *temp, *succ, *min;

    // creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root->left->right->right;

    succ = inOrderSuccessor(root, temp);
    if (succ != NULL)
        cout << "\n Inorder Successor of " << temp->data<< " is "<< succ->data;
    else
        cout <<"\n Inorder Successor doesn't exit";

    getchar();
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
    struct node* parent;
};

struct node* minValue(struct node* node);

struct node* inOrderSuccessor(
    struct node* root,
    struct node* n)
{
    // step 1 of the above algorithm
    if (n->right != NULL)
        return minValue(n->right);

    // step 2 of the above algorithm
    struct node* p = n->parent;
    while (p != NULL && n == p->right) {
        n = p;
        p = p->parent;
    }
    return p;
}

/* Given a non-empty binary search tree,
    return the minimum data 
    value found in that tree. Note that
    the entire tree does not need
    to be searched. */
struct node* minValue(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL) {
        current = current->left;
    }
    return current;
}

/* Helper function that allocates a new
    node with the given data and
    NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)
        malloc(sizeof(
            struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->parent = NULL;

    return (node);
}

/* Give a binary search tree and
   a number, inserts a new node with   
    the given number in the correct
    place in the tree. Returns the new
    root pointer which the caller should
    then use (the standard trick to
    avoid using reference parameters). */
struct node* insert(struct node* node,
                    int data)
{
    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == NULL)
        return (newNode(data));
    else {
        struct node* temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data) {
            temp = insert(node->left, data);
            node->left = temp;
            temp->parent = node;
        }
        else {
            temp = insert(node->right, data);
            node->right = temp;
            temp->parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }
}

/* Driver program to test above functions*/
int main()
{
    struct node *root = NULL, *temp, *succ, *min;

    // creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root->left->right->right;

    succ = inOrderSuccessor(root, temp);
    if (succ != NULL)
        printf(
            "\n Inorder Successor of %d is %d ",
            temp->data, succ->data);
    else
        printf("\n Inorder Successor doesn't exit");

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// value node in Binary Search Tree

// A binary tree node
class Node {

    int data;
    Node left, right, parent;

    Node(int d)
    {
        data = d;
        left = right = parent = null;
    }
}

class BinaryTree {

    static Node head;

    /* Given a binary search tree and a number,
     inserts a new node with the given number in
     the correct place in the tree. Returns the new
     root pointer which the caller should then use
     (the standard trick to avoid using reference
     parameters). */
    Node insert(Node node, int data)
    {

        /* 1\. If the tree is empty, return a new,    
         single node */
        if (node == null) {
            return (new Node(data));
        }
        else {

            Node temp = null;

            /* 2\. Otherwise, recur down the tree */
            if (data <= node.data) {
                temp = insert(node.left, data);
                node.left = temp;
                temp.parent = node;
            }
            else {
                temp = insert(node.right, data);
                node.right = temp;
                temp.parent = node;
            }

            /* return the (unchanged) node pointer */
            return node;
        }
    }

    Node inOrderSuccessor(Node root, Node n)
    {

        // step 1 of the above algorithm
        if (n.right != null) {
            return minValue(n.right);
        }

        // step 2 of the above algorithm
        Node p = n.parent;
        while (p != null && n == p.right) {
            n = p;
            p = p.parent;
        }
        return p;
    }

    /* Given a non-empty binary search
       tree, return the minimum data 
       value found in that tree. Note that
       the entire tree does not need
       to be searched. */
    Node minValue(Node node)
    {
        Node current = node;

        /* loop down to find the leftmost leaf */
        while (current.left != null) {
            current = current.left;
        }
        return current;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        Node root = null, temp = null, suc = null, min = null;
        root = tree.insert(root, 20);
        root = tree.insert(root, 8);
        root = tree.insert(root, 22);
        root = tree.insert(root, 4);
        root = tree.insert(root, 12);
        root = tree.insert(root, 10);
        root = tree.insert(root, 14);
        temp = root.left.right.right;
        suc = tree.inOrderSuccessor(root, temp);
        if (suc != null) {
            System.out.println(
                "Inorder successor of "
                + temp.data + " is " + suc.data);
        }
        else {
            System.out.println(
                "Inorder successor does not exist");
        }
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find the inorder successor in a BST

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def inOrderSuccessor(n):

    # Step 1 of the above algorithm
    if n.right is not None:
        return minValue(n.right)

    # Step 2 of the above algorithm
    p = n.parent
    while( p is not None):
        if n != p.right :
            break
        n = p
        p = p.parent
    return p

# Given a non-empty binary search tree, return the
# minimum data value found in that tree. Note that the
# entire tree doesn't need to be searched
def minValue(node):
    current = node

    # loop down to find the leftmost leaf
    while(current is not None):
        if current.left is None:
            break
        current = current.left

    return current

# Given a binary search tree and a number, inserts a
# new node with the given number in the correct place
# in the tree. Returns the new root pointer which the
# caller should then use( the standard trick to avoid
# using reference parameters)
def insert( node, data):

    # 1) If tree is empty then return a new singly node
    if node is None:
        return Node(data)
    else:

        # 2) Otherwise, recur down the tree
        if data <= node.data:
            temp = insert(node.left, data)
            node.left = temp
            temp.parent = node
        else:
            temp = insert(node.right, data)
            node.right = temp
            temp.parent = node

        # return  the unchanged node pointer
        return node

# Driver program to test above function

root = None

# Creating the tree given in the above diagram
root = insert(root, 20)
root = insert(root, 8);
root = insert(root, 22);
root = insert(root, 4);
root = insert(root, 12);
root = insert(root, 10); 
root = insert(root, 14);   
temp = root.left.right.right

succ = inOrderSuccessor( root, temp)
if succ is not None:
    print "\nInorder Successor of % d is % d " \
            %(temp.data, succ.data)
else:
    print "\nInorder Successor doesn't exist"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to find minimum
// value node in Binary Search Tree
using System;

// A binary tree node
public
  class Node
  {
    public
      int data;
    public
      Node left, right, parent;
    public
      Node(int d)
    {
      data = d;
      left = right = parent = null;
    }
  }

public class BinaryTree
{
  static Node head;

  /* Given a binary search tree and a number,
     inserts a new node with the given number in
     the correct place in the tree. Returns the new
     root pointer which the caller should then use
     (the standard trick to avoid using reference
     parameters). */
  Node insert(Node node, int data)
  {

    /* 1\. If the tree is empty, return a new,    
         single node */
    if (node == null)
    {
      return (new Node(data));
    }
    else
    {

      Node temp = null;

      /* 2\. Otherwise, recur down the tree */
      if (data <= node.data)
      {
        temp = insert(node.left, data);
        node.left = temp;
        temp.parent = node;
      }
      else
      {
        temp = insert(node.right, data);
        node.right = temp;
        temp.parent = node;
      }

      /* return the (unchanged) node pointer */
      return node;
    }
  }

  Node inOrderSuccessor(Node root, Node n)
  {

    // step 1 of the above algorithm
    if (n.right != null)
    {
      return minValue(n.right);
    }

    // step 2 of the above algorithm
    Node p = n.parent;
    while (p != null && n == p.right)
    {
      n = p;
      p = p.parent;
    }
    return p;
  }

  /* Given a non-empty binary search
       tree, return the minimum data 
       value found in that tree. Note that
       the entire tree does not need
       to be searched. */
  Node minValue(Node node)
  {
    Node current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
    {
      current = current.left;
    }
    return current;
  }

  // Driver program to test above functions
  public static void Main(String[] args)
  {
    BinaryTree tree = new BinaryTree();
    Node root = null, temp = null, suc = null, min = null;
    root = tree.insert(root, 20);
    root = tree.insert(root, 8);
    root = tree.insert(root, 22);
    root = tree.insert(root, 4);
    root = tree.insert(root, 12);
    root = tree.insert(root, 10);
    root = tree.insert(root, 14);
    temp = root.left.right.right;
    suc = tree.inOrderSuccessor(root, temp);
    if (suc != null) {
      Console.WriteLine(
        "Inorder successor of "
        + temp.data + " is " + suc.data);
    }
    else {
      Console.WriteLine(
        "Inorder successor does not exist");
    }
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// value node in Binary Search Tree

// A binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
        this.parent = null;
    }
}

    var head;

    /*
     * Given a binary search tree and a number,
     inserts a new node with the given
     * number in the correct place in the tree.
     Returns the new root pointer which
     * the caller should then use
     (the standard trick to afunction using reference
     * parameters).
     */
    function insert(node , data) {

        /*
         * 1\. If the tree is empty,
         return a new, single node
         */
        if (node == null) {
            return (new Node(data));
        } else {

            var temp = null;

            /* 2\. Otherwise, recur down the tree */
            if (data <= node.data) {
                temp = insert(node.left, data);
                node.left = temp;
                temp.parent = node;
            } else {
                temp = insert(node.right, data);
                node.right = temp;
                temp.parent = node;
            }

            /* return the (unchanged) node pointer */
            return node;
        }
    }

    function inOrderSuccessor(root,  n) {

        // step 1 of the above algorithm
        if (n.right != null) {
            return minValue(n.right);
        }

        // step 2 of the above algorithm
        var p = n.parent;
        while (p != null && n == p.right) {
            n = p;
            p = p.parent;
        }
        return p;
    }

    /*
     * Given a non-empty binary search tree,
     return the minimum data value found in
     * that tree. Note that the entire tree
     does not need to be searched.
     */
    function minValue(node) {
        var current = node;

        /* loop down to find the leftmost leaf */
        while (current.left != null) {
            current = current.left;
        }
        return current;
    }

    // Driver program to test above functions

        var root = null, temp = null,
        suc = null, min = null;
        root = insert(root, 20);
        root = insert(root, 8);
        root = insert(root, 22);
        root = insert(root, 4);
        root = insert(root, 12);
        root = insert(root, 10);
        root = insert(root, 14);
        temp = root.left.right.right;
        suc = inOrderSuccessor(root, temp);
        if (suc != null) {
            document.write("Inorder successor of " +
            temp.data + " is " + suc.data);
        } else {
            document.write(
            "Inorder successor does not exist"
            );
        }

// This code contributed by gauravrajput1

</script>
```

**Output**

```
 Inorder Successor of 14 is 20
```

**复杂度分析:**

*   **时间复杂度:** O(h)，其中 h 是树的高度。
    就像第二种情况(假设是倾斜的树)一样，我们必须一路朝着树根前进。
*   **辅助空间:** O(1)。
    由于没有使用任何数据结构来存储值。

**方法 2(从根开始搜索)**
该算法不需要父指针。该算法根据输入节点的右子树是否为空分为两种情况。

**输入:** *节点，根* // *节点*是需要 Inorder 后继的节点。

**输出:** *成功*/*成功*是*节点*的后续节点。

1.  如果*节点*的右子树不是*空*，则*成功*位于右子树中。请执行以下操作。
    转到右子树，返回右子树中键值最小的节点。
2.  如果*节点*的右子树为空，那么从根开始使用类似搜索的技术。请执行以下操作。
    沿着树往下走，如果一个节点的数据大于根节点的数据，那么走右边，否则走左边。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
    struct node* parent;
};

struct node* minValue(struct node* node);

struct node* inOrderSuccessor(struct node* root,
                              struct node* n)
{

    // Step 1 of the above algorithm
    if (n->right != NULL)
        return minValue(n->right);

    struct node* succ = NULL;

    // Start from root and search for
    // successor down the tree
    while (root != NULL)
    {
        if (n->data < root->data)
        {
            succ = root;
            root = root->left;
        }
        else if (n->data > root->data)
            root = root->right;
        else
            break;
    }

    return succ;
}

// Given a non-empty binary search tree,
// return the minimum data value found
// in that tree. Note that the entire
// tree does not need to be searched.
struct node* minValue(struct node* node)
{
    struct node* current = node;

    // Loop down to find the leftmost leaf
    while (current->left != NULL)
    {
        current = current->left;
    }
    return current;
}

// Helper function that allocates a new
// node with the given data and NULL left
// and right pointers.
struct node* newNode(int data)
{
    struct node* node = (struct node*)
    malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->parent = NULL;

    return (node);
}

// Give a binary search tree and a
// number, inserts a new node with
// the given number in the correct
// place in the tree. Returns the new
// root pointer which the caller should
// then use (the standard trick to
// avoid using reference parameters).
struct node* insert(struct node* node,
                    int data)
{

    /* 1\. If the tree is empty, return a new,
       single node */
    if (node == NULL)
        return (newNode(data));
    else
    {
        struct node* temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data)
        {
            temp = insert(node->left, data);
            node->left = temp;
            temp->parent = node;
        }
        else
        {
            temp = insert(node->right, data);
            node->right = temp;
            temp->parent = node;
        }

        /* Return the (unchanged) node pointer */
        return node;
    }
}

// Driver code
int main()
{
    struct node *root = NULL, *temp, *succ, *min;

    // Creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root->left->right->right;

    // Function Call
    succ = inOrderSuccessor(root, temp);
    if (succ != NULL)
        cout << "\n Inorder Successor of "
             << temp->data << " is "<< succ->data;
    else
        cout <<"\n Inorder Successor doesn't exit";

    getchar();
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
    struct node* parent;
};

struct node* minValue(struct node* node);

struct node* inOrderSuccessor(
    struct node* root,
    struct node* n)
{

    // step 1 of the above algorithm
    if (n->right != NULL)
        return minValue(n->right);

    struct node* succ = NULL;

    // Start from root and search for
    // successor down the tree
    while (root != NULL)
    {
        if (n->data < root->data)
        {
            succ = root;
            root = root->left;
        }
        else if (n->data > root->data)
            root = root->right;
        else
            break;
    }

    return succ;
}

/* Given a non-empty binary search tree,
    return the minimum data 
    value found in that tree. Note that
    the entire tree does not need
    to be searched. */
struct node* minValue(struct node* node)
{
    struct node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
    {
        current = current->left;
    }
    return current;
}

/* Helper function that allocates a new
    node with the given data and
    NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)
        malloc(sizeof(
            struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->parent = NULL;

    return (node);
}

/* Give a binary search tree and
   a number, inserts a new node with   
    the given number in the correct
    place in the tree. Returns the new
    root pointer which the caller should
    then use (the standard trick to
    avoid using reference parameters). */
struct node* insert(struct node* node,
                    int data)
{
    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == NULL)
        return (newNode(data));
    else
    {
        struct node* temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data)
        {
            temp = insert(node->left, data);
            node->left = temp;
            temp->parent = node;
        }
        else
        {
            temp = insert(node->right, data);
            node->right = temp;
            temp->parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }
}

/* Driver program to test above functions*/
int main()
{
    struct node *root = NULL, *temp, *succ, *min;

    // creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root->left->right->right;

    // Function Call
    succ = inOrderSuccessor(root, temp);
    if (succ != NULL)
        printf(
            "\n Inorder Successor of %d is %d ",
            temp->data, succ->data);
    else
        printf("\n Inorder Successor doesn't exit");

    getchar();
    return 0;
}

// Thanks to R.Srinivasan for suggesting this method.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
static class node
{
    int data;
    node left;
    node right;
    node parent;
};

static node inOrderSuccessor(
    node root,
    node n)
{

    // step 1 of the above algorithm
    if (n.right != null)
        return minValue(n.right);

    node succ = null;

    // Start from root and search for
    // successor down the tree
    while (root != null)
    {
        if (n.data < root.data)
        {
            succ = root;
            root = root.left;
        }
        else if (n.data > root.data)
            root = root.right;
        else
            break;
    }
    return succ;
}

/* Given a non-empty binary search tree,
    return the minimum data 
    value found in that tree. Note that
    the entire tree does not need
    to be searched. */
static node minValue(node node)
{
    node current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
    {
        current = current.left;
    }
    return current;
}

/* Helper function that allocates a new
    node with the given data and
    null left and right pointers. */
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    node.parent = null;

    return (node);
}

/* Give a binary search tree and
   a number, inserts a new node with   
    the given number in the correct
    place in the tree. Returns the new
    root pointer which the caller should
    then use (the standard trick to
    astatic void using reference parameters). */
static  node insert(node node,
                    int data)
{

    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == null)
        return (newNode(data));
    else
    {
        node temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
        {
            temp = insert(node.left, data);
            node.left = temp;
            temp.parent = node;
        }
        else
        {
            temp = insert(node.right, data);
            node.right = temp;
            temp.parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }
}

/* Driver program to test above functions*/
public static void main(String[] args)
{
    node root = null, temp, succ, min;

    // creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root.left.right.right;

    // Function Call
    succ = inOrderSuccessor(root, temp);
    if (succ != null)
        System.out.printf(
            "\n Inorder Successor of %d is %d ",
            temp.data, succ.data);
    else
        System.out.printf("\n Inorder Successor doesn't exit");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python program to find
# the inorder successor in a BST

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def inOrderSuccessor(root, n):

    # Step 1 of the above algorithm
    if n.right is not None:
        return minValue(n.right)

    # Step 2 of the above algorithm
    succ=Node(None)

    while( root):
        if(root.data<n.data):
            root=root.right
        elif(root.data>n.data):
            succ=root
            root=root.left
        else:
            break
    return succ

# Given a non-empty binary search tree,
# return the minimum data value
# found in that tree. Note that the
# entire tree doesn't need to be searched
def minValue(node):
    current = node

    # loop down to find the leftmost leaf
    while(current is not None):
        if current.left is None:
            break
        current = current.left

    return current

# Given a binary search tree
# and a number, inserts a
# new node with the given
# number in the correct place
# in the tree. Returns the
# new root pointer which the
# caller should then use
# (the standard trick to avoid
# using reference parameters)
def insert( node, data):

    # 1) If tree is empty
    # then return a new singly node
    if node is None:
        return Node(data)
    else:

        # 2) Otherwise, recur down the tree
        if data <= node.data:
            temp = insert(node.left, data)
            node.left = temp
            temp.parent = node
        else:
            temp = insert(node.right, data)
            node.right = temp
            temp.parent = node

        # return  the unchanged node pointer
        return node

# Driver program to test above function
if __name__ == "__main__":
    root = None

  # Creating the tree given in the above diagram
  root = insert(root, 20)
  root = insert(root, 8);
  root = insert(root, 22);
  root = insert(root, 4);
  root = insert(root, 12);
  root = insert(root, 10); 
  root = insert(root, 14);   
  temp = root.left.right

  succ = inOrderSuccessor( root, temp)
  if succ is not None:
      print("Inorder Successor of" ,
               temp.data ,"is" ,succ.data)
  else:
      print("InInorder Successor doesn't exist")
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

  /* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
  public
    class node
    {
      public
        int data;
      public
        node left;
      public
        node right;
      public
        node parent;
    };

  static node inOrderSuccessor(
    node root,
    node n)
  {

    // step 1 of the above algorithm
    if (n.right != null)
      return minValue(n.right);

    node succ = null;

    // Start from root and search for
    // successor down the tree
    while (root != null)
    {
      if (n.data < root.data)
      {
        succ = root;
        root = root.left;
      }
      else if (n.data > root.data)
        root = root.right;
      else
        break;
    }
    return succ;
  }

  /* Given a non-empty binary search tree,
    return the minimum data 
    value found in that tree. Note that
    the entire tree does not need
    to be searched. */
  static node minValue(node node)
  {
    node current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
    {
      current = current.left;
    }
    return current;
  }

  /* Helper function that allocates a new
    node with the given data and
    null left and right pointers. */
  static node newNode(int data)
  {
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    node.parent = null;

    return (node);
  }

  /* Give a binary search tree and
   a number, inserts a new node with   
    the given number in the correct
    place in the tree. Returns the new
    root pointer which the caller should
    then use (the standard trick to
    astatic void using reference parameters). */
  static  node insert(node node,
                      int data)
  {

    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == null)
      return (newNode(data));
    else
    {
      node temp;

      /* 2\. Otherwise, recur down the tree */
      if (data <= node.data)
      {
        temp = insert(node.left, data);
        node.left = temp;
        temp.parent = node;
      }
      else
      {
        temp = insert(node.right, data);
        node.right = temp;
        temp.parent = node;
      }

      /* return the (unchanged) node pointer */
      return node;
    }
  }

  /* Driver program to test above functions*/
  public static void Main(String[] args)
  {
    node root = null, temp, succ;

    // creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root.left.right.right;

    // Function Call
    succ = inOrderSuccessor(root, temp);
    if (succ != null)
      Console.Write(
      "\n Inorder Successor of {0} is {1} ",
      temp.data, succ.data);
    else
      Console.Write("\n Inorder Successor doesn't exit");
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

class Node
{
    constructor(data)
    {
        this.data=data;;
        this.left=this.right=this.parent=null;
    }
}

function inOrderSuccessor(root,n)
{
    // step 1 of the above algorithm
    if (n.right != null)
        return minValue(n.right);

    let succ = null;

    // Start from root and search for
    // successor down the tree
    while (root != null)
    {
        if (n.data < root.data)
        {
            succ = root;
            root = root.left;
        }
        else if (n.data > root.data)
            root = root.right;
        else
            break;
    }
    return succ;
}

function minValue(node)
{
    let current = node;

    /* loop down to find the leftmost leaf */
    while (current.left != null)
    {
        current = current.left;
    }
    return current;
}

function insert(node,data)
{
    /* 1\. If the tree is empty, return a new,
      single node */
    if (node == null)
        return (new Node(data));
    else
    {
        let temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
        {
            temp = insert(node.left, data);
            node.left = temp;
            temp.parent = node;
        }
        else
        {
            temp = insert(node.right, data);
            node.right = temp;
            temp.parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }
}

let root = null, temp, succ, min;

// creating the tree given in the above diagram
root = insert(root, 20);
root = insert(root, 8);
root = insert(root, 22);
root = insert(root, 4);
root = insert(root, 12);
root = insert(root, 10);
root = insert(root, 14);
temp = root.left.right.right;

// Function Call
succ = inOrderSuccessor(root, temp);
if (succ != null)
    document.write(
"<br> Inorder Successor of "+temp.data+"  is "+
 succ.data);
else
    document.write("<br> Inorder Successor doesn't exit");

// This code is contributed by unknown2108

</script>
```

**Output**

```
 Inorder Successor of 14 is 20
```

**复杂度分析:**

*   **时间复杂度:** O(h)，其中 h 是树的高度。
    在最糟糕的情况下，如上所述，我们穿越了整个树的高度
*   **辅助空间:** O(1)。
    由于没有使用任何数据结构来存储值。

**方法 3(有序遍历)**BST 的有序横向产生排序序列。因此，我们执行有序遍历。第一个遇到的值大于该节点的节点是后续节点。

**输入:**节点，根//节点是需要 ignorer 后继的节点。
**输出:**成功//成功是节点的后续节点。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

/* A binary tree node has data,
   the pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
    struct node* parent;
};
struct node* newNode(int data);

void inOrderTraversal(struct node* root,
                              struct node* n,
                              struct node* succ)
{   
    if(root==nullptr) { return; }

    inOrderTraversal(root->left, n, succ);
    if(root->data>n->data && !succ->left) { succ->left = root; return; }
    inOrderTraversal(root->right, n, succ);    
}

struct node* inOrderSuccessor(struct node* root,
                              struct node* n)
{   
    struct node* succ = newNode(0);
    inOrderTraversal(root, n, succ);
    return succ->left;
}

// Helper function that allocates a new
// node with the given data and NULL left
// and right pointers.
struct node* newNode(int data)
{
    struct node* node = (struct node*)
    malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->parent = NULL;

    return (node);
}

// Give a binary search tree and a
// number, inserts a new node with
// the given number in the correct
// place in the tree. Returns the new
// root pointer which the caller should
// then use (the standard trick to
// avoid using reference parameters).
struct node* insert(struct node* node,
                    int data)
{

    /* 1\. If the tree is empty, return a new,
       single node */
    if (node == NULL)
        return (newNode(data));
    else
    {
        struct node* temp;

        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data)
        {
            temp = insert(node->left, data);
            node->left = temp;
            temp->parent = node;
        }
        else
        {
            temp = insert(node->right, data);
            node->right = temp;
            temp->parent = node;
        }

        /* Return the (unchanged) node pointer */
        return node;
    }
}

// Driver code
int main()
{
    struct node *root = NULL, *temp, *succ, *min;

    // Creating the tree given in the above diagram
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 22);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    temp = root->left->right->right;

    // Function Call
    succ = inOrderSuccessor(root, temp);
    if (succ != NULL)
        cout << "\n Inorder Successor of "
             << temp->data << " is "<< succ->data;
    else
        cout <<"\n Inorder Successor doesn't exist";

    //getchar();
    return 0;
}

// This code is contributed by jaisw7
```

**Output**

```
 Inorder Successor of 14 is 20
```

**复杂度分析:**

**时间复杂度** : O(h)，其中 h 是树的高度。在最糟糕的情况下，如上所述，我们在树的整个高度上旅行
**【辅助空间】** : O(1)。由于没有使用任何数据结构来存储值。

& list = plqm 7 alxfyshcxd 7 R1 J1 K9 ZG _ gbb 1 dbk

**参考文献:**
[http://net . pku . edu . cn/~ course/cs101/2007/resource/intro 2 algorithm/book 6/chap 13 . htm](http://net.pku.edu.cn/~course/cs101/2007/resource/Intro2Algorithm/book6/chap13.htm)
如发现有不正确的地方，或想分享更多关于以上讨论话题的信息，请写评论。