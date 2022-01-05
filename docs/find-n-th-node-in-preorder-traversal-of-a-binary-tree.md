# 在二叉树的前序遍历中找到第 n 个节点

> 原文:[https://www . geeksforgeeks . org/find-n-th-node-in-preorder-遍历二叉树/](https://www.geeksforgeeks.org/find-n-th-node-in-preorder-traversal-of-a-binary-tree/)

给定一棵二叉树和一个数字 N，编写一个程序，在给定二叉树的 Preorder 遍历中找到第 N 个节点。
**先决条件:** [树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
**示例:**

```
Input:      N = 4
              11
            /   \
           21    31
         /   \
        41     51
Output: 51
Explanation: Preorder Traversal of given Binary Tree is 11 21 41 51 31, 
so 4th node will be 51.

Input:      N = 5
             25
           /    \
          20    30
        /    \ /   \
      18    22 24   32
Output: 30
```

解决这个问题的思路是对给定的二叉树进行[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并在遍历该树时跟踪访问的节点数，当该数等于 n 时打印当前节点

## C++

```
// C++ program to find n-th node of
// Preorder Traversal of Binary Tree
#include <bits/stdc++.h>
using namespace std;

// Tree node
struct Node {
    int data;
    Node *left, *right;
};

// function to create new node
struct Node* createNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// function to find the N-th node in the preorder
// traversal of a given binary tree
void NthPreordernode(struct Node* root, int N)
{
    static int flag = 0;

    if (root == NULL)
        return;

    if (flag <= N) {
        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            cout << root->data;

        // left recursion
        NthPreordernode(root->left, N);

        // right recursion
        NthPreordernode(root->right, N);
    }
}

// Driver code
int main()
{
    // construction of binary tree
    struct Node* root = createNode(25);
    root->left = createNode(20);
    root->right = createNode(30);
    root->left->left = createNode(18);
    root->left->right = createNode(22);
    root->right->left = createNode(24);
    root->right->right = createNode(32);

    // nth node
    int N = 6;

    // prints n-th found found
    NthPreordernode(root, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th node of
// Preorder Traversal of Binary Tree
class GFG
{

// Tree node
static class Node
{
    int data;
    Node left, right;
};

// function to create new node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}
static int flag = 0;

// function to find the N-th node in the preorder
// traversal of a given binary tree
static void NthPreordernode(Node root, int N)
{

    if (root == null)
        return;

    if (flag <= N)
    {
        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            System.out.print( root.data);

        // left recursion
        NthPreordernode(root.left, N);

        // right recursion
        NthPreordernode(root.right, N);
    }
}

// Driver code
public static void main(String args[])
{
    // construction of binary tree
    Node root = createNode(25);
    root.left = createNode(20);
    root.right = createNode(30);
    root.left.left = createNode(18);
    root.left.right = createNode(22);
    root.right.left = createNode(24);
    root.right.right = createNode(32);

    // nth node
    int N = 6;

    // prints n-th found found
    NthPreordernode(root, N);
}
}

// This code contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to find n-th node of
# Preorder Traversal of Binary Tree

class createNode():

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to find the N-th node in the preorder
# traversal of a given binary tree
flag = [0]
def NthPreordernode(root, N):
    if (root == None):
        return

    if (flag[0] <= N):
        flag[0] += 1

        # prints the n-th node of preorder traversal
        if (flag[0] == N):
            print(root.data)

        # left recursion
        NthPreordernode(root.left, N)

        # right recursion
        NthPreordernode(root.right, N)

# Driver code
if __name__ == '__main__':

    # construction of binary tree
    root = createNode(25)
    root.left = createNode(20)
    root.right = createNode(30)
    root.left.left = createNode(18)
    root.left.right = createNode(22)
    root.right.left = createNode(24)
    root.right.right = createNode(32)

    # nth node
    N = 6

    # prints n-th found found
    NthPreordernode(root, N)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find n-th node of
// Preorder Traversal of Binary Tree
using System;

class GFG
{

// Tree node
public class Node
{
    public int data;
    public Node left, right;
};

// function to create new node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}
static int flag = 0;

// function to find the N-th node in the preorder
// traversal of a given binary tree
static void NthPreordernode(Node root, int N)
{

    if (root == null)
        return;

    if (flag <= N)
    {
        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            Console.Write( root.data);

        // left recursion
        NthPreordernode(root.left, N);

        // right recursion
        NthPreordernode(root.right, N);
    }
}

// Driver code
public static void Main(String []args)
{
    // construction of binary tree
    Node root = createNode(25);
    root.left = createNode(20);
    root.right = createNode(30);
    root.left.left = createNode(18);
    root.left.right = createNode(22);
    root.right.left = createNode(24);
    root.right.right = createNode(32);

    // nth node
    int N = 6;

    // prints n-th found found
    NthPreordernode(root, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find n-th node of
// Preorder Traversal of Binary Tree

// Tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// function to create new node
function createNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;

    return temp;
}

var flag = 0;

// function to find the N-th node in the preorder
// traversal of a given binary tree
function NthPreordernode(root, N)
{

    if (root == null)
        return;

    if (flag <= N)
    {
        flag++;

        // prints the n-th node of preorder traversal
        if (flag == N)
            document.write( root.data);

        // left recursion
        NthPreordernode(root.left, N);

        // right recursion
        NthPreordernode(root.right, N);
    }
}

// Driver code
// construction of binary tree
var root = createNode(25);
root.left = createNode(20);
root.right = createNode(30);
root.left.left = createNode(18);
root.left.right = createNode(22);
root.right.left = createNode(24);
root.right.right = createNode(32);

// nth node
var N = 6;

// prints n-th found found
NthPreordernode(root, N);

// This code is contributed by famously.
</script>
```

**Output:** 

```
24
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。
**辅助空间:** O(1)