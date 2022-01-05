# 在二叉树顶视图中打印节点|集合 2

> 原文:[https://www . geesforgeks . org/print-nodes-in-top-view-of-二叉树-set-2/](https://www.geeksforgeeks.org/print-nodes-in-top-view-of-binary-tree-set-2/)

二叉树的俯视图是从顶部看树时可见的一组节点。给定一棵二叉树，打印它的顶视图。输出节点要从**左到右**打印。

**注**:如果 x 是其水平距离上最顶端的节点，则输出中有一个节点 x。节点 x 的左子节点的水平距离等于 x 减 1 的水平距离，右子节点的水平距离是 x 加 1 的水平距离。

```
Input:
       1
    /     \
   2       3
  /  \    / \
 4    5  6   7
Output: Top view: 4 2 1 3 7

Input:
        1
      /   \
    2       3
      \   
        4  
          \
            5
             \
               6
Output: Top view: 2 1 3 6
```

想法是做一些类似[垂直顺序遍历](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)的事情。像[垂直顺序遍历](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)一样，我们需要将水平距离相同的节点分组在一起。我们进行水平顺序遍历，以便在水平节点上的最顶端节点比它下面水平距离相同的任何其他节点先被访问。一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)用于将节点的水平距离与节点的数据和节点的垂直距离进行映射。

下面是上述方法的实现:

## C++

```
// C++ Program to print Top View of Binary Tree
// using hashmap and recursion
#include <bits/stdc++.h>
using namespace std;

// Node structure
struct Node {
    // Data of the node
    int data;

    // Horizontal Distance of the node
    int hd;

    // Reference to left node
    struct Node* left;

    // Reference to right node
    struct Node* right;
};

// Initialising node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->hd = INT_MAX;
    node->left = NULL;
    node->right = NULL;
    return node;
}

void printTopViewUtil(Node* root, int height,
    int hd, map<int, pair<int, int> >& m)
{
    // Base Case
    if (root == NULL)
        return;

    // If the node for particular horizontal distance
    // is not present in the map, add it.
    // For top view, we consider the first element
    // at horizontal distance in level order traversal
    if (m.find(hd) == m.end()) {
        m[hd] = make_pair(root->data, height);
    }
    else{
        pair<int, int> p = (m.find(hd))->second;

        if (p.second > height) {
            m.erase(hd);
            m[hd] = make_pair(root->data, height);
        }
    }

    // Recur for left and right subtree
    printTopViewUtil(root->left, height + 1, hd - 1, m);
    printTopViewUtil(root->right, height + 1, hd + 1, m);
}

void printTopView(Node* root)
{
    // Map to store horizontal distance,
    // height and node's data
    map<int, pair<int, int> > m;
    printTopViewUtil(root, 0, 0, m);

    // Print the node's value stored by printTopViewUtil()
    for (map<int, pair<int, int> >::iterator it = m.begin();
                                        it != m.end(); it++) {
        pair<int, int> p = it->second;
        cout << p.first << " ";
    }
}

int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->right = newNode(4);
    root->left->right->right = newNode(5);
    root->left->right->right->right = newNode(6);

    cout << "Top View : ";
    printTopView(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print Top View of Binary Tree
// using hashmap and recursion
import java.util.*;

class GFG {

    // Node structure
    static class Node {
        // Data of the node
        int data;

        // Reference to left node
        Node left;

        // Reference to right node
        Node right;
    };
    static class pair {
        int data, height;
        public pair(int data, int height)
        {
            this.data = data;
            this.height = height;
        }
    }

    // Initialising node
    static Node newNode(int data)
    {
        Node node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;
        return node;
    }

    static void printTopViewUtil(Node root, int height,
                                 int hd,
                                 Map<Integer, pair> m)
    {
        // Base Case
        if (root == null)
            return;

        // If the node for particular horizontal distance
        // is not present in the map, add it.
        // For top view, we consider the first element
        // at horizontal distance in level order traversal
        if (!m.containsKey(hd)) {
            m.put(hd, new pair(root.data, height));
        }
        else {
            pair p = m.get(hd);

            if (p.height >= height) {
                m.put(hd, new pair(root.data, height));
            }
        }

        // Recur for left and right subtree
        printTopViewUtil(root.left, height + 1, hd - 1, m);
        printTopViewUtil(root.right, height + 1, hd + 1, m);
    }

    static void printTopView(Node root)
    {
        // Map to store horizontal distance,
        // height and node's data
        Map<Integer, pair> m = new TreeMap<>();
        printTopViewUtil(root, 0, 0, m);

        // Print the node's value stored by
        // printTopViewUtil()
        for (Map.Entry<Integer, pair> it : m.entrySet()) {
            pair p = it.getValue();
            System.out.print(p.data + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.right = newNode(4);
        root.left.right.right = newNode(5);
        root.left.right.right.right = newNode(6);

        System.out.print("Top View : ");
        printTopView(root);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to prTop View of
# Binary Tree using hash and recursion
from collections import OrderedDict

# A binary tree node
class newNode:

    # A constructor to create a
    # new Binary tree Node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.hd = 2**32

def printTopViewUtil(root, height, hd, m):

    # Base Case
    if (root == None):
        return

    # If the node for particular horizontal
    # distance is not present in the map, add it.
    # For top view, we consider the first element
    # at horizontal distance in level order traversal
    if hd not in m :
        m[hd] = [root.data, height]
    else:
        p = m[hd]
        if p[1] > height:
            m[hd] = [root.data, height]

    # Recur for left and right subtree
    printTopViewUtil(root.left,
                     height + 1, hd - 1, m)
    printTopViewUtil(root.right,
                     height + 1, hd + 1, m)

def printTopView(root):

    # to store horizontal distance,
    # height and node's data
    m = OrderedDict()
    printTopViewUtil(root, 0, 0, m)

    # Print the node's value stored
    # by printTopViewUtil()
    for i in sorted(list(m)):
        p = m[i]
        print(p[0], end = " ")

# Driver Code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.right = newNode(4)
root.left.right.right = newNode(5)
root.left.right.right.right = newNode(6)

print("Top View : ", end = "")
printTopView(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to print Top View of Binary
// Tree using hashmap and recursion
using System;
using System.Collections.Generic;

class GFG{

// Node structure
class Node
{

    // Data of the node
    public int data;

    // Reference to left node
    public Node left;

    // Reference to right node
    public Node right;
};

class pair
{
    public int data, height;

    public pair(int data, int height)
    {
        this.data = data;
        this.height = height;
    }
}

// Initialising node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
}

static void printTopViewUtil(Node root, int height,
                             int hd,
                             SortedDictionary<int, pair> m)
{

    // Base Case
    if (root == null)
        return;

    // If the node for particular horizontal distance
    // is not present in the map, add it.
    // For top view, we consider the first element
    // at horizontal distance in level order traversal
    if (!m.ContainsKey(hd))
    {
        m[hd] = new pair(root.data, height);
    }
    else
    {
        pair p = m[hd];

        if (p.height >= height)
        {
            m[hd] = new pair(root.data, height);
        }
    }

    // Recur for left and right subtree
    printTopViewUtil(root.left, height + 1,
                     hd - 1, m);
    printTopViewUtil(root.right, height + 1,
                     hd + 1, m);
}

static void printTopView(Node root)
{

    // Map to store horizontal distance,
    // height and node's data
    SortedDictionary<int,
                     pair> m = new SortedDictionary<int,
                                                    pair>();

    printTopViewUtil(root, 0, 0, m);

    // Print the node's value stored by
    // printTopViewUtil()
    foreach(var it in m.Values)
    {
        Console.Write(it.data + " ");
    }
}

// Driver code
public static void Main(string[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.left.right.right = newNode(5);
    root.left.right.right.right = newNode(6);

    Console.Write("Top View : ");

    printTopView(root);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to print Top View of Binary
// Tree using hashmap and recursion

// Node structure
class Node
{
    constructor()
    {
      // Data of the node
      this.data = 0;
      // Reference to left node
      this.left = null;
      // Reference to right node
      this.right = null;
    }
};

class pair
{
  constructor(data, height)
  {
    this.data = data;
    this.height = height;
  }
}

// Initialising node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
}

function printTopViewUtil(root, height, hd, m)
{

    // Base Case
    if (root == null)
        return;

    // If the node for particular horizontal distance
    // is not present in the map, add it.
    // For top view, we consider the first element
    // at horizontal distance in level order traversal
    if (!m.has(hd))
    {
        m.set(hd, new pair(root.data, height));
    }
    else
    {
        var p = m.get(hd);

        if (p.height >= height)
        {
            m.set(hd, new pair(root.data, height));
        }
    }

    // Recur for left and right subtree
    printTopViewUtil(root.left, height + 1,
                     hd - 1, m);
    printTopViewUtil(root.right, height + 1,
                     hd + 1, m);
}

function printTopView(root)
{

    // Map to store horizontal distance,
    // height and node's data
    var m = new Map();

    printTopViewUtil(root, 0, 0, m);

    // Print the node's value stored by
    // printTopViewUtil()
    for(var it of [...m].sort())
    {
        document.write(it[1].data + " ");
    }
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.right = newNode(4);
root.left.right.right = newNode(5);
root.left.right.right.right = newNode(6);
document.write("Top View : ");
printTopView(root);

</script>
```

**Output**

```
Top View : 2 1 3 6
```