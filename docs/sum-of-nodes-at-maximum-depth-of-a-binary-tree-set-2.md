# 二叉树最大深度的节点总和|集合 2

> 原文:[https://www . geeksforgeeks . org/二叉树最大深度节点总数-集合-2/](https://www.geeksforgeeks.org/sum-of-nodes-at-maximum-depth-of-a-binary-tree-set-2/)

给定一棵树的根节点，求距根节点最大深度的所有叶节点的和。
**例:**

```
      1
    /   \
   2     3
  / \   / \
 4   5 6   7

Input : root(of above tree)
Output : 22

Explanation:
Nodes at maximum depth are: 4, 5, 6, 7\. 
So, sum of these nodes = 22
```

在[上一篇文章](https://www.geeksforgeeks.org/sum-nodes-maximum-depth-binary-tree/)中，我们讨论了一个递归解决方案，它首先找到最大级别，然后找到该级别上所有节点的总和。
在本文中，我们将看到一个递归解决方案，而不需要找到高度或深度。其思想是在遍历节点时，将节点的级别与 max_level(直到当前节点的最大级别)进行比较。如果当前级别超过最大级别，则将 max_level 更新为当前级别。如果最大级别和当前级别相同，则将根数据添加到当前总和，否则如果级别小于 max_level，则不执行任何操作。
以下是上述办法的实施:

## C++

```
// C++ Program to find sum of nodes at maximum
// Depth of the Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Variables to store sum and
// maximum level
int sum = 0, max_level = INT_MIN;

// Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
};

// Utility function to create and
// return a new Binary Tree Node
Node* createNode(int val)
{

    Node* node = new Node;

    node->data = val;
    node->left = NULL;
    node->right = NULL;

    return node;
}

// Function to find the sum of the node which
// are present at the maximum depth
void sumOfNodesAtMaxDepth(Node* root, int level)
{
    if (root == NULL)
        return;

    // If the current level exceeds the
    // maximum level, update the max_level
    // as current level.
    if (level > max_level) {
        sum = root->data;
        max_level = level;
    }

    // If the max level and current level
    // are same, add the root data to
    // current sum.
    else if (level == max_level) {
        sum = sum + root->data;
    }

    // Traverse the left and right subtrees
    sumOfNodesAtMaxDepth(root->left, level + 1);
    sumOfNodesAtMaxDepth(root->right, level + 1);
}

// Driver Code
int main()
{
    Node* root;
    root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);

    sumOfNodesAtMaxDepth(root, 0);

    cout << sum;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of nodes at maximum
// Depth of the Binary Tree

class GfG
{

// Variables to store sum and
// maximum level
static int sum = 0,
    max_level = Integer.MIN_VALUE;

// Binary Tree Node
static class Node
{
    int data;
    Node left;
    Node right;
}

// Utility function to create and
// return a new Binary Tree Node
static Node createNode(int val)
{

    Node node = new Node();
    node.data = val;
    node.left = null;
    node.right = null;

    return node;
}

// Function to find the sum of
// the node which are present
// at the maximum depth
static void sumOfNodesAtMaxDepth(Node root,
                                int level)
{
    if (root == null)
        return;

    // If the current level exceeds the
    // maximum level, update the max_level
    // as current level.
    if (level > max_level)
    {
        sum = root.data;
        max_level = level;
    }

    // If the max level and current level
    // are same, add the root data to
    // current sum.
    else if (level == max_level)
    {
        sum = sum + root.data;
    }

    // Traverse the left and right subtrees
    sumOfNodesAtMaxDepth(root.left, level + 1);
    sumOfNodesAtMaxDepth(root.right, level + 1);
}

// Driver Code
public static void main(String[] args)
{
    Node root = null;
    root = createNode(1);
    root.left = createNode(2);
    root.right = createNode(3);
    root.left.left = createNode(4);
    root.left.right = createNode(5);
    root.right.left = createNode(6);
    root.right.right = createNode(7);

    sumOfNodesAtMaxDepth(root, 0);
    System.out.println(sum);
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
# Python3 Program to find sum of nodes at maximum
# Depth of the Binary Tree

# Variables to store sum and
# maximum level
sum = [0]
max_level = [-(2**32)]

# Binary tree node
class createNode:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find the sum of the node which
# are present at the maximum depth
def sumOfNodesAtMaxDepth(root, level):
    if (root == None):
        return

    # If the current level exceeds the
    # maximum level, update the max_level
    # as current level.
    if (level > max_level[0]):
        sum[0] = root.data
        max_level[0] = level

    # If the max level and current level
    #are same, add the root data to
    # current sum.
    elif (level == max_level[0]):
        sum[0] = sum[0] + root.data

    # Traverse the left and right subtrees
    sumOfNodesAtMaxDepth(root.left, level + 1)
    sumOfNodesAtMaxDepth(root.right, level + 1)

# Driver Code
root = createNode(1)
root.left = createNode(2)
root.right = createNode(3)
root.left.left = createNode(4)
root.left.right = createNode(5)
root.right.left = createNode(6)
root.right.right = createNode(7)

sumOfNodesAtMaxDepth(root, 0)

print(sum[0])

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C#  Program to find sum of nodes at maximum
// Depth of the Binary Tree
using System;
public class GfG
{

    // Variables to store sum and
    // maximum level
    static int sum = 0,
        max_level = int.MinValue;

    // Binary Tree Node
    class Node
    {
        public int data;
        public Node left;
        public Node right;
    }

    // Utility function to create and
    // return a new Binary Tree Node
    static Node createNode(int val)
    {

        Node node = new Node();
        node.data = val;
        node.left = null;
        node.right = null;

        return node;
    }

    // Function to find the sum of
    // the node which are present
    // at the maximum depth
    static void sumOfNodesAtMaxDepth(Node root,
                                    int level)
    {
        if (root == null)
            return;

        // If the current level exceeds the
        // maximum level, update the max_level
        // as current level.
        if (level > max_level)
        {
            sum = root.data;
            max_level = level;
        }

        // If the max level and current level
        // are same, add the root data to
        // current sum.
        else if (level == max_level)
        {
            sum = sum + root.data;
        }

        // Traverse the left and right subtrees
        sumOfNodesAtMaxDepth(root.left, level + 1);
        sumOfNodesAtMaxDepth(root.right, level + 1);
    }

    // Driver Code
    public static void Main()
    {
        Node root = null;
        root = createNode(1);
        root.left = createNode(2);
        root.right = createNode(3);
        root.left.left = createNode(4);
        root.left.right = createNode(5);
        root.right.left = createNode(6);
        root.right.right = createNode(7);

        sumOfNodesAtMaxDepth(root, 0);
        Console.WriteLine(sum);
    }
}

/* This code is contributed PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript Program to find sum of nodes at maximum
    // Depth of the Binary Tree

    // Variables to store sum and
    // maximum level
    let sum = 0;
    let max_level = Number.MIN_VALUE;

    // Binary Tree Node
    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.data = val;
        }
    }

    // Utility function to create and
    // return a new Binary Tree Node
    function createNode(val)
    {

        let node = new Node(val);
        return node;
    }

    // Function to find the sum of
    // the node which are present
    // at the maximum depth
    function sumOfNodesAtMaxDepth(root, level)
    {
        if (root == null)
            return;

        // If the current level exceeds the
        // maximum level, update the max_level
        // as current level.
        if (level > max_level)
        {
            sum = root.data;
            max_level = level;
        }

        // If the max level and current level
        // are same, add the root data to
        // current sum.
        else if (level == max_level)
        {
            sum = sum + root.data;
        }

        // Traverse the left and right subtrees
        sumOfNodesAtMaxDepth(root.left, level + 1);
        sumOfNodesAtMaxDepth(root.right, level + 1);
    }

    let root = null;
    root = createNode(1);
    root.left = createNode(2);
    root.right = createNode(3);
    root.left.left = createNode(4);
    root.left.right = createNode(5);
    root.right.left = createNode(6);
    root.right.right = createNode(7);

    sumOfNodesAtMaxDepth(root, 0);
    document.write(sum);

</script>
```

**Output:** 

```
22
```

**时间复杂度** : O(N)，其中 N 为二叉树中的顶点数。
**辅助空间** : O(N)。