# 对二叉树中每一级的小于当前级最小值节点的所有下级节点进行计数

> 原文:[https://www . geesforgeks . org/count-来自所有较低级别的节点-小于当前级别的最小值-二叉树中每一级别的节点/](https://www.geeksforgeeks.org/count-nodes-from-all-lower-levels-smaller-than-minimum-valued-node-of-current-level-for-every-level-in-a-binary-tree/)

给定一个[**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，每个级别的任务是打印所有较低级别的节点总数，该总数小于或等于该级别的每个节点。

**示例:**

> **输入:**下面是给定的树:
> 4
> /\
> 3 5
> /\/\
> 10 2 3 1
> 
> **输出:** 4 3 0
> **说明:**
> 1 级节点有 4 个，分别为 2 级的(3)和 3 级的(2，3，1)。
> 2 级节点有 3 个 3 级节点(2，3，1)。
> 3 级节点下面没有剩余的等级。
> 
> **输入:**下面是给定的树:
> 
> **4
> /\
> 7 9
> /\
> 1 3 1** 
> 
> ****输出:** 3 3 0**

****方法:**按照以下步骤解决问题:**

1.  **使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)计算每一级的最小值。**
2.  **对树执行[后顺序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，检查每个节点在步骤 1 中计算的节点是否大于或等于该节点。如果发现为真，则在该级别将计数增加 1，前提是该特定级别在其下一级别中存在的节点的值小于或等于该级别中存在的所有节点。**
3.  **打印给出该级别节点数的最终数组。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program of the
// above approach

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

// Function to find the min value
// of node for each level
void calculateMin(Node* root,
                  vector<int>& levelMin)
{
    queue<Node*> qt;
    qt.push(root);

    // Count is used to differentiate
    // each level of the tree
    int count = 1;
    int min_v = INT_MAX;
    while (!qt.empty()) {

        Node* temp = qt.front();

        min_v = min(min_v, temp->key);

        qt.pop();

        if (temp->left) {
            qt.push(temp->left);
        }
        if (temp->right) {
            qt.push(temp->right);
        }
        count--;
        if (count == 0) {
            levelMin.push_back(min_v);
            min_v = INT_MAX;
            count = qt.size();
        }
    }
}

// Function to check whether the nodes in
// the level below it are smaller
// by performing post order traversal
void findNodes(Node* root, vector<int>& levelMin,
               vector<int>& levelResult, int level)
{
    if (root == NULL)
        return;

    // Traverse the left subtree
    findNodes(root->left, levelMin,
              levelResult, level + 1);

    // Traverse right subtree
    findNodes(root->right, levelMin,
              levelResult, level + 1);

    // Check from minimum values
    // computed at each level
    for (int i = 0; i < level; i++) {
        if (root->key <= levelMin[i]) {
            levelResult[i] += 1;
        }
    }
}

// Function to print count of
// nodes from all lower levels
// having values less than the
// the nodes in the current level
void printNodes(Node* root)
{
    vector<int> levelMin;
    calculateMin(root, levelMin);

    // Stores the number of levels
    int numLevels = levelMin.size();

    // Stores the required count
    // of nodes for each level
    vector<int> levelResult(numLevels, 0);
    findNodes(root, levelMin, levelResult, 0);

    for (int i = 0; i < numLevels; i++) {
        cout << levelResult[i] << " ";
    }
}

// Driver Code
int main()
{
    /*
              4
           /     \
           3        5
         /  \     /   \
       10    2   3     1
      */

    Node* root = newNode(4);

    root->left = newNode(3);
    root->right = newNode(5);

    root->right->left = newNode(3);
    root->right->right = newNode(1);

    root->left->left = newNode(10);
    root->left->right = newNode(2);
    printNodes(root);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program of the
// above approach
import java.util.*;
class GFG{

// Stores the nodes to be deleted
static Map<Integer,
           Boolean> mp = new HashMap<Integer,
                                     Boolean>();

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

// Function to find the min value
// of node for each level
static void calculateMin(Node root,
                         Vector<Integer> levelMin)
{
  Queue<Node> qt = new LinkedList<>();
  qt.add(root);

  // Count is used to differentiate
  // each level of the tree
  int count = 1;
  int min_v = Integer.MAX_VALUE;
  while (!qt.isEmpty())
  {
    Node temp = qt.peek();
    min_v = Math.min(min_v, temp.key);
    qt.remove();

    if (temp.left != null)
    {
      qt.add(temp.left);
    }
    if (temp.right != null)
    {
      qt.add(temp.right);
    }
    count--;
    if (count == 0)
    {
      levelMin.add(min_v);
      min_v = Integer.MAX_VALUE;
      count = qt.size();
    }
  }
}

// Function to check whether the nodes in
// the level below it are smaller
// by performing post order traversal
static void findNodes(Node root,
                      Vector<Integer> levelMin,
                      int []levelResult, int level)
{
  if (root == null)
    return;

  // Traverse the left subtree
  findNodes(root.left, levelMin,
            levelResult, level + 1);

  // Traverse right subtree
  findNodes(root.right, levelMin,
            levelResult, level + 1);

  // Check from minimum values
  // computed at each level
  for (int i = 0; i < level; i++)
  {
    if (root.key <= levelMin.get(i))
    {
      levelResult[i] += 1;
    }
  }
}

// Function to print count of
// nodes from all lower levels
// having values less than the
// the nodes in the current level
static void printNodes(Node root)
{
  Vector<Integer> levelMin =
         new Vector<Integer>();
  calculateMin(root, levelMin);

  // Stores the number of levels
  int numLevels = levelMin.size();

  // Stores the required count
  // of nodes for each level
  int []levelResult = new int[numLevels];
  findNodes(root, levelMin, levelResult, 0);

  for (int i = 0; i < numLevels; i++)
  {
    System.out.print(levelResult[i] + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  /*
              4
           /     \
           3        5
         /  \     /   \
       10    2   3     1
      */

  Node root = newNode(4);

  root.left = newNode(3);
  root.right = newNode(5);

  root.right.left = newNode(3);
  root.right.right = newNode(1);

  root.left.left = newNode(10);
  root.left.right = newNode(2);
  printNodes(root);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program of the
# above approach
from collections import deque
from sys import maxsize as INT_MAX

# Stores the nodes to be deleted
mp = dict()

# Structure of a Tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to find the min value
# of node for each level
def calculateMin(root: Node,
             levelMin: list) -> None:

    qt = deque()
    qt.append(root)

    # Count is used to differentiate
    # each level of the tree
    count = 1
    min_v = INT_MAX

    while (qt):
        temp = qt.popleft()
        min_v = min(min_v, temp.key)

        if (temp.left):
            qt.append(temp.left)

        if (temp.right):
            qt.append(temp.right)

        count -= 1

        if (count == 0):
            levelMin.append(min_v)
            min_v = INT_MAX
            count = len(qt)

# Function to check whether the nodes in
# the level below it are smaller
# by performing post order traversal
def findNodes(root: Node,
          levelMin: list,
       levelResult: list,
             level: int) -> None:

    if (root == None):
        return

    # Traverse the left subtree
    findNodes(root.left, levelMin,
              levelResult, level + 1)

    # Traverse right subtree
    findNodes(root.right, levelMin,
              levelResult, level + 1)

    # Check from minimum values
    # computed at each level
    for i in range(level):
        if (root.key <= levelMin[i]):
            levelResult[i] += 1

# Function to print count of
# nodes from all lower levels
# having values less than the
# the nodes in the current level
def printNodes(root: Node) -> None:

    levelMin = []
    calculateMin(root, levelMin)

    # Stores the number of levels
    numLevels = len(levelMin)

    # Stores the required count
    # of nodes for each level
    levelResult = [0] * numLevels
    findNodes(root, levelMin, levelResult, 0)

    for i in range(numLevels):
        print(levelResult[i], end = " ")

# Driver Code
if __name__ == "__main__":

    '''
              4
           /     \
          3        5
        /  \     /   \
      10    2   3     1
      '''

    root = Node(4)

    root.left = Node(3)
    root.right = Node(5)

    root.right.left = Node(3)
    root.right.right = Node(1)

    root.left.left = Node(10)
    root.left.right = Node(2)

    printNodes(root)

# This code is contributed by sanjeev2552
```

## **C#**

```
// C# program of the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Stores the nodes to be deleted
static Dictionary<int,
                  Boolean> mp = new Dictionary<int,
                                               Boolean>();

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

// Function to find the min value
// of node for each level
static void calculateMin(Node root,
                         List<int> levelMin)
{
    Queue<Node> qt = new Queue<Node>();
    qt.Enqueue(root);

    // Count is used to differentiate
    // each level of the tree
    int count = 1;
    int min_v = int.MaxValue;

    while (qt.Count != 0)
    {
        Node temp = qt.Peek();
        min_v = Math.Min(min_v, temp.key);
        qt.Dequeue();

        if (temp.left != null)
        {
            qt.Enqueue(temp.left);
        }
        if (temp.right != null)
        {
            qt.Enqueue(temp.right);
        }
        count--;

        if (count == 0)
        {
            levelMin.Add(min_v);
            min_v = int.MaxValue;
            count = qt.Count;
        }
    }
}

// Function to check whether the nodes in
// the level below it are smaller
// by performing post order traversal
static void findNodes(Node root,
                      List<int> levelMin,
                      int []levelResult,
                      int level)
{
    if (root == null)
        return;

    // Traverse the left subtree
    findNodes(root.left, levelMin,
              levelResult, level + 1);

    // Traverse right subtree
    findNodes(root.right, levelMin,
              levelResult, level + 1);

    // Check from minimum values
    // computed at each level
    for(int i = 0; i < level; i++)
    {
        if (root.key <= levelMin[i])
        {
            levelResult[i] += 1;
        }
    }
}

// Function to print count of
// nodes from all lower levels
// having values less than the
// the nodes in the current level
static void printNodes(Node root)
{
    List<int> levelMin = new List<int>();

    calculateMin(root, levelMin);

    // Stores the number of levels
    int numLevels = levelMin.Count;

    // Stores the required count
    // of nodes for each level
    int []levelResult = new int[numLevels];
    findNodes(root, levelMin, levelResult, 0);

    for(int i = 0; i < numLevels; i++)
    {
        Console.Write(levelResult[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
/*
           4
         /     \
        3      5
       / \     / \
     10   2 3    1
    */

    Node root = newNode(4);

    root.left = newNode(3);
    root.right = newNode(5);

    root.right.left = newNode(3);
    root.right.right = newNode(1);

    root.left.left = newNode(10);
    root.left.right = newNode(2);
    printNodes(root);
}
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>

    // JavaScript program for the above approach

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

    // Function to find the min value
    // of node for each level
    function calculateMin(root, levelMin)
    {
      let qt = [];
      qt.push(root);

      // Count is used to differentiate
      // each level of the tree
      let count = 1;
      let min_v = Number.MAX_VALUE;
      while (qt.length > 0)
      {
        let temp = qt[0];
        min_v = Math.min(min_v, temp.key);
        qt.shift();

        if (temp.left != null)
        {
          qt.push(temp.left);
        }
        if (temp.right != null)
        {
          qt.push(temp.right);
        }
        count--;
        if (count == 0)
        {
          levelMin.push(min_v);
          min_v = Number.MAX_VALUE;
          count = qt.length;
        }
      }
    }

    // Function to check whether the nodes in
    // the level below it are smaller
    // by performing post order traversal
    function findNodes(root, levelMin, levelResult, level)
    {
      if (root == null)
        return;

      // Traverse the left subtree
      findNodes(root.left, levelMin,
                levelResult, level + 1);

      // Traverse right subtree
      findNodes(root.right, levelMin,
                levelResult, level + 1);

      // Check from minimum values
      // computed at each level
      for (let i = 0; i < level; i++)
      {
        if (root.key <= levelMin[i])
        {
          levelResult[i] += 1;
        }
      }
    }

    // Function to print count of
    // nodes from all lower levels
    // having values less than the
    // the nodes in the current level
    function printNodes(root)
    {
      let levelMin = [];
      calculateMin(root, levelMin);

      // Stores the number of levels
      let numLevels = levelMin.length;

      // Stores the required count
      // of nodes for each level
      let levelResult = new Array(numLevels);
      levelResult.fill(0);
      findNodes(root, levelMin, levelResult, 0);

      for (let i = 0; i < levelResult.length; i++)
      {
        document.write(levelResult[i] + " ");
      }
    }

    /*
              4
           /     \
           3        5
         /  \     /   \
       10    2   3     1
      */

    let root = newNode(4);

    root.left = newNode(3);
    root.right = newNode(5);

    root.right.left = newNode(3);
    root.right.right = newNode(1);

    root.left.left = newNode(10);
    root.left.right = newNode(2);
    printNodes(root);

</script>
```

****Output:** 

```
4 3 0
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***