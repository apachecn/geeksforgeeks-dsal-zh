# 二叉树最大深度的节点之和|迭代方法

> 原文:[https://www . geeksforgeeks . org/二叉树最大深度节点总和迭代方法/](https://www.geeksforgeeks.org/sum-of-nodes-at-maximum-depth-of-a-binary-tree-iterative-approach/)

给定一棵树的根节点，求距根节点最大深度的所有叶节点的和。

**示例:**

```
      1
    /   \
   2     3
  / \   / \
 4   5 6   7

Input : root(of above tree)
Output : 22

Explanation:
Nodes at maximum depth are 4, 5, 6, 7\. 
So, the sum of these nodes = 22
```

**方法:**这个问题存在一种[递归](https://write.geeksforgeeks.org/sum-of-nodes-at-maximum-depth-of-a-binary-tree/)方法。这也可以使用级别顺序遍历和映射来解决。其思想是使用队列进行遍历，并跟踪当前级别。一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)已经被用来存储当前级别的节点总数。一旦访问了所有节点并完成遍历，地图的最后一个元素将包含树的最大深度的总和。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the sum of
// nodes at the maximum depth of a binary tree
#include <bits/stdc++.h>
using namespace std;

struct node {
    int data;
    node *left, *right;
} * temp;

node* newNode(int data)
{
    temp = new node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Function to return the sum
int SumAtMaxLevel(node* root)
{
    // Map to store level wise sum.
    map<int, int> mp;

    // Queue for performing Level Order Traversal.
    // First entry is the node and
    // second entry is the level of this node.
    queue<pair<node*, int> > q;

    // Root has level 0.
    q.push({ root, 0 });

    while (!q.empty()) {

        // Get the node from front of Queue.
        pair<node*, int> temp = q.front();
        q.pop();

        // Get the depth of current node.
        int depth = temp.second;

        // Add the value of this node in map.
        mp[depth] += (temp.first)->data;

        // Push children of this node,
        // with increasing the depth.
        if (temp.first->left)
            q.push({ temp.first->left, depth + 1 });

        if (temp.first->right)
            q.push({ temp.first->right, depth + 1 });
    }

    map<int, int>::iterator it;

    // Get the max depth from map.
    it = mp.end();

    // last element
    it--;

    // return the max Depth sum.
    return it->second;
}

// Driver Code
int main()
{
    node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    cout << SumAtMaxLevel(root) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the sum of nodes at the
// maximum depth of a binary tree
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Queue;

class GFG{

static class Node
{
  int data;
  Node left, right;
  public Node(int data)
  {
    this.data = data;
    this.left = this.right =
                null;
  }
}

static class Pair
{
  Node node;
  int data;
  public Pair(Node node,
              int data)
  {
    this.node = node;
    this.data = data;
  }
}

// Function to return the sum
static int SumAtMaxLevel(Node root)
{
  // Map to store level wise sum.
  HashMap<Integer,
          Integer> mp = new HashMap<>();

  // Queue for performing Level
  // Order Traversal. First entry
  // is the node and second entry
  // is the level of this node.
  Queue<Pair> q = new LinkedList<>();

  // Root has level 0.
  q.add(new Pair(root, 0));

  while (!q.isEmpty())
  {
    // Get the node from
    // front of Queue.
    Pair temp = q.poll();

    // Get the depth of
    // current node.
    int depth = temp.data;

    // Add the value of this
    // node in map.
    if (!mp.containsKey(depth))
      mp.put(depth, 0);
    mp.put(depth, mp.get(depth) +
           temp.node.data);

    // Push children of this node,
    // with increasing the depth.
    if (temp.node.left != null)
      q.add(new Pair(temp.node.left,
                     depth + 1));

    if (temp.node.right != null)
      q.add(new Pair(temp.node.right,
                     depth + 1));
  }

  Object[] values = mp.values().toArray();
  return (int) values[values.length - 1];
}

// Driver Code
public static void main(String[] args)
{
  Node root = new Node(1);
  root.left = new Node(2);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(5);
  root.right.left = new Node(6);
  root.right.right = new Node(7);

  System.out.println(SumAtMaxLevel(root));
}     
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to calculate the
# sum of nodes at the maximum depth
# of a binary tree

# Helper function that allocates a
# new node with the given data and
# None left and right poers.                                    
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to return the sum
def SumAtMaxLevel(root):

    # Map to store level wise sum.
    mp = {}

    # Queue for performing Level Order
    # Traversal. First entry is the node
    # and second entry is the level of
    # this node.
    q = []

    # Root has level 0.
    q.append([root, 0])

    while (len(q)):

        # Get the node from front
        # of Queue.
        temp = q[0]
        q.pop(0)

        # Get the depth of current node.
        depth = temp[1]

        # Add the value of this node in map.
        if depth not in mp:
            mp[depth] = 0
        mp[depth] += (temp[0]).data

        # append children of this node,
        # with increasing the depth.
        if (temp[0].left) :
            q.append([temp[0].left,
                        depth + 1])

        if (temp[0].right) :
            q.append([temp[0].right,
                         depth + 1])

    # return the max Depth sum.
    return list(mp.values())[-1]

# Driver Code
if __name__ == '__main__':

    # Let us construct the Tree
    # shown in the above figure
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    print(SumAtMaxLevel(root))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to calculate
// the sum of nodes at the
// maximum depth of a binary tree
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG{

class Node
{
  public int data;
public Node left, right;
  public Node(int data)
  {
    this.data = data;
    this.left = this.right =
                null;
  }
}

class Pair
{
  public Node node;
  public int data;
  public Pair(Node node,
              int data)
  {
    this.node = node;
    this.data = data;
  }
}

// Function to return the sum
static int SumAtMaxLevel(Node root)
{
  // Map to store level wise sum.
  Dictionary<int,int> mp = new Dictionary<int,int>();

  // Queue for performing Level
  // Order Traversal. First entry
  // is the node and second entry
  // is the level of this node.
  Queue q = new Queue();

  // Root has level 0.
  q.Enqueue(new Pair(root, 0));

  while (q.Count != 0)
  {
    // Get the node from
    // front of Queue.
    Pair temp = (Pair)q.Dequeue();

    // Get the depth of
    // current node.
    int depth = temp.data;

    // Add the value of this
    // node in map.
    if (!mp.ContainsKey(depth))
      mp[depth]= 0;

    mp[depth] = mp[depth]+temp.node.data;

    // Push children of this node,
    // with increasing the depth.
    if (temp.node.left != null)
      q.Enqueue(new Pair(temp.node.left,
                     depth + 1));

    if (temp.node.right != null)
      q.Enqueue(new Pair(temp.node.right,
                     depth + 1));
  }

  return mp.Values.Last();
}

// Driver Code
public static void Main(string[] args)
{
  Node root = new Node(1);
  root.left = new Node(2);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(5);
  root.right.left = new Node(6);
  root.right.right = new Node(7);

  Console.WriteLine(SumAtMaxLevel(root));
}     
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to calculate
// the sum of nodes at the maximum
// depth of a binary tree
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

class Pair
{
    constructor(node, data)
    {
        this.node = node;
        this.data = data;
    }
}

// Function to return the sum
function SumAtMaxLevel(root)
{

    // Map to store level wise sum.
    var mp = new Map();

    // Queue for performing Level
    // Order Traversal. First entry
    // is the node and second entry
    // is the level of this node.
    var q = [];

    // Root has level 0.
    q.push(new Pair(root, 0));

    while (q.length != 0)
    {

        // Get the node from
        // front of Queue.
        var temp = q.pop();

        // Get the depth of
        // current node.
        var depth = temp.data;

        // Add the value of this
        // node in map.
        if (!mp.has(depth))
            mp.set(depth, 0);

        mp.set(depth, mp.get(depth) +
                      temp.node.data)

        // Push children of this node,
        // with increasing the depth.
        if (temp.node.left != null)
            q.push(new Pair(temp.node.left,
                            depth + 1));

        if (temp.node.right != null)
            q.push(new Pair(temp.node.right,
                            depth + 1));
    }
    return [...mp][mp.size - 1][1];
}

// Driver Code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);

document.write(SumAtMaxLevel(root));

// This code is contributed by famously

</script>
```

**Output:** 

```
22
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)