# 删除整个二叉树的非递归程序

> 原文:[https://www . geesforgeks . org/非递归程序删除整棵二叉树/](https://www.geeksforgeeks.org/non-recursive-program-to-delete-an-entire-binary-tree/)

我们已经讨论了删除整个二叉树的递归实现[这里](https://www.geeksforgeeks.org/write-a-c-program-to-delete-a-tree/)。
**我们强烈建议你尽量减少浏览器，先自己试试这个。**
现在如何不用递归删除整棵树。借助[级序树遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/) **可以很容易地做到这一点。**想法是对于队列中每个出列的节点，在对其左右节点(如果有)进行排队后将其删除。该解决方案将在我们从上到下逐级遍历树的所有节点时起作用，并且在删除父节点之前，我们将其子节点存储到稍后将被删除的队列中。

## C++

```
/* Non-Recursive Program to delete an entire binary tree. */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

/* Non-recursive function to delete an entire binary tree. */
void _deleteTree(Node *root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue for level order traversal
    queue<Node *> q;

    // Do level order traversal starting from root
    q.push(root);
    while (!q.empty())
    {
        Node *node = q.front();
        q.pop();

        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);

        free(node);
    }
}

/* Deletes a tree and sets the root as NULL */
void deleteTree(Node** node_ref)
{
  _deleteTree(*node_ref);
  *node_ref = NULL;
}

// Utility function to create a new tree Node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Driver program to test above functions
int main()
{
    // create a binary tree
    Node *root =  newNode(15);
    root->left = newNode(10);
    root->right = newNode(20);
    root->left->left = newNode(8);
    root->left->right = newNode(12);
    root->right->left = newNode(16);
    root->right->right = newNode(25);

    //delete entire binary tree
    deleteTree(&root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Non-recursive program to delete the entire binary tree */
import java.util.*;

// A binary tree node
class Node
{
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* Non-recursive function to delete an entire binary tree. */
    void _deleteTree()
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue for level order traversal
        Queue<Node> q = new LinkedList<Node>();

        // Do level order traversal starting from root
        q.add(root);
        while (!q.isEmpty())
        {
            Node node = q.peek();
            q.poll();

            if (node.left != null)
                q.add(node.left);
            if (node.right != null)
                q.add(node.right);
        }
    }

    /* Deletes a tree and sets the root as NULL */
    void deleteTree()
    {
        _deleteTree();
        root = null;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        // create a binary tree
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(15);
        tree.root.left = new Node(10);
        tree.root.right = new Node(20);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(12);
        tree.root.right.left = new Node(16);
        tree.root.right.right = new Node(25);

        // delete entire binary tree
        tree.deleteTree();
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 计算机编程语言

```
# Python program to delete an entire binary tree
# using non-recursive approach

# A binary tree node
class Node:

    # A constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Non-recursive function to delete an entrie binary tree
def _deleteTree(root):

    # Base Case
    if root is None:
        return

    # Create a empty queue for level order traversal
    q = []

    # Do level order traversal starting from root
    q.append(root)
    while(len(q)>0):
        node = q.pop(0)

        if node.left is not None:
            q.append(node.left)

        if node.right is not None:
            q.append(node.right)

        node = None
    return node

# Deletes a tree and sets the root as None
def deleteTree(node_ref):
    node_ref = _deleteTree(node_ref)
    return node_ref

# Driver program to test above function

# Create a binary tree
root = Node(15)
root.left = Node(10)
root.right = Node(20)
root.left.left = Node(8)
root.left.right = Node(12)
root.right.left = Node(16)
root.right.right = Node(25)

# delete entire binary tree
root = deleteTree(root)

# This program is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
/* Non-recursive program to delete the entire binary tree */
using System;
using System.Collections.Generic;

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

public class BinaryTree
{
    Node root;

    /* Non-recursive function to
    delete an entire binary tree. */
    void _deleteTree()
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue for level order traversal
        Queue<Node> q = new Queue<Node>();

        // Do level order traversal starting from root
        q.Enqueue(root);
        while (q.Count != 0)
        {
            Node node = q.Peek();
            q.Dequeue();

            if (node.left != null)
                q.Enqueue(node.left);
            if (node.right != null)
                q.Enqueue(node.right);
        }
    }

    /* Deletes a tree and sets the root as NULL */
    void deleteTree()
    {
        _deleteTree();
        root = null;
    }

    // Driver program to test above functions
    public static void Main(String[] args)
    {
        // create a binary tree
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(15);
        tree.root.left = new Node(10);
        tree.root.right = new Node(20);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(12);
        tree.root.right.left = new Node(16);
        tree.root.right.right = new Node(25);

        // delete entire binary tree
        tree.deleteTree();
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
/* Non-recursive program to delete the entire binary tree */

// A binary tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

let root;

/* Non-recursive function to delete an entire binary tree. */
function _deleteTree()
{
    // Base Case
        if (root == null)
            return;

        // Create an empty queue for level order traversal
        let q = [];

        // Do level order traversal starting from root
        q.push(root);
        while (q.length != 0)
        {
            let node = q.shift();

            if (node.left != null)
                q.push(node.left);
            if (node.right != null)
                q.push(node.right);
        }
}

    /* Deletes a tree and sets the root as NULL */
function deleteTree()
{
    _deleteTree();
        root = null;
}

// Driver program to test above functions
root = new Node(15);
root.left = new Node(10);
root.right = new Node(20);
root.left.left = new Node(8);
root.left.right = new Node(12);
root.right.left = new Node(16);
root.right.right = new Node(25);

// delete entire binary tree
deleteTree();

// This code is contributed by rag2127
</script>
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息