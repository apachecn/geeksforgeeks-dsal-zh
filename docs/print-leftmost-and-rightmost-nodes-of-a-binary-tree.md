# 打印二叉树最左边和最右边的节点

> 原文:[https://www . geesforgeks . org/print-二叉树的最左和最右节点/](https://www.geeksforgeeks.org/print-leftmost-and-rightmost-nodes-of-a-binary-tree/)

给定一棵二叉树，打印每一层的角节点。最左边的节点和最右边的节点。
例如，以下输出为 **15、10、20、8、25** 。

![](img/ac8f45eb24948136a752b2a5001247c2.png)

一个简单的解决方案是使用针对[打印左视图](http://https://www.geeksforgeeks.org/print-left-view-binary-tree/)和[右视图](https://www.geeksforgeeks.org/print-right-view-binary-tree-2/)所讨论的方法进行两次遍历。
**我们能用一次遍历打印所有的角节点吗？**
思路是使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。每次我们将队列的大小存储在变量 n 中，n 是该级别的节点数。对于每一级，我们检查当前节点是否是第一个(即索引 0 处的节点)和最后一个索引处的节点(即索引 n-1 处的节点)，如果是这两个节点中的任何一个，我们打印该节点的值。

<gfg-tab role="tab" slot="tab" id="gfg-tab-0">C/C++</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-0" data-code-lang="C"></gfg-panel>

```
 // C/C++ program to print corner node at each level
// of binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has key, pointer to left
   child and a pointer to right child */
struct Node
{
    int key;
    struct Node* left, *right;
};

/* To create a newNode of tree and return pointer */
struct Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

/* Function to print corner node at each level */
void printCorner(Node *root)
{
    //If the root is null then simply return
    if(root == NULL)
        return;
    //Do level order traversal using a single queue
    queue<Node*> q;
    q.push(root);

    while(!q.empty())
    {
        //n denotes the size of the current level in the queue
        int n = q.size();

        for(int i =0;i<n;i++)
        {
            Node *temp = q.front();
            q.pop();

            //If it is leftmost corner value or rightmost corner value then print it
            if(i==0 || i==n-1)
               cout<<temp->key<<" ";

            //push the left and right children of the temp node
            if(temp->left)
                q.push(temp->left);
            if(temp->right)
                q.push(temp->right);
        }
    }
}
// Driver program to test above function
int main ()
{
    Node *root =  newNode(15);
    root->left = newNode(10);
    root->right = newNode(20);
    root->left->left = newNode(8);
    root->left->right = newNode(12);
    root->right->left = newNode(16);
    root->right->right = newNode(25);
    printCorner(root);
    return 0; 
}

// This code is contributed by Utkarsh Choubey 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print corner node at each level in a binary tree

import java.util.*;

/* A binary tree node has key, pointer to left
   child and a pointer to right child */
class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* Function to print corner node at each level */
    void printCorner(Node root)
    {
        //  star node is for keeping track of levels
        Queue<Node> q = new LinkedList<Node>();

        // pushing root node and star node
        q.add(root);
        // Do level order traversal of Binary Tree
        while (!q.isEmpty())
        {
            // n is the no of nodes in current Level
            int n = q.size();
            for(int i = 0 ; i < n ; i++){
            // dequeue the front node from the queue
            Node temp = q.peek();
            q.poll();
            //If it is leftmost corner value or rightmost corner value then print it
            if(i==0 || i==n-1)
                System.out.print(temp.key + "  ");
            //push the left and right children of the temp node
            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);
        }
        }

    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(15);
        tree.root.left = new Node(10);
        tree.root.right = new Node(20);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(12);
        tree.root.right.left = new Node(16);
        tree.root.right.right = new Node(25);

        tree.printCorner(tree.root);
    }
}

// This code has been contributed by Utkarsh Choubey
```

## 蟒蛇 3

```
# Python3 program to print corner
# node at each level of binary tree
from collections import deque

# A binary tree node has key, pointer to left
# child and a pointer to right child
class Node:
    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to print corner node at each level
def printCorner(root: Node):

    # If the root is null then simply return
    if root == None:
        return

    # Do level order traversal
    # using a single queue
    q = deque()
    q.append(root)

    while q:

        # n denotes the size of the current
        # level in the queue
        n = len(q)
        for i in range(n):
            temp = q[0]
            q.popleft()

            # If it is leftmost corner value or
            # rightmost corner value then print it
            if i == 0 or i == n - 1:
                print(temp.key, end = " ")

            # push the left and right children
            # of the temp node
            if temp.left:
                q.append(temp.left)
            if temp.right:
                q.append(temp.right)

# Driver Code
if __name__ == "__main__":

    root = Node(15)
    root.left = Node(10)
    root.right = Node(20)
    root.left.left = Node(8)
    root.left.right = Node(12)
    root.right.left = Node(16)
    root.right.right = Node(25)

    printCorner(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to print corner node
// at each level in a binary tree
using System;
using System.Collections.Generic;

/* A binary tree node has key, pointer to left
child and a pointer to right child */
public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

public class BinaryTree
{
    Node root;

    /* Function to print corner node at each level */
    void printCorner(Node root)
    {
        // star node is for keeping track of levels
        Queue<Node> q = new Queue<Node>();

        // pushing root node and star node
        q.Enqueue(root);
        // Do level order traversal of Binary Tree
        while (q.Count != 0)
        {
            // n is the no of nodes in current Level
            int n = q.Count;
            for(int i = 0 ; i < n ; i++){
                Node temp = q.Peek();
                q.Dequeue();
                //If it is leftmost corner value or rightmost corner value then print it
                if(i==0||i==n-1)
                    Console.Write(temp.key + " ");
            //push the left and right children of the temp node
                if (temp.left != null)
                    q.Enqueue(temp.left);
                if (temp.right != null)
                    q.Enqueue(temp.right);

            }
        }

}

    // Driver code
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(15);
        tree.root.left = new Node(10);
        tree.root.right = new Node(20);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(12);
        tree.root.right.left = new Node(16);
        tree.root.right.right = new Node(25);

        tree.printCorner(tree.root);
    }
}

// This code is contributed by Utkarsh Choubey
```

**输出:**

```
15  10  20  8  25  
```

**时间复杂度:** O(n)，其中 n 为二叉树中的节点数。

本文由乌卡什·乔贝供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。