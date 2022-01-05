# 检查给定的通用 N 元树是否水平对称

> 原文:[https://www . geesforgeks . org/check-if-given-generic-n-ary-tree-is-symmetric-horizontal/](https://www.geeksforgeeks.org/check-if-given-generic-n-ary-tree-is-symmetric-horizontally/)

给定一个 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/) **根，**任务是检查它是否水平对称(自身的镜像)。

**示例:**

> **输入:**根=**7
> /\ \
> 4 2 2 4
> /|/| | \ | \
> 3 2 6 7 6 2 3
> **输出:**真
> **解释:**树的左侧是右侧的镜像**
> 
> ****输入:**根=**2
> /| \
> 3 4 3
> /| \
> 5 6 5
> **输出:**真****

******方法:**给定的问题可以通过使用[前序遍历](http://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)来解决。其思想是将两个根节点作为参数传递，检查当前节点的值是否相同，并使用递归检查左节点的子节点的值是否与右节点的子节点的值相同。****

****可以遵循以下步骤来解决问题:****

*   ****在 N 元树上应用[预序遍历](https://www.geeksforgeeks.org/post-order-traversal-of-binary-tree-in-on-using-o1-space/):****
*   ****检查两个根节点的值是否相同。****
*   ****另外，检查两个根的节点数是否相同****
*   ****从左到右迭代左根的子节点，同时从右到左迭代右节点的节点，并使用递归。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

class Node
{
public:
    vector<Node *> children;
    int val;

    // constructor
    Node(int v)
    {

        val = v;
        children = {};
    }
};

// Preorder traversal to check
// if the generic tree
// is symmetric or not
bool preorder(
    Node *root1, Node *root2)
{

    // If the values of both the
    // root is not the same or if
    // the number of children are
    // not the same then return false
    if (root1->val != root2->val || root1->children.size() != root2->children.size())
        return false;

    // Number of children
    int size = root1->children.size();

    // Iterate left to right on
    // left root and right to left
    // on the right root
    for (int i = 0; i < size; i++)
    {

        // If any one branch is not
        // symmetric then return false
        if (!preorder(
                root1->children[i],
                root2->children[size - 1 - i]))
            return false;
    }

    // Tree is symmetric return true
    return true;
}

// Function to check if the generic
// tree is symmetric or not
bool isSymmetric(Node *root)
{

    // Base case
    if (root == NULL)
        return true;

    // Apply preorder traversal
    // on the tree
    return preorder(root, root);
}

// Driver code
int main()
{

    // Initialize the tree
    Node *seven = new Node(7);
    Node *five1 = new Node(5);
    Node *five2 = new Node(5);
    Node *four = new Node(4);
    seven->children.push_back(five1);
    seven->children.push_back(four);
    seven->children.push_back(five2);

    // Call the function
    // and print the result
    if (isSymmetric(seven))
    {
        cout << "true" << endl;
    }
    else
    {
        cout << "false" << endl;
    }
    return 0;
}

// This code is contributed by Potta Lokesh**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to check if the generic
    // tree is symmetric or not
    public static boolean isSymmetric(Node root)
    {

        // Base case
        if (root == null)
            return true;

        // Apply preorder traversal
        // on the tree
        return preorder(root, root);
    }

    // Preorder traversal to check
    // if the generic tree
    // is symmetric or not
    public static boolean preorder(
        Node root1, Node root2)
    {

        // If the values of both the
        // root is not the same or if
        // the number of children are
        // not the same then return false
        if (root1.val != root2.val
            || root1.children.size()
                   != root2.children.size())
            return false;

        // Number of children
        int size = root1.children.size();

        // Iterate left to right on
        // left root and right to left
        // on the right root
        for (int i = 0; i < size; i++) {

            // If any one branch is not
            // symmetric then return false
            if (!preorder(
                    root1.children.get(i),
                    root2.children.get(size - 1 - i)))
                return false;
        }

        // Tree is symmetric return true
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the tree
        Node seven = new Node(7);
        Node five1 = new Node(5);
        Node five2 = new Node(5);
        Node four = new Node(4);
        seven.children.add(five1);
        seven.children.add(four);
        seven.children.add(five2);

        // Call the function
        // and print the result
        System.out.println(
            isSymmetric(seven));
    }

    static class Node {

        List<Node> children;
        int val;

        // constructor
        public Node(int val)
        {

            this.val = val;
            children = new ArrayList<>();
        }
    }
}**
```

## ****C#****

```
**// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Function to check if the generic
  // tree is symmetric or not
  static bool isSymmetric(Node root)
  {

    // Base case
    if (root == null)
      return true;

    // Apply preorder traversal
    // on the tree
    return preorder(root, root);
  }

  // Preorder traversal to check
  // if the generic tree
  // is symmetric or not
  static bool preorder(
    Node root1, Node root2)
  {

    // If the values of both the
    // root is not the same or if
    // the number of children are
    // not the same then return false
    if (root1.val != root2.val
        || root1.children.Count
        != root2.children.Count)
      return false;

    // Number of children
    int size = root1.children.Count;

    // Iterate left to right on
    // left root and right to left
    // on the right root
    for (int i = 0; i < size; i++) {

      // If any one branch is not
      // symmetric then return false
      if (!preorder(
        root1.children[i],
        root2.children[size - 1 - i]))
        return false;
    }

    // Tree is symmetric return true
    return true;
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Initialize the tree
    Node seven = new Node(7);
    Node five1 = new Node(5);
    Node five2 = new Node(5);
    Node four = new Node(4);
    seven.children.Add(five1);
    seven.children.Add(four);
    seven.children.Add(five2);

    // Call the function
    // and print the result
    Console.WriteLine(
      isSymmetric(seven));
  }

  class Node {

    public List<Node> children;
    public int val;

    // constructor
    public Node(int val)
    {

      this.val = val;
      children = new List<Node>();
    }
  }
}

// This code is contributed by shikhasingrajput**
```

## ****java 描述语言****

```
**<script>
// Javascript code for the above approach

class Node {
  // constructor
  constructor(v) {
    this.val = v;
    this.children = [];
  }
};

// Preorder traversal to check
// if the generic tree
// is symmetric or not
function preorder(root1, root2) {

  // If the values of both the
  // root is not the same or if
  // the number of children are
  // not the same then return false
  if (root1.val != root2.val || root1.children.length != root2.children.length)
    return false;

  // Number of children
  let size = root1.children.length;

  // Iterate left to right on
  // left root and right to left
  // on the right root
  for (let i = 0; i < size; i++) {

    // If any one branch is not
    // symmetric then return false
    if (!preorder(
      root1.children[i],
      root2.children[size - 1 - i]))
      return false;
  }

  // Tree is symmetric return true
  return true;
}

// Function to check if the generic
// tree is symmetric or not
function isSymmetric(root) {

  // Base case
  if (root == null)
    return true;

  // Apply preorder traversal
  // on the tree
  return preorder(root, root);
}

// Driver code

// Initialize the tree
let seven = new Node(7);
let five1 = new Node(5);
let five2 = new Node(5);
let four = new Node(4);
seven.children.push(five1);
seven.children.push(four);
seven.children.push(five2);

// Call the function
// and print the result
if (isSymmetric(seven)) {
  document.write("true");
}
else {
  document.write("false");
}

// This code is contributed by gfgking.
 </script>**
```

******Output**

```
true
```**** 

******时间复杂度:** O(N)，其中 N 为树的节点数
T3】辅助空间: O(H)，其中 H 为树的高度****