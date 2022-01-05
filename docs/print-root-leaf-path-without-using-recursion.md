# 不使用递归打印根到叶路径

> 原文:[https://www . geesforgeks . org/print-root-leaf-path-不使用递归/](https://www.geeksforgeeks.org/print-root-leaf-path-without-using-recursion/)

给定一棵二叉树，不使用递归打印其所有根到叶路径。例如，考虑下面的二叉树。

```
        6
     /    \
    3      5
  /   \     \
 2     5     4
     /   \
    7     4

There are 4 leaves, hence 4 root to leaf paths -
  6->3->2              
  6->3->5->7
  6->3->5->4
  6->5>4
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
我们可以迭代遍历树(我们已经使用了[迭代预排序](https://www.geeksforgeeks.org/iterative-preorder-traversal/))。问题是，如何扩展遍历来打印根到叶的路径？其思想是维护一个映射来存储二叉树节点的父指针。现在，每当我们在进行迭代前序遍历时遇到一个叶节点，我们就可以使用父指针轻松地打印根到叶路径。下面是这个想法的实现。

## C++

```
// C++ program to Print root to leaf path WITHOUT
// using recursion
#include <bits/stdc++.h>
using namespace std;

/* A binary tree */
struct Node
{
    int data;
    struct Node *left, *right;
};

/* Helper function that allocates a new node
   with the given data and NULL left and right
   pointers.*/
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

/* Function to print root to leaf path for a leaf
   using parent nodes stored in map */
void printTopToBottomPath(Node* curr,
                         map<Node*, Node*> parent)
{
    stack<Node*> stk;

    // start from leaf node and keep on pushing
    // nodes into stack till root node is reached
    while (curr)
    {
        stk.push(curr);
        curr = parent[curr];
    }

    // Start popping nodes from stack and print them
    while (!stk.empty())
    {
        curr = stk.top();
        stk.pop();
        cout << curr->data << " ";
    }
    cout << endl;
}

/* An iterative function to do preorder traversal
   of binary tree  and print root to leaf path
   without using recursion */
void printRootToLeaf(Node* root)
{
    // Corner Case
    if (root == NULL)
        return;

    // Create an empty stack and push root to it
    stack<Node*> nodeStack;
    nodeStack.push(root);

    // Create a map to store parent pointers of binary
    // tree nodes
    map<Node*, Node*> parent;

    // parent of root is NULL
    parent[root] = NULL;

    /* Pop all items one by one. Do following for
       every popped item
        a) push its right child and set its parent
           pointer
        b) push its left child and set its parent
           pointer
       Note that right child is pushed first so that
       left is processed first */
    while (!nodeStack.empty())
    {
        // Pop the top item from stack
        Node* current = nodeStack.top();
        nodeStack.pop();

        // If leaf node encountered, print Top To
        // Bottom path
        if (!(current->left) && !(current->right))
            printTopToBottomPath(current, parent);

        // Push right & left children of the popped node
        // to stack. Also set their parent pointer in
        // the map
        if (current->right)
        {
            parent[current->right] = current;
            nodeStack.push(current->right);
        }
        if (current->left)
        {
            parent[current->left] = current;
            nodeStack.push(current->left);
        }
    }
}

// Driver program to test above functions
int main()
{
    /* Constructed binary tree is
         10
        /  \
       8    2
      / \   /
     3     5 2     */
    Node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->left = newNode(2);

    printRootToLeaf(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Print root to leaf path WITHOUT
// using recursion
import java.util.Stack;
import java.util.HashMap;
public class PrintPath {

    /* Function to print root to leaf path for a leaf
    using parent nodes stored in map */
    public static void printTopToBottomPath(Node curr, HashMap<Node,Node> parent)
    {
        Stack<Node> stk=new Stack<>() ;

        // start from leaf node and keep on pushing
        // nodes into stack till root node is reached
        while (curr!=null)
        {
            stk.push(curr);
            curr = parent.get(curr);
        }

        // Start popping nodes from stack and print them
        while (!stk.isEmpty())
        {
            curr = stk.pop();
            System.out.print(curr.data+" ");
        }
        System.out.println();
    }

    /* An iterative function to do preorder traversal
    of binary tree  and print root to leaf path
    without using recursion */
    public static void printRootToLeaf(Node root)
    {
        // Corner Case
        if (root == null)
            return;

        // Create an empty stack and push root to it
        Stack<Node> nodeStack=new Stack<>();
        nodeStack.push(root);

        // Create a map to store parent pointers of binary
        // tree nodes
        HashMap<Node,Node> parent=new HashMap<>();

        // parent of root is NULL
        parent.put(root,null);

        /* Pop all items one by one. Do following for
        every popped item
            a) push its right child and set its parent
            pointer
            b) push its left child and set its parent
            pointer
        Note that right child is pushed first so that
        left is processed first */
        while (!nodeStack.isEmpty())
        {
            // Pop the top item from stack
            Node current = nodeStack.pop();

            // If leaf node encountered, print Top To
            // Bottom path
            if (current.left==null && current.right==null)
                printTopToBottomPath(current, parent);

            // Push right & left children of the popped node
            // to stack. Also set their parent pointer in
            // the map
            if (current.right!=null)
            {
                parent.put(current.right,current);
                nodeStack.push(current.right);
            }
            if (current.left!=null)
            {
                parent.put(current.left,current);
                nodeStack.push(current.left);
            }
        }
    }

    public static void main(String args[]) {
        Node root=new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.left.right = new Node(5);
        root.right.left = new Node(2);
        printRootToLeaf(root);
    }
}

/* A binary tree node */
class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        left=right=null;
        this.data=data;
    }
};
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python3 program to Print root to
# leaf path without using recursion

# Helper function that allocates a new
# node with the given data and None left
# and right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to print root to leaf path for a
# leaf using parent nodes stored in map
def printTopToBottomPath(curr, parent):
    stk = []

    # start from leaf node and keep on appending
    # nodes into stack till root node is reached
    while (curr):
        stk.append(curr)
        curr = parent[curr]

    # Start popping nodes from stack
    # and print them
    while len(stk) != 0:
        curr = stk[-1]
        stk.pop(-1)
        print(curr.data, end = " ")
    print()

# An iterative function to do preorder
# traversal of binary tree and print
# root to leaf path without using recursion
def printRootToLeaf(root):

    # Corner Case
    if (root == None):
        return

    # Create an empty stack and
    # append root to it
    nodeStack = []
    nodeStack.append(root)

    # Create a map to store parent
    # pointers of binary tree nodes
    parent = {}

    # parent of root is None
    parent[root] = None

    # Pop all items one by one. Do following
    # for every popped item
    # a) append its right child and set its 
    #     parent pointer
    # b) append its left child and set its
    #     parent pointer
    # Note that right child is appended first
    # so that left is processed first
    while len(nodeStack) != 0:

        # Pop the top item from stack
        current = nodeStack[-1]
        nodeStack.pop(-1)

        # If leaf node encountered, print
        # Top To Bottom path
        if (not (current.left) and
            not (current.right)):
            printTopToBottomPath(current, parent)

        # append right & left children of the
        # popped node to stack. Also set their
        # parent pointer in the map
        if (current.right):
            parent[current.right] = current
            nodeStack.append(current.right)
        if (current.left):
            parent[current.left] = current
            nodeStack.append(current.left)

# Driver Code
if __name__ == '__main__':

    # Constructed binary tree is
    #     10
    # / \
    # 8 2
    # / \ /
    # 3 5 2    
    root = newNode(10)
    root.left = newNode(8)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.left = newNode(2)

    printRootToLeaf(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to Print root to leaf path WITHOUT
// using recursion
using System;
using System.Collections.Generic;

public class PrintPath
{

    /* Function to print root to leaf path for a leaf
    using parent nodes stored in map */
    public static void printTopToBottomPath(Node curr,
                        Dictionary<Node,Node> parent)
    {
        Stack<Node> stk = new Stack<Node>() ;

        // start from leaf node and keep on pushing
        // nodes into stack till root node is reached
        while (curr != null)
        {
            stk.Push(curr);
            curr = parent[curr];
        }

        // Start popping nodes from stack and print them
        while (stk.Count != 0)
        {
            curr = stk.Pop();
            Console.Write(curr.data + " ");
        }
        Console.WriteLine();
    }

    /* An iterative function to do preorder traversal
    of binary tree and print root to leaf path
    without using recursion */
    public static void printRootToLeaf(Node root)
    {
        // Corner Case
        if (root == null)
            return;

        // Create an empty stack and push root to it
        Stack<Node> nodeStack = new Stack<Node>();
        nodeStack.Push(root);

        // Create a map to store parent 
        // pointers of binary tree nodes
        Dictionary<Node,Node> parent = new Dictionary<Node,Node>();

        // parent of root is NULL
        parent.Add(root, null);

        /* Pop all items one by one. Do following for
        every popped item
            a) push its right child and set its parent
            pointer
            b) push its left child and set its parent
            pointer
        Note that right child is pushed first so that
        left is processed first */
        while (nodeStack.Count != 0)
        {
            // Pop the top item from stack
            Node current = nodeStack.Pop();

            // If leaf node encountered, print Top To
            // Bottom path
            if (current.left == null && current.right == null)
                printTopToBottomPath(current, parent);

            // Push right & left children of the popped node
            // to stack. Also set their parent pointer in
            // the map
            if (current.right != null)
            {
                parent.Add(current.right,current);
                nodeStack.Push(current.right);
            }
            if (current.left != null)
            {
                parent.Add(current.left,current);
                nodeStack.Push(current.left);
            }
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.left.right = new Node(5);
        root.right.left = new Node(2);
        printRootToLeaf(root);
    }
}

/* A binary tree node */
public class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        left = right = null;
        this.data = data;
    }
};

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to Print root to leaf path WITHOUT
// using recursion

/* Function to print root to leaf path for a leaf
using parent nodes stored in map */
function printTopToBottomPath(curr, parent)
{
    var stk = [];

    // start from leaf node and keep on pushing
    // nodes into stack till root node is reached
    while (curr != null)
    {
        stk.push(curr);
        curr = parent.get(curr);
    }

    // Start popping nodes from stack and print them
    while (stk.length != 0)
    {
        curr = stk[stk.length-1];
        stk.pop();
        document.write(curr.data + " ");
    }
    document.write("<br>");
}
/* An iterative function to do preorder traversal
of binary tree and print root to leaf path
without using recursion */
function printRootToLeaf(root)
{
    // Corner Case
    if (root == null)
        return;

    // Create an empty stack and push root to it
    var nodeStack = [];
    nodeStack.push(root);

    // Create a map to store parent 
    // pointers of binary tree nodes
    var parent = new Map();

    // parent of root is NULL
    parent.set(root, null);

    /* pop all items one by one. Do following for
    every popped item
        a) push its right child and set its parent
        pointer
        b) push its left child and set its parent
        pointer
    Note that right child is pushed first so that
    left is processed first */
    while (nodeStack.length != 0)
    {
        // pop the top item from stack
        var current = nodeStack[nodeStack.length-1];
        nodeStack.pop();

        // If leaf node encountered, print Top To
        // Bottom path
        if (current.left == null && current.right == null)
            printTopToBottomPath(current, parent);

        // push right & left children of the popped node
        // to stack. Also set their parent pointer in
        // the map
        if (current.right != null)
        {
            parent.set(current.right,current);
            nodeStack.push(current.right);
        }
        if (current.left != null)
        {
            parent.set(current.left,current);
            nodeStack.push(current.left);
        }
    }
}

/* binary tree node */
class Node
{
  constructor(data)
  {
    this.left = null;
    this.data = data;
    this.right = null;
  }
}

// Driver code
var root = new Node(10);
root.left = new Node(8);
root.right = new Node(2);
root.left.left = new Node(3);
root.left.right = new Node(5);
root.right.left = new Node(2);
printRootToLeaf(root);

// This code is contributed by itsok.
</script>
```

**输出:**

```
10 8 3 
10 8 5 
10 2 2 
```

本文由**阿迪蒂亚·戈尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息