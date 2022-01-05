# 节点的最大节点数小于其子树中的值

> 原文:[https://www . geesforgeks . org/节点在其子树中具有小于其值的最大节点数/](https://www.geeksforgeeks.org/node-having-maximum-number-of-nodes-less-than-its-value-in-its-subtree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是从给定的树中找到节点，该树在其子树中具有最大数量的节点，其值小于该节点的值。如果多个可能的节点具有相同的最大节点数，则返回任何这样的节点。

**示例:**

> **输入:**
> 
> 4
> /\
> 6 10
> /\/\
> 2 3 7 14
> /
> 5
> 
> **输出:** 6
> **说明:**
> 值为 6 的节点在 as (2，3，5)即 3 的 6 的子树中具有小于 6 的最大节点数。
> 
> **输入:**
> 10
> /
> 21
> /\
> 2 4
> \
> 11
> 
> **输出:** 21
> **说明:**
> 值为 21 的节点在 as (2，4，11)即 3 的 21 的子树中具有小于 21 的最大节点数。

**方法:**思路是使用[后序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal/)。以下是步骤:

1.  对给定的树执行后顺序遍历。
2.  将左侧子树和右侧子树的节点与其根值进行比较，如果小于根值，则存储小于根节点的节点。
3.  在每个节点上使用上述步骤，找到节点数，然后选择具有最大节点数的节点，其键小于当前节点。
4.  在上述遍历之后，打印该节点，该节点具有比该节点更小的节点值的最大计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the nodes to be deleted
unordered_map<int, bool> mp;

// Structure of a Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to compare the current node
// key with keys received from it left
// & right tree by Post Order traversal
vector<int> findNodes(Node* root, int& max_v,
                      int& rootIndex)
{
    // Base Case
    if (!root) {
        return vector<int>{};
    }

    // Find nodes lesser than the current
    // root in the left subtree
    vector<int> left
        = findNodes(root->left, max_v,
                    rootIndex);

    // Find nodes lesser than the current
    // root in the right subtree
    vector<int> right
        = findNodes(root->right, max_v,
                    rootIndex);

    // Stores all the nodes less than
    // the current node's
    vector<int> combined;
    int count = 0;

    // Add the nodes which are less
    // than current node in left[]
    for (int i = 0;
         i < left.size(); i++) {

        if (left[i] < root->key) {
            count += 1;
        }
        combined.push_back(left[i]);
    }

    // Add the nodes which are less
    // than current node in right[]
    for (int i = 0;
         i < right.size(); i++) {

        if (right[i] < root->key) {
            count += 1;
        }
        combined.push_back(right[i]);
    }

    // Create a combined vector for
    // pass to it's parent
    combined.push_back(root->key);

    // Stores key that has maximum nodes
    if (count > max_v) {
        rootIndex = root->key;
        max_v = count;
    }

    // Return the vector of nodes
    return combined;
}

// Driver Code
int main()
{
    /*
              3
           /     \
           4        6
         /  \     /   \
       10    2   4     5
    */

    // Given Tree
    Node* root = newNode(3);
    root->left = newNode(4);
    root->right = newNode(6);
    root->right->left = newNode(4);
    root->right->right = newNode(5);
    root->left->left = newNode(10);
    root->left->right = newNode(2);

    int max_v = 0;
    int rootIndex = -1;

    // Function Call
    findNodes(root, max_v, rootIndex);

    // Print the node value
    cout << rootIndex;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Stores the nodes to be deleted
static HashMap<Integer,
               Boolean> mp = new HashMap<Integer,
                                         Boolean>();
static int max_v, rootIndex;
// Structure of a Tree node
static class Node
{
  int key;
  Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
  Node temp = new Node();
  temp.key = key;
  temp.left = temp.right = null;
  return (temp);
}

// Function to compare the current node
// key with keys received from it left
// & right tree by Post Order traversal
static Vector<Integer> findNodes(Node root)
{
  // Base Case
  if (root == null)
  {
    return new Vector<Integer>();
  }

  // Find nodes lesser than the current
  // root in the left subtree
  Vector<Integer> left = findNodes(root.left);

  // Find nodes lesser than the current
  // root in the right subtree
  Vector<Integer> right = findNodes(root.right);

  // Stores all the nodes less than
  // the current node's
  Vector<Integer> combined = new Vector<Integer>();
  int count = 0;

  // Add the nodes which are less
  // than current node in left[]
  for (int i = 0; i < left.size(); i++)
  {
    if (left.get(i) < root.key)
    {
      count += 1;
    }
    combined.add(left.get(i));
  }

  // Add the nodes which are less
  // than current node in right[]
  for (int i = 0; i < right.size(); i++)
  {
    if (right.get(i) < root.key)
    {
      count += 1;
    }
    combined.add(right.get(i));
  }

  // Create a combined vector for
  // pass to it's parent
  combined.add(root.key);

  // Stores key that has maximum nodes
  if (count > max_v)
  {
    rootIndex = root.key;
    max_v = count;
  }

  // Return the vector of nodes
  return combined;
}

// Driver Code
public static void main(String[] args)
{
  /*
              3
           /     \
          4       6
         /  \    /  \
       10    2  4    5
    */

  // Given Tree
  Node root = newNode(3);
  root.left = newNode(4);
  root.right = newNode(6);
  root.right.left = newNode(4);
  root.right.right = newNode(5);
  root.left.left = newNode(10);
  root.left.right = newNode(2);

  max_v = 0;
  rootIndex = -1;

  // Function Call
  findNodes(root);

  // Print the node value
  System.out.print(rootIndex);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the nodes to be deleted
max_v = 0
rootIndex  = 0
mp = {}

# Structure of a Tree node
class newNode:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to compare the current node
# key with keys received from it left
# & right tree by Post Order traversal
def findNodes(root):

    global max_v
    global rootIndex
    global mp

    # Base Case
    if (root == None):
        return []

    # Find nodes lesser than the current
    # root in the left subtree
    left = findNodes(root.left)

    # Find nodes lesser than the current
    # root in the right subtree
    right = findNodes(root.right)

    # Stores all the nodes less than
    # the current node's
    combined = []
    count = 0

    # Add the nodes which are less
    # than current node in left[]
    for i in range(len(left)):
        if (left[i] < root.key):
            count += 1

        combined.append(left[i])

    # Add the nodes which are less
    # than current node in right[]
    for i in range(len(right)):
        if (right[i] < root.key):
            count += 1

        combined.append(right[i])

    # Create a combined vector for
    # pass to it's parent
    combined.append(root.key)

    # Stores key that has maximum nodes
    if (count > max_v):
        rootIndex = root.key
        max_v = count

    # Return the vector of nodes
    return combined

# Driver Code
if __name__ == '__main__':

    '''
               3
            /     \
           4       6
          / \     / \
        10   2   4   5
    '''

    # Given Tree
    root = None
    root = newNode(3)
    root.left = newNode(4)
    root.right = newNode(6)
    root.right.left = newNode(4)
    root.right.right = newNode(5)
    root.left.left = newNode(10)
    root.left.right = newNode(2)

    max_v = 0
    rootIndex = -1

    # Function Call
    findNodes(root)

    # Print the node value
    print(rootIndex)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Stores the nodes to be deleted
static Dictionary<int,
                  Boolean> mp = new Dictionary<int,
                                               Boolean>();
static int max_v, rootIndex;

// Structure of a Tree node
class Node
{
    public int key;
    public Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to compare the current node
// key with keys received from it left
// & right tree by Post Order traversal
static List<int> findNodes(Node root)
{

    // Base Case
    if (root == null)
    {
        return new List<int>();
    }

    // Find nodes lesser than the current
    // root in the left subtree
    List<int> left = findNodes(root.left);

    // Find nodes lesser than the current
    // root in the right subtree
    List<int> right = findNodes(root.right);

    // Stores all the nodes less than
    // the current node's
    List<int> combined = new List<int>();
    int count = 0;

    // Add the nodes which are less
    // than current node in []left
    for(int i = 0; i < left.Count; i++)
    {
        if (left[i] < root.key)
        {
            count += 1;
        }
        combined.Add(left[i]);
    }

    // Add the nodes which are less
    // than current node in []right
    for(int i = 0; i < right.Count; i++)
    {
        if (right[i] < root.key)
        {
            count += 1;
        }
        combined.Add(right[i]);
    }

    // Create a combined vector for
    // pass to it's parent
    combined.Add(root.key);

    // Stores key that has maximum nodes
    if (count > max_v)
    {
        rootIndex = root.key;
        max_v = count;
    }

    // Return the vector of nodes
    return combined;
}

// Driver Code
public static void Main(String[] args)
{
    /*
               3
            /     \
           4      6
          / \    / \
        10   2  4   5
        */

    // Given Tree
    Node root = newNode(3);
    root.left = newNode(4);
    root.right = newNode(6);
    root.right.left = newNode(4);
    root.right.right = newNode(5);
    root.left.left = newNode(10);
    root.left.right = newNode(2);

    max_v = 0;
    rootIndex = -1;

    // Function call
    findNodes(root);

    // Print the node value
    Console.Write(rootIndex);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Stores the nodes to be deleted
    let mp = new Map();

    let max_v, rootIndex;

    // Structure of a Tree node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
      let temp = new Node(key);
      return (temp);
    }

    // Function to compare the current node
    // key with keys received from it left
    // & right tree by Post Order traversal
    function findNodes(root)
    {
      // Base Case
      if (root == null)
      {
        return [];
      }

      // Find nodes lesser than the current
      // root in the left subtree
      let left = findNodes(root.left);

      // Find nodes lesser than the current
      // root in the right subtree
      let right = findNodes(root.right);

      // Stores all the nodes less than
      // the current node's
      let combined = [];
      let count = 0;

      // Add the nodes which are less
      // than current node in left[]
      for (let i = 0; i < left.length; i++)
      {
        if (left[i] < root.key)
        {
          count += 1;
        }
        combined.push(left[i]);
      }

      // Add the nodes which are less
      // than current node in right[]
      for (let i = 0; i < right.length; i++)
      {
        if (right[i] < root.key)
        {
          count += 1;
        }
        combined.push(right[i]);
      }

      // Create a combined vector for
      // pass to it's parent
      combined.push(root.key);

      // Stores key that has maximum nodes
      if (count > max_v)
      {
        rootIndex = root.key;
        max_v = count;
      }

      // Return the vector of nodes
      return combined;
    }

    /*
              3
           /     \
          4       6
         /  \    /  \
       10    2  4    5
    */

    // Given Tree
    let root = newNode(3);
    root.left = newNode(4);
    root.right = newNode(6);
    root.right.left = newNode(4);
    root.right.right = newNode(5);
    root.left.left = newNode(10);
    root.left.right = newNode(2);

    max_v = 0;
    rootIndex = -1;

    // Function Call
    findNodes(root);

    // Print the node value
    document.write(rootIndex);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*