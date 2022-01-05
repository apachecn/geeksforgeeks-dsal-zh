# 使用一个堆栈从左到右打印二叉树中的叶节点

> 原文:[https://www . geesforgeks . org/print-leaf-nodes-in-二叉树-从左到右-使用一个堆栈/](https://www.geeksforgeeks.org/print-leaf-nodes-in-binary-tree-from-left-to-right-using-one-stack/)

给定一棵二叉树，任务是从左到右打印给定二叉树的所有叶节点。也就是说，节点应该按照它们在给定树中从左到右的顺序打印。
**例:**

```
Input : 
           1
          /  \
         2    3
        / \  / \
       4  5  6  7
Output : 4 5 6 7

Input :
            4
           /  \
          5    9
         / \  / \
        8   3 7  2
       /         / \
      12        6   1
Output : 12 3 7 6 1
```

我们已经讨论了使用两个堆栈的[迭代](https://www.geeksforgeeks.org/print-all-leaf-nodes-of-a-binary-tree-from-left-to-right-set-2-iterative-approach/)方法。
**方法:**想法是使用一个堆栈执行迭代[后序遍历并打印叶节点。
以下是上述方法的实施:](https://www.geeksforgeeks.org/iterative-postorder-traversal-using-stack/) 

## C++

```
// C++ program to print leaf nodes from
// left to right using one stack
#include <bits/stdc++.h>
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
void printLeafLeftToRight(Node* p)
{
    // stack to store the nodes
    stack<Node*> s;

    while (1) {
        // If p is not null then push
        // it on the stack
        if (p) {
            s.push(p);
            p = p->left;
        }

        else {
            // If stack is empty then come out
            // of the loop
            if (s.empty())
                break;
            else {
                // If the node on top of the stack has its
                // right subtree as null then pop that node and
                // print the node only if its left
                // subtree is also null
                if (s.top()->right == NULL) {
                    p = s.top();
                    s.pop();

                    // Print the leaf node
                    if (p->left == NULL)
                        printf("%d ", p->data);
                }

                while (p == s.top()->right) {
                    p = s.top();
                    s.pop();

                    if (s.empty())
                        break;
                }

                // If stack is not empty then assign p as
                // the stack's top node's right child
                if (!s.empty())
                    p = s.top()->right;
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

    printLeafLeftToRight(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print leaf nodes from
// left to{ right using one stack
import java.util.*;
class GfG
{

// Structure of binary tree
static class Node
{
    Node left;
    Node right;
    int data;
}

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.data = key;
    return node;
}

// Function to Print all the leaf nodes
// of Binary tree using one stack
static void printLeafLeftToRight(Node p)
{
    // stack to store the nodes
    Stack<Node> s = new Stack<Node> ();

    while (true)
    {
        // If p is not null then push
        // it on the stack
        if (p != null)
        {
            s.push(p);
            p = p.left;
        }

        else
        {
            // If stack is empty then come out
            // of the loop
            if (s.isEmpty())
                break;
            else
            {
                // If the node on top of the stack has its
                // right subtree as null then pop that node and
                // print the node only if its left
                // subtree is also null
                if (s.peek().right == null)
                {
                    p = s.peek();
                    s.pop();

                    // Print the leaf node
                    if (p.left == null)
                        System.out.print(p.data + " ");
                }

                while (p == s.peek().right)
                {
                    p = s.peek();
                    s.pop();

                    if (s.isEmpty())
                        break;
                }

                // If stack is not empty then assign p as
                // the stack's top node's right child
                if (!s.isEmpty())
                    p = s.peek().right;
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

    printLeafLeftToRight(root);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to print leaf nodes from
# left to right using one stack

# Binary tree node
class newNode:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to Print all the leaf nodes
# of Binary tree using one stack
def printLeafLeftToRight(p):

    # stack to store the nodes
    s = []
    while (1):

        # If p is not None then push
        # it on the stack
        if (p):
            s.insert(0, p)
            p = p.left

        else:

            # If stack is empty then come out
            # of the loop
            if len(s) == 0:
                break

            else:

                # If the node on top of the stack has its
                # right subtree as None then pop that node
                # and print the node only if its left
                # subtree is also None
                if (s[0].right == None):
                    p = s[0]
                    s.pop(0)

                    # Print the leaf node
                    if (p.left == None):
                        print(p.data, end = " ")

                while (p == s[0].right):
                    p = s[0]
                    s.pop(0)

                    if len(s) == 0:
                        break

                # If stack is not empty then assign p as
                # the stack's top node's right child
                if len(s):
                    p = s[0].right

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

printLeafLeftToRight(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to print leaf nodes from
// left to{ right using one stack
using System;
using System.Collections.Generic;

class GfG
{

// Structure of binary tree
public class Node
{
    public Node left;
    public Node right;
    public int data;
}

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.data = key;
    return node;
}

// Function to Print all the leaf nodes
// of Binary tree using one stack
static void printLeafLeftToRight(Node p)
{
    // stack to store the nodes
    Stack<Node> s = new Stack<Node> ();

    while (true)
    {
        // If p is not null then push
        // it on the stack
        if (p != null)
        {
            s.Push(p);
            p = p.left;
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
                // right subtree as null then pop that node and
                // print the node only if its left
                // subtree is also null
                if (s.Peek().right == null)
                {
                    p = s.Peek();
                    s.Pop();

                    // Print the leaf node
                    if (p.left == null)
                        Console.Write(p.data + " ");
                }

                while (p == s.Peek().right)
                {
                    p = s.Peek();
                    s.Pop();

                    if (s.Count == 0)
                        break;
                }

                // If stack is not empty then assign p as
                // the stack's top node's right child
                if (s.Count != 0)
                    p = s.Peek().right;
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

    printLeafLeftToRight(root);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to print leaf nodes from
    // left to{ right using one stack

    // Structure of binary tree
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let node = new Node(key);
        return node;
    }

    // Function to Print all the leaf nodes
    // of Binary tree using one stack
    function printLeafLeftToRight(p)
    {
        // stack to store the nodes
        let s = [];

        while (true)
        {
            // If p is not null then push
            // it on the stack
            if (p != null)
            {
                s.push(p);
                p = p.left;
            }

            else
            {
                // If stack is empty then come out
                // of the loop
                if (s.length == 0)
                    break;
                else
                {
                    // If the node on top of the stack has its
                    // right subtree as null then pop that node and
                    // print the node only if its left
                    // subtree is also null
                    if (s[s.length - 1].right == null)
                    {
                        p = s[s.length - 1];
                        s.pop();

                        // Print the leaf node
                        if (p.left == null)
                            document.write(p.data + " ");
                    }

                    while (p == s[s.length - 1].right)
                    {
                        p = s[s.length - 1];
                        s.pop();

                        if (s.length == 0)
                            break;
                    }

                    // If stack is not empty then assign p as
                    // the stack's top node's right child
                    if (s.length != 0)
                        p = s[s.length - 1].right;
                    else
                        p = null;
                }
            }
        }
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    printLeafLeftToRight(root);

</script>
```

**Output:** 

```
4 5 6 7
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)