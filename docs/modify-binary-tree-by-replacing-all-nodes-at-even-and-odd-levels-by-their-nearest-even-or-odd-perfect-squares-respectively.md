# 修改二叉树，将偶数和奇数层的所有节点分别替换为最近的偶数或奇数完美方块

> 原文:[https://www . geeksforgeeks . org/modify-二叉树-通过用最接近的偶数或奇数完美正方形分别替换偶数和奇数层的所有节点/](https://www.geeksforgeeks.org/modify-binary-tree-by-replacing-all-nodes-at-even-and-odd-levels-by-their-nearest-even-or-odd-perfect-squares-respectively/)

给定一个由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是用最接近的偶数[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)替换二叉树中所有出现在偶数层的节点，用最接近的奇数[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)替换奇数层的节点。

**示例:**

> **输入:** 5
> / \
> 3 2
> / \
> 16 19
> 
> **输出:** 9
> / \
> 4 4
> / \
> 9 25
> 
> **说明:**
> 1 级:离 5 最近的奇完美平方是 9。
> 2 级:距离 3 和 2 最近的偶数完美方块是 4。
> 等级 3:离 16 最近的奇数完美平方是 9，离 19 最近的是 25。
> 
> **输入:** 45
> / \
> 65 32
> /
> 89
> 
> **输出:** 49
> / \
> 64 36
> /
> 81
> 
> **说明:**
> 一级:离 45 最近的奇完美平方是 49。
> 2 级:距离 65 和 32 最近的偶数完美方块分别是 64 和 36。
> 3 级:离 89 最近的奇完美平方是 81。

**方法:**给定的问题可以使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)来解决。按照以下步骤解决问题:

1.  初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，说 **q.**
2.  [将**根**推入队列。](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)
3.  当[队列不为空时循环](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)
    *   将当前节点存储在一个变量中，比如 **temp_node** 。
    *   如果[当前节点值是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，检查以下内容:
        *   如果 level 的值为奇数，当前节点的值为偶数，则查找最近的奇数[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)并更新 **temp_node→data** 。
        *   如果 level 的值为偶数，当前节点的值为奇数，则找到最近的偶数[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)并更新 **temp_node→data** 。
    *   否则，如果 level 的值为奇数，则寻找最近的奇完美平方；如果 level 的值为偶数，则寻找最近的偶完美平方。更新**temp _ node→数据**。
    *   Print **temp_node→data** 。
    *   [将](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/) **temp_node** 的子节点(先**左**，再**右**子节点)入队到 **q** ，如果存在的话。
    *   [从 **q** 出队](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)当前节点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a
// Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to replace all nodes
// at even and odd levels with their
// nearest even or odd perfect squares
void LevelOrderTraversal(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue
    // for level order traversal
    queue<Node*> q;

    // Enqueue root
    q.push(root);

    // Initialize height
    int lvl = 1;

    // Iterate until queue is not empty
    while (q.empty() == false) {

        // Store the size
        // of the queue
        int n = q.size();

        // Traverse in range [1, n]
        for (int i = 0; i < n; i++) {

            // Store the current node
            Node* node = q.front();

            // Store its square root
            double num = sqrt(node->data);
            int x1 = floor(num);
            int x2 = ceil(num);

            // Check if it is a perfect square
            if (x1 == x2) {

                // If level is odd and value is even,
                // find the closest odd perfect square
                if ((lvl & 1) && !(x1 & 1)) {

                    int num1 = x1 - 1, num2 = x1 + 1;

                    node->data
                        = (abs(node->data - num1 * num1)
                           < abs(node->data - num2 * num2))
                              ? (num1 * num1)
                              : (num2 * num2);
                }

                // If level is even and value is odd,
                // find the closest even perfect square
                if (!(lvl & 1) && (x1 & 1)) {

                    int num1 = x1 - 1, num2 = x1 + 1;

                    node->data
                        = (abs(node->data - num1 * num1)
                           < abs(node->data - num2 * num2))
                              ? (num1 * num1)
                              : (num2 * num2);
                }
            }

            // Otherwise, find the find
            // the nearest perfect square
            else {
                if (lvl & 1)
                    node->data
                        = (x1 & 1) ? (x1 * x1) : (x2 * x2);
                else
                    node->data
                        = (x1 & 1) ? (x2 * x2) : (x1 * x1);
            }

            // Print front of queue
            // and remove it from queue
            cout << node->data << " ";
            q.pop();

            // Enqueue left child
            if (node->left != NULL)
                q.push(node->left);

            // Enqueue right child
            if (node->right != NULL)
                q.push(node->right);
        }

        // Increment the level by 1
        lvl++;
        cout << endl;
    }
}

// Utility function to
// create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver Code
int main()
{
    // Binary Tree
    Node* root = newNode(5);
    root->left = newNode(3);
    root->right = newNode(2);
    root->right->left = newNode(16);
    root->right->right = newNode(19);

    LevelOrderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

// Structure of a
// Binary Tree Node
class Node
{
    int data;
    Node left, right;

    Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class GFG{

// Function to replace all nodes
// at even and odd levels with their
// nearest even or odd perfect squares
static void LevelOrderTraversal(Node root)
{

    // Base Case
    if (root == null)
        return;

    // Create an empty queue
    // for level order traversal
    Queue<Node> q = new LinkedList<>();

    // Enqueue root
    q.add(root);

    // Initialize height
    int lvl = 1;

    // Iterate until queue is not empty
    while (q.size() != 0)
    {

        // Store the size
        // of the queue
        int n = q.size();

        // Traverse in range [1, n]
        for(int i = 0; i < n; i++)
        {

            // Store the current node
            Node node = q.peek();

            // Store its square root
            double num = Math.sqrt(node.data);
            int x1 = (int)Math.floor(num);
            int x2 = (int)Math.ceil(num);

            // Check if it is a perfect square
            if (x1 == x2)
            {

                // If level is odd and value is even,
                // find the closest odd perfect square
                if (((lvl & 1) != 0) && !((x1 & 1) != 0))
                {
                    int num1 = x1 - 1, num2 = x1 + 1;

                    node.data = (Math.abs(node.data - num1 * num1) <
                                 Math.abs(node.data - num2 * num2)) ?
                                 (num1 * num1) : (num2 * num2);
                }

                // If level is even and value is odd,
                // find the closest even perfect square
                if (!((lvl & 1) != 0) && ((x1 & 1) != 0))
                {
                    int num1 = x1 - 1, num2 = x1 + 1;

                    node.data = (Math.abs(node.data - num1 * num1) <
                                 Math.abs(node.data - num2 * num2)) ?
                                 (num1 * num1) : (num2 * num2);
                }
            }

            // Otherwise, find the find
            // the nearest perfect square
            else
            {
                if ((lvl & 1) != 0)
                    node.data = (x1 & 1) != 0 ?
                                (x1 * x1) : (x2 * x2);
                else
                    node.data = (x1 & 1) != 0 ?
                                (x2 * x2) : (x1 * x1);
            }

            // Print front of queue
            // and remove it from queue
            System.out.print(node.data + " ");
            q.poll();

            // Enqueue left child
            if (node.left != null)
                q.add(node.left);

            // Enqueue right child
            if (node.right != null)
                q.add(node.right);
        }

        // Increment the level by 1
        lvl++;
        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{

    // Binary Tree
    Node root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(2);
    root.right.left = new Node(16);
    root.right.right = new Node(19);

    LevelOrderTraversal(root);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque
from math import sqrt, ceil, floor

# Structure of a
# Binary Tree Node
class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# Function to replace all nodes
# at even and odd levels with their
# nearest even or odd perfect squares
def LevelOrderTraversal(root):

    # Base Case
    if (root == None):
        return

    # Create an empty queue
    # for level order traversal
    q = deque()

    # Enqueue root
    q.append(root)

    # Initialize height
    lvl = 1

    # Iterate until queue is not empty
    while (len(q) > 0):

        # Store the size
        # of the queue
        n = len(q)

        # Traverse in range [1, n]
        for i in range(n):

            # Store the current node
            node = q.popleft()

            # Store its square root
            num = sqrt(node.data)
            x1 = floor(num)
            x2 = ceil(num)

            # Check if it is a perfect square
            if (x1 == x2):

                # If level is odd and value is even,
                # find the closest odd perfect square
                if ((lvl & 1) and not (x1 & 1)):
                    num1, num2 = x1 - 1, x1 + 1
                    node.data = (num1 * num1) if (abs(node.data - num1 * num1) < abs(node.data - num2 * num2)) else (num2 * num2)

                # If level is even and value is odd,
                # find the closest even perfect square
                if (not (lvl & 1) and (x1 & 1)):
                    num1,num2 = x1 - 1, x1 + 1
                    node.data = (num1 * num1) if (abs(node.data - num1 * num1) < abs(node.data - num2 * num2)) else (num2 * num2)

            # Otherwise, find the find
            # the nearest perfect square
            else:
                if (lvl & 1):
                    node.data = (x1 * x1) if (x1 & 1) else (x2 * x2)
                else:
                    node.data = (x2 * x2) if (x1 & 1) else (x1 * x1)

            # Prfront of queue
            # and remove it from queue
            print(node.data, end = " ")

            # Enqueue left child
            if (node.left != None):
                q.append(node.left)

            # Enqueue right child
            if (node.right != None):
                q.append(node.right)

        # Increment the level by 1
        lvl += 1
        print()

# Driver Code
if __name__ == '__main__':

    # Binary Tree
    root = Node(5)
    root.left = Node(3)
    root.right = Node(2)
    root.right.left = Node(16)
    root.right.right = Node(19)

    LevelOrderTraversal(root)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Structure of a
// Binary Tree Node
public class Node
{
  public int data;
  public Node left, right;

  public Node(int data)
  {
    this.data = data;
    left = right = null;
  }
}

public class GFG
{

  // Function to replace all nodes
  // at even and odd levels with their
  // nearest even or odd perfect squares
  static void LevelOrderTraversal(Node root)
  {

    // Base Case
    if (root == null)
      return;

    // Create an empty queue
    // for level order traversal
    Queue<Node> q = new Queue<Node>();

    // Enqueue root
    q.Enqueue(root);

    // Initialize height
    int lvl = 1;

    // Iterate until queue is not empty
    while (q.Count != 0)
    {

      // Store the size
      // of the queue
      int n = q.Count;

      // Traverse in range [1, n]
      for(int i = 0; i < n; i++)
      {

        // Store the current node
        Node node = q.Peek();

        // Store its square root
        double num = Math.Sqrt(node.data);
        int x1 = (int)Math.Floor(num);
        int x2 = (int)Math.Ceiling(num);

        // Check if it is a perfect square
        if (x1 == x2)
        {

          // If level is odd and value is even,
          // find the closest odd perfect square
          if (((lvl & 1) != 0) && !((x1 & 1) != 0))
          {
            int num1 = x1 - 1, num2 = x1 + 1;

            node.data = (Math.Abs(node.data - num1 * num1) <
                         Math.Abs(node.data - num2 * num2)) ?
              (num1 * num1) : (num2 * num2);
          }

          // If level is even and value is odd,
          // find the closest even perfect square
          if (!((lvl & 1) != 0) && ((x1 & 1) != 0))
          {
            int num1 = x1 - 1, num2 = x1 + 1;

            node.data = (Math.Abs(node.data - num1 * num1) <
                         Math.Abs(node.data - num2 * num2)) ?
              (num1 * num1) : (num2 * num2);
          }
        }

        // Otherwise, find the find
        // the nearest perfect square
        else
        {
          if ((lvl & 1) != 0)
            node.data = (x1 & 1) != 0 ?
            (x1 * x1) : (x2 * x2);
          else
            node.data = (x1 & 1) != 0 ?
            (x2 * x2) : (x1 * x1);
        }

        // Print front of queue
        // and remove it from queue
        Console.Write(node.data + " ");
        q.Dequeue();

        // Enqueue left child
        if (node.left != null)
          q.Enqueue(node.left);

        // Enqueue right child
        if (node.right != null)
          q.Enqueue(node.right);
      }

      // Increment the level by 1
      lvl++;
      Console.WriteLine();
    }
  }

  // Driver Code
  static public void Main ()
  {

    // Binary Tree
    Node root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(2);
    root.right.left = new Node(16);
    root.right.right = new Node(19);

    LevelOrderTraversal(root);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to replace all nodes
    // at even and odd levels with their
    // nearest even or odd perfect squares
    function LevelOrderTraversal(root)
    {

        // Base Case
        if (root == null)
            return;

        // Create an empty queue
        // for level order traversal
        let q = [];

        // Enqueue root
        q.push(root);

        // Initialize height
        let lvl = 1;

        // Iterate until queue is not empty
        while (q.length != 0)
        {

            // Store the size
            // of the queue
            let n = q.length;

            // Traverse in range [1, n]
            for(let i = 0; i < n; i++)
            {

                // Store the current node
                let node = q[0];

                // Store its square root
                let num = Math.sqrt(node.data);
                let x1 = Math.floor(num);
                let x2 = Math.ceil(num);

                // Check if it is a perfect square
                if (x1 == x2)
                {

                    // If level is odd and value is even,
                    // find the closest odd perfect square
                    if (((lvl & 1) != 0) && !((x1 & 1) != 0))
                    {
                      let num1 = x1 - 1, num2 = x1 + 1;

                      node.data = (Math.abs(node.data - num1 * num1) <
                                   Math.abs(node.data - num2 * num2))?
                                     (num1 * num1) : (num2 * num2);
                    }

                    // If level is even and value is odd,
                    // find the closest even perfect square
                    if (!((lvl & 1) != 0) && ((x1 & 1) != 0))
                    {
                      let num1 = x1 - 1, num2 = x1 + 1;

                      node.data = (Math.abs(node.data - num1 * num1) <
                                  Math.abs(node.data - num2 * num2)) ?
                                     (num1 * num1) : (num2 * num2);
                    }
                }

                // Otherwise, find the find
                // the nearest perfect square
                else
                {
                    if ((lvl & 1) != 0)
                        node.data = (x1 & 1) != 0 ?
                                    (x1 * x1) : (x2 * x2);
                    else
                        node.data = (x1 & 1) != 0 ?
                                    (x2 * x2) : (x1 * x1);
                }

                // Print front of queue
                // and remove it from queue
                document.write(node.data + " ");
                q.shift();

                // Enqueue left child
                if (node.left != null)
                    q.push(node.left);

                // Enqueue right child
                if (node.right != null)
                    q.push(node.right);
            }

            // Increment the level by 1
            lvl++;
            document.write("</br>");
        }
    }

    // Binary Tree
    let root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(2);
    root.right.left = new Node(16);
    root.right.right = new Node(19);

    LevelOrderTraversal(root);

</script>
```

**Output:** 

```
9 
4 4 
9 25
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)