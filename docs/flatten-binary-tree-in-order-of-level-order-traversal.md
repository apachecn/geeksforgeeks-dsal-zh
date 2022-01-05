# 按照层级顺序遍历的顺序展平二叉树

> 原文:[https://www . geeksforgeeks . org/flat-二叉树-按级别顺序-顺序-遍历/](https://www.geeksforgeeks.org/flatten-binary-tree-in-order-of-level-order-traversal/)

给定一棵二叉树，任务是按照树的[级遍历顺序](https://www.geeksforgeeks.org/level-order-tree-traversal/)将其展平。在展平的二叉树中，所有节点的左节点必须为空。
**例:**

```
Input: 
          1 
        /   \ 
       5     2 
      / \   / \ 
     6   4 9   3 
Output: 1 5 2 6 4 9 3

Input:
      1
       \
        2
         \
          3
           \
            4
             \
              5
Output: 1 2 3 4 5
```

**方法:**我们将通过模拟二叉树的级别顺序遍历来解决这个问题，如下所示:

1.  创建一个队列来存储二叉树的节点。
2.  创建一个变量“prev”，并通过父节点初始化它。
3.  将父代的左右子代推入队列。
4.  应用级别顺序遍历。假设“curr”是队列中最前面的元素。然后，
    *   如果“curr”为空，则继续。
    *   否则在队列中推送货币->左和货币->右
    *   预测集= curr

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the Binary tree
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

// Function to flatten Binary tree using
// level order traversal
void flatten(node* parent)
{
    // Queue to store nodes
    // for BFS
    queue<node*> q;
    q.push(parent->left);
    q.push(parent->right);
    node* prev = parent;

    // Code for BFS
    while (q.size()) {

        // Size of queue
        int s = q.size();
        while (s--) {

            // Front most node in
            // the queue
            node* curr = q.front();
            q.pop();

            // Base case
            if (curr == NULL)
                continue;
            prev->right = curr;
            prev->left = NULL;
            prev = curr;

            // Pushing new elements
            // in queue
            q.push(curr->left);
            q.push(curr->right);
        }
    }

    prev->left = NULL;
    prev->right = NULL;
}

// Function to print flattened
// Binary Tree
void print(node* parent)
{
    node* curr = parent;
    while (curr != NULL)
        cout << curr->data << " ", curr = curr->right;
}

// Driver code
int main()
{
    node* root = new node(1);
    root->left = new node(5);
    root->right = new node(2);
    root->left->left = new node(6);
    root->left->right = new node(4);
    root->right->left = new node(9);
    root->right->right = new node(3);

    // Calling required functions
    flatten(root);
    print(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Node of the Binary tree
static class node
{
    int data;
    node left;
    node right;
    node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};

// Function to flatten Binary tree using
// level order traversal
static void flatten(node parent)
{
    // Queue to store nodes
    // for BFS
    Queue<node> q = new LinkedList<>();
    q.add(parent.left);
    q.add(parent.right);
    node prev = parent;

    // Code for BFS
    while (q.size() > 0)
    {

        // Size of queue
        int s = q.size();
        while (s-- > 0)
        {

            // Front most node in
            // the queue
            node curr = q.peek();
            q.remove();

            // Base case
            if (curr == null)
                continue;
            prev.right = curr;
            prev.left = null;
            prev = curr;

            // Pushing new elements
            // in queue
            q.add(curr.left);
            q.add(curr.right);
        }
    }
    prev.left = null;
    prev.right = null;
}

// Function to print flattened
// Binary Tree
static void print(node parent)
{
    node curr = parent;
    while (curr != null)
    {
        System.out.print(curr.data + " ");
        curr = curr.right;
    }
}

// Driver code
public static void main(String[] args)
{
    node root = new node(1);
    root.left = new node(5);
    root.right = new node(2);
    root.left.left = new node(6);
    root.left.right = new node(4);
    root.right.left = new node(9);
    root.right.right = new node(3);

    // Calling required functions
    flatten(root);
    print(root);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of above algorithm

# Utility class to create a node
class node:
    def __init__(self, key):
        self.data = key
        self.left = self.right = None

# Function to flatten Binary tree using
# level order traversal
def flatten( parent):

    # Queue to store nodes
    # for BFS
    q = []
    q.append(parent.left)
    q.append(parent.right)
    prev = parent

    # Code for BFS
    while (len(q) > 0) :

        # Size of queue
        s = len(q)
        while (s > 0) :
            s = s - 1

            # Front most node in
            # the queue
            curr = q[0]
            q.pop(0)

            # Base case
            if (curr == None):
                continue
            prev.right = curr
            prev.left = None
            prev = curr

            # appending elements
            # in queue
            q.append(curr.left)
            q.append(curr.right)

    prev.left = None
    prev.right = None

# Function to print flattened
# Binary Tree
def print_(parent):

    curr = parent
    while (curr != None):
        print( curr.data , end=" ")
        curr = curr.right

# Driver code
root = node(1)
root.left = node(5)
root.right = node(2)
root.left.left = node(6)
root.left.right = node(4)
root.right.left = node(9)
root.right.right = node(3)

# Calling required functions
flatten(root)
print_(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Node of the Binary tree
public class node
{
    public int data;
    public node left;
    public node right;
    public node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};

// Function to flatten Binary tree using
// level order traversal
static void flatten(node parent)
{
    // Queue to store nodes
    // for BFS
    Queue<node> q = new Queue<node>();
    q.Enqueue(parent.left);
    q.Enqueue(parent.right);
    node prev = parent;

    // Code for BFS
    while (q.Count > 0)
    {

        // Size of queue
        int s = q.Count;
        while (s-- > 0)
        {

            // Front most node in
            // the queue
            node curr = q.Peek();
            q.Dequeue();

            // Base case
            if (curr == null)
                continue;
            prev.right = curr;
            prev.left = null;
            prev = curr;

            // Pushing new elements
            // in queue
            q.Enqueue(curr.left);
            q.Enqueue(curr.right);
        }
    }
    prev.left = null;
    prev.right = null;
}

// Function to print flattened
// Binary Tree
static void print(node parent)
{
    node curr = parent;
    while (curr != null)
    {
        Console.Write(curr.data + " ");
        curr = curr.right;
    }
}

// Driver code
public static void Main(String[] args)
{
    node root = new node(1);
    root.left = new node(5);
    root.right = new node(2);
    root.left.left = new node(6);
    root.left.right = new node(4);
    root.right.left = new node(9);
    root.right.right = new node(3);

    // Calling required functions
    flatten(root);
    print(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Node of the Binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Function to flatten Binary tree using
// level order traversal
function flatten(parent)
{
    // Queue to store nodes
    // for BFS
    let q = [];
    q.push(parent.left);
    q.push(parent.right);
    let prev = parent;

    // Code for BFS
    while (q.length > 0)
    {

        // Size of queue
        let s = q.length;
        while (s-- > 0)
        {

            // Front most node in
            // the queue
            let curr = q.shift();

            // Base case
            if (curr == null)
                continue;
            prev.right = curr;
            prev.left = null;
            prev = curr;

            // Pushing new elements
            // in queue
            q.push(curr.left);
            q.push(curr.right);
        }
    }
    prev.left = null;
    prev.right = null;
}

// Function to print flattened
// Binary Tree
function print(parent)
{
    let curr = parent;
    while (curr != null)
    {
        document.write(curr.data + " ");
        curr = curr.right;
    }
}

// Driver code
let root = new node(1);
root.left = new node(5);
root.right = new node(2);
root.left.left = new node(6);
root.left.right = new node(4);
root.right.left = new node(9);
root.right.right = new node(3);

// Calling required functions
flatten(root);
print(root);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
1 5 2 6 4 9 3 
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N)其中 N 是二叉树的大小。