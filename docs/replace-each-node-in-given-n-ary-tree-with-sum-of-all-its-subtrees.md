# 用其所有子树的和替换给定 N 元树中的每个节点

> 原文:[https://www . geesforgeks . org/用其所有子树的和替换给定 n 元树中的每个节点/](https://www.geeksforgeeks.org/replace-each-node-in-given-n-ary-tree-with-sum-of-all-its-subtrees/)

给定一棵[T1【N】T2 树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)。任务是用所有**子树**和**节点本身**的总和替换每个节点的值。

**示例**

> **输入:**1
> /| \
> 2 3 4
> /\ \
> 5 67
> **输出:**初始预序遍历:1 2 5 6 7 3 4
> 最终预序遍历:28 20 5 6 7 3 4
> **解释:**每个节点的值被其所有子树和节点本身的和所代替。
> 
> **输入:**1
> /| \
> 4 2 3
> /\ \
> 7 6 5
> **输出:**初始预序遍历:1 4 7 6 3 5
> 最终预序遍历:23 13 7 6 28 5

**方法:**这个问题可以用[递归](http://www.geeksforgeeks.org/recursion/)解决。按照以下步骤解决给定的问题。

*   做这道题最简单的方法就是使用**递归**。
*   当**当前节点等于空**时，从基本条件开始，然后**返回 0** ，因为这意味着它是叶节点。
*   否则，通过使用循环遍历对其所有子节点进行递归调用，并将其中所有子节点的总和相加。
*   最后返回当前节点的数据。
*   这样，所有节点的值都将被所有子树和自身的总和所替换。

下面是上述方法的实现。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Class for the node of the tree
struct Node {
    int data;

    // List of children
    struct Node** children;

    int length;

    Node()
    {
        length = 0;
        data = 0;
    }

    Node(int n, int data_)
    {
        children = new Node*();
        length = n;
        data = data_;
    }
};

// Function to replace node with
// sum of its left subtree, right
// subtree and its sum
int sumReplacementNary(Node* node)
{
    if (node == NULL)
        return 0;

    // Total children count
    int total = node->length;

    // Taking sum of all the nodes
    for (int i = 0; i < total; i++)
        node->data += sumReplacementNary(node->children[i]);

    return node->data;
}

void preorderTraversal(Node* node)
{
    if (node == NULL)
        return;

    // Total children count
    int total = node->length;

    // Print the current node's data
    cout << node->data << " ";

    // All the children except the last
    for (int i = 0; i < total - 1; i++)
        preorderTraversal(node->children[i]);

    // Last child
    preorderTraversal(node->children[total - 1]);
}

// Driver code
int main()
{

    /* Create the following tree
                    1
              / | \
             2  3  4
       / \ \
      5  6  7
    */
    int N = 3;
    Node* root = new Node(N, 1);
    root->children[0] = new Node(N, 2);
    root->children[1] = new Node(N, 3);
    root->children[2] = new Node(N, 4);
    root->children[0]->children[0] = new Node(N, 5);
    root->children[0]->children[1] = new Node(N, 6);
    root->children[0]->children[2] = new Node(N, 7);

    cout << "Initial Pre-order Traversal: ";
    preorderTraversal(root);
    cout << endl;

    cout << "Final Pre-order Traversal: ";
    sumReplacementNary(root);
    preorderTraversal(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

  // Class for the node of the tree
  static class Node {
    int data;

    // List of children
    Node []children;

    int length;

    Node()
    {
      length = 0;
      data = 0;
    }

    Node(int n, int data_)
    {
      children = new Node[n];
      length = n;
      data = data_;
    }
  };

  // Function to replace node with
  // sum of its left subtree, right
  // subtree and its sum
  static int sumReplacementNary(Node node)
  {
    if (node == null)
      return 0;

    // Total children count
    int total = node.length;

    // Taking sum of all the nodes
    for (int i = 0; i < total; i++)
      node.data += sumReplacementNary(node.children[i]);

    return node.data;
  }

  static void preorderTraversal(Node node)
  {
    if (node == null)
      return;

    // Total children count
    int total = node.length;

    // Print the current node's data
    System.out.print(node.data+ " ");

    // All the children except the last
    for (int i = 0; i < total - 1; i++)
      preorderTraversal(node.children[i]);

    // Last child
    preorderTraversal(node.children[total - 1]);
  }

  // Driver code
  public static void main(String[] args)
  {

    /* Create the following tree
                    1
              / | \
             2  3  4
       / \ \
      5  6  7
    */
    int N = 3;
    Node root = new Node(N, 1);
    root.children[0] = new Node(N, 2);
    root.children[1] = new Node(N, 3);
    root.children[2] = new Node(N, 4);
    root.children[0].children[0] = new Node(N, 5);
    root.children[0].children[1] = new Node(N, 6);
    root.children[0].children[2] = new Node(N, 7);

    System.out.print("Initial Pre-order Traversal: ");
    preorderTraversal(root);
    System.out.println();

    System.out.print("Final Pre-order Traversal: ");
    sumReplacementNary(root);
    preorderTraversal(root);
  }
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;
public class GFG{

  // Class for the node of the tree
  class Node {
    public int data;

    // List of children
    public Node []children;
    public int length;

    public Node()
    {
      length = 0;
      data = 0;
    }

    public Node(int n, int data_)
    {
      children = new Node[n];
      length = n;
      data = data_;
    }
  };

  // Function to replace node with
  // sum of its left subtree, right
  // subtree and its sum
  static int sumReplacementNary(Node node)
  {
    if (node == null)
      return 0;

    // Total children count
    int total = node.length;

    // Taking sum of all the nodes
    for (int i = 0; i < total; i++)
      node.data += sumReplacementNary(node.children[i]);

    return node.data;
  }

  static void preorderTraversal(Node node)
  {
    if (node == null)
      return;

    // Total children count
    int total = node.length;

    // Print the current node's data
    Console.Write(node.data+ " ");

    // All the children except the last
    for (int i = 0; i < total - 1; i++)
      preorderTraversal(node.children[i]);

    // Last child
    preorderTraversal(node.children[total - 1]);
  }

  // Driver code
  public static void Main(String[] args)
  {

    /* Create the following tree
                    1
              / | \
             2  3  4
       / \ \
      5  6  7
    */
    int N = 3;
    Node root = new Node(N, 1);
    root.children[0] = new Node(N, 2);
    root.children[1] = new Node(N, 3);
    root.children[2] = new Node(N, 4);
    root.children[0].children[0] = new Node(N, 5);
    root.children[0].children[1] = new Node(N, 6);
    root.children[0].children[2] = new Node(N, 7);

    Console.Write("Initial Pre-order Traversal: ");
    preorderTraversal(root);
    Console.WriteLine();

    Console.Write("Final Pre-order Traversal: ");
    sumReplacementNary(root);
    preorderTraversal(root);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // Class for the node of the tree
   class Node {

     // List of children
     constructor(n = 0, data_ = 0) {
       this.children = new Array(10000);
       this.length = n;
       this.data = data_;
     }
   }

   // Function to replace node with
   // sum of its left subtree, right
   // subtree and its sum
   function sumReplacementNary(node) {
     if (node == null)
       return 0;

     // Total children count
     let total = node.length;

     // Taking sum of all the nodes
     for (let i = 0; i < total; i++)
       node.data += sumReplacementNary(node.children[i]);

     return node.data;
   }

   function preorderTraversal(node) {
     if (node == null)
       return;

     // Total children count
     let total = node.length;

     // Print the current node's data
     document.write(node.data + " ");

     // All the children except the last
     for (let i = 0; i < total - 1; i++)
       preorderTraversal(node.children[i]);

     // Last child
     preorderTraversal(node.children[total - 1]);
   }

   // Driver code

   /* Create the following tree
                   1
             / | \
            2  3  4
      / \ \
     5  6  7
   */
   let N = 3;
   let root = new Node(N, 1);
   root.children[0] = new Node(N, 2);
   root.children[1] = new Node(N, 3);
   root.children[2] = new Node(N, 4);
   root.children[0].children[0] = new Node(N, 5);
   root.children[0].children[1] = new Node(N, 6);
   root.children[0].children[2] = new Node(N, 7);

   document.write("Initial Pre-order Traversal: ");
   preorderTraversal(root);
   document.write('<br>')

   document.write("Final Pre-order Traversal: ");
   sumReplacementNary(root);
   preorderTraversal(root);

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
Initial Pre-order Travedsal: 1 2 5 6 7 3 4 
Final Pre-order Traversal: 28 20 5 6 7 3 4 
```

**时间复杂度:** O(N)，其中 N 为树中节点数。