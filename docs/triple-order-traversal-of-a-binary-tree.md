# 二叉树的三阶遍历

> 原文:[https://www . geesforgeks . org/二叉树的三阶遍历/](https://www.geeksforgeeks.org/triple-order-traversal-of-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到它的**三阶遍历**。

> **三阶遍历**是一种树遍历技术，其中每个节点按照以下顺序遍历三次:
> 
> *   访问根节点
> *   遍历左边的子树
> *   访问根节点
> *   遍历右子树
> *   访问根节点。

**示例:**

```
Input:
            A
           / \
          B   C
         / \   \
        F   D   E

Output: A B F F F B D D D B A C C E E E C A

Input:
            A
           / \
          B   C
         / \   
        E   D   
       /
      F
Output: A B E F F F E E B D D D B A C C C A 
```

**方法:**
按照以下步骤解决问题:

*   从**根**开始遍历。
*   如果**当前节点**不存在，只需从中返回即可。
*   否则:
    *   打印**当前节点**的值。
    *   递归遍历**左子树**。
    *   再次打印**当前节点**。
    *   递归遍历**右子树**。
    *   再次打印**当前节点**。
*   重复以上步骤，直到访问了树中的所有节点。

下面是上述方法的实现:

## C++

```
// C++ Program to implement triple
// order traversal of a binary tree
#include <iostream>
using namespace std;

// Structure of a Node
struct node {
    char data;
    struct node *left, *right;
};

// Function to create new node
struct node* newNode(char ch)
{
    // Allocating a new node in the memory.
    struct node* Node = new node();
    Node->data = ch;
    Node->left = NULL;
    Node->right = NULL;
    return Node;
}

// Function to print Triple Order traversal
void tripleOrderTraversal(struct node* root)
{
    if (root) {

        // Print the current node
        cout << root->data << " ";

        // Traverse left subtree
        tripleOrderTraversal(root->left);

        // Print the current node
        cout << root->data << " ";

        // Traverse right subtree
        tripleOrderTraversal(root->right);

        // Print the current node
        cout << root->data << " ";
    }
}

// Driver Code
int main()
{
    struct node* root = newNode('A');
    root->left = newNode('B');
    root->right = newNode('C');
    root->left->left = newNode('F');
    root->left->right = newNode('D');
    root->right->right = newNode('E');

    tripleOrderTraversal(root);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement triple
// order traversal of a binary tree
import java.util.*;

class GFG{

// Structure of a Node
static class node
{
    char data;
    node left, right;
};

// Function to create new node
static node newNode(char ch)
{

    // Allocating a new node in the memory.
    node n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Triple Order traversal
static void tripleOrderTraversal(node root)
{
    if (root != null)
    {

        // Print the current node
        System.out.print(root.data + " ");

        // Traverse left subtree
        tripleOrderTraversal(root.left);

        // Print the current node
        System.out.print(root.data + " ");

        // Traverse right subtree
        tripleOrderTraversal(root.right);

        // Print the current node
        System.out.print(root.data + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    node root = newNode('A');
    root.left = newNode('B');
    root.right = newNode('C');
    root.left.left = newNode('F');
    root.left.right = newNode('D');
    root.right.right = newNode('E');

    tripleOrderTraversal(root);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement triple
# order traversal of a binary tree

# Structure of node
class Node:

    # Initialise the node
    def __init__(self, ch):

        self.data = ch
        self.left = None
        self.right = None

# Function to print the Triple Order Traversal
def tripleOrderTraversal(root):

    if root:

        # Print the current node
        print(root.data, end = ' ')

        # Print the left subtree
        tripleOrderTraversal(root.left)

        # Print the current node
        print(root.data, end = ' ')

        # Print the right subtree
        tripleOrderTraversal(root.right)

        # Print the current node
        print(root.data, end = ' ')

# Driver code
root = Node('A')
root.left = Node('B')
root.right = Node('C')
root.left.left = Node('F')
root.left.right = Node('D')
root.right.right = Node('E')

tripleOrderTraversal(root)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to implement triple
// order traversal of a binary tree
using System;

class GFG{

// Structure of a Node
public class node
{
    public char data;
    public node left, right;
};

// Function to create new node
static node newNode(char ch)
{

    // Allocating a new node in the memory.
    node n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Triple Order traversal
static void tripleOrderTraversal(node root)
{
    if (root != null)
    {

        // Print the current node
        Console.Write(root.data + " ");

        // Traverse left subtree
        tripleOrderTraversal(root.left);

        // Print the current node
        Console.Write(root.data + " ");

        // Traverse right subtree
        tripleOrderTraversal(root.right);

        // Print the current node
        Console.Write(root.data + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    node root = newNode('A');
    root.left = newNode('B');
    root.right = newNode('C');
    root.left.left = newNode('F');
    root.left.right = newNode('D');
    root.right.right = newNode('E');

    tripleOrderTraversal(root);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// javascript Program to implement triple
// order traversal of a binary tree

// Structure of a Node
class node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to create new node
function newNode(ch)
{
    // Allocating a new node in the memory.
    var n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Triple Order traversal
function tripleOrderTraversal(root)
{
    if (root) {

        // Print the current node
        document.write( root.data + " ");

        // Traverse left subtree
        tripleOrderTraversal(root.left);

        // Print the current node
        document.write( root.data + " ");

        // Traverse right subtree
        tripleOrderTraversal(root.right);

        // Print the current node
        document.write( root.data + " ");
    }
}

// Driver Code
var root = newNode('A');
root.left = newNode('B');
root.right = newNode('C');
root.left.left = newNode('F');
root.left.right = newNode('D');
root.right.right = newNode('E');
tripleOrderTraversal(root);

</script>
```

**Output:** 

```
A B F F F B D D D B A C C E E E C A
```

***时间复杂度:** O(N)，*其中 N 是二叉树中的节点总数。
***辅助空间:** O(N)*
**应用:** [欧拉一树之旅](https://www.geeksforgeeks.org/euler-tour-tree/)是三阶遍历的修改版。