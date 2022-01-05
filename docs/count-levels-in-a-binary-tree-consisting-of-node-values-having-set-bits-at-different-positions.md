# 由节点值组成的二叉树中的计数级别，节点值在不同的位置有设定位

> 原文:[https://www . geesforgeks . org/count-levels-in-a-a-binary-tree-由节点值组成-在不同位置具有集合位/](https://www.geeksforgeeks.org/count-levels-in-a-binary-tree-consisting-of-node-values-having-set-bits-at-different-positions/)

给定由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算**二叉树**中的级别数，使得同一级别的所有节点值的设置位位于不同的位置。

**示例:**

> **输入:**
> 
> ```
>       
>                5
>               / \
>              6   9
>             / \   \
>            1   4   7
> ```
> 
> **输出:** 2
> **说明:**
> 一级只有 5 (= (101) <sub>2</sub> )。
> 2 级有 6 (= (0110) <sub>2</sub> )和 9 (= (1001) <sub>2</sub> )。所有设置位都位于唯一的位置。
> 三级有 1 (0001) <sub>2</sub> 、4 (0100) <sub>2</sub> 和 7(0111) <sub>2</sub> 。因此，节点值 5 和 7 的第 0<sup>位被设置。</sup>
> 
> **输入:**
> 
> ```
>   
>             1
>            / \
>           2   3
>          / \   \
>         5   4   7
> ```
> 
> **输出:** 1

**朴素方法:**解决这个问题最简单的方法是使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)遍历二叉树，并在树的每一级使用 Map 存储所有节点的集合位。遍历地图，检查同一位置的置位频率是否小于等于 1。如果发现为真，则增加计数。最后，打印获得的计数。

***时间复杂度:**O(N)*
T5**辅助空间:** O(32)

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果两个数字 A 和 B 的所有设置位都在不同的位置
> 异或 B = A 或 B

按照以下步骤解决问题:

*   初始化一个变量，比如 **prefiX_XOR** ，存储每一级所有节点的前缀 XOR。
*   初始化一个变量，比如 **prefiX_OR** ，存储每一级所有节点的 prefix OR。
*   [使用层级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)遍历二叉树。在每一个 **i <sup>th</sup>** 级别，检查 **prefix_XOR ^节点**是否等于 **(prefix_OR | nodes)** 。如果发现当前级别的所有节点都为真，则增加计数。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Structure of a node in
// the binary tree
struct TreeNode
{
  int val = 0;
  TreeNode *left,*right;
  TreeNode(int x)
  {
        val = x;
        left = NULL;
        right = NULL;
  }
};

// Function to find total unique levels
void uniqueLevels(TreeNode *root)
{

    // Stores count of levels, where the set
    // bits of all the nodes are at
    // different positions
    int uniqueLevels = 0;

    // Store nodes at  each level of
    // the tree using BFS
    queue<TreeNode*> que;
    que.push(root);

    // Performing level order traversal
    while (que.size() > 0)
    {

        // Stores count of nodes at
        // current level
        int length = que.size();

        // Stores prefix XOR of all
        // the nodes at current level
        int prefix_XOR = 0;

        // Stores prefix OR of all
        // the nodes at current level
        int prefix_OR = 0;

        // Check if set bit of all the nodes
        // at current level is at different
        // positions or not
        bool flag = true;

        // Traverse nodes at current level
        for(int i = 0; i < length; i++){

            // Stores front element
            // of the que
            TreeNode *temp = que.front();
            que.pop();

            // Update prefix_OR
            prefix_OR |= temp->val;

            // Update prefix_XOR
            prefix_XOR ^= temp->val;
            if (prefix_XOR != prefix_OR)
                flag = false;

            // If left subtree not NULL
            if (temp->left)
                que.push(temp->left);

            // If right subtree not NULL
            if (temp->right)
                que.push(temp->right);

            // Update length
        }

        //If bitwise AND is zero
        if (flag)
            uniqueLevels += 1;
      }
    cout << uniqueLevels;
}

// Driver Code
int main()
{
  TreeNode *root = new TreeNode(5);
  root->left = new TreeNode(6);
  root->right = new TreeNode(9);
  root->left->left = new TreeNode(1);
  root->left->right = new TreeNode(4);
  root->right->right = new TreeNode(7);

  // Function Call
  uniqueLevels(root);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Structure of a node in
  // the binary tree
  static class TreeNode
  {
    int val = 0;
    TreeNode left, right;
    TreeNode(int x)
    {
      val = x;
      left = null;
      right = null;
    }
  };

  // Function to find total unique levels
  static void uniqueLevels(TreeNode root)
  {

    // Stores count of levels, where the set
    // bits of all the nodes are at
    // different positions
    int uniqueLevels = 0;

    // Store nodes at  each level of
    // the tree using BFS
    Queue<TreeNode> que = new LinkedList<>();
    que.add(root);

    // Performing level order traversal
    while (que.size() > 0)
    {

      // Stores count of nodes at
      // current level
      int length = que.size();

      // Stores prefix XOR of all
      // the nodes at current level
      int prefix_XOR = 0;

      // Stores prefix OR of all
      // the nodes at current level
      int prefix_OR = 0;

      // Check if set bit of all the nodes
      // at current level is at different
      // positions or not
      boolean flag = true;

      // Traverse nodes at current level
      for(int i = 0; i < length; i++)
      {

        // Stores front element
        // of the que
        TreeNode temp = que.peek();
        que.remove();

        // Update prefix_OR
        prefix_OR |= temp.val;

        // Update prefix_XOR
        prefix_XOR ^= temp.val;
        if (prefix_XOR != prefix_OR)
          flag = false;

        // If left subtree not null
        if (temp.left != null)
          que.add(temp.left);

        // If right subtree not null
        if (temp.right != null)
          que.add(temp.right);

        // Update length
      }

      //If bitwise AND is zero
      if (flag)
        uniqueLevels += 1;
    }
    System.out.print(uniqueLevels);
  }

  // Driver Code
  public static void main(String[] args)
  {
    TreeNode root = new TreeNode(5);
    root.left = new TreeNode(6);
    root.right = new TreeNode(9);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(4);
    root.right.right = new TreeNode(7);

    // Function Call
    uniqueLevels(root);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Structure of a node in
# the binary tree
class TreeNode:
    def __init__(self, val = 0, left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to find total unique levels
def uniqueLevels(root):

    # Stores count of levels, where the set
    # bits of all the nodes are at
    # different positions
    uniqueLevels = 0

    # Store nodes at  each level of
    # the tree using BFS
    que = [root]

    # Performing level order traversal
    while len(que):

        # Stores count of nodes at
        # current level
        length = len(que)

        # Stores prefix XOR of all
        # the nodes at current level
        prefix_XOR = 0;

        # Stores prefix OR of all
        # the nodes at current level
        prefix_OR = 0

        # Check if set bit of all the nodes
        # at current level is at different
        # positions or not
        flag = True

        # Traverse nodes at current level
        while length:

            # Stores front element
            # of the que
            temp = que.pop(0)

            # Update prefix_OR
            prefix_OR |= temp.val

            # Update prefix_XOR
            prefix_XOR ^= temp.val

            if prefix_XOR != prefix_OR:
                flag = False

            # If left subtree not NULL
            if temp.left:
                que.append(temp.left)

            # If right subtree not NULL   
            if temp.right:
                que.append(temp.right)

            # Update length   
            length -= 1

        # If bitwise AND is zero
        if flag:
            uniqueLevels += 1

    print(uniqueLevels)

# Driver Code
if __name__ == '__main__':

    root = TreeNode(5)
    root.left = TreeNode(6)
    root.right = TreeNode(9)
    root.left.left = TreeNode(1)
    root.left.right = TreeNode(4)
    root.right.right = TreeNode(7)

    # Function Call
    uniqueLevels(root)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Structure of a node in
  // the binary tree
  class TreeNode
  {
    public int val = 0;
    public TreeNode left, right;
    public TreeNode(int x)
    {
      val = x;
      left = null;
      right = null;
    }
  };

  // Function to find total unique levels
  static void uniqueLevels(TreeNode root)
  {

    // Stores count of levels, where the set
    // bits of all the nodes are at
    // different positions
    int uniqueLevels = 0;

    // Store nodes at  each level of
    // the tree using BFS
    Queue<TreeNode> que = new Queue<TreeNode>();
    que.Enqueue(root);

    // Performing level order traversal
    while (que.Count > 0)
    {

      // Stores count of nodes at
      // current level
      int length = que.Count;

      // Stores prefix XOR of all
      // the nodes at current level
      int prefix_XOR = 0;

      // Stores prefix OR of all
      // the nodes at current level
      int prefix_OR = 0;

      // Check if set bit of all the nodes
      // at current level is at different
      // positions or not
      bool flag = true;

      // Traverse nodes at current level
      for(int i = 0; i < length; i++)
      {

        // Stores front element
        // of the que
        TreeNode temp = que.Peek();
        que.Dequeue();

        // Update prefix_OR
        prefix_OR |= temp.val;

        // Update prefix_XOR
        prefix_XOR ^= temp.val;
        if (prefix_XOR != prefix_OR)
          flag = false;

        // If left subtree not null
        if (temp.left != null)
          que.Enqueue(temp.left);

        // If right subtree not null
        if (temp.right != null)
          que.Enqueue(temp.right);

        // Update length
      }

      //If bitwise AND is zero
      if (flag)
        uniqueLevels += 1;
    }
    Console.Write(uniqueLevels);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    TreeNode root = new TreeNode(5);
    root.left = new TreeNode(6);
    root.right = new TreeNode(9);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(4);
    root.right.right = new TreeNode(7);

    // Function Call
    uniqueLevels(root);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Structure of a node in
// the binary tree
class TreeNode
{
    constructor(x)
    {
        this.val = x;
        this.left = null;
          this.right = null;
    }
}

// Function to find total unique levels
function uniqueLevels(root)
{

    // Stores count of levels, where the set
    // bits of all the nodes are at
    // different positions
    let uniqueLevels = 0;

    // Store nodes at  each level of
    // the tree using BFS
    let que = [];
    que.push(root);

    // Performing level order traversal
    while (que.length > 0)
    {

        // Stores count of nodes at
        // current level
        let length = que.length;

        // Stores prefix XOR of all
        // the nodes at current level
        let prefix_XOR = 0;

        // Stores prefix OR of all
        // the nodes at current level
        let prefix_OR = 0;

        // Check if set bit of all the nodes
        // at current level is at different
        // positions or not
        let flag = true;

        // Traverse nodes at current level
        for(let i = 0; i < length; i++)
        {

            // Stores front element
            // of the que
            let temp = que[0];
            que.shift();

            // Update prefix_OR
            prefix_OR |= temp.val;

            // Update prefix_XOR
            prefix_XOR ^= temp.val;
            if (prefix_XOR != prefix_OR)
                flag = false;

            // If left subtree not null
            if (temp.left != null)
                que.push(temp.left);

            // If right subtree not null
            if (temp.right != null)
                que.push(temp.right);
        }

        // If bitwise AND is zero
        if (flag)
            uniqueLevels += 1;
    }
    document.write(uniqueLevels);
}

// Driver Code
let root = new TreeNode(5);
root.left = new TreeNode(6);
root.right = new TreeNode(9);
root.left.left = new TreeNode(1);
root.left.right = new TreeNode(4);
root.right.right = new TreeNode(7);

// Function Call
uniqueLevels(root);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)