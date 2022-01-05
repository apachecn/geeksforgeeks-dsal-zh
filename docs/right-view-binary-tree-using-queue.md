# 使用队列的二叉树右视图

> 原文:[https://www . geesforgeks . org/right-view-二叉树-use-queue/](https://www.geeksforgeeks.org/right-view-binary-tree-using-queue/)

给定一个二叉树，打印它的右视图。二叉树的右视图是从右侧访问树时可见的一组节点。
**例:**

```
Input : 
              10
            /     \
          2         3
        /   \    /    \
       7     8  12     15
                      /
                    14
Output : 10 3 15 14
The output nodes are the rightmost
nodes of their respective levels.
```

我们已经讨论了右视图的[递归解。本文讨论了基于](https://www.geeksforgeeks.org/print-right-view-binary-tree-2/)[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)的解决方案。
如果我们仔细观察，会发现我们的主要任务是打印每一级最右边的节点。因此，我们将在树上进行级别顺序遍历，并在每个级别打印最右边的节点。
以下是上述方法的实施:

## C++

```
// C++ program to print right view of
// Binary Tree

#include<bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// function to print right view of
// binary tree
void printRightView(Node* root)
{
    if (!root)
        return;

    queue<Node*> q;
    q.push(root);

    while (!q.empty())
    {   
        // number of nodes at current level
        int n = q.size();

        // Traverse all nodes of current level
        for(int i = 1; i <= n; i++)
        {
            Node* temp = q.front();
            q.pop();

            // Print the right most element
            // at the level
            if (i == n)
                cout<<temp->data<<" ";

            // Add left node to queue
            if (temp->left != NULL)
                q.push(temp->left);

            // Add right node to queue
            if (temp->right != NULL)
                q.push(temp->right);
        }
    }
}   

// Driver program to test above functions
int main()
{
    // Let's construct the tree as
    // shown in example

    Node* root = newNode(10);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(7);
    root->left->right = newNode(8);
    root->right->right = newNode(15);
    root->right->left = newNode(12);
    root->right->right->left = newNode(14);

    printRightView(root);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print right view of Binary
// Tree
import java.util.*;

public class PrintRightView
{  
    // Binary tree node
    private static class Node
    {
        int data;
        Node left, right;

        public Node(int data) {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    // function to print right view of binary tree
    private static void printRightView(Node root)
    {
        if (root == null)
            return;

        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty())
        {  
            // number of nodes at current level
            int n = queue.size();

            // Traverse all nodes of current level
            for (int i = 1; i <= n; i++) {
                Node temp = queue.poll();

                // Print the right most element at
                // the level
                if (i == n)
                    System.out.print(temp.data + " ");

                // Add left node to queue
                if (temp.left != null)
                    queue.add(temp.left);

                // Add right node to queue
                if (temp.right != null)
                    queue.add(temp.right);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // construct binary tree as shown in
        // above diagram
        Node root = new Node(10);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(7);
        root.left.right = new Node(8);
        root.right.right = new Node(15);
        root.right.left = new Node(12);
        root.right.right.left = new Node(14);

        printRightView(root);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print right view of
# Binary Tree

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None
        self.hd = 0

# function to print right view of
# binary tree
def printRightView(root):

    if (not root):
        return

    q = []
    q.append(root)

    while (len(q)):

        # number of nodes at current level
        n = len(q)

        # Traverse all nodes of current level
        for i in range(1, n + 1):        
            temp = q[0]
            q.pop(0)

            # Print the right most element
            # at the level
            if (i == n) :
                print(temp.data, end = " " )

            # Add left node to queue
            if (temp.left != None) :
                q.append(temp.left)

            # Add right node to queue
            if (temp.right != None) :
                q.append(temp.right)

# Driver Code
if __name__ == '__main__':

    root = newNode(10)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(7)
    root.left.right = newNode(8)
    root.right.right = newNode(15)
    root.right.left = newNode(12)
    root.right.right.left = newNode(14)
    printRightView(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to print right view
// of Binary Tree
using System;
using System.Collections.Generic;

public class PrintRightView
{
    // Binary tree node
    private class Node
    {
        public int data;
        public Node left, right;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    // function to print right view of binary tree
    private static void printRightView(Node root)
    {
        if (root == null)
            return;

        Queue<Node> queue = new Queue<Node>();
        queue.Enqueue(root);

        while (queue.Count != 0)
        {
            // number of nodes at current level
            int n = queue.Count;

            // Traverse all nodes of current level
            for (int i = 1; i <= n; i++)
            {
                Node temp = queue.Dequeue();

                // Print the right most element at
                // the level
                if (i == n)
                    Console.Write(temp.data + " ");

                // Add left node to queue
                if (temp.left != null)
                    queue.Enqueue(temp.left);

                // Add right node to queue
                if (temp.right != null)
                    queue.Enqueue(temp.right);
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // construct binary tree as shown in
        // above diagram
        Node root = new Node(10);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(7);
        root.left.right = new Node(8);
        root.right.right = new Node(15);
        root.right.left = new Node(12);
        root.right.right.left = new Node(14);
        printRightView(root);
    }
}

// This code is contributed 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to print right view
// of Binary Tree
// Binary tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// function to print right view of binary tree
function printRightView(root)
{
    if (root == null)
        return;

    var queue = [];
    queue.push(root);

    while (queue.length != 0)
    {
        // number of nodes at current level
        var n = queue.length;

        // Traverse all nodes of current level
        for (var i = 1; i <= n; i++)
        {
            var temp = queue.shift();

            // Print the right most element at
            // the level
            if (i == n)
                document.write(temp.data + " ");

            // Add left node to queue
            if (temp.left != null)
                queue.push(temp.left);

            // Add right node to queue
            if (temp.right != null)
                queue.push(temp.right);
        }
    }
}
// Driver code
// construct binary tree as shown in
// above diagram
var root = new Node(10);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(7);
root.left.right = new Node(8);
root.right.right = new Node(15);
root.right.left = new Node(12);
root.right.right.left = new Node(14);
printRightView(root);

</script>
```

**输出:**

```
10 3 15 14
```

**时间复杂度** : O( n)，其中 n 为二叉树中的节点数。

**辅助空间:** O( n)为队列数据结构

？list = plqm 7 alhxfyshcxd 7r 1j0ky 9 ZG _ gbb 1 dbk〖t0〗]

本文由**bibas Abhishek**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。