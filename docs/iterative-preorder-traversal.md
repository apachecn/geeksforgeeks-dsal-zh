# 迭代预序遍历

> 原文:[https://www.geeksforgeeks.org/iterative-preorder-traversal/](https://www.geeksforgeeks.org/iterative-preorder-traversal/)

给定一棵二叉树，编写一个迭代函数来打印给定二叉树的 Preorder 遍历。
二叉树的递归前序遍历参见[本](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。为了将固有的递归过程转换为迭代过程，我们需要一个显式堆栈。下面是一个简单的基于堆栈的迭代过程来打印 Preorder 遍历。
**1)** 创建一个空栈*节点栈*并将根节点推送到栈。
**2)** 当*节点堆栈*不为空时，执行以下操作。
…。 **a)** 从堆栈中弹出一个项目并打印。
…。 **b)** 将弹出项的右子项推至堆栈
…。 **c)** 将弹出项的左子推栈
将右子推在左子之前，确保先处理左子树。

## C++

```
// C++ program to implement iterative preorder traversal
#include <bits/stdc++.h>

using namespace std;

/* A binary tree node has data, left child and right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node with the given data and
   NULL left and right  pointers.*/
struct node* newNode(int data)
{
    struct node* node = new struct node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// An iterative process to print preorder traversal of Binary tree
void iterativePreorder(node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty stack and push root to it
    stack<node*> nodeStack;
    nodeStack.push(root);

    /* Pop all items one by one. Do following for every popped item
       a) print it
       b) push its right child
       c) push its left child
    Note that right child is pushed first so that left is processed first */
    while (nodeStack.empty() == false) {
        // Pop the top item from stack and print it
        struct node* node = nodeStack.top();
        printf("%d ", node->data);
        nodeStack.pop();

        // Push right and left children of the popped node to stack
        if (node->right)
            nodeStack.push(node->right);
        if (node->left)
            nodeStack.push(node->left);
    }
}

// Driver program to test above functions
int main()
{
    /* Constructed binary tree is
            10
          /   \
        8      2
      /  \    /
    3     5  2
  */
    struct node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->left = newNode(2);
    iterativePreorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement iterative preorder traversal
import java.util.Stack;

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {

    Node root;

    void iterativePreorder()
    {
        iterativePreorder(root);
    }

    // An iterative process to print preorder traversal of Binary tree
    void iterativePreorder(Node node)
    {

        // Base Case
        if (node == null) {
            return;
        }

        // Create an empty stack and push root to it
        Stack<Node> nodeStack = new Stack<Node>();
        nodeStack.push(root);

        /* Pop all items one by one. Do following for every popped item
         a) print it
         b) push its right child
         c) push its left child
         Note that right child is pushed first so that left is processed first */
        while (nodeStack.empty() == false) {

            // Pop the top item from stack and print it
            Node mynode = nodeStack.peek();
            System.out.print(mynode.data + " ");
            nodeStack.pop();

            // Push right and left children of the popped node to stack
            if (mynode.right != null) {
                nodeStack.push(mynode.right);
            }
            if (mynode.left != null) {
                nodeStack.push(mynode.left);
            }
        }
    }

    // driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(2);
        tree.iterativePreorder();
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to perform iterative preorder traversal

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# An iterative process to print preorder traversal of BT
def iterativePreorder(root):

    # Base CAse
    if root is None:
        return

    # create an empty stack and push root to it
    nodeStack = []
    nodeStack.append(root)

    # Pop all items one by one. Do following for every popped item
    # a) print it
    # b) push its right child
    # c) push its left child
    # Note that right child is pushed first so that left
    # is processed first */
    while(len(nodeStack) > 0):

        # Pop the top item from stack and print it
        node = nodeStack.pop()
        print (node.data, end=" ")

        # Push right and left children of the popped node
        # to stack
        if node.right is not None:
            nodeStack.append(node.right)
        if node.left is not None:
            nodeStack.append(node.left)

# Driver program to test above function
root = Node(10)
root.left = Node(8)
root.right = Node(2)
root.left.left = Node(3)
root.left.right = Node(5)
root.right.left = Node(2)
iterativePreorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to implement iterative
// preorder traversal
using System;
using System.Collections.Generic;

// A binary tree node
public class Node {
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG {
    public Node root;

    public virtual void iterativePreorder()
    {
        iterativePreorder(root);
    }

    // An iterative process to print preorder
    // traversal of Binary tree
    public virtual void iterativePreorder(Node node)
    {

        // Base Case
        if (node == null) {
            return;
        }

        // Create an empty stack and push root to it
        Stack<Node> nodeStack = new Stack<Node>();
        nodeStack.Push(root);

        /* Pop all items one by one. Do following
       for every popped item
    a) print it
    b) push its right child
    c) push its left child
    Note that right child is pushed first so
    that left is processed first */
        while (nodeStack.Count > 0) {

            // Pop the top item from stack and print it
            Node mynode = nodeStack.Peek();
            Console.Write(mynode.data + " ");
            nodeStack.Pop();

            // Push right and left children of
            // the popped node to stack
            if (mynode.right != null) {
                nodeStack.Push(mynode.right);
            }
            if (mynode.left != null) {
                nodeStack.Push(mynode.left);
            }
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        GFG tree = new GFG();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(2);
        tree.iterativePreorder();
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to implement iterative
// preorder traversal

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

var root = null;

// An iterative process to print preorder
// traversal of Binary tree
function iterativePreorder(node)
{

    // Base Case
    if (node == null)
    {
        return;
    }

    // Create an empty stack and push root to it
    var nodeStack = [];
    nodeStack.push(root);

    /* Pop all items one by one. Do following
    for every popped item
    a) print it
    b) push its right child
    c) push its left child
    Note that right child is pushed first so
    that left is processed first */
    while (nodeStack.length > 0)
    {

        // Pop the top item from stack and print it
        var mynode = nodeStack[nodeStack.length - 1];
        document.write(mynode.data + " ");
        nodeStack.pop();

        // Push right and left children of
        // the popped node to stack
        if (mynode.right != null)
        {
            nodeStack.push(mynode.right);
        }
        if (mynode.left != null)
        {
            nodeStack.push(mynode.left);
        }
    }
}

// Driver Code
root = new Node(10);
root.left = new Node(8);
root.right = new Node(2);
root.left.left = new Node(3);
root.left.right = new Node(5);
root.right.left = new Node(2);

iterativePreorder(root);

// This code is contributed by itsok

</script>
```

**Output:** 

```
10 8 3 5 2 2
```

**时间复杂度** : O(N)
**辅助空间** : O(N)，其中 N 为树中节点总数。

**空间优化解决方案**:思路是从根节点开始遍历树，边存在边继续打印左子，同时在一个辅助栈中推送每个节点的右子。一旦我们到达一个空节点，从辅助栈弹出一个右子栈，并在辅助栈不为空时重复这个过程。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Tree Node
struct Node {
    int data;
    Node *left, *right;

    Node(int data)
    {
        this->data = data;
        this->left = this->right = NULL;
    }
};

// Iterative function to do Preorder traversal of the tree
void preorderIterative(Node* root)
{
    if (root == NULL)
        return;

    stack<Node*> st;

    // start from root node (set current node to root node)
    Node* curr = root;

    // run till stack is not empty or current is
    // not NULL
    while (!st.empty() || curr != NULL) {
        // Print left children while exist
        // and keep pushing right into the
        // stack.
        while (curr != NULL) {
            cout << curr->data << " ";

            if (curr->right)
                st.push(curr->right);

            curr = curr->left;
        }

        // We reach when curr is NULL, so We
        // take out a right child from stack
        if (st.empty() == false) {
            curr = st.top();
            st.pop();
        }
    }
}

// Driver Code
int main()
{
    Node* root = new Node(10);
    root->left = new Node(20);
    root->right = new Node(30);
    root->left->left = new Node(40);
    root->left->left->left = new Node(70);
    root->left->right = new Node(50);
    root->right->left = new Node(60);
    root->left->left->right = new Node(80);

    preorderIterative(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Stack;

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree{

Node root;

void preorderIterative()
{
    preorderIterative(root);
}

// Iterative function to do Preorder
// traversal of the tree
void preorderIterative(Node node)
{
    if (node == null)
    {
        return;
    }

    Stack<Node> st = new Stack<Node>();

    // Start from root node (set curr
    // node to root node)
    Node curr = node;

    // Run till stack is not empty or
    // current is not NULL
    while (curr != null || !st.isEmpty())
    {

        // Print left children while exist
        // and keep pushing right into the 
        // stack.
        while (curr != null)
        {
            System.out.print(curr.data + " ");

            if (curr.right != null)
                st.push(curr.right);

            curr = curr.left;
        }

        // We reach when curr is NULL, so We
        // take out a right child from stack
        if (!st.isEmpty())
        {
            curr = st.pop();
        }
    }
}

// Driver code
public static void main(String args[])
{
    BinaryTree tree = new BinaryTree();

    tree.root = new Node(10);
    tree.root.left = new Node(20);
    tree.root.right = new Node(30);
    tree.root.left.left = new Node(40);
    tree.root.left.left.left = new Node(70);
    tree.root.left.right = new Node(50);
    tree.root.right.left = new Node(60);
    tree.root.left.left.right = new Node(80);

    tree.preorderIterative();
}
}

// This code is contributed by Vivek Singh Bhadauria
```

## 蟒蛇 3

```
# Tree Node
class Node:

    def __init__(self, data = 0):
        self.data = data
        self.left = None
        self.right = None

# Iterative function to do Preorder traversal of the tree
def preorderIterative(root):

    if (root == None):
        return

    st = []

    # start from root node (set current node to root node)
    curr = root

    # run till stack is not empty or current is
    # not NULL
    while (len(st) or curr != None):

        # Print left children while exist
        # and keep appending right into the
        # stack.
        while (curr != None):

            print(curr.data, end = " ")

            if (curr.right != None):
                st.append(curr.right)

            curr = curr.left

        # We reach when curr is NULL, so We
        # take out a right child from stack
        if (len(st) > 0):
            curr = st[-1]
            st.pop()

# Driver Code

root = Node(10)
root.left = Node(20)
root.right = Node(30)
root.left.left = Node(40)
root.left.left.left = Node(70)
root.left.right = Node(50)
root.right.left = Node(60)
root.left.left.right = Node(80)

preorderIterative(root)

# This code is contributed by Arnab Kundu
```

## C#

```
using System;
using System.Collections.Generic;

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

public class BinaryTree{

Node root;

void preorderIterative()
{
    preorderIterative(root);
}

// Iterative function to do Preorder
// traversal of the tree
void preorderIterative(Node node)
{
    if (node == null)
    {
        return;
    }

    Stack<Node> st = new Stack<Node>();

    // Start from root node (set curr
    // node to root node)
    Node curr = node;

    // Run till stack is not empty or
    // current is not NULL
    while (curr != null || st.Count!=0)
    {

        // Print left children while exist
        // and keep pushing right into the 
        // stack.
        while (curr != null)
        {
            Console.Write(curr.data + " ");

            if (curr.right != null)
                st.Push(curr.right);

            curr = curr.left;
        }

        // We reach when curr is NULL, so We
        // take out a right child from stack
        if (st.Count != 0)
        {
            curr = st.Pop();
        }
    }
}

// Driver code
public static void Main(String []args)
{
    BinaryTree tree = new BinaryTree();

    tree.root = new Node(10);
    tree.root.left = new Node(20);
    tree.root.right = new Node(30);
    tree.root.left.left = new Node(40);
    tree.root.left.left.left = new Node(70);
    tree.root.left.right = new Node(50);
    tree.root.right.left = new Node(60);
    tree.root.left.left.right = new Node(80);

    tree.preorderIterative();
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

class Node
{
    constructor(item)
    {
        this.left = null;
        this.right = null;
        this.data = item;
    }
}

let root;

// Iterative function to do Preorder
// traversal of the tree
function preorderiterative(node)
{
    if (node == null)
    {
        return;
    }

    let st = [];

    // Start from root node (set curr
    // node to root node)
    let curr = node;

    // Run till stack is not empty or
    // current is not NULL
    while (curr != null || st.length > 0)
    {

        // Print left children while exist
        // and keep pushing right into the
        // stack.
        while (curr != null)
        {
            document.write(curr.data + " ");

            if (curr.right != null)
                st.push(curr.right);

            curr = curr.left;
        }

        // We reach when curr is NULL, so We
        // take out a right child from stack
        if (st.length > 0)
        {
            curr = st.pop();
        }
    }
}

function preorderIterative()
{
    preorderiterative(root);
}

// Driver code
root = new Node(10);
root.left = new Node(20);
root.right = new Node(30);
root.left.left = new Node(40);
root.left.left.left = new Node(70);
root.left.right = new Node(50);
root.right.left = new Node(60);
root.left.left.right = new Node(80);

preorderIterative();

// This code is contributed by decode2207

</script>
```

**Output:** 

```
10 20 40 70 80 50 30 60
```

**时间复杂度** : O(N)
**辅助空间** : O(H)，其中 H 为树高。

本文由 Saurabh Sharma 编辑，GeeksforGeeks 团队审阅。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。