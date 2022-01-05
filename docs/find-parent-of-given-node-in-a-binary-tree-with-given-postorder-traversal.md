# 通过给定的后序遍历找到二叉树中给定节点的父节点

> 原文:[https://www . geesforgeks . org/find-给定后序遍历二叉树中给定节点的父节点/](https://www.geeksforgeeks.org/find-parent-of-given-node-in-a-binary-tree-with-given-postorder-traversal/)

给定两个整数 **N** 和 **K** ，其中 N 表示二叉树的高度，任务是在[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)中找到值为 K 的节点的父节点，该二叉树的[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)是第一个

![2^{N}-1       ](img/9ca35d606253a77c6349d3919d637824.png "Rendered by QuickLaTeX.com")

自然数

![(1, 2, ... 2^{N}-1)      ](img/e4c533fd6e981a080eb2658fef039d42.png "Rendered by QuickLaTeX.com")

```
For N = 3, the Tree will be -

      7
    /   \
   3     6
 /   \  /  \
1     2 4   5
```

**示例:**

> **输入:** N = 4，K = 5
> **输出:** 6
> **说明:**
> 节点 5 的父节点为 6。如上图所示。
> **输入:** N = 5，K = 3
> **输出:** 7
> **说明:**
> 节点 3 的父节点为 7。如上图所示。

**朴素方法:**一种简单的方法是按照以下模式构建树，然后遍历整棵树，找到给定节点的父节点。
**高效方法:**思路是用一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到节点的父节点。正如我们所知，高度为 N 的二叉树

![2^{N}-1       ](img/9ca35d606253a77c6349d3919d637824.png "Rendered by QuickLaTeX.com")

节点。因此，二分搜索法的搜索空间将是 1 到

![2^{N}-1       ](img/9ca35d606253a77c6349d3919d637824.png "Rendered by QuickLaTeX.com")

现在每个节点都有子值

![\frac{X}{2}       ](img/0e761438b0fed3148748c38105931111.png "Rendered by QuickLaTeX.com")

或者

![X-1       ](img/65f61f182dc104efaed005e08e6b7855.png "Rendered by QuickLaTeX.com")

因此，很容易找到这种节点的父节点。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// parent of the given node K in
// a binary tree whose post-order
// traversal is N natural numbers

#include <bits/stdc++.h>
using namespace std;

// Function to find the parent
// of the given node
int findParent(int height, int node)
{
    int start = 1;
    int end = pow(2, height) - 1;

    // Condition to check whether
    // the given node is a root node.
    // if it is then return -1 because
    // root node has no parent
    if (end == node)
        return -1;

    // Loop till we found
    // the given node
    while (node >= 1) {
        end = end - 1;

        // Finding the middle node of the
        // tree because at every level
        // tree parent is
        // divided into two halves
        int mid = start
                  + (end - start)
                        / 2;

        // if the node is found return
        // the parent always the child
        // nodes of every node
        // is node/2 or (node-1)
        if (mid == node || end == node) {
            return (end + 1);
        }

        // if the node to be found
        // is greater than the mid
        // search for left subtree else
        // search in right subtree
        else if (node < mid) {
            end = mid;
        }
        else {
            start = mid;
        }
    }
}

// Driver Code
int main()
{
    int height = 4;
    int node = 6;

    int k = findParent(height, node);
    cout << k;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// parent of the given node K in
// a binary tree whose post-order
// traversal is N natural numbers
import java.util.*;
class GFG{

// Function to find the parent
// of the given node
static int findParent(int height,
                      int node)
{
  int start = 1;
  int end = (int)Math.pow(2, height) - 1;

  // Condition to check whether
  // the given node is a root node.
  // if it is then return -1 because
  // root node has no parent
  if (end == node)
    return -1;

  // Loop till we found
  // the given node
  while (node >= 1)
  {
    end = end - 1;

    // Finding the middle node of the
    // tree because at every level
    // tree parent is
    // divided into two halves
    int mid = start + (end - start) / 2;

    // if the node is found return
    // the parent always the child
    // nodes of every node
    // is node*/2 or (node-1)
    if (mid == node || end == node)
    {
      return (end + 1);
    }

    // if the node to be found
    // is greater than the mid
    // search for left subtree else
    // search in right subtree
    else if (node < mid)
    {
      end = mid;
    }
    else
    {
      start = mid;
    }
  }
  return -1;
}

// Driver Code
public static void main(String[] args)
{
  int height = 4;
  int node = 6;
  int k = findParent(height, node);
  System.out.print(k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python implementation to find the
# parent of the given node

import math

# Function to find the parent
# of the given node
def findParent(height, node):

    start = 1
    end = pow(2, height) - 1

    # Check whether the given node
    # is a root node.if it is then
    # return -1 because root
    # node has no parent
    if (end == node):
        return -1

    # Loop till we found
    # the given node
    while(node >= 1):

        end = end - 1

        # Find the middle node of the
        # tree because at every level
        # tree parent is divided
        # into two halves
        mid = start + (end - start)//2

        # if the node is found
        # return the parent
        # always the child nodes of every
        # node is node / 2 or (node-1)
        if(mid == node or end == node):
            return (end + 1)

        # if the node to be found is greater
        # than the mid search for left
        # subtree else search in right subtree
        elif (node < mid):
            end = mid

        else:
            start = mid

# Driver code
if __name__ == "__main__":
    height = 4
    node = 6

    # Function Call
    k = findParent(height, node)
    print(k)
```

## C#

```
// C# implementation to find the
// parent of the given node K in
// a binary tree whose post-order
// traversal is N natural numbers
using System;
class GFG{

// Function to find the parent
// of the given node
static int findParent(int height,
                      int node)
{
  int start = 1;
  int end = (int)Math.Pow(2, height) - 1;

  // Condition to check whether
  // the given node is a root node.
  // if it is then return -1 because
  // root node has no parent
  if (end == node)
    return -1;

  // Loop till we found
  // the given node
  while (node >= 1)
  {
    end = end - 1;

    // Finding the middle node of the
    // tree because at every level
    // tree parent is
    // divided into two halves
    int mid = start + (end - start) / 2;

    // if the node is found return
    // the parent always the child
    // nodes of every node
    // is node*/2 or (node-1)
    if (mid == node || end == node)
    {
      return (end + 1);
    }

    // if the node to be found
    // is greater than the mid
    // search for left subtree else
    // search in right subtree
    else if (node < mid)
    {
      end = mid;
    }
    else
    {
      start = mid;
    }
  }
  return -1;
}

// Driver Code
public static void Main(String[] args)
{
  int height = 4;
  int node = 6;
  int k = findParent(height, node);
  Console.Write(k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // parent of the given node K in
    // a binary tree whose post-order
    // traversal is N natural numbers

    // Function to find the parent
    // of the given node
    function findParent(height, node)
    {
      let start = 1;
      let end = Math.pow(2, height) - 1;

      // Condition to check whether
      // the given node is a root node.
      // if it is then return -1 because
      // root node has no parent
      if (end == node)
        return -1;

      // Loop till we found
      // the given node
      while (node >= 1)
      {
        end = end - 1;

        // Finding the middle node of the
        // tree because at every level
        // tree parent is
        // divided into two halves
        let mid = start + parseInt((end - start) / 2, 10);

        // if the node is found return
        // the parent always the child
        // nodes of every node
        // is node*/2 or (node-1)
        if (mid == node || end == node)
        {
          return (end + 1);
        }

        // if the node to be found
        // is greater than the mid
        // search for left subtree else
        // search in right subtree
        else if (node < mid)
        {
          end = mid;
        }
        else
        {
          start = mid;
        }
      }
      return -1;
    }

    let height = 4;
    let node = 6;
    let k = findParent(height, node);
    document.write(k);

 // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
7
```