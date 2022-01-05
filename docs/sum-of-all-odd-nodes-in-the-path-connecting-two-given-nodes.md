# 连接两个给定节点的路径中所有奇数节点的总和

> 原文:[https://www . geesforgeks . org/连接两个给定节点的路径中所有奇数节点的总和/](https://www.geeksforgeeks.org/sum-of-all-odd-nodes-in-the-path-connecting-two-given-nodes/)

给定一棵二叉树和该二叉树的两个节点。求连接两个给定节点的路径中所有奇数节点的和。

![Binary Tree](img/bf1c9b4105790a6c6d531bffa9c46ff8.png)

**例如**:在上面的二叉树中，节点![5    ](img/68fce31473210d463625887e78c83617.png "Rendered by QuickLaTeX.com")和![6    ](img/03e9dd9410187feeba6b33f1ddf86d54.png "Rendered by QuickLaTeX.com")之间的路径中所有奇数节点的和将是 **5 + 1 + 3 = 9** 。

**来源** : [亚马逊校园面试体验](https://www.geeksforgeeks.org/amazon-interview-experience-on-campus/)
**途径**:思路是先用[中讨论的概念找到二叉树两个给定节点之间的路径，打印任意两个节点之间的路径](https://www.geeksforgeeks.org/print-path-between-any-two-nodes-in-a-binary-tree/)。
一旦我们有了两个给定节点之间的路径，计算该路径中所有奇数值节点的和并打印出来。
以下是上述方法的实施:

## C++

```
// C++ program to find sum of all odd nodes
// in the path connecting two given nodes

#include<bits/stdc++.h>
using namespace std;

// Binary Tree node
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create a
// new Binary Tree node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
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

// Function to get the sum of odd nodes in the
// path between any two nodes in a binary tree
int sumOddNodes(Node* root, int n1, int n2)
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

    int sum = 0;

    // calculate sum of ODD nodes from the path
    for (int i = path1.size() - 1; i > intersection; i--)
        if(path1[i]%2)
            sum += path1[i];

    for (int i = intersection; i < path2.size(); i++)
        if(path2[i]%2)
            sum += path2[i];

    return sum;       
}

// Driver Code
int main()
{
    struct Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(6);

    int node1 = 5;
    int node2 = 6;

    cout<<sumOddNodes(root, node1, node2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all odd nodes
// in the path connecting two given nodes

import java.util.*;
class solution
{

// Binary Tree node
static class Node
{
    int data;
     Node left;
     Node right;
}

// Utility function to create a
// new Binary Tree node
 static Node newNode(int data)
{
     Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
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

// Function to get the sum of odd nodes in the
// path between any two nodes in a binary tree
static int sumOddNodes(Node root, int n1, int n2)
{
    // vector to store the path of
    // first node n1 from root
    Vector<Integer> path1= new Vector<Integer>();

    // vector to store the path of
    // second node n2 from root
    Vector<Integer> path2= new Vector<Integer>();

    getPath(root, path1, n1);
    getPath(root, path2, n2);

    int intersection = -1;

    // Get intersection point
    int i = 0, j = 0;
    while (i != path1.size() || j != path2.size()) {

        // Keep moving forward until no intersection
        // is found
        if (i == j && path1.get(i) == path2.get(j)) {
            i++;
            j++;
        }
        else {
            intersection = j - 1;
            break;
        }
    }

    int sum = 0;

    // calculate sum of ODD nodes from the path
    for (i = path1.size() - 1; i > intersection; i--)
        if(path1.get(i)%2!=0)
            sum += path1.get(i);

    for (i = intersection; i < path2.size(); i++)
        if(path2.get(i)%2!=0)
            sum += path2.get(i);

    return sum;        
}

// Driver Code
public static void main(String args[])
{
     Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    int node1 = 5;
    int node2 = 6;

    System.out.print(sumOddNodes(root, node1, node2));

}
}
```

## 蟒蛇 3

```
# Python3 program to find sum of all odd nodes
# in the path connecting two given nodes

# Binary Tree node
class Node:
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# Utility function to create a
# Binary Tree node
def newNode( data):

    node = Node()
    node.data = data
    node.left = None
    node.right = None

    return node

# Function to check if there is a path from root
# to the given node. It also populates
# 'arr' with the given path
def getPath(root, arr, x):

    # if root is None
    # there is no path
    if (root == None) :
        return False

    # push the node's value in 'arr'
    arr.append(root.data)

    # if it is the required node
    # return True
    if (root.data == x) :
        return True

    # else check whether the required node lies
    # in the left subtree or right subtree of
    # the current node
    if (getPath(root.left, arr, x) or getPath(root.right, arr, x)) :
        return True

    # required node does not lie either in the
    # left or right subtree of the current node
    # Thus, remove current node's value from
    # 'arr'and then return False
    arr.pop()
    return False

# Function to get the sum of odd nodes in the
# path between any two nodes in a binary tree
def sumOddNodes(root, n1, n2) :

    # vector to store the path of
    # first node n1 from root
    path1 = []

    # vector to store the path of
    # second node n2 from root
    path2 = []

    getPath(root, path1, n1)
    getPath(root, path2, n2)

    intersection = -1

    # Get intersection point
    i = 0
    j = 0
    while (i != len(path1) or j != len(path2)):

        # Keep moving forward until no intersection
        # is found
        if (i == j and path1[i] == path2[j]):
            i = i + 1
            j = j + 1

        else :
            intersection = j - 1
            break

    sum = 0

    i = len(path1) - 1

    # calculate sum of ODD nodes from the path
    while ( i > intersection ):
        if(path1[i] % 2 != 0):
            sum += path1[i]
        i = i - 1

    i = intersection
    while ( i < len(path2) ):
        if(path2[i] % 2 != 0) :
            sum += path2[i]
        i = i + 1

    return sum       

# Driver Code

root = newNode(1)

root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.right = newNode(6)

node1 = 5
node2 = 6

print(sumOddNodes(root, node1, node2))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to find sum of all odd nodes
// in the path connecting two given nodes
using System;
using System.Collections.Generic;

class GFG
{

// Binary Tree node
public class Node
{
    public int data;
    public Node left;
    public Node right;
}

// Utility function to create a
// new Binary Tree node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// Function to check if there is a path from
// root to the given node. It also populates
// 'arr' with the given path
static Boolean getPath(Node root,
                       List<int> arr, int x)
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
    if (getPath(root.left, arr, x) ||
        getPath(root.right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, Remove current node's value from
    // 'arr'and then return false
    arr.RemoveAt(arr.Count - 1);
    return false;
}

// Function to get the sum of odd nodes in the
// path between any two nodes in a binary tree
static int sumOddNodes(Node root, int n1, int n2)
{
    // List to store the path of
    // first node n1 from root
    List<int> path1 = new List<int>();

    // List to store the path of
    // second node n2 from root
    List<int> path2 = new List<int>();

    getPath(root, path1, n1);
    getPath(root, path2, n2);

    int intersection = -1;

    // Get intersection point
    int i = 0, j = 0;
    while (i < path1.Count || j < path2.Count)
    {

        // Keep moving forward until
        // no intersection is found
        if ( i == j && path1[i] == path2[j])
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
    int sum = 0;

    // calculate sum of ODD nodes from the path
    for (i = path1.Count - 1; i > intersection; i--)
        if(path1[i] % 2 != 0)
            sum += path1[i];

    for (i = intersection; i < path2.Count; i++)
        if(path2[i] % 2 != 0)
            sum += path2[i];

    return sum;        
}

// Driver Code
public static void Main(String []args)
{
    Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    int node1 = 5;
    int node2 = 6;

    Console.Write(sumOddNodes(root, node1, node2));
}
}

// This code is contributed by Arnub Kundu
```

## java 描述语言

```
<script>

    // JavaScript program to find sum of all odd nodes
    // in the path connecting two given nodes

    // Binary Tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Utility function to create a
    // new Binary Tree node
    function newNode(data)
    {
          let node = new Node(data);
        return node;
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

    // Function to get the sum of odd nodes in the
    // path between any two nodes in a binary tree
    function sumOddNodes(root, n1, n2)
    {
        // vector to store the path of
        // first node n1 from root
        let path1= [];

        // vector to store the path of
        // second node n2 from root
        let path2= [];

        getPath(root, path1, n1);
        getPath(root, path2, n2);

        let intersection = -1;

        // Get intersection point
        let i = 0, j = 0;
        while (i != path1.length || j != path2.length) {

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

        let sum = 0;

        // calculate sum of ODD nodes from the path
        for (i = path1.length - 1; i > intersection; i--)
            if(path1[i]%2!=0)
                sum += path1[i];

        for (i = intersection; i < path2.length; i++)
            if(path2[i]%2!=0)
                sum += path2[i];

        return sum;        
    }

    let root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    let node1 = 5;
    let node2 = 6;

    document.write(sumOddNodes(root, node1, node2));

</script>
```

**输出:**

```
9
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)