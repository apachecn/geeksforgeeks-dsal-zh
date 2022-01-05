# 当二叉树的节点成为叶节点时打印它们

> 原文:[https://www . geesforgeks . org/print-二叉树的节点成为叶子节点/](https://www.geeksforgeeks.org/print-the-nodes-of-binary-tree-as-they-become-the-leaf-node/)

给定一棵二叉树。首先打印所有的叶节点，然后从树中移除所有的叶节点，现在打印所有新形成的叶节点，并一直这样做，直到所有的节点都从树中移除。
**例**:

```
Input :  
              8
             / \
           3    10
          / \   / \
         1  6  14  4
        / \
       7   13

Output : 
4 6 7 13 14
1 10
3
8
```

**来源** : [Flipkart 校园招聘](https://www.geeksforgeeks.org/flipkart-on-campus-recruitment/)
**途径**:思路是进行简单的 dfs，根据以下条件给每个节点分配不同的值:

1.  最初将值为 0 的所有节点赋值。
2.  现在，给所有节点赋值为**(两个子节点的最大值)+1** 。

**DFS 之前的树**:临时值零被分配给所有节点。

![before dfs](img/3913e21754c849605079911f7c404b3f.png)

**DFS 后的树**:节点赋值为**(两个子节点的最大值)+1** 。

![after dfs](img/ea75e344945ff406a02d368e9a73e82c.png)

现在，您可以在上面的树中看到，在将所有值分配给每个节点后，任务现在减少到根据分配给它们的节点值的升序来打印树。
以下是上述方法的实施:

## C++

```
// C++ program to print the nodes of binary
// tree as they become the leaf node

#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    int data;
    int order;
    struct Node* left;
    struct Node* right;
};

// Utility function to allocate a new node
struct Node* newNode(int data, int order)
{
    struct Node* node = new Node;
    node->data = data;
    node->order = order;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

// Function for postorder traversal of tree and
// assigning values to nodes
void Postorder(struct Node* node, vector<pair<int, int> >& v)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    Postorder(node->left, v);

    /* now recur on right child */
    Postorder(node->right, v);

    // If current node is leaf node, it's order will be 1
    if (node->right == NULL && node->left == NULL) {
        node->order = 1;

        // make pair of assigned value and tree value
        v.push_back(make_pair(node->order, node->data));
    }
    else {
        // otherwise, the order will be:
        // max(left_child_order, right_child_order) + 1
        node->order = max((node->left)->order, (node->right)->order) + 1;

        // make pair of assigned value and tree value
        v.push_back(make_pair(node->order, node->data));
    }
}

// Function to print leaf nodes in
// the given order
void printLeafNodes(int n, vector<pair<int, int> >& v)
{
    // Sort the vector in increasing order of
    // assigned node values
    sort(v.begin(), v.end());

    for (int i = 0; i < n; i++) {
        if (v[i].first == v[i + 1].first)
            cout << v[i].second << " ";

        else
            cout << v[i].second << "\n";
    }
}

// Driver Code
int main()
{
    struct Node* root = newNode(8, 0);
    root->left = newNode(3, 0);
    root->right = newNode(10, 0);
    root->left->left = newNode(1, 0);
    root->left->right = newNode(6, 0);
    root->right->left = newNode(14, 0);
    root->right->right = newNode(4, 0);
    root->left->left->left = newNode(7, 0);
    root->left->left->right = newNode(13, 0);

    int n = 9;

    vector<pair<int, int> > v;

    Postorder(root, v);
    printLeafNodes(n, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the nodes of binary
// tree as they become the leaf node
import java.util.*;

class GFG
{

// Binary tree node
static class Node
{
    int data;
    int order;
    Node left;
    Node right;
};

static class Pair
{
    int first,second;

    Pair(int a,int b)
    {
        first = a;
        second = b;
    }
}

// Utility function to allocate a new node
static Node newNode(int data, int order)
{
    Node node = new Node();
    node.data = data;
    node.order = order;
    node.left = null;
    node.right = null;

    return (node);
}
static Vector<Pair> v = new Vector<Pair>();

// Function for postorder traversal of tree and
// assigning values to nodes
static void Postorder(Node node)
{
    if (node == null)
        return;

    /* first recur on left child */
    Postorder(node.left);

    /* now recur on right child */
    Postorder(node.right);

    // If current node is leaf node, it's order will be 1
    if (node.right == null && node.left == null)
    {
        node.order = 1;

        // make pair of assigned value and tree value
        v.add(new Pair(node.order, node.data));
    }
    else
    {
        // otherwise, the order will be:
        // max(left_child_order, right_child_order) + 1
        node.order = Math.max((node.left).order, (node.right).order) + 1;

        // make pair of assigned value and tree value
        v.add(new Pair(node.order, node.data));
    }
}
static class Sort implements Comparator<Pair>
{
    // Used for sorting in ascending order of
    // roll number
    public int compare(Pair a, Pair b)
    {
        if(a.first != b.first)
        return (a.first - b.first);
        else
        return (a.second-b.second);
    }
}

// Function to print leaf nodes in
// the given order
static void printLeafNodes(int n)
{
    // Sort the vector in increasing order of
    // assigned node values
    Collections.sort(v,new Sort());
    for (int i = 0; i < v.size(); i++)
    {
        if (i != v.size()-1 && v.get(i).first == v.get(i + 1).first)
            System.out.print( v.get(i).second + " ");

        else
            System.out.print( v.get(i).second + "\n");
    }
}

// Driver Code
public static void main(String args[])
{
    Node root = newNode(8, 0);
    root.left = newNode(3, 0);
    root.right = newNode(10, 0);
    root.left.left = newNode(1, 0);
    root.left.right = newNode(6, 0);
    root.right.left = newNode(14, 0);
    root.right.right = newNode(4, 0);
    root.left.left.left = newNode(7, 0);
    root.left.left.right = newNode(13, 0);

    int n = 9;

    Postorder(root);
    printLeafNodes(n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print the nodes of binary
# tree as they become the leaf node

# Binary tree node
class newNode:

    def __init__(self, data,order):
        self.data = data
        self.order=order
        self.left = None
        self.right = None

# Function for postorder traversal of tree and
# assigning values to nodes
def Postorder(node,v):
    if (node == None):
        return

    """ first recur on left child """
    Postorder(node.left, v)

    """ now recur on right child """
    Postorder(node.right, v)

    # If current node is leaf node,
    # it's order will be 1
    if (node.right == None and
        node.left == None):
        node.order = 1

        # make pair of assigned value and tree value
        v[0].append([node.order, node.data])

    else:

        # otherwise, the order will be:
        # max(left_child_order, right_child_order) + 1
        node.order = max((node.left).order,
                         (node.right).order) + 1

        # make pair of assigned value and tree value
        v[0].append([node.order, node.data])

# Function to print leaf nodes in
# the given order
def printLeafNodes(n, v):

    # Sort the vector in increasing order of
    # assigned node values
    v=sorted(v[0])
    for i in range(n - 1):
        if (v[i][0]== v[i + 1][0]):
            print(v[i][1], end = " ")
        else:
            print(v[i][1])
    if (v[-1][0]== v[-2][0]):
            print(v[-1][1], end = " ")
    else:
        print(v[-1][1])

# Driver Code
root = newNode(8, 0)
root.left = newNode(3, 0)
root.right = newNode(10, 0)
root.left.left = newNode(1, 0)
root.left.right = newNode(6, 0)
root.right.left = newNode(14, 0)
root.right.right = newNode(4, 0)
root.left.left.left = newNode(7, 0)
root.left.left.right = newNode(13, 0)

n = 9
v = [[] for i in range(1)]

Postorder(root, v)
printLeafNodes(n, v)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to print the nodes of binary
// tree as they become the leaf node
using System;
using System.Collections.Generic;

class GFG
{

// Binary tree node
public class Node
{
    public int data;
    public int order;
    public Node left;
    public Node right;
};

public class Pair
{
    public int first,second;

    public Pair(int a,int b)
    {
        first = a;
        second = b;
    }
}

// Utility function to allocate a new node
static Node newNode(int data, int order)
{
    Node node = new Node();
    node.data = data;
    node.order = order;
    node.left = null;
    node.right = null;

    return (node);
}

static List<Pair> v = new List<Pair>();

// Function for postorder traversal of
// tree and assigning values to nodes
static void Postorder(Node node)
{
    if (node == null)
        return;

    /* first recur on left child */
    Postorder(node.left);

    /* now recur on right child */
    Postorder(node.right);

    // If current node is leaf node,
    // it's order will be 1
    if (node.right == null &&
        node.left == null)
    {
        node.order = 1;

        // make pair of assigned value
        // and tree value
        v.Add(new Pair(node.order, node.data));
    }
    else
    {
        // otherwise, the order will be:
        // Max(left_child_order,
        //     right_child_order) + 1
        node.order = Math.Max((node.left).order,
                              (node.right).order) + 1;

        // make pair of assigned value
        // and tree value
        v.Add(new Pair(node.order, node.data));
    }
}

// Used for sorting in ascending order
// of roll number
public static int compare(Pair a, Pair b)
{
    if(a.first != b.first)
        return (a.first - b.first);
    else
        return (a.second - b.second);
}

// Function to print leaf nodes in
// the given order
static void printLeafNodes(int n)
{
    // Sort the List in increasing order
    // of assigned node values
    v.Sort(compare);
    for (int i = 0; i < v.Count; i++)
    {
        if (i != v.Count - 1 &&
            v[i].first == v[i + 1].first)
            Console.Write(v[i].second + " ");

        else
            Console.Write(v[i].second + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    Node root = newNode(8, 0);
    root.left = newNode(3, 0);
    root.right = newNode(10, 0);
    root.left.left = newNode(1, 0);
    root.left.right = newNode(6, 0);
    root.right.left = newNode(14, 0);
    root.right.right = newNode(4, 0);
    root.left.left.left = newNode(7, 0);
    root.left.left.right = newNode(13, 0);

    int n = 9;

    Postorder(root);
    printLeafNodes(n);
}
}

// This code is contributed
// by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to print the nodes of binary
// tree as they become the leaf node

class Node
{
    constructor()
    {
        this.data = 0;
        this.order = 0;
        this.left = this.right = null;
    }
}

class Pair
{
    constructor(a, b)
    {
        this.first = a;
        this.second = b;
    }
}

// Utility function to allocate a new node
function newNode(data,order)
{
    let node = new Node();
    node.data = data;
    node.order = order;
    node.left = null;
    node.right = null;

    return (node);
}

let v = [];

// Function for postorder traversal of tree and
// assigning values to nodes
function Postorder(node)
{
    if (node == null)
        return;

    /* first recur on left child */
    Postorder(node.left);

    /* now recur on right child */
    Postorder(node.right);

    // If current node is leaf node, it's order will be 1
    if (node.right == null && node.left == null)
    {
        node.order = 1;

        // make pair of assigned value and tree value
        v.push(new Pair(node.order, node.data));
    }
    else
    {
        // otherwise, the order will be:
        // max(left_child_order, right_child_order) + 1
        node.order = Math.max((node.left).order, (node.right).order) + 1;

        // make pair of assigned value and tree value
        v.push(new Pair(node.order, node.data));
    }
}

// Function to print leaf nodes in
// the given order
function printLeafNodes(n)
{

    // Sort the vector in increasing order of
    // assigned node values
    v.sort(function(a,b){
        if(a.first != b.first)
            return (a.first - b.first);
        else
            return (a.second-b.second);})
    for (let i = 0; i < v.length; i++)
    {
        if (i != v.length-1 && v[i].first == v[i+1].first)
            document.write( v[i].second + " ");

        else
            document.write( v[i].second + "<br>");
    }
}

// Driver Code
let root = newNode(8, 0);
root.left = newNode(3, 0);
root.right = newNode(10, 0);
root.left.left = newNode(1, 0);
root.left.right = newNode(6, 0);
root.right.left = newNode(14, 0);
root.right.right = newNode(4, 0);
root.left.left.left = newNode(7, 0);
root.left.left.right = newNode(13, 0);

let n = 9;

Postorder(root);
printLeafNodes(n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4 6 7 13 14
1 10
3
8
```

**时间复杂度** : O(nlogn)
**辅助空间** : O(n)，其中 n 是给定二叉树中的节点数。