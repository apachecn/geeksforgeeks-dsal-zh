# 二叉树各层最大值|集合-2(迭代方法)

> 原文:[https://www . geesforgeks . org/最大值-级别-二叉树-集合-2-迭代-方法/](https://www.geeksforgeeks.org/largest-value-level-binary-tree-set-2-iterative-approach/)

给定一个包含 **n 个**节点的二叉树。问题是找到并打印每个级别中存在的最大值。
**例:**

```
Input :
        1
       / \
      2   3 
Output : 1 3

Input : 
        4
       / \
      9   2
     / \   \
    3   5   7 
Output : 4 9 7
```

**方法:**在[之前的帖子](https://www.geeksforgeeks.org/largest-value-level-binary-tree/)中，已经讨论了递归方法。这篇文章讨论了一种迭代方法。其思想是使用队列执行二叉树的[迭代级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。遍历时，保留 **max** 变量，该变量存储正在处理的树的当前级别的最大元素。当水平完全通过时，打印该**最大**值。

## C++

```
// C++ implementation to print largest
// value in each level of Binary Tree
#include <bits/stdc++.h>

using namespace std;

// structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// function to get a new node
Node* newNode(int data)
{
    // allocate space
    Node* temp = new Node;

    // put in the data
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// function to print largest value
// in each level of Binary Tree
void largestValueInEachLevel(Node* root)
{
    // if tree is empty
    if (!root)
        return;

    queue<Node*> q;
    int nc, max;

    // push root to the queue 'q'
    q.push(root);

    while (1) {
        // node count for the current level
        nc = q.size();

        // if true then all the nodes of
        // the tree have been traversed
        if (nc == 0)
            break;

        // maximum element for the current
        // level
        max = INT_MIN;

        while (nc--) {

            // get the front element from 'q'
            Node* front = q.front();

            // remove front element from 'q'
            q.pop();

            // if true, then update 'max'
            if (max < front->data)
                max = front->data;

            // if left child exists
            if (front->left)
                q.push(front->left);

            // if right child exists
            if (front->right)
                q.push(front->right);
        }

        // print maximum element of
        // current level
        cout << max << " ";
    }
}

// Driver code
int main()
{
    /* Construct a Binary Tree
        4
       / \
      9   2
     / \   \
    3   5   7 */

    Node* root = NULL;
    root = newNode(4);
    root->left = newNode(9);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->right = newNode(7);

    // Function call
    largestValueInEachLevel(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print largest
// value in each level of Binary Tree
import java.util.*;
class GfG {

    // structure of a node of binary tree
    static class Node
    {
        int data;
        Node left = null;
        Node right = null;
    }

    // function to get a new node
    static Node newNode(int val)
    {
        // allocate space
        Node temp = new Node();

        // put in the data
        temp.data = val;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // function to print largest value
    // in each level of Binary Tree
    static void largestValueInEachLevel(Node root)
    {
        // if tree is empty
        if (root == null)
            return;

        Queue<Node> q = new LinkedList<Node>();
        int nc, max;

        // push root to the queue 'q'
        q.add(root);

        while (true)
        {
            // node count for the current level
            nc = q.size();

            // if true then all the nodes of
            // the tree have been traversed
            if (nc == 0)
                break;

            // maximum element for the current
            // level
            max = Integer.MIN_VALUE;

            while (nc != 0)
            {

                // get the front element from 'q'
                Node front = q.peek();

                // remove front element from 'q'
                q.remove();

                // if true, then update 'max'
                if (max < front.data)
                    max = front.data;

                // if left child exists
                if (front.left != null)
                    q.add(front.left);

                // if right child exists
                if (front.right != null)
                    q.add(front.right);
                nc--;
            }

            // print maximum element of
            // current level
            System.out.println(max + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        /* Construct a Binary Tree
            4
        / \
        9 2
        / \ \
        3 5 7 */

        Node root = null;
        root = newNode(4);
        root.left = newNode(9);
        root.right = newNode(2);
        root.left.left = newNode(3);
        root.left.right = newNode(5);
        root.right.right = newNode(7);

        // Function call
        largestValueInEachLevel(root);
    }
}
```

## 蟒蛇 3

```
# Python program to print largest value
# on each level of binary tree

INT_MIN = -2147483648

# Helper function that allocates a new
# node with the given data and None left
# and right pointers.

class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to find largest values

def largestValueInEachLevel(root):
    if (not root):
        return
    q = []
    nc = 10
    max = 0
    q.append(root)
    while (1):
        # node count for the current level
        nc = len(q)

        # if true then all the nodes of
        # the tree have been traversed
        if (nc == 0):
            break

        # maximum element for the current
        # level
        max = INT_MIN
        while (nc):

            # get the front element from 'q'
            front = q[0]

            # remove front element from 'q'
            q = q[1:]

            # if true, then update 'max'
            if (max < front.data):
                max = front.data

            # if left child exists
            if (front.left):
                q.append(front.left)

            # if right child exists
            if (front.right != None):
                q.append(front.right)
            nc -= 1

        # print maximum element of
        # current level
        print(max, end=" ")

# Driver Code
if __name__ == '__main__':
    """ Let us construct the following Tree
        4
        / \
        9 2
    / \ \
    3 5 7 """
    root = newNode(4)
    root.left = newNode(9)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.right = newNode(7)

    # Function call
    largestValueInEachLevel(root)

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation to print largest
// value in each level of Binary Tree
using System;
using System.Collections.Generic;

class GfG
{

    // structure of a node of binary tree
    class Node
    {
        public int data;
        public Node left = null;
        public Node right = null;
    }

    // function to get a new node
    static Node newNode(int val)
    {
        // allocate space
        Node temp = new Node();

        // put in the data
        temp.data = val;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // function to print largest value
    // in each level of Binary Tree
    static void largestValueInEachLevel(Node root)
    {
        // if tree is empty
        if (root == null)
            return;

        Queue<Node> q = new Queue<Node>();
        int nc, max;

        // push root to the queue 'q'
        q.Enqueue(root);

        while (true)
        {
            // node count for the current level
            nc = q.Count;

            // if true then all the nodes of
            // the tree have been traversed
            if (nc == 0)
                break;

            // maximum element for the current
            // level
            max = int.MinValue;

            while (nc != 0)
            {
                // get the front element from 'q'
                Node front = q.Peek();

                // remove front element from 'q'
                q.Dequeue();

                // if true, then update 'max'
                if (max < front.data)
                    max = front.data;

                // if left child exists
                if (front.left != null)
                    q.Enqueue(front.left);

                // if right child exists
                if (front.right != null)
                    q.Enqueue(front.right);
                nc--;
            }

            // print maximum element of
            // current level
            Console.Write(max + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        /* Construct a Binary Tree
            4
        / \
        9 2
        / \ \
        3 5 7 */

        Node root = null;
        root = newNode(4);
        root.left = newNode(9);
        root.right = newNode(2);
        root.left.left = newNode(3);
        root.left.right = newNode(5);
        root.right.right = newNode(7);

        // Function call
        largestValueInEachLevel(root);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation to print largest
    // value in each level of Binary Tree

    // structure of a node of binary tree
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to get a new node
    function newNode(val)
    {
        // allocate space
        let temp = new Node(val);
        return temp;
    }

    // function to print largest value
    // in each level of Binary Tree
    function largestValueInEachLevel(root)
    {
        // if tree is empty
        if (root == null)
            return;

        let q = [];
        let nc, max;

        // push root to the queue 'q'
        q.push(root);

        while (true)
        {
            // node count for the current level
            nc = q.length;

            // if true then all the nodes of
            // the tree have been traversed
            if (nc == 0)
                break;

            // maximum element for the current
            // level
            max = Number.MIN_VALUE;

            while (nc != 0)
            {

                // get the front element from 'q'
                let front = q[0];

                // remove front element from 'q'
                q.shift();

                // if true, then update 'max'
                if (max < front.data)
                    max = front.data;

                // if left child exists
                if (front.left != null)
                    q.push(front.left);

                // if right child exists
                if (front.right != null)
                    q.push(front.right);
                nc--;
            }

            // print maximum element of
            // current level
            document.write(max + " ");
        }
    }

    /* Construct a Binary Tree
           4
          / \
          9 2
          / \ \
          3 5 7 */

    let root = null;
    root = newNode(4);
    root.left = newNode(9);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    // Function call
    largestValueInEachLevel(root);

</script>
```

**Output**

```
4 9 7 
```