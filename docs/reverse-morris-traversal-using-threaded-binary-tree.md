# 使用线程二叉树进行反向莫里斯遍历

> 原文:[https://www . geesforgeks . org/reverse-Morris-遍历-使用-线程-二叉树/](https://www.geeksforgeeks.org/reverse-morris-traversal-using-threaded-binary-tree/)

给定一棵二叉树，任务是使用莫里斯遍历进行反向有序遍历。

![TBT](img/138d357bc0f4ad58ca70f4062501ccdb.png)

**先决条件:**
[莫里斯遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)
[线程二叉树](https://www.geeksforgeeks.org/threaded-binary-tree/)

在具有 **n** 个节点的二叉树中，存在浪费内存的 **n + 1** 个空指针。因此，线程二叉树利用这些空指针来节省大量内存。
所以，在 [**线程二叉树**](https://www.geeksforgeeks.org/threaded-binary-tree/) 中，这些空指针会存储一些有用的信息。

1)仅在空左指针中存储前置信息，称为左线程二叉树。
2)仅在空右指针中存储后继信息，称为右线程二叉树。
3)将前置信息存储在空左指针中，将后续信息存储在空右指针中，称为全线程二叉树或简单线程二叉树。

[Morris 遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)可以用来做 order 遍历、reverse Inorder 遍历、Pre-order 遍历，用不变的额外内存消耗 O(1)。

**反向莫里斯遍历:**简直就是莫里斯遍历的反向形式。在反向 Morris 遍历中，首先创建到当前节点的有序后继节点的链接，并使用这些链接打印数据，最后恢复更改以恢复原始树，这将给出反向有序遍历。

**算法:**

```
1) Initialize Current as root.

2) While current is not NULL :

  2.1) If current has no right child
   a) Visit the current node.
   b) Move to the left child of current.

  2.2) Else, here we have 2 cases:
   a) Find the inorder successor of current node. 
      Inorder successor is the left most node 
      in the right subtree or right child itself.
   b) If the left child of the inorder successor is NULL:
      1) Set current as the left child of its inorder successor.
      2) Move current node to its right.
   c) Else, if the threaded link between the current node 
      and it's inorder successor already exists :
      1) Set left pointer of the inorder successor as NULL.
      2) Visit Current node.
      3) Move current to it's left child.
```

## C++

```
// CPP code for reverse Morris Traversal
#include<bits/stdc++.h>

using namespace std;

// Node structure
struct Node {
    int data;
    Node *left, *right;
};

// helper function to create a new node
Node *newNode(int data){
    Node *temp = new Node;

    temp->data = data;
    temp->right = temp->left = NULL;

    return temp;
}

// function for reverse inorder traversal
void MorrisReverseInorder(Node *root)
{

    if(!root)
        return ;

    // Auxiliary node pointers
    Node *curr, *successor;

    // initialize current as root
    curr = root;

    while(curr)
    {
        // case-1, if curr has no right child then
        // visit current and move to left child
        if(curr -> right == NULL)
        {
            cout << curr->data << " ";
            curr = curr->left;
        }

        // case-2
        else
        {
            // find the inorder successor of
            // current node i.e left most node in
            // right subtree or right child itself
            successor = curr->right;

            // finding left most in right subtree
            while(successor->left != NULL &&
                  successor->left != curr)
                    successor = successor->left;

            // if the left of inorder successor is NULL
            if(successor->left == NULL)
            {
                // then connect left link to current node
                successor->left = curr;

                // move current to right child
                curr = curr->right;
            }

            // otherwise inorder successor's left is
            // not NULL and already left is linked
            // with current node
            else
            {
                successor->left = NULL;

                // visiting the current node
                cout << curr->data << " ";

                // move current to its left child
                curr = curr->left;
            }
        }
    }
}

// Driver code
int main()
{

/* Constructed binary tree is
          1
        /   \
       2     3
     /  \   /  \
    4    5  6    7
*/

Node *root = newNode(1);
root->left = newNode(2);
root->right = newNode(3);
root->left->left = newNode(4);
root->left->right = newNode(5);
root->right->left = newNode(6);
root->right->right = newNode(7);

//reverse inorder traversal.
MorrisReverseInorder(root);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for reverse Morris Traversal
class GFG
{

// Node structure
static class Node
{
    int data;
    Node left, right;
};

// helper function to create a new node
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.right = temp.left = null;

    return temp;
}

// function for reverse inorder traversal
static void MorrisReverseInorder(Node root)
{

    if(root == null)
        return ;

    // Auxiliary node pointers
    Node curr, successor;

    // initialize current as root
    curr = root;

    while(curr != null)
    {
        // case-1, if curr has no right child then
        // visit current and move to left child
        if(curr . right == null)
        {
                System.out.print( curr.data + " ");
            curr = curr.left;
        }

        // case-2
        else
        {
            // find the inorder successor of
            // current node i.e left most node in
            // right subtree or right child itself
            successor = curr.right;

            // finding left most in right subtree
            while(successor.left != null &&
                successor.left != curr)
                    successor = successor.left;

            // if the left of inorder successor is null
            if(successor.left == null)
            {
                // then connect left link to current node
                successor.left = curr;

                // move current to right child
                curr = curr.right;
            }

            // otherwise inorder successor's left is
            // not null and already left is linked
            // with current node
            else
            {
                successor.left = null;

                // visiting the current node
                System.out.print( curr.data + " ");

                // move current to its left child
                curr = curr.left;
            }
        }
    }
}

// Driver code
public static void main(String args[])
{

/* Constructed binary tree is
        1
        / \
    2     3
    / \ / \
    4 5 6 7
*/

Node root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);

// reverse inorder traversal.
MorrisReverseInorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 for reverse Morris Traversal

# Utility function to create a new
# tree node
class newNode:
    def __init__(self,data):
        self.data = data
        self.left = self.right = None

# function for reverse inorder traversal
def MorrisReverseInorder(root):

    if( not root) :
        return

    # initialize current as root
    curr = root
    successor = 0

    while(curr):

        # case-1, if curr has no right child then
        # visit current and move to left child
        if(curr.right == None) :

            print(curr.data, end = " ")
            curr = curr.left

        # case-2
        else:

            # find the inorder successor of
            # current node i.e left most node in
            # right subtree or right child itself
            successor = curr.right

            # finding left most in right subtree
            while(successor.left != None and
                  successor.left != curr):
                successor = successor.left

            # if the left of inorder successor is None
            if(successor.left == None) :

                # then connect left link to current node
                successor.left = curr

                # move current to right child
                curr = curr.right

            # otherwise inorder successor's left is
            # not None and already left is linked
            # with current node
            else:

                successor.left = None

                # visiting the current node
                print(curr.data, end = " " )

                # move current to its left child
                curr = curr.left

# Driver code
if __name__ =="__main__":
    """ Constructed binary tree is
        1
        / \
    2     3
    / \ / \
    4 5 6 7
"""

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)

    #reverse inorder traversal.
    MorrisReverseInorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# code for reverse Morris Traversal
using System;

class GFG
{

// Node structure
public class Node
{
    public int data;
    public Node left, right;
};

// helper function to create a new node
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.right = temp.left = null;

    return temp;
}

// function for reverse inorder traversal
static void MorrisReverseInorder(Node root)
{

    if(root == null)
        return ;

    // Auxiliary node pointers
    Node curr, successor;

    // initialize current as root
    curr = root;

    while(curr != null)
    {
        // case-1, if curr has no right child then
        // visit current and move to left child
        if(curr . right == null)
        {
                Console.Write( curr.data + " ");
            curr = curr.left;
        }

        // case-2
        else
        {
            // find the inorder successor of
            // current node i.e left most node in
            // right subtree or right child itself
            successor = curr.right;

            // finding left most in right subtree
            while(successor.left != null &&
                successor.left != curr)
                    successor = successor.left;

            // if the left of inorder successor is null
            if(successor.left == null)
            {
                // then connect left link to current node
                successor.left = curr;

                // move current to right child
                curr = curr.right;
            }

            // otherwise inorder successor's left is
            // not null and already left is linked
            // with current node
            else
            {
                successor.left = null;

                // visiting the current node
                Console.Write( curr.data + " ");

                // move current to its left child
                curr = curr.left;
            }
        }
    }
}

// Driver code
public static void Main(String []args)
{

/* Constructed binary tree is
        1
        / \
    2 3
    / \ / \
    4 5 6 7
*/

Node root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);

// reverse inorder traversal.
MorrisReverseInorder(root);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript code for reverse Morris Traversal

// Node structure
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Helper function to create a new node
function  newNode(data)
{
    var temp = new Node();

    temp.data = data;
    temp.right = temp.left = null;

    return temp;
}

// Function for reverse inorder traversal
function MorrisReverseInorder(root)
{
    if (root == null)
        return;

    // Auxiliary node pointers
    var curr, successor;

    // Initialize current as root
    curr = root;

    while (curr != null)
    {

        // case-1, if curr has no right child then
        // visit current and move to left child
        if (curr . right == null)
        {
            document.write( curr.data + " ");
            curr = curr.left;
        }

        // case-2
        else
        {

            // Find the inorder successor of
            // current node i.e left most node in
            // right subtree or right child itself
            successor = curr.right;

            // Finding left most in right subtree
            while(successor.left != null &&
                  successor.left != curr)
                successor = successor.left;

            // If the left of inorder successor is null
            if (successor.left == null)
            {

                // Then connect left link to current node
                successor.left = curr;

                // Move current to right child
                curr = curr.right;
            }

            // Otherwise inorder successor's left is
            // not null and already left is linked
            // with current node
            else
            {
                successor.left = null;

                // Visiting the current node
                document.write( curr.data + " ");

                // Move current to its left child
                curr = curr.left;
            }
        }
    }
}

// Driver code
/* Constructed binary tree is
         1
        / \
       2   3
      / \ / \
     4  5 6  7
*/
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);

// Reverse inorder traversal.
MorrisReverseInorder(root);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
7 3 6 1 5 2 4
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)