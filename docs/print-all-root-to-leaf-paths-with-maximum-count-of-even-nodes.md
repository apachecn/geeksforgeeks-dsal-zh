# 打印偶数节点数最多的所有根到叶路径

> 原文:[https://www . geeksforgeeks . org/print-所有根到叶路径具有最大偶数节点数/](https://www.geeksforgeeks.org/print-all-root-to-leaf-paths-with-maximum-count-of-even-nodes/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是[打印所有可能的根到叶路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)，它们具有最大数量的偶数值节点。

**示例:**

> **输入:**
> 
> ```
>              2
>             / \
>            6   3
>           / \   \
>          4   7   11
>         / \   \
>        10  12   1
> ```
> 
> **输出:**
> 2->6->4->10
> 2->6->4->12
> T5】解释:
> 路径上偶数节点的计数 2 - > 6 - > 4 - > 10 = 4
> 路径上偶数节点的计数 2 - > 6 - > 4 - > 12 = 4 - > 7 - > 1 = 2
> 路径上偶数节点的计数 2 - > 3 - > 11 = 1
> 因此，由偶数节点的最大计数组成的路径为{2 - > 6 - > 4 - > 10}和{2 - > 6 - > 4 - > 12 }。
> 
> **输入:**
> 
> ```
>              5
>             / \
>            6   3
>           / \   \
>          4   9   2
> ```
> 
> **输出:** 5 - > 6 - > 4。

**方法:**使用[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)可以解决问题。这个想法是[遍历给定的二叉树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并找到根到叶路径中可能的偶数节点的最大数量。最后，遍历树并打印所有可能的根到叶路径，这些路径具有偶数节点的最大数量。按照以下步骤解决问题:

*   初始化两个变量，比如 **cntMaxEven** 和 **cntEven** 来存储从根到叶节点的偶数节点的最大计数和从根到叶节点的偶数节点的计数。
*   [遍历树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)检查以下情况:
    *   检查当前节点是否为叶节点，以及**是否为>节点。如果发现是真的，那么更新 **cntMaxEven = cntEven** 。**
    *   否则，检查当前节点是否为偶数节点。如果发现为真，则更新 **cntEven += 1** 。
*   最后，遍历树并打印偶数节点数等于 **cntMaxEven** 的所有可能的根到叶路径。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of the binary tree
struct Node {
    // Stores data
    int data;

    // Stores left child
    Node* left;

    // Stores right child
    Node* right;

    // Initialize a node
    // of binary tree
    Node(int val)
    {

        // Update data;
        data = val;
        left = right = NULL;
    }
};

// Function to find maximum count
// of even nodes in a path
int cntMaxEvenNodes(Node* root)
{

    // If the tree is an
    // empty binary tree.
    if (root == NULL) {
        return 0;
    }

    // Stores count of even nodes
    // in current subtree
    int cntEven = 0;

    // If root node is
    // an even node
    if (root->data % 2
        == 0) {

        // Update cntEven
        cntEven += 1;
    }

    // Stores count of even nodes
    // in left subtree.
    int X = cntMaxEvenNodes(
        root->left);

    // Stores count of even nodes
    // in right subtree.
    int Y = cntMaxEvenNodes(
        root->right);

    // cntEven
    cntEven += max(X, Y);

    return cntEven;
}

// Function to print paths having
// count of even nodes equal
// to maximum count of even nodes
void printPath(Node* root, int cntEven,
               int cntMaxEven,
               vector<int>& path)
{
    // If the tree is an
    // empty Binary Tree
    if (root == NULL) {
        return;
    }

    // If current node value is even
    if (root->data % 2 == 0) {
        path.push_back(
            root->data);
        cntEven += 1;
    }

    // If current node is
    // a leaf node
    if (root->left == NULL
        && root->right == NULL) {

        // If count of even nodes in
        // path is equal to cntMaxEven
        if (cntEven == cntMaxEven) {

            // Stores length of path
            int N = path.size();

            // Print path
            for (int i = 0; i < N - 1;
                 i++) {
                cout << path[i] << " -> ";
            }
            cout << path[N - 1] << endl;
        }
    }

    // Left subtree
    printPath(root->left, cntEven,
              cntMaxEven, path);

    // Right subtree
    printPath(root->right, cntEven,
              cntMaxEven, path);

    // If current node is even
    if (root->data % 2 == 0) {
        path.pop_back();

        // Update cntEven
        cntEven--;
    }
}

// Utility Function to print path
// from root to leaf node having
// maximum count of even nodes
void printMaxPath(Node* root)
{
    // Stores maximum count of even
    // nodes of a path in the tree
    int cntMaxEven;

    cntMaxEven
        = cntMaxEvenNodes(root);

    // Stores path of tree having
    // even nodes
    vector<int> path;

    printPath(root, 0, cntMaxEven,
              path);
}

// Driver code
int main()
{
    // Create tree.
    Node* root = NULL;
    root = new Node(2);
    root->left = new Node(6);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(7);
    root->right->right = new Node(11);
    root->left->left->left = new Node(10);
    root->left->left->right = new Node(12);
    root->left->right->right = new Node(1);

    printMaxPath(root);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of the binary tree
static class Node
{

    // Stores data
    int data;

    // Stores left child
    Node left;

    // Stores right child
    Node right;

    // Initialize a node
    // of binary tree
    Node(int val)
    {

        // Update data;
        data = val;
        left = right = null;
    }
};

// Function to find maximum count
// of even nodes in a path
static int cntMaxEvenNodes(Node root)
{

    // If the tree is an
    // empty binary tree.
    if (root == null)
    {
        return 0;
    }

    // Stores count of even nodes
    // in current subtree
    int cntEven = 0;

    // If root node is
    // an even node
    if (root.data % 2 == 0)
    {

        // Update cntEven
        cntEven += 1;
    }

    // Stores count of even nodes
    // in left subtree.
    int X = cntMaxEvenNodes(root.left);

    // Stores count of even nodes
    // in right subtree.
    int Y = cntMaxEvenNodes(root.right);

    // cntEven
    cntEven += Math.max(X, Y);

    return cntEven;
}

// Function to print paths having
// count of even nodes equal
// to maximum count of even nodes
static void printPath(Node root, int cntEven,
                      int cntMaxEven,
                      Vector<Integer> path)
{

    // If the tree is an
    // empty Binary Tree
    if (root == null)
    {
        return;
    }

    // If current node value is even
    if (root.data % 2 == 0)
    {
        path.add(root.data);
        cntEven += 1;
    }

    // If current node is
    // a leaf node
    if (root.left == null &&
       root.right == null)
    {

        // If count of even nodes in
        // path is equal to cntMaxEven
        if (cntEven == cntMaxEven)
        {

            // Stores length of path
            int N = path.size();

            // Print path
            for(int i = 0; i < N - 1; i++)
            {
                System.out.print(path.get(i) + " -> ");
            }
            System.out.print(path.get(N - 1) + "\n");
        }
    }

    // Left subtree
    printPath(root.left, cntEven,
              cntMaxEven, path);

    // Right subtree
    printPath(root.right, cntEven,
              cntMaxEven, path);

    // If current node is even
    if (root.data % 2 == 0)
    {
        path.remove(path.size() - 1);

        // Update cntEven
        cntEven--;
    }
}

// Utility Function to print path
// from root to leaf node having
// maximum count of even nodes
static void printMaxPath(Node root)
{

    // Stores maximum count of even
    // nodes of a path in the tree
    int cntMaxEven;

    cntMaxEven = cntMaxEvenNodes(root);

    // Stores path of tree having
    // even nodes
    Vector<Integer> path = new Vector<>();

    printPath(root, 0, cntMaxEven,
              path);
}

// Driver code
public static void main(String[] args)
{

    // Create tree.
    Node root = null;
    root = new Node(2);
    root.left = new Node(6);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(7);
    root.right.right = new Node(11);
    root.left.left.left = new Node(10);
    root.left.left.right = new Node(12);
    root.left.right.right = new Node(1);

    printMaxPath(root);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of the binary tree
class newNode:

    def __init__(self, val):

        self.data = val
        self.left = None
        self.right = None

path = []

# Function to find maximum count
# of even nodes in a path
def cntMaxEvenNodes(root):

    # If the tree is an
    # empty binary tree.
    if (root == None):
        return 0

    # Stores count of even nodes
    # in current subtree
    cntEven = 0

    # If root node is
    # an even node
    if (root.data % 2 == 0):

        # Update cntEven
        cntEven += 1

    # Stores count of even nodes
    # in left subtree.
    X = cntMaxEvenNodes(root.left)

    # Stores count of even nodes
    # in right subtree.
    Y = cntMaxEvenNodes(root.right)

    # cntEven
    cntEven += max(X, Y)

    return cntEven

# Function to print paths having
# count of even nodes equal
# to maximum count of even nodes
def printPath(root, cntEven, cntMaxEven):

    global path

    # If the tree is an
    # empty Binary Tree
    if (root == None):
        return

    # If current node value is even
    if (root.data % 2 == 0):
        path.append(root.data)
        cntEven += 1

    # If current node is
    # a leaf node
    if (root.left == None and
       root.right == None):

        # If count of even nodes in
        # path is equal to cntMaxEven
        if (cntEven == cntMaxEven):

            # Stores length of path
            N = len(path)

            # Print path
            for i in range(N - 1):
                print(path[i], end = "->")

            print(path[N - 1])

    # Left subtree
    printPath(root.left, cntEven, cntMaxEven)

    # Right subtree
    printPath(root.right, cntEven, cntMaxEven)

    # If current node is even
    if (root.data % 2 == 0):
        path.remove(path[len(path) - 1])

        # Update cntEven
        cntEven -= 1

# Utility Function to print path
# from root to leaf node having
# maximum count of even nodes
def printMaxPath(root):

    global path

    # Stores maximum count of even
    # nodes of a path in the tree
    cntMaxEven = cntMaxEvenNodes(root)

    printPath(root, 0, cntMaxEven)

# Driver code
if __name__ == '__main__':

    # Create tree.
    root = None
    root = newNode(2)
    root.left = newNode(6)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(7)
    root.right.right = newNode(11)
    root.left.left.left = newNode(10)
    root.left.left.right = newNode(12)
    root.left.right.right = newNode(1)

    printMaxPath(root)

# This code is contributed by bgangwar59
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Structure of the binary tree
class Node
{   
  // Stores data
  public int data;

  // Stores left child
  public Node left;

  // Stores right child
  public Node right;

  // Initialize a node
  // of binary tree
  public Node(int val)
  {
    // Update data;
    data = val;
    left = right = null;
  }
};

// Function to find maximum count
// of even nodes in a path
static int cntMaxEvenNodes(Node root)
{   
  // If the tree is an
  // empty binary tree.
  if (root == null)
  {
    return 0;
  }

  // Stores count of even
  // nodes in current subtree
  int cntEven = 0;

  // If root node is
  // an even node
  if (root.data % 2 == 0)
  {
    // Update cntEven
    cntEven += 1;
  }

  // Stores count of even
  // nodes in left subtree.
  int X = cntMaxEvenNodes(root.left);

  // Stores count of even nodes
  // in right subtree.
  int Y = cntMaxEvenNodes(root.right);

  // cntEven
  cntEven += Math.Max(X, Y);

  return cntEven;
}

// Function to print paths having
// count of even nodes equal
// to maximum count of even nodes
static void printPath(Node root,
                      int cntEven,
                      int cntMaxEven,
                      List<int> path)
{   
  // If the tree is an
  // empty Binary Tree
  if (root == null)
  {
    return;
  }

  // If current node value
  // is even
  if (root.data % 2 == 0)
  {
    path.Add(root.data);
    cntEven += 1;
  }

  // If current node is
  // a leaf node
  if (root.left == null &&
      root.right == null)
  {
    // If count of even nodes in
    // path is equal to cntMaxEven
    if (cntEven == cntMaxEven)
    {
      // Stores length of path
      int N = path.Count;

      // Print path
      for(int i = 0;
              i < N - 1; i++)
      {
        Console.Write(path[i] +
                      " -> ");
      }
      Console.Write(path[N - 1] +
                    "\n");
    }
  }

  // Left subtree
  printPath(root.left, cntEven,
            cntMaxEven, path);

  // Right subtree
  printPath(root.right, cntEven,
            cntMaxEven, path);

  // If current node is even
  if (root.data % 2 == 0)
  {
    path.RemoveAt(path.Count - 1);

    // Update cntEven
    cntEven--;
  }
}

// Utility Function to print path
// from root to leaf node having
// maximum count of even nodes
static void printMaxPath(Node root)
{
  // Stores maximum count of even
  // nodes of a path in the tree
  int cntMaxEven;

  cntMaxEven = cntMaxEvenNodes(root);

  // Stores path of tree having
  // even nodes
  List<int> path = new List<int>();

  printPath(root, 0,
            cntMaxEven, path);
}

// Driver code
public static void Main(String[] args)
{
  // Create tree.
  Node root = null;
  root = new Node(2);
  root.left = new Node(6);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(7);
  root.right.right = new Node(11);
  root.left.left.left = new Node(10);
  root.left.left.right = new Node(12);
  root.left.right.right = new Node(1);

  printMaxPath(root);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Structure of the binary tree
class Node
{
    constructor(val)
    {
        this.left = null;
        this.right = null;
        this.data = val;
    }
}

// Function to find maximum count
// of even nodes in a path
function cntMaxEvenNodes(root)
{

    // If the tree is an
    // empty binary tree.
    if (root == null)
    {
        return 0;
    }

    // Stores count of even nodes
    // in current subtree
    let cntEven = 0;

    // If root node is
    // an even node
    if (root.data % 2 == 0)
    {

        // Update cntEven
        cntEven += 1;
    }

    // Stores count of even nodes
    // in left subtree.
    let X = cntMaxEvenNodes(root.left);

    // Stores count of even nodes
    // in right subtree.
    let Y = cntMaxEvenNodes(root.right);

    // cntEven
    cntEven += Math.max(X, Y);

    return cntEven;
}

// Function to print paths having
// count of even nodes equal
// to maximum count of even nodes
function printPath(root, cntEven,
                   cntMaxEven, path)
{

    // If the tree is an
    // empty Binary Tree
    if (root == null)
    {
        return;
    }

    // If current node value is even
    if (root.data % 2 == 0)
    {
        path.push(root.data);
        cntEven += 1;
    }

    // If current node is
    // a leaf node
    if (root.left == null &&
       root.right == null)
    {

        // If count of even nodes in
        // path is equal to cntMaxEven
        if (cntEven == cntMaxEven)
        {

            // Stores length of path
            let N = path.length;

            // Print path
            for(let i = 0; i < N - 1; i++)
            {
                document.write(path[i] + " -> ");
            }
            document.write(path[N - 1] + "</br>");
        }
    }

    // Left subtree
    printPath(root.left, cntEven,
              cntMaxEven, path);

    // Right subtree
    printPath(root.right, cntEven,
              cntMaxEven, path);

    // If current node is even
    if (root.data % 2 == 0)
    {
        path.pop();

        // Update cntEven
        cntEven--;
    }
}

// Utility Function to print path
// from root to leaf node having
// maximum count of even nodes
function printMaxPath(root)
{

    // Stores maximum count of even
    // nodes of a path in the tree
    let cntMaxEven;

    cntMaxEven = cntMaxEvenNodes(root);

    // Stores path of tree having
    // even nodes
    let path = [];

    printPath(root, 0, cntMaxEven, path);
}

// Driver code

// Create tree.
let root = null;
root = new Node(2);
root.left = new Node(6);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(7);
root.right.right = new Node(11);
root.left.left.left = new Node(10);
root.left.left.right = new Node(12);
root.left.right.right = new Node(1);

printMaxPath(root);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
2 -> 6 -> 4 -> 10
2 -> 6 -> 4 -> 12
```

**时间复杂度:** O(N)，其中 N 为二叉树中的节点数。
**辅助空间:** O(N)