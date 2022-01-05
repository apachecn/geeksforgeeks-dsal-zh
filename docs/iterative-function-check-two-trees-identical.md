# 检查两棵树是否相同的迭代函数

> 原文:[https://www . geesforgeks . org/iterative-function-check-two-trees-同文/](https://www.geeksforgeeks.org/iterative-function-check-two-trees-identical/)

当两棵树具有相同的数据并且数据的排列也相同时，它们是相同的。为了确定两棵树是否相同，我们需要同时遍历这两棵树，并且在遍历时，我们需要比较数据和树的子树。
**例:**

```
Input : Roots of below trees
    10           10
  /   \         /
 5     6       5 
Output : false

Input : Roots of below trees
    10            10
  /   \         /   \
 5     6       5     6
Output : true
```

我们在这里讨论了递归解。本文讨论迭代解法。
的想法是用[等级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。我们同时遍历这两个树，并且每当我们出列和从队列中取出项目时比较数据。下面是这个想法的实现。

## C++

```
/* Iterative C++ program to check if two */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Iterative method to find height of Binary Tree
bool areIdentical(Node *root1, Node *root2)
{
    // Return true if both trees are empty
    if (root1==NULL  && root2==NULL) return true;

    // Return false if one is empty and other is not
    if (root1 == NULL) return false;
    if (root2 == NULL) return false;

    // Create an empty queues for simultaneous traversals
    queue<Node *> q1, q2;

    // Enqueue Roots of trees in respective queues
    q1.push(root1);
    q2.push(root2);

    while (!q1.empty() && !q2.empty())
    {
        // Get front nodes and compare them
        Node *n1 = q1.front();
        Node *n2 = q2.front();

        if (n1->data != n2->data)
           return false;

        // Remove front nodes from queues
        q1.pop(), q2.pop();

        /* Enqueue left children of both nodes */
        if (n1->left && n2->left)
        {
            q1.push(n1->left);
            q2.push(n2->left);
        }

        // If one left child is empty and other is not
        else if (n1->left || n2->left)
            return false;

        // Right child code (Similar to left child code)
        if (n1->right && n2->right)
        {
            q1.push(n1->right);
            q2.push(n2->right);
        }
        else if (n1->right || n2->right)
            return false;
    }

    return true;
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    Node *root1 = newNode(1);
    root1->left = newNode(2);
    root1->right = newNode(3);
    root1->left->left = newNode(4);
    root1->left->right = newNode(5);

    Node *root2 = newNode(1);
    root2->left = newNode(2);
    root2->right = newNode(3);
    root2->left->left = newNode(4);
    root2->left->right = newNode(5);

    areIdentical(root1, root2)? cout << "Yes"
                              : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Iterative Java program to check if two */
import java.util.*;
class GfG {

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
}

// Iterative method to find height of Binary Tree
static boolean areIdentical(Node root1, Node root2)
{
    // Return true if both trees are empty
    if (root1 == null && root2 == null)  return true;

    // Return false if one is empty and other is not
    if (root1 == null || root2 == null) return false;

    // Create an empty queues for simultaneous traversals
    Queue<Node > q1 = new LinkedList<Node> ();
    Queue<Node>  q2 = new LinkedList<Node> ();

    // Enqueue Roots of trees in respective queues
    q1.add(root1);
    q2.add(root2);

    while (!q1.isEmpty() && !q2.isEmpty())
    {
        // Get front nodes and compare them
        Node n1 = q1.peek();
        Node n2 = q2.peek();

        if (n1.data != n2.data)
        return false;

        // Remove front nodes from queues
        q1.remove();
        q2.remove();

        /* Enqueue left children of both nodes */
        if (n1.left != null && n2.left != null)
        {
            q1.add(n1.left);
            q2.add(n2.left);
        }

        // If one left child is empty and other is not
        else if (n1.left != null || n2.left != null)
            return false;

        // Right child code (Similar to left child code)
        if (n1.right != null && n2.right != null)
        {
            q1.add(n1.right);
            q2.add(n2.right);
        }
        else if (n1.right != null || n2.right != null)
            return false;
    }

    return true;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver program to test above functions
public static void main(String[] args)
{
    Node root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);

    Node root2 = newNode(1);
    root2.left = newNode(2);
    root2.right = newNode(3);
    root2.left.left = newNode(4);
    root2.left.right = newNode(5);

    if(areIdentical(root1, root2) == true)
    System.out.println("Yes");
    else
    System.out.println("No");
}
}
```

## 蟒蛇 3

```
# Iterative Python3 program to check
# if two trees are identical
from queue import Queue

# Utility function to create a
# new tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Iterative method to find height of
# Binary Tree
def areIdentical(root1, root2):

    # Return true if both trees are empty
    if (root1 and root2):
        return True

    # Return false if one is empty and
    # other is not
    if (root1 or root2):
        return False

    # Create an empty queues for
    # simultaneous traversals
    q1 = Queue()
    q2 = Queue()

    # Enqueue Roots of trees in
    # respective queues
    q1.put(root1)
    q2.put(root2)

    while (not q1.empty() and not q2.empty()):

        # Get front nodes and compare them
        n1 = q1.queue[0]
        n2 = q2.queue[0]

        if (n1.data != n2.data):
            return False

        # Remove front nodes from queues
        q1.get()
        q2.get()

        # Enqueue left children of both nodes
        if (n1.left and n2.left):
            q1.put(n1.left)
            q2.put(n2.left)

        # If one left child is empty and
        # other is not
        elif (n1.left or n2.left):
            return False

        # Right child code (Similar to
        # left child code)
        if (n1.right and n2.right):
            q1.put(n1.right)
            q2.put(n2.right)
        elif (n1.right or n2.right):
            return False

    return True

# Driver Code
if __name__ == '__main__':
    root1 = newNode(1)
    root1.left = newNode(2)
    root1.right = newNode(3)
    root1.left.left = newNode(4)
    root1.left.right = newNode(5)

    root2 = newNode(1)
    root2.left = newNode(2)
    root2.right = newNode(3)
    root2.left.left = newNode(4)
    root2.left.right = newNode(5)

    if areIdentical(root1, root2):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
/* Iterative C# program to check if two */
using System;
using System.Collections.Generic;

class GfG
{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left, right;
}

// Iterative method to find height of Binary Tree
static bool areIdentical(Node root1, Node root2)
{
    // Return true if both trees are empty
    if (root1 == null && root2 == null)
        return true;

    // Return false if one is empty and other is not
    if (root1 == null || root2 == null)
        return false;

    // Create an empty queues for
    // simultaneous traversals
    Queue<Node> q1 = new Queue<Node> ();
    Queue<Node> q2 = new Queue<Node> ();

    // Enqueue Roots of trees in respective queues
    q1.Enqueue(root1);
    q2.Enqueue(root2);

    while (q1.Count != 0 && q2.Count != 0)
    {
        // Get front nodes and compare them
        Node n1 = q1.Peek();
        Node n2 = q2.Peek();

        if (n1.data != n2.data)
        return false;

        // Remove front nodes from queues
        q1.Dequeue();
        q2.Dequeue();

        /* Enqueue left children of both nodes */
        if (n1.left != null && n2.left != null)
        {
            q1.Enqueue(n1.left);
            q2.Enqueue(n2.left);
        }

        // If one left child is empty and other is not
        else if (n1.left != null || n2.left != null)
            return false;

        // Right child code (Similar to left child code)
        if (n1.right != null && n2.right != null)
        {
            q1.Enqueue(n1.right);
            q2.Enqueue(n2.right);
        }
        else if (n1.right != null || n2.right != null)
            return false;
    }

    return true;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void Main(String[] args)
{
    Node root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);

    Node root2 = newNode(1);
    root2.left = newNode(2);
    root2.right = newNode(3);
    root2.left.left = newNode(4);
    root2.left.right = newNode(5);

    if(areIdentical(root1, root2) == true)
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

/* Iterative Javascript program to check if two */

// A Binary Tree Node
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
}

// Iterative method to find height of Binary Tree
function areIdentical(root1, root2)
{
    // Return true if both trees are empty
    if (root1 == null && root2 == null)
        return true;

    // Return false if one is empty and other is not
    if (root1 == null || root2 == null)
        return false;

    // Create an empty queues for
    // simultaneous traversals
    var q1 = [];
    var q2 = [];

    // push Roots of trees in respective queues
    q1.push(root1);
    q2.push(root2);

    while (q1.length != 0 && q2.length != 0)
    {
        // Get front nodes and compare them
        var n1 = q1[0];
        var n2 = q2[0];

        if (n1.data != n2.data)
        return false;

        // Remove front nodes from queues
        q1.shift();
        q2.shift();

        /* push left children of both nodes */
        if (n1.left != null && n2.left != null)
        {
            q1.push(n1.left);
            q2.push(n2.left);
        }

        // If one left child is empty and other is not
        else if (n1.left != null || n2.left != null)
            return false;

        // Right child code (Similar to left child code)
        if (n1.right != null && n2.right != null)
        {
            q1.push(n1.right);
            q2.push(n2.right);
        }
        else if (n1.right != null || n2.right != null)
            return false;
    }

    return true;
}

// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
var root1 = newNode(1);
root1.left = newNode(2);
root1.right = newNode(3);
root1.left.left = newNode(4);
root1.left.right = newNode(5);
var root2 = newNode(1);
root2.left = newNode(2);
root2.right = newNode(3);
root2.left.left = newNode(4);
root2.left.right = newNode(5);
if(areIdentical(root1, root2) == true)
  document.write("Yes");
else
  document.write("No");

</script>
```

**输出:**

```
Yes
```

上述解的时间复杂度为 O(n + m)，其中 m 和 n 是两棵树中的节点数。

本文由**安库尔·莱西亚**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。