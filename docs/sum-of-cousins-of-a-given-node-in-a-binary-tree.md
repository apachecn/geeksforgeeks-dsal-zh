# 二叉树中给定节点的同类之和

> 原文:[https://www . geesforgeks . org/二叉树中给定节点的表亲之和/](https://www.geeksforgeeks.org/sum-of-cousins-of-a-given-node-in-a-binary-tree/)

给定二叉树和节点的数据值。任务是找到给定节点的表亲节点的和。如果给定节点没有表亲，则返回-1。
**注:**假设所有节点都有不同的值，并且给定的节点存在于树中。
示例:

```
Input: 
                1
              /  \
             3    7
           /  \  / \
          6   5  4  13
             /  / \
            10 17 15
         key = 13
Output: 11
Cousin nodes are 5 and 6 which gives sum 11\. 

Input:
                1
              /  \
             3    7
           /  \  / \
          6   5  4  13
             /  / \
            10 17 15
           key = 7
Output: -1
No cousin nodes of node having value 7.
```

**方法:**方法是对树进行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。在执行级别顺序遍历时，查找下一级的子节点之和。将子节点的值添加到总和中，并检查子节点是否是目标节点。如果是，则不要将任何一个子代的值添加到总和中。遍历当前层级后，如果目标节点出现在下一层级，则结束层级顺序遍历，找到的和即为表亲节点的和。
以下是上述方法的实施:

## C++

```
// CPP program to find sum of cousins
// of given node in binary tree.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new
// Binary Tree Node
struct Node* newNode(int item)
{
    struct Node* temp = new Node();
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find sum of cousins of
// a given node.
int findCousinSum(Node* root, int key)
{
    if (root == NULL)
        return -1;

    // Root node has no cousins so return -1.
    if (root->data == key) {
        return -1;
    }

    // To store sum of cousins.
    int currSum = 0;

    // To store size of current level.
    int size;

    // To perform level order traversal.
    queue<Node*> q;
    q.push(root);

    // To represent that target node is
    // found.
    bool found = false;

    while (!q.empty()) {

        // If target node is present at
        // current level, then return
        // sum of cousins stored in currSum.
        if (found == true) {
            return currSum;
        }

        // Find size of current level and
        // traverse entire level.
        size = q.size();
        currSum = 0;

        while (size) {
            root = q.front();
            q.pop();

            // Check if either of the existing
            // children of given node is target
            // node or not. If yes then set
            // found equal to true.
            if ((root->left && root->left->data == key)
                || (root->right && root->right->data == key)) {
                found = true;
            }

            // If target node is not children of
            // current node, then its childeren can be cousin
            // of target node, so add their value to sum.
            else {
                if (root->left) {
                    currSum += root->left->data;
                    q.push(root->left);
                }

                if (root->right) {
                    currSum += root->right->data;
                    q.push(root->right);
                }
            }

            size--;
        }
    }

    return -1;
}

// Driver Code
int main()
{
    /*
                1
              /  \
             3    7
           /  \  / \
          6   5  4  13
             /  / \
            10 17 15
    */

    struct Node* root = newNode(1);
    root->left = newNode(3);
    root->right = newNode(7);
    root->left->left = newNode(6);
    root->left->right = newNode(5);
    root->left->right->left = newNode(10);
    root->right->left = newNode(4);
    root->right->right = newNode(13);
    root->right->left->left = newNode(17);
    root->right->left->right = newNode(15);

    cout << findCousinSum(root, 13) << "\n";

    cout << findCousinSum(root, 7) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of cousins
// of given node in binary tree.
import java.util.*;
class Sol
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// A utility function to create a new
// Binary Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find sum of cousins of
// a given node.
static int findCousinSum(Node root, int key)
{
    if (root == null)
        return -1;

    // Root node has no cousins so return -1.
    if (root.data == key)
    {
        return -1;
    }

    // To store sum of cousins.
    int currSum = 0;

    // To store size of current level.
    int size;

    // To perform level order traversal.
    Queue<Node> q=new LinkedList<Node>();
    q.add(root);

    // To represent that target node is
    // found.
    boolean found = false;

    while (q.size() > 0)
    {

        // If target node is present at
        // current level, then return
        // sum of cousins stored in currSum.
        if (found == true)
        {
            return currSum;
        }

        // Find size of current level and
        // traverse entire level.
        size = q.size();
        currSum = 0;

        while (size > 0)
        {
            root = q.peek();
            q.remove();

            // Check if either of the existing
            // children of given node is target
            // node or not. If yes then set
            // found equal to true.
            if ((root.left!=null && root.left.data == key)
                || (root.right!=null && root.right.data == key))
            {
                found = true;
            }

            // If target node is not children of
            // current node, then its childeren can be cousin
            // of target node, so add their value to sum.
            else
            {
                if (root.left != null)
                {
                    currSum += root.left.data;
                    q.add(root.left);
                }

                if (root.right != null)
                {
                    currSum += root.right.data;
                    q.add(root.right);
                }
            }

            size--;
        }
    }

    return -1;
}

// Driver Code
public static void main(String args[])
{
    /*
                1
            / \
            3 7
        / \ / \
        6 5 4 13
            / / \
            10 17 15
    */

    Node root = newNode(1);
    root.left = newNode(3);
    root.right = newNode(7);
    root.left.left = newNode(6);
    root.left.right = newNode(5);
    root.left.right.left = newNode(10);
    root.right.left = newNode(4);
    root.right.right = newNode(13);
    root.right.left.left = newNode(17);
    root.right.left.right = newNode(15);

    System.out.print( findCousinSum(root, 13) + "\n");

    System.out.print( findCousinSum(root, 7) + "\n");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
""" Python3 program to find sum of cousins
of given node in binary tree """

# A Binary Tree Node
# Utility function to create a new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find sum of cousins of
# a given node.
def findCousinSum( root, key):

    if (root == None):
        return -1

    # Root node has no cousins so return -1.
    if (root.data == key):
        return -1

    # To store sum of cousins.
    currSum = 0

    # To store size of current level.
    size = 0

    # To perform level order traversal.
    q = []
    q.append(root)

    # To represent that target node is
    # found.
    found = False

    while (len(q)):

        # If target node is present at
        # current level, then return
        # sum of cousins stored in currSum.
        if (found == True):
            return currSum

        # Find size of current level and
        # traverse entire level.
        size = len(q)
        currSum = 0

        while (size):
            root = q[0]
            q.pop(0)

            # Check if either of the existing
            # children of given node is target
            # node or not. If yes then set
            # found equal to true.
            if ((root.left and root.left.data == key) or
                (root.right and root.right.data == key)) :
                found = True

            # If target node is not children of current
            # node, then its childeren can be cousin
            # of target node, so add their value to sum.
            else:
                if (root.left):
                    currSum += root.left.data
                    q.append(root.left)

                if (root.right) :
                    currSum += root.right.data
                    q.append(root.right)

            size -= 1
    return -1

# Driver Code
if __name__ == '__main__':

    """
                1
            / \
            3 7
        / \ / \
        6 5 4 13
            / / \
            10 17 15
    """
    root = newNode(1)
    root.left = newNode(3)
    root.right = newNode(7)
    root.left.left = newNode(6)
    root.left.right = newNode(5)
    root.left.right.left = newNode(10)
    root.right.left = newNode(4)
    root.right.right = newNode(13)
    root.right.left.left = newNode(17)
    root.right.left.right = newNode(15)

    print(findCousinSum(root, 13))

    print(findCousinSum(root, 7))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find sum of cousins
// of given node in binary tree.
using System;
using System.Collections.Generic;

class Sol
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
};

// A utility function to create a new
// Binary Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find sum of cousins of
// a given node.
static int findCousinSum(Node root, int key)
{
    if (root == null)
        return -1;

    // Root node has no cousins so return -1.
    if (root.data == key)
    {
        return -1;
    }

    // To store sum of cousins.
    int currSum = 0;

    // To store size of current level.
    int size;

    // To perform level order traversal.
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    // To represent that target node is
    // found.
    bool found = false;

    while (q.Count > 0)
    {

        // If target node is present at
        // current level, then return
        // sum of cousins stored in currSum.
        if (found == true)
        {
            return currSum;
        }

        // Find size of current level and
        // traverse entire level.
        size = q.Count;
        currSum = 0;

        while (size > 0)
        {
            root = q.Peek();
            q.Dequeue();

            // Check if either of the existing
            // children of given node is target
            // node or not. If yes then set
            // found equal to true.
            if ((root.left != null && root.left.data == key)
                || (root.right != null && root.right.data == key))
            {
                found = true;
            }

            // If target node is not children of
            // current node, then its childeren can be cousin
            // of target node, so add their value to sum.
            else
            {
                if (root.left != null)
                {
                    currSum += root.left.data;
                    q.Enqueue(root.left);
                }

                if (root.right != null)
                {
                    currSum += root.right.data;
                    q.Enqueue(root.right);
                }
            }

            size--;
        }
    }

    return -1;
}

// Driver Code
public static void Main(String []args)
{
    /*
                1
            / \
            3 7
        / \ / \
        6 5 4 13
            / / \
            10 17 15
    */

    Node root = newNode(1);
    root.left = newNode(3);
    root.right = newNode(7);
    root.left.left = newNode(6);
    root.left.right = newNode(5);
    root.left.right.left = newNode(10);
    root.right.left = newNode(4);
    root.right.right = newNode(13);
    root.right.left.left = newNode(17);
    root.right.left.right = newNode(15);

    Console.Write( findCousinSum(root, 13) + "\n");

    Console.Write( findCousinSum(root, 7) + "\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find sum of cousins
// of given node in binary tree.

// A Binary Tree Node
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
};

// A utility function to create a new
// Binary Tree Node
function newNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find sum of cousins of
// a given node.
function findCousinSum(root, key)
{
    if (root == null)
        return -1;

    // Root node has no cousins so return -1.
    if (root.data == key)
    {
        return -1;
    }

    // To store sum of cousins.
    var currSum = 0;

    // To store size of current level.
    var size;

    // To perform level order traversal.
    var q = [];
    q.push(root);

    // To represent that target node is
    // found.
    var found = false;

    while (q.length > 0)
    {

        // If target node is present at
        // current level, then return
        // sum of cousins stored in currSum.
        if (found == true)
        {
            return currSum;
        }

        // Find size of current level and
        // traverse entire level.
        size = q.length;
        currSum = 0;

        while (size > 0)
        {
            root = q[0];
            q.shift();

            // Check if either of the existing
            // children of given node is target
            // node or not. If yes then set
            // found equal to true.
            if ((root.left != null && root.left.data == key)
                || (root.right != null && root.right.data == key))
            {
                found = true;
            }

            // If target node is not children of
            // current node, then its childeren can be cousin
            // of target node, so add their value to sum.
            else
            {
                if (root.left != null)
                {
                    currSum += root.left.data;
                    q.push(root.left);
                }

                if (root.right != null)
                {
                    currSum += root.right.data;
                    q.push(root.right);
                }
            }

            size--;
        }
    }

    return -1;
}

// Driver Code
/*
            1
        / \
        3 7
    / \ / \
    6 5 4 13
        / / \
        10 17 15
*/
var root = newNode(1);
root.left = newNode(3);
root.right = newNode(7);
root.left.left = newNode(6);
root.left.right = newNode(5);
root.left.right.left = newNode(10);
root.right.left = newNode(4);
root.right.right = newNode(13);
root.right.left.left = newNode(17);
root.right.left.right = newNode(15);
document.write( findCousinSum(root, 13) + "<br>");
document.write( findCousinSum(root, 7) + "<br>");

</script>
```

**Output:** 

```
11
-1
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)