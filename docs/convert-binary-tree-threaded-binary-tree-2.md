# 将二叉树转换为线程二叉树|集合 1(使用队列)

> 原文:[https://www . geesforgeks . org/convert-二叉树-threaded-二叉树-2/](https://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree-2/)

我们已经讨论了[线程二叉树](http://geeksquiz.com/threaded-binary-tree/)。线程二叉树的思想是使有序遍历更快，并且不需要堆栈和递归。在一个简单的线程二叉树中，空右指针被用来存储后续数据。当右指针为空时，它被用来存储后续数据。
下图显示了一个单线程二叉树的例子。虚线代表螺纹。

![threadedBT](img/abdc49bbfde3b2352262a2bd1161d6dd.png)

下面是单线程二叉树的结构。

## C

```
struct Node {
    int key;
    Node *left, *right;

    // Used to indicate whether the right pointer is a normal right
    // pointer or a pointer to inorder successor.
    bool isThreaded;
};
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static class Node {
    int key;
    Node left, right;

    // Used to indicate whether the right pointer is a normal right
    // pointer or a pointer to inorder successor.
    boolean isThreaded;
};

// This code is contributed by umadevi9616
```

## java 描述语言

```
class Node
{
    constructor(item)
    {
        // Used to indicate whether the right pointer is a normal
          // right pointer or a pointer to inorder successor.
        let isThreaded;
        this.data=item;
        this.left = this.right = null;

    }
}
```

**如何将给定的二叉树转换成线程二叉树？**
我们基本上需要设置空的右指针来指示后继者。我们首先对树进行有序遍历，并将其存储在一个队列中(我们也可以使用一个简单的数组)，以便有序的后继节点成为下一个节点。我们再次进行有序遍历，每当我们发现一个右边为空的节点时，我们从队列中取出前面的项目，并使其成为当前节点的右边。我们还将 isThreaded 设置为 true，以指示右边的指针是一个线程链接。
以下是上述思路的实现。

## C++

```
/* C++ program to convert a Binary Tree to Threaded Tree */
#include <bits/stdc++.h>
using namespace std;

/* Structure of a node in threaded binary tree */
struct Node {
    int key;
    Node *left, *right;

    // Used to indicate whether the right pointer is a normal
    // right pointer or a pointer to inorder successor.
    bool isThreaded;
};

// Helper function to put the Nodes in inorder into queue
void populateQueue(Node* root, std::queue<Node*>* q)
{
    if (root == NULL)
        return;
    if (root->left)
        populateQueue(root->left, q);
    q->push(root);
    if (root->right)
        populateQueue(root->right, q);
}

// Function to traverse queue, and make tree threaded
void createThreadedUtil(Node* root, std::queue<Node*>* q)
{
    if (root == NULL)
        return;

    if (root->left)
        createThreadedUtil(root->left, q);
    q->pop();

    if (root->right)
        createThreadedUtil(root->right, q);

    // If right pointer is NULL, link it to the
    // inorder successor and set 'isThreaded' bit.
    else {
        root->right = q->front();
        root->isThreaded = true;
    }
}

// This function uses populateQueue() and
// createThreadedUtil() to convert a given binary tree
// to threaded tree.
void createThreaded(Node* root)
{
    // Create a queue to store inorder traversal
    std::queue<Node*> q;

    // Store inorder traversal in queue
    populateQueue(root, &q);

    // Link NULL right pointers to inorder successor
    createThreadedUtil(root, &q);
}

// A utility function to find leftmost node in a binary
// tree rooted with 'root'. This function is used in inOrder()
Node* leftMost(Node* root)
{
    while (root != NULL && root->left != NULL)
        root = root->left;
    return root;
}

// Function to do inorder traversal of a threaded binary tree
void inOrder(Node* root)
{
    if (root == NULL)
        return;

    // Find the leftmost node in Binary Tree
    Node* cur = leftMost(root);

    while (cur != NULL) {
        cout << cur->key << " ";

        // If this Node is a thread Node, then go to
        // inorder successor
        if (cur->isThreaded)
            cur = cur->right;

        else // Else go to the leftmost child in right subtree
            cur = leftMost(cur->right);
    }
}

// A utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->left = temp->right = NULL;
    temp->key = key;
    return temp;
}

// Driver program to test above functions
int main()
{
    /*       1
            / \
           2   3
          / \ / \
         4  5 6  7     */
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    createThreaded(root);

    cout << "Inorder traversal of created threaded tree is\n";
    inOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert binary tree to threaded tree
import java.util.LinkedList;
import java.util.Queue;

/* Class containing left and right child of current
 node and key value*/
class Node {
    int data;
    Node left, right;

    // Used to indicate whether the right pointer is a normal
    // right pointer or a pointer to inorder successor.
    boolean isThreaded;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    // Helper function to put the Nodes in inorder into queue
    void populateQueue(Node node, Queue<Node> q)
    {
        if (node == null)
            return;
        if (node.left != null)
            populateQueue(node.left, q);
        q.add(node);
        if (node.right != null)
            populateQueue(node.right, q);
    }

    // Function to traverse queue, and make tree threaded
    void createThreadedUtil(Node node, Queue<Node> q)
    {
        if (node == null)
            return;

        if (node.left != null)
            createThreadedUtil(node.left, q);
        q.remove();

        if (node.right != null)
            createThreadedUtil(node.right, q);

        // If right pointer is NULL, link it to the
        // inorder successor and set 'isThreaded' bit.
        else {
            node.right = q.peek();
            node.isThreaded = true;
        }
    }

    // This function uses populateQueue() and
    // createThreadedUtil() to convert a given binary tree
    // to threaded tree.
    void createThreaded(Node node)
    {
        // Create a queue to store inorder traversal
        Queue<Node> q = new LinkedList<Node>();

        // Store inorder traversal in queue
        populateQueue(node, q);

        // Link NULL right pointers to inorder successor
        createThreadedUtil(node, q);
    }

    // A utility function to find leftmost node in a binary
    // tree rooted with 'root'. This function is used in inOrder()
    Node leftMost(Node node)
    {
        while (node != null && node.left != null)
            node = node.left;
        return node;
    }

    // Function to do inorder traversal of a threaded binary tree
    void inOrder(Node node)
    {
        if (node == null)
            return;

        // Find the leftmost node in Binary Tree
        Node cur = leftMost(node);

        while (cur != null) {
            System.out.print(" " + cur.data + " ");

            // If this Node is a thread Node, then go to
            // inorder successor
            if (cur.isThreaded == true)
                cur = cur.right;
            else // Else go to the leftmost child in right subtree
                cur = leftMost(cur.right);
        }
    }

    // Driver program to test for above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);

        tree.createThreaded(tree.root);
        System.out.println("Inorder traversal of created threaded tree");
        tree.inOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to convert
# a Binary Tree to Threaded Tree

# Structure of a node in threaded binary tree
class Node:

    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

        # Used to indicate whether the right pointer
        # is a normal right pointer or a pointer to
        # inorder successor.
        self.isThreaded = False

# Helper function to put the Nodes
# in inorder into queue
def populateQueue(root, q):

    if root == None: return
    if root.left:
        populateQueue(root.left, q)
    q.append(root)

    if root.right:
        populateQueue(root.right, q)

# Function to traverse queue,
# and make tree threaded
def createThreadedUtil(root, q):

    if root == None: return

    if root.left:
        createThreadedUtil(root.left, q)
    q.pop(0)

    if root.right:
        createThreadedUtil(root.right, q)

    # If right pointer is None, link it to the
    # inorder successor and set 'isThreaded' bit.
    else:
        if len(q) == 0: root.right = None
        else: root.right = q[0]
        root.isThreaded = True

# This function uses populateQueue() and
# createThreadedUtil() to convert a given
# binary tree to threaded tree.
def createThreaded(root):

    # Create a queue to store inorder traversal
    q = []

    # Store inorder traversal in queue
    populateQueue(root, q)

    # Link None right pointers to inorder successor
    createThreadedUtil(root, q)

# A utility function to find leftmost node
# in a binary tree rooted with 'root'.
# This function is used in inOrder()
def leftMost(root):

    while root != None and root.left != None:
        root = root.left
    return root

# Function to do inorder traversal
# of a threaded binary tree
def inOrder(root):

    if root == None: return

    # Find the leftmost node in Binary Tree
    cur = leftMost(root)

    while cur != None:

        print(cur.key, end = " ")

        # If this Node is a thread Node,
        # then go to inorder successor
        if cur.isThreaded:
            cur = cur.right

        # Else go to the leftmost child
        # in right subtree
        else:
            cur = leftMost(cur.right)

# Driver Code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    createThreaded(root)

    print("Inorder traversal of created",
                      "threaded tree is")
    inOrder(root)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to convert binary tree to threaded tree
using System;
using System.Collections.Generic;

/* Class containing left and right child of current
node and key value*/
public class Node {
    public int data;
    public Node left, right;

    // Used to indicate whether the right pointer is a normal
    // right pointer or a pointer to inorder successor.
    public bool isThreaded;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree {
    Node root;

    // Helper function to put the Nodes in inorder into queue
    void populateQueue(Node node, Queue<Node> q)
    {
        if (node == null)
            return;
        if (node.left != null)
            populateQueue(node.left, q);
        q.Enqueue(node);
        if (node.right != null)
            populateQueue(node.right, q);
    }

    // Function to traverse queue, and make tree threaded
    void createThreadedUtil(Node node, Queue<Node> q)
    {
        if (node == null)
            return;

        if (node.left != null)
            createThreadedUtil(node.left, q);
        q.Dequeue();

        if (node.right != null)
            createThreadedUtil(node.right, q);

        // If right pointer is NULL, link it to the
        // inorder successor and set 'isThreaded' bit.
        else {
            if (q.Count != 0)
                node.right = q.Peek();
            node.isThreaded = true;
        }
    }

    // This function uses populateQueue() and
    // createThreadedUtil() to convert a given binary tree
    // to threaded tree.
    void createThreaded(Node node)
    {
        // Create a queue to store inorder traversal
        Queue<Node> q = new Queue<Node>();

        // Store inorder traversal in queue
        populateQueue(node, q);

        // Link NULL right pointers to inorder successor
        createThreadedUtil(node, q);
    }

    // A utility function to find leftmost node in a binary
    // tree rooted with 'root'. This function is used in inOrder()
    Node leftMost(Node node)
    {
        while (node != null && node.left != null)
            node = node.left;
        return node;
    }

    // Function to do inorder traversal of a threaded binary tree
    void inOrder(Node node)
    {
        if (node == null)
            return;

        // Find the leftmost node in Binary Tree
        Node cur = leftMost(node);

        while (cur != null) {
            Console.Write(" " + cur.data + " ");

            // If this Node is a thread Node, then go to
            // inorder successor
            if (cur.isThreaded == true)
                cur = cur.right;
            else // Else go to the leftmost child in right subtree
                cur = leftMost(cur.right);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);

        tree.createThreaded(tree.root);
        Console.WriteLine("Inorder traversal of created threaded tree");
        tree.inOrder(tree.root);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to convert
// binary tree to threaded tree

/* Class containing left and right child of current
 node and key value*/
class Node
{
    constructor(item)
    {
    // Used to indicate whether the right pointer is a normal
    // right pointer or a pointer to inorder successor.
        let isThreaded;
        this.data=item;
        this.left = this.right = null;

    }
}

let root;
// Helper function to put the Nodes in inorder into queue
function populateQueue(node,q)
{
     if (node == null)
            return;
        if (node.left != null)
            populateQueue(node.left, q);
        q.push(node);
        if (node.right != null)
            populateQueue(node.right, q);
}

 // Function to traverse queue, and make tree threaded
function createThreadedUtil(node,q)
{
     if (node == null)
            return;

        if (node.left != null)
            createThreadedUtil(node.left, q);
        q.shift();

        if (node.right != null)
            createThreadedUtil(node.right, q);

        // If right pointer is NULL, link it to the
        // inorder successor and set 'isThreaded' bit.
        else {
            node.right = q[0];
            node.isThreaded = true;
        }
}

// This function uses populateQueue() and
// createThreadedUtil() to convert a given binary tree
// to threaded tree.
function createThreaded(node)
{
    // Create a queue to store inorder traversal
        let q = [];

        // Store inorder traversal in queue
        populateQueue(node, q);

        // Link NULL right pointers to inorder successor
        createThreadedUtil(node, q);
}

// A utility function to find leftmost node in a binary
// tree rooted with 'root'. This function is used in inOrder()
function leftMost(node)
{
    while (node != null && node.left != null)
            node = node.left;
        return node;
}

// Function to do inorder traversal of a threaded binary tree
function inOrder(node)
{
    if (node == null)
            return;

        // Find the leftmost node in Binary Tree
        let cur = leftMost(node);

        while (cur != null) {
            document.write(" " + cur.data + " ");

            // If this Node is a thread Node, then go to
            // inorder successor
            if (cur.isThreaded == true)
                cur = cur.right;
            else // Else go to the leftmost child in right subtree
                cur = leftMost(cur.right);
        }
}

// Driver program to test for above functions
root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);

        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);

        createThreaded(root);

        document.write(
        "Inorder traversal of created threaded tree<br>"
        );
        inOrder(root);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Inorder traversal of created threaded tree is
4 2 5 1 6 3 7
```

[**将二叉树转换为线程二叉树|集合 2(高效)**](https://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree-set-2-efficient/)
本文由 **Minhaz** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息