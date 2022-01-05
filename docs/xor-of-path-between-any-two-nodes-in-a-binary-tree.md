# 二叉树中任意两个节点之间路径的异或

> 原文:[https://www . geesforgeks . org/二叉树中任意两个节点之间路径的异或/](https://www.geeksforgeeks.org/xor-of-path-between-any-two-nodes-in-a-binary-tree/)

给定具有不同节点和一对两个节点的二叉树。任务是找到给定两个节点之间路径上所有节点的异或。

![](img/e7a5527e0835931600c29cf52ce2408b.png)

**例如**，在上面的二叉树中对于节点 **(3，5)** 路径的异或将是(3 异或 1 异或 0 异或 2 异或 5) = 5。

其思想是利用异或的这两个性质:

*   相同元素的异或为零。
*   元素与零的异或得到元素本身。

现在，对于每个节点，沿着从根到该节点的路径查找并存储异或。这可以使用简单的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 来完成。现在任意两个节点之间的异或路径将是:

```
(XOR of path from root to first node) XOR (XOR of path from root to second node)
```

**解释**:出现了两种不同的情况:

1.  **如果两个节点在根节点的不同子树**中。一个在左子树，另一个在右子树。在这种情况下，很明显，上面写的公式将给出正确的结果，因为节点之间的路径通过根与所有不同的节点。
2.  **如果节点在同一个子树中**。要么在左子树，要么在右子树。在这种情况下，您需要观察从根到两个节点的路径将有一个交点，在该交点之前，从根到两个节点的路径是公共的。该公共路径的异或计算两次并抵消，因此不会影响结果。

**注**:对于单对节点，不需要存储从根到所有节点的路径。考虑到是否有节点对的列表，并且对于每一对，我们必须找到二叉树中两个节点之间路径的异或，这是有效的和书面的。
以下是上述办法的实施情况:

## C++

```
// C++ program to find XOR of path between
// any two nodes in a Binary Tree
#include <bits/stdc++.h>
using namespace std;

// structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* getNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function to store XOR of path from
// root to every node
// mp[x] will store XOR of path from root to node x
void storePath(Node* root, unordered_map<int, int>& mp, int XOR)
{
    // if root is NULL
    // there is no path
    if (!root)
        return;

    mp.insert(make_pair(root->data, XOR ^ root->data));

    XOR ^= root->data;

    if (root->left)
        storePath(root->left, mp, XOR);

    if (root->right)
        storePath(root->right, mp, XOR);
}

// Function to get XOR of nodes between any two nodes
int findXORPath(unordered_map<int, int> mp, int node1, int node2)
{
    return mp[node1] ^ mp[node2];
}

// Driver Code
int main()
{
    // binary tree formation
    struct Node* root = getNode(0);
    root->left = getNode(1);
    root->left->left = getNode(3);
    root->left->left->left = getNode(7);
    root->left->right = getNode(4);
    root->left->right->left = getNode(8);
    root->left->right->right = getNode(9);
    root->right = getNode(2);
    root->right->left = getNode(5);
    root->right->right = getNode(6);

    int XOR = 0;
    unordered_map<int, int> mp;

    int node1 = 3;
    int node2 = 5;

    // Store XOR path from root to every node
    storePath(root, mp, XOR);

    cout << findXORPath(mp, node1, node2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of path between
// any two nodes in a Binary Tree
import java.util.*;
class Solution
{

// structure of a node of binary tree
static class Node {
    int data;
    Node left, right;
}

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
 static Node getNode(int data)
{
     Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// Function to store XOR of path from
// root to every node
// mp[x] will store XOR of path from root to node x
static void storePath(Node root, Map<Integer, Integer> mp, int XOR)
{
    // if root is null
    // there is no path
    if (root==null)
        return;

    mp.put(root.data, XOR ^ root.data);

    XOR ^= root.data;

    if (root.left!=null)
        storePath(root.left, mp, XOR);

    if (root.right!=null)
        storePath(root.right, mp, XOR);
}

// Function to get XOR of nodes between any two nodes
static int findXORPath(Map<Integer, Integer> mp, int node1, int node2)
{
    return mp.get(node1) ^ mp.get(node2);
}

// Driver Code
public static void main(String args[])
{
    // binary tree formation
     Node root = getNode(0);
    root.left = getNode(1);
    root.left.left = getNode(3);
    root.left.left.left = getNode(7);
    root.left.right = getNode(4);
    root.left.right.left = getNode(8);
    root.left.right.right = getNode(9);
    root.right = getNode(2);
    root.right.left = getNode(5);
    root.right.right = getNode(6);

    int XOR = 0;
    Map<Integer, Integer> mp= new HashMap<Integer, Integer>();

    int node1 = 3;
    int node2 = 5;

    // Store XOR path from root to every node
    storePath(root, mp, XOR);

    System.out.println( findXORPath(mp, node1, node2));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find XOR of path between
# any two nodes in a Binary Tree

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates a node with the
# given data and None left and right pointers.
def getNode(data):

    newNode = Node(0)
    newNode.data = data
    newNode.left = newNode.right = None
    return newNode

mp = dict()

# Function to store XOR of path from
# root to every node
# mp[x] will store XOR of path from root to node x
def storePath( root, XOR) :
    global mp

    # if root is None
    # there is no path
    if (root == None) :
        return

    mp[root.data] = XOR ^ root.data;

    XOR = XOR ^ root.data

    if (root.left != None):
        storePath(root.left, XOR)

    if (root.right != None) :
        storePath(root.right, XOR)

# Function to get XOR of nodes between any two nodes
def findXORPath( node1, node2) :
    global mp
    return mp.get(node1,0) ^ mp.get(node2,0)

# Driver Code

# binary tree formation
root = getNode(0)
root.left = getNode(1)
root.left.left = getNode(3)
root.left.left.left = getNode(7)
root.left.right = getNode(4)
root.left.right.left = getNode(8)
root.left.right.right = getNode(9)
root.right = getNode(2)
root.right.left = getNode(5)
root.right.right = getNode(6)

XOR = 0

node1 = 3
node2 = 5

# Store XOR path from root to every node
storePath(root, XOR)

print( findXORPath( node1, node2))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to find XOR of path between
// any two nodes in a Binary Tree
using System;
using System.Collections.Generic;

class GFG
{

    // structure of a node of binary tree
    class Node
    {
        public int data;
        public Node left, right;
    }

    /* Helper function that allocates
    a new node with the given data and
     null left and right pointers. */
    static Node getNode(int data)
    {
        Node newNode = new Node();
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
    }

    // Function to store XOR of path from
    // root to every node
    // mp[x] will store XOR of path from root to node x
    static void storePath(Node root,
                Dictionary<int, int> mp, int XOR)
    {
        // if root is null
        // there is no path
        if (root == null)
            return;

        mp.Add(root.data, XOR ^ root.data);

        XOR ^= root.data;

        if (root.left != null)
            storePath(root.left, mp, XOR);

        if (root.right != null)
            storePath(root.right, mp, XOR);
    }

    // Function to get XOR of nodes between any two nodes
    static int findXORPath(Dictionary<int, int> mp,
                            int node1, int node2)
    {
        return mp[node1] ^ mp[node2];
    }

    // Driver Code
    public static void Main()
    {
        // binary tree formation
        Node root = getNode(0);
        root.left = getNode(1);
        root.left.left = getNode(3);
        root.left.left.left = getNode(7);
        root.left.right = getNode(4);
        root.left.right.left = getNode(8);
        root.left.right.right = getNode(9);
        root.right = getNode(2);
        root.right.left = getNode(5);
        root.right.right = getNode(6);

        int XOR = 0;
        Dictionary<int, int> mp = new Dictionary<int, int>();

        int node1 = 3;
        int node2 = 5;

        // Store XOR path from root to every node
        storePath(root, mp, XOR);

        Console.WriteLine( findXORPath(mp, node1, node2));
    }
}

/* This code is contributed PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript program to find XOR of path between
    // any two nodes in a Binary Tree

    // structure of a node of binary tree
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    /* Helper function that allocates a new node with the
    given data and null left and right pointers. */
    function getNode(data)
    {
        let newNode = new Node(data);
        return newNode;
    }

    // Function to store XOR of path from
    // root to every node
    // mp[x] will store XOR of path from root to node x
    function storePath(root, mp, XOR)
    {
        // if root is null
        // there is no path
        if (root==null)
            return;

        mp.set(root.data, XOR ^ root.data);

        XOR ^= root.data;

        if (root.left!=null)
            storePath(root.left, mp, XOR);

        if (root.right!=null)
            storePath(root.right, mp, XOR);
    }

    // Function to get XOR of nodes between any two nodes
    function findXORPath(mp, node1, node2)
    {
        return mp.get(node1) ^ mp.get(node2);
    }

    // binary tree formation
    let root = getNode(0);
    root.left = getNode(1);
    root.left.left = getNode(3);
    root.left.left.left = getNode(7);
    root.left.right = getNode(4);
    root.left.right.left = getNode(8);
    root.left.right.right = getNode(9);
    root.right = getNode(2);
    root.right.left = getNode(5);
    root.right.right = getNode(6);

    let XOR = 0;
    let mp= new Map();

    let node1 = 3;
    let node2 = 5;

    // Store XOR path from root to every node
    storePath(root, mp, XOR);

    document.write(findXORPath(mp, node1, node2));

</script>
```

**Output:** 

```
5
```

**时间复杂度** : O(N)
**辅助空间** : O(N)，其中 N 为节点数。