# 交换一个 BST 的两个节点，纠正 BST | Set-2

> 原文:[https://www . geesforgeks . org/BST 的两个节点被交换-纠正-bst-set-2/](https://www.geeksforgeeks.org/two-nodes-of-a-bst-are-swapped-correct-the-bst-set-2/)

给定一个交换了二叉查找树的两个节点的二叉查找树。任务是修复(或纠正)基站。
**注**:BST 不会有重复。

**示例**:

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

**进场:**

*   按顺序遍历 BST，并将节点存储在一个向量中。
*   然后这个向量在创建副本后被排序。
*   当数组几乎被排序时，使用插入排序，因为它工作得最好和最快。在这个问题中，只有两个元素将被替换，所以插入排序将在线性时间内工作。
*   排序后，比较排序后的向量和之前创建的向量的副本，通过这种方式，找出错误-一些节点，并通过在树中找到它们并交换它们来修复它们。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node has data, pointer
// to left child and a pointer to right child
struct node {
    int data;
    struct node *left, *right;
    node(int x)
    {
        data = x;
        left = right = NULL;
    }
};

// Utility function for insertion sort
void insertionSort(vector<int>& v, int n)
{
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = v[i];
        j = i - 1;
        while (j >= 0 && v[j] > key) {
            v[j + 1] = v[j];
            j = j - 1;
        }
        v[j + 1] = key;
    }
}

// Utility function to create a vector
// with inorder traversal of a binary tree
void inorder(node* root, vector<int>& v)
{
    // Base cases
    if (!root)
        return;

    // Recursive call for left subtree
    inorder(root->left, v);

    // Insert node into vector
    v.push_back(root->data);

    // Recursive call for right subtree
    inorder(root->right, v);
}

// Function to exchange data
// for incorrect nodes
void find(node* root, int res, int res2)
{
    // Base cases
    if (!root) {
        return;
    }

    // Recursive call to find
    // the node in left subtree
    find(root->left, res, res2);

    // Check if current node
    // is incorrect and exchange
    if (root->data == res) {
        root->data = res2;
    }
    else if (root->data == res2) {
        root->data = res;
    }

    // Recursive call to find
    // the node in right subtree
    find(root->right, res, res2);
}

// Primary function to fix the two nodes
struct node* correctBST(struct node* root)
{
    // Vector to store the
    // inorder traversal of tree
    vector<int> v;

    // Function call to insert
    // nodes into vector
    inorder(root, v);

    // create a copy of the vector
    vector<int> v1 = v;

    // Sort the original vector thereby
    // making it a valid BST's inorder
    insertionSort(v, v.size());

    // Traverse through both vectors and
    // compare misplaced values in original BST
    for (int i = 0; i < v.size(); i++) {

        // Find the mismatched values
        // and interchange them
        if (v[i] != v1[i]) {

            // Find and exchange the
            // data of the two nodes
            find(root, v1[i], v[i]);

            // As it given only two values are
            // wrong we don't need to check further
            break;
        }
    }

    // Return the root of corrected BST
    return root;
}

// A utility function to
// print Inorder traversal
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

int main()
{
    struct node* root = new node(6);
    root->left = new node(10);
    root->right = new node(2);
    root->left->left = new node(1);
    root->left->right = new node(3);
    root->right->right = new node(12);
    root->right->left = new node(7);

    printf("Inorder Traversal of the");
    printf("original tree \n");

    printInorder(root);

    correctBST(root);

    printf("\nInorder Traversal of the");
    printf("fixed tree \n");

    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.ArrayList;
class GFG
{

    // A binary tree node has data, pointer
    // to left child and a pointer to right child
    static class node
    {
        int data;
        node left, right;

        public node(int x)
        {
            data = x;
            left = right = null;
        }
    };

    // Utility function for insertion sort
    static void insertionSort(ArrayList<Integer> v, int n) {
        int i, key, j;
        for (i = 1; i < n; i++) {
            key = v.get(i);
            j = i - 1;
            while (j >= 0 && v.get(j) > key) {
                v.set(j + 1, v.get(i));
                j = j - 1;
            }
            v.set(j + 1, key);
        }
    }

    // Utility function to create a vector
    // with inorder traversal of a binary tree
    static void inorder(node root, ArrayList<Integer> v) {
        // Base cases
        if (root == null)
            return;

        // Recursive call for left subtree
        inorder(root.left, v);

        // Insert node into vector
        v.add(root.data);

        // Recursive call for right subtree
        inorder(root.right, v);
    }

    // Function to exchange data
    // for incorrect nodes
    static void find(node root, int res, int res2)
    {

        // Base cases
        if (root == null) {
            return;
        }

        // Recursive call to find
        // the node in left subtree
        find(root.left, res, res2);

        // Check if current node
        // is incorrect and exchange
        if (root.data == res) {
            root.data = res2;
        } else if (root.data == res2) {
            root.data = res;
        }

        // Recursive call to find
        // the node in right subtree
        find(root.right, res, res2);
    }

    // Primary function to fix the two nodes
    static node correctBST(node root)
    {

        // Vector to store the
        // inorder traversal of tree
        ArrayList<Integer> v = new ArrayList<>();

        // Function call to insert
        // nodes into vector
        inorder(root, v);

        // create a copy of the vector
        ArrayList<Integer> v1 = new ArrayList<>(v);

        // Sort the original vector thereby
        // making it a valid BST's inorder
        insertionSort(v, v.size());

        // Traverse through both vectors and
        // compare misplaced values in original BST
        for (int i = 0; i < v.size(); i++) {

            // Find the mismatched values
            // and interchange them
            if (v.get(i) != v1.get(i)) {

                // Find and exchange the
                // data of the two nodes
                find(root, v1.get(i), v.get(i));

                // As it given only two values are
                // wrong we don't need to check further
                break;
            }
        }

        // Return the root of corrected BST
        return root;
    }

    // A utility function to
    // print Inorder traversal
    static void printInorder(node node) {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.printf("%d ", node.data);
        printInorder(node.right);
    }

  // Driver code
    public static void main(String[] args) {

        node root = new node(6);
        root.left = new node(10);
        root.right = new node(2);
        root.left.left = new node(1);
        root.left.right = new node(3);
        root.right.right = new node(12);
        root.right.left = new node(7);

        System.out.printf("Inorder Traversal of the");
        System.out.printf("original tree \n");

        printInorder(root);

        correctBST(root);

        System.out.printf("\nInorder Traversal of the");
        System.out.printf("fixed tree \n");

        printInorder(root);

    }
}

    // This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# A binary tree node has data, pointer
# to left child and a pointer to right child
class node:
    def __init__(self, x):
        self.data = x
        self.left = self.right = None

# Utility function for insertion sort

def insertionSort(v, n):
    for i in range(n):
        key = v[i]
        j = i - 1
        while (j >= 0 and v[j] > key):
            v[j + 1] = v[j]
            j = j - 1
        v[j + 1] = key

# Utility function to create a list
# with inorder traversal of a binary tree

def inorder(root, v):

    # Base cases
    if (not root):
        return

    # Recursive call for left subtree
    inorder(root.left, v)

    # Insert node into list
    v.append(root.data)

    # Recursive call for right subtree
    inorder(root.right, v)

# Function to exchange data
# for incorrect nodes

def find(root, res, res2):

    # Base cases
    if not root:
        return

    # Recursive call to find
    # the node in left subtree
    find(root.left, res, res2)

    # Check if current node
    # is incorrect and exchange
    if (root.data == res):
        root.data = res2

    elif (root.data == res2):
        root.data = res

    # Recursive call to find
    # the node in right subtree
    find(root.right, res, res2)

# Primary function to fix the two nodes

def correctBST(root):

    # List to store the
    # inorder traversal of tree
    v = []

    # Function call to insert
    # nodes into list
    inorder(root, v)

    # create a copy of the list
    v1 = v.copy()

    # Sort the original list thereby
    # making it a valid BST's inorder
    insertionSort(v, len(v))

    # Traverse through both list and
    # compare misplaced values in original BST
    for i in range(len(v)):

        # Find the mismatched values
        # and interchange them
        if (v[i] != v1[i]):

            # Find and exchange the
            # data of the two nodes
            find(root, v1[i], v[i])

            # As it given only two values are
            # wrong we don't need to check further
            break
    # Return the root of corrected BST
    return root

# A utility function to
# print Inorder traversal

def printInorder(node):

    if (node == None):
        return
    printInorder(node.left)
    print("{} ".format(node.data), end=' ')
    printInorder(node.right)

if __name__ == '__main__':
    root = node(6)
    root.left = node(10)
    root.right = node(2)
    root.left.left = node(1)
    root.left.right = node(3)
    root.right.right = node(12)
    root.right.left = node(7)

    print("Inorder Traversal of the original tree ")

    printInorder(root)

    correctBST(root)

    print()
    print("Inorder Traversal of the fixed tree ")

    printInorder(root)
    print()
# This code is contributed by
# Amartya Ghosh
```

**Output**

```
Inorder Traversal of theoriginal tree 
1 10 3 6 7 2 12 
Inorder Traversal of thefixed tree 
1 2 3 6 7 10 12 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)，其中 N 为二叉树中的节点数。

**方法二:**

要理解这一点，首先需要理解[T1】莫里斯遍历 T3】或者](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)[T5】莫里斯穿线 T7】遍历。它利用叶节点的左/右指针在二叉树上实现 O(1)空间遍历。](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)

因此，在这种方法中，我们可以在 **O(n)时间和 O(1)空间，即常数空间**中求解这个问题，只需遍历给定的 BST。由于 BST 的有序遍历总是一个排序的数组，所以这个问题可以简化为一个排序数组的两个元素被交换的问题。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std ;

/* A binary tree node has data,
pointer to left child
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

/* Helper function that allocates
a new node with the
given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;
    return(Node);
}

// Function for inorder traversal using
// Morris Traversal
void MorrisTraversal(struct node* root,
                     struct node* &first,
                     struct node* &last,
                     struct node* &prev )
{
       // Current node
      struct  node* curr = root;

        while(curr != NULL)
        {
            if(curr->left==NULL)
            {

                // If this node is smaller than
                // the previous node, it's 
                // violating the BST rule.
                if(first == NULL && prev != NULL &&
                   prev->data > curr->data)
                {
                    // If this is first violation,
                    // mark these two nodes as
                    // 'first' and 'last'
                    first = prev;
                    last = curr;
                }

                if(first != NULL &&
                   prev->data > curr->data)
                {
                  // If this is second violation,         
                  // mark this node as last
                    last = curr;
                }
                prev = curr;

                curr = curr->right;
            }
            else
            {
                  /* Find the inorder predecessor of current */
                 struct   node*  pre = curr->left;
                while(pre->right!=NULL && pre->right!=curr)
                {
                    pre = pre->right;
                }

                /* Make current as right child of
                its inorder predecessor */
                if(pre->right==NULL)
                {
                    pre->right = curr;
                    curr = curr->left;
                }
                else
                {
                    // If this node is smaller than
                    // the previous node, it's 
                    // violating the BST rule.
                    if(first == NULL && prev!=NULL &&
                       prev->data > curr->data)
                    {
                          // If this is first violation,
                        // mark these two nodes as
                        // 'first' and 'last'
                        first = prev;
                        last = curr;
                    }

                    if(first != NULL &&
                       prev->data > curr->data)
                    {
                          // If this is second violation,
                           // mark this node as last
                        last = curr;
                    }
                    prev = curr;

                      /* Revert the changes made in the
                    'if' part to restore the 
                    original tree i.e., fix the
                    right child of predecessor*/
                    pre->right = NULL;
                    curr = curr->right;
                }
            }
        }
    }

// A function to fix a given BST
// where two nodes are swapped. This
// function uses correctBSTUtil()
// to find out two nodes and swaps the
// nodes to fix the BST
void correctBST( struct node* root )
{
    // Initialize pointers needed
    // for correctBSTUtil()
    struct node* first =NULL ;
    struct node* last = NULL ;
    struct node* prev =NULL ;

    // Set the pointers to find out two nodes
    MorrisTraversal( root ,first ,last , prev);

    // Fix (or correct) the tree
    swap( &(first->data), &(last->data) );

    // else nodes have not been swapped,
    // passed tree is really BST.
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

/* Driver Code */
int main()
{
    /*   6
        / \
       10  2
      / \ / \
     1  3 7 12
    10 and 2 are swapped
    */

    struct node *root = newNode(6);
    root->left     = newNode(10);
    root->right     = newNode(2);
    root->left->left = newNode(1);
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
// This code is contributed by
// Sagara Jangra and Naresh Saharan
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

class BinaryTree {

       Node first, last, prev;

    // This function does inorder traversal
    // Using Morris Traversal to find out the two
      // swapped nodes.
    void MorrisTraversal( Node root)
    {
       // current node
        Node curr = root;
        Node pre = null;
        while(curr != null)
        {
            if(curr.left==null)
            {

              // If this node is smaller than
              // the previous node, it's 
              // violating the BST rule.

                if(first == null && prev != null &&
                   prev.data > curr.data)
                {
                      // If this is first violation,
                    // mark these two nodes as
                    // 'first' and 'last'
                    first = prev;
                    last = curr;
                }

                if(first != null &&
                   prev.data > curr.data)
                {
                  // If this is second violation,         
                  // mark this node as last
                    last = curr;
                }
                prev = curr;

                curr = curr.right;
            }
            else
            {
                  /* Find the inorder predecessor of current */
                pre = curr.left;
                while(pre.right!=null &&
                      pre.right!=curr)
                {
                    pre = pre.right;
                }

                // Make current as right child of
                // its inorder predecessor */
                if(pre.right==null)
                {
                    pre.right = curr;
                    curr = curr.left;
                }
                else
                {
                    // If this node is smaller than
                    // the previous node, it's 
                    // violating the BST rule.
                    if(first == null && prev!=null &&
                       prev.data > curr.data)
                    {
                          // If this is first violation,
                        // mark these two nodes as
                        // 'first' and 'last'
                        first = prev;
                        last = curr;
                    }

                    if(first != null &&
                       prev.data > curr.data)
                    {
                          // If this is second violation,
                           // mark this node as last
                        last = curr;
                    }
                    prev = curr;

                      /* Revert the changes made in the
                    'if' part to restore the 
                    original tree i.e., fix the
                    right child of predecessor*/
                    pre.right = null;
                    curr = curr.right;
                }
            }
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
        first = last = prev = null;

        // Set the pointers to find out 
        // two nodes
        MorrisTraversal( root );

        // Fix (or correct) the tree
          int temp = first.data;
        first.data = last.data;
          last.data = temp; 
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

    // Driver Code
    public static void main (String[] args) 
    {
        /*   6
            / \
           10  2
          / \ / \
         1  3 7 12

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
// This code is contributed by
// Naresh Saharan and Sagara Jangra
```

## C#

```
// C# program to correct the BST 
// if two nodes are swapped
using System;
public

 class Node {

    public

 int data;
   public

  Node left, right;

    public Node(int d) {
        data = d;
        left = right = null;
    }
}

public class GFG {

       Node first, last, prev;

    // This function does inorder traversal
    // Using Morris Traversal to find out the two
      // swapped nodes.
    void MorrisTraversal( Node root)
    {
       // current node
        Node curr = root;
        Node pre = null;
        while(curr != null)
        {
            if(curr.left==null)
            {

              // If this node is smaller than
              // the previous node, it's 
              // violating the BST rule.

                if(first == null && prev != null &&
                   prev.data > curr.data)
                {
                      // If this is first violation,
                    // mark these two nodes as
                    // 'first' and 'last'
                    first = prev;
                    last = curr;
                }

                if(first != null &&
                   prev.data > curr.data)
                {
                  // If this is second violation,         
                  // mark this node as last
                    last = curr;
                }
                prev = curr;

                curr = curr.right;
            }
            else
            {
                  /* Find the inorder predecessor of current */
                pre = curr.left;
                while(pre.right!=null &&
                      pre.right!=curr)
                {
                    pre = pre.right;
                }

                // Make current as right child of
                // its inorder predecessor */
                if(pre.right==null)
                {
                    pre.right = curr;
                    curr = curr.left;
                }
                else
                {
                    // If this node is smaller than
                    // the previous node, it's 
                    // violating the BST rule.
                    if(first == null && prev!=null &&
                       prev.data > curr.data)
                    {
                          // If this is first violation,
                        // mark these two nodes as
                        // 'first' and 'last'
                        first = prev;
                        last = curr;
                    }

                    if(first != null &&
                       prev.data > curr.data)
                    {
                          // If this is second violation,
                           // mark this node as last
                        last = curr;
                    }
                    prev = curr;

                      /* Revert the changes made in the
                    'if' part to restore the 
                    original tree i.e., fix the
                    right child of predecessor*/
                    pre.right = null;
                    curr = curr.right;
                }
            }
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
        first = last = prev = null;

        // Set the pointers to find out 
        // two nodes
        MorrisTraversal( root );

        // Fix (or correct) the tree
          int temp = first.data;
        first.data = last.data;
          last.data = temp; 
    }

       /* A utility function to print 
     Inorder traversal */
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        Console.Write(" " + node.data);
        printInorder(node.right);
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        /*   6
            / \
           10  2
          / \ / \
         1  3 7 12

        10 and 2 are swapped
        */

        Node root = new Node(6);
        root.left = new Node(10);
        root.right = new Node(2);
        root.left.left = new Node(1);
        root.left.right = new Node(3);
        root.right.right = new Node(12);
        root.right.left = new Node(7);

        Console.WriteLine("Inorder Traversal"+
                        " of the original tree");
        GFG tree = new GFG();
        tree.printInorder(root);

        tree.correctBST(root);

        Console.WriteLine("\nInorder Traversal"+
                          " of the fixed tree");
        tree.printInorder(root);
    }
}
// This code contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# A binary tree node has data,
# pointer to left child
# and a pointer to right child
class node:
    def __init__(self, d):
        self.data = d
        self.left = self.right = None

# Function for inorder traversal using
# Morris Traversal

def MorrisTraversal(root, first, last, prev):

    # Current node
    curr = root

    while(curr != None):

        if(curr.left == None):

            # If this node is smaller than
            # the previous node, it's
            # violating the BST rule.
            if(first == None and prev is not None and prev.data > curr.data):
                # If this is first violation,
                # mark these two nodes as
                # 'first' and 'last'
                first = prev
                last = curr

            if(first != None and prev.data > curr.data):

                # If this is second violation,
                # mark this node as last
                last = curr
            prev = curr

            curr = curr.right
        else:
            # Find the inorder predecessor of current
            pre = curr.left
            while(pre.right != None and pre.right != curr):
                pre = pre.right

            # Make current as right child of
            # its inorder predecessor
            if(pre.right == None):
                pre.right = curr
                curr = curr.left
            else:

                # If this node is smaller than
                # the previous node, it's
                # violating the BST rule.
                if(first == None and prev != None and prev.data > curr.data):
                    # If this is first violation
                    # mark these two nodes as
                    # 'first' and 'last'
                    first = prev
                    last = curr

                if(first != None and prev.data > curr.data):
                    # If this is second violation,
                    # mark this node as last
                    last = curr
                prev = curr

                # Revert the changes made in the
                # 'if' part to restore the
                # original tree i.e., fix the
                # right child of predecessor
                pre.right = None
                curr = curr.right
    return first,last

# A function to fix a given BST
# where two nodes are swapped. This
# function uses correctBSTUtil()
# to find out two nodes and swaps the
# nodes to fix the BST

def correctBST(root):
    # Initialize pointers needed
    # for correctBSTUtil()
    first = last = prev = None

    # Set the pointers to find out two nodes
    first,last=MorrisTraversal(root, first, last, prev)

    # Fix (or correct) the tree
    first.data, last.data = last.data, first.data

    # else nodes have not been swapped,
    # passed tree is really BST.

# A utility function to print Inorder traversal

def printInorder(node):
    if (node == None):
        return
    printInorder(node.left)
    print("{} ".format(node.data),end=' ')
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':
    #      6
    #     / \
    #    10  2
    #   / \ / \
    #  1  3 7 12
    # 10 and 2 are swapped

    root = node(6)
    root.left = node(10)
    root.right = node(2)
    root.left.left = node(1)
    root.left.right = node(3)
    root.right.right = node(12)
    root.right.left = node(7)

    print("Inorder Traversal of the original tree ")
    printInorder(root)

    correctBST(root)

    print()
    print("Inorder Traversal of the fixed tree ")
    printInorder(root)
# This code is contributed by
# Amartya Ghosh
```

**Output**

```
Inorder Traversal of the original tree 
1 10 3 6 7 2 12 
Inorder Traversal of the fixed tree 
1 2 3 6 7 10 12 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)