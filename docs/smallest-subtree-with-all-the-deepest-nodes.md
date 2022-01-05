# 包含所有最深节点的最小子树

> 原文:[https://www . geeksforgeeks . org/最小-子树-所有-最深-节点/](https://www.geeksforgeeks.org/smallest-subtree-with-all-the-deepest-nodes/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到包含给定二叉树所有最深节点的**最小子树**，并返回该子树的根。
***注意:**每个节点的深度定义为从根到给定节点的路径长度。*

**例:**

> ***输入:***
> 
> ```
>             1
>           /   \
>          2     3
>        /  \   /  \
>       4    5  6   7
>                  /  \
>                 8    9
> ```
> 
> **输出** : 7
> 
> ***输入:***
> 
> ```
>                1
>              /   \
>             2     3
> ```
> 
> **输出:** 1

**方法:**按照以下步骤解决问题:

*   使用[离散傅立叶变换](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)递归遍历[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)。
*   对于每个节点，找出其左右子树的深度。
*   **如果左子树的深度>右子树的深度:**遍历左子树。
*   **如果右子树的深度>左子树的深度:**遍历右子树。
*   否则，返回当前节点。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
struct TreeNode {

    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int data)
    {
        this->val = data;
        left = NULL;
        right = NULL;
    }
};

// Function to return depth of
// the Tree from root
int find_ht(TreeNode* root)
{
    if (!root)
        return 0;

    // If current node is a leaf node
    if (root->left == NULL
        && root->right == NULL)
        return 1;

    return max(find_ht(root->left),
               find_ht(root->right))
           + 1;
}

// Function to find the root of the smallest
// subtree consisting of all deepest nodes
void find_node(TreeNode* root, TreeNode*& req_node)
{
    if (!root)
        return;

    // Stores height of left subtree
    int left_ht = find_ht(root->left);

    // Stores height of right subtree
    int right_ht = find_ht(root->right);

    // If height of left subtree exceeds
    // that of the right subtree
    if (left_ht > right_ht) {

        // Traverse left subtree
        find_node(root->left, req_node);
    }

    // If height of right subtree exceeds
    // that of the left subtree
    else if (right_ht > left_ht) {
        find_node(root->right, req_node);
    }

    // Otherwise
    else {

        // Return current node
        req_node = root;
        return;
    }
}

// Driver Code
int main()
{
    struct TreeNode* root
        = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);

    TreeNode* req_node = NULL;

    find_node(root, req_node);

    cout << req_node->val;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Structure of a Node
static class TreeNode
{
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int data)
    {
        this.val = data;
        left = null;
        right = null;
    }
};

// Function to return depth of
// the Tree from root
static int find_ht(TreeNode root)
{
    if (root == null)
        return 0;

    // If current node is a leaf node
    if (root.left == null
        && root.right == null)
        return 1;
    return Math.max(find_ht(root.left),
               find_ht(root.right))
           + 1;
}

// Function to find the root of the smallest
// subtree consisting of all deepest nodes
static TreeNode find_node(TreeNode root, TreeNode req_node)
{
    if (root == null)
        return req_node;

    // Stores height of left subtree
    int left_ht = find_ht(root.left);

    // Stores height of right subtree
    int right_ht = find_ht(root.right);

    // If height of left subtree exceeds
    // that of the right subtree
    if (left_ht > right_ht)
    {

        // Traverse left subtree
        req_node = find_node(root.left, req_node);
    }

    // If height of right subtree exceeds
    // that of the left subtree
    else if (right_ht > left_ht)
    {
        req_node = find_node(root.right, req_node);
    }

    // Otherwise
    else
    {

        // Return current node
        req_node = root;
        return req_node;
    }
    return req_node;
}

// Driver Code
public static void main(String[] args)
{
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    TreeNode req_node = null;
    req_node = find_node(root, req_node);
    System.out.print(req_node.val);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of a Node
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

# Function to return depth of
# the Tree from root
def find_ht(root):
    if (not root):
        return 0

    # If current node is a leaf node
    if (root.left == None and root.right == None):
        return 1

    return max(find_ht(root.left), find_ht(root.right)) + 1

# Function to find the root of the smallest
# subtree consisting of all deepest nodes
def find_node(root):
    global req_node

    if (not root):
        return

    # Stores height of left subtree
    left_ht = find_ht(root.left)

    # Stores height of right subtree
    right_ht = find_ht(root.right)

    # If height of left subtree exceeds
    # that of the right subtree
    if (left_ht > right_ht):

        # Traverse left subtree
        find_node(root.left)

    # If height of right subtree exceeds
    # that of the left subtree
    elif (right_ht > left_ht):
        find_node(root.right)

    # Otherwise
    else:

        # Return current node
        req_node = root
        return

# Driver Code
if __name__ == '__main__':

    root = TreeNode(1)
    root.left = TreeNode(2)
    root.right = TreeNode(3)
    req_node = None
    find_node(root)
    print(req_node.val)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Structure of a Node
public class TreeNode
{
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int data)
    {
        this.val = data;
        left = null;
        right = null;
    }
};

// Function to return depth of
// the Tree from root
static int find_ht(TreeNode root)
{
    if (root == null)
        return 0;

    // If current node is a leaf node
    if (root.left == null
        && root.right == null)
        return 1;
    return Math.Max(find_ht(root.left),
               find_ht(root.right))
           + 1;
}

// Function to find the root of the smallest
// subtree consisting of all deepest nodes
static TreeNode find_node(TreeNode root, TreeNode req_node)
{
    if (root == null)
        return req_node;

    // Stores height of left subtree
    int left_ht = find_ht(root.left);

    // Stores height of right subtree
    int right_ht = find_ht(root.right);

    // If height of left subtree exceeds
    // that of the right subtree
    if (left_ht > right_ht)
    {

        // Traverse left subtree
        req_node = find_node(root.left, req_node);
    }

    // If height of right subtree exceeds
    // that of the left subtree
    else if (right_ht > left_ht)
    {
        req_node = find_node(root.right, req_node);
    }

    // Otherwise
    else
    {

        // Return current node
        req_node = root;
        return req_node;
    }
    return req_node;
}

// Driver Code
public static void Main(String[] args)
{
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    TreeNode req_node = null;
    req_node = find_node(root, req_node);
    Console.Write(req_node.val);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

  // JavaScript program for above approach

  // Structure of a Node
  class TreeNode
  {
      constructor(data) {
         this.left = null;
         this.right = null;
         this.val = data;
      }
  }

  // Function to return depth of
  // the Tree from root
  function find_ht(root)
  {
      if (root == null)
          return 0;

      // If current node is a leaf node
      if (root.left == null
          && root.right == null)
          return 1;
      return Math.max(find_ht(root.left),
                 find_ht(root.right))
             + 1;
  }

  // Function to find the root of the smallest
  // subtree consisting of all deepest nodes
  function find_node(root, req_node)
  {
      if (root == null)
          return req_node;

      // Stores height of left subtree
      let left_ht = find_ht(root.left);

      // Stores height of right subtree
      let right_ht = find_ht(root.right);

      // If height of left subtree exceeds
      // that of the right subtree
      if (left_ht > right_ht)
      {

          // Traverse left subtree
          req_node = find_node(root.left, req_node);
      }

      // If height of right subtree exceeds
      // that of the left subtree
      else if (right_ht > left_ht)
      {
          req_node = find_node(root.right, req_node);
      }

      // Otherwise
      else
      {

          // Return current node
          req_node = root;
          return req_node;
      }
      return req_node;
  }

  let root = new TreeNode(1);
  root.left = new TreeNode(2);
  root.right = new TreeNode(3);
  let req_node = null;
  req_node = find_node(root, req_node);
  document.write(req_node.val);

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(NlogN)*
*最坏情况的复杂度出现在* [*偏斜二叉树*](https://www.geeksforgeeks.org/skewed-binary-tree/) *上，其遍历左或右子树都需要 O(N)的复杂度，计算子树的高度也需要 O(logN)的计算复杂度。*
***辅助空间:** O(1)*