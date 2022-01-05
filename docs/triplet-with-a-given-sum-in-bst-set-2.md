# BST 中给定和的三元组|集合 2

> 原文:[https://www . geeksforgeeks . org/带有给定 bst-set-2 的三元组/](https://www.geeksforgeeks.org/triplet-with-a-given-sum-in-bst-set-2/)

给定一个二叉查找树和一个整数 **X** ，任务是找出是否存在和 **X** 的三元组。对应打印**是**或**否**。**注意**三个节点不一定是截然不同的。

**示例:**

```
Input: X = 15
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
Output: Yes
{5, 5, 5} is one such triplet.
{3, 5, 7}, {2, 5, 8}, {4, 5, 6} are some others.

Input: X = 16
      1
       \
        2
         \
          3
           \
            4
             \
              5
Output: No
```

**简单方法:**一个简单的方法是将 BST 转换成一个排序的数组，然后使用三个指针找到三元组。这将占用 O(N)个额外空间，其中 N 是二叉查找树中存在的节点数。我们已经在这篇[文章](https://www.geeksforgeeks.org/check-if-a-triplet-with-given-sum-exists-in-bst/)中讨论了一个类似的问题，它占用了 O(N)个额外空间。

**更好的方法:**我们将使用一种空间高效的方法来解决这个问题，方法是将额外的空间复杂度降低到 O(H)，其中 H 是 BST 的高度。为此，我们将在 BST 上使用两个指针技术。
我们将逐一遍历树的所有节点，对于每个节点，我们将尝试找到总和等于(X–curr->data)的一对，其中“curr”是我们正在遍历的 BST 的当前节点。
我们将使用类似于在这篇[文章](https://www.geeksforgeeks.org/pair-with-a-given-sum-in-bst-set-2/)中讨论的技术来寻找一对。

**算法:**逐个遍历 BST 的每个节点，对于每个节点:

1.  为 BST 创建一个向前和向后的迭代器。假设它们所指向的节点的值是 v1 和 v2。
2.  现在在每一步，
    *   如果 v1 + v2 = X，我们找到了一对，因此我们将把计数增加 1。
    *   如果 v1 + v2 小于或等于 x，我们将使前向迭代器指向下一个元素。
    *   如果 v1 + v2 大于 x，我们将使向后迭代器指向前一个元素。
3.  当左边的迭代器没有指向值大于右边节点的节点时，我们将继续上面的操作。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function that returns true if a pair exists
// in the binary search tree with sum equal to x
bool existsPair(node* root, int x)
{
    // Iterators for BST
    stack<node *> it1, it2;

    // Initializing forward iterator
    node* c = root;
    while (c != NULL)
        it1.push(c), c = c->left;

    // Initializing backward iterator
    c = root;
    while (c != NULL)
        it2.push(c), c = c->right;

    // Two pointer technique
    while (it1.size() and it2.size()) {

        // Variables to store values at
        // it1 and it2
        int v1 = it1.top()->data, v2 = it2.top()->data;

        // Base case
        if (v1 + v2 == x)
            return 1;

        if (v1 > v2)
            break;

        // Moving forward pointer
        if (v1 + v2 < x) {
            c = it1.top()->right;
            it1.pop();
            while (c != NULL)
                it1.push(c), c = c->left;
        }
        // Moving backward pointer
        else {
            c = it2.top()->left;
            it2.pop();
            while (c != NULL)
                it2.push(c), c = c->right;
        }
    }

    // Case when no pair is found
    return 0;
}

// Function that returns true if a triplet exists
// in the binary search tree with sum equal to x
bool existsTriplet(node* root, node* curr, int x)
{
    // If current node is NULL
    if (curr == NULL)
        return 0;

    // Conditions for existence of a triplet
    return (existsPair(root, x - curr->data)
            || existsTriplet(root, curr->left, x)
            || existsTriplet(root, curr->right, x));
}

// Driver code
int main()
{
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    int x = 24;

    if (existsTriplet(root, root, x))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

// Node of the binary tree
class Node
{
  int data;
  Node left, right;  
  Node(int item)
  {
    data = item;
    left = right = null;
  }
}

class GFG
{
  static Node root;

  // Function that returns true if a pair exists
  // in the binary search tree with sum equal to x
  static boolean existsPair(Node root, int x)
  {

    // Iterators for BST
    Stack<Node> it1 = new Stack<Node>();
    Stack<Node> it2 = new Stack<Node>();

    // Initializing forward iterator
    Node c = root;
    while (c != null)
    {
      it1.push(c);
      c = c.left;
    }

    // Initializing backward iterator
    c = root;
    while (c != null)
    {
      it2.push(c);
      c = c.right;
    }

    // Two pointer technique
    while (it1.size() > 0 && it2.size() > 0)
    {

      // Variables to store values at
      // it1 and it2
      int v1 = it1.peek().data;
      int v2 = it2.peek().data;

      // Base case
      if (v1 + v2 == x)
      {
        return true;
      }
      if (v1 > v2)
      {
        break;
      }

      // Moving forward pointer
      if (v1 + v2 < x)
      {
        c = it1.peek().right;
        it1.pop();
        while (c != null)
        {
          it1.push(c);
          c = c.left;
        }
      }

      // Moving backward pointer
      else
      {
        c = it2.peek().left;
        it2.pop();
        while(c != null)
        {
          it2.push(c);
          c = c.right;
        }
      }
    }

    // Case when no pair is found
    return false;
  }

  // Function that returns true if a triplet exists
  // in the binary search tree with sum equal to x
  static boolean existsTriplet(Node root,
                               Node curr, int x )
  {

    // If current node is NULL
    if(curr == null)
    {
      return false;
    }

    // Conditions for existence of a triplet
    return (existsPair(root, x - curr.data) ||
            existsTriplet(root, curr.left, x) ||
            existsTriplet(root, curr.right, x));
  }

  // Driver code
  public static void main (String[] args)
  {
    GFG  tree = new GFG();
    tree.root = new Node(5);
    tree.root.left = new Node(3);
    tree.root.right = new Node(7);
    tree.root.left.left = new Node(2);
    tree.root.left.right = new Node(4);
    tree.root.right.left = new Node(6);
    tree.root.right.right = new Node(8);
    int x = 24;
    if (existsTriplet(root, root, x))
    {
      System.out.println("Yes");
    }
    else
    {
      System.out.println("No");
    }   
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# Function that returns true if a pair exists
# in the binary search tree with sum equal to x
def existsPair(root, x):

    # Iterators for BST
    it1, it2 = [], []

    # Initializing forward iterator
    c = root
    while (c != None):
        it1.append(c)
        c = c.left

    # Initializing backward iterator
    c = root
    while (c != None):
        it2.append(c)
        c = c.right

    # Two pointer technique
    while (len(it1) > 0 and len(it2) > 0):

        # Variables to store values at
        # it1 and it2
        v1 = it1[-1].data
        v2 = it2[-1].data

        # Base case
        if (v1 + v2 == x):
            return 1

        if (v1 > v2):
            break

        # Moving forward pointer
        if (v1 + v2 < x):
            c = it1[-1].right
            del it1[-1]
            while (c != None):
                it1.append(c)
                c = c.left

        # Moving backward pointer
        else:
            c = it2[-1].left
            del it2[-1]
            while (c != None):
                it2.append(c)
                c = c.right

    # Case when no pair is found
    return 0

# Function that returns true if a triplet exists
# in the binary search tree with sum equal to x
def existsTriplet(root, curr, x):

    # If current node is NULL
    if (curr == None):
        return 0

    # Conditions for existence of a triplet
    return (existsPair(root, x - curr.data)
            or existsTriplet(root, curr.left, x)
            or existsTriplet(root, curr.right, x))

# Driver code
if __name__ == '__main__':

    root = Node(5)
    root.left = Node(3)
    root.right = Node(7)
    root.left.left = Node(2)
    root.left.right = Node(4)
    root.right.left = Node(6)
    root.right.right = Node(8)

    x = 24

    if (existsTriplet(root, root, x)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

// Node of the binary tree
class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG{

static Node root;

// Function that returns true if a pair exists
// in the binary search tree with sum equal to x
static bool existsPair(Node root, int x)
{

    // Iterators for BST
    Stack<Node> it1 = new Stack<Node>();
    Stack<Node> it2 = new Stack<Node>();

    // Initializing forward iterator
    Node c = root;

    while (c != null)
    {
        it1.Push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root;

    while (c != null)
    {
        it2.Push(c);
        c = c.right;
    }

    // Two pointer technique
    while (it1.Count > 0 && it2.Count > 0)
    {

        // Variables to store values at
        // it1 and it2
        int v1 = it1.Peek().data;
        int v2 = it2.Peek().data;

        // Base case
        if (v1 + v2 == x)
        {
            return true;
        }
        if (v1 > v2)
        {
            break;
        }

        // Moving forward pointer
        if (v1 + v2 < x)
        {
            c = it1.Peek().right;
            it1.Pop();

            while (c != null)
            {
                it1.Push(c);
                c = c.left;
            }
        }

        // Moving backward pointer
        else
        {
            c = it2.Peek().left;
            it2.Pop();

            while(c != null)
            {
                it2.Push(c);
                c = c.right;
            }
        }
    }

    // Case when no pair is found
    return false;
}

// Function that returns true if a triplet exists
// in the binary search tree with sum equal to x
static bool existsTriplet(Node root, Node curr, int x)
{

    // If current node is NULL
    if (curr == null)
    {
        return false;
    }

    // Conditions for existence of a triplet
    return (existsPair(root, x - curr.data) ||
          existsTriplet(root, curr.left, x) ||
          existsTriplet(root, curr.right, x));
}

// Driver code
static public void Main()
{
    GFG.root = new Node(5);
    GFG.root.left = new Node(3);
    GFG.root.right = new Node(7);
    GFG.root.left.left = new Node(2);
    GFG.root.left.right = new Node(4);
    GFG.root.right.left = new Node(6);
    GFG.root.right.right = new Node(8);

    int x = 24;

    if (existsTriplet(root, root, x))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of the binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Function to find a pair with given sum
function existsPair(root, x)
{

    // Iterators for BST
    let it1 = [], it2 = [];

    // Initializing forward iterator
    let c = root;
    while (c != null)
    {
        it1.push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root;
    while (c != null)
    {
        it2.push(c);
        c = c.right;
    }

    // Two pointer technique
    while (it1.length > 0 && it2.length > 0)
    {

        // Variables to store values at
        // it1 and it2
        let v1 = it1[it1.length - 1].data,
            v2 = it2[it2.length - 1].data;

        // Base case
        if (v1 + v2 == x)
            return true;

        if (v1 > v2)
        {
            break;
        }

        // Moving forward pointer
        if (v1 + v2 < x)
        {
            c = it1[it1.length - 1].right;
            it1.pop();
            while (c != null)
            {
                it1.push(c);
                c = c.left;
            }
        }

        // Moving backward pointer
        else
        {
            c = it2[it2.length - 1].left;
            it2.pop();

            while (c != null)
            {
                it2.push(c);
                c = c.right;
            }
        }
    }

    // Case when no pair is found
    return false;
}

// Function that returns true if a
// triplet exists in the binary
// search tree with sum equal to x
function existsTriplet(root, curr, x)
{

    // If current node is NULL
    if (curr == null)
    {
      return false;
    }

    // Conditions for existence of a triplet
    return (existsPair(root, x - curr.data) ||
            existsTriplet(root, curr.left, x) ||
            existsTriplet(root, curr.right, x));
}

// Driver code
let root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

let x = 24;

// Calling required function
if (existsTriplet(root, root, x))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N<sup>2</sup>)
T5】空间复杂度: O(H)