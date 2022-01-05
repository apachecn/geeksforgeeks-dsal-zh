# 打印二叉树的所有内部节点

> 原文:[https://www . geesforgeks . org/print-所有内部二进制树节点/](https://www.geeksforgeeks.org/print-all-internal-nodes-of-a-binary-tree/)

给定一个二叉树，任务是打印树中的所有内部节点。
内部节点是携带至少一个子节点的节点，或者换句话说，内部节点不是叶节点。这里我们打算按级别顺序打印所有这样的内部节点。考虑以下二叉树:

> **输入:**
> 
> ![](img/c35975ff02b33077883e5901580c1c2d.png)
> 
> **输出:** 15 10 20

解决这个问题的方法包括一个 BFS 树。算法如下:

*   通过逐个推送队列中的节点来执行级别顺序遍历。
*   逐个弹出队列中的元素，并跟踪以下情况:
    1.  该节点只有一个左子节点。
    2.  该节点只有一个右子节点。
    3.  该节点既有左子节点也有右子节点。
    4.  该节点根本没有子节点。
*   除了案例 4，打印所有其他 3 个案例的节点中的数据。

以下是上述方法的实现:

## C++

```
// C++ program to print all internal
// nodes in tree
#include <bits/stdc++.h>
using namespace std;

// A node in the Binary tree
struct Node {
    int data;
    Node *left, *right;
    Node(int data)
    {
       left = right = NULL;
       this->data = data;
    }
};

// Function to print all internal nodes
// in level order from left to right
void printInternalNodes(Node* root)
{
    // Using a queue for a level order traversal
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {

        // Check and pop the element in
        // the front of the queue
        Node* curr = q.front();
        q.pop();

        // The variable flag keeps track of
        // whether a node is an internal node
        bool isInternal = 0;

        // The node has a left child
        if (curr->left) {
            isInternal = 1;
            q.push(curr->left);
        }

        // The node has a right child
        if (curr->right) {
            isInternal = 1;
            q.push(curr->right);
        }

        // In case the node has either a left
        // or right child or both print the data
        if (isInternal)
            cout << curr->data << " ";
    }
}

// Driver program to build a sample tree
int main()
{
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->right = new Node(6);
    root->right->right->right = new Node(10);
    root->right->right->left = new Node(7);
    root->right->left->left = new Node(8);
    root->right->left->right = new Node(9);

    // A call to the function
    printInternalNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all internal
// nodes in tree
import java.util.*;
class GfG
{

// A node in the Binary tree
static class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        left = right = null;
        this.data = data;
    }
}

// Function to print all internal nodes
// in level order from left to right
static void printInternalNodes(Node root)
{
    // Using a queue for a level order traversal
    Queue<Node> q = new LinkedList<Node>();
    q.add(root);
    while (!q.isEmpty())
    {

        // Check and pop the element in
        // the front of the queue
        Node curr = q.peek();
        q.remove();

        // The variable flag keeps track of
        // whether a node is an internal node
        boolean isInternal = false;

        // The node has a left child
        if (curr.left != null)
        {
            isInternal = true;
            q.add(curr.left);
        }

        // The node has a right child
        if (curr.right != null)
        {
            isInternal = true;
            q.add(curr.right);
        }

        // In case the node has either a left
        // or right child or both print the data
        if (isInternal == true)
            System.out.print(curr.data + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.right.right = new Node(10);
    root.right.right.left = new Node(7);
    root.right.left.left = new Node(8);
    root.right.left.right = new Node(9);

    // A call to the function
    printInternalNodes(root);
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to print all internal
# nodes in tree

# A node in the Binary tree
class new_Node:

    # Constructor to create a new_Node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print all internal nodes
# in level order from left to right
def printInternalNodes(root):

    # Using a queue for a level order traversal
    q = []
    q.append(root)
    while (len(q)):

        # Check and pop the element in
        # the front of the queue
        curr = q[0]
        q.pop(0)

        # The variable flag keeps track of
        # whether a node is an internal node
        isInternal = 0

        # The node has a left child
        if (curr.left):
            isInternal = 1
            q.append(curr.left)

        # The node has a right child
        if (curr.right):
            isInternal = 1
            q.append(curr.right)

        # In case the node has either a left
        # or right child or both print the data
        if (isInternal):
            print(curr.data, end = " ")

# Driver Code
root = new_Node(1)
root.left = new_Node(2)
root.right = new_Node(3)
root.left.left = new_Node(4)
root.right.left = new_Node(5)
root.right.right = new_Node(6)
root.right.right.right = new_Node(10)
root.right.right.left = new_Node(7)
root.right.left.left = new_Node(8)
root.right.left.right = new_Node(9)

# A call to the function
printInternalNodes(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to print all internal
// nodes in tree
using System;
using System.Collections.Generic;

class GFG
{

// A node in the Binary tree
public class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        left = right = null;
        this.data = data;
    }
}

// Function to print all internal nodes
// in level order from left to right
static void printInternalNodes(Node root)
{
    // Using a queue for a level order traversal
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);
    while (q.Count != 0)
    {

        // Check and pop the element in
        // the front of the queue
        Node curr = q.Peek();
        q.Dequeue();

        // The variable flag keeps track of
        // whether a node is an internal node
        Boolean isInternal = false;

        // The node has a left child
        if (curr.left != null)
        {
            isInternal = true;
            q.Enqueue(curr.left);
        }

        // The node has a right child
        if (curr.right != null)
        {
            isInternal = true;
            q.Enqueue(curr.right);
        }

        // In case the node has either a left
        // or right child or both print the data
        if (isInternal == true)
            Console.Write(curr.data + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.right.right = new Node(10);
    root.right.right.left = new Node(7);
    root.right.left.left = new Node(8);
    root.right.left.right = new Node(9);

    // A call to the function
    printInternalNodes(root);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to print all internal nodes in tree

    // A node in the Binary tree
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to print all internal nodes
    // in level order from left to right
    function printInternalNodes(root)
    {
        // Using a queue for a level order traversal
        let q = [];
        q.push(root);
        while (q.length > 0)
        {

            // Check and pop the element in
            // the front of the queue
            let curr = q[0];
            q.shift();

            // The variable flag keeps track of
            // whether a node is an internal node
            let isInternal = false;

            // The node has a left child
            if (curr.left != null)
            {
                isInternal = true;
                q.push(curr.left);
            }

            // The node has a right child
            if (curr.right != null)
            {
                isInternal = true;
                q.push(curr.right);
            }

            // In case the node has either a left
            // or right child or both print the data
            if (isInternal == true)
                document.write(curr.data + " ");
        }
    }

    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.right.right = new Node(10);
    root.right.right.left = new Node(7);
    root.right.left.left = new Node(8);
    root.right.left.right = new Node(9);

    // A call to the function
    printInternalNodes(root);

</script>
```

**Output:** 

```
1 2 3 5 6
```