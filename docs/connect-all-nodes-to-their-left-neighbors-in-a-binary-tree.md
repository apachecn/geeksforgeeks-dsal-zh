# 在二叉树中将所有节点连接到它们的左邻居

> 原文:[https://www . geeksforgeeks . org/将所有节点连接到它们在二叉树中的左邻居/](https://www.geeksforgeeks.org/connect-all-nodes-to-their-left-neighbors-in-a-binary-tree/)

给定一个二叉树，其中每个节点包含一个初始为空的额外空指针。任务是使用这个额外的指针将二叉树的所有节点连接到它们在同一级别的左邻居。
**例:**

```
Input : 
       A
      / \
     B   C
    / \   \
   D   E   F
Output :
       NULL<--A
             / \
     NULL<--B<--C
           / \   \
   NULL<--D<--E<--F
```

**方法:**
我们可以在每次调用时通过节点级别来使用树的预序遍历。根节点位于级别 0。遍历时，我们将该级别最近看到的节点存储在节点指针数组中。预排序遍历确保阵列中特定级别的节点是同一级别的下一个节点的左邻居。
以下是上述方法的实施:

## C++

```
// CPP program to connect nodes
// at same level using extended
// pre-order traversal

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Binary tree node, with extra pointer leftNeighbour
// to store the neighbour to left nodes
class node {
public:
    int data;
    node* left;
    node* right;
    node* leftNeighbour;

    /* Constructor that allocates a new node with the
       given data and NULL left and right pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
        this->leftNeighbour = NULL;
    }
};

// Array to store the recent visited
// node at particular level represented
// by indices
node* a[100];

// Function to connect nodes using preorder
// traversal
void connectNodes(node* p, int l)
{
    if (p == NULL)
        return;

    // assigning left neighbor
    p->leftNeighbour = a[l];

    // updating value of the recent
    // node at level
    a[l] = p;
    connectNodes(p->left, l + 1);
    connectNodes(p->right, l + 1);
}

// Utility function to connect nodes to neighbours
// using preorder traversal
void connectNodesUtil(node* root)
{  
    // Initialize nodes at every level to NULL
    for (int i = 0; i < 100; i++)
        a[i] = NULL;

    // Populates next left pointer in all nodes
    connectNodes(root, 0);

    // Let us check the values of next left pointers
    cout << "Following are populated leftNeighbour"
            <<" pointers in the tree:\n";

    cout << "leftNeighbour of " << root->data << " is "
            << (root->leftNeighbour ?
                root->leftNeighbour->data : -1) << endl;

    cout << "leftNeighbour of " << root->left->data << " is "
            << (root->left->leftNeighbour ?
                root->left->leftNeighbour->data : -1) << endl;

    cout << "leftNeighbour of " << root->right->data << " is "
            << (root->right->leftNeighbour ?
                root->right->leftNeighbour->data : -1) << endl;

    cout << "leftNeighbour of " << root->left->left->data << " is "
            << (root->left->left->leftNeighbour ?
                root->left->left->leftNeighbour->data : -1) << endl;
}

// Driver Code
int main()
{

    /* Constructed binary tree is
            10
            / \
           8   2
          /
         3
    */
    node* root = new node(10);
    root->left = new node(8);
    root->right = new node(2);
    root->left->left = new node(3);

    connectNodesUtil(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to connect nodes
// at same level using extended
// pre-order traversal
import java.util.*;

class GFG
{

// Binary tree node, with extra pointer leftNeighbour
// to store the neighbour to left nodes
static class node
{
    int data;
    node left;
    node right;
    node leftNeighbour;

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
        this.leftNeighbour = null;
    }
}

// Array to store the recent visited
// node at particulat level represented
// by indices
static node a[] = new node[100];

// Function to connect nodes using preorder
// traversal
static void connectNodes(node p, int l)
{
    if (p == null)
        return;

    // assigning left neighbor
    p.leftNeighbour = a[l];

    // updating value of the recent
    // node at level
    a[l] = p;
    connectNodes(p.left, l + 1);
    connectNodes(p.right, l + 1);
}

// Utility function to connect nodes to neighbours
// using preorder traversal
static void connectNodesUtil(node root)
{
    // Initialize nodes at every level to null
    for (int i = 0; i < 100; i++)
        a[i] = new node(-1);

    // Populates next left pointer in all nodes
    connectNodes(root, 0);

    // Let us check the values of next left pointers
    System.out.println( "Following are populated leftNeighbour" +
                        " pointers in the tree:");

    System.out.println( "leftNeighbour of " + root.data +
                        " is " + (root.leftNeighbour != null ?
                                  root.leftNeighbour.data : -1));

    System.out.println( "leftNeighbour of " + root.left.data +
                        " is " + (root.left.leftNeighbour != null ?
                                  root.left.leftNeighbour.data : -1));

    System.out.println( "leftNeighbour of " + root.right.data +
                        " is " + (root.right.leftNeighbour != null ?
                                  root.right.leftNeighbour.data : -1) );

    System.out.println( "leftNeighbour of " + root.left.left.data +
                        " is " + (root.left.left.leftNeighbour != null ?
                                  root.left.left.leftNeighbour.data : -1));
}

// Driver Code
public static void main(String args[])
{

    /* Constructed binary tree is
            10
            / \
        8 2
        /
        3
    */
    node root = new node(10);
    root.left = new node(8);
    root.right = new node(2);
    root.left.left = new node(3);

    connectNodesUtil(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to connect nodes
# at same level using extended
# pre-order traversal

# Binary tree node, with extra
# pointer leftNeighbour to store
# the neighbour to left nodes
class node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None
        self.leftNeighbour = None

# Array to store the recent visited
# node at particulat level represented
# by indices
a = [None for i in range(100)]

# Function to connect nodes using
# preorder traversal
def connectNodes(p, l):

    if (p == None):
        return

    # assigning left neighbor
    p.leftNeighbour = a[l]

    # updating value of the
    # recent node at level
    a[l] = p
    connectNodes(p.left,
                 l + 1)
    connectNodes(p.right,
                 l + 1)

# Utility function to connect
# nodes to neighbours
# using preorder traversal
def connectNodesUtil(root):

    # Populates next left
    # pointer in all nodes
    connectNodes(root, 0)

    # Let us check the values
    # of next left pointers
    print("Following are populated" +
          "leftNeighbour pointers in" +
          "the tree:")
    x =- 1

    if root.leftNeighbour:
        x = root.leftNeighbour.data

    print("leftNeighbour of ",
          root.data, " is ", x)

    x =- 1

    if root.left.leftNeighbour:
        x = root.left.leftNeighbour.data

    print("leftNeighbour of ",
          root.left.data, " is ", x)

    x =- 1

    if root.right.leftNeighbour:
        x = root.right.leftNeighbour.data

    print("leftNeighbour of ",
          root.right.data, " is ", x)

    x =- 1

    if root.left.left.leftNeighbour:
        x = root.left.left.leftNeighbour.data

    print("leftNeighbour of ",
          root.left.left.data, " is ", x)

# Driver Code
if __name__ == '__main__':

    # /* Constructed binary tree is
    #         10
    #         / \
    #        8   2
    #       /
    #      3
    # */
    root = node(10)
    root.left = node(8)
    root.right = node(2)
    root.left.left = node(3)
    connectNodesUtil(root)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to connect nodes
// at same level using extended
// pre-order traversal
using System;

// Binary tree node, with extra pointer leftNeighbour
// to store the neighbour to left nodes
class node
{
    public int data;
    public node left;
    public node right;
    public node leftNeighbour;

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    public node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
        this.leftNeighbour = null;
    }
}
class GFG
{
    static node root;

  // Array to store the recent visited
    // node at particulat level represented
    // by indices
    static node[] a = new node[100];

    // Function to connect nodes using preorder
    // traversal
    static void connectNodes(node p, int l)
    {
        if (p == null)
        {
            return;
        }

        // assigning left neighbor
        p.leftNeighbour = a[l];

        // updating value of the recent
        // node at level
        a[l] = p;
        connectNodes(p.left, l + 1);
        connectNodes(p.right, l + 1);
    }

    // Utility function to connect nodes to neighbours
    // using preorder traversal
    static void connectNodesUtil(node root)
    {

    // Initialize nodes at every level to null
    for (int i = 0; i < 100; i++)
    {
        a[i] = new node(-1);
    }

    // Populates next left pointer in all nodes
    connectNodes(root, 0);

    // Let us check the values of next left pointers
    Console.WriteLine("Following are populated leftNeighbour" +
                      " pointers in the tree:");
    Console.WriteLine("leftNeighbour of " + root.data +
                      " is " + (root.leftNeighbour != null ?
                                root.leftNeighbour.data : -1));
    Console.WriteLine("leftNeighbour of " + root.left.data +
                      " is " + (root.left.leftNeighbour != null ?
                                root.left.leftNeighbour.data : -1));
    Console.WriteLine("leftNeighbour of " + root.right.data +
                      " is " + (root.right.leftNeighbour != null ?
                                root.right.leftNeighbour.data : -1) );
    Console.WriteLine( "leftNeighbour of " + root.left.left.data +
                      " is " + (root.left.left.leftNeighbour != null ?
                                root.left.left.leftNeighbour.data : -1));
    }

    // Driver Code
    static public void Main ()
    {

        /* Constructed binary tree is
            10
            / \
        8 2
        /
        3
    */
        GFG.root = new node(10);
        GFG.root.left = new node(8);
        GFG.root.right = new node(2);
        GFG.root.left.left = new node(3);
        connectNodesUtil(root);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to connect nodes
// at same level using extended
// pre-order traversal

// Binary tree node, with extra pointer leftNeighbour
// to store the neighbour to left nodes
class node
{

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
        this.leftNeighbour = null;
    }
}

// Array to store the recent visited
// node at particulat level represented
// by indices
let a=new Array(100);

// Function to connect nodes using preorder
// traversal
function connectNodes(p,l)
{
    if (p == null)
        return;

    // assigning left neighbor
    p.leftNeighbour = a[l];

    // updating value of the recent
    // node at level
    a[l] = p;
    connectNodes(p.left, l + 1);
    connectNodes(p.right, l + 1);
}

// Utility function to connect nodes to neighbours
// using preorder traversal
function connectNodesUtil(root)
{

    // Initialize nodes at every level to null
    for (let i = 0; i < 100; i++)
        a[i] = new node(-1);

    // Populates next left pointer in all nodes
    connectNodes(root, 0);

    // Let us check the values of next left pointers
    document.write( "Following are populated leftNeighbour" +
                        " pointers in the tree:<br>");

    document.write( "leftNeighbour of " + root.data +
                        " is " + (root.leftNeighbour != null ?
                                  root.leftNeighbour.data : -1)+"<br>");

    document.write( "leftNeighbour of " + root.left.data +
                        " is " + (root.left.leftNeighbour != null ?
                                  root.left.leftNeighbour.data : -1)+"<br>");

    document.write( "leftNeighbour of " + root.right.data +
                        " is " + (root.right.leftNeighbour != null ?
                                  root.right.leftNeighbour.data : -1) +"<br>");

    document.write( "leftNeighbour of " + root.left.left.data +
                        " is " + (root.left.left.leftNeighbour != null ?
                                  root.left.left.leftNeighbour.data : -1)+"<br>");
}

// Driver Code
/* Constructed binary tree is
            10
            / \
        8 2
        /
        3
    */
    let root = new node(10);
    root.left = new node(8);
    root.right = new node(2);
    root.left.left = new node(3);

    connectNodesUtil(root);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Following are populated leftNeighbour pointers in the tree:
leftNeighbour of 10 is -1
leftNeighbour of 8 is -1
leftNeighbour of 2 is 8
leftNeighbour of 3 is -1
```