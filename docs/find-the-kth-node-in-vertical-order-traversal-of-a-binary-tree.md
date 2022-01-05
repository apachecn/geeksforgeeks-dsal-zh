# 在二叉树的垂直顺序遍历中找到第 kth 个节点

> 原文:[https://www . geesforgeks . org/find-the-kth-node-in-vertical-order-遍历二叉树/](https://www.geeksforgeeks.org/find-the-kth-node-in-vertical-order-traversal-of-a-binary-tree/)

给定一棵二叉树和一个整数 **k** ，任务是打印二叉树的 [**垂直顺序遍历**](https://www.geeksforgeeks.org/print-binary-tree-vertical-order/) 中的第 kth 个节点。如果不存在这样的节点，则打印 **-1** 。
二叉树的垂直顺序遍历是指垂直打印。
**示例:**

```
Input: 
           1
         /   \
       2       3
     /  \     /  \
   4     5   6    7
              \    \
               8    9  
k = 3
Output: 1
The vertical order traversal of above tree is:
4
2
1 5 6
3 8
7
9

Input:
           1
         /   \
       2       3
     /  \     /  \
   4     5   6    7
              \    \
               8    9
k = 13
Output: -1
```

**方法:**思路是执行[垂直顺序遍历](https://www.geeksforgeeks.org/print-a-binary-tree-in-vertical-order-set-3-using-level-order-traversal/)并检查当前节点是否为第 kth 个节点然后打印其值，如果树中的节点数小于 K 则打印-1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure for a binary tree node
struct Node {
    int key;
    Node *left, *right;
};

// A utility function to create a new node
Node* newNode(int key)
{
    Node* node = new Node;
    node->key = key;
    node->left = node->right = NULL;
    return node;
}

// Function to find kth node
// in vertical order traversal
int KNodeVerticalOrder(Node* root, int k)
{
    // Base case
    if (!root || k == 0)
        return -1;

    int n = 0;

    // Variable to store kth node
    int k_node = -1;

    // Create a map and store vertical order in
    // map
    map<int, vector<int> > m;
    int hd = 0;

    // Create queue to do level order traversal
    // Every item of queue contains node and
    // horizontal distance
    queue<pair<Node*, int> > que;
    que.push(make_pair(root, hd));

    while (!que.empty()) {
        // Pop from queue front
        pair<Node*, int> temp = que.front();
        que.pop();
        hd = temp.second;
        Node* node = temp.first;

        // Insert this node's data in vector of hash
        m[hd].push_back(node->key);

        if (node->left != NULL)
            que.push(make_pair(node->left, hd - 1));
        if (node->right != NULL)
            que.push(make_pair(node->right, hd + 1));
    }

    // Traverse the map and find kth
    // node
    map<int, vector<int> >::iterator it;
    for (it = m.begin(); it != m.end(); it++) {
        for (int i = 0; i < it->second.size(); ++i) {
            n++;
            if (n == k)
                return (it->second[i]);
        }
    }

    if (k_node == -1)
        return -1;
}

// Driver code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);
    root->right->right->right = newNode(9);
    root->right->right->left = newNode(10);
    root->right->right->left->right = newNode(11);
    root->right->right->left->right->right = newNode(12);

    int k = 5;
    cout << KNodeVerticalOrder(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Map;
import java.util.Queue;
import java.util.SortedMap;
import java.util.TreeMap;

class GFG{

// Structure for a binary tree node
static class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        this.left = this.right = null;
    }
};

static class Pair
{
    Node first;
    int second;

    public Pair(Node first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find kth node
// in vertical order traversal
static int KNodeVerticalOrder(Node root, int k)
{

    // Base case
    if (root == null || k == 0)
        return -1;

    int n = 0;

    // Variable to store kth node
    int k_node = -1;

    // Create a map and store vertical order in
    // map
    SortedMap<Integer,
    ArrayList<Integer>> m = new TreeMap<Integer,
                              ArrayList<Integer>>();
    int hd = 0;

    // Create queue to do level order traversal
    // Every item of queue contains node and
    // horizontal distance
    Queue<Pair> que = new LinkedList<>();
    que.add(new Pair(root, hd));

    while (!que.isEmpty())
    {

        // Pop from queue front
        Pair temp = que.poll();
        hd = temp.second;
        Node node = temp.first;

        // Insert this node's data in
        // vector of hash
        if (m.get(hd) == null)
            m.put(hd, new ArrayList<>());

        m.get(hd).add(node.key);

        if (node.left != null)
            que.add(new Pair(node.left, hd - 1));
        if (node.right != null)
            que.add(new Pair(node.right, hd + 1));
    }

    // Traverse the map and find kth
    // node
    for(Map.Entry<Integer,
        ArrayList<Integer>> it : m.entrySet())
    {
        for(int i = 0;
                i < it.getValue().size();
                i++)
        {
            n++;
            if (n == k)
            {
                return it.getValue().get(i);
            }
        }
    }

    if (k_node == -1)
        return -1;

    return 0;
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.right.left.right = new Node(8);
    root.right.right.right = new Node(9);
    root.right.right.left = new Node(10);
    root.right.right.left.right = new Node(11);
    root.right.right.left.right.right = new Node(12);

    int k = 5;

    System.out.println(KNodeVerticalOrder(root, k));

}
}

 // This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Tree node structure
class Node:

    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Function to find kth node
# in vertical order traversal
def KNodeVerticalOrder(root, k):

    # Base case
    if not root or k == 0:
        return -1

    n = 0

    # Variable to store kth node
    k_node = -1

    # Create a map and store
    # vertical order in map
    m = {}
    hd = 0

    # Create queue to do level order
    # traversal Every item of queue contains
    # node and horizontal distance
    que = []
    que.append((root, hd))

    while len(que) > 0:

        # Pop from queue front
        temp = que.pop(0)
        hd = temp[1]
        node = temp[0]

        # Insert this node's data in vector of hash
        if hd not in m: m[hd] = []
        m[hd].append(node.key)

        if node.left != None:
            que.append((node.left, hd - 1))
        if node.right != None:
            que.append((node.right, hd + 1))

    # Traverse the map and find kth node
    for it in sorted(m):
        for i in range(0, len(m[it])):
            n += 1
            if n == k:
                return m[it][i]

    if k_node == -1:
        return -1

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.right.left.right = Node(8)
    root.right.right.right = Node(9)
    root.right.right.left = Node(10)
    root.right.right.left.right = Node(11)
    root.right.right.left.right.right = Node(12)

    k = 5
    print(KNodeVerticalOrder(root, k))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System.Collections.Generic;
using System.Collections;
using System;
class GFG{

// Structure for a
// binary tree node
class Node
{
  public int key;
  public Node left,
              right;

  public Node(int key)
  {
    this.key = key;
    this.left =
    this.right = null;
  }
};

class Pair
{
  public Node first;
  public int second;

  public Pair(Node first,
              int second)
  {
    this.first = first;
    this.second = second;
  }
}

// Function to find kth node
// in vertical order traversal
static int KNodeVerticalOrder(Node root,
                              int k)
{    
  // Base case
  if (root == null || k == 0)
    return -1;

  int n = 0;

  // Variable to store
  // kth node
  int k_node = -1;

  // Create a map and store
  // vertical order in map
  SortedDictionary<int,
                   ArrayList> m =
                   new SortedDictionary<int,
                                        ArrayList>();
  int hd = 0;

  // Create queue to do level order
  // traversal. Every item of queue
  // contains node and horizontal
  // distance
  Queue que = new Queue();

  que.Enqueue(new KeyValuePair<Node,
                               int>(root,
                                    hd));

  while(que.Count != 0)
  {
    // Pop from queue front
    KeyValuePair<Node,
                 int> temp =
                 (KeyValuePair<Node,
                               int>)que.Dequeue();
    hd = temp.Value;
    Node node = temp.Key;

    // Insert this node's data in
    // vector of hash
    if (!m.ContainsKey(hd))
      m[hd] = new ArrayList();

    m[hd].Add(node.key);

    if (node.left != null)
      que.Enqueue(
      new KeyValuePair<Node,
                       int>(node.left,
                            hd - 1));
    if (node.right != null)
      que.Enqueue(
      new KeyValuePair<Node,
                       int>(node.right,
                            hd + 1));
  }

  // Traverse the map and find kth
  // node
  foreach(KeyValuePair<int,
                       ArrayList> it in m)
  {
    for(int i = 0; i < it.Value.Count; i++)
    {
      n++;
      if (n == k)
      {
        return (int)it.Value[i];
      }
    }
  }

  if (k_node == -1)
    return -1;

  return 0;
}

// Driver code
public static void Main(string[] args)
{
  Node root = new Node(1);
  root.left = new Node(2);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(5);
  root.right.left = new Node(6);
  root.right.right = new Node(7);
  root.right.left.right = new Node(8);
  root.right.right.right = new Node(9);
  root.right.right.left = new Node(10);
  root.right.right.left.right = new Node(11);
  root.right.right.left.right.right = new Node(12);

  int k = 5;
  Console.Write(KNodeVerticalOrder(root, k));
}
}

// This code is contributed by Rutvik_56
```

**Output:** 

```
6
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)