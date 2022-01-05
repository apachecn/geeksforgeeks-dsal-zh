# 寻找有序遍历的第 n 个节点

> 原文:[https://www . geesforgeks . org/find-n-th-node-in order-traversation/](https://www.geeksforgeeks.org/find-n-th-node-inorder-traversal/)

给定二叉树，你必须找出[的第 n 个节点，以便遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

**例:**

```
Input : n = 4
              10
            /   \
           20     30
         /   \
        40     50
Output : 10
Inorder Traversal is : 40 20 50 10 30

Input :  n = 3
            7
          /   \
         2     3
             /   \
            8     5
Output : 8
Inorder: 2 7 8 3 5
3th node is 8
```

我们做简单的有序遍历。在遍历时，我们会记录到目前为止访问的节点数。当计数变为 n 时，我们打印节点。

下面是上述方法的实现。

## C

```
// C program for  nth nodes of  inorder traversals
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node =
          (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

/* Given a binary tree, print its nth nodes of inorder*/
void NthInorder(struct Node* node, int n)
{
    static int count = 0;
    if (node == NULL)
        return;

    if (count <= n) {

        /* first recur on left child */
        NthInorder(node->left, n);
        count++;

        // when count = n then print element
        if (count == n)
            printf("%d ", node->data);

        /* now recur on right child */
        NthInorder(node->right, n);
    }
}

/* Driver program to test above functions*/
int main()
{
    struct Node* root = newNode(10);
    root->left = newNode(20);
    root->right = newNode(30);
    root->left->left = newNode(40);
    root->left->right = newNode(50);

    int n = 4;

    NthInorder(root, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for  nth nodes of  inorder traversals

import java.util. *;

class Solution
{
static int count =0; 
/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node {
    int data;
     Node left;
     Node right;
}

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
 static Node newNode(int data)
{
     Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Given a binary tree, print its nth nodes of inorder*/
static void NthInorder( Node node, int n)
{ 
    if (node == null)
        return;

    if (count <= n) {
        /* first recur on left child */
        NthInorder(node.left, n);
        count++;

        // when count = n then print element
        if (count == n)
            System.out.printf("%d ", node.data);

        /* now recur on right child */
        NthInorder(node.right, n);
    }
}

/* Driver program to test above functions*/
public static void main(String args[])
{
     Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.left = newNode(40);
    root.left.right = newNode(50);

    int n = 4;

    NthInorder(root, n);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
"""Python3 program for nth node of
   inorder traversal"""

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.visited = False

count = [0]

""" Given a binary tree, print the nth
    node of inorder traversal"""
def NthInorder(node, n):

    if (node == None):
        return

    if (count[0] <= n):

        """ first recur on left child """
        NthInorder(node.left, n)
        count[0] += 1

        # when count = n then prelement
        if (count[0] == n):
            print(node.data, end = " ")

        """ now recur on right child """
        NthInorder(node.right, n)

# Driver Code
if __name__ == '__main__':

    root = newNode(10)
    root.left = newNode(20)
    root.right = newNode(30)
    root.left.left = newNode(40)
    root.left.right = newNode(50)

    n = 4

    NthInorder(root, n)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program for nth nodes of
// inorder traversals
using System;

class GFG
{
public static int count = 0;

/* A binary tree node has data, pointer
to left child and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
}

/* Helper function that allocates a
new node with the given data and null
left and right pointers. */
public static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Given a binary tree, print its
nth nodes of inorder*/
public static void NthInorder(Node node, int n)
{
    if (node == null)
    {
        return;
    }

    if (count <= n)
    {
        /* first recur on left child */
        NthInorder(node.left, n);
        count++;

        // when count = n then print element
        if (count == n)
        {
            Console.Write("{0:D} ", node.data);
        }

        /* now recur on right child */
        NthInorder(node.right, n);
    }
}

// Driver Code
public static void Main(string[] args)
{
    Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.left = newNode(40);
    root.left.right = newNode(50);

    int n = 4;

    NthInorder(root, n);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program for  nth nodes of  inorder traversals

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
    }
}

let count =0; 

/* Given a binary tree, print its nth nodes of inorder*/
function NthInorder(node,n)
{
    if (node == null)
        return;

    if (count <= n) {
        /* first recur on left child */
        NthInorder(node.left, n);
        count++;

        // when count = n then print element
        if (count == n)
            document.write(node.data+" ");

        /* now recur on right child */
        NthInorder(node.right, n);
    }
}

/* Driver program to test above functions*/
let  root = new Node(10);
root.left = new Node(20);
root.right = new Node(30);
root.left.left = new Node(40);
root.left.right = new Node(50);

let n = 4;

NthInorder(root, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
10
```

**时间复杂度:** O(n)