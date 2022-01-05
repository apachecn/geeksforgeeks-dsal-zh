# 递归程序，以交替顺序打印每一级二叉树的极端节点

> 原文:[https://www . geeksforgeeks . org/递归-程序-打印-交替顺序二进制树每一级的极端节点/](https://www.geeksforgeeks.org/recursive-program-to-print-extreme-nodes-of-each-level-of-binary-tree-in-alternate-order/)

给定一棵二叉树，任务是以交替的顺序打印每一级的极端角落的节点。
**例:**

```
Input : 
         1
        /  \
       2    3
      /    /  \
     4    5    6
    /    / \
   7    8   9
Output : 1 2 6 7
Print the rightmost node at 1st level: 1
Print the leftmost node at 2nd level: 2
Print the rightmost node at 3rd level: 6
Print the leftmost node at 4th level: 7
*Other possible output will be* -> 1 3 4 9

Input :
        3 
       /  \
      8    1
     / \  / \
    9  5 6   4
Output : 3 8 4
```

我们已经讨论了[迭代方法](https://www.geeksforgeeks.org/print-extreme-nodes-of-each-level-of-binary-tree-in-alternate-order/)来解决这个问题。本文讨论递归方法。
**方法:**想法是以螺旋形式执行[级顺序遍历，在每一级打印遍历过程中的第一个节点，这些节点将是交替形式中出现的极端拐角处的节点。
以下是上述方法的实施:](https://www.geeksforgeeks.org/level-order-traversal-in-spiral-form/) 

## C++

```
// C++ program to print nodes of extreme corners
// of each level in alternate order

#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Utility function to allocate memory for a new node
Node* newNode(int data)
{
    Node* node = new (Node);
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function that returns the height of the binary tree
int height(Node* root)
{
    if (root == NULL)
        return 0;

    int lheight = height(root->left);
    int rheight = height(root->right);

    return max(lheight, rheight) + 1;
}

// Function performs level order traversal from right to
// left and prints the first node during the traversal
void rightToLeft(Node* root, int level, int& f)
{
    if (root == NULL)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f == 0) {
        printf("%d ", root->data);
        f = 1;
    }

    else if (level > 1) {
        rightToLeft(root->right, level - 1, f);
        rightToLeft(root->left, level - 1, f);
    }
}

// Function performs level order traversal from left to
// right and prints the first node during the traversal
void leftToRight(Node* root, int level, int& f)
{
    if (root == NULL)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f == 1) {
        printf("%d ", root->data);
        f = 0;
    }

    else if (level > 1) {
        leftToRight(root->left, level - 1, f);
        leftToRight(root->right, level - 1, f);
    }
}

// Function to print the extreme nodes of
// a given binary tree
void printExtremeNodes(Node* root)
{
    // Stores height of binary tree
    int h = height(root);

    // Flag to mark the change in level
    int flag = 0;

    // To check if the extreme node of a
    // particular level has been visited
    int f = 0;

    for (int i = 1; i <= h; i++) {
        // If flag is zero then traverse from
        // right to left at the given level and
        // print the first node during the traversal
        if (flag == 0) {
            rightToLeft(root, i, f);
            flag = 1;
        }

        // If flag is one then traverse from
        // left to right at the given level and
        // print the first node during the traversal
        else if (flag == 1) {
            leftToRight(root, i, f);
            flag = 0;
        }
    }

    return;
}

// Driver code
int main()
{
    Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);

    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(7);

    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(11);
    root->right->right->left = newNode(14);
    root->right->right->right = newNode(15);

    root->left->left->left->left = newNode(16);
    root->left->left->left->right = newNode(17);
    root->right->right->right->right = newNode(31);

    printExtremeNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print nodes of extreme corners
// of each level in alternate order
import java.util.*;

class GFG
{

//INT class
static class INT
{
    int a;
}

// A binary tree node
static class Node
{
    int data;
    Node left, right;
};

// Utility function to allocate memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function that returns the height of the binary tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int lheight = height(root.left);
    int rheight = height(root.right);

    return Math.max(lheight, rheight) + 1;
}

// Function performs level order traversal from right to
// left and prints the first node during the traversal
static void rightToLeft(Node root, int level, INT f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 0)
    {
        System.out.printf("%d ", root.data);
        f.a = 1;
    }

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1, f);
        rightToLeft(root.left, level - 1, f);
    }
}

// Function performs level order traversal from left to
// right and prints the first node during the traversal
static void leftToRight(Node root, int level, INT f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 1)
    {
        System.out.printf("%d ", root.data);
        f.a = 0;
    }

    else if (level > 1)
    {
        leftToRight(root.left, level - 1, f);
        leftToRight(root.right, level - 1, f);
    }
}

// Function to print the extreme nodes of
// a given binary tree
static void printExtremeNodes(Node root)
{
    // Stores height of binary tree
    int h = height(root);

    // Flag to mark the change in level
    int flag = 0;

    // To check if the extreme node of a
    // particular level has been visited
    INT f=new INT();
    f.a = 0;

    for (int i = 1; i <= h; i++)
    {
        // If flag is zero then traverse from
        // right to left at the given level and
        // print the first node during the traversal
        if (flag == 0)
        {
            rightToLeft(root, i, f);
            flag = 1;
        }

        // If flag is one then traverse from
        // left to right at the given level and
        // print the first node during the traversal
        else if (flag == 1)
        {
            leftToRight(root, i, f);
            flag = 0;
        }
    }

    return;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(10);
    root.left.right.right = newNode(11);
    root.right.right.left = newNode(14);
    root.right.right.right = newNode(15);

    root.left.left.left.left = newNode(16);
    root.left.left.left.right = newNode(17);
    root.right.right.right.right = newNode(31);

    printExtremeNodes(root);

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print nodes of
# extreme corners of each level in
# alternate order
from collections import deque

# A binary tree node has key, pointer to left
# child and a pointer to right child
class Node:
    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function that returns the height of
# the binary tree
def height(root: Node) -> int:

    if (root is None):
        return 0

    lheight = height(root.left)
    rheight = height(root.right)

    return max(lheight, rheight) + 1

# Function performs level order traversal
# from right to left and prints the first
# node during the traversal
def rightToLeft(root: Node, level: int) -> int:

    global f

    if (root is None):
        return

    # Checks for the value of f so that
    # only first node is printed during
    # the traversal and no other node is printed
    if (level == 1 and f == 0):
        print("%d " % root.data, end = "")
        f = 1

    elif (level > 1):
        rightToLeft(root.right, level - 1)
        rightToLeft(root.left, level - 1)

# Function performs level order traversal
# from left to right and prints the first
# node during the traversal
def leftToRight(root: Node, level: int):

    global f

    if (root is None):
        return

    # Checks for the value of f so that
    # only first node is printed during
    # the traversal and no other node is printed
    if (level == 1 and f == 1):
        print("%d " % root.data, end = "")
        f = 0

    elif (level > 1):
        leftToRight(root.left, level - 1)
        leftToRight(root.right, level - 1)

# Function to print the extreme nodes of
# a given binary tree
def printExtremeNodes(root: Node):

    global f

    # Stores height of binary tree
    h = height(root)

    # Flag to mark the change in level
    flag = 0

    # To check if the extreme node of a
    # particular level has been visited
    f = 0

    for i in range(1, h + 1):

        # If flag is zero then traverse from
        # right to left at the given level and
        # print the first node during the traversal
        if (flag == 0):
            rightToLeft(root, i)
            flag = 1

        # If flag is one then traverse from
        # left to right at the given level and
        # print the first node during the traversal
        elif (flag == 1):
            leftToRight(root, i)
            flag = 0

    return

# Driver Code
if __name__ == "__main__":

    root = Node(1)

    root.left = Node(2)
    root.right = Node(3)

    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(7)

    root.left.left.left = Node(8)
    root.left.left.right = Node(9)
    root.left.right.left = Node(10)
    root.left.right.right = Node(11)
    root.right.right.left = Node(14)
    root.right.right.right = Node(15)

    root.left.left.left.left = Node(16)
    root.left.left.left.right = Node(17)
    root.right.right.right.right = Node(31)

    printExtremeNodes(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to print nodes of extreme corners
// of each level in alternate order
using System;

class GFG
{

//INT class
public class INT
{
    public int a;
}

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;
};

// Utility function to allocate memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function that returns the height of the binary tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int lheight = height(root.left);
    int rheight = height(root.right);

    return Math.Max(lheight, rheight) + 1;
}

// Function performs level order traversal from right to
// left and prints the first node during the traversal
static void rightToLeft(Node root, int level, INT f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 0)
    {
        Console.Write("{0} ", root.data);
        f.a = 1;
    }

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1, f);
        rightToLeft(root.left, level - 1, f);
    }
}

// Function performs level order traversal from left to
// right and prints the first node during the traversal
static void leftToRight(Node root, int level, INT f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 1)
    {
        Console.Write("{0} ", root.data);
        f.a = 0;
    }

    else if (level > 1)
    {
        leftToRight(root.left, level - 1, f);
        leftToRight(root.right, level - 1, f);
    }
}

// Function to print the extreme nodes of
// a given binary tree
static void printExtremeNodes(Node root)
{
    // Stores height of binary tree
    int h = height(root);

    // Flag to mark the change in level
    int flag = 0;

    // To check if the extreme node of a
    // particular level has been visited
    INT f=new INT();
    f.a = 0;

    for (int i = 1; i <= h; i++)
    {
        // If flag is zero then traverse from
        // right to left at the given level and
        // print the first node during the traversal
        if (flag == 0)
        {
            rightToLeft(root, i, f);
            flag = 1;
        }

        // If flag is one then traverse from
        // left to right at the given level and
        // print the first node during the traversal
        else if (flag == 1)
        {
            leftToRight(root, i, f);
            flag = 0;
        }
    }

    return;
}

// Driver code
public static void Main()
{
    Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(10);
    root.left.right.right = newNode(11);
    root.right.right.left = newNode(14);
    root.right.right.right = newNode(15);

    root.left.left.left.left = newNode(16);
    root.left.left.left.right = newNode(17);
    root.right.right.right.right = newNode(31);

    printExtremeNodes(root);

}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to print nodes of extreme corners
// of each level in alternate order

//INT class
class INT
{
    constructor()
    {
        this.a = 0;
    }
}

// A binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to allocate memory for a new node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function that returns the height of the binary tree
function height(root)
{
    if (root == null)
        return 0;

    var lheight = height(root.left);
    var rheight = height(root.right);

    return Math.max(lheight, rheight) + 1;
}

// Function performs level order traversal from right to
// left and prints the first node during the traversal
function rightToLeft(root, level, f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 0)
    {
        document.write(root.data + " ");
        f.a = 1;
    }

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1, f);
        rightToLeft(root.left, level - 1, f);
    }
}

// Function performs level order traversal from left to
// right and prints the first node during the traversal
function leftToRight(root, level, f)
{
    if (root == null)
        return;

    // Checks for the value of f so that
    // only first node is printed during
    // the traversal and no other node is printed
    if (level == 1 && f.a == 1)
    {
        document.write(root.data+ " ");
        f.a = 0;
    }

    else if (level > 1)
    {
        leftToRight(root.left, level - 1, f);
        leftToRight(root.right, level - 1, f);
    }
}

// Function to print the extreme nodes of
// a given binary tree
function printExtremeNodes(root)
{
    // Stores height of binary tree
    var h = height(root);

    // Flag to mark the change in level
    var flag = 0;

    // To check if the extreme node of a
    // particular level has been visited
    var f=new INT();
    f.a = 0;

    for (var i = 1; i <= h; i++)
    {
        // If flag is zero then traverse from
        // right to left at the given level and
        // print the first node during the traversal
        if (flag == 0)
        {
            rightToLeft(root, i, f);
            flag = 1;
        }

        // If flag is one then traverse from
        // left to right at the given level and
        // print the first node during the traversal
        else if (flag == 1)
        {
            leftToRight(root, i, f);
            flag = 0;
        }
    }

    return;
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.right = newNode(7);
root.left.left.left = newNode(8);
root.left.left.right = newNode(9);
root.left.right.left = newNode(10);
root.left.right.right = newNode(11);
root.right.right.left = newNode(14);
root.right.right.right = newNode(15);
root.left.left.left.left = newNode(16);
root.left.left.left.right = newNode(17);
root.right.right.right.right = newNode(31);
printExtremeNodes(root);

</script>
```

**Output:** 

```
1 2 7 8 31    
```

**时间复杂度** : O(N^2)，其中 n 是二叉树中节点的总数。
**辅助空间:** O(N)