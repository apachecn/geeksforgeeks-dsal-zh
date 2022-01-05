# 从右向左打印二叉树的所有叶节点

> 原文:[https://www . geeksforgeeks . org/print-从右向左的二叉树的所有叶节点/](https://www.geeksforgeeks.org/print-all-leaf-nodes-of-a-binary-tree-from-right-to-left/)

给定一棵二叉树，任务是从右向左打印二叉树的所有叶节点。

**示例:**

```
Input : 
       1
      /  \
     2    3
    / \  / \
   4   5 6  7
Output : 7 6 5 4

Input :
        1
       /  \
      2    3
     / \    \
    4   5    6
        /   / \
       7    8  9
Output : 9 8 7 4
```

**递归方法:**以 Preorder 方式遍历树，首先处理根，然后是右子树，然后是左子树，并执行以下操作:

*   检查根是否为空，然后从函数返回。
*   如果它是叶节点，那么打印它。
*   如果没有，则检查它是否有正确的子节点，如果有，则递归调用该节点的正确子节点的函数。
*   检查它是否有左子节点，如果有，则递归调用该节点左子节点的函数。

下面是上述方法的实现:

## C++

```
// C++ program to print leaf nodes from right to left

#include <iostream>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to print leaf
// nodes from right to left
void printLeafNodes(Node* root)
{
    // If node is null, return
    if (!root)
        return;

    // If node is leaf node, print its data
    if (!root->left && !root->right) {
        cout << root->data << " ";
        return;
    }

    // If right child exists, check for leaf
    // recursively
    if (root->right)
        printLeafNodes(root->right);

    // If left child exists, check for leaf
    // recursively
    if (root->left)
        printLeafNodes(root->left);
}

// Driver code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->right->right->left = newNode(9);
    root->left->left->left->right = newNode(10);

    printLeafNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print leaf nodes from right to left
import java.util.*;

class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to print leaf
// nodes from right to left
static void printLeafNodes(Node root)
{
    // If node is null, return
    if (root == null)
        return;

    // If node is leaf node, print its data
    if (root.left == null && root.right == null)
    {
        System.out.print( root.data +" ");
        return;
    }

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
        printLeafNodes(root.right);

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
        printLeafNodes(root.left);
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.right.right.left = newNode(9);
    root.left.left.left.right = newNode(10);

    printLeafNodes(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print
# leaf nodes from right to left

# Binary tree node
class newNode:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print leaf
# nodes from right to left
def printLeafNodes(root):

    # If node is null, return
    if root == None:
        return

    # If node is leaf node,
    # print its data
    if (root.left == None and
        root.right == None):
        print(root.data, end = " ")
        return

    # If right child exists,
    # check for leaf recursively
    if root.right:
        printLeafNodes(root.right)

    # If left child exists,
    # check for leaf recursively
    if root.left:
        printLeafNodes(root.left)

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.left = newNode(6)
root.right.right = newNode(7)
root.left.left.left = newNode(8)
root.right.right.left = newNode(9)
root.left.left.left.right = newNode(10)

printLeafNodes(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
using System;

// C# program to print leaf nodes from right to left
class GFG
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
}

// Utility function to create a new tree node
public static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to print leaf
// nodes from right to left
public static void printLeafNodes(Node root)
{
    // If node is null, return
    if (root == null)
    {
        return;
    }

    // If node is leaf node, print its data
    if (root.left == null && root.right == null)
    {
        Console.Write(root.data + " ");
        return;
    }

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
    {
        printLeafNodes(root.right);
    }

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
    {
        printLeafNodes(root.left);
    }
}

// Driver code
public static void Main(string[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.right.right.left = newNode(9);
    root.left.left.left.right = newNode(10);

    printLeafNodes(root);
}
}

// This code is contributed by shrikanth13
```

## java 描述语言

```
<script>

// JavaScript program to print leaf nodes from right to left

// A Binary Tree Node
class Node
{
    constructor()
    {
        this.data = 0;
        this.right = null;
        this.left = null;
    }
}

// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to print leaf
// nodes from right to left
function printLeafNodes(root)
{
    // If node is null, return
    if (root == null)
    {
        return;
    }

    // If node is leaf node, print its data
    if (root.left == null && root.right == null)
    {
        document.write(root.data + " ");
        return;
    }

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
    {
        printLeafNodes(root.right);
    }

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
    {
        printLeafNodes(root.left);
    }
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);
root.left.left.left = newNode(8);
root.right.right.left = newNode(9);
root.left.left.left.right = newNode(10);
printLeafNodes(root);

</script>
```

**Output:** 

```
9 6 5 10
```

**迭代方式:**思路是使用一个栈执行迭代的后序遍历，但是以修改的方式，首先我们会访问右子树，然后是左子树，最后是根节点，打印叶节点。

下面是上述方法的实现:

## C++

```
// C++ program to print leaf nodes from
// right to left using one stack

#include<bits/stdc++.h>
using namespace std;

// Structure of binary tree
struct Node {
    Node* left;
    Node* right;
    int data;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* node = new Node();
    node->left = node->right = NULL;
    node->data = key;
    return node;
}

// Function to Print all the leaf nodes
// of Binary tree using one stack
void printLeafRightToLeft(Node* p)
{
    // stack to store the nodes
    stack<Node*> s;

    while (1) {
        // If p is not null then push
        // it on the stack
        if (p) {
            s.push(p);
            p = p->right;
        }

        else {
            // If stack is empty then come out
            // of the loop
            if (s.empty())
                break;
            else {
                // If the node on top of the stack has its
                // left subtree as null then pop that node and
                // print the node only if its right
                // subtree is also null
                if (s.top()->left == NULL) {
                    p = s.top();
                    s.pop();

                    // Print the leaf node
                    if (p->right == NULL)
                        printf("%d ", p->data);
                }

                while (p == s.top()->left) {
                    p = s.top();
                    s.pop();

                    if (s.empty())
                        break;
                }

                // If stack is not empty then assign p as
                // the stack's top node's left child
                if (!s.empty())
                    p = s.top()->left;
                else
                    p = NULL;
            }
        }
    }
}

// Driver Code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    printLeafRightToLeft(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print leaf nodes from
// right to left using one stack
import java.util.Stack;

class GFG
{

    // Structure of binary tree
    static class Node
    {
        Node left;
        Node right;
        int data;
    };

    // Function to create a new node
    static Node newNode(int key)
    {
        Node node = new Node();
        node.left = node.right = null;
        node.data = key;
        return node;
    }

    // Function to Print all the leaf nodes
    // of Binary tree using one stack
    static void printLeafRightToLeft(Node p)
    {
        // stack to store the nodes
        Stack<Node> s = new Stack<>();

        while (true)
        {
            // If p is not null then push
            // it on the stack
            if (p != null)
            {
                s.push(p);
                p = p.right;
            }

            else
            {
                // If stack is empty then come out
                // of the loop
                if (s.empty())
                    break;
                else
                {
                    // If the node on top of the stack has its
                    // left subtree as null then pop that node and
                    // print the node only if its right
                    // subtree is also null
                    if (s.peek().left == null)
                    {
                        p = s.peek();
                        s.pop();

                        // Print the leaf node
                        if (p.right == null)
                            System.out.print( p.data+" ");
                    }

                    while (p == s.peek().left)
                    {
                        p = s.peek();
                        s.pop();

                        if (s.empty())
                            break;
                    }

                    // If stack is not empty then assign p as
                    // the stack's top node's left child
                    if (!s.empty())
                        p = s.peek().left;
                    else
                        p = null;
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);

        printLeafRightToLeft(root);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print leaf nodes 
# from right to left using one stack

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to create a new node
def newNode(key) :

    node = Node(0)
    node.left = node.right = None
    node.data = key
    return node

# Function to Print all the leaf nodes
# of Binary tree using one stack
def printLeafRightToLeft(p) :

    # stack to store the nodes
    s = []

    while (True) :

        # If p is not None then append
        # it on the stack
        if (p != None) :
            s.append(p)
            p = p.right

        else:

            # If stack is len then come out
            # of the loop
            if (len(s) == 0) :
                break
            else:

                # If the node on top of the stack has
                # its left subtree as None then pop 
                # that node and print the node only
                # if its right subtree is also None
                if (s[-1].left == None) :

                    p = s[-1]
                    s.pop()

                    # Print the leaf node
                    if (p.right == None) :
                        print( p.data, end = " ")

                while (p == s[-1].left) :

                    p = s[-1]
                    s.pop()

                    if (len(s) == 0) :
                        break

                # If stack is not len then assign p as
                # the stack's top node's left child
                if (len(s) > 0) :
                    p = s[-1].left
                else:
                    p = None

# Driver Code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.left = newNode(6)
root.right.right = newNode(7)

printLeafRightToLeft(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to print leaf nodes from
// right to left using one stack
using System;
using System.Collections.Generic;

class GFG
{

    // Structure of binary tree
    public class Node
    {
        public Node left;
        public Node right;
        public int data;
    };

    // Function to create a new node
    static Node newNode(int key)
    {
        Node node = new Node();
        node.left = node.right = null;
        node.data = key;
        return node;
    }

    // Function to Print all the leaf nodes
    // of Binary tree using one stack
    static void printLeafRightToLeft(Node p)
    {
        // stack to store the nodes
        Stack<Node> s = new Stack<Node>();

        while (true)
        {
            // If p is not null then push
            // it on the stack
            if (p != null)
            {
                s.Push(p);
                p = p.right;
            }

            else
            {
                // If stack is empty then come out
                // of the loop
                if (s.Count == 0)
                    break;
                else
                {
                    // If the node on top of the stack has its
                    // left subtree as null then pop that node and
                    // print the node only if its right
                    // subtree is also null
                    if (s.Peek().left == null)
                    {
                        p = s.Peek();
                        s.Pop();

                        // Print the leaf node
                        if (p.right == null)
                            Console.Write(p.data + " ");
                    }

                    while (p == s.Peek().left)
                    {
                        p = s.Peek();
                        s.Pop();

                        if (s.Count == 0)
                            break;
                    }

                    // If stack is not empty then assign p as
                    // the stack's top node's left child
                    if (s.Count != 0)
                        p = s.Peek().left;
                    else
                        p = null;
                }
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);

        printLeafRightToLeft(root);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to print leaf nodes from
// right to left using one stack

// Structure of binary tree
class Node
{
    constructor()
    {
        this.left = null;
        this.right = null;
        this.data = 0;
    }
};

// Function to create a new node
function newNode(key)
{
    var node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

// Function to Print all the leaf nodes
// of Binary tree using one stack
function printLeafRightToLeft(p)
{

    // Stack to store the nodes
    var s = [];

    while (true)
    {

        // If p is not null then push
        // it on the stack
        if (p != null)
        {
            s.push(p);
            p = p.right;
        }
        else
        {

            // If stack is empty then come out
            // of the loop
            if (s.length == 0)
                break;
            else
            {

                // If the node on top of the stack has
                // its left subtree as null then pop
                // that node and print the node only
                // if its right subtree is also null
                if (s[s.length - 1].left == null)
                {
                    p = s[s.length - 1];
                    s.pop();

                    // Print the leaf node
                    if (p.right == null)
                        document.write(p.data + " ");
                }
                while (p == s[s.length - 1].left)
                {
                    p = s[s.length - 1];
                    s.pop();

                    if (s.length == 0)
                        break;
                }

                // If stack is not empty then assign p as
                // the stack's top node's left child
                if (s.length != 0)
                    p = s[s.length - 1].left;
                else
                    p = null;
            }
        }
    }
}

// Driver Code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);

printLeafRightToLeft(root);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
7 6 5 4
```

**时间复杂度** : O(N)，其中 N 为二叉树中的节点总数。
**辅助空间:** O(N)