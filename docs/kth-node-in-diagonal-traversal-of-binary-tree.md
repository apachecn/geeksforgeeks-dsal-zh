# 二叉树对角遍历的第 k 个节点

> 原文:[https://www . geesforgeks . org/kth-二叉树对角遍历节点/](https://www.geeksforgeeks.org/kth-node-in-diagonal-traversal-of-binary-tree/)

给定一棵二叉树和一个值 **K** 。任务是打印二叉树对角遍历中的第 k 个**节点。如果不存在这样的节点，则打印-1。
**例:**** 

```
Input : 
         8
       /   \
      3    10
     /    /  \
    1    6   14
        / \  /
       4  7 13
k = 5
Output : 6
Diagonal Traversal of the above tree is:
8 10 14
3 6 7 13
1 4

Input :
       1
      / \
     2   3
    /     \
   4       5
k = 7   
Output : -1
```

**方法:**思想是执行二叉树的[对角](https://www.geeksforgeeks.org/iterative-diagonal-traversal-binary-tree/)遍历，直到在对角遍历中访问到 K 个节点。遍历每个访问的节点时，递减变量 **K** 的值，当 K 的值变为零时返回当前节点。如果对角遍历不包含至少 K 个节点，则返回-1。
以下是上述方法的实现:

## C++

```
// C++ program to print kth node
// in the diagonal traversal of a binary tree

#include <bits/stdc++.h>
using namespace std;

// A binary tree node has data, pointer to left
// child and a pointer to right child
struct Node {
    int data;
    Node *left, *right;
};

// Helper function that allocates a new node
Node* newNode(int data)
{
    Node* node = new Node();
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Iterative function to print kth node
// in diagonal traversal of binary tree
int diagonalPrint(Node* root, int k)
{
    // Base cases
    if (root == NULL || k == 0)
        return -1;

    int ans = -1;
    queue<Node*> q;

    // Push root node
    q.push(root);

    // Push delimiter NULL
    q.push(NULL);

    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        if (temp == NULL) {
            if (q.empty()) {
                // If kth node exists then return
                // the answer
                if (k == 0)
                    return ans;

                // If kth node doesnt exists
                // then break from the while loop
                else
                    break;
            }
            q.push(NULL);
        }
        else {
            while (temp) {
                // If the required kth node
                // has been found then return the answer
                if (k == 0)
                    return ans;

                k--;

                // Update the value of variable ans
                // each time
                ans = temp->data;

                if (temp->left)
                    q.push(temp->left);

                temp = temp->right;
            }
        }
    }

    // If kth node doesnt exists then
    // return -1
    return -1;
}

// Driver Code
int main()
{
    Node* root = newNode(8);
    root->left = newNode(3);
    root->right = newNode(10);
    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->right->right = newNode(14);
    root->right->right->left = newNode(13);
    root->left->right->left = newNode(4);
    root->left->right->right = newNode(7);

    int k = 9;

    cout << diagonalPrint(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print kth node
// in the diagonal traversal of a binary tree
import java.util.*;

class GFG
{

// A binary tree node has data, pointer to left
//child and a pointer to right child
static class Node
{
    int data;
    Node left, right;
};

// Helper function that allocates a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Iterative function to print kth node
// in diagonal traversal of binary tree
static int diagonalPrint(Node root, int k)
{
    // Base cases
    if (root == null || k == 0)
        return -1;

    int ans = -1;
    Queue<Node> q = new LinkedList<Node>();

    // add root node
    q.add(root);

    // add delimiter null
    q.add(null);

    while (q.size() > 0)
    {
        Node temp = q.peek();
        q.remove();

        if (temp == null)
        {
            if (q.size() == 0)
            {
                // If kth node exists then return
                // the answer
                if (k == 0)
                    return ans;

                // If kth node doesnt exists
                // then break from the while loop
                else
                    break;
            }
            q.add(null);
        }
        else {
            while (temp != null)
            {
                // If the required kth node
                // has been found then return the answer
                if (k == 0)
                    return ans;

                k--;

                // Update the value of variable ans
                // each time
                ans = temp.data;

                if (temp.left!=null)
                    q.add(temp.left);

                temp = temp.right;
            }
        }
    }

    // If kth node doesnt exists then
    // return -1
    return -1;
}

// Driver Code
public static void main(String args[])
{
    Node root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.right.right = newNode(14);
    root.right.right.left = newNode(13);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);

    int k = 9;

    System.out.println( diagonalPrint(root, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to print kth node
# in the diagonal traversal of a binary tree

# Linked List node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates a new node
def newNode(data) :

    node = Node(0)
    node.data = data
    node.left = node.right = None
    return (node)

# Iterative function to print kth node
# in diagonal traversal of binary tree
def diagonalPrint( root, k) :

    # Base cases
    if (root == None or k == 0) :
        return -1

    ans = -1
    q = []

    # append root node
    q.append(root)

    # append delimiter None
    q.append(None)

    while (len(q) > 0):

        temp = q[0]
        q.pop(0)

        if (temp == None):

            if (len(q) == 0) :

                # If kth node exists then return
                # the answer
                if (k == 0) :
                    return ans

                # If kth node doesnt exists
                # then break from the while loop
                else:
                    break

            q.append(None)

        else :
            while (temp != None):

                # If the required kth node
                # has been found then return the answer
                if (k == 0) :
                    return ans

                k = k - 1

                # Update the value of variable ans
                # each time
                ans = temp.data

                if (temp.left != None):
                    q.append(temp.left)

                temp = temp.right

    # If kth node doesnt exists then
    # return -1
    return -1

# Driver Code

root = newNode(8)
root.left = newNode(3)
root.right = newNode(10)
root.left.left = newNode(1)
root.left.right = newNode(6)
root.right.right = newNode(14)
root.right.right.left = newNode(13)
root.left.right.left = newNode(4)
root.left.right.right = newNode(7)

k = 9

print( diagonalPrint(root, k))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to print kth node
// in the diagonal traversal of a binary tree
using System;
using System.Collections.Generic;

class GFG
{

// A binary tree node has data, pointer to left
//child and a pointer to right child
public class Node
{
    public int data;
    public Node left, right;
};

// Helper function that allocates a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Iterative function to print kth node
// in diagonal traversal of binary tree
static int diagonalPrint(Node root, int k)
{
    // Base cases
    if (root == null || k == 0)
        return -1;

    int ans = -1;
    Queue<Node> q = new Queue<Node>();

    // Enqueue root node
    q.Enqueue(root);

    // Enqueue delimiter null
    q.Enqueue(null);

    while (q.Count > 0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        if (temp == null)
        {
            if (q.Count == 0)
            {
                // If kth node exists then return
                // the answer
                if (k == 0)
                    return ans;

                // If kth node doesnt exists
                // then break from the while loop
                else
                    break;
            }
            q.Enqueue(null);
        }
        else
        {
            while (temp != null)
            {
                // If the required kth node
                // has been found then return the answer
                if (k == 0)
                    return ans;

                k--;

                // Update the value of variable ans
                // each time
                ans = temp.data;

                if (temp.left!=null)
                    q.Enqueue(temp.left);

                temp = temp.right;
            }
        }
    }

    // If kth node doesnt exists then
    // return -1
    return -1;
}

// Driver Code
public static void Main(String []args)
{
    Node root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.right.right = newNode(14);
    root.right.right.left = newNode(13);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);

    int k = 9;

    Console.WriteLine( diagonalPrint(root, k));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to print kth node
// in the diagonal traversal of a binary tree

// A binary tree node has data, pointer to left
//child and a pointer to right child
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Helper function that allocates a new node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Iterative function to print kth node
// in diagonal traversal of binary tree
function diagonalPrint(root, k)
{
    // Base cases
    if (root == null || k == 0)
        return -1;

    var ans = -1;
    var q = [];

    // push root node
    q.push(root);

    // push delimiter null
    q.push(null);

    while (q.length > 0)
    {
        var temp = q[0];
        q.shift();

        if (temp == null)
        {
            if (q.length == 0)
            {
                // If kth node exists then return
                // the answer
                if (k == 0)
                    return ans;

                // If kth node doesnt exists
                // then break from the while loop
                else
                    break;
            }
            q.push(null);
        }
        else
        {
            while (temp != null)
            {
                // If the required kth node
                // has been found then return the answer
                if (k == 0)
                    return ans;

                k--;

                // Update the value of variable ans
                // each time
                ans = temp.data;

                if (temp.left!=null)
                    q.push(temp.left);

                temp = temp.right;
            }
        }
    }

    // If kth node doesnt exists then
    // return -1
    return -1;
}

// Driver Code
var root = newNode(8);
root.left = newNode(3);
root.right = newNode(10);
root.left.left = newNode(1);
root.left.right = newNode(6);
root.right.right = newNode(14);
root.right.right.left = newNode(13);
root.left.right.left = newNode(4);
root.left.right.right = newNode(7);
var k = 9;
document.write( diagonalPrint(root, k));

</script>
```

**Output:** 

```
4
```

**时间复杂度** : O(N)，其中 N 为二叉树中的节点总数。
**辅助空间:** O(N)