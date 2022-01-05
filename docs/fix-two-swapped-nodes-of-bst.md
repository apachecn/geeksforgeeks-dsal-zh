# 一个 BST 的两个节点互换，修正 BST

> 原文:[https://www.geeksforgeeks.org/fix-two-swapped-nodes-of-bst/](https://www.geeksforgeeks.org/fix-two-swapped-nodes-of-bst/)

二叉查找树的两个节点被交换。修正 BST。

```
Input Tree:
         10
        /  \
       5    8
      / \
     2   20

In the above tree, nodes 20 and 8 must be swapped to fix the tree.  
Following is the output tree
         10
        /  \
       5    20
      / \
     2   8
```

对 BST 的有序遍历产生一个排序的数组。所以一个简单的方法是将输入树的有序遍历存储在一个辅助数组中。对辅助数组进行排序。最后，将辅助数组元素插回 BST，保持 BST 的结构不变。该方法的时间复杂度为 O(nLogn)，所需的辅助空间为 O(n)。

**我们可以在 O(n)个时间内解决这个问题，只需遍历给定的 BST** 。因为 BST 的有序遍历总是一个排序数组，所以这个问题可以简化为一个排序数组的两个元素被交换的问题。有两种情况需要我们处理:
**1。**交换的节点在 BST 的有序遍历中不相邻。

```
 For example, Nodes 5 and 25 are swapped in {3 5 7 8 10 15 20 25}. 
 The inorder traversal of the given tree is 3 25 7 8 10 15 20 5 
```

如果我们仔细观察，在有序遍历期间，我们发现节点 7 小于先前访问的节点 25。这里保存节点 25(前一个节点)的上下文。同样，我们发现节点 5 小于前一个节点 20。这一次，我们保存节点 5(当前节点)的上下文。最后，交换两个节点的值。
**2。**交换的节点在 BST 的有序遍历中是相邻的。

```
  For example, Nodes 7 and 8 are swapped in {3 5 7 8 10 15 20 25}. 
  The inorder traversal of the given tree is 3 5 8 7 10 15 20 25 
```

与案例#1 不同，这里只存在一个节点值小于前一个节点值的点。例如节点 7 小于节点 8。

**如何解决？** *我们会保持三分球，第一，中，最后。当我们找到当前节点值小于前一个节点值的第一个点时，我们用前一个节点&更新第一个，用当前节点更新中间。当我们找到当前节点值小于前一个节点值的第二个点时，我们用当前节点更新最后一个。在#2 的情况下，我们永远找不到第二点。所以，最后一个指针不会被更新。处理后，如果最后一个节点值为空，则 BST 的两个交换节点相邻*。

下面是给定代码的实现。

## C++

```
// Two nodes in the BST's swapped, correct the BST.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node *left, *right;
};

// A utility function to swap two integers
void swap( int* a, int* b )
{
    int t = *a;
    *a = *b;
    *b = t;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node *)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

// This function does inorder traversal to find out the two swapped nodes.
// It sets three pointers, first, middle and last.  If the swapped nodes are
// adjacent to each other, then first and middle contain the resultant nodes
// Else, first and last contain the resultant nodes
void correctBSTUtil( struct node* root, struct node** first,
                     struct node** middle, struct node** last,
                     struct node** prev )
{
    if( root )
    {
        // Recur for the left subtree
        correctBSTUtil( root->left, first, middle, last, prev );

        // If this node is smaller than the previous node, it's violating
        // the BST rule.
        if (*prev && root->data < (*prev)->data)
        {

            // If this is first violation, mark these two nodes as
            // 'first' and 'middle'
            if ( !*first )
            {
                *first = *prev;
                *middle = root;
            }

            // If this is second violation, mark this node as last
            else
                *last = root;
        }

        // Mark this node as previous
        *prev = root;

        // Recur for the right subtree
        correctBSTUtil( root->right, first, middle, last, prev );
    }
}

// A function to fix a given BST where two nodes are swapped.  This
// function uses correctBSTUtil() to find out two nodes and swaps the
// nodes to fix the BST
void correctBST( struct node* root )
{

    // Initialize pointers needed for correctBSTUtil()
    struct node *first, *middle, *last, *prev;
    first = middle = last = prev = NULL;

    // Set the pointers to find out two nodes
    correctBSTUtil( root, &first, &middle, &last, &prev );

    // Fix (or correct) the tree
    if( first && last )
        swap( &(first->data), &(last->data) );
    else if( first && middle ) // Adjacent nodes swapped
        swap( &(first->data), &(middle->data) );

    // else nodes have not been swapped, passed tree is really BST.
}

/* A utility function to print Inorder traversal */
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout <<"  "<< node->data;
    printInorder(node->right);
}

/* Driver program to test above functions*/
int main()
{
    /*   6
        /  \
       10    2
      / \   / \
     1   3 7  12
     10 and 2 are swapped
    */

    struct node *root = newNode(6);
    root->left        = newNode(10);
    root->right       = newNode(2);
    root->left->left  = newNode(1);
    root->left->right = newNode(3);
    root->right->right = newNode(12);
    root->right->left = newNode(7);

    cout <<"Inorder Traversal of the original tree \n";
    printInorder(root);

    correctBST(root);

    cout <<"\nInorder Traversal of the fixed tree \n";
    printInorder(root);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// Two nodes in the BST's swapped, correct the BST.
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node *left, *right;
};

// A utility function to swap two integers
void swap( int* a, int* b )
{
    int t = *a;
    *a = *b;
    *b = t;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node *)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

// This function does inorder traversal to find out the two swapped nodes.
// It sets three pointers, first, middle and last.  If the swapped nodes are
// adjacent to each other, then first and middle contain the resultant nodes
// Else, first and last contain the resultant nodes
void correctBSTUtil( struct node* root, struct node** first,
                     struct node** middle, struct node** last,
                     struct node** prev )
{
    if( root )
    {
        // Recur for the left subtree
        correctBSTUtil( root->left, first, middle, last, prev );

        // If this node is smaller than the previous node, it's violating
        // the BST rule.
        if (*prev && root->data < (*prev)->data)
        {
            // If this is first violation, mark these two nodes as
            // 'first' and 'middle'
            if ( !*first )
            {
                *first = *prev;
                *middle = root;
            }

            // If this is second violation, mark this node as last
            else
                *last = root;
        }

        // Mark this node as previous
        *prev = root;

        // Recur for the right subtree
        correctBSTUtil( root->right, first, middle, last, prev );
    }
}

// A function to fix a given BST where two nodes are swapped.  This
// function uses correctBSTUtil() to find out two nodes and swaps the
// nodes to fix the BST
void correctBST( struct node* root )
{
    // Initialize pointers needed for correctBSTUtil()
    struct node *first, *middle, *last, *prev;
    first = middle = last = prev = NULL;

    // Set the pointers to find out two nodes
    correctBSTUtil( root, &first, &middle, &last, &prev );

    // Fix (or correct) the tree
    if( first && last )
        swap( &(first->data), &(last->data) );
    else if( first && middle ) // Adjacent nodes swapped
        swap( &(first->data), &(middle->data) );

    // else nodes have not been swapped, passed tree is really BST.
}

/* A utility function to print Inorder traversal */
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

/* Driver program to test above functions*/
int main()
{
    /*   6
        /  \
       10    2
      / \   / \
     1   3 7  12
     10 and 2 are swapped
    */

    struct node *root = newNode(6);
    root->left        = newNode(10);
    root->right       = newNode(2);
    root->left->left  = newNode(1);
    root->left->right = newNode(3);
    root->right->right = newNode(12);
    root->right->left = newNode(7);

    printf("Inorder Traversal of the original tree \n");
    printInorder(root);

    correctBST(root);

    printf("\nInorder Traversal of the fixed tree \n");
    printInorder(root);

    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to correct the BST 
// if two nodes are swapped
import java.util.*;
import java.lang.*;
import java.io.*;

class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class BinaryTree
{
    Node first, middle, last, prev;

    // This function does inorder traversal
    // to find out the two swapped nodes.
    // It sets three pointers, first, middle
    // and last. If the swapped nodes are
    // adjacent to each other, then first 
    // and middle contain the resultant nodes
    // Else, first and last contain the 
    // resultant nodes
    void correctBSTUtil( Node root)
    {
        if( root != null )
        {
            // Recur for the left subtree
            correctBSTUtil( root.left);

            // If this node is smaller than
            // the previous node, it's 
            // violating the BST rule.
            if (prev != null && root.data <
                                prev.data)
            {
                // If this is first violation,
                // mark these two nodes as
                // 'first' and 'middle'
                if (first == null)
                {
                    first = prev;
                    middle = root;
                }

                // If this is second violation,
                // mark this node as last
                else
                    last = root;
            }

            // Mark this node as previous
            prev = root;

            // Recur for the right subtree
            correctBSTUtil( root.right);
        }
    }

    // A function to fix a given BST where 
    // two nodes are swapped. This function 
    // uses correctBSTUtil() to find out 
    // two nodes and swaps the nodes to 
    // fix the BST
    void correctBST( Node root )
    {
        // Initialize pointers needed 
        // for correctBSTUtil()
        first = middle = last = prev = null;

        // Set the pointers to find out 
        // two nodes
        correctBSTUtil( root );

        // Fix (or correct) the tree
        if( first != null && last != null )
        {
            int temp = first.data;
            first.data = last.data;
            last.data = temp; 
        }
        // Adjacent nodes swapped
        else if( first != null && middle !=
                                    null ) 
        {
            int temp = first.data;
            first.data = middle.data;
            middle.data = temp;
        }

        // else nodes have not been swapped,
        // passed tree is really BST.
    }

    /* A utility function to print 
     Inorder traversal */
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.print(" " + node.data);
        printInorder(node.right);
    }

    // Driver program to test above functions
    public static void main (String[] args) 
    {
        /*   6
            / \
           10  2
          / \ / \
         1  3 7 12

        10 and 2 are swapped
        */

        Node root = new Node(6);
        root.left = new Node(10);
        root.right = new Node(2);
        root.left.left = new Node(1);
        root.left.right = new Node(3);
        root.right.right = new Node(12);
        root.right.left = new Node(7);

        System.out.println("Inorder Traversal"+
                        " of the original tree");
        BinaryTree tree = new BinaryTree();
        tree.printInorder(root);

        tree.correctBST(root);

        System.out.println("\nInorder Traversal"+
                          " of the fixed tree");
        tree.printInorder(root);
    }
}
// This code is contributed by Chhavi

```

## 蟒蛇 3

```
# Python3 program to correct the BST  
# if two nodes are swapped 
class Node: 

    # Constructor to create a new node 
    def __init__(self, data):

        self.key = data 
        self.left = None
        self.right = None

# Utility function to track the nodes
# that we have to swap
def correctBstUtil(root, first, middle,
                   last, prev):

    if(root):

        # Recur for the left sub tree
        correctBstUtil(root.left, first,
                       middle, last, prev)

        # If this is the first violation, mark these 
        # two nodes as 'first and 'middle'
        if(prev[0] and root.key < prev[0].key):
            if(not first[0]):
                first[0] = prev[0]
                middle[0] = root
            else:

                # If this is the second violation,
                # mark this node as last
                last[0] = root

        prev[0] = root

        # Recur for the right subtree
        correctBstUtil(root.right, first, 
                       middle, last, prev)

# A function to fix a given BST where 
# two nodes are swapped. This function
# uses correctBSTUtil() to find out two
# nodes and swaps the nodes to fix the BST 
def correctBst(root):

    # Followed four lines just for forming
    # an array with only index 0 filled 
    # with None and we will update it accordingly.
    # we made it null so that we can fill 
    # node data in them.
    first = [None]
    middle = [None]
    last = [None]
    prev = [None]

    # Setting arrays (having zero index only) 
    # for capturing the required node
    correctBstUtil(root, first, middle,
                   last, prev)

    # Fixing the two nodes
    if(first[0] and last[0]):

        # Swapping for first and last key values
        first[0].key, last[0].key = (last[0].key, 
                                    first[0].key)

    elif(first[0] and middle[0]):

        # Swapping for first and middle key values
        first[0].key, middle[0].key = (middle[0].key,
                                        first[0].key)

    # else tree will be fine

# Function to print inorder
# traversal of tree
def PrintInorder(root):

    if(root):
        PrintInorder(root.left)
        print(root.key, end = " ")
        PrintInorder(root.right)

    else:
        return

# Driver code

#      6
#     /   \
#   10    2
#  / \   / \
# 1   3 7   12

# Following 7 lines are for tree formation
root = Node(6) 
root.left = Node(10) 
root.right = Node(2) 
root.left.left = Node(1) 
root.left.right = Node(3) 
root.right.left = Node(7) 
root.right.right = Node(12) 

# Printing inorder traversal of normal tree
print("inorder traversal of normal tree")
PrintInorder(root)
print("")

# Function call to do the task
correctBst(root)

# Printing inorder for corrected Bst tree
print("")
print("inorder for corrected BST")

PrintInorder(root)

# This code is contributed by rajutkarshai

```

## C#

```
// C# program to correct the BST 
// if two nodes are swapped
using System;
class Node{

public int data;
public Node left, right;
public Node(int d) 
{
  data = d;
  left = right = null;
}
}

class BinaryTree
{
  Node first, middle, 
       last, prev;

// This function does inorder traversal
// to find out the two swapped nodes.
// It sets three pointers, first, middle
// and last. If the swapped nodes are
// adjacent to each other, then first 
// and middle contain the resultant nodes
// Else, first and last contain the 
// resultant nodes
void correctBSTUtil( Node root)
{
  if( root != null )
  {
    // Recur for the 
    // left subtree
    correctBSTUtil(root.left);

    // If this node is smaller than
    // the previous node, it's 
    // violating the BST rule.
    if (prev != null && root.data <
        prev.data)
    {
      // If this is first violation,
      // mark these two nodes as
      // 'first' and 'middle'
      if (first == null)
      {
        first = prev;
        middle = root;
      }

      // If this is second violation,
      // mark this node as last
      else
        last = root;
    }

    // Mark this node 
    // as previous
    prev = root;

    // Recur for the
    // right subtree
    correctBSTUtil(root.right);
  }
}

// A function to fix a given BST where 
// two nodes are swapped. This function 
// uses correctBSTUtil() to find out 
// two nodes and swaps the nodes to 
// fix the BST
void correctBST( Node root )
{
  // Initialize pointers needed 
  // for correctBSTUtil()
  first = middle = last = 
          prev = null;

  // Set the pointers to 
  // find out two nodes
  correctBSTUtil(root);

  // Fix (or correct) 
  // the tree
  if(first != null && 
     last != null)
  {
    int temp = first.data;
    first.data = last.data;
    last.data = temp; 
  }

  // Adjacent nodes swapped
  else if(first != null && 
          middle != null) 
  {
    int temp = first.data;
    first.data = middle.data;
    middle.data = temp;
  }

  // else nodes have not been 
  // swapped, passed tree is 
  // really BST.
}

// A utility function to print 
// Inorder traversal 
void printInorder(Node node)
{
  if (node == null)
    return;
  printInorder(node.left);
  Console.Write(" " + node.data);
  printInorder(node.right);
}

// Driver code
public static void Main(String[] args) 
{
  /*         6
            / \
           10  2
          / \ / \
         1  3 7 12

        10 and 2 are swapped
        */

  Node root = new Node(6);
  root.left = new Node(10);
  root.right = new Node(2);
  root.left.left = new Node(1);
  root.left.right = new Node(3);
  root.right.right = new Node(12);
  root.right.left = new Node(7);

  Console.WriteLine("Inorder Traversal" +
                    " of the original tree");
  BinaryTree tree = new BinaryTree();
  tree.printInorder(root);
  tree.correctBST(root);
  Console.WriteLine("\nInorder Traversal" +
                    " of the fixed tree");
  tree.printInorder(root);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to correct the BST 
// if two nodes are swapped

class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    var first, middle, last, prev;

    // This function does inorder traversal
    // to find out the two swapped nodes.
    // It sets three pointers, first, middle
    // and last. If the swapped nodes are
    // adjacent to each other, then first
    // and middle contain the resultant nodes
    // Else, first and last contain the
    // resultant nodes
    function correctBSTUtil(root) {
        if (root != null) {
            // Recur for the left subtree
            correctBSTUtil(root.left);

            // If this node is smaller than
            // the previous node, it's
            // violating the BST rule.
            if (prev != null && root.data < prev.data) {
                // If this is first violation,
                // mark these two nodes as
                // 'first' and 'middle'
                if (first == null) {
                    first = prev;
                    middle = root;
                }

                // If this is second violation,
                // mark this node as last
                else
                    last = root;
            }

            // Mark this node as previous
            prev = root;

            // Recur for the right subtree
            correctBSTUtil(root.right);
        }
    }

    // A function to fix a given BST where
    // two nodes are swapped. This function
    // uses correctBSTUtil() to find out
    // two nodes and swaps the nodes to
    // fix the BST
    function correctBST(root) {
        // Initialize pointers needed
        // for correctBSTUtil()
        first = middle = last = prev = null;

        // Set the pointers to find out
        // two nodes
        correctBSTUtil(root);

        // Fix (or correct) the tree
        if (first != null && last != null) {
            var temp = first.data;
            first.data = last.data;
            last.data = temp;
        }
        // Adjacent nodes swapped
        else if (first != null && middle != null) {
            var temp = first.data;
            first.data = middle.data;
            middle.data = temp;
        }

        // else nodes have not been swapped,
        // passed tree is really BST.
    }

    /*
     * A utility function to print Inorder traversal
     */
    function printInorder(node) {
        if (node == null)
            return;
        printInorder(node.left);
        document.write(" " + node.data);
        printInorder(node.right);
    }

    // Driver program to test above functions

        /*
         * 6 / \ 10 2 / \ / \ 1 3 7 12
         * 
         * 10 and 2 are swapped
         */

var root = new Node(6);
        root.left = new Node(10);
        root.right = new Node(2);
        root.left.left = new Node(1);
        root.left.right = new Node(3);
        root.right.right = new Node(12);
        root.right.left = new Node(7);

        document.write("Inorder Traversal" +
        " of the original tree<br/>");
        printInorder(root);

        correctBST(root);

        document.write("<br/>Inorder Traversal" + 
        " of the fixed tree<br/>");
        printInorder(root);

// This code contributed by aashish1995

</script>

```

**输出:**

```
Inorder Traversal of the original tree
1 10 3 6 7 2 12
Inorder Traversal of the fixed tree
1 2 3 6 7 10 12
```

**时间复杂度:** O(n)

以上代码的不同测试用例见[本](http://ideone.com/uNlPx)。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息