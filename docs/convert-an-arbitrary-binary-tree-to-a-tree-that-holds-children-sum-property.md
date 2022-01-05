# 将任意二叉树转换为持有子和属性的树

> 原文:[https://www . geeksforgeeks . org/convert-a-a-any-binary-tree-a-tree-a-hold-children-sum-property/](https://www.geeksforgeeks.org/convert-an-arbitrary-binary-tree-to-a-tree-that-holds-children-sum-property/)

**问题:**给定任意二叉树，将其转换为持有[子和属性](https://www.geeksforgeeks.org/check-for-children-sum-property-in-a-binary-tree/)的二叉树。您只能增加任何节点中的数据值(您不能更改树的结构，也不能减少任何节点的值)。
例如，下面的树不持有子 sum 属性，将其转换为持有该属性的树。

```
             50
           /     \     
         /         \
       7             2
     / \             /\
   /     \          /   \
  3        5      1      30
```

**算法:**
依次遍历给定的树进行转换，即先改变左右子树持有子树 sum 属性，再改变父节点。
让节点的数据和子和之间的差不同。

```
     diff = node’s children sum - node’s data  
```

如果 diff 为 0，则无需执行任何操作。
如果 diff > 0(节点的数据小于节点的子节点总和)，则将节点的数据增加 diff。
如果 diff < 0(节点的数据大于节点的子节点总和)，则增加一个子节点的数据。如果左子和右子都不为空，我们可以选择递增。让我们总是先增加左边的孩子。增加一个子树会改变子树的 sum 属性，所以我们也需要改变左子树。所以我们递归地增加左边的孩子。如果左子代为空，那么我们递归调用右子代的 increment()。
让我们运行给定示例的算法。
首先转换左边的子树(增量 7 到 8)。

```
             50
           /     \     
         /         \
       8             2
     / \             /\
   /     \          /   \
  3        5      1      30
```

然后转换右子树(增量 2 到 31)

```
          50
        /    \     
      /        \
    8            31
   / \           / \
 /     \       /     \
3       5    1       30
```

现在转换根，我们必须增加左子树来转换根。

```
          50
        /    \     
      /        \
    19           31
   / \           /  \
 /     \       /      \
14      5     1       30
```

请注意最后一步——我们已经增加了 8 到 19，为了修复子树，我们已经增加了 3 到 14。
**执行:**

## C++

```
/* C++ Program to convert an aribitary
binary tree to a tree that hold
children sum property */
#include<bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node* left;
    node* right;

    /* Constructor that allocates a new node
    with the given data and NULL left and right
    pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

/* This function is used
to increment left subtree */
void increment(node* node, int diff);

/* This function changes a tree
to hold children sum property */
void convertTree(node* node)
{
    int left_data = 0, right_data = 0, diff;

    /* If tree is empty or it's a leaf 
        node then return true */
    if (node == NULL || (node->left == NULL &&
                        node->right == NULL))
        return;
    else
    {
        /* convert left and right subtrees */
        convertTree(node->left);
        convertTree(node->right);

        /* If left child is not present then 0 is used
        as data of left child */
        if (node->left != NULL)
        left_data = node->left->data;

        /* If right child is not present then 0 is used
        as data of right child */
        if (node->right != NULL)
        right_data = node->right->data;

        /* get the diff of node's data and children sum */
        diff = left_data + right_data - node->data;

        /* If node's children sum is
        greater than the node's data */
        if (diff > 0)
        node->data = node->data + diff;

        /* THIS IS TRICKY --> If node's data
        is greater than children sum,
        then increment subtree by diff */
        if (diff < 0)
        increment(node, -diff); // -diff is used to make diff positive
    }
}

/* This function is used
to increment subtree by diff */
void increment(node* node, int diff)
{
    /* IF left child is not
    NULL then increment it */
    if(node->left != NULL)
    {
        node->left->data = node->left->data + diff;

        // Recursively call to fix
        // the descendants of node->left
        increment(node->left, diff);
    }
    else if (node->right != NULL) // Else increment right child
    {
        node->right->data = node->right->data + diff;

        // Recursively call to fix
        // the descendants of node->right
        increment(node->right, diff);
    }
}

/* Given a binary tree,
printInorder() prints out its
inorder traversal*/
void printInorder(node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    cout<<node->data<<" ";

    /* now recur on right child */
    printInorder(node->right);
}

/* Driver code */
int main()
{
    node *root = new node(50);
    root->left = new node(7);
    root->right = new node(2);
    root->left->left = new node(3);
    root->left->right = new node(5);
    root->right->left = new node(1);
    root->right->right = new node(30);

    cout << "\nInorder traversal before conversion: " << endl;
    printInorder(root);

    convertTree(root);

    cout << "\nInorder traversal after conversion: " << endl;
    printInorder(root);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
/* Program to convert an aribitary binary tree to
   a tree that holds children sum property */

#include <stdio.h>
#include <stdlib.h>

struct node
{
  int data;
  struct node* left;
  struct node* right;
};

/* This function is used to increment left subtree */
void increment(struct node* node, int diff);

/* Helper function that allocates a new node
 with the given data and NULL left and right
 pointers. */
struct node* newNode(int data);

/* This function changes a tree to hold children sum
   property */
void convertTree(struct node* node)
{
  int left_data = 0,  right_data = 0, diff;

  /* If tree is empty or it's a leaf node then
     return true */
  if (node == NULL ||
     (node->left == NULL && node->right == NULL))
    return;
  else
  {
    /* convert left and right subtrees  */
    convertTree(node->left);
    convertTree(node->right);

    /* If left child is not present then 0 is used
       as data of left child */
    if (node->left != NULL)
      left_data = node->left->data;

    /* If right child is not present then 0 is used
      as data of right child */
    if (node->right != NULL)
      right_data = node->right->data;

    /* get the diff of node's data and children sum */
    diff = left_data + right_data - node->data;

    /* If node's children sum is greater than the node's data */
    if (diff > 0)
       node->data = node->data + diff;

    /* THIS IS TRICKY --> If node's data is greater than children sum,
      then increment subtree by diff */
    if (diff < 0)
      increment(node, -diff);  // -diff is used to make diff positive
  }
}

/* This function is used to increment subtree by diff */
void increment(struct node* node, int diff)
{
  /* IF left child is not NULL then increment it */
  if(node->left != NULL)
  {
    node->left->data = node->left->data + diff;

    // Recursively call to fix the descendants of node->left
    increment(node->left, diff); 
  }
  else if (node->right != NULL) // Else increment right child
  {
    node->right->data = node->right->data + diff;

    // Recursively call to fix the descendants of node->right
    increment(node->right, diff);
  }
}

/* Given a binary tree, printInorder() prints out its
   inorder traversal*/
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

/* Helper function that allocates a new node
 with the given data and NULL left and right
 pointers. */
struct node* newNode(int data)
{
  struct node* node =
      (struct node*)malloc(sizeof(struct node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;
  return(node);
}

/* Driver program to test above functions */
int main()
{
  struct node *root = newNode(50);
  root->left        = newNode(7);
  root->right       = newNode(2);
  root->left->left  = newNode(3);
  root->left->right = newNode(5);
  root->right->left  = newNode(1);
  root->right->right = newNode(30);

  printf("\n Inorder traversal before conversion ");
  printInorder(root);

  convertTree(root);

  printf("\n Inorder traversal after conversion ");
  printInorder(root);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
    // Java program to convert an arbitrary binary tree to a tree that holds
// children sum property

// A binary tree node
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

class BinaryTree
{
    Node root;
    /* This function changes a tree to hold children sum
       property */

    void convertTree(Node node)
    {
        int left_data = 0, right_data = 0, diff;

        /* If tree is empty or it's a leaf node then
         return true */
        if (node == null
                || (node.left == null && node.right == null))
            return;
        else
        {
            /* convert left and right subtrees  */
            convertTree(node.left);
            convertTree(node.right);

            /* If left child is not present then 0 is used
             as data of left child */
            if (node.left != null)
                left_data = node.left.data;

            /* If right child is not present then 0 is used
             as data of right child */
            if (node.right != null)
                right_data = node.right.data;

            /* get the diff of node's data and children sum */
            diff = left_data + right_data - node.data;

            /* If node's children sum is greater than the node's data */
            if (diff > 0)
                node.data = node.data + diff;

            /* THIS IS TRICKY --> If node's data is greater than children
               sum, then increment subtree by diff */
            if (diff < 0)

                // -diff is used to make diff positive
                increment(node, -diff); 
        }
    }

    /* This function is used to increment subtree by diff */
    void increment(Node node, int diff)
    {
        /* IF left child is not NULL then increment it */
        if (node.left != null)
        {
            node.left.data = node.left.data + diff;

            // Recursively call to fix the descendants of node->left
            increment(node.left, diff);
        }
        else if (node.right != null) // Else increment right child
        {
            node.right.data = node.right.data + diff;

            // Recursively call to fix the descendants of node->right
            increment(node.right, diff);
        }
    }

    /* Given a binary tree, printInorder() prints out its
     inorder traversal*/
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

    // Driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(50);
        tree.root.left = new Node(7);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(1);
        tree.root.right.right = new Node(30);

        System.out.println("Inorder traversal before conversion is :");
        tree.printInorder(tree.root);

        tree.convertTree(tree.root);
        System.out.println("");

        System.out.println("Inorder traversal after conversion is :");
        tree.printInorder(tree.root);

    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
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

# This function changes a tree to
# hold children sum property
def convertTree(node):

    left_data = 0
    right_data = 0
    diff=0

    # If tree is empty or it's a
    # leaf node then return true
    if (node == None or (node.left == None and
                         node.right == None)):
        return

    else:

        """ convert left and right subtrees """
        convertTree(node.left)
        convertTree(node.right)

    """ If left child is not present then 0
    is used as data of left child """
    if (node.left != None):
        left_data = node.left.data

    """ If right child is not present then 0
    is used as data of right child """
    if (node.right != None):
        right_data = node.right.data

    """ get the diff of node's data
        and children sum """
    diff = left_data + right_data - node.data

    """ If node's children sum is greater
        than the node's data """
    if (diff > 0):
        node.data = node.data + diff

    """ THIS IS TRICKY -. If node's data is
    greater than children sum, then increment
    subtree by diff """
    if (diff < 0):
        increment(node, -diff) # -diff is used to
                               # make diff positive

""" This function is used to increment
    subtree by diff """
def increment(node, diff):

    """ IF left child is not None
        then increment it """
    if(node.left != None):
        node.left.data = node.left.data + diff

        # Recursively call to fix the
        # descendants of node.left
        increment(node.left, diff)

    elif(node.right != None): # Else increment right child
        node.right.data = node.right.data + diff

        # Recursively call to fix the
        # descendants of node.right
        increment(node.right, diff)

""" Given a binary tree, printInorder()
prints out its inorder traversal"""
def printInorder(node):

    if (node == None):
        return

    """ first recur on left child """
    printInorder(node.left)

    """ then print the data of node """
    print(node.data,end=" ")

    """ now recur on right child """
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':
    root = newNode(50)
    root.left     = newNode(7)
    root.right     = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.left = newNode(1)
    root.right.right = newNode(30)

    print("Inorder traversal before conversion")
    printInorder(root)

    convertTree(root)

    print("\nInorder traversal after conversion ")
    printInorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to convert an arbitrary
// binary tree to a tree that holds
// children sum property
using System;

// A binary tree node
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

class GFG
{
public Node root;

/* This function changes a tree to
hold children sum property */
public virtual void convertTree(Node node)
{
    int left_data = 0, right_data = 0, diff;

    /* If tree is empty or it's a leaf
    node then return true */
    if (node == null || (node.left == null &&
                         node.right == null))
    {
        return;
    }
    else
    {
        /* convert left and right subtrees */
        convertTree(node.left);
        convertTree(node.right);

        /* If left child is not present then
        0 is used as data of left child */
        if (node.left != null)
        {
            left_data = node.left.data;
        }

        /* If right child is not present then
        0 is used as data of right child */
        if (node.right != null)
        {
            right_data = node.right.data;
        }

        /* get the diff of node's data
           and children sum */
        diff = left_data + right_data - node.data;

        /* If node's children sum is greater
           than the node's data */
        if (diff > 0)
        {
            node.data = node.data + diff;
        }

        /* THIS IS TRICKY --> If node's data is
        greater than children sum, then increment
        subtree by diff */
        if (diff < 0)
        {

            // -diff is used to make diff positive
            increment(node, -diff);
        }
    }
}

/* This function is used to increment
subtree by diff */
public virtual void increment(Node node, int diff)
{
    /* IF left child is not NULL then
    increment it */
    if (node.left != null)
    {
        node.left.data = node.left.data + diff;

        // Recursively call to fix the
        // descendants of node->left
        increment(node.left, diff);
    }
    else if (node.right != null) // Else increment right child
    {
        node.right.data = node.right.data + diff;

        // Recursively call to fix the
        // descendants of node->right
        increment(node.right, diff);
    }
}

/* Given a binary tree, printInorder()
prints out its inorder traversal*/
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
    tree.root = new Node(50);
    tree.root.left = new Node(7);
    tree.root.right = new Node(2);
    tree.root.left.left = new Node(3);
    tree.root.left.right = new Node(5);
    tree.root.right.left = new Node(1);
    tree.root.right.right = new Node(30);

    Console.WriteLine("Inorder traversal " +
                  "before conversion is :");
    tree.printInorder(tree.root);

    tree.convertTree(tree.root);
    Console.WriteLine("");

    Console.WriteLine("Inorder traversal " +
                   "after conversion is :");
    tree.printInorder(tree.root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

      // JavaScript program to convert an arbitrary binary tree
    // to a tree that holds children sum property

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let root;
    /* This function changes a tree to hold children sum
       property */

    function convertTree(node)
    {
        let left_data = 0, right_data = 0, diff;

        /* If tree is empty or it's a leaf node then
         return true */
        if (node == null
                || (node.left == null && node.right == null))
            return;
        else
        {
            /* convert left and right subtrees  */
            convertTree(node.left);
            convertTree(node.right);

            /* If left child is not present then 0 is used
             as data of left child */
            if (node.left != null)
                left_data = node.left.data;

            /* If right child is not present then 0 is used
             as data of right child */
            if (node.right != null)
                right_data = node.right.data;

            /* get the diff of node's data and children sum */
            diff = left_data + right_data - node.data;

            /* If node's children sum is greater
            than the node's data */
            if (diff > 0)
                node.data = node.data + diff;

            /* THIS IS TRICKY --> If node's data
               is greater than children
               sum, then increment subtree by diff */
            if (diff < 0)

                // -diff is used to make diff positive
                increment(node, -diff); 
        }
    }

    /* This function is used to increment subtree by diff */
    function increment(node, diff)
    {
        /* IF left child is not NULL then increment it */
        if (node.left != null)
        {
            node.left.data = node.left.data + diff;

            // Recursively call to fix the
            // descendants of node->left
            increment(node.left, diff);
        }
        else if (node.right != null) // Else increment right child
        {
            node.right.data = node.right.data + diff;

            // Recursively call to fix the
            // descendants of node->right
            increment(node.right, diff);
        }
    }

    /* Given a binary tree, printInorder() prints out its
     inorder traversal*/
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

    root = new Node(50);
    root.left = new Node(7);
    root.right = new Node(2);
    root.left.left = new Node(3);
    root.left.right = new Node(5);
    root.right.left = new Node(1);
    root.right.right = new Node(30);

    document.write("Inorder traversal before conversion is :" +
    "</br>");
    printInorder(root);

    convertTree(root);
    document.write("</br>");

    document.write("Inorder traversal after conversion is :" +
    "</br>");
    printInorder(root);

</script>
```

**输出:**

```
Inorder traversal before conversion is :
3 7 5 50 1 2 30
Inorder traversal after conversion is :
14 19 5 50 1 31 30
```

**时间复杂度:** O(n^2)，最坏情况的复杂度是对于倾斜的树，使得节点从根到叶是递减的顺序。

如果发现以上算法有什么 bug 或者有更好的方法解决同样的问题，请写评论。