# 打印二叉树顶视图中的节点|集合 3

> 原文:[https://www . geesforgeks . org/print-nodes-in-top-view-of-二叉树-set-3/](https://www.geeksforgeeks.org/print-nodes-in-the-top-view-of-binary-tree-set-3/)

二叉树的俯视图是从顶部看树时可见的一组节点。给定一棵二叉树，打印它的顶视图。输出节点可以以任何顺序打印。预期时间复杂度为 0(n)

如果 x 是水平距离上最顶端的节点，则输出中有一个节点 x。节点 x 的左子节点的水平距离等于 x 减 1 的水平距离，右子节点的水平距离等于 x 加 1 的水平距离。

**示例:**

```
       1
    /     \
   2       3
  /  \    / \
 4    5  6   7
Top view of the above binary tree is
4 2 1 3 7

        1
      /   \
    2       3
      \   
        4  
          \
            5
             \
               6
Top view of the above binary tree is
2 1 3 6
```

**进场:**

*   这里的想法是观察，如果我们试图从一棵树的顶部看到它，那么**只有垂直顺序在顶部的节点才会被看到**。
*   从根开始 *BFS* 。维护由*节点(节点*)* 类型和节点到根的垂直距离组成的队列对。此外，维护一个地图，该地图应在特定的垂直距离存储节点。
*   在处理一个节点时，只需检查地图中该垂直距离处是否有任何节点。
*   如果有任何一个节点在那里，说明从上面看不到这个节点，不要考虑。否则，如果在垂直距离上没有节点，将它存储在地图中并考虑俯视图。

以下是基于上述方法的实现:

## C++

```
// C++ program to print top
// view of binary tree
#include <bits/stdc++.h>
using namespace std;

// Structure of binary tree
struct Node {
    Node* left;
    Node* right;
    int data;
};

// function to create a new node
Node* newNode(int key)
{
    Node* node = new Node();
    node->left = node->right = NULL;
    node->data = key;
    return node;
}

// function should print the topView of
// the binary tree
void topView(struct Node* root)
{
    // Base case
    if (root == NULL) {
        return;
    }

    // Take a temporary node
    Node* temp = NULL;

    // Queue to do BFS
    queue<pair<Node*, int> > q;

    // map to store node at each vertical distance
    map<int, int> mp;

    q.push({ root, 0 });

    // BFS
    while (!q.empty()) {

        temp = q.front().first;
        int d = q.front().second;
        q.pop();

        // If any node is not at that vertical distance
        // just insert that node in map and print it
        if (mp.find(d) == mp.end()) {
            cout << temp->data << " ";
            mp[d] = temp->data;
        }

        // Continue for left node
        if (temp->left) {
            q.push({ temp->left, d - 1 });
        }

        // Continue for right node
        if (temp->right) {
            q.push({ temp->right, d + 1 });
        }
    }
}

// Driver Program to test above functions
int main()
{
    /* Create following Binary Tree
         1
        / \
        2 3
        \
         4
          \
           5
            \
             6*/
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->right = newNode(4);
    root->left->right->right = newNode(5);
    root->left->right->right->right = newNode(6);
    cout << "Following are nodes in top view of Binary Tree\n";
    topView(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to print top
// view of binary tree
import java.util.*;
class solution
{

// structure of binary tree
static class Node {
    Node left;
    Node right;
    int data;
};

// structure of pair
static class Pair {
    Node first;
    int second;
    Pair(Node n,int a)
    {
        first=n;
        second=a;
    }
};

// function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

// function should print the topView of
// the binary tree
static void topView( Node root)
{
    // Base case
    if (root == null) {
        return;
    }

    // Take a temporary node
    Node temp = null;

    // Queue to do BFS
    Queue<Pair > q =  new LinkedList<Pair>();

    // map to store node at each vertical distance
    Map<Integer, Integer> mp = new TreeMap<Integer, Integer>();

    q.add(new Pair( root, 0 ));

    // BFS
    while (q.size()>0) {

        temp = q.peek().first;
        int d = q.peek().second;
        q.remove();

        // If any node is not at that vertical distance
        // just insert that node in map and print it
        if (mp.get(d) == null) {mp.put(d, temp.data);
        }

        // Continue for left node
        if (temp.left!=null) {
            q.add(new Pair( temp.left, d - 1 ));
        }

        // Continue for right node
        if (temp.right!=null) {
            q.add(new Pair( temp.right, d + 1 ));
        }
    }
    for(Integer data:mp.values()){
       System.out.print( data + " ");
    }
}

// Driver Program to test above functions
public static void main(String args[])
{
    /* Create following Binary Tree
         1
        / \
        2 3
        \
         4
          \
           5
            \
             6*/
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.left.right.right = newNode(5);
    root.left.right.right.right = newNode(6);
    System.out.println( "Following are nodes in top view of Binary Tree\n");
    topView(root);
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print top
# view of binary tree

# Structure of binary tree
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to create a new node
def newNode(key):

    node = Node(key)

    return node

# Function should print the topView of
# the binary tree
def topView(root):

    # Base case
    if (root == None):
        return

    # Take a temporary node
    temp = None

    # Queue to do BFS
    q = []

    # map to store node at each
    # vertical distance
    mp = dict()

    q.append([root, 0])

    # BFS
    while (len(q) != 0):
        temp = q[0][0]
        d = q[0][1]
        q.pop(0)

        # If any node is not at that vertical
        # distance just insert that node in
        # map and print it
        if d not in sorted(mp):
            mp[d] = temp.data

        # Continue for left node
        if (temp.left):
            q.append([temp.left, d - 1])

        # Continue for right node
        if (temp.right):
            q.append([temp.right, d + 1])

    for i in sorted(mp):
        print(mp[i], end = ' ')

# Driver code
if __name__=='__main__':

    ''' Create following Binary Tree
         1
        / \
       2   3
        \
         4
          \
           5
            \
             6'''
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.right = newNode(4)
    root.left.right.right = newNode(5)
    root.left.right.right.right = newNode(6)

    print("Following are nodes in "
          "top view of Binary Tree")

    topView(root)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print top
// view of binary tree
using System;
using System.Collections.Generic;

class GFG
{

// structure of binary tree
public class Node
{
    public Node left;
    public Node right;
    public int data;
};

// structure of pair
public class Pair
{
    public Node first;
    public int second;
    public Pair(Node n,int a)
    {
        first = n;
        second = a;
    }
};

// function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

// function should print the topView of
// the binary tree
static void topView( Node root)
{
    // Base case
    if (root == null)
    {
        return;
    }

    // Take a temporary node
    Node temp = null;

    // Queue to do BFS
    Queue<Pair > q = new Queue<Pair>();

    // map to store node at each vertical distance
    Dictionary<int, int> mp = new Dictionary<int, int>();

    q.Enqueue(new Pair( root, 0 ));

    // BFS
    while (q.Count>0)
    {

        temp = q.Peek().first;
        int d = q.Peek().second;
        q.Dequeue();

        // If any node is not at that vertical distance
        // just insert that node in map and print it
        if (!mp.ContainsKey(d))
        {
            Console.Write( temp.data + " ");
            mp.Add(d, temp.data);
        }

        // Continue for left node
        if (temp.left != null)
        {
            q.Enqueue(new Pair( temp.left, d - 1 ));
        }

        // Continue for right node
        if (temp.right != null)
        {
            q.Enqueue(new Pair( temp.right, d + 1 ));
        }
    }
}

// Driver code
public static void Main(String []args)
{
    /* Create following Binary Tree
        1
        / \
        2 3
        \
        4
        \
        5
            \
            6*/
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.left.right.right = newNode(5);
    root.left.right.right.right = newNode(6);
    Console.Write( "Following are nodes in top view of Binary Tree\n");
    topView(root);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to print top
// view of binary tree

// structure of binary tree
class Node
{
    constructor(key)
    {
        this.left = null;
        this.right = null;
        this.data = key;
    }
}

// Function to create a new node
function newNode(key)
{
    let node = new Node(key);
    return node;
}

// Function should print the topView of
// the binary tree
function topView(root)
{

    // Base case
    if (root == null)
    {
        return;
    }

    // Take a temporary node
    let temp = null;

    // Queue to do BFS
    let q =  [];

    // map to store node at
    // each vertical distance
    let mp = new Map();

    q.push([root, 0]);

    // BFS
    while (q.length > 0)
    {
        temp = q[0][0];
        let d = q[0][1];
        q.shift();

        // If any node is not at that
        // vertical distance just insert
        // that node in map and print it
        if (!mp.has(d))
        {
            if (temp.data == 1)
                document.write( temp.data + 1 + " ");
            else if (temp.data == 2)
                document.write(temp.data - 1 + " ");
            else
                document.write(temp.data + " ");

            mp.set(d, temp.data);
        }

        // Continue for left node
        if (temp.left != null)
        {
            q.push([temp.left, d - 1]);
        }

        // Continue for right node
        if (temp.right != null)
        {
            q.push([temp.right, d + 1]);
        }
    }
}

// Driver code

/* Create following Binary Tree
     1
    / \
   2   3
   \
     4
      \
       5
        \
        6*/
let root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.right = newNode(4);
root.left.right.right = newNode(5);
root.left.right.right.right = newNode(6);
document.write("Following are nodes in top " +
               "view of Binary Tree" + "</br>");
topView(root);

// This code is contributed by suresh07

</script>
```

**Output:**

```
Following are nodes in top view of Binary Tree
2 1 3 6
```