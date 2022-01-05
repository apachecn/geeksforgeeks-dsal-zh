# 计算从一个节点到由相同值的节点组成的叶子的对角线路径

> 原文:[https://www . geesforgeks . org/count-对角线路径-从节点到叶子-由相同值的节点组成/](https://www.geeksforgeeks.org/count-diagonal-paths-from-a-node-to-a-leaf-consisting-of-same-valued-nodes/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到到达二叉树叶子的[对角线](https://www.geeksforgeeks.org/diagonal-traversal-of-binary-tree/)路径的计数，使得同一对角线上所有节点的值相等。

**示例:**

> **输入:**
> 
> ```
>        5
>       / \
>      6   5
>       \   \
>        6   5
> ```
> 
> **输出:** 2
> **说明:**
> 对角线 6–6 和 5–5 包含相等的值。
> 因此，要求的输出为 2。
> 
> **输入:**
> 
> ```
>        5
>       / \
>      6   5
>       \   \
>        5   5
> ```
> 
> **输出:** 1

**方法:**主要思路是[使用](https://www.geeksforgeeks.org/diagonal-traversal-of-binary-tree/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)沿对角线遍历树。按照以下步骤解决此问题:

*   [以对角线顺序遍历给定的二叉树](https://www.geeksforgeeks.org/diagonal-traversal-of-binary-tree/)并将每个对角线的起始节点存储为**键**，对于每个**键**，将该对角线中的所有值存储在 [Hashset](https://www.geeksforgeeks.org/hashset-in-java/) 中。
*   遍历结束后，找到集合大小等于 **1** 的**键**的个数，打印为答案。

下面是上述方法的实现。

## C++14

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

struct TreeNode
{
    int val = 0;
    TreeNode *left, *right;

    TreeNode(int x)
    {
        val = x;
        left = NULL;
        right = NULL;
    }
};

// Function to perform diagonal
// traversal on the given binary tree
void fillMap(TreeNode *root, int left,
             map<int, set<int>> &diag)
{

    // If tree is empty
    if (!root)
        return;

    // If current diagonal is not visited
    if (diag[left].size() == 0)
    {

        // Update diag[left]
        diag[left].insert(root->val);
    }

    // Otherwise, map current node
    // with its diagonal
    else
        diag[left].insert(root->val);

    // Recursively, traverse left subtree
    fillMap(root->left, left + 1, diag);

    // Recursively, traverse right subtree
    fillMap(root->right, left, diag);
}

// Function to count diagonal
// paths having same-valued nodes
int sameDiag(TreeNode *root)
{

    // Maps the values of all
    // nodes with its diagonal
    map<int, set<int>> diag;

    // Stores indexing of diagonal
    int left = 0;

    // Function call to perform
    // diagonal traversal
    fillMap(root, left, diag);

    // Stores count of diagonals such
    // that all the nodes on the same
    // diagonal are equal
    int count = 0;

    // Traverse each diagonal
    for(auto d : diag)
    {

        // If all nodes on the current
        // diagonal are equal
        if (diag[d.first].size() == 1)

            // Update count
            count += 1;
    }
    return count;
}

// Driver Code
int main()
{

    // Given tree
    TreeNode *root = new TreeNode(5);
    root->left = new TreeNode(6);
    root->right = new TreeNode(5);
    root->left->right = new TreeNode(6);
    root->right->right = new TreeNode(5);

    // Function call
    cout << sameDiag(root);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Structure of a Node
  static class TreeNode
  {
    int val;
    TreeNode left, right;

    TreeNode(int key)
    {
      val = key;
      left = null;
      right = null;
    }
  };

  // Function to perform diagonal
  // traversal on the given binary tree
  static void fillMap(TreeNode root, int left,
                      Map<Integer,Set<Integer>> diag)
  {

    // If tree is empty
    if (root == null)
      return;

    // If current diagonal is not visited
    if (diag.get(left) == null)
    {

      // Update diag[left]
      diag.put(left, new HashSet<Integer>());
      diag.get(left).add(root.val);
    }

    // Otherwise, map current node
    // with its diagonal
    else
      diag.get(left).add(root.val);

    // Recursively, traverse left subtree
    fillMap(root.left, left + 1, diag);

    // Recursively, traverse right subtree
    fillMap(root.right, left, diag);
  }

  // Function to count diagonal
  // paths having same-valued nodes
  static int sameDiag(TreeNode root)
  {

    // Maps the values of all
    // nodes with its diagonal
    Map<Integer, Set<Integer>> diag = new HashMap<>();

    // Stores indexing of diagonal
    int left = 0;

    // Function call to perform
    // diagonal traversal
    fillMap(root, left, diag);

    // Stores count of diagonals such
    // that all the nodes on the same
    // diagonal are equal
    int count = 0;

    // Traverse each diagonal
    for(Map.Entry<Integer,Set<Integer>> d:diag.entrySet())
    {

      // If all nodes on the current
      // diagonal are equal
      if (d.getValue().size() == 1)

        // Update count
        count += 1;
    }
    return count;
  }

  // Driver function
  public static void main (String[] args)
  {
    TreeNode root = new TreeNode(5);
    root.left = new TreeNode(6);
    root.right = new TreeNode(5);
    root.left.right = new TreeNode(6);
    root.right.right = new TreeNode(5);

    System.out.println(sameDiag(root));
  }
}
// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Structure of a Node
class TreeNode:
    def __init__(self, val = 0, left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to count diagonal
# paths having same-valued nodes
def sameDiag(root):

    # Maps the values of all
    # nodes with its diagonal
    diag = {}

    # Stores indexing of diagonal
    left = 0

    # Function to perform diagonal
    # traversal on the given binary tree
    def fillMap(root, left):

        # If tree is empty
        if not root:
            return

        # If current diagonal is not visited
        if left not in diag:

            # Update diag[left]
            diag[left] = set([root.val])

        # Otherwise, map current node
        # with its diagonal
        else:
            diag[left].add(root.val)

        # Recursively, traverse left subtree
        fillMap(root.left, left + 1)

        # Recursively, traverse right subtree
        fillMap(root.right, left)

    # Function call to perform
    # diagonal traversal
    fillMap(root, left)

    # Stores count of diagonals such
    # that all the nodes on the same
    # diagonal are equal
    count = 0

    # Traverse each diagonal
    for d in diag:

        # If all nodes on the current
        # diagonal are equal
        if len(list(diag[d])) == 1:

            # Update count
            count += 1
    return count

# Driver Code
if __name__ == '__main__':

    # Given tree
    root = TreeNode(5)
    root.left = TreeNode(6)
    root.right = TreeNode(5)
    root.left.right = TreeNode(6)
    root.right.right = TreeNode(5)

    # Function call
    print(sameDiag(root))
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Structure of a Node
class TreeNode
{
    constructor(key)
    {
        this.val=key;
        this.left=this.right=null;
    }
}

// Function to perform diagonal
// traversal on the given binary tree
function fillMap(root,left,diag)
{
    // If tree is empty
    if (root == null)
      return;

    // If current diagonal is not visited
    if (diag.get(left) == null)
    {

      // Update diag[left]
      diag.set(left, new Set());
      diag.get(left).add(root.val);
    }

    // Otherwise, map current node
    // with its diagonal
    else
      diag.get(left).add(root.val);

    // Recursively, traverse left subtree
    fillMap(root.left, left + 1, diag);

    // Recursively, traverse right subtree
    fillMap(root.right, left, diag);
}

// Function to count diagonal
// paths having same-valued nodes
function sameDiag(root)
{
    // Maps the values of all
    // nodes with its diagonal
    let diag = new Map();

    // Stores indexing of diagonal
    let left = 0;

    // Function call to perform
    // diagonal traversal
    fillMap(root, left, diag);

    // Stores count of diagonals such
    // that all the nodes on the same
    // diagonal are equal
    let count = 0;

    // Traverse each diagonal
    for(let [key, value] of diag.entries())
    {

      // If all nodes on the current
      // diagonal are equal
      if (value.size == 1)

        // Update count
        count += 1;
    }
    return count;
}

// Driver function
let root = new TreeNode(5);
root.left = new TreeNode(6);
root.right = new TreeNode(5);
root.left.right = new TreeNode(6);
root.right.right = new TreeNode(5);

document.write(sameDiag(root));

// This code is contributed by patel2127

</script>
```

## C#

```
using System;
using System.Collections.Generic;
public class TreeNode
  {
    public int val;
    public TreeNode left, right;

    public TreeNode(int key)
    {
      val = key;
      left = null;
      right = null;
    }
  }

public class GFG{

    // Function to perform diagonal
  // traversal on the given binary tree
  static void fillMap(TreeNode root, int left,
                      Dictionary<int,HashSet<int>> diag)
  {

    // If tree is empty
    if (root == null)
      return;

    // If current diagonal is not visited
    if (!diag.ContainsKey(left))
    {

      // Update diag[left]
      diag.Add(left, new HashSet<int>());
      diag[left].Add(root.val);
    }

    // Otherwise, map current node
    // with its diagonal
    else
      diag[left].Add(root.val);

    // Recursively, traverse left subtree
    fillMap(root.left, left + 1, diag);

    // Recursively, traverse right subtree
    fillMap(root.right, left, diag);
  }

  // Function to count diagonal
  // paths having same-valued nodes
  static int sameDiag(TreeNode root)
  {

    // Maps the values of all
    // nodes with its diagonal
    Dictionary<int,HashSet<int>> diag = new Dictionary<int,HashSet<int>>();

    // Stores indexing of diagonal
    int left = 0;

    // Function call to perform
    // diagonal traversal
    fillMap(root, left, diag);

    // Stores count of diagonals such
    // that all the nodes on the same
    // diagonal are equal
    int count = 0;

    // Traverse each diagonal
    foreach(KeyValuePair<int,HashSet<int>> d in diag)
    {

      // If all nodes on the current
      // diagonal are equal
      if (d.Value.Count == 1)

        // Update count
        count += 1;
    }
    return count;
  }
    // Driver function
    static public void Main (){

        TreeNode root = new TreeNode(5);
    root.left = new TreeNode(6);
    root.right = new TreeNode(5);
    root.left.right = new TreeNode(6);
    root.right.right = new TreeNode(5);

    Console.WriteLine(sameDiag(root));

    }
}
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)