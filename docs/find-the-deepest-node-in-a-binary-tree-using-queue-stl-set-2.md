# 使用队列 STL-SET 2 找到二叉树中最深的节点

> 原文:[https://www . geesforgeks . org/find-二叉树中最深的节点-使用队列-stl-set-2/](https://www.geeksforgeeks.org/find-the-deepest-node-in-a-binary-tree-using-queue-stl-set-2/)

给定一棵二叉树。任务是找到给定二叉树中最深 est 节点的值。

**示例:**

```
Input: Root of below tree
            1
          /   \
         2      3
        / \    / \ 
       4   5  6   7
                   \
                    8
Output: 8

Input: Root of below tree
            1
          /   \
         2      3
               / 
              6  
Output: 6
```

**方法:**我们已经在[这篇](https://www.geeksforgeeks.org/find-deepest-node-binary-tree/)帖子中讨论了寻找二叉树最深节点的两种不同方法。在这里，我们将使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)数据结构找到树中最深的节点。我们将首先把根推入队列，然后在从队列中移除父节点之后，我们将推入它的子节点。我们将继续这个过程，直到队列变空。队列中的最后一个节点是二叉树的最深节点。

下面是上述方法的实现:

## C++

```
// C++ program to find the value of the
// deepest node in a given binary tree.
#include <bits/stdc++.h>
using namespace std;

// A tree node
struct Node
{
    int data;
    struct Node *left , *right;
};

// Utility function to create a new node
Node *newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find the deepest node in a tree
int findDeepest(struct Node* root) {

    struct Node* temp = NULL;

    queue <Node *> q;

    if(root == NULL)
        return 0;

    // Push the root node
    q.push(root);

    while(!q.empty()) {

        temp = q.front();
        q.pop();

        // Push left child
        if(temp->left)
            q.push(temp->left);

        // Push right child
        if(temp->right)
            q.push(temp->right);
    }

    // Return the deepest node's value
    return temp->data;
}

// Driver code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);

    // Function call
    cout << findDeepest(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value of the
// deepest node in a given binary tree.
import java.util.*;

class GFG
{

// A tree node
static class Node
{
    int data;
    Node left , right;
};

// Utility function to create a new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the deepest node in a tree
static int findDeepest(Node root)
{
    Node temp = null;

    Queue <Node> q = new LinkedList<Node>();

    if(root == null)
        return 0;

    // Push the root node
    q.add(root);

    while(!q.isEmpty())
    {
        temp = q.peek();
        q.remove();

        // Push left child
        if(temp.left!=null)
            q.add(temp.left);

        // Push right child
        if(temp.right!=null)
            q.add(temp.right);
    }

    // Return the deepest node's value
    return temp.data;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);

    // Function call
    System.out.println(findDeepest(root));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the value of the
# deepest node in a given binary tree.
from collections import deque

# A tree node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to find the deepest node in a tree
def findDeepest(root: Node) -> int:

    temp = None
    q = deque()

    if (root == None):
        return 0

    # Push the root node
    q.append(root)

    while q:
        temp = q[0]
        q.popleft()

        # Push left child
        if (temp.left):
            q.append(temp.left)

        # Append right child
        if (temp.right):
            q.append(temp.right)

    # Return the deepest node's value
    return temp.data

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.right.left = Node(5)
    root.right.right = Node(6)
    root.right.left.right = Node(7)
    root.right.right.right = Node(8)
    root.right.left.right.left = Node(9)

    # Function call
    print(findDeepest(root))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to find the value of the
// deepest node in a given binary tree.
using System;
using System.Collections.Generic;

class GFG
{

// A tree node
public class Node
{
    public int data;
    public Node left , right;
};

// Utility function to create a new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the deepest node in a tree
static int findDeepest(Node root)
{
    Node temp = null;

    Queue <Node> q = new Queue <Node>();

    if(root == null)
        return 0;

    // Push the root node
    q.Enqueue(root);

    while(q.Count != 0)
    {
        temp = q.Peek();
        q.Dequeue();

        // Push left child
        if(temp.left != null)
            q.Enqueue(temp.left);

        // Push right child
        if(temp.right != null)
            q.Enqueue(temp.right);
    }

    // Return the deepest node's value
    return temp.data;
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);

    // Function call
    Console.WriteLine(findDeepest(root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the value of the
// deepest node in a given binary tree.

// A tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create a new node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the deepest node in a tree
function findDeepest(root)
{
    var temp = null;
    var q = [];

    if (root == null)
        return 0;

    // Push the root node
    q.push(root);

    while (q.length != 0)
    {
        temp = q[0];
        q.shift();

        // Push left child
        if (temp.left != null)
            q.push(temp.left);

        // Push right child
        if (temp.right != null)
            q.push(temp.right);
    }

    // Return the deepest node's value
    return temp.data;
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.right.left = newNode(5);
root.right.right = newNode(6);
root.right.left.right = newNode(7);
root.right.right.right = newNode(8);
root.right.left.right.left = newNode(9);

// Function call
document.write(findDeepest(root));

// This code is contributed by noob2000

</script>
```

**输出:**

```
 9
```

**时间复杂度:** O(N)