# 求最大水平的叶子的和

> 原文:[https://www . geesforgeks . org/find-the-sum-of-leaves-at-max-level/](https://www.geeksforgeeks.org/find-the-sum-of-leafs-at-maximum-level/)

给定一个包含 **n 个**节点的二叉树。任务是找出最大级别上所有叶节点的总和。
**例:**

```
Input:
              1
            /   \
           2     3
         /  \   /  \
        4   5   6   7
           /     \
          8       9

Output: 17
Leaf nodes 8 and 9 are at maximum level.
Their sum = (8 + 9) = 17.

Input:
              5
            /   \
           8     13
         /
        4 

Output: 4
```

**方法:**使用队列执行[迭代级序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)，找出每一级的节点之和，如果当前级的每个节点都没有子节点，则将该级标记为最大级。最大级别的所有叶节点的总和将是必需的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// Function to get a new node
Node* getNode(int data)
{
    // Allocate space
    Node* newNode = (Node*)malloc(sizeof(Node));

    // Put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function to return the sum of the
// leaf nodes at maximum level
int sumOfLeafNodesAtMaxLevel(Node* root)
{
    // If tree is empty
    if (!root)
        return 0;

    // If there is only one node
    if (!root->left && !root->right)
        return root->data;

    // Queue used for level order traversal
    queue<Node*> q;
    int leafSum = 0;
    bool f = 0;

    // Push root node in the queue 'q'
    q.push(root);

    while (true) {

        // Count number of nodes in the
        // current level
        int nc = q.size();

        // If the queue is empty, it means that the
        // last processed level was the maximum level
        if (nc == 0)
            return leafSum;

        // Initialize leafSum for current level
        leafSum = 0;

        // Traverse the current level nodes
        while (nc--) {

            // Get front element from 'q'
            Node* top = q.front();
            q.pop();

            // If it is a leaf node
            if (!top->left && !top->right) {

                // Accumulate data to 'sum'
                leafSum += top->data;
            }
            else {

                // If top's left and right child
                // exist then push them to 'q'
                if (top->left)
                    q.push(top->left);
                if (top->right)
                    q.push(top->right);
            }
        }
    }
}

// Driver code
int main()
{
    // Binary tree creation
    Node* root = getNode(1);
    root->left = getNode(2);
    root->right = getNode(3);
    root->left->left = getNode(4);
    root->left->right = getNode(5);
    root->right->left = getNode(6);
    root->right->right = getNode(7);
    root->left->right->left = getNode(8);
    root->right->left->right = getNode(9);

    cout << sumOfLeafNodesAtMaxLevel(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Structure of a node of binary tree
    static class Node {
        int data;
        Node left, right;
    };

    // Function to get a new node
    static Node getNode(int data)
    {
        // Allocate space
        Node newNode = new Node();

        // Put in the data
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
    }

    // Function to return the sum of the
    // leaf nodes at maximum level
    static int sumOfLeafNodesAtMaxLevel(Node root)
    {
        // If tree is empty
        if (root == null)
            return 0;

        // If there is only one node
        if (root.left == null && root.right == null)
            return root.data;

        // Queue used for level order traversal
        Queue<Node> q = new LinkedList<>();
        int leafSum = 0;
        boolean f = false;

        // Push root node in the queue 'q'
        q.add(root);

        while (true) {

            // Count number of nodes in the
            // current level
            int nc = q.size();

            // If the queue is empty, it means that the
            // last processed level was the maximum level
            if (nc == 0)
                return leafSum;

            // Initialize leafSum for current level
            leafSum = 0;

            // Traverse the current level nodes
            while (nc-- > 0) {

                // Get front element from 'q'
                Node top = q.peek();
                q.remove();

                // If it is a leaf node
                if (top.left == null && top.right == null) {

                    // Accumulate data to 'sum'
                    leafSum += top.data;
                }
                else {

                    // If top's left and right child
                    // exist then push them to 'q'
                    if (top.left != null)
                        q.add(top.left);
                    if (top.right != null)
                        q.add(top.right);
                }
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        // Binary tree creation
        Node root = getNode(1);
        root.left = getNode(2);
        root.right = getNode(3);
        root.left.left = getNode(4);
        root.left.right = getNode(5);
        root.right.left = getNode(6);
        root.right.right = getNode(7);
        root.left.right.left = getNode(8);
        root.right.left.right = getNode(9);

        System.out.print(sumOfLeafNodesAtMaxLevel(root));
    }
}

// This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Structure of a node of binary tree
    public class Node {
        public int data;
        public Node left, right;
    };

    // Function to get a new node
    static Node getNode(int data)
    {
        // Allocate space
        Node newNode = new Node();

        // Put in the data
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
    }

    // Function to return the sum of the
    // leaf nodes at maximum level
    static int sumOfLeafNodesAtMaxLevel(Node root)
    {
        // If tree is empty
        if (root == null)
            return 0;

        // If there is only one node
        if (root.left == null && root.right == null)
            return root.data;

        // Queue used for level order traversal
        Queue<Node> q = new Queue<Node>();
        int leafSum = 0;

        // Push root node in the queue 'q'
        q.Enqueue(root);

        while (true) {

            // Count number of nodes in the
            // current level
            int nc = q.Count;

            // If the queue is empty, it means that the
            // last processed level was the maximum level
            if (nc == 0)
                return leafSum;

            // Initialize leafSum for current level
            leafSum = 0;

            // Traverse the current level nodes
            while (nc-- > 0) {

                // Get front element from 'q'
                Node top = q.Peek();
                q.Dequeue();

                // If it is a leaf node
                if (top.left == null && top.right == null) {

                    // Accumulate data to 'sum'
                    leafSum += top.data;
                }
                else {

                    // If top's left and right child
                    // exist then push them to 'q'
                    if (top.left != null)
                        q.Enqueue(top.left);
                    if (top.right != null)
                        q.Enqueue(top.right);
                }
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Binary tree creation
        Node root = getNode(1);
        root.left = getNode(2);
        root.right = getNode(3);
        root.left.left = getNode(4);
        root.left.right = getNode(5);
        root.right.left = getNode(6);
        root.right.right = getNode(7);
        root.left.right.left = getNode(8);
        root.right.left.right = getNode(9);

        Console.Write(sumOfLeafNodesAtMaxLevel(root));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// Structure of a node of binary tree
class Node {
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to get a new node
function getNode(data)
{
    // Allocate space
    var newNode = new Node();
    // Put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}
// Function to return the sum of the
// leaf nodes at maximum level
function sumOfLeafNodesAtMaxLevel(root)
{
    // If tree is empty
    if (root == null)
        return 0;
    // If there is only one node
    if (root.left == null && root.right == null)
        return root.data;
    // Queue used for level order traversal
    var q = [];
    var leafSum = 0;
    // Push root node in the queue 'q'
    q.push(root);
    while (true) {
        // Count number of nodes in the
        // current level
        var nc = q.length;
        // If the queue is empty, it means that the
        // last processed level was the maximum level
        if (nc == 0)
            return leafSum;
        // Initialize leafSum for current level
        leafSum = 0;
        // Traverse the current level nodes
        while (nc-- > 0) {
            // Get front element from 'q'
            var top = q[0];
            q.shift();
            // If it is a leaf node
            if (top.left == null && top.right == null) {
                // Accumulate data to 'sum'
                leafSum += top.data;
            }
            else {
                // If top's left and right child
                // exist then push them to 'q'
                if (top.left != null)
                    q.push(top.left);
                if (top.right != null)
                    q.push(top.right);
            }
        }
    }
}

// Driver code
// Binary tree creation
var root = getNode(1);
root.left = getNode(2);
root.right = getNode(3);
root.left.left = getNode(4);
root.left.right = getNode(5);
root.right.left = getNode(6);
root.right.right = getNode(7);
root.left.right.left = getNode(8);
root.right.left.right = getNode(9);
document.write(sumOfLeafNodesAtMaxLevel(root));

</script>
```

**Output:** 

```
17
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)