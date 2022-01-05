# 去除根到叶路径上的长度节点< K

> 原文:[https://www . geesforgeks . org/remove-nodes-root-leaf-path-length-k/](https://www.geeksforgeeks.org/remove-nodes-root-leaf-paths-length-k/)

给定一棵二叉树和一个数字 k，移除所有仅位于长度小于 k 的根到叶路径上的节点。如果一个节点 X 位于多个根到叶路径上，并且如果任何路径的路径长度> = k，则 X 不会从二叉树中删除。换句话说，如果经过一个节点的所有路径的长度都小于 k，则该节点被删除。考虑下面的二叉树
示例

```
               1
           /      \
         2          3
      /     \         \
    4         5        6
  /                   /
 7                   8 
Input: Root of above Binary Tree
       k = 4

Output: The tree should be changed to following  
           1
        /     \
      2          3
     /             \
   4                 6
 /                  /
7                  8
There are 3 paths 
i) 1->2->4->7      path length = 4
ii) 1->2->5        path length = 3
iii) 1->3->6->8    path length = 4 
There is only one path " 1->2->5 " of length smaller than 4\.  
The node 5 is the only node that lies only on this path, so 
node 5 is removed.
Nodes 2 and 1 are not removed as they are parts of other paths
of length 4 as well.

If k is 5 or greater than 5, then whole tree is deleted. 

If k is 3 or less than 3, then nothing is deleted.
```

**我们强烈建议尽量减少你的浏览器，先自己试试这个**
这里的想法是使用后序遍历树。在移除一个节点之前，我们需要检查该节点在较短路径中的所有子节点是否已经被移除。
有 2 种情况:
i)这个节点变成叶节点，在这种情况下需要删除。
ii)该节点在路径长度为> = k 的路径上有其他子节点，此时无需删除。
上述方式的实施如下:

## C++

```
// C++ program to remove nodes on root to leaf paths of length < K
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node *left, *right;
};

//New node of a tree
Node *newNode(int data)
{
    Node *node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Utility method that actually removes the nodes which are not
// on the pathLen >= k. This method can change the root as well.
Node *removeShortPathNodesUtil(Node *root, int level, int k)
{
    //Base condition
    if (root == NULL)
        return NULL;

    // Traverse the tree in postorder fashion so that if a leaf
    // node path length is shorter than k, then that node and
    // all of its descendants till the node which are not
    // on some other path are removed.
    root->left = removeShortPathNodesUtil(root->left, level + 1, k);
    root->right = removeShortPathNodesUtil(root->right, level + 1, k);

    // If root is a leaf node and it's level is less than k then
    // remove this node.
    // This goes up and check for the ancestor nodes also for the
    // same condition till it finds a node which is a part of other
    // path(s) too.
    if (root->left == NULL && root->right == NULL && level < k)
    {
        delete root;
        return NULL;
    }

    // Return root;
    return root;
}

// Method which calls the utility method to remove the short path
// nodes.
Node *removeShortPathNodes(Node *root, int k)
{
    int pathLen = 0;
    return removeShortPathNodesUtil(root, 1, k);
}

//Method to print the tree in inorder fashion.
void printInorder(Node *root)
{
    if (root)
    {
        printInorder(root->left);
        cout << root->data << " ";
        printInorder(root->right);
    }
}

// Driver method.
int main()
{
    int k = 4;
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->left->left = newNode(7);
    root->right->right = newNode(6);
    root->right->right->left = newNode(8);
    cout << "Inorder Traversal of Original tree" << endl;
    printInorder(root);
    cout << endl;
    cout << "Inorder Traversal of Modified tree" << endl;
    Node *res = removeShortPathNodes(root, k);
    printInorder(res);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove nodes on root to leaf paths of length < k

/* Class containing left and right child of current
   node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // Utility method that actually removes the nodes which are not
    // on the pathLen >= k. This method can change the root as well.
    Node removeShortPathNodesUtil(Node node, int level, int k)
    {
        //Base condition
        if (node == null)
            return null;

        // Traverse the tree in postorder fashion so that if a leaf
        // node path length is shorter than k, then that node and
        // all of its descendants till the node which are not
        // on some other path are removed.
        node.left = removeShortPathNodesUtil(node.left, level + 1, k);
        node.right = removeShortPathNodesUtil(node.right, level + 1, k);

        // If root is a leaf node and it's level is less than k then
        // remove this node.
        // This goes up and check for the ancestor nodes also for the
        // same condition till it finds a node which is a part of other
        // path(s) too.
        if (node.left == null && node.right == null && level < k)
            return null;

        // Return root;
        return node;
    }

    // Method which calls the utility method to remove the short path
    // nodes.
    Node removeShortPathNodes(Node node, int k)
    {
        int pathLen = 0;
        return removeShortPathNodesUtil(node, 1, k);
    }

    //Method to print the tree in inorder fashion.
    void printInorder(Node node)
    {
        if (node != null)
        {
            printInorder(node.left);
            System.out.print(node.data + " ");
            printInorder(node.right);
        }
    }

    // Driver program to test for samples
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        int k = 4;
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.left.left = new Node(7);
        tree.root.right.right = new Node(6);
        tree.root.right.right.left = new Node(8);
        System.out.println("The inorder traversal of original tree is : ");
        tree.printInorder(tree.root);
        Node res = tree.removeShortPathNodes(tree.root, k);
        System.out.println("");
        System.out.println("The inorder traversal of modified tree is : ");
        tree.printInorder(res);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to remove nodes on root
# to leaf paths of length < K

# New node of a tree
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Utility method that actually removes
# the nodes which are not on the pathLen >= k.
# This method can change the root as well.
def removeShortPathNodesUtil(root, level, k) :

    # Base condition
    if (root == None) :
        return None

    # Traverse the tree in postorder fashion
    # so that if a leaf node path length is
    # shorter than k, then that node and all
    # of its descendants till the node which 
    # are not on some other path are removed.
    root.left = removeShortPathNodesUtil(root.left,
                                         level + 1, k)
    root.right = removeShortPathNodesUtil(root.right,
                                          level + 1, k)

    # If root is a leaf node and it's level
    # is less than k then remove this node.
    # This goes up and check for the ancestor
    # nodes also for the same condition till
    # it finds a node which is a part of other
    # path(s) too.
    if (root.left == None and
        root.right == None and level < k) :
        return None

    # Return root
    return root

# Method which calls the utility method
# to remove the short path nodes.
def removeShortPathNodes(root, k) :
    pathLen = 0
    return removeShortPathNodesUtil(root, 1, k)

# Method to print the tree in
# inorder fashion.
def prInorder(root) :

    if (root) :

        prInorder(root.left)
        print(root.data, end = " " )
        prInorder(root.right)

# Driver Code
if __name__ == '__main__':
    k = 4
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.left.left.left = newNode(7)
    root.right.right = newNode(6)
    root.right.right.left = newNode(8)
    print("Inorder Traversal of Original tree" )
    prInorder(root)
    print()
    print("Inorder Traversal of Modified tree" )
    res = removeShortPathNodes(root, k)
    prInorder(res)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
using System;

// C# program to remove nodes on root to leaf paths of length < k

/* Class containing left and right child of current 
   node and key value*/
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

public class BinaryTree
{
    public Node root;

    // Utility method that actually removes the nodes which are not
    // on the pathLen >= k. This method can change the root as well.
    public virtual Node removeShortPathNodesUtil(Node node, int level, int k)
    {
        //Base condition
        if (node == null)
        {
            return null;
        }

        // Traverse the tree in postorder fashion so that if a leaf
        // node path length is shorter than k, then that node and
        // all of its descendants till the node which are not
        // on some other path are removed.
        node.left = removeShortPathNodesUtil(node.left, level + 1, k);
        node.right = removeShortPathNodesUtil(node.right, level + 1, k);

        // If root is a leaf node and it's level is less than k then
        // remove this node.
        // This goes up and check for the ancestor nodes also for the
        // same condition till it finds a node which is a part of other
        // path(s) too.
        if (node.left == null && node.right == null && level < k)
        {
            return null;
        }

        // Return root;
        return node;
    }

    // Method which calls the utility method to remove the short path
    // nodes.
    public virtual Node removeShortPathNodes(Node node, int k)
    {
        int pathLen = 0;
        return removeShortPathNodesUtil(node, 1, k);
    }

    //Method to print the tree in inorder fashion.
    public virtual void printInorder(Node node)
    {
        if (node != null)
        {
            printInorder(node.left);
            Console.Write(node.data + " ");
            printInorder(node.right);
        }
    }

    // Driver program to test for samples
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int k = 4;
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.left.left = new Node(7);
        tree.root.right.right = new Node(6);
        tree.root.right.right.left = new Node(8);
        Console.WriteLine("The inorder traversal of original tree is : ");
        tree.printInorder(tree.root);
        Node res = tree.removeShortPathNodes(tree.root, k);
        Console.WriteLine("");
        Console.WriteLine("The inorder traversal of modified tree is : ");
        tree.printInorder(res);
    }
}

  //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program to remove nodes on
    // root to leaf paths of length < k

    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root;

    // Utility method that actually removes the nodes which are not
    // on the pathLen >= k. This method can change the root as well.
    function removeShortPathNodesUtil(node, level, k)
    {
        //Base condition
        if (node == null)
            return null;

        // Traverse the tree in postorder fashion so that if a leaf
        // node path length is shorter than k, then that node and
        // all of its descendants till the node which are not
        // on some other path are removed.
        node.left = removeShortPathNodesUtil(node.left, level + 1, k);
        node.right = removeShortPathNodesUtil(node.right, level + 1, k);

        // If root is a leaf node and it's level is less than k then
        // remove this node.
        // This goes up and check for the ancestor nodes also for the
        // same condition till it finds a node which is a part of other
        // path(s) too.
        if (node.left == null && node.right == null && level < k)
            return null;

        // Return root;
        return node;
    }

    // Method which calls the utility method to remove the short path
    // nodes.
    function removeShortPathNodes(node, k)
    {
        let pathLen = 0;
        return removeShortPathNodesUtil(node, 1, k);
    }

    //Method to print the tree in inorder fashion.
    function printInorder(node)
    {
        if (node != null)
        {
            printInorder(node.left);
            document.write(node.data + " ");
            printInorder(node.right);
        }
    }

    let k = 4;
    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.left.left.left = new Node(7);
    root.right.right = new Node(6);
    root.right.right.left = new Node(8);
    document.write("The inorder traversal of Original tree is : " +
    "</br>");
    printInorder(root);
    let res = removeShortPathNodes(root, k);
    document.write("</br>");
    document.write("The inorder traversal of Modified tree is : " +
    "</br>");
    printInorder(res);

</script>
```

**输出:**

```
Inorder Traversal of Original tree
7 4 2 5 1 3 8 6
Inorder Traversal of Modified tree
7 4 2 1 3 8 6
```

上述解决方案的时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。

本文由**库马尔·高塔姆**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息