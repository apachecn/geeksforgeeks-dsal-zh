# 将二叉树转换为线程二叉树|集合 2(高效)

> 原文:[https://www . geesforgeks . org/convert-二叉树-线程-二叉树-集合-2-高效/](https://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree-set-2-efficient/)

[线程二叉树](http://geeksquiz.com/threaded-binary-tree/)的思想是为了让有序遍历更快，做到无栈无递归。在一个简单的线程二叉树中，空右指针被用来存储后续数据。当右指针为空时，它被用来存储后续数据。
下图显示了一个单线程二叉树的例子。虚线代表螺纹。

![threadedBT](img/abdc49bbfde3b2352262a2bd1161d6dd.png)

下面是单线程二叉树的结构。

## C

```
struct Node
{
    int key;
    Node *left, *right;

    // Used to indicate whether the right pointer is a normal right
    // pointer or a pointer to inorder successor.
    bool isThreaded;
};
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static class Node
{
    int key;
    Node left, right;

    // Used to indicate whether the right pointer is a normal right
    // pointer or a pointer to inorder successor.
    boolean isThreaded;
};

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
class Node:
    def __init__(self, data):
        self.key = data;
        self.left = none;
        self.right = none;
        self.isThreaded = false;
    # Used to indicate whether the right pointer is a normal right
    # pointer or a pointer to inorder successor.

# This code is contributed by umadevi9616
```

## C#

```
public class Node {
    public int key;
    public Node left, right;

    // Used to indicate whether the right pointer is a normal right
    // pointer or a pointer to inorder successor.
    public bool isThreaded;
};

// This code is contributed by umadevi9616
```

## java 描述语言

```
/* structure of a node in threaded binary tree */
 class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;

    // Used to indicate whether the right pointer
    // is a normal right pointer or a pointer
    // to inorder successor.
    this.isThreaded = false;
    }
    }

    // This code is contributed by famously.
```

**如何将给定的二叉树转换成线程二叉树？**
我们已经讨论了基于队列的解决方案。在这篇文章中，讨论了不需要队列的节省空间的解决方案。
这个想法是基于这样一个事实，即我们从一个有序的前身链接到一个节点。我们链接那些位于节点子树中的有序前身。因此，如果一个节点的左边不为空，我们会找到它的前一个节点。节点的前一个节点(其左边为空)是左子节点中最右边的节点。一旦我们找到了前身，我们就从它链接一个线程到当前节点。
以下是上述思路的实现。

## C++

```
/* C++ program to convert a Binary Tree to
    Threaded Tree */
#include <bits/stdc++.h>
using namespace std;

/* Structure of a node in threaded binary tree */
struct Node
{
    int key;
    Node *left, *right;

    // Used to indicate whether the right pointer
    // is a normal right pointer or a pointer
    // to inorder successor.
    bool isThreaded;
};

// Converts tree with given root to threaded
// binary tree.
// This function returns rightmost child of
// root.
Node *createThreaded(Node *root)
{
    // Base cases : Tree is empty or has single
    //              node
    if (root == NULL)
        return NULL;
    if (root->left == NULL &&
        root->right == NULL)
        return root;

    // Find predecessor if it exists
    if (root->left != NULL)
    {
        // Find predecessor of root (Rightmost
        // child in left subtree)
        Node* l = createThreaded(root->left);

        // Link a thread from predecessor to
        // root.
        l->right = root;
        l->isThreaded = true;
    }

    // If current node is rightmost child
    if (root->right == NULL)
        return root;

    // Recur for right subtree.
    return createThreaded(root->right);
}

// A utility function to find leftmost node
// in a binary tree rooted with 'root'.
// This function is used in inOrder()
Node *leftMost(Node *root)
{
    while (root != NULL && root->left != NULL)
        root = root->left;
    return root;
}

// Function to do inorder traversal of a threadded
// binary tree
void inOrder(Node *root)
{
    if (root == NULL) return;

    // Find the leftmost node in Binary Tree
    Node *cur = leftMost(root);

    while (cur != NULL)
    {
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
Node *newNode(int key)
{
    Node *temp = new Node;
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
         4  5 6  7   */
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    createThreaded(root);

    cout << "Inorder traversal of created "
            "threaded tree is\n";
    inOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to convert a Binary Tree to
    Threaded Tree */
import java.util.*;
class solution
{

/* structure of a node in threaded binary tree */
static class Node
{
    int key;
    Node left, right;

    // Used to indicate whether the right pointer
    // is a normal right pointer or a pointer
    // to inorder successor.
    boolean isThreaded;
};

// Converts tree with given root to threaded
// binary tree.
// This function returns rightmost child of
// root.
static Node createThreaded(Node root)
{
    // Base cases : Tree is empty or has single
    //              node
    if (root == null)
        return null;
    if (root.left == null &&
        root.right == null)
        return root;

    // Find predecessor if it exists
    if (root.left != null)
    {
        // Find predecessor of root (Rightmost
        // child in left subtree)
        Node l = createThreaded(root.left);

        // Link a thread from predecessor to
        // root.
        l.right = root;
        l.isThreaded = true;
    }

    // If current node is rightmost child
    if (root.right == null)
        return root;

    // Recur for right subtree.
    return createThreaded(root.right);
}

// A utility function to find leftmost node
// in a binary tree rooted with 'root'.
// This function is used in inOrder()
static Node leftMost(Node root)
{
    while (root != null && root.left != null)
        root = root.left;
    return root;
}

// Function to do inorder traversal of a threadded
// binary tree
static void inOrder(Node root)
{
    if (root == null) return;

    // Find the leftmost node in Binary Tree
    Node cur = leftMost(root);

    while (cur != null)
    {
        System.out.print(cur.key + " ");

        // If this Node is a thread Node, then go to
        // inorder successor
        if (cur.isThreaded)
            cur = cur.right;

        else // Else go to the leftmost child in right subtree
            cur = leftMost(cur.right);
    }
}

// A utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.left = temp.right = null;
    temp.key = key;
    return temp;
}

// Driver program to test above functions
public static void main(String args[])
{
   /*       1
            / \
           2   3
          / \ / \
         4  5 6  7   */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    createThreaded(root);

    System.out.println("Inorder traversal of created "+"threaded tree is\n");
    inOrder(root); 
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to convert a Binary Tree to
# Threaded Tree

# A utility function to create a new node
class newNode:
    def __init__(self, key):
        self.left = self.right = None
        self.key = key
        self.isThreaded = None

# Converts tree with given root to threaded
# binary tree.
# This function returns rightmost child of
# root.
def createThreaded(root):

    # Base cases : Tree is empty or has 
    #               single node
    if root == None:
        return None
    if root.left == None and root.right == None:
        return root

    # Find predecessor if it exists
    if root.left != None:

        # Find predecessor of root (Rightmost
        # child in left subtree)
        l = createThreaded(root.left)

        # Link a thread from predecessor
        # to root.
        l.right = root
        l.isThreaded = True

    # If current node is rightmost child
    if root.right == None:
        return root

    # Recur for right subtree.
    return createThreaded(root.right)

# A utility function to find leftmost node
# in a binary tree rooted with 'root'.
# This function is used in inOrder()
def leftMost(root):
    while root != None and root.left != None:
        root = root.left
    return root

# Function to do inorder traversal of a
# threaded binary tree
def inOrder(root):
    if root == None:
        return

    # Find the leftmost node in Binary Tree
    cur = leftMost(root)

    while cur != None:
        print(cur.key, end = " ")

        # If this Node is a thread Node, then
        # go to inorder successor
        if cur.isThreaded:
            cur = cur.right

        else: # Else go to the leftmost child
              # in right subtree
            cur = leftMost(cur.right)

# Driver Code
if __name__ == '__main__':

    #         1
    #     / \
    #     2 3
    #     / \ / \
    #     4 5 6 7
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)

    createThreaded(root)

    print("Inorder traversal of created",
                      "threaded tree is")
    inOrder(root)

# This code is contributed by PranchalK
```

## C#

```
using System;

/* C# program to convert a Binary Tree to 
    Threaded Tree */
public class solution
{

/* structure of a node in threaded binary tree */
public class Node
{
    public int key;
    public Node left, right;

    // Used to indicate whether the right pointer 
    // is a normal right pointer or a pointer 
    // to inorder successor. 
    public bool isThreaded;
}

// Converts tree with given root to threaded 
// binary tree. 
// This function returns rightmost child of 
// root. 
public static Node createThreaded(Node root)
{
    // Base cases : Tree is empty or has single 
    //              node 
    if (root == null)
    {
        return null;
    }
    if (root.left == null && root.right == null)
    {
        return root;
    }

    // Find predecessor if it exists 
    if (root.left != null)
    {
        // Find predecessor of root (Rightmost 
        // child in left subtree) 
        Node l = createThreaded(root.left);

        // Link a thread from predecessor to 
        // root. 
        l.right = root;
        l.isThreaded = true;
    }

    // If current node is rightmost child 
    if (root.right == null)
    {
        return root;
    }

    // Recur for right subtree. 
    return createThreaded(root.right);
}

// A utility function to find leftmost node 
// in a binary tree rooted with 'root'. 
// This function is used in inOrder() 
public static Node leftMost(Node root)
{
    while (root != null && root.left != null)
    {
        root = root.left;
    }
    return root;
}

// Function to do inorder traversal of a threadded 
// binary tree 
public static void inOrder(Node root)
{
    if (root == null)
    {
        return;
    }

    // Find the leftmost node in Binary Tree 
    Node cur = leftMost(root);

    while (cur != null)
    {
        Console.Write(cur.key + " ");

        // If this Node is a thread Node, then go to 
        // inorder successor 
        if (cur.isThreaded)
        {
            cur = cur.right;
        }

        else // Else go to the leftmost child in right subtree
        {
            cur = leftMost(cur.right);
        }
    }
}

// A utility function to create a new node 
public static Node newNode(int key)
{
    Node temp = new Node();
    temp.left = temp.right = null;
    temp.key = key;
    return temp;
}

// Driver program to test above functions 
public static void Main(string[] args)
{
   /*       1 
            / \ 
           2   3 
          / \ / \ 
         4  5 6  7   */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    createThreaded(root);

    Console.WriteLine("Inorder traversal of created " + "threaded tree is\n");
    inOrder(root);
}
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
/* javascript program to convert a Binary Tree to
    Threaded Tree */

/* structure of a node in threaded binary tree */
 class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;

    // Used to indicate whether the right pointer
    // is a normal right pointer or a pointer
    // to inorder successor.
    this.isThreaded = false;
    }
    }

// Converts tree with given root to threaded
// binary tree.
// This function returns rightmost child of
// root.
function createThreaded(root)
{
    // Base cases : Tree is empty or has single
    //              node
    if (root == null)
        return null;
    if (root.left == null &&
        root.right == null)
        return root;

    // Find predecessor if it exists
    if (root.left != null)
    {
        // Find predecessor of root (Rightmost
        // child in left subtree)
        var l = createThreaded(root.left);

        // Link a thread from predecessor to
        // root.
        l.right = root;
        l.isThreaded = true;
    }

    // If current node is rightmost child
    if (root.right == null)
        return root;

    // Recur for right subtree.
    return createThreaded(root.right);
}

// A utility function to find leftmost node
// in a binary tree rooted with 'root'.
// This function is used in inOrder()
function leftMost(root)
{
    while (root != null && root.left != null)
        root = root.left;
    return root;
}

// Function to do inorder traversal of a threadded
// binary tree
function inOrder(root)
{
    if (root == null) return;

    // Find the leftmost node in Binary Tree
    var cur = leftMost(root);

    while (cur != null)
    {
        document.write(cur.key + " ");

        // If this Node is a thread Node, then go to
        // inorder successor
        if (cur.isThreaded)
            cur = cur.right;

        else // Else go to the leftmost child in right subtree
            cur = leftMost(cur.right);
    }
}

// A utility function to create a new node
function newNode(key)
{
    var temp = new Node();
    temp.left = temp.right = null;
    temp.key = key;
    return temp;
}

// Driver program to test above functions

   /*       1
            / \
           2   3
          / \ / \
         4  5 6  7   */
    var root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    createThreaded(root);

    document.write("Inorder traversal of created "+"threaded tree is<br/>");
    inOrder(root); 

// This code contributed by aashish1995
</script>
```

**输出:**

```
Inorder traversal of created threaded tree is
4 2 5 1 6 3 7
```

该算法工作在 O(n)时间复杂度和 O(1)空间，而不是函数调用栈。

本文由 **Gopal Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。