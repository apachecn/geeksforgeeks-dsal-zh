# 打印给定二叉树每一级除最左边节点外的所有节点

> 原文:[https://www . geesforgeks . org/print-除了给定二叉树的每一级中最左边的节点之外的所有节点/](https://www.geeksforgeeks.org/print-all-the-nodes-except-the-leftmost-node-in-every-level-of-the-given-binary-tree/)

给定一棵二叉树，任务是打印除了树的每一级中最左边的节点之外的所有节点。根被视为 0 级，任何级别的最左侧节点被视为 0 位置的节点。

**示例:**

```
Input:
          1
       /     \
      2       3
    /   \       \
   4     5       6
        /  \
       7    8
      /      \
     9        10

Output:
3
5  6
8
10

Input:
          1
        /   \
       2     3
        \     \
         4     5
Output:
3
5
```

**方法:**要逐级打印节点，请使用级别顺序遍历。思路是基于[逐行打印级序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)。为此，逐级遍历节点，并在每级处理之前标记**最左边的**标志为真，在每级处理第一个节点之后标记为假。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of the tree node
struct Node {
    int data;
    Node *left, *right;
};

// Utility method to create a node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to print all the nodes
// except the leftmost in every level
// of the given binary tree
// with level order traversal
void excludeLeftmost(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue for level
    // order traversal
    queue<Node*> q;

    // Enqueue root
    q.push(root);

    while (1) {

        // nodeCount (queue size) indicates
        // number of nodes at current level.
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Initialize leftmost as true
        // just before the beginning
        // of each level
        bool leftmost = true;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0) {
            Node* node = q.front();

            // Switch leftmost flag after processing
            // the leftmost node
            if (leftmost)
                leftmost = !leftmost;

            // Print all the nodes except leftmost
            else
                cout << node->data << " ";
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;
        }
        cout << "\n";
    }
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->right->left = newNode(8);
    root->left->right->right = newNode(9);
    root->left->right->right->right = newNode(10);

    excludeLeftmost(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class Sol
{

// Structure of the tree node
static class Node
{
    int data;
    Node left, right;
};

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print all the nodes
// except the leftmost in every level
// of the given binary tree
// with level order traversal
static void excludeLeftmost(Node root)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new LinkedList<Node>();

    // Enqueue root
    q.add(root);

    while (true)
    {

        // nodeCount (queue size) indicates
        // number of nodes at current level.
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Initialize leftmost as true
        // just before the beginning
        // of each level
        boolean leftmost = true;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            Node node = q.peek();

            // Switch leftmost flag after processing
            // the leftmost node
            if (leftmost)
                leftmost = !leftmost;

            // Print all the nodes except leftmost
            else
                System.out.print( node.data + " ");
            q.remove();
            if (node.left != null)
                q.add(node.left);
            if (node.right != null)
                q.add(node.right);
            nodeCount--;
        }
        System.out.println();
    }
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
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.right.right = newNode(10);

    excludeLeftmost(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach
from collections import deque

# Structure of the tree node
class Node:
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# Utility method to create a node
def newNode(data: int) -> Node:
    node = Node()
    node.data = data
    node.left = None
    node.right = None
    return node

# Function to print all the nodes
# except the leftmost in every level
# of the given binary tree
# with level order traversal
def excludeLeftMost(root: Node):

    # Base Case
    if root is None:
        return

    # Create an empty queue for level
    # order traversal
    q = deque()

    # Enqueue root
    q.append(root)

    while 1:

        # nodeCount (queue size) indicates
        # number of nodes at current level
        nodeCount = len(q)
        if nodeCount == 0:
            break

        # Initialize leftmost as true
        # just before the beginning
        # of each level
        leftmost = True

        # Dequeue all nodes of current level
        # and Enqueue all nodes of next level
        while nodeCount > 0:
            node = q[0]

            # Switch leftmost flag after processing
            # the leftmost node
            if leftmost:
                leftmost = not leftmost

            # Print all the nodes except leftmost
            else:
                print(node.data, end=" ")
            q.popleft()

            if node.left is not None:
                q.append(node.left)
            if node.right is not None:
                q.append(node.right)
            nodeCount -= 1
        print()

# Driver Code
if __name__ == "__main__":
    root = Node()
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.left.right.left = newNode(8)
    root.left.right.right = newNode(9)
    root.left.right.right.right = newNode(10)
    excludeLeftMost(root)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Structure of the tree node
public class Node
{
    public int data;
    public Node left, right;
};

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print all the nodes
// except the leftmost in every level
// of the given binary tree
// with level order traversal
static void excludeLeftmost(Node root)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new Queue<Node>();

    // Enqueue root
    q.Enqueue(root);

    while (true)
    {

        // nodeCount (queue size) indicates
        // number of nodes at current level.
        int nodeCount = q.Count;
        if (nodeCount == 0)
            break;

        // Initialize leftmost as true
        // just before the beginning
        // of each level
        Boolean leftmost = true;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            Node node = q.Peek();

            // Switch leftmost flag after processing
            // the leftmost node
            if (leftmost)
                leftmost = !leftmost;

            // Print all the nodes except leftmost
            else
                Console.Write( node.data + " ");
            q.Dequeue();
            if (node.left != null)
                q.Enqueue(node.left);
            if (node.right != null)
                q.Enqueue(node.right);
            nodeCount--;
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.right.right = newNode(10);

    excludeLeftmost(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Structure of the tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Utility method to create a node
function newNode(data)
{
    let node = new Node(data);
    return (node);
}

// Function to print all the nodes
// except the leftmost in every level
// of the given binary tree
// with level order traversal
function excludeLeftmost(root)
{

    // Base Case
    if (root == null)
        return;

    // Create an empty queue for level
    // order traversal
    let q = [];

    // Enqueue root
    q.push(root);

    while (true)
    {

        // nodeCount (queue size) indicates
        // number of nodes at current level.
        let nodeCount = q.length;
        if (nodeCount == 0)
            break;

        // Initialize leftmost as true
        // just before the beginning
        // of each level
        let leftmost = true;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            let node = q[0];

            // Switch leftmost flag after processing
            // the leftmost node
            if (leftmost)
                leftmost = !leftmost;

            // Print all the nodes except leftmost
            else
                document.write(node.data + " ");

            q.shift();
            if (node.left != null)
                q.push(node.left);
            if (node.right != null)
                q.push(node.right);

            nodeCount--;
        }
        document.write("</br>");
    }
}

// Driver code
let root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);
root.left.right.left = newNode(8);
root.left.right.right = newNode(9);
root.left.right.right.right = newNode(10);

excludeLeftmost(root);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
3 
5 6 7 
9
```