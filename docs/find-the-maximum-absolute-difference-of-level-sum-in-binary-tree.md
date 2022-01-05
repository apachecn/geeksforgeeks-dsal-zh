# 二叉树中任意两级和的最大绝对差

> 原文:[https://www . geeksforgeeks . org/find-二进制树中级别和的最大绝对差/](https://www.geeksforgeeks.org/find-the-maximum-absolute-difference-of-level-sum-in-binary-tree/)

给定一个有正负节点的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找出其中水平和的最大绝对差。

**示例:**

```
Input:                     
       4
     /   \
    2    -5
  /  \   / \
-1    3 -2  6
Output: 9
Explanation: 
Sum of all nodes of 0 level is 4
Sum of all nodes of 1 level is -3
Sum of all nodes of 2 level is 6
Hence maximum absolute difference
of level sum = 9 (6 - (-3))

Input: 
        1
      /   \
     2     3
   /  \     \
  4    5     8
            / \
           6   7
Output: 16
```

**逼近:**求水平和的最大绝对差，我们只需要求**最大水平和**和**最小水平和**，因为最大和最小水平和的绝对差总是给我们最大绝对差，即

> 最大绝对差值=绝对值(最大水平总和–最小水平总和)

以下是上述观察的算法步骤:

1.  思路是做[级顺序遍历树](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
2.  遍历时，分别处理不同级别的节点。
3.  对于正在处理的每个级别，计算级别中节点的[和，并跟踪**最大**和**最小**级别和。](https://www.geeksforgeeks.org/sum-nodes-k-th-level-tree-represented-string/)
4.  然后返回最大和最小电平和的**绝对差**。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum
// absolute difference of level
// sum in Binary Tree
#include <bits/stdc++.h>
using namespace std;

// Class containing left and
// right child of current
// node and key value
struct Node
{
    int data;
    Node *left, *right;
};

Node *newNode(int data)
{
    Node *node = new Node();
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}

// Function to find the maximum
// absolute difference of level
// sum in binary tree
// using level order traversal
int maxAbsDiffLevelSum(Node *root)
{

    // Initialize value of maximum
    // and minimum level sum
    int maxsum = INT_MIN;
    int minsum = INT_MAX;

    queue<Node *> qu;
    qu.push(root);

    // Do Level order traversal
    // keeping track of number
    // of nodes at every level.
    while (!qu.empty())
    {

        // Get the size of queue when
        // the level order traversal
        // for one level finishes
        int sz = qu.size();

        // Iterate for all the nodes in
        // the queue currently
        int sum = 0;

        for(int i = 0; i < sz; i++)
        {

            // Dequeue an node from queue
            Node *t = qu.front();
            qu.pop();

            // Add this node's value to
            // the current sum.
            sum += t->data;

            // Enqueue left and
            // right children of
            // dequeued node
            if (t->left != NULL)
                qu.push(t->left);

            if (t->right != NULL)
                qu.push(t->right);
        }

        // Update the maximum
        // level sum value
        maxsum = max(maxsum, sum);

        // Update the minimum
        // level sum value
        minsum = min(minsum, sum);
    }

    // return the maximum absolute
    // difference of level sum
    return abs(maxsum - minsum);
}

// Driver code
int main()
{
    Node *root = new Node();

    root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(-5);
    root->left->left = newNode(-1);
    root->left->right = newNode(3);
    root->right->left = newNode(-2);
    root->right->right = newNode(6);

    /*   Constructed Binary tree is:
        4
      /   \
    2      -5
    /  \     / \
    -1    3  -2   6 */

    cout << maxAbsDiffLevelSum(root) << endl;
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// absolute difference of level
// sum in Binary Tree

import java.util.*;

// Class containing left and
// right child of current
// node and key value
class Node {

    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {

    // Root of the Binary Tree
    Node root;

    public BinaryTree()
    {
        root = null;
    }

    // Function to find
    // the maximum absolute
    // difference of level
    // sum in binary tree
    // using level order traversal
    public int maxAbsDiffLevelSum()
    {

        // Initialize value of maximum
        // and minimum level sum
        int maxsum = Integer.MIN_VALUE;
        int minsum = Integer.MAX_VALUE;

        Queue<Node> qu = new LinkedList<>();
        qu.offer(root);

        // Do Level order traversal
        // keeping track of number
        // of nodes at every level.
        while (!qu.isEmpty()) {

            // Get the size of queue when
            // the level order traversal
            // for one level finishes
            int sz = qu.size();

            // Iterate for all the nodes in
            // the queue currently
            int sum = 0;

            for (int i = 0; i < sz; i++) {

                // Dequeue an node from queue
                Node t = qu.poll();

                // Add this node's value to
                // the current sum.
                sum += t.data;

                // Enqueue left and
                // right children of
                // dequeued node
                if (t.left != null)
                    qu.offer(t.left);

                if (t.right != null)
                    qu.offer(t.right);
            }

            // Update the maximum
            // level sum value
            maxsum = Math.max(maxsum, sum);

            // Update the minimum
            // level sum value
            minsum = Math.min(minsum, sum);
        }
        // return the maximum absolute
        // difference of level sum
        return Math.abs(maxsum - minsum);
    }

    // Driver code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(4);
        tree.root.left = new Node(2);
        tree.root.right = new Node(-5);
        tree.root.left.left = new Node(-1);
        tree.root.left.right = new Node(3);
        tree.root.right.left = new Node(-2);
        tree.root.right.right = new Node(6);

        /*   Constructed Binary tree is:
              4
            /   \
          2      -5
        /  \     / \
      -1    3  -2   6 */

        System.out.println(
            tree.maxAbsDiffLevelSum());
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# the maximum absolute difference
# of level sum in Binary Tree

import sys
# Class containing left and
# right child of current
# node and key value

class newNode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to find the maximum
# absolute difference of level
# sum in binary tree
# using level order traversal
def maxAbsDiffLevelSum(root):

    # Initialize value of maximum
    # and minimum level sum
    maxsum = -sys.maxsize - 1
    minsum = sys.maxsize

    qu = []
    qu.append(root)

    # Do Level order traversal
    # keeping track of number
    # of nodes at every level.
    while (len(qu) > 0):

        # Get the size of queue when
        # the level order traversal
        # for one level finishes
        sz = len(qu)

        # Iterate for all the nodes in
        # the queue currently
        sum = 0

        for i in range(sz):

            # Dequeue an node from
            # queue
            t = qu[0]
            qu.remove(qu[0])

            # Add this node's value
            # to the current sum.
            sum += t.data

            # Enqueue left and
            # right children of
            # dequeued node
            if (t.left != None):
                qu.append(t.left)

            if (t.right != None):
                qu.append(t.right)

        # Update the maximum
        # level sum value
        maxsum = max(maxsum, sum)

        # Update the minimum
        # level sum value
        minsum = min(minsum, sum)

    # return the maximum absolute
    # difference of level sum
    return abs(maxsum - minsum)

# Driver code
if __name__ == '__main__':

    root = newNode(4)
    root.left = newNode(2)
    root.right = newNode(-5)
    root.left.left = newNode(-1)
    root.left.right = newNode(3)
    root.right.left = newNode(-2)
    root.right.right = newNode(6)

    '''/*   Constructed Binary tree is:
        4
      /   \
    2      -5
    / /     / \
    -1    3  -2   6 */
    '''

    print(maxAbsDiffLevelSum(root))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to find the maximum
// absolute difference of level
// sum in Binary Tree
using System;
using System.Collections.Generic;

// Class to represent Tree node
public class Node 
{
    public int data;
    public Node left, right;

    public Node(int item) 
    {
        data = item;
        left = null;
        right = null;
    }
}

class BinaryTree{

Node root;

// Function to find the maximum
// absolute difference of level
// sum in binary tree
// using level order traversal
public int maxAbsDiffLevelSum()
{

    // Initialize value of maximum
    // and minimum level sum
    int maxsum = Int32.MinValue;
    int minsum = Int32.MaxValue;

    Queue<Node> qu = new Queue<Node>();
    qu.Enqueue(root);

    // Do Level order traversal
    // keeping track of number
    // of nodes at every level.
    while (qu.Count != 0)
    {

        // Get the size of queue when
        // the level order traversal
        // for one level finishes
        int sz = qu.Count;

        // Iterate for all the nodes in
        // the queue currently
        int sum = 0;

        for(int i = 0; i < sz; i++)
        {

            // Dequeue an node from queue
            Node t = qu.Dequeue();

            // Add this node's value to
            // the current sum.
            sum += t.data;

            // Enqueue left and
            // right children of
            // dequeued node
            if (t.left != null)
                qu.Enqueue(t.left);

            if (t.right != null)
                qu.Enqueue(t.right);
        }

        // Update the maximum
        // level sum value
        maxsum = Math.Max(maxsum, sum);

        // Update the minimum
        // level sum value
        minsum = Math.Min(minsum, sum);
    }

    // Return the maximum absolute
    // difference of level sum
    return Math.Abs(maxsum - minsum);
}

// Driver code
static public void Main ()
{
    BinaryTree tree = new BinaryTree();

    tree.root = new Node(4);
    tree.root.left = new Node(2);
    tree.root.right = new Node(-5);
    tree.root.left.left = new Node(-1);
    tree.root.left.right = new Node(3);
    tree.root.right.left = new Node(-2);
    tree.root.right.right = new Node(6);

    /*   Constructed Binary tree is:
          4
        /   \
      2      -5
    /  \     / \
  -1    3  -2   6 */

   Console.WriteLine(tree.maxAbsDiffLevelSum());
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
    // Javascript program to find the maximum
    // absolute difference of level
    // sum in Binary Tree

    // Class to represent Tree node
    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root;

    // Function to find the maximum
    // absolute difference of level
    // sum in binary tree
    // using level order traversal
    function maxAbsDiffLevelSum()
    {

        // Initialize value of maximum
        // and minimum level sum
        let maxsum = Number.MIN_VALUE;
        let minsum = Number.MAX_VALUE;

        let qu = [];
        qu.push(root);

        // Do Level order traversal
        // keeping track of number
        // of nodes at every level.
        while (qu.length != 0)
        {

            // Get the size of queue when
            // the level order traversal
            // for one level finishes
            let sz = qu.length;

            // Iterate for all the nodes in
            // the queue currently
            let sum = 0;

            for(let i = 0; i < sz; i++)
            {

                // Dequeue an node from queue
                let t = qu.shift();

                // Add this node's value to
                // the current sum.
                sum += t.data;

                // Enqueue left and
                // right children of
                // dequeued node
                if (t.left != null)
                    qu.push(t.left);

                if (t.right != null)
                    qu.push(t.right);
            }

            // Update the maximum
            // level sum value
            maxsum = Math.max(maxsum, sum);

            // Update the minimum
            // level sum value
            minsum = Math.min(minsum, sum);
        }

        // Return the maximum absolute
        // difference of level sum
        return Math.abs(maxsum - minsum);
    }

    root = new Node(4);
    root.left = new Node(2);
    root.right = new Node(-5);
    root.left.left = new Node(-1);
    root.left.right = new Node(3);
    root.right.left = new Node(-2);
    root.right.right = new Node(6);

    /*   Constructed Binary tree is:
            4
          /   \
        2      -5
      /  \     / \
    -1    3  -2   6 */

      document.write(maxAbsDiffLevelSum());

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)