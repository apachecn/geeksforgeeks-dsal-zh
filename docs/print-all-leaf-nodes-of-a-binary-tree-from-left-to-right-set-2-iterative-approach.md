# 从左到右打印二叉树的所有叶节点| Set-2(迭代方法)

> 原文:[https://www . geesforgeks . org/print-二叉树的所有叶节点-从左到右-集合-2-迭代方法/](https://www.geeksforgeeks.org/print-all-leaf-nodes-of-a-binary-tree-from-left-to-right-set-2-iterative-approach/)

给定一棵二叉树，任务是从左到右打印叶节点。节点必须按照从左到右的顺序打印。
**例:**

```
Input :
           1
          /  \
         2    3
        / \  / \
       4  5  6  7

Output :4 5 6 7

Input :
            4
           /  \
          5    9
         / \  / \
        8   3 7  2
       /         / \
      12        6   1

Output :12 3 7 6 1
```

我们已经讨论了[递归](https://www.geeksforgeeks.org/print-leaf-nodes-left-right-binary-tree/)方法。这里我们将使用两个堆栈来解决这个问题。
**做法:**思路是用两个栈，一个存储树的所有节点，一个存储所有叶子节点。我们将弹出第一个堆栈的顶部节点。如果该节点有一个左子节点，我们将把它推到第一个堆栈的顶部，如果它有一个右子节点，我们将把它推到第一个堆栈的顶部，但是如果该节点是一个叶节点，我们将把它推到第二个堆栈的顶部。我们将对所有节点执行此操作，直到我们完全遍历了二叉树。
然后我们将开始弹出第二个堆栈，并打印其所有元素，直到堆栈变空。
以下是上述方法的实现:

## C++

```
// C++ program to print all the leaf nodes
// of a Binary tree from left to right
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    Node* left;
    Node* right;
    int data;
};

// Function to create a new
// Binary node
Node* newNode(int data)
{
    Node* temp = new Node;

    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// Function to Print all the leaf nodes
// of Binary tree using two stacks
void PrintLeafLeftToRight(Node* root)
{
    // Stack to store all the nodes of tree
    stack<Node*> s1;

    // Stack to store all the leaf nodes
    stack<Node*> s2;

    // Push the root node
    s1.push(root);

    while (!s1.empty()) {
        Node* curr = s1.top();
        s1.pop();

        // If current node has a left child
        // push it onto the first stack
        if (curr->left)
            s1.push(curr->left);

        // If current node has a right child
        // push it onto the first stack
        if (curr->right)
            s1.push(curr->right);

        // If current node is a leaf node
        // push it onto the second stack
        else if (!curr->left && !curr->right)
            s2.push(curr);
    }

    // Print all the leaf nodes
    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}

// Driver code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(7);
    root->left->left->left = newNode(10);
    root->left->left->right = newNode(11);
    root->right->right->left = newNode(8);

    PrintLeafLeftToRight(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the leaf nodes
// of a Binary tree from left to right
import java.util.*;

class GFG
{

// Binary tree node
static class Node
{
    Node left;
    Node right;
    int data;
};

// Function to create a new
// Binary node
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Function to Print all the leaf nodes
// of Binary tree using two stacks
static void PrintLeafLeftToRight(Node root)
{
    // Stack to store all the nodes of tree
    Stack<Node> s1 = new Stack<>();

    // Stack to store all the leaf nodes
    Stack<Node> s2 = new Stack<>();;

    // Push the root node
    s1.push(root);

    while (!s1.empty())
    {
        Node curr = s1.peek();
        s1.pop();

        // If current node has a left child
        // push it onto the first stack
        if (curr.left!=null)
            s1.push(curr.left);

        // If current node has a right child
        // push it onto the first stack
        if (curr.right!=null)
            s1.push(curr.right);

        // If current node is a leaf node
        // push it onto the second stack
        else if (curr.left==null && curr.right==null)
            s2.push(curr);
    }

    // Print all the leaf nodes
    while (!s2.empty())
    {
        System.out.print(s2.peek().data +" ");
        s2.pop();
    }
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(7);
    root.left.left.left = newNode(10);
    root.left.left.right = newNode(11);
    root.right.right.left = newNode(8);

    PrintLeafLeftToRight(root);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print all the leaf
# nodes of a Binary tree from left to right

# Binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to Print all the leaf nodes
# of Binary tree using two stacks
def PrintLeafLeftToRight(root):

    # Stack to store all the nodes
    # of tree
    s1 = []

    # Stack to store all the
    # leaf nodes
    s2 = []

    # Push the root node
    s1.append(root)

    while len(s1) != 0:
        curr = s1.pop()

        # If current node has a left child
        # push it onto the first stack
        if curr.left:
            s1.append(curr.left)

        # If current node has a right child
        # push it onto the first stack
        if curr.right:
            s1.append(curr.right)

        # If current node is a leaf node
        # push it onto the second stack
        elif not curr.left and not curr.right:
            s2.append(curr)

    # Print all the leaf nodes
    while len(s2) != 0:
        print(s2.pop().data, end = " ")

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.right.left = Node(5)
    root.right.right = Node(7)
    root.left.left.left = Node(10)
    root.left.left.right = Node(11)
    root.right.right.left = Node(8)

    PrintLeafLeftToRight(root)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to print all the leaf nodes
// of a Binary tree from left to right
using System;
using System.Collections.Generic;

class GFG
{

// Binary tree node
public class Node
{
    public Node left;
    public Node right;
    public int data;
};

// Function to create a new
// Binary node
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Function to Print all the leaf nodes
// of Binary tree using two stacks
static void PrintLeafLeftToRight(Node root)
{
    // Stack to store all the nodes of tree
    Stack<Node> s1 = new Stack<Node>();

    // Stack to store all the leaf nodes
    Stack<Node> s2 = new Stack<Node>();;

    // Push the root node
    s1.Push(root);

    while (s1.Count != 0)
    {
        Node curr = s1.Peek();
        s1.Pop();

        // If current node has a left child
        // push it onto the first stack
        if (curr.left != null)
            s1.Push(curr.left);

        // If current node has a right child
        // push it onto the first stack
        if (curr.right != null)
            s1.Push(curr.right);

        // If current node is a leaf node
        // push it onto the second stack
        else if (curr.left == null && curr.right == null)
            s2.Push(curr);
    }

    // Print all the leaf nodes
    while (s2.Count != 0)
    {
        Console.Write(s2.Peek().data + " ");
        s2.Pop();
    }
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(7);
    root.left.left.left = newNode(10);
    root.left.left.right = newNode(11);
    root.right.right.left = newNode(8);

    PrintLeafLeftToRight(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create a new
    // Binary node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Function to Print all the leaf nodes
    // of Binary tree using two stacks
    function PrintLeafLeftToRight(root)
    {
        // Stack to store all the nodes of tree
        let s1 = [];

        // Stack to store all the leaf nodes
        let s2 = [];

        // Push the root node
        s1.push(root);

        while (s1.length > 0)
        {
            let curr = s1[s1.length - 1];
            s1.pop();

            // If current node has a left child
            // push it onto the first stack
            if (curr.left!=null)
                s1.push(curr.left);

            // If current node has a right child
            // push it onto the first stack
            if (curr.right!=null)
                s1.push(curr.right);

            // If current node is a leaf node
            // push it onto the second stack
            else if (curr.left==null && curr.right==null)
                s2.push(curr);
        }

        // Print all the leaf nodes
        while (s2.length > 0)
        {
            document.write(s2[s2.length - 1].data +" ");
            s2.pop();
        }
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(7);
    root.left.left.left = newNode(10);
    root.left.left.right = newNode(11);
    root.right.right.left = newNode(8);

    PrintLeafLeftToRight(root);

</script>
```

**Output:** 

```
10 11 5 8
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)