# 求二叉树的中值数组

> 原文:[https://www . geesforgeks . org/find-中值数组换二叉树/](https://www.geeksforgeeks.org/find-the-median-array-for-binary-tree/)

**先决条件:** [树遍历(有序、前序和后序)](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)、[中值](https://www.geeksforgeeks.org/median/)
给定一棵具有整数节点的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是为树的前序、后序和有序遍历中的每个位置找到[中值](https://www.geeksforgeeks.org/median/)。

> 中值数组是借助于树的前序、后序和有序遍历形成的数组，这样
> **med[i] =中值(前序[i]、有序[i]、有序[i])**

**例:**

```
Input: Tree =
               1
             /   \
            2     3
          /  \
         4    5 
Output: {4, 2, 4, 3, 3}
Explanation:
Preorder traversal = {1 2 4 5 3}
Inorder traversal =  {4 2 5 1 3}
Postorder traversal = {4 5 2 3 1}
median[0] = median(1, 4, 4) = 4
median[1] = median(2, 2, 5) = 2
median[2] = median(4, 5, 2) = 4
median[3] = median(5, 1, 3) = 3
median[4] = median(3, 3, 1) = 3
Hence, Median array = {4 2 4 3 3}

Input: Tree = 
               25
             /    \
           20      30
         /    \   /   \
       18     22 24   32 
Output: 18 20 20 24 30 30 32
```

**进场:**

*   首先，找到给定二叉树的[前序、后序和有序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并将它们分别存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
*   现在，对于从 0 到 N 的每个位置，将每个遍历数组中该位置的值插入一个向量。矢量大小为 3N。
*   最后，[对这个向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序，这个位置的中位数由**第二元素**给出。在这个向量中，它有 3N 个元素。因此在排序之后，中间的元素，第二个元素，每 3 个元素给出一个中间值。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to Obtain the median
// array for the preorder, postorder
// and inorder traversal of a binary tree

#include <bits/stdc++.h>
using namespace std;

// A binary tree node has data,
// a pointer to the left child
// and a pointer to the right child
struct Node {
    int data;
    struct Node *left, *right;
    Node(int data)
    {
        this->data = data;
        left = right = NULL;
    }
};

// Postorder traversal
void Postorder(
    struct Node* node,
    vector<int>& postorder)
{
    if (node == NULL)
        return;

    // First recur on left subtree
    Postorder(node->left, postorder);

    // then recur on right subtree
    Postorder(node->right, postorder);

    // now deal with the node
    postorder.push_back(node->data);
}

// Inorder traversal
void Inorder(
    struct Node* node,
    vector<int>& inorder)
{
    if (node == NULL)
        return;

    // First recur on left child
    Inorder(node->left, inorder);

    // then print the data of node
    inorder.push_back(node->data);

    // now recur on right child
    Inorder(node->right, inorder);
}

// Preorder traversal
void Preorder(
    struct Node* node,
    vector<int>& preorder)
{
    if (node == NULL)
        return;

    // First print data of node
    preorder.push_back(node->data);

    // then recur on left subtree
    Preorder(node->left, preorder);

    // now recur on right subtree
    Preorder(node->right, preorder);
}

// Function to print the any array
void PrintArray(vector<int> median)
{
    for (int i = 0;
         i < median.size(); i++)
        cout << median[i] << " ";

    return;
}

// Function to create and print
// the Median array
void MedianArray(struct Node* node)
{
    // Vector to store
    // the median values
    vector<int> median;

    if (node == NULL)
        return;

    vector<int> preorder,
        postorder,
        inorder;

    // Traverse the tree
    Postorder(node, postorder);
    Inorder(node, inorder);
    Preorder(node, preorder);

    int n = preorder.size();
    for (int i = 0; i < n; i++) {

        // Temporary vector to sort
        // the three values
        vector<int> temp;

        // Insert the values at ith index
        // for each traversal into temp
        temp.push_back(postorder[i]);
        temp.push_back(inorder[i]);
        temp.push_back(preorder[i]);

        // Sort the temp vector to
        // find the median
        sort(temp.begin(), temp.end());

        // Insert the middle value in
        // temp into the median vector
        median.push_back(temp[1]);
    }

    PrintArray(median);
    return;
}

// Driver Code
int main()
{
    struct Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    MedianArray(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Obtain the median
// array for the preorder, postorder
// and inorder traversal of a binary tree
import java.io.*;
import java.util.*;

// A binary tree node has data,
// a pointer to the left child
// and a pointer to the right child
class Node
{
  int data;
  Node left,right;
  Node(int item)
  {
    data = item;
    left = right = null;
  }
}
class Tree {
  public static Vector<Integer> postorder = new Vector<Integer>();
  public static Vector<Integer> inorder = new Vector<Integer>();
  public static Vector<Integer> preorder = new Vector<Integer>();
  public static Node root;

  // Postorder traversal
  public static void Postorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First recur on left subtree
    Postorder(node.left);

    // then recur on right subtree
    Postorder(node.right);

    // now deal with the node
    postorder.add(node.data);
  }
  // Inorder traversal
  public static void Inorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First recur on left child
    Inorder(node.left);

    // then print the data of node
    inorder.add(node.data);

    // now recur on right child
    Inorder(node.right);      
  }

  // Preorder traversal
  public static void Preorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First print data of node
    preorder.add(node.data);

    // then recur on left subtree
    Preorder(node.left);

    // now recur on right subtree
    Preorder(node.right);
  }

  // Function to print the any array    
  public static void PrintArray(Vector<Integer> median)
  {
    for(int i = 0; i < median.size(); i++)
    {
      System.out.print(median.get(i) + " ");
    }
  }

  // Function to create and print
  // the Median array
  public static void MedianArray(Node node)
  {

    // Vector to store
    // the median values
    Vector<Integer> median = new Vector<Integer>();
    if(node == null)
    {
      return;
    }

    // Traverse the tree
    Postorder(node);
    Inorder(node);
    Preorder(node);
    int n = preorder.size();
    for(int i = 0; i < n; i++)
    {

      // Temporary vector to sort
      // the three values
      Vector<Integer> temp = new Vector<Integer>();

      // Insert the values at ith index
      // for each traversal into temp
      temp.add(postorder.get(i));
      temp.add(inorder.get(i));
      temp.add(preorder.get(i));

      // Sort the temp vector to
      // find the median
      Collections.sort(temp);

      // Insert the middle value in
      // temp into the median vector
      median.add(temp.get(1));
    }
    PrintArray(median);
  }

  // Driver Code
  public static void main (String[] args)
  {
    Tree.root = new Node(1);
    Tree.root.left = new Node(2);
    Tree.root.right = new Node(3);
    Tree.root.left.left = new Node(4);
    Tree.root.left.right = new Node(5);
    MedianArray(root);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to Obtain the median
# array for the preorder, postorder
# and inorder traversal of a binary tree

# A binary tree node has data,
# a pointer to the left child
# and a pointer to the right child
class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# Postorder traversal
def Postorder(node):
    global preorder
    if (node == None):
        return
    # First recur on left subtree
    Postorder(node.left)

    # then recur on right subtree
    Postorder(node.right)

    # now deal with the node
    postorder.append(node.data)

# Inorder traversal
def Inorder(node):
    global inorder
    if (node == None):
        return

    # First recur on left child
    Inorder(node.left)

    # then print the data of node
    inorder.append(node.data)

    # now recur on right child
    Inorder(node.right)

# Preorder traversal
def Preorder(node):
    global preorder

    if (node == None):
        return

    # First print data of node
    preorder.append(node.data)

    # then recur on left subtree
    Preorder(node.left)

    # now recur on right subtree
    Preorder(node.right)

# Function to print the any array
def PrintArray(median):
    for i in range(len(median)):
        print(median[i], end = " ")

    return

# Function to create and print
# the Median array
def MedianArray(node):
    global inorder, postorder, preorder

    # Vector to store
    # the median values
    median = []

    if (node == None):
        return

    # Traverse the tree
    Postorder(node)
    Inorder(node)
    Preorder(node)

    n = len(preorder)

    for i in range(n):

        # Temporary vector to sort
        # the three values
        temp = []

        # Insert the values at ith index
        # for each traversal into temp
        temp.append(postorder[i])
        temp.append(inorder[i])
        temp.append(preorder[i])

        # Sort the temp vector to
        # find the median
        temp = sorted(temp)

        # Insert the middle value in
        # temp into the median vector
        median.append(temp[1])

    PrintArray(median)

# Driver Code
if __name__ == '__main__':
    preorder, inorder, postorder = [], [], []
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    MedianArray(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to Obtain the median
// array for the preorder, postorder
// and inorder traversal of a binary tree
using System;
using System.Collections.Generic;
using System.Numerics;

// A binary tree node has data,
// a pointer to the left child
// and a pointer to the right child
public class Node
{
  public int data;
  public Node left,right;
  public Node(int item)
  {
    data = item;
    left = right = null;
  }
}
public class Tree{
  static List<int> postorder = new List<int>();
  static List<int> inorder = new List<int>();
  static List<int> preorder = new List<int>();

  static Node root;
  // Postorder traversal
  public static void Postorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First recur on left subtree
    Postorder(node.left);

    // then recur on right subtree
    Postorder(node.right);

    // now deal with the node
    postorder.Add(node.data);
  }
  // Inorder traversal
  public static void Inorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First recur on left child
    Inorder(node.left);

    // then print the data of node
    inorder.Add(node.data);

    // now recur on right child
    Inorder(node.right);      
  }
  // Preorder traversal
  public static void Preorder(Node node)
  {
    if(node == null)
    {
      return;
    }

    // First print data of node
    preorder.Add(node.data);

    // then recur on left subtree
    Preorder(node.left);

    // now recur on right subtree
    Preorder(node.right);
  }

  // Function to print the any array    
  public static void PrintArray(List<int> median)
  {
    for(int i = 0; i < median.Count; i++)
    {
      Console.Write(median[i] + " ");
    }
  }

  // Function to create and print
  // the Median array
  public static void MedianArray(Node node)
  {

    // Vector to store
    // the median values
    List<int> median = new List<int>();
    if(node == null)
    {
      return;
    }

    // Traverse the tree
    Postorder(node);
    Inorder(node);
    Preorder(node);
    int n = preorder.Count;
    for(int i = 0; i < n; i++)
    {

      // Temporary vector to sort
      // the three values
      List<int> temp = new List<int>();

      // Insert the values at ith index
      // for each traversal into temp
      temp.Add(postorder[i]);
      temp.Add(inorder[i]);
      temp.Add(preorder[i]);

      // Sort the temp vector to
      // find the median
      temp.Sort();

      // Insert the middle value in
      // temp into the median vector
      median.Add(temp[1]);
    }
    PrintArray(median);
  }

  // Driver code
  static public void Main ()
  {
    Tree.root = new Node(1);
    Tree.root.left = new Node(2);
    Tree.root.right = new Node(3);
    Tree.root.left.left = new Node(4);
    Tree.root.left.right = new Node(5);
    MedianArray(root);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// JavaScript program to Obtain the median
// array for the preorder, postorder
// and inorder traversal of a binary tree

// A binary tree node has data,
// a pointer to the left child
// and a pointer to the right child
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = null;
    }
}

let postorder = [];
let inorder = [];
let preorder = [];

// Postorder traversal
function Postorder(node)
{
    if(node == null)
    {
      return;
    }

    // First recur on left subtree
    Postorder(node.left);

    // then recur on right subtree
    Postorder(node.right);

    // now deal with the node
    postorder.push(node.data);
}

// Inorder traversal
function Inorder(node)
{
    if(node == null)
    {
      return;
    }

    // First recur on left child
    Inorder(node.left);

    // then print the data of node
    inorder.push(node.data);

    // now recur on right child
    Inorder(node.right);  
}

// Preorder traversal
function Preorder(node)
{
    if(node == null)
    {
      return;
    }

    // First print data of node
    preorder.push(node.data);

    // then recur on left subtree
    Preorder(node.left);

    // now recur on right subtree
    Preorder(node.right);
}
// Function to print the any array
function PrintArray(median)
{
    for(let i = 0; i < median.length; i++)
    {
      document.write(median[i] + " ");
    }
}

// Function to create and print
  // the Median array
function MedianArray(node)
{
    // Vector to store
    // the median values
    let median = [];
    if(node == null)
    {
      return;
    }

    // Traverse the tree
    Postorder(node);
    Inorder(node);
    Preorder(node);
    let n = preorder.length;
    for(let i = 0; i < n; i++)
    {

      // Temporary vector to sort
      // the three values
      let temp = [];

      // Insert the values at ith index
      // for each traversal into temp
      temp.push(postorder[i]);
      temp.push(inorder[i]);
      temp.push(preorder[i]);

      // Sort the temp vector to
      // find the median
      temp.sort(function(a,b){return a-b;});

      // Insert the middle value in
      // temp into the median vector
      median.push(temp[1]);
    }
    PrintArray(median);
}

 // Driver Code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
MedianArray(root);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4 2 4 3 3
```

***时间复杂度:**O(N)*T4】