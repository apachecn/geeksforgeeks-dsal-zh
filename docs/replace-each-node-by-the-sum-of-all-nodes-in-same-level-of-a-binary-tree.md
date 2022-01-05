# 用二叉树同一层级的所有节点之和替换每个节点

> 原文:[https://www . geeksforgeeks . org/用二进制同层树中所有节点的总和替换每个节点/](https://www.geeksforgeeks.org/replace-each-node-by-the-sum-of-all-nodes-in-same-level-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是用同一级别中所有节点的总和替换每个节点的值。

**示例:**

> **输入:**
> 
> ```
>              9
>             / \
>            6   10
>           / \   \
>          4   7   11
>         / \   \
>        3  5   8
> ```
> 
> **输出:**
> 
> ```
>              9
>             / \
>           16   16
>           / \   \
>         22   22  22
>         / \   \
>       16  16   16
> ```
> 
> **说明:**
> 1:9 级节点之和
> 2:6+10 级节点之和= 16
> 3:4+7+11 级节点之和= 22
> 4:3+5+8 级节点之和= 16
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
> **输出:**
> 
> ```
>              5
>             / \
>            9   9
>           / \   \
>         15   15   15
> ```

**方法:**利用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)找到树的每一级节点的和并用该级节点的和替换每个节点的思想。按照以下步骤解决问题:

*   初始化两个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，比如 **que1** 和 **que2** ，可以用 **que1** 计算每一级节点的总和，用 **que2** 将每一个节点替换为同一级所有节点的总和。
*   使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)计算树的每一级所有节点的总和。
*   使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，用树中该级所有节点的和替换每个节点。
*   最后，使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)打印树。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of the binary tree
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

// Function to replace each node of the tree
// with the sum of nodes in the same level
TreeNode* replaceLvl(TreeNode *root){

  // If root is null
  if (!root)
    return root;

  // Queue to store nodes
  // of each level of the Tree
  queue<TreeNode*> que1;
  queue<TreeNode*> que2;
  que1.push(root);
  que2.push(root);

  while (true)
  {

    // Stores length of que1
    int lenque1 = que1.size();

    // Stores length of que2
    int lenque2 = que2.size();

    // Stores sum of nodes at
    // each level of the tree
    int lvlsum = 0;

    if (lenque1 == 0)
      break;

    // Traverse the tree and store
    // the sum at each level
    while (lenque1 > 0)
    {

      // Stores the front element
      // of the queue
      auto temp = que1.front();
      que1.pop();

      // Update lvlsum
      lvlsum += temp->val;

      // If left subtree not null
      if (temp->left)
        que1.push(temp->left);

      // If right subtree not null
      if (temp->right)
        que1.push(temp->right);

      // Update lenque1
      lenque1 -= 1;
    }

    // Replace all the nodes of at
    // each level of the tree
    while (lenque2 > 0)
    {

      // Stores front element
      // of the queue
      auto temp = que2.front();
      que2.pop();

      // Replace current node with
      // the sum of nodes
      temp->val = lvlsum;

      // If left subtree is not null
      if (temp->left)
        que2.push(temp->left);

      // If right subtree is not null
      if (temp->right)
        que2.push(temp->right);

      // Update lenque2
      lenque2 -= 1;
    }
  }
  return root;
}

// Function to print level order
// traversal of the Binary Tree
void printLvl(TreeNode *root)
{

  // Push root node into queue
  queue<TreeNode*> que;
  que.push(root);

  while (true)
  {

    // Stores count of nodes
    // at each level
    int length = que.size();

    // If no nodes left
    if (length == 0)
      break;

    while (length)
    {

      //Stores front element
      // of the queue
      auto temp = que.front();
      que.pop();
      cout << temp->val << " ";

      // If left subtree is not null
      if (temp->left)
        que.push(temp->left);

      // If right subtree is not null
      if (temp->right)
        que.push(temp->right);

      // Update length
      length -= 1;
    }
    cout << endl;
  }
}

// Driver Code
int main()
{

  TreeNode *root = new TreeNode(4);
  root->left = new TreeNode(5);
  root->right = new TreeNode(7);
  root->left->left = new TreeNode(1);
  root->left->right = new TreeNode(3);
  root->right->right = new TreeNode(5);

  // To update the tree
  root = replaceLvl(root);

  // To display the updated tree
  printLvl(root);

  return 0;
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

  // Function to replace each node of the tree
  // with the sum of nodes in the same level
  static TreeNode replaceLvl(TreeNode root){

    // If root is null
    if (root==null)
      return root;

    // Queue to store nodes
    // of each level of the Tree
    Queue<TreeNode> que1=new LinkedList<>();
    Queue<TreeNode> que2=new LinkedList<>();
    que1.add(root);
    que2.add(root);

    while (true)
    {

      // Stores length of que1
      int lenque1 = que1.size();

      // Stores length of que2
      int lenque2 = que2.size();

      // Stores sum of nodes at
      // each level of the tree
      int lvlsum = 0;

      if (lenque1 == 0)
        break;

      // Traverse the tree and store
      // the sum at each level
      while (lenque1 > 0)
      {

        // Stores the front element
        // of the queue
        TreeNode temp = que1.peek();
        que1.poll();

        // Update lvlsum
        lvlsum += temp.val;

        // If left subtree not null
        if (temp.left!=null)
          que1.add(temp.left);

        // If right subtree not null
        if (temp.right!=null)
          que1.add(temp.right);

        // Update lenque1
        lenque1 -= 1;
      }

      // Replace all the nodes of at
      // each level of the tree
      while (lenque2 > 0)
      {

        // Stores front element
        // of the queue
        TreeNode temp = que2.peek();
        que2.poll();

        // Replace current node with
        // the sum of nodes
        temp.val = lvlsum;

        // If left subtree is not null
        if (temp.left!=null)
          que2.add(temp.left);

        // If right subtree is not null
        if (temp.right!=null)
          que2.add(temp.right);

        // Update lenque2
        lenque2 -= 1;
      }
    }
    return root;
  }

  // Function to print level order
  // traversal of the Binary Tree
  static void printLvl(TreeNode root)
  {

    // Push root node into queue
    Queue<TreeNode> que = new LinkedList<>();
    que.add(root);

    while (true)
    {

      // Stores count of nodes
      // at each level
      int length = que.size();

      // If no nodes left
      if (length == 0)
        break;

      while (length>0)
      {

        //Stores front element
        // of the queue
        TreeNode temp = que.peek();
        que.poll();
        System.out.print(temp.val+" ");

        // If left subtree is not null
        if (temp.left != null)
          que.add(temp.left);

        // If right subtree is not null
        if (temp.right != null)
          que.add(temp.right);

        // Update length
        length -= 1;
      }
      System.out.println();
    }
  }

  // Driver function
  public static void main (String[] args) {
    TreeNode root = new TreeNode(4);
    root.left = new TreeNode(5);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(3);
    root.right = new TreeNode(7);
    root.right.right = new TreeNode(5);

    // To update the tree
    root = replaceLvl(root);

    // To display the updated tree
    printLvl(root);

  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Structure of the binary tree
class TreeNode:
    def __init__(self, val = 0,
                left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to replace each node of the tree
# with the sum of nodes in the same level
def replaceLvl(root):

    # If root is null
    if not root:
        return

    # Queue to store nodes
    # of each level of the Tree   
    que1 = [root]
    que2 = [root]

    while True:

        # Stores length of que1
        lenque1 = len(que1)

        # Stores length of que2
        lenque2 = len(que2)

        # Stores sum of nodes at
        # each level of the tree
        lvlsum = 0
        if not lenque1:
            break

        # Traverse the tree and store
        # the sum at each level
        while lenque1:

            # Stores the front element
            # of the queue
            temp = que1.pop(0)

            # Update lvlsum
            lvlsum += temp.val

            # If left subtree not null
            if temp.left:
                que1.append(temp.left)

            # If right subtree not null   
            if temp.right:
                que1.append(temp.right)

            # Update lenque1   
            lenque1 -= 1

        # Replace all the nodes of at
        # each level of the tree
        while lenque2:

            # Stores front element
            # of the queue
            temp = que2.pop(0)

            # Replace current node with
            # the sum of nodes
            temp.val = lvlsum

            # If left subtree is not null
            if temp.left:
                que2.append(temp.left)

            # If right subtree is not null   
            if temp.right:
                que2.append(temp.right)

            # Update lenque2   
            lenque2 -= 1
    return root

# Function to print level order
# traversal of the Binary Tree
def printLvl(root):

    # Push root node into queue
    que = [root]
    while True:

        # Stores count of nodes
        # at each level
        length = len(que)

        # If no nodes left
        if not length:
            break

        while length:

            # Stores front element
            # of the queue
            temp = que.pop(0)
            print(temp.val, end =' ')

            # If left subtree is not null
            if temp.left:
                que.append(temp.left)

            # If right subtree is not null   
            if temp.right:
                que.append(temp.right)

            # Update length   
            length -= 1
        print()

# Driver Code

root = TreeNode(4)
root.left = TreeNode(5)
root.right = TreeNode(7)
root.left.left = TreeNode(1)
root.left.right = TreeNode(3)
root.right.right = TreeNode(5)

# To update the tree
root = replaceLvl(root)

# To display the updated tree
printLvl(root)
```

## C#

```
// C# program for above approach

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

    // Function to replace each node of the tree
  // with the sum of nodes in the same level
  static TreeNode replaceLvl(TreeNode root){

    // If root is null
    if (root==null)
      return root;

    // Queue to store nodes
    // of each level of the Tree
    Queue<TreeNode> que1=new Queue<TreeNode>();
    Queue<TreeNode> que2=new Queue<TreeNode>();
    que1.Enqueue(root);
    que2.Enqueue(root);

    while (true)
    {

      // Stores length of que1
      int lenque1 = que1.Count;

      // Stores length of que2
      int lenque2 = que2.Count;

      // Stores sum of nodes at
      // each level of the tree
      int lvlsum = 0;

      if (lenque1 == 0)
        break;

      // Traverse the tree and store
      // the sum at each level
      while (lenque1 > 0)
      {

        // Stores the front element
        // of the queue
        TreeNode temp = que1.Dequeue();

        // Update lvlsum
        lvlsum += temp.val;

        // If left subtree not null
        if (temp.left!=null)
          que1.Enqueue(temp.left);

        // If right subtree not null
        if (temp.right!=null)
          que1.Enqueue(temp.right);

        // Update lenque1
        lenque1 -= 1;
      }

      // Replace all the nodes of at
      // each level of the tree
      while (lenque2 > 0)
      {

        // Stores front element
        // of the queue
        TreeNode temp = que2.Dequeue();

        // Replace current node with
        // the sum of nodes
        temp.val = lvlsum;

        // If left subtree is not null
        if (temp.left!=null)
          que2.Enqueue(temp.left);

        // If right subtree is not null
        if (temp.right!=null)
          que2.Enqueue(temp.right);

        // Update lenque2
        lenque2 -= 1;
      }
    }
    return root;
  }

  // Function to print level order
  // traversal of the Binary Tree
  static void printLvl(TreeNode root)
  {

    // Push root node into queue
    Queue<TreeNode> que = new Queue<TreeNode>();
    que.Enqueue(root);

    while (true)
    {

      // Stores count of nodes
      // at each level
      int length = que.Count;

      // If no nodes left
      if (length == 0)
        break;

      while (length>0)
      {

        //Stores front element
        // of the queue
        TreeNode temp = que.Dequeue();

        Console.Write(temp.val+" ");

        // If left subtree is not null
        if (temp.left != null)
          que.Enqueue(temp.left);

        // If right subtree is not null
        if (temp.right != null)
          que.Enqueue(temp.right);

        // Update length
        length -= 1;
      }
      Console.WriteLine();
    }
  }

  // Driver function

    static public void Main (){

        TreeNode root = new TreeNode(4);
    root.left = new TreeNode(5);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(3);
    root.right = new TreeNode(7);
    root.right.right = new TreeNode(5);

    // To update the tree
    root = replaceLvl(root);

    // To display the updated tree
    printLvl(root);

    }
}

// This code is contributed by patel2127
```

## java 描述语言

```
<script>

  // JavaScript program for above approach

  // Structure of a Node
  class TreeNode
  {
      constructor(key) {
         this.left = null;
         this.right = null;
         this.val = key;
      }
  }

  // Function to replace each node of the tree
  // with the sum of nodes in the same level
  function replaceLvl(root){

    // If root is null
    if (root==null)
      return root;

    // Queue to store nodes
    // of each level of the Tree
    let que1 = [];
    let que2 = [];
    que1.push(root);
    que2.push(root);

    while (true)
    {

      // Stores length of que1
      let lenque1 = que1.length;

      // Stores length of que2
      let lenque2 = que2.length;

      // Stores sum of nodes at
      // each level of the tree
      let lvlsum = 0;

      if (lenque1 == 0)
        break;

      // Traverse the tree and store
      // the sum at each level
      while (lenque1 > 0)
      {

        // Stores the front element
        // of the queue
        let temp = que1[0];
        que1.shift();

        // Update lvlsum
        lvlsum += temp.val;

        // If left subtree not null
        if (temp.left!=null)
          que1.push(temp.left);

        // If right subtree not null
        if (temp.right!=null)
          que1.push(temp.right);

        // Update lenque1
        lenque1 -= 1;
      }

      // Replace all the nodes of at
      // each level of the tree
      while (lenque2 > 0)
      {

        // Stores front element
        // of the queue
        let temp = que2[0];
        que2.shift();

        // Replace current node with
        // the sum of nodes
        temp.val = lvlsum;

        // If left subtree is not null
        if (temp.left!=null)
          que2.push(temp.left);

        // If right subtree is not null
        if (temp.right!=null)
          que2.push(temp.right);

        // Update lenque2
        lenque2 -= 1;
      }
    }
    return root;
  }

  // Function to print level order
  // traversal of the Binary Tree
  function printLvl(root)
  {

    // Push root node into queue
    let que = [];
    que.push(root);

    while (true)
    {

      // Stores count of nodes
      // at each level
      let length = que.length;

      // If no nodes left
      if (length == 0)
        break;

      while (length>0)
      {

        //Stores front element
        // of the queue
        let temp = que[0];
        que.shift();
        document.write(temp.val+" ");

        // If left subtree is not null
        if (temp.left != null)
          que.push(temp.left);

        // If right subtree is not null
        if (temp.right != null)
          que.push(temp.right);

        // Update length
        length -= 1;
      }
      document.write("</br>");
    }
  }

  let root = new TreeNode(4);
  root.left = new TreeNode(5);
  root.left.left = new TreeNode(1);
  root.left.right = new TreeNode(3);
  root.right = new TreeNode(7);
  root.right.right = new TreeNode(5);

  // To update the tree
  root = replaceLvl(root);

  // To display the updated tree
  printLvl(root);

</script>
```

**Output:** 

```
4 
12 12 
9 9 9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)