# 二叉树底视图中的节点总数

> 原文：[https://www.geeksforgeeks.org/sum-of-nodes-in-bottom-view-of-binary-tree/](https://www.geeksforgeeks.org/sum-of-nodes-in-bottom-view-of-binary-tree/)

给定一个二叉树，任务是在给定的二叉树的底部视图中打印节点总数。 二叉树的底部视图是从底部查看树时可见的节点集。

**示例**：

```
Input : 
     1
    /  \
   2    3
  / \    \
 4   5    6

Output : 20

Input :
        1         
       / \         
      2    3         
       \         
         4         
          \         
            5         
             \         
               6

Output : 17

```

**方法**：想法是使用队列。

1.  将树节点放入队列以进行[层次顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)

2.  从根节点的水平距离（`hd`）0 开始，继续将左子节点与水平距离添加为`hd-1`，将右子节点添加为`hd + 1`。

3.  使用映射来存储`hd`值（作为键）和具有相应`hd`值的最后一个节点（作为对）。

4.  每次遇到新的水平距离或现有的水平距离时，都将水平距离的节点数据作为关键。 它将第一次添加到映射中，下次它将替换该值。 这将确保映射中存在该水平距离的最底部元素。

5.  最后，遍历映射并计算所有元素的总和。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of binary tree
struct Node {
    Node* left;
    Node* right;
    int hd;
    int data;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* node = new Node();
    node->left = node->right = NULL;
    node->data = key;
    return node;
}

// Function that returns the sum of
// nodes in bottom view of binary tree
int SumOfBottomView(Node* root)
{
    if (root == NULL)
        return 0;
    queue<Node*> q;

    map<int, int> m;
    int hd = 0;
    root->hd = hd;

    int sum = 0;

    // Push node and horizontal distance to queue
    q.push(root);

    while (q.size()) {
        Node* temp = q.front();
        q.pop();

        hd = temp->hd;

        // Put the dequeued tree node to Map
        // having key as horizontal distance. Every
        // time we find a node having same horizontal
        // distance we need to replace the data in
        // the map.
        m[hd] = temp->data;

        if (temp->left) {
            temp->left->hd = hd - 1;
            q.push(temp->left);
        }
        if (temp->right) {
            temp->right->hd = hd + 1;
            q.push(temp->right);
        }
    }

    map<int, int>::iterator itr;

    // Sum up all the nodes in bottom view of the tree
    for (itr = m.begin(); itr != m.end(); itr++)
        sum += itr->second;

    return sum;
}

// Driver Code
int main()
{
    Node* root = newNode(20);
    root->left = newNode(8);
    root->right = newNode(22);
    root->left->left = newNode(5);
    root->left->right = newNode(3);
    root->right->left = newNode(4);
    root->right->right = newNode(25);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(14);

    cout << SumOfBottomView(root);

    return 0;
}

```

## Python3

```py

# Python3 implementation of the approach 

class Node: 

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.hd = None

# Function that returns the Sum of 
# nodes in bottom view of binary tree 
def SumOfBottomView(root): 

    if root == None:
        return 0

    q = [] 
    m = {}
    hd, Sum = 0, 0
    root.hd = hd 

    # Push node and horizontal 
    # distance to queue 
    q.append(root) 

    while len(q) > 0: 
        temp = q.pop(0) 
        hd = temp.hd 

        # Put the dequeued tree node to Map 
        # having key as horizontal distance. 
        # Every time we find a node having 
        # same horizontal distance we need 
        # to replace the data in the map. 
        m[hd] = temp.data 

        if temp.left != None: 
            temp.left.hd = hd - 1
            q.append(temp.left) 

        if temp.right != None: 
            temp.right.hd = hd + 1
            q.append(temp.right) 

    # Sum up all the nodes in bottom 
    # view of the tree 
    for itr in m:
        Sum += m[itr] 

    return Sum

# Driver Code 
if __name__ == "__main__": 

    root = Node(20) 
    root.left = Node(8) 
    root.right = Node(22) 
    root.left.left = Node(5) 
    root.left.right = Node(3) 
    root.right.left = Node(4) 
    root.right.right = Node(25) 
    root.left.right.left = Node(10) 
    root.left.right.right = Node(14) 

    print(SumOfBottomView(root)) 

# This code is contributed by Rituraj Jain

```

## C#

```cs

// C# implementation of 
// the above approach
using System;
using System.Collections; 
using System.Collections.Generic;
class GFG
{ 
// Structure of binary tree
public class Node
{
  public Node left;
  public Node right;
  public int hd;
  public int data;
};

// Function to create 
// a new node
static Node newNode(int key) 
{
  Node node = new Node();
  node.data = key;
  node.left = null;
  node.right = null;
  return node;
}

// Function that returns the sum of
// nodes in bottom view of binary tree
static int SumOfBottomView(Node root)
{
  if (root == null)
    return 0;

  Queue q = new Queue(); 
  Dictionary<int,
             int> m = new Dictionary<int,
                                     int>();
  int hd = 0;
  root.hd = hd;
  int sum = 0;

  // Push node and horizontal 
  // distance to queue
  q.Enqueue(root);

  while (q.Count != 0) 
  {
    Node temp = (Node)q.Peek();
    q.Dequeue();
    hd = temp.hd;

    // Put the dequeued tree node 
    // to Map having key as horizontal 
    // distance. Every time we find a 
    // node having same horizontal distance 
    // we need to replace the data in
    // the map.
    m[hd] = temp.data;

    if (temp.left != null) 
    {
      temp.left.hd = hd - 1;
      q.Enqueue(temp.left);
    }
    if (temp.right != null) 
    {
      temp.right.hd = hd + 1;
      q.Enqueue(temp.right);
    }
  }    

  // Sum up all the nodes in 
  // bottom view of the tree    
  foreach(KeyValuePair<int,
                       int> itr in m)
  {
    sum += itr.Value;
  }
  return sum;
}

// Driver code 
public static void Main(string[] args) 
{
  Node root = newNode(20);
  root.left = newNode(8);
  root.right = newNode(22);
  root.left.left = newNode(5);
  root.left.right = newNode(3);
  root.right.left = newNode(4);
  root.right.right = newNode(25);
  root.left.right.left = newNode(10);
  root.left.right.right = newNode(14);
  Console.Write(SumOfBottomView(root));
}
}

// This code is contributed by rutvik_56

```

**输出**： 

```
58         

```



* * *

* * *



