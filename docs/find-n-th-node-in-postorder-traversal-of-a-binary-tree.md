# 求二叉树后序遍历的第 n 个节点

> 原文:[https://www . geeksforgeeks . org/find-n-th-节点后序遍历二叉树/](https://www.geeksforgeeks.org/find-n-th-node-in-postorder-traversal-of-a-binary-tree/)

给定一棵二叉树和一个数字 N，编写一个程序，在给定二叉树的后序遍历中找到第 N 个节点。
**先决条件** : [树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
**示例:**

```
Input : N = 4
              11
            /   \
           21    31
         /   \
        41     51
Output : 31
Explanation: Postorder Traversal of given Binary Tree is 41 51 21 31 11, 
so 4th node will be 31.

Input : N = 5
             25
           /    \
          20    30
        /    \ /   \
      18    22 24   32
Output : 32
```

解决这个问题的思路是对给定的二叉树进行[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，在遍历树的同时跟踪访问的节点数，当计数变为 n 时打印当前节点
以下是上述方法的实现:

## C++

```
// C++ program to find n-th node of
// Postorder Traversal of Binary Tree
#include <bits/stdc++.h>
using namespace std;

// node of tree
struct Node {
    int data;
    Node *left, *right;
};

// function to create a new node
struct Node* createNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// function to find the N-th node in the postorder
// traversal of a given binary tree
void NthPostordernode(struct Node* root, int N)
{
    static int flag = 0;

    if (root == NULL)
        return;

    if (flag <= N) {

        // left recursion
        NthPostordernode(root->left, N);

        // right recursion
        NthPostordernode(root->right, N);

        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            cout << root->data;
    }
}

// driver code
int main()
{
    struct Node* root = createNode(25);
    root->left = createNode(20);
    root->right = createNode(30);
    root->left->left = createNode(18);
    root->left->right = createNode(22);
    root->right->left = createNode(24);
    root->right->right = createNode(32);

    int N = 6;

    // prints n-th node found
    NthPostordernode(root, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th node of
// Postorder Traversal of Binary Tree
public class NthNodePostOrder {

    static int flag = 0;

    // function to find the N-th node in the postorder
    // traversal of a given binary tree
    public static void NthPostordernode(Node root, int N)
    {

        if (root == null)
            return;

        if (flag <= N)
        {  
            // left recursion
            NthPostordernode(root.left, N);
            // right recursion
            NthPostordernode(root.right, N);
            flag++;
            // prints the n-th node of preorder traversal
            if (flag == N)
                System.out.print(root.data);
        }
    }

    public static void main(String args[]) {
        Node root = new Node(25);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(18);
        root.left.right = new Node(22);
        root.right.left = new Node(24);
        root.right.right = new Node(32);

        int N = 6;

        // prints n-th node found
        NthPostordernode(root, N);
    }
}

/* A binary tree node structure */
class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        this.data=data;
    }
};
// This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
"""Python3 program to find n-th node of
Postorder Traversal of Binary Tree"""

# A Binary Tree Node
# Utility function to create a new tree node
class createNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data= data
        self.left = None
        self.right = None

# function to find the N-th node
# in the postorder traversal of
# a given binary tree
flag = [0]
def NthPostordernode(root, N):

    if (root == None):
        return

    if (flag[0] <= N[0]):

        # left recursion
        NthPostordernode(root.left, N)

        # right recursion
        NthPostordernode(root.right, N)

        flag[0] += 1

        # prints the n-th node of
        # preorder traversal
        if (flag[0] == N[0]):
            print(root.data)

# Driver Code
if __name__ == '__main__':
    root = createNode(25)
    root.left = createNode(20)
    root.right = createNode(30)
    root.left.left = createNode(18)
    root.left.right = createNode(22)
    root.right.left = createNode(24)
    root.right.right = createNode(32)

    N = [6]

    # prints n-th node found
    NthPostordernode(root, N)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find n-th node of
// Postorder Traversal of Binary Tree
using System;

public class NthNodePostOrder
{

    /* A binary tree node structure */
    public class Node
    {
        public int data;
        public Node left, right;
        public Node(int data)
        {
            this.data=data;
        }
    }
    static int flag = 0;

    // function to find the N-th node in the postorder
    // traversal of a given binary tree
    static void NthPostordernode(Node root, int N)
    {
        if (root == null)
            return;

        if (flag <= N)
        {
            // left recursion
            NthPostordernode(root.left, N);

            // right recursion
            NthPostordernode(root.right, N);
            flag++;

            // prints the n-th node of preorder traversal
            if (flag == N)
                Console.Write(root.data);
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        Node root = new Node(25);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(18);
        root.left.right = new Node(22);
        root.right.left = new Node(24);
        root.right.right = new Node(32);

        int N = 6;

        // prints n-th node found
        NthPostordernode(root, N);
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to find n-th node of
// Postorder Traversal of Binary Tree
/* A binary tree node structure */
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

var flag = 0;
// function to find the N-th node in the postorder
// traversal of a given binary tree
function NthPostordernode(root, N)
{
    if (root == null)
        return;

    if (flag <= N)
    {
        // left recursion
        NthPostordernode(root.left, N);

        // right recursion
        NthPostordernode(root.right, N);
        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            document.write(root.data);
    }
}

// Driver code
var root = new Node(25);
root.left = new Node(20);
root.right = new Node(30);
root.left.left = new Node(18);
root.left.right = new Node(22);
root.right.left = new Node(24);
root.right.right = new Node(32);
var N = 6;
// prints n-th node found
NthPostordernode(root, N);

</script>
```

**Output:** 

```
30
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。
**辅助空间:** O(1)