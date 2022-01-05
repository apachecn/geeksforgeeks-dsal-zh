# 检查二叉树是否完美的迭代方法

> 原文:[https://www . geesforgeks . org/迭代方法检查二叉树是否完美/](https://www.geeksforgeeks.org/iterative-approach-to-check-if-a-binary-tree-is-perfect/)

给定一棵**二叉树**，任务是检查给定的二叉树是否是一棵完美的二叉树。
二叉树是一种[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，其中所有内部节点都有两个子节点，所有叶子都处于同一级别。
**例:**

```
Input : 
          1
         /  \
        2    3
       / \   / \
      4   5 6   7
Output : Yes

Input :
           20
         /   \
        8     22
       / \    / \
      5   3  4   25
     / \  / \     \
    1  10 2  14    6
Output : No 
One leaf node with value 4 is not present at the 
last level and node with value 25 has 
only one child.
```

我们已经讨论了[递归方法](https://www.geeksforgeeks.org/check-weather-given-binary-tree-perfect-not/)。在这篇文章中，讨论了迭代方法。
**方法:**想法是使用一个队列和一个变量**标志**，初始化为零，检查是否发现了叶节点。我们将检查:

1.  如果当前节点有两个子节点，那么我们将检查**标志**的值。如果**标志**的值为零，则推送队列中的左右子节点，但是如果**标志**的值为 1，则返回 false，因为这意味着已经找到了一个叶节点，并且在一个完美的二叉树中，所有的叶节点必须出现在最后一级，任何其他级别都不应该出现叶节点。
2.  如果当前节点没有子节点，说明是叶节点，那么将**标志**标记为 1。
3.  如果当前节点只有一个子节点，则返回 false，因为在完美的二叉树中，除了叶节点之外，所有节点都有两个子节点，叶节点必须出现在树的最后一级。

以下是上述方法的实现:

## C++

```
// C++ program to check if the
// given binary tree is perfect
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Utility function to allocate memory for a new node
Node* newNode(int data)
{
    Node* node = new (Node);
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to check if the given tree is perfect
bool CheckPerfectTree(Node* root)
{
    queue<Node*> q;

    // Push the root node
    q.push(root);

    // Flag to check if leaf nodes have been found
    int flag = 0;

    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        // If current node has both left and right child
        if (temp->left && temp->right) {
            // If a leaf node has already been found
            // then return false
            if (flag == 1)
                return false;

            // If a leaf node has not been discovered yet
            // push the left and right child in the queue
            else {
                q.push(temp->left);
                q.push(temp->right);
            }
        }

        // If a leaf node is found mark flag as one
        else if (!temp->left && !temp->right) {
            flag = 1;
        }

        // If the current node has only one child
        // then return false
        else if (!temp->left || !temp->right)
            return false;
    }

    // If the given tree is perfect return true
    return true;
}

// Driver code
int main()
{
    Node* root = newNode(7);
    root->left = newNode(5);
    root->right = newNode(6);
    root->left->left = newNode(8);
    root->left->right = newNode(1);
    root->right->left = newNode(3);
    root->right->right = newNode(9);
    root->right->right->right = newNode(13);
    root->right->right->left = newNode(10);

    if (CheckPerfectTree(root))
        printf("Yes");
    else
        printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// given binary tree is perfect
import java.util.*;

class GFG
{

// A binary tree node
static class Node
{
    int data;
    Node left, right;
};

// Utility function to allocate memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to check if the given tree is perfect
static boolean CheckPerfectTree(Node root)
{
    Queue<Node> q = new LinkedList<Node>();

    // add the root node
    q.add(root);

    // Flag to check if leaf nodes have been found
    int flag = 0;

    while (q.size() > 0)
    {
        Node temp = q.peek();
        q.remove();

        // If current node has both left and right child
        if (temp.left != null && temp.right != null)
        {
            // If a leaf node has already been found
            // then return false
            if (flag == 1)
                return false;

            // If a leaf node has not been discovered yet
            // add the left and right child in the queue
            else
            {
                q.add(temp.left);
                q.add(temp.right);
            }
        }

        // If a leaf node is found mark flag as one
        else if (temp.left == null && temp.right == null)
        {
            flag = 1;
        }

        // If the current node has only one child
        // then return false
        else if (temp.left == null || temp.right == null)
            return false;
    }

    // If the given tree is perfect return true
    return true;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(7);
    root.left = newNode(5);
    root.right = newNode(6);
    root.left.left = newNode(8);
    root.left.right = newNode(1);
    root.right.left = newNode(3);
    root.right.right = newNode(9);
    root.right.right.right = newNode(13);
    root.right.right.left = newNode(10);

    if (CheckPerfectTree(root))
        System.out.printf("Yes");
    else
        System.out.printf("No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to check if the
# given binary tree is perfect
import sys
import math

# A binary tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to allocate
# memory for a new node
def newNode(data):
    return Node(data)

# Function to check if the
# given tree is perfect
def CheckPerfectTree(root):
    q = []

    # Push the root node
    q.append(root)

    # Flag to check if leaf nodes
    # have been found
    flag = 0

    while(q):
        temp = q[0]
        q.pop(0)

        # If current node has both
        # left and right child
        if (temp.left and temp.right):

            # If a leaf node has already been found
            # then return false
            if (flag == 1):
                return False

            # If a leaf node has not been discovered yet
            # push the left and right child in the queue
            else:
                q.append(temp.left)
                q.append(temp.right)

        # If a leaf node is found
        # mark flag as one    
        elif(not temp.left and
             not temp.right):
            flag = 1

        # If the current node has only one child
        # then return false
        elif(not temp.left or
             not temp.right):
            return False

    # If the given tree is perfect
    # return true
    return True

# Driver Code
if __name__=='__main__':
    root = newNode(7)
    root.left = newNode(5)
    root.left.left = newNode(8)
    root.left.right = newNode(1)
    root.right = newNode(6)
    root.right.left = newNode(3)
    root.right.right = newNode(9)
    root.right.right.left = newNode(10)
    root.right.right.right = newNode(13)

    if CheckPerfectTree(root):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Vikash Kumar 37
```

## C#

```
// C# program to check if the
// given binary tree is perfect
using System;
using System.Collections.Generic;

class GFG
{

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;
};

// Utility function to allocate
// memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to check if the given tree is perfect
static Boolean CheckPerfectTree(Node root)
{
    Queue<Node > q = new Queue<Node>();

    // add the root node
    q.Enqueue(root);

    // Flag to check if leaf nodes
    // have been found
    int flag = 0;

    while (q.Count > 0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        // If current node has both
        // left and right child
        if (temp.left != null &&
            temp.right != null)
        {
            // If a leaf node has already been found
            // then return false
            if (flag == 1)
                return false;

            // If a leaf node has not been discovered yet
            // add the left and right child in the queue
            else
            {
                q.Enqueue(temp.left);
                q.Enqueue(temp.right);
            }
        }

        // If a leaf node is found mark flag as one
        else if (temp.left == null &&
                 temp.right == null)
        {
            flag = 1;
        }

        // If the current node has only one child
        // then return false
        else if (temp.left == null ||
                 temp.right == null)
            return false;
    }

    // If the given tree is perfect return true
    return true;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(7);
    root.left = newNode(5);
    root.right = newNode(6);
    root.left.left = newNode(8);
    root.left.right = newNode(1);
    root.right.left = newNode(3);
    root.right.right = newNode(9);
    root.right.right.right = newNode(13);
    root.right.right.left = newNode(10);

    if (CheckPerfectTree(root))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to check if the
// given binary tree is perfect

// A binary tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Function to check if the given tree is perfect
function CheckPerfectTree(root)
{
    let q = [];

    // add the root node
    q.push(root);

    // Flag to check if leaf nodes have been found
    let flag = 0;

    while (q.length > 0)
    {
        let temp = q[0];
        q.shift();

        // If current node has both left and right child
        if (temp.left != null && temp.right != null)
        {
            // If a leaf node has already been found
            // then return false
            if (flag == 1)
                return false;

            // If a leaf node has not been discovered yet
            // add the left and right child in the queue
            else
            {
                q.push(temp.left);
                q.push(temp.right);
            }
        }

        // If a leaf node is found mark flag as one
        else if (temp.left == null && temp.right == null)
        {
            flag = 1;
        }

        // If the current node has only one child
        // then return false
        else if (temp.left == null || temp.right == null)
            return false;
    }

    // If the given tree is perfect return true
    return true;
}

// Driver code
let root = new Node(7);
root.left = new Node(5);
root.right = new Node(6);
root.left.left = new Node(8);
root.left.right = new Node(1);
root.right.left = new Node(3);
root.right.right = new Node(9);
root.right.right.right = new Node(13);
root.right.right.left = new Node(10);

if (CheckPerfectTree(root))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
No    
```

**时间复杂度** : O(N)，其中 N 为二叉树中的节点总数。
**辅助空间:** O(N)