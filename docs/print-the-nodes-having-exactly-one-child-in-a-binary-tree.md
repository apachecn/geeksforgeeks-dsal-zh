# 打印二叉树中正好有一个子节点的节点

> 原文:[https://www . geeksforgeeks . org/print-the-nodes-with-the-twist-in-one-child-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-nodes-having-exactly-one-child-in-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印所有恰好有一个子节点的节点。如果不存在这样的节点，则打印“-1”。
**例:**

```
Input: 
            2
           / \
          3   5
         /   / \
        7   8   6
Output: 3
Explanation:
There is only one node having
single child that is 3.

Input:
           9
          / \
         7   8
            / \
           4   3
Output: -1
Explanation:
There is no node having exactly one
child in the binary tree. 
```

**方法:**想法是在[中遍历树，以便遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并且在遍历的每一步检查节点是否正好有一个子节点。然后将该节点追加到结果数组中，以跟踪这些节点。遍历之后，只需打印这个结果数组的每个元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to print
// the nodes having a single child
#include <bits/stdc++.h>
using namespace std;

// Class of the Binary Tree node
struct Node
{
  int data;
  Node *left, *right;

  Node(int x)
  {
    data = x;
    left = right = NULL;
  }
};

vector<int> lst;

// Function to find the nodes
// having single child
void printNodesOneChild(Node* root)
{
  // Base case
  if (root == NULL)
    return;

  // Condition to check if the
  // node is having only one child
  if (root->left != NULL &&
      root->right == NULL ||
      root->left == NULL &&
      root->right != NULL)
  {
    lst.push_back(root->data);
  }

  // Traversing the left child
  printNodesOneChild(root -> left);

  // Traversing the right child
  printNodesOneChild(root -> right);
}

//Driver code
int main()
{
  // Constructing the binary tree
  Node *root = new Node(2);
  root -> left = new Node(3);
  root -> right = new Node(5);
  root -> left -> left = new Node(7);
  root -> right -> left = new Node(8);
  root -> right -> right = new Node(6);

  // Function calling
  printNodesOneChild(root);

  // Condition to check if there is
  // no such node having single child
  if (lst.size() == 0)
    printf("-1");
  else
  {
    for(int value : lst)
    {
      cout << (value) << endl;
    }
  }
}

// This code is contributed by Mohit Kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// the nodes having a single child
import java.util.Vector;

// Class of the Binary Tree node
class Node
{
    int data;
    Node left, right;

    Node(int data)
    {
        this.data = data;
    }
}

class GFG{

// List to keep track of nodes
// having single child
static Vector<Integer> list = new Vector<>();

// Function to find the nodes 
// having single child 
static void printNodesOneChild(Node root)
{
    // Base case
    if (root == null)
        return;

    // Condition to check if the node
    // is having only one child
    if (root.left != null && root.right == null ||
        root.left == null && root.right != null)
    {
        list.add(root.data);
    }

    // Traversing the left child
    printNodesOneChild(root.left);

    // Traversing the right child
    printNodesOneChild(root.right);
}

// Driver code
public static void main(String[] args)
{

    // Constructing the binary tree
    Node root = new Node(2);
    root.left = new Node(3);
    root.right = new Node(5);
    root.left.left = new Node(7);
    root.right.left = new Node(8);
    root.right.right = new Node(6);

    // Function calling
    printNodesOneChild(root);

    // Condition to check if there is
    // no such node having single child
    if (list.size() == 0)
        System.out.println(-1);
    else
    {
        for(int value : list)
        {
            System.out.println(value);
        }
    }
}
}

// This code is contributed by sumit_9
```

## 蟒蛇 3

```
# Python3 implementation to print
# the nodes having a single child

# Class of the Binary Tree node
class node:

    # Constructor to construct
    # the node of the Binary tree
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# List to keep track of
# nodes having single child
single_child_nodes = []

# Function to find the nodes
# having single child
def printNodesOneChild(root):

    # Base Case
    if not root:
        return

    # Condition to check if the node
    # is having only one child
    if not root.left and root.right:
        single_child_nodes.append(root)
    elif root.left and not root.right:
        single_child_nodes.append(root)

    # Traversing the left child
    printNodesOneChild(root.left)

    # Traversing the right child
    printNodesOneChild(root.right)
    return

# Driver Code
if __name__ == "__main__":

    # Condtruction of Binary Tree
    root = node(2)
    root.left = node(3)
    root.right = node(5)
    root.left.left = node(7)
    root.right.left = node(8)
    root.right.right = node(6)

    # Function Call
    printNodesOneChild(root)

    # Condition to check if there is
    # no such node having single child
    if not len(single_child_nodes):
        print(-1)
    else:
        for i in single_child_nodes:
            print(i.val, end = " ")
        print()
```

## C#

```
// C# implementation to print
// the nodes having a single child
using System;
using System.Collections;

class GFG{

// Structure of binary tree
public class Node 
{
    public Node left;
    public Node right;
    public int data;
};

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

// List to keep track of nodes
// having single child
static ArrayList list = new ArrayList();

// Function to find the nodes 
// having single child 
static void printNodesOneChild(Node root)
{

    // Base case
    if (root == null)
        return;

    // Condition to check if the node
    // is having only one child
    if (root.left != null && root.right == null ||
        root.left == null && root.right != null)
    {
        list.Add(root.data);
    }

    // Traversing the left child
    printNodesOneChild(root.left);

    // Traversing the right child
    printNodesOneChild(root.right);
}

// Driver code
static public void Main()
{

    // Constructing the binary tree
    Node root = newNode(2);
    root.left = newNode(3);
    root.right = newNode(5);
    root.left.left = newNode(7);
    root.right.left = newNode(8);
    root.right.right = newNode(6);

    // Function calling
    printNodesOneChild(root);

    // Condition to check if there is
    // no such node having single child
    if (list.Count == 0)
        Console.WriteLine(-1);
    else
    {
        foreach(int value in list)
        {
            Console.WriteLine(value);
        }
    }
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// Javascript implementation to print
// the nodes having a single child

// Class of the Binary Tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left=this.right=null;
    }

}

// List to keep track of nodes
// having single child
let list = [];

// Function to find the nodes
// having single child
function printNodesOneChild(root)
{
    // Base case
    if (root == null)
        return;

    // Condition to check if the node
    // is having only one child
    if (root.left != null && root.right == null ||
        root.left == null && root.right != null)
    {
        list.push(root.data);
    }

    // Traversing the left child
    printNodesOneChild(root.left);

    // Traversing the right child
    printNodesOneChild(root.right);
}

// Driver code
// Constructing the binary tree
    let root = new Node(2);
    root.left = new Node(3);
    root.right = new Node(5);
    root.left.left = new Node(7);
    root.right.left = new Node(8);
    root.right.right = new Node(6);

    // Function calling
    printNodesOneChild(root);

    // Condition to check if there is
    // no such node having single child
    if (list.length == 0)
        document.write(-1);
    else
    {
        document.write(list.join("<br>"))
    }

// This code is contributed by patel2127
</script>
```

**Output**

```
3
```