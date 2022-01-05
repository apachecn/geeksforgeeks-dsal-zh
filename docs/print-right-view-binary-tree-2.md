# 打印二叉树的右视图

> 原文:[https://www . geesforgeks . org/print-right-view-binary-tree-2/](https://www.geeksforgeeks.org/print-right-view-binary-tree-2/)

给定一个二叉树，打印它的右视图。二叉树的右视图是从右侧访问树时可见的一组节点。

```
Right view of following tree is 1 3 7 8

          1
       /     \
     2        3
   /   \     /  \
  4     5   6    7
                  \
                   8
```

这个问题可以用简单的递归遍历来解决。我们可以通过向所有递归调用传递一个参数来跟踪节点的级别。这个想法也是为了跟踪最高水平。并以访问右子树先于访问左子树的方式遍历树。每当我们看到一个节点的级别超过目前为止的最大级别，我们就打印该节点，因为这是其级别中的最后一个节点(注意，我们在左子树之前遍历右子树)。下面是这种方法的实现。

## C++

```
// C++ program to print right view of Binary Tree
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to
// create a new Binary Tree Node
struct Node *newNode(int item)
{
    struct Node *temp = (struct Node *)malloc(
                          sizeof(struct Node));
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Recursive function to print
// right view of a binary tree.
void rightViewUtil(struct Node *root,
                   int level, int *max_level)
{
    // Base Case
    if (root == NULL) return;

    // If this is the last Node of its level
    if (*max_level < level)
    {
        cout << root->data << "\t";
        *max_level = level;
    }

    // Recur for right subtree first,
    // then left subtree
    rightViewUtil(root->right, level + 1, max_level);
    rightViewUtil(root->left, level + 1, max_level);
}

// A wrapper over rightViewUtil()
void rightView(struct Node *root)
{
    int max_level = 0;
    rightViewUtil(root, 1, &max_level);
}

// Driver Code
int main()
{
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->right->right = newNode(8);

    rightView(root);

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to print right view of Binary Tree
#include<stdio.h>
#include<stdlib.h>

struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary Tree Node
struct Node *newNode(int item)
{
    struct Node *temp =  (struct Node *)malloc(sizeof(struct Node));
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Recursive function to print right view of a binary tree.
void rightViewUtil(struct Node *root, int level, int *max_level)
{
    // Base Case
    if (root==NULL)  return;

    // If this is the last Node of its level
    if (*max_level < level)
    {
        printf("%d\t", root->data);
        *max_level = level;
    }

    // Recur for right subtree first, then left subtree
    rightViewUtil(root->right, level+1, max_level);
    rightViewUtil(root->left, level+1, max_level);
}

// A wrapper over rightViewUtil()
void rightView(struct Node *root)
{
    int max_level = 0;
    rightViewUtil(root, 1, &max_level);
}

// Driver Program to test above functions
int main()
{
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    rightView(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print right view of binary tree

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}

// class to access maximum level by reference
class Max_level {

    int max_level;
}

class BinaryTree {

    Node root;
    Max_level max = new Max_level();

    // Recursive function to print right view of a binary tree.
    void rightViewUtil(Node node, int level, Max_level max_level) {

        // Base Case
        if (node == null)
            return;

        // If this is the last Node of its level
        if (max_level.max_level < level) {
            System.out.print(node.data + " ");
            max_level.max_level = level;
        }

        // Recur for right subtree first, then left subtree
        rightViewUtil(node.right, level + 1, max_level);
        rightViewUtil(node.left, level + 1, max_level);
    }

    void rightView()
    {
        rightView(root);
    }

    // A wrapper over rightViewUtil()
    void rightView(Node node) {

        rightViewUtil(node, 1, max);
    }

    // Driver program to test the above functions
    public static void main(String args[]) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);

        tree.rightView();

        }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to print right view of Binary Tree

# A binary tree node
class Node:
    # A constructor to create a new Binary tree Node
    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None

# Recursive function to print right view of Binary Tree
# used max_level as reference list ..only max_level[0]
# is helpful to us
def rightViewUtil(root, level, max_level):

    # Base Case
    if root is None:
        return

    # If this is the last node of its level
    if (max_level[0] < level):
        print "%d   " %(root.data),
        max_level[0] = level

    # Recur for right subtree first, then left subtree
    rightViewUtil(root.right, level+1, max_level)
    rightViewUtil(root.left, level+1, max_level)

def rightView(root):
    max_level = [0]
    rightViewUtil(root, 1, max_level)

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)
root.right.left.right = Node(8)

rightView(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to print right view of binary tree

// A binary tree node
public class Node
{

    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// class to access maximum level by reference
public class Max_level
{

    public int max_level;
}

public class BinaryTree
{

    public Node root;
    public Max_level max = new Max_level();

    // Recursive function to print right view of a binary tree.
    public virtual void rightViewUtil(Node node, int level,
                                        Max_level max_level)
    {

        // Base Case
        if (node == null)
        {
            return;
        }

        // If this is the last Node of its level
        if (max_level.max_level < level)
        {
            Console.Write(node.data + " ");
            max_level.max_level = level;
        }

        // Recur for right subtree first, then left subtree
        rightViewUtil(node.right, level + 1, max_level);
        rightViewUtil(node.left, level + 1, max_level);
    }

    public virtual void rightView()
    {
        rightView(root);
    }

    // A wrapper over rightViewUtil()
    public virtual void rightView(Node node)
    {

        rightViewUtil(node, 1, max);
    }

    // Driver program to test the above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);

        tree.rightView();

    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program to print
    // right view of binary tree

    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let max_level = 0;

    let root;

    // Recursive function to print right view of a binary tree.
    function rightViewUtil(node, level) {

        // Base Case
        if (node == null)
            return;

        // If this is the last Node of its level
        if (max_level < level) {
            document.write(node.data + " ");
            max_level = level;
        }

        // Recur for right subtree first, then left subtree
        rightViewUtil(node.right, level + 1);
        rightViewUtil(node.left, level + 1);
    }

    function rightView()
    {
        rightview(root);
    }

    // A wrapper over rightViewUtil()
    function rightview(node) {

        rightViewUtil(node, 1);
    }

    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.right.left.right = new Node(8);

    rightView();

</script>
```

**Output**

```
1    3    7    8    
```

[使用队列](https://www.geeksforgeeks.org/right-view-binary-tree-using-queue/)
**对二叉树进行右视图时间复杂度:**函数对树进行简单遍历，因此复杂度为 O(n)。

**方法二:**该方法讨论了基于[级序遍历的](https://www.geeksforgeeks.org/level-order-tree-traversal/)解。如果我们仔细观察，会发现我们的主要任务是打印每一级最右边的节点。因此，我们将在树上进行级别顺序遍历，并在每个级别打印最后一个节点。下面是上述方法的实现:

## C++

```
// C++ program to print left view of
// Binary Tree

#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// function to print Right view of
// binary tree
void printRightView(Node* root)
{
    if (root == NULL)
        return;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        // get number of nodes for each level
        int n = q.size();

        // traverse all the nodes of the current level
        while (n--) {

            Node* x = q.front();
            q.pop();

            // print the last node of each level
            if (n == 0) {
                cout << x->data << " ";
            }
            // if left child is not null push it into the
            // queue
            if (x->left)
                q.push(x->left);
            // if right child is not null push it into the
            // queue
            if (x->right)
                q.push(x->right);
        }
    }
}

// Driver code
int main()
{
    // Let's construct the tree as
    // shown in example

    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    printRightView(root);
}

// This code is contributed by
// Snehasish Dhar
```

## 蟒蛇 3

```
# Python3 program to print right
# view of Binary Tree
from collections import deque

# A binary tree node
class Node:

    # A constructor to create a new
    # Binary tree Node
    def __init__(self, val):
        self.data = val
        self.left = None
        self.right = None

# Function to print Right view of
# binary tree
def rightView(root):

    if root is None:
        return

    q = deque()
    q.append(root)

    while q:

        # Get number of nodes for each level
        n = len(q)

        # Traverse all the nodes of the
        # current level

        while n > 0:
            n -= 1

            # Get the front node in the queue
            node = q.popleft()

            # Print the last node of each level
            if n == 0:
                print(node.data, end = " ")

            # If left child is not null push it
            # into the queue
            if node.left:
                q.append(node.left)

            # If right child is not null push
            # it into the queue
            if node.right:
                q.append(node.right)

# Driver code

# Let's construct the tree as
# shown in example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)
root.right.left.right = Node(8)

rightView(root)

# This code is contributed by Pulkit Pansari
```

## java 描述语言

```
<script>

    // JavaScript program to print left view of Binary Tree

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Utility function to create a new tree node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // function to print Right view of
    // binary tree
    function printRightView(root)
    {
        if (root == null)
            return;

        let q = [];
        q.push(root);

        while (q.length > 0) {
            // get number of nodes for each level
            let n = q.length;

            // traverse all the nodes of the current level
            while (n-- > 0) {

                let x = q[0];
                q.shift();

                // print the last node of each level
                if (n == 0) {
                    document.write(x.data + " ");
                }
                // if left child is not null push it into the
                // queue
                if (x.left != null)
                    q.push(x.left);
                // if right child is not null push it into the
                // queue
                if (x.right != null)
                    q.push(x.right);
            }
        }
    }

    // Let's construct the tree as
    // shown in example

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);

    printRightView(root);

</script>
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print right view of
// Binary Tree

import java.io.*;
import java.util.LinkedList;
import java.util.Queue;

// A Binary Tree Node
class Node {
    int data;
    Node left, right;
    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    // function to print Right view of
    // binary tree
    void rightView(Node root)
    {
        if (root == null) {
            return;
        }

        Queue<Node> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {

            // get number of nodes for each level
            int n = q.size();

            // traverse all the nodes of the current level
            for (int i = 0; i < n; i++) {
                Node curr = q.peek();
                q.remove();

                // print the last node of each level
                if (i == n - 1) {
                    System.out.print(curr.data);
                    System.out.print(" ");
                }

                // if left child is not null add it into
                // the
                // queue
                if (curr.left != null) {
                    q.add(curr.left);
                }

                // if right child is not null add it into
                // the
                // queue
                if (curr.right != null) {
                    q.add(curr.right);
                }
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Let's construct the tree as
        // shown in example
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);

        tree.rightView(tree.root);
    }
}

// This code is contributed by Biswajit Rajak
```

**Output**

```
1 3 7 8 
```

**时间复杂度:** O(n)，其中 n 为二叉树中的节点数。

本文由 **Biswajit Rajak** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息