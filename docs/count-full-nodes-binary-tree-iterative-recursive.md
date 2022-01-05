# 计算二叉树中的完整节点数(迭代和递归)

> 原文:[https://www . geesforgeks . org/count-full-nodes-二叉树-迭代-递归/](https://www.geeksforgeeks.org/count-full-nodes-binary-tree-iterative-recursive/)

给定一棵二叉树，在不使用递归和使用递归的情况下，如何计算所有完整的节点(两个子节点都不为空的节点)？请注意，不能触摸树叶，因为它们的两个子代都为空。

![](img/30e1318aa63d5d7584fc7931b6c2d5d8.png)

节点 2 和 6 是完整节点，都有子节点。所以上面树中的完整节点数是 2

**方法:迭代**
思路是利用层次顺序遍历高效解决这个问题。

```
1) Create an empty Queue Node and push root node to Queue.
2) Do following while nodeQeue is not empty.
   a) Pop an item from Queue and process it.
      a.1) If it is full node then increment count++.
   b) Push left child of popped item to Queue, if available.
   c) Push right child of popped item to Queue, if available.
```

下面是这个想法的实现。

## C++

```
// C++ program to count
// full nodes in a Binary Tree
#include <bits/stdc++.h>
using namespace std;

// A binary tree Node has data, pointer to left
// child and a pointer to right child
struct Node
{
    int data;
    struct Node* left, *right;
};

// Function to get the count of full Nodes in
// a binary tree
unsigned int getfullCount(struct Node* node)
{
    // If tree is empty
    if (!node)
        return 0;
    queue<Node *> q;

    // Do level order traversal starting from root
    int count = 0; // Initialize count of full nodes
    q.push(node);
    while (!q.empty())
    {
        struct Node *temp = q.front();
        q.pop();

        if (temp->left && temp->right)
            count++;

        if (temp->left != NULL)
            q.push(temp->left);
        if (temp->right != NULL)
            q.push(temp->right);
    }
    return count;
}

/* Helper function that allocates a new Node with the
given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver program
int main(void)
{
    /* 2
     / \
    7     5
    \     \
     6     9
    / \ /
    1 11 4
    Let us create Binary Tree as shown
    */

    struct Node *root = newNode(2);
    root->left     = newNode(7);
    root->right     = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(11);
    root->right->right = newNode(9);
    root->right->right->left = newNode(4);

    cout << getfullCount(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// full nodes in a Binary Tree
// using Iterative approach
import java.util.Queue;
import java.util.LinkedList;

// Class to represent Tree node
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to count full nodes of Tree
class BinaryTree
{

    Node root;

    /* Function to get the count of full Nodes in
    a binary tree*/
    int getfullCount()
    {
        // If tree is empty
        if (root==null)
        return 0;

        // Initialize empty queue.
        Queue<Node> queue = new LinkedList<Node>();

        // Do level order traversal starting from root
        queue.add(root);

        int count=0; // Initialize count of full nodes
        while (!queue.isEmpty())
        {

            Node temp = queue.poll();
            if (temp.left!=null && temp.right!=null)
            count++;

            // Enqueue left child
            if (temp.left != null)
            {
                queue.add(temp.left);
            }

            // Enqueue right child
            if (temp.right != null)
            {
                queue.add(temp.right);
            }
        }
        return count;
    }

    public static void main(String args[])
    {
        /* 2
          / \
        7     5
        \     \
        6     9
        / \ /
        1 11 4
        Let us create Binary Tree as shown
        */
        BinaryTree tree_level = new BinaryTree();
        tree_level.root = new Node(2);
        tree_level.root.left = new Node(7);
        tree_level.root.right = new Node(5);
        tree_level.root.left.right = new Node(6);
        tree_level.root.left.right.left = new Node(1);
        tree_level.root.left.right.right = new Node(11);
        tree_level.root.right.right = new Node(9);
        tree_level.root.right.right.left = new Node(4);

        System.out.println(tree_level.getfullCount());

    }
}
```

## 计算机编程语言

```
# Python program to count
# full nodes in a Binary Tree
# using iterative approach

# A node structure
class Node:
    # A utility function to create a new node
    def __init__(self ,key):
        self.data = key
        self.left = None
        self.right = None

# Iterative Method to count full nodes of binary tree
def getfullCount(root):
    # Base Case
    if root is None:
        return 0

    # Create an empty queue for level order traversal
    queue = []

    # Enqueue Root and initialize count
    queue.append(root)

    count = 0 #initialize count for full nodes
    while(len(queue) > 0):
        node = queue.pop(0)

        # if it is full node then increment count
        if node.left is not None and node.right is not None:
            count = count+1

        # Enqueue left child
        if node.left is not None:
            queue.append(node.left)

        # Enqueue right child
        if node.right is not None:
            queue.append(node.right)

    return count

# Driver Program to test above function
root = Node(2)
root.left = Node(7)
root.right = Node(5)
root.left.right = Node(6)
root.left.right.left = Node(1)
root.left.right.right = Node(11)
root.right.right = Node(9)
root.right.right.left = Node(4)

print "%d" %(getfullCount(root))
```

## C#

```
// C# program to count
// full nodes in a Binary Tree
// using Iterative approach
using System;
using System.Collections.Generic;

// Class to represent Tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to count full nodes of Tree
public class BinaryTree
{

    Node root;

    /* Function to get the count of full Nodes in
    a binary tree*/
    int getfullCount()
    {
        // If tree is empty
        if (root == null)
        return 0;

        // Initialize empty queue.
        Queue<Node> queue = new Queue<Node>();

        // Do level order traversal starting from root
        queue.Enqueue(root);

        int count = 0; // Initialize count of full nodes
        while (queue.Count != 0)
        {

            Node temp = queue.Dequeue();
            if (temp.left != null && temp.right != null)
            count++;

            // Enqueue left child
            if (temp.left != null)
            {
                queue.Enqueue(temp.left);
            }

            // Enqueue right child
            if (temp.right != null)
            {
                queue.Enqueue(temp.right);
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String []args)
    {
        /* 2
        / \
        7 5
        \ \
        6 9
        / \ /
        1 11 4
        Let us create Binary Tree as shown
        */
        BinaryTree tree_level = new BinaryTree();
        tree_level.root = new Node(2);
        tree_level.root.left = new Node(7);
        tree_level.root.right = new Node(5);
        tree_level.root.left.right = new Node(6);
        tree_level.root.left.right.left = new Node(1);
        tree_level.root.left.right.right = new Node(11);
        tree_level.root.right.right = new Node(9);
        tree_level.root.right.right.left = new Node(4);

        Console.WriteLine(tree_level.getfullCount());
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count
// full nodes in a Binary Tree
// using Iterative approach

// Class to represent Tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}
let root;

// Function to get the count of full
// Nodes in a binary tree
function getfullCount()
{

    // If tree is empty
    if (root == null)
        return 0;

    // Initialize empty queue.
    let queue = [];

    // Do level order traversal starting from root
    queue.push(root);

    // Initialize count of full nodes
    let count = 0;

    while (queue.length != 0)
    {
        let temp = queue.shift();
        if (temp.left != null && temp.right != null)
            count++;

        // Enqueue left child
        if (temp.left != null)
        {
            queue.push(temp.left);
        }

        // Enqueue right child
        if (temp.right != null)
        {
            queue.push(temp.right);
        }
    }
    return count;
}

// Driver code
/* 2
  / \
7     5
\     \
 6     9
/ \  /
1 11 4
Let us create Binary Tree as shown
*/
root = new Node(2);
root.left = new Node(7);
root.right = new Node(5);
root.left.right = new Node(6);
root.left.right.left = new Node(1);
root.left.right.right = new Node(11);
root.right.right = new Node(9);
root.right.right.left = new Node(4);

document.write(getfullCount());

// This code is contributed by rag2127

</script>
```

**输出:**

```
 2
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)其中，n 是给定二叉树中的节点数

**方法:递归**
思路是按后序遍历树。如果当前节点已满，我们将结果增加 1，并将左右子树的返回值相加。

## C++

```
// C++ program to count full nodes in a Binary Tree
#include <bits/stdc++.h>
using namespace std;

// A binary tree Node has data, pointer to left
// child and a pointer to right child
struct Node
{
    int data;
    struct Node* left, *right;
};

// Function to get the count of full Nodes in
// a binary tree
unsigned int getfullCount(struct Node* root)
{
    if (root == NULL)
       return 0;

    int res = 0;
    if  (root->left && root->right)
       res++;

    res += (getfullCount(root->left) +
            getfullCount(root->right));
    return res;
}

/* Helper function that allocates a new
   Node with the given data and NULL left
   and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver program
int main(void)
{
    /* 2
     / \
    7    5
    \    \
     6   9
    / \ /
    1 11 4
    Let us create Binary Tree as shown
    */

    struct Node *root = newNode(2);
    root->left    = newNode(7);
    root->right   = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(11);
    root->right->right = newNode(9);
    root->right->right->left = newNode(4);

    cout << getfullCount(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count full nodes in a Binary Tree
import java.util.*;
class GfG {

// A binary tree Node has data, pointer to left
// child and a pointer to right child
static class Node
{
    int data;
    Node left, right;
}

// Function to get the count of full Nodes in
// a binary tree
static int getfullCount(Node root)
{
    if (root == null)
    return 0;

    int res = 0;
    if (root.left != null && root.right != null)
    res++;

    res += (getfullCount(root.left) + getfullCount(root.right));
    return res;
}

/* Helper function that allocates a new
Node with the given data and NULL left
and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver program
public static void main(String[] args)
{
    /* 2
    / \
    7 5
    \ \
    6 9
    / \ /
    1 11 4
    Let us create Binary Tree as shown
    */

    Node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    System.out.println(getfullCount(root));

}
}
```

## 蟒蛇 3

```
# Python program to count full
# nodes in a Binary Tree
class newNode():

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get the count of 
# full Nodes in a binary tree
def getfullCount(root):

    if (root == None):
        return 0

    res = 0
    if (root.left and root.right):
        res += 1

    res += (getfullCount(root.left) +
            getfullCount(root.right))
    return res

# Driver code
if __name__ == '__main__':
    """ 2
    / \
    7 5
    \ \
    6 9
    / \ /
    1 11 4
    Let us create Binary Tree as shown
    """

    root = newNode(2)
    root.left = newNode(7)
    root.right = newNode(5)
    root.left.right = newNode(6)
    root.left.right.left = newNode(1)
    root.left.right.right = newNode(11)
    root.right.right = newNode(9)
    root.right.right.left = newNode(4)

    print(getfullCount(root))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to count full nodes in a Binary Tree
using System;

class GfG
{

// A binary tree Node has data, pointer to left
// child and a pointer to right child
public class Node
{
    public int data;
    public Node left, right;
}

// Function to get the count of full Nodes in
// a binary tree
static int getfullCount(Node root)
{
    if (root == null)
    return 0;

    int res = 0;
    if (root.left != null && root.right != null)
    res++;

    res += (getfullCount(root.left) + getfullCount(root.right));
    return res;
}

/* Helper function that allocates a new
Node with the given data and NULL left
and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver program
public static void Main()
{
    /* 2
    / \
    7 5
    \ \
    6 9
    / \ /
    1 11 4
    Let us create Binary Tree as shown
    */

    Node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    Console.WriteLine(getfullCount(root));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to count full nodes in a Binary Tree

// A binary tree Node has data, pointer to left
// child and a pointer to right child
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

// Function to get the count of full Nodes in
// a binary tree
function getfullCount(root)
{
    if (root == null)
    return 0;

    var res = 0;
    if (root.left != null && root.right != null)
    res++;

    res += (getfullCount(root.left) + getfullCount(root.right));
    return res;
}

/* Helper function that allocates a new
Node with the given data and NULL left
and right pointers. */
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver program
/* 2
/ \
7 5
\ \
6 9
/ \ /
1 11 4
Let us create Binary Tree as shown
*/
var root = newNode(2);
root.left = newNode(7);
root.right = newNode(5);
root.left.right = newNode(6);
root.left.right.left = newNode(1);
root.left.right.right = newNode(11);
root.right.right = newNode(9);
root.right.right.left = newNode(4);
document.write(getfullCount(root));

</script>
```

**输出:**

```
 2
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

其中，n 是给定二叉树中的节点数

**类似文章:**

*   [计算二叉树中的半个节点(迭代和递归)](https://www.geeksforgeeks.org/count-half-nodes-in-a-binary-tree-iterative-and-recursive/)
*   [程序获取二叉树叶节点数](https://www.geeksforgeeks.org/write-a-c-program-to-get-count-of-leaf-nodes-in-a-binary-tree/)
*   [给定一棵二叉树，如何去掉所有的半节点？](https://www.geeksforgeeks.org/given-a-binary-tree-how-do-you-remove-all-the-half-nodes/)
*   [打印二叉树中的所有完整节点](https://www.geeksforgeeks.org/print-full-nodes-binary-tree/)

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。