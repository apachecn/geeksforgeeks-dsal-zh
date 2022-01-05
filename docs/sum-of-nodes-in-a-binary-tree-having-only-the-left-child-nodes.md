# 只有左边子节点的二叉树中节点的总和

> 原文:[https://www . geeksforgeeks . org/二进制树中只有左边子节点的节点总数/](https://www.geeksforgeeks.org/sum-of-nodes-in-a-binary-tree-having-only-the-left-child-nodes/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到只有左边子节点的二叉树节点的[和。](https://www.geeksforgeeks.org/sum-nodes-binary-tree/)

**示例:**

> **输入:**8
> /\
> 3 7
> /\/
> 5 6 0
> /
> 1 2
> **输出:** 18
> **说明:**值为 5、6、7 的节点只有剩下的子节点
> 
> **输入:**2
> /\
> 3 1
> /
> 5 6
> T7】输出: 4

**方法:**给定的问题可以通过[使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历二叉树来解决。其思想是检查一个节点是否只包含一个左子节点，如果条件为真，则将当前节点的值添加到答案中。可以遵循以下步骤来解决问题:

*   使用后置遍历遍历二叉树
    *   如果**根**为空，则返回 0
    *   在左边的子树上使用[递归](https://www.geeksforgeeks.org/recursion/)，并将其答案存储在左边的变量**中**
    *   在右子树上使用[递归](https://www.geeksforgeeks.org/recursion/)，并将其答案存储在变量**右**中
    *   如果**根.左！= null & & root.right == null，**然后返回 **root.val + left + right** 的值
    *   否则返回**左+右**

以下是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

struct Node
{

    int val;
    Node *left;
    Node *right;
    Node(int value)
    {
        val = value;
        left = NULL;
        right = NULL;
    }
};

// Function to find the sum of nodes
// having only left child node
int sumLeftChild(Node *root)
{
    if (root == NULL)
        return 0;

    // Sum of nodes having only left
    // child node from left subtree
    int left = sumLeftChild(root->left);

    // Sum of nodes having only left
    // child node from right subtree
    int right = sumLeftChild(root->right);

    // If current node has only left
    // child node return the sum from
    // left subtree + right
    // subtree + root->val
    if (root->left != NULL && root->right == NULL)
    {

        return root->val + left + right;
    }

    // Return the value from left
    // and right subtrees
    return left + right;
}

// Driver code
int main()
{

    // Initialize the tree
    Node *root = new Node(2);
    root->left = new Node(3);
    root->right = new Node(4);
    root->left->left = new Node(5);
    root->right->left = new Node(7);
    cout << (sumLeftChild(root));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the sum of nodes
    // having only left child node
    public static int sumLeftChild(Node root)
    {
        if (root == null)
            return 0;

        // Sum of nodes having only left
        // child node from left subtree
        int left = sumLeftChild(root.left);

        // Sum of nodes having only left
        // child node from right subtree
        int right = sumLeftChild(root.right);

        // If current node has only left
        // child node return the sum from
        // left subtree + right
        // subtree + root.val
        if (root.left != null && root.right == null) {

            return root.val + left + right;
        }

        // Return the value from left
        // and right subtrees
        return left + right;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the tree
        Node root = new Node(2);
        root.left = new Node(3);
        root.right = new Node(4);
        root.left.left = new Node(5);
        root.right.left = new Node(7);
        System.out.println(sumLeftChild(root));
    }

    static class Node {

        int val;
        Node left, right;
        public Node(int val)
        {
            this.val = val;
        }
    }
}
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

// Function to find the sum of nodes
// having only left child node
function sumLeftChild(root) {
  if (root == null)
    return 0;

  // Sum of nodes having only left
  // child node from left subtree
  let left = sumLeftChild(root.left);

  // Sum of nodes having only left
  // child node from right subtree
  let right = sumLeftChild(root.right);

  // If current node has only left
  // child node return the sum from
  // left subtree + right
  // subtree + root.val
  if (root.left != null && root.right == null) {

    return root.val + left + right;
  }

  // Return the value from left
  // and right subtrees
  return left + right;
}

// Driver code

// Initialize the tree
let root = new Node(2);
root.left = new Node(3);
root.right = new Node(4);
root.left.left = new Node(5);
root.right.left = new Node(7);
document.write(sumLeftChild(root));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
7
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)