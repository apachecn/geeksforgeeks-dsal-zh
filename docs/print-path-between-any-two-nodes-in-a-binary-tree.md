# 打印二叉树中任意两个节点之间的路径

> 原文:[https://www . geesforgeks . org/print-二叉树中任意两个节点之间的路径/](https://www.geeksforgeeks.org/print-path-between-any-two-nodes-in-a-binary-tree/)

给定由不同节点和一对节点组成的二叉树。任务是找到并打印二叉树中两个给定节点之间的路径。

![](img/e7a5527e0835931600c29cf52ce2408b.png)

**例如**，在上面的二叉树中节点 **7 和 4** 之间的路径是 **7 - > 3 - > 1 - > 4** 。

这个想法是[找到从根节点到两个节点](https://www.geeksforgeeks.org/print-path-root-given-node-binary-tree/)的路径，并将它们存储在两个独立的向量或数组中，比如路径 1 和路径 2。
现在，出现了两种不同的情况:

1.  **如果两个节点在根节点的不同子树中**。一个在左子树，另一个在右子树。在这种情况下，很明显根节点将位于从节点 1 到节点 2 的路径之间。因此，以相反的顺序打印路径 1，然后打印路径 2。
2.  **如果节点在同一个子树中**。要么在左子树，要么在右子树。在这种情况下，您需要观察从根节点到两个节点的路径将有一个交叉点，在此之前，从根节点到两个节点的路径是公共的。找到该交点，并以类似于上述情况的方式从该点打印节点。

以下是上述方法的实现:

## C++

```
// C++ program to print path between any
// two nodes in a Binary Tree
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

// Function to check if there is a path from root
// to the given node. It also populates
// 'arr' with the given path
bool getPath(Node* root, vector<int>& arr, int x)
{
    // if root is NULL
    // there is no path
    if (!root)
        return false;

    // push the node's value in 'arr'
    arr.push_back(root->data);

    // if it is the required node
    // return true
    if (root->data == x)
        return true;

    // else check whether the required node lies
    // in the left subtree or right subtree of
    // the current node
    if (getPath(root->left, arr, x) || getPath(root->right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from
    // 'arr'and then return false
    arr.pop_back();
    return false;
}

// Function to print the path between
// any two nodes in a binary tree
void printPathBetweenNodes(Node* root, int n1, int n2)
{
    // vector to store the path of
    // first node n1 from root
    vector<int> path1;

    // vector to store the path of
    // second node n2 from root
    vector<int> path2;

    getPath(root, path1, n1);
    getPath(root, path2, n2);

    int intersection = -1;

    // Get intersection point
    int i = 0, j = 0;
    while (i != path1.size() || j != path2.size()) {

        // Keep moving forward until no intersection
        // is found
        if (i == j && path1[i] == path2[j]) {
            i++;
            j++;
        }
        else {
            intersection = j - 1;
            break;
        }
    }

    // Print the required path
    for (int i = path1.size() - 1; i > intersection; i--)
        cout << path1[i] << " ";

    for (int i = intersection; i < path2.size(); i++)
        cout << path2[i] << " ";
}

// Driver program
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

    int node1 = 7;
    int node2 = 4;
    printPathBetweenNodes(root, node1, node2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print path between any
// two nodes in a Binary Tree
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

// Function to check if there is a path from root
// to the given node. It also populates
// 'arr' with the given path
static boolean getPath(Node root, Vector<Integer> arr, int x)
{
    // if root is null
    // there is no path
    if (root==null)
        return false;

    // push the node's value in 'arr'
    arr.add(root.data);

    // if it is the required node
    // return true
    if (root.data == x)
        return true;

    // else check whether the required node lies
    // in the left subtree or right subtree of
    // the current node
    if (getPath(root.left, arr, x) || getPath(root.right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from
    // 'arr'and then return false
    arr.remove(arr.size()-1);
    return false;
}

// Function to print the path between
// any two nodes in a binary tree
static void printPathBetweenNodes(Node root, int n1, int n2)
{
    // vector to store the path of
    // first node n1 from root
    Vector<Integer> path1= new Vector<Integer>();

    // vector to store the path of
    // second node n2 from root
    Vector<Integer> path2=new Vector<Integer>();

    getPath(root, path1, n1);
    getPath(root, path2, n2);

    int intersection = -1;

    // Get intersection point
    int i = 0, j = 0;
    while (i != path1.size() || j != path2.size()) {

        // Keep moving forward until no intersection
        // is found
        if (i == j && path1.get(i) == path2.get(i)) {
            i++;
            j++;
        }
        else {
            intersection = j - 1;
            break;
        }
    }

    // Print the required path
    for ( i = path1.size() - 1; i > intersection; i--)
        System.out.print( path1.get(i) + " ");

    for ( i = intersection; i < path2.size(); i++)
        System.out.print( path2.get(i) + " ");
}

// Driver program
public static void main(String[] args)
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

    int node1 = 7;
    int node2 = 4;
    printPathBetweenNodes(root, node1, node2);

}
}
// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python3 program to print path between any
# two nodes in a Binary Tree

import sys
import math

# structure of a node of binary tree
class Node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates a new node with the
#given data and NULL left and right pointers.
def getNode(data):
        return Node(data)

# Function to check if there is a path from root
# to the given node. It also populates
# 'arr' with the given path
def getPath(root, rarr, x):

    # if root is NULL
    # there is no path
    if not root:
        return False

    # push the node's value in 'arr'
    rarr.append(root.data)

    # if it is the required node
    # return true
    if root.data == x:
        return True

    # else check whether the required node lies
    # in the left subtree or right subtree of
    # the current node
    if getPath(root.left, rarr, x) or getPath(root.right, rarr, x):
        return True

    # required node does not lie either in the
    # left or right subtree of the current node
    # Thus, remove current node's value from
    # 'arr'and then return false
    rarr.pop()
    return False

# Function to print the path between
# any two nodes in a binary tree
def printPathBetweenNodes(root, n1, n2):

    # vector to store the path of
    # first node n1 from root
    path1 = []

    # vector to store the path of
    # second node n2 from root
    path2 = []
    getPath(root, path1, n1)
    getPath(root, path2, n2)

    # Get intersection point
    i, j = 0, 0
    intersection=-1
    while(i != len(path1) or j != len(path2)):

        # Keep moving forward until no intersection
        # is found
        if (i == j and path1[i] == path2[j]):
            i += 1
            j += 1
        else:
            intersection = j - 1
            break

    # Print the required path
    for i in range(len(path1) - 1, intersection - 1, -1):
        print("{} ".format(path1[i]), end = "")
    for j in range(intersection + 1, len(path2)):
        print("{} ".format(path2[j]), end = "")

# Driver program
if __name__=='__main__':

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
    node1=7
    node2=4
    printPathBetweenNodes(root,node1,node2)

# This Code is Contributed By Vikash Kumar 37
```

## C#

```
// C# program to print path between any
// two nodes in a Binary Tree
using System;
using System.Collections.Generic;

class Solution
{

// structure of a node of binary tree
public class Node
{
    public int data;
    public Node left, right;
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

// Function to check if there is a path from root
// to the given node. It also populates
// 'arr' with the given path
static Boolean getPath(Node root, List<int> arr, int x)
{
    // if root is null
    // there is no path
    if (root == null)
        return false;

    // push the node's value in 'arr'
    arr.Add(root.data);

    // if it is the required node
    // return true
    if (root.data == x)
        return true;

    // else check whether the required node lies
    // in the left subtree or right subtree of
    // the current node
    if (getPath(root.left, arr, x) || getPath(root.right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from
    // 'arr'and then return false
    arr.RemoveAt(arr.Count-1);
    return false;
}

// Function to print the path between
// any two nodes in a binary tree
static void printPathBetweenNodes(Node root, int n1, int n2)
{
    // vector to store the path of
    // first node n1 from root
    List<int> path1 = new List<int>();

    // vector to store the path of
    // second node n2 from root
    List<int> path2 = new List<int>();

    getPath(root, path1, n1);
    getPath(root, path2, n2);

    int intersection = -1;

    // Get intersection point
    int i = 0, j = 0;
    while (i != path1.Count || j != path2.Count)
    {

        // Keep moving forward until no intersection
        // is found
        if (i == j && path1[i] == path2[i])
        {
            i++;
            j++;
        }
        else
        {
            intersection = j - 1;
            break;
        }
    }

    // Print the required path
    for ( i = path1.Count - 1; i > intersection; i--)
        Console.Write( path1[i] + " ");

    for ( i = intersection; i < path2.Count; i++)
        Console.Write( path2[i] + " ");
}

// Driver code
public static void Main(String[] args)
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

    int node1 = 7;
    int node2 = 4;
    printPathBetweenNodes(root, node1, node2);

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to print path between any
    // two nodes in a Binary Tree

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

    // Function to check if there is a path from root
    // to the given node. It also populates
    // 'arr' with the given path
    function getPath(root, arr, x)
    {
        // if root is null
        // there is no path
        if (root==null)
            return false;

        // push the node's value in 'arr'
        arr.push(root.data);

        // if it is the required node
        // return true
        if (root.data == x)
            return true;

        // else check whether the required node lies
        // in the left subtree or right subtree of
        // the current node
        if (getPath(root.left, arr, x) || getPath(root.right, arr, x))
            return true;

        // required node does not lie either in the
        // left or right subtree of the current node
        // Thus, remove current node's value from
        // 'arr'and then return false
        arr.pop();
        return false;
    }

    // Function to print the path between
    // any two nodes in a binary tree
    function printPathBetweenNodes(root, n1, n2)
    {
        // vector to store the path of
        // first node n1 from root
        let path1= [];

        // vector to store the path of
        // second node n2 from root
        let path2 = [];

        getPath(root, path1, n1);
        getPath(root, path2, n2);

        let intersection = -1;

        // Get intersection point
        let i = 0, j = 0;
        while (i != path1.length || j != path2.length) {

            // Keep moving forward until no intersection
            // is found
            if (i == j && path1[i] == path2[i]) {
                i++;
                j++;
            }
            else {
                intersection = j - 1;
                break;
            }
        }

        // Print the required path
        for ( i = path1.length - 1; i > intersection; i--)
            document.write( path1[i] + " ");

        for ( i = intersection; i < path2.length; i++)
            document.write( path2[i] + " ");
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

    let node1 = 7;
    let node2 = 4;
    printPathBetweenNodes(root, node1, node2);

</script>
```

**Output:** 

```
7 3 1 4
```