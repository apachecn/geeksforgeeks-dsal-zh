# 对由值为 1 的节点组成的二叉树中的级别进行计数，这些节点组合在一起

> 原文:[https://www . geesforgeks . org/count-levels-in-a-a-binary-tree-由节点组成-value-1-group-together/](https://www.geeksforgeeks.org/count-levels-in-a-binary-tree-consisting-of-nodes-valued-1-grouped-together/)

给定一个仅由 **0** s 和 **1** s 组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)中的级别计数，其中所有 **1** s 连续放置在一个组中。

**示例:**

> **输入:** 0
> 
> / \
> 
>                   1     0
> 
> / \ / \
> 
>              1   0 1   0
> 
> **输出:** 2
> 
> **说明:**在 1 级和 2 级中，值为 1 的所有节点都是连续放置的。
> 
> **输入:** 0
> 
> / \
> 
>                 1     0
> 
> / \ \
> 
>              1   1       0
> 
> / \ \ / \
> 
>            1   1   1  0    0
> 
> **输出:** 4
> 
> **说明:**在所有级别中，值为 1 的节点是连续放置的。

**方法:**按照以下步骤解决问题:

*   使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)执行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
*   遍历[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)的每一级，考虑以下三个变量:
    1.  第一次出现值为 **1** 的节点后，**标志 1:** 设置为 **1** 。
    2.  第一次出现值为 **0 的节点后**设置为 **1** ，第二次出现值为 1 的节点后设置为。
    3.  **标志 2:** 在第一次出现值为 **1** 的节点后设置，此时**标志 0** 和**标志 1** 都设置为 **1** 。
*   遍历每个级别后，检查标志 1 是否设置为 1，标志 2 是否为 0。如果发现是真的，将该级别包括在计数中。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct node {

    // Left Child
    struct node* left;

    int data;

    // Right Child
    struct node* right;
};

// Function to perform level order traversal
// count levels with all 1s grouped together
int countLevels(node* root)
{
    if (root == NULL)
        return 0;

    int Count = 0;

    // Create an empty queue for
    // level order traversal
    queue<node*> q;

    // Stores front element of the queue
    node* curr;

    // Enqueue root and NULL node
    q.push(root);

    // Stores Nodes of
    // Current Level
    while (!q.empty()) {
        int n = q.size();

        int flag0 = 0, flag1 = 0, flag2 = 0;

        while (n--) {

            // Stores first node of
            // the current level
            curr = q.front();
            q.pop();

            if (curr) {

                // If left child exists
                if (curr->left)

                    // Push into the Queue
                    q.push(curr->left);

                // If right child exists
                if (curr->right)

                    // Push into the Queue
                    q.push(curr->right);

                if (curr->data == 1) {

                    // If current node is the first
                    // node with value 1
                    if (!flag1)
                        flag1 = 1;

                    // If current node has value 1
                    // after occurrence of nodes
                    // with value 0 following a
                    // sequence of nodes with value 1
                    if (flag1 && flag0)
                        flag2 = 1;
                }

                // If current node is the first node
                // with value 0 after a sequence
                // of nodes with value 1
                if (curr->data == 0 && flag1)
                    flag0 = 1;
            }
        }

        if (flag1 && !flag2)
            Count++;
    }

    return Count;
}

// Function to create a Tree Node
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Driver Code
int main()
{
    node* root = newNode(0);
    root->left = newNode(0);
    root->right = newNode(1);
    root->left->left = newNode(0);
    root->left->right = newNode(1);
    root->right->left = newNode(1);
    root->right->right = newNode(0);

    cout << countLevels(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

// A Binary Tree Node
static class node
{

    // Left Child
    node left;
    int data;

    // Right Child
    node right;
};

// Function to perform level order traversal
// count levels with all 1s grouped together
static int countLevels(node root)
{
    if (root == null)
        return 0;
    int Count = 0;

    // Create an empty queue for
    // level order traversal
    Queue<node> q = new LinkedList<>();

    // Stores front element of the queue
    node curr;

    // Enqueue root and null node
    q.add(root);

    // Stores Nodes of
    // Current Level
    while (!q.isEmpty())
    {
        int n = q.size();
        int flag0 = 0, flag1 = 0, flag2 = 0;
        while (n-- >0)
        {

            // Stores first node of
            // the current level
            curr = q.peek();
            q.remove();
            if (curr != null)
            {

                // If left child exists
                if (curr.left != null)

                    // Push into the Queue
                    q.add(curr.left);

                // If right child exists
                if (curr.right != null)

                    // Push into the Queue
                    q.add(curr.right);

                if (curr.data == 1)
                {

                    // If current node is the first
                    // node with value 1
                    if (flag1 == 0)
                        flag1 = 1;

                    // If current node has value 1
                    // after occurrence of nodes
                    // with value 0 following a
                    // sequence of nodes with value 1
                    if (flag1 > 0 && flag0 > 0)
                        flag2 = 1;
                }

                // If current node is the first node
                // with value 0 after a sequence
                // of nodes with value 1
                if (curr.data == 0 && flag1 > 0)
                    flag0 = 1;
            }
        }

        if (flag1 > 0 && flag2 == 0)
            Count++;
    }
    return Count;
}

// Function to create a Tree Node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver Code
public static void main(String[] args)
{
    node root = newNode(0);
    root.left = newNode(0);
    root.right = newNode(1);
    root.left.left = newNode(0);
    root.left.right = newNode(1);
    root.right.left = newNode(1);
    root.right.right = newNode(0);
    System.out.print(countLevels(root));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import deque

# A Binary Tree Node
class node:

    def __init__(self):

        # Left Child
        self.left = None

        self.data = 0

        # Right Child
        self.right = None

# Function to perform level order traversal
# count levels with all 1s grouped together
def countLevels(root):

    if (root == None):
        return 0

    Count = 0

    # Create an empty queue for
    # level order traversal
    q = deque()

    # Stores front element of the queue
    curr = node()

    # Enqueue root and None node
    q.append(root)

    # Stores Nodes of
    # Current Level
    while q:
        n = len(q)
        flag0 = 0
        flag1 = 0
        flag2 = 0

        while (n):

            # Stores first node of
            # the current level
            curr = q[0]
            q.popleft()

            if (curr):

                # If left child exists
                if (curr.left):

                    # Push into the Queue
                    q.append(curr.left)

                # If right child exists
                if (curr.right):

                    # Push into the Queue
                    q.append(curr.right)

                if (curr.data == 1):

                    # If current node is the first
                    # node with value 1
                    if (not flag1):
                        flag1 = 1

                    # If current node has value 1
                    # after occurrence of nodes
                    # with value 0 following a
                    # sequence of nodes with value 1
                    if (flag1 and flag0):
                        flag2 = 1

                # If current node is the first node
                # with value 0 after a sequence
                # of nodes with value 1
                if (curr.data == 0 and flag1):
                    flag0 = 1

            n -= 1

        if (flag1 and not flag2):
            Count += 1

    return Count

# Function to create a Tree Node
def newNode(data):

    temp = node()
    temp.data = data
    temp.left = None
    temp.right = None
    return temp

# Driver Code
if __name__ == "__main__":

    root = newNode(0)
    root.left = newNode(0)
    root.right = newNode(1)
    root.left.left = newNode(0)
    root.left.right = newNode(1)
    root.right.left = newNode(1)
    root.right.right = newNode(0)

    print(countLevels(root))

# This code is contributed by sanjeev2552
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// A Binary Tree Node
class node
{

    // Left Child
    public node left;
    public int data;

    // Right Child
    public node right;
};

// Function to perform level order traversal
// count levels with all 1s grouped together
static int countLevels(node root)
{
    if (root == null)
        return 0;
    int Count = 0;

    // Create an empty queue for
    // level order traversal
    Queue<node> q = new Queue<node>();

    // Stores front element of the queue
    node curr;

    // Enqueue root and null node
    q.Enqueue(root);

    // Stores Nodes of
    // Current Level
    while (q.Count != 0)
    {
        int n = q.Count;
        int flag0 = 0, flag1 = 0, flag2 = 0;
        while (n-- >0)
        {

            // Stores first node of
            // the current level
            curr = q.Peek();
            q.Dequeue();
            if (curr != null)
            {

                // If left child exists
                if (curr.left != null)

                    // Push into the Queue
                    q.Enqueue(curr.left);

                // If right child exists
                if (curr.right != null)

                    // Push into the Queue
                    q.Enqueue(curr.right);

                if (curr.data == 1)
                {

                    // If current node is the first
                    // node with value 1
                    if (flag1 == 0)
                        flag1 = 1;

                    // If current node has value 1
                    // after occurrence of nodes
                    // with value 0 following a
                    // sequence of nodes with value 1
                    if (flag1 > 0 && flag0 > 0)
                        flag2 = 1;
                }

                // If current node is the first node
                // with value 0 after a sequence
                // of nodes with value 1
                if (curr.data == 0 && flag1 > 0)
                    flag0 = 1;
            }
        }
        if (flag1 > 0 && flag2 == 0)
            Count++;
    }
    return Count;
}

// Function to create a Tree Node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver Code
public static void Main(String[] args)
{
    node root = newNode(0);
    root.left = newNode(0);
    root.right = newNode(1);
    root.left.left = newNode(0);
    root.left.right = newNode(1);
    root.right.left = newNode(1);
    root.right.right = newNode(0);
    Console.Write(countLevels(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

  // JavaScript program for above approach

  // A Binary Tree Node
  class node
  {
      constructor(data) {
         this.left = null;
         this.right = null;
         this.data = data;
      }
  }

  // Function to create a Tree Node
  function newNode(data)
  {
      let temp = new node(data);
      return temp;
  }

  // Function to perform level order traversal
  // count levels with all 1s grouped together
  function countLevels(root)
  {
      if (root == null)
          return 0;
      let Count = 0;

      // Create an empty queue for
      // level order traversal
      let q = [];

      // Stores front element of the queue
      let curr;

      // Enqueue root and null node
      q.push(root);

      // Stores Nodes of
      // Current Level
      while (q.length > 0)
      {
          let n = q.length;
          let flag0 = 0, flag1 = 0, flag2 = 0;
          while (n-- >0)
          {

              // Stores first node of
              // the current level
              curr = q[0];
              q.shift();
              if (curr != null)
              {

                  // If left child exists
                  if (curr.left != null)

                      // Push into the Queue
                      q.push(curr.left);

                  // If right child exists
                  if (curr.right != null)

                      // Push into the Queue
                      q.push(curr.right);

                  if (curr.data == 1)
                  {

                      // If current node is the first
                      // node with value 1
                      if (flag1 == 0)
                          flag1 = 1;

                      // If current node has value 1
                      // after occurrence of nodes
                      // with value 0 following a
                      // sequence of nodes with value 1
                      if (flag1 > 0 && flag0 > 0)
                          flag2 = 1;
                  }

                  // If current node is the first node
                  // with value 0 after a sequence
                  // of nodes with value 1
                  if (curr.data == 0 && flag1 > 0)
                      flag0 = 1;
              }
          }

          if (flag1 > 0 && flag2 == 0)
              Count++;
      }
      return Count;
  }

  let root = newNode(0);
  root.left = newNode(0);
  root.right = newNode(1);
  root.left.left = newNode(0);
  root.left.right = newNode(1);
  root.right.left = newNode(1);
  root.right.right = newNode(0);
  document.write(countLevels(root));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)