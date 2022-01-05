# 检查两个节点是否在根节点的同一个子树中

> 原文:[https://www . geesforgeks . org/check-如果两个节点在根节点的同一个子树中/](https://www.geeksforgeeks.org/check-if-two-nodes-are-in-same-subtree-of-the-root-node/)

给定一个具有不同节点的**二叉树**。给定两个节点**节点 1** 和**节点 2** ，检查这两个节点是否位于根节点的同一个子树中。也就是说，根节点的左右子树。

![](img/59b40bdc7f7089a3f266a51b2b763893.png)

**例如**:在上面的二叉树中，节点 **3 和 8** 在同一个子树中，但是 **4 和 5** 在不同的子树中。

**先决条件** : [检查二叉树](https://www.geeksforgeeks.org/search-a-node-in-binary-tree/)中是否存在节点。
这个想法类似于在二叉树中搜索一个节点。有四种不同的情况:

1.  如果节点 1 和节点 2 都在根节点的左子树中。
2.  如果节点 1 和节点 2 都在根节点的右子树中。
3.  如果节点 1 在根节点的左子树中，节点 2 在根节点的右子树中。
4.  如果节点 1 在根节点的右子树中，节点 2 在根节点的左子树中。

使用在二叉树中搜索节点的方法，检查上面列出的前两种情况是否为真。如果上面列出的前两种情况中的任何一种被发现为真，则打印是，否则打印否
下面是上述方法的实现:

## C++

```
// C++ program to check if two nodes
// are in same subtrees of the root node

#include <iostream>
using namespace std;

// Binary tree node
struct Node {
    int data;
    struct Node *left, *right;
    Node(int data)
    {
        this->data = data;
        left = right = NULL;
    }
};

// Function to traverse the tree in preorder
// and check if the given node exists in
// a binary tree
bool ifNodeExists(struct Node* node, int key)
{
    if (node == NULL)
        return false;

    if (node->data == key)
        return true;

    /* then recur on left subtree */
    bool res1 = ifNodeExists(node->left, key);

    /* now recur on right subtree */
    bool res2 = ifNodeExists(node->right, key);

    return res1 || res2;
}

// Function to check if the two given nodes
// are in same subtrees of the root node
bool ifSameSubTree(Node* root, int node1, int node2)
{
    if (root == NULL)
       return false;

    // CASE 1: If both nodes are in left subtree
    if (ifNodeExists(root->left, node1)
        && ifNodeExists(root->left, node2)) {
        return true;
    }

    // CASE 2: If both nodes are in right subtree
    else if (ifNodeExists(root->right, node1)
             && ifNodeExists(root->right, node2)) {
        return true;
    }

    // CASE 3 and 4: Nodes are in different subtrees
    else
        return false;
}

// Driver Code
int main()
{
    struct Node* root = new Node(0);
    root->left = new Node(1);
    root->left->left = new Node(3);
    root->left->left->left = new Node(7);
    root->left->right = new Node(4);
    root->left->right->left = new Node(8);
    root->left->right->right = new Node(9);
    root->right = new Node(2);
    root->right->left = new Node(5);
    root->right->right = new Node(6);

    int node1 = 3, node2 = 8;

    if (ifSameSubTree(root, node1, node2))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two nodes
// are in same subtrees of the root node
import java.util.*;
class solution
{

// Binary tree node
 static class Node {
    int data;
     Node left, right;
    Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Function to traverse the tree in preorder
// and check if the given node exists in
// a binary tree
static boolean ifNodeExists( Node node, int key)
{
    if (node == null)
        return false;

    if (node.data == key)
        return true;

    /* then recur on left subtree */
    boolean res1 = ifNodeExists(node.left, key);

    /* now recur on right subtree */
    boolean res2 = ifNodeExists(node.right, key);

    return res1 || res2;
}

// Function to check if the two given nodes
// are in same subtrees of the root node
static boolean ifSameSubTree(Node root, int node1, int node2)
{
    if (root == null)
    return false;

    // CASE 1: If both nodes are in left subtree
    if (ifNodeExists(root.left, node1)
        && ifNodeExists(root.left, node2)) {
        return true;
    }

    // CASE 2: If both nodes are in right subtree
    else if (ifNodeExists(root.right, node1)
            && ifNodeExists(root.right, node2)) {
        return true;
    }

    // CASE 3 and 4: Nodes are in different subtrees
    else
        return false;
}

// Driver Code
public static void main(String args[])
{
     Node root = new Node(0);
    root.left = new Node(1);
    root.left.left = new Node(3);
    root.left.left.left = new Node(7);
    root.left.right = new Node(4);
    root.left.right.left = new Node(8);
    root.left.right.right = new Node(9);
    root.right = new Node(2);
    root.right.left = new Node(5);
    root.right.right = new Node(6);

    int node1 = 3, node2 = 8;

    if (ifSameSubTree(root, node1, node2))
        System.out.println("YES");
    else
        System.out.println( "NO");

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
"""Python3 program to check if two nodes
are in same subtrees of the root node """

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data= data
        self.left = None
        self.right = None
        self.visited = False

# Function to traverse the tree in
# preorder and check if the given
# node exists in a binary tree
def ifNodeExists(node, key) :
    if (node == None):
        return False

    if (node.data == key):
        return True

    """ then recur on left subtree """
    res1 = ifNodeExists(node.left, key)

    """ now recur on right subtree """
    res2 = ifNodeExists(node.right, key)

    return res1 or res2

# Function to check if the two given nodes
# are in same subtrees of the root node
def ifSameSubTree(root, node1, node2):

    if (root == None) :
        return False

    # CASE 1: If both nodes are in
    # left subtree
    if (ifNodeExists(root.left, node1)
        and ifNodeExists(root.left, node2)):
        return True

    # CASE 2: If both nodes are in
    # right subtree
    elif (ifNodeExists(root.right, node1)
            and ifNodeExists(root.right, node2)):
        return True

    # CASE 3 and 4: Nodes are in
    # different subtrees
    else:
        return False

# Driver Code
if __name__ == '__main__':
    root = newNode(0)
    root.left = newNode(1)
    root.left.left = newNode(3)
    root.left.left.left = newNode(7)
    root.left.right = newNode(4)
    root.left.right.left = newNode(8)
    root.left.right.right = newNode(9)
    root.right = newNode(2)
    root.right.left = newNode(5)
    root.right.right = newNode(6)

    node1 = 3
    node2 = 8

    if (ifSameSubTree(root, node1, node2)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to check if two nodes
// are in same subtrees of the root node
using System;

class GFG
{

// Binary tree node
class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Function to traverse the tree in preorder
// and check if the given node exists in
// a binary tree
static bool ifNodeExists( Node node, int key)
{
    if (node == null)
        return false;

    if (node.data == key)
        return true;

    /* then recur on left subtree */
    bool res1 = ifNodeExists(node.left, key);

    /* now recur on right subtree */
    bool res2 = ifNodeExists(node.right, key);

    return res1 || res2;
}

// Function to check if the two given nodes
// are in same subtrees of the root node
static bool ifSameSubTree(Node root,
                int node1, int node2)
{
    if (root == null)
    return false;

    // CASE 1: If both nodes are in left subtree
    if (ifNodeExists(root.left, node1)
        && ifNodeExists(root.left, node2))
    {
        return true;
    }

    // CASE 2: If both nodes are in right subtree
    else if (ifNodeExists(root.right, node1)
            && ifNodeExists(root.right, node2))
    {
        return true;
    }

    // CASE 3 and 4: Nodes are in different subtrees
    else
        return false;
}

// Driver Code
public static void Main()
{
    Node root = new Node(0);
    root.left = new Node(1);
    root.left.left = new Node(3);
    root.left.left.left = new Node(7);
    root.left.right = new Node(4);
    root.left.right.left = new Node(8);
    root.left.right.right = new Node(9);
    root.right = new Node(2);
    root.right.left = new Node(5);
    root.right.right = new Node(6);

    int node1 = 3, node2 = 8;

    if (ifSameSubTree(root, node1, node2))
        Console.WriteLine("YES");
    else
        Console.WriteLine( "NO");

}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

// JavaScript program to check if two nodes
// are in same subtrees of the root node

    // Binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    // Function to traverse the tree in preorder
    // and check if the given node exists in
    // a binary tree
    function ifNodeExists(node , key) {
        if (node == null)
            return false;

        if (node.data == key)
            return true;

        /* then recur on left subtree */
        var res1 = ifNodeExists(node.left, key);

        /* now recur on right subtree */
        var res2 = ifNodeExists(node.right, key);

        return res1 || res2;
    }

    // Function to check if the two given nodes
    // are in same subtrees of the root node
    function ifSameSubTree(root , node1 , node2) {
        if (root == null)
            return false;

        // CASE 1: If both nodes are in left subtree
        if (ifNodeExists(root.left, node1) &&
        ifNodeExists(root.left, node2)) {
            return true;
        }

        // CASE 2: If both nodes are in right subtree
        else if (ifNodeExists(root.right, node1) &&
        ifNodeExists(root.right, node2)) {
            return true;
        }

        // CASE 3 and 4: Nodes are in different subtrees
        else
            return false;
    }

    // Driver Code

        var root = new Node(0);
        root.left = new Node(1);
        root.left.left = new Node(3);
        root.left.left.left = new Node(7);
        root.left.right = new Node(4);
        root.left.right.left = new Node(8);
        root.left.right.right = new Node(9);
        root.right = new Node(2);
        root.right.left = new Node(5);
        root.right.right = new Node(6);

        var node1 = 3, node2 = 8;

        if (ifSameSubTree(root, node1, node2))
            document.write("YES");
        else
            document.write("NO");

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
YES
```