# 打印二叉树每一级除最右边节点外的所有节点

> 原文:[https://www . geesforgeks . org/print-所有节点-除了-二叉树每一级的最右边节点/](https://www.geeksforgeeks.org/print-all-nodes-except-rightmost-node-of-every-level-of-the-binary-tree/)

给定一个二叉树，任务是打印除了树的每一级中最右边的节点之外的所有节点。根被视为 0 级，任何级别的最右边的节点被视为 0 位置的节点。
**例:**

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
2
4 5
7
9

Input:
          1
        /   \
       2     3
        \     \
         4     5
Output:
2
4
```

**方法:**要逐级打印节点，请使用级别顺序遍历。思路是基于[逐行打印级序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)。为此，逐级遍历节点，如果级别顺序队列中的节点是最后一个节点，则该节点将是最右边的节点，并且不打印该节点。
以下是上述方法的实施:

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
// except the rightmost in every level
// of the given binary tree
// with level order traversal
void excluderightmost(Node* root)
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

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0) {
            Node* node = q.front();

            // If node is not rightmost print
            if (nodeCount != 1)
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

    excluderightmost(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class Sol {

    // Structure of the tree node
    static class Node {
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
    // except the rightmost in every level
    // of the given binary tree
    // with level order traversal
    static void excluderightmost(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new LinkedList<Node>();

        // Enqueue root
        q.add(root);

        while (true) {

            // nodeCount (queue size) indicates
            // number of nodes at current level.
            int nodeCount = q.size();
            if (nodeCount == 0)
                break;

            // Dequeue all nodes of current level
            // and Enqueue all nodes of next level
            while (nodeCount > 0) {
                Node node = q.peek();

                // If node is not rightmost print
                if (nodeCount != 1)
                    System.out.print(node.data + " ");
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

        excluderightmost(root);
    }
}
```

## 计算机编程语言

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
# except the rightmost in every level
# of the given binary tree
# with level order traversal
def excluderightmost(root: Node):

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

        # Dequeue all nodes of current level
        # and Enqueue all nodes of next level
        while nodeCount > 0:
            node = q[0]

            # If Node is not right most print
            if nodeCount != 1:
                print(node.data, end =" ")
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
    excluderightmost(root)
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Structure of the tree node
    public class Node {
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
    // except the rightmost in every level
    // of the given binary tree
    // with level order traversal
    static void excluderightmost(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new Queue<Node>();

        // Enqueue root
        q.Enqueue(root);

        while (true) {

            // nodeCount (queue size) indicates
            // number of nodes at current level.
            int nodeCount = q.Count;
            if (nodeCount == 0)
                break;

            // Dequeue all nodes of current level
            // and Enqueue all nodes of next level
            while (nodeCount > 0) {
                Node node = q.Peek();

                // if Node is not right most print
                if (nodeCount != 1)
                    Console.Write(node.data + " ");
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
    public static void Main(String[] args)
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

        excluderightmost(root);
    }
}
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
// Structure of the tree node

class Node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};
// Utility method to create a node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}
// Function to print all the nodes
// except the rightmost in every level
// of the given binary tree
// with level order traversal
function excluderightmost(root)
{
    // Base Case
    if (root == null)
        return;
    // Create an empty queue for level
    // order traversal
    var q = [];
    // push root
    q.push(root);
    while (true) {
        // nodeCount (queue size) indicates
        // number of nodes at current level.
        var nodeCount = q.length;
        if (nodeCount == 0)
            break;
        // Dequeue all nodes of current level
        // and push all nodes of next level
        while (nodeCount > 0) {
            var node = q[0];
            // if Node is not right most print
            if (nodeCount != 1)
                document.write(node.data + " ");
            q.shift();
            if (node.left != null)
                q.push(node.left);
            if (node.right != null)
                q.push(node.right);
            nodeCount--;
        }
        document.write("<br>");
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
root.left.right.left = newNode(8);
root.left.right.right = newNode(9);
root.left.right.right.right = newNode(10);
excluderightmost(root);

</script>
```

**Output:** 

```
2 
4 5 6 
8
```