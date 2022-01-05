# 打印二叉树中给定节点的表兄弟

> 原文:[https://www . geesforgeks . org/print-给定二进制树节点的表亲/](https://www.geeksforgeeks.org/print-cousins-of-a-given-node-in-binary-tree/)

给定一个二叉树和一个节点，打印给定节点的所有表兄弟。请注意，不应打印兄弟姐妹。
**例:**

```
Input : root of below tree 
             1
           /   \
          2     3
        /   \  /  \
       4    5  6   7
       and pointer to a node say 5.

Output : 6, 7
```

首先使用这里讨论的方法找到给定节点的级别。找到级别后，我们可以使用这里[讨论的方法](https://www.geeksforgeeks.org/print-nodes-at-k-distance-from-root/)打印给定级别的所有节点。唯一要照顾的是，弟妹不要印。为了处理这个问题，我们将打印功能更改为首先检查同级节点，只有当它不是同级节点时才打印节点。
下面是上面想法的实现。

## C++

```
// C++ program to print cousins of a node
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    Node *left, *right;
};

// A utility function to create a new
// Binary Tree Node
Node *newNode(int item)
{
    Node *temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* It returns level of the node if it is
present in tree, otherwise returns 0.*/
int getLevel(Node *root, Node *node, int level)
{

    // base cases
    if (root == NULL)
        return 0;
    if (root == node)
        return level;

    // If node is present in left subtree
    int downlevel = getLevel(root->left,
                             node, level + 1);
    if (downlevel != 0)
        return downlevel;

    // If node is not present in left subtree
    return getLevel(root->right, node, level + 1);
}

/* Print nodes at a given level such that
sibling of node is not printed if it exists */
void printGivenLevel(Node* root, Node *node, int level)
{
    // Base cases
    if (root == NULL || level < 2)
        return;

    // If current node is parent of a node
    // with given level
    if (level == 2)
    {
        if (root->left == node || root->right == node)
            return;
        if (root->left)
            cout << root->left->data << " ";
        if (root->right)
            cout << root->right->data;
    }

    // Recur for left and right subtrees
    else if (level > 2)
    {
        printGivenLevel(root->left, node, level - 1);
        printGivenLevel(root->right, node, level - 1);
    }
}

// This function prints cousins of a given node
void printCousins(Node *root, Node *node)
{
    // Get level of given node
    int level = getLevel(root, node, 1);

    // Print nodes of given level.
    printGivenLevel(root, node, level);
}

// Driver Code
int main()
{
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->right->right = newNode(15);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    printCousins(root, root->left->right);

    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to print cousins of a node
#include <stdio.h>
#include <stdlib.h>

// A Binary Tree Node
struct Node
{
    int data;
    Node *left, *right;
};

// A utility function to create a new Binary
// Tree Node
Node *newNode(int item)
{
    Node *temp =  new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* It returns level of the node if it is present
   in tree, otherwise returns 0.*/
int getLevel(Node *root, Node *node, int level)
{
    // base cases
    if (root == NULL)
        return 0;
    if (root == node)
        return level;

    // If node is present in left subtree
    int downlevel = getLevel(root->left, node, level+1);
    if (downlevel != 0)
        return downlevel;

    // If node is not present in left subtree
    return getLevel(root->right, node, level+1);
}

/* Print nodes at a given level such that sibling of
   node is not printed if it exists  */
void printGivenLevel(Node* root, Node *node, int level)
{
    // Base cases
    if (root == NULL || level < 2)
        return;

    // If current node is parent of a node with
    // given level
    if (level == 2)
    {
        if (root->left == node || root->right == node)
            return;
        if (root->left)
           printf("%d ", root->left->data);
        if (root->right)
           printf("%d ", root->right->data);
    }

    // Recur for left and right subtrees
    else if (level > 2)
    {
        printGivenLevel(root->left, node, level-1);
        printGivenLevel(root->right, node, level-1);
    }
}

// This function prints cousins of a given node
void printCousins(Node *root, Node *node)
{
    // Get level of given node
    int level = getLevel(root, node, 1);

    // Print nodes of given level.
    printGivenLevel(root, node, level);
}

// Driver Program to test above functions
int main()
{
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->right->right = newNode(15);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    printCousins(root, root->left->right);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print cousins of a node
class GfG {

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
}

// A utility function to create a new Binary
// Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

/* It returns level of the node if it is present
in tree, otherwise returns 0.*/
static int getLevel(Node root, Node node, int level)
{
    // base cases
    if (root == null)
        return 0;
    if (root == node)
        return level;

    // If node is present in left subtree
    int downlevel = getLevel(root.left, node, level+1);
    if (downlevel != 0)
        return downlevel;

    // If node is not present in left subtree
    return getLevel(root.right, node, level+1);
}

/* Print nodes at a given level such that sibling of
node is not printed if it exists */
static void printGivenLevel(Node root, Node node, int level)
{
    // Base cases
    if (root == null || level < 2)
        return;

    // If current node is parent of a node with
    // given level
    if (level == 2)
    {
        if (root.left == node || root.right == node)
            return;
        if (root.left != null)
        System.out.print(root.left.data + " ");
        if (root.right != null)
        System.out.print(root.right.data + " ");
    }

    // Recur for left and right subtrees
    else if (level > 2)
    {
        printGivenLevel(root.left, node, level-1);
        printGivenLevel(root.right, node, level-1);
    }
}

// This function prints cousins of a given node
static void printCousins(Node root, Node node)
{
    // Get level of given node
    int level = getLevel(root, node, 1);

    // Print nodes of given level.
    printGivenLevel(root, node, level);
}

// Driver Program to test above functions
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.left.right.right = newNode(15);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);

    printCousins(root, root.left.right);
}
}
```

## 蟒蛇 3

```
# Python3 program to print cousins of a node

# A utility function to create a new
# Binary Tree Node
class newNode:
    def __init__(self, item):
        self.data = item
        self.left = self.right = None

# It returns level of the node if it is
# present in tree, otherwise returns 0.
def getLevel(root, node, level):

    # base cases
    if (root == None):
        return 0
    if (root == node):
        return level

    # If node is present in left subtree
    downlevel = getLevel(root.left, node,
                               level + 1)
    if (downlevel != 0):
        return downlevel

    # If node is not present in left subtree
    return getLevel(root.right, node, level + 1)

# Prnodes at a given level such that
# sibling of node is not printed if
# it exists
def printGivenLevel(root, node, level):

    # Base cases
    if (root == None or level < 2):
        return

    # If current node is parent of a
    # node with given level
    if (level == 2):
        if (root.left == node or
            root.right == node):
            return
        if (root.left):
            print(root.left.data, end = " ")
        if (root.right):
            print(root.right.data, end = " ")

    # Recur for left and right subtrees
    elif (level > 2):
        printGivenLevel(root.left, node, level - 1)
        printGivenLevel(root.right, node, level - 1)

# This function prints cousins of a given node
def printCousins(root, node):

    # Get level of given node
    level = getLevel(root, node, 1)

    # Prnodes of given level.
    printGivenLevel(root, node, level)

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.left.right.right = newNode(15)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.right.left.right = newNode(8)

    printCousins(root, root.left.right)

# This code is contributed by PranchalK
```

## C#

```
// C# program to print cousins of a node
using System;

public class GfG
{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left, right;
}

// A utility function to create 
// a new Binary Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

/* It returns level of the node
if it is present in tree,
 otherwise returns 0.*/
static int getLevel(Node root,
            Node node, int level)
{
    // base cases
    if (root == null)
        return 0;
    if (root == node)
        return level;

    // If node is present in left subtree
    int downlevel = getLevel(root.left, node, level + 1);
    if (downlevel != 0)
        return downlevel;

    // If node is not present in left subtree
    return getLevel(root.right, node, level + 1);
}

/* Print nodes at a given level
such that sibling of node is
 not printed if it exists */
static void printGivenLevel(Node root,
                    Node node, int level)
{
    // Base cases
    if (root == null || level < 2)
        return;

    // If current node is parent of a node with
    // given level
    if (level == 2)
    {
        if (root.left == node || root.right == node)
            return;
        if (root.left != null)
            Console.Write(root.left.data + " ");
        if (root.right != null)
            Console.Write(root.right.data + " ");
    }

    // Recur for left and right subtrees
    else if (level > 2)
    {
        printGivenLevel(root.left, node, level - 1);
        printGivenLevel(root.right, node, level - 1);
    }
}

// This function prints cousins of a given node
static void printCousins(Node root, Node node)
{
    // Get level of given node
    int level = getLevel(root, node, 1);

    // Print nodes of given level.
    printGivenLevel(root, node, level);
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.left.right.right = newNode(15);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);

    printCousins(root, root.left.right);
}
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to print cousins of a node

// A Binary Tree Node
class Node
{
  constructor()
  {
    this.data=0;
    this.left= null;
    this.right = null;
  }
}

// A utility function to create 
// a new Binary Tree Node
function newNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

/* It returns level of the node
if it is present in tree,
 otherwise returns 0.*/
function getLevel(root, node, level)
{
    // base cases
    if (root == null)
        return 0;
    if (root == node)
        return level;

    // If node is present in left subtree
    var downlevel = getLevel(root.left, node, level + 1);
    if (downlevel != 0)
        return downlevel;

    // If node is not present in left subtree
    return getLevel(root.right, node, level + 1);
}

/* Print nodes at a given level
such that sibling of node is
 not printed if it exists */
function printGivenLevel(root, node, level)
{
    // Base cases
    if (root == null || level < 2)
        return;

    // If current node is parent of a node with
    // given level
    if (level == 2)
    {
        if (root.left == node || root.right == node)
            return;
        if (root.left != null)
            document.write(root.left.data + " ");
        if (root.right != null)
            document.write(root.right.data + " ");
    }

    // Recur for left and right subtrees
    else if (level > 2)
    {
        printGivenLevel(root.left, node, level - 1);
        printGivenLevel(root.right, node, level - 1);
    }
}

// This function prints cousins of a given node
function printCousins(root, node)
{
    // Get level of given node
    var level = getLevel(root, node, 1);

    // Print nodes of given level.
    printGivenLevel(root, node, level);
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.left.right.right = newNode(15);
root.right.left = newNode(6);
root.right.right = newNode(7);
root.right.left.right = newNode(8);
printCousins(root, root.left.right);

</script>
```

**输出:**

```
6 7
```

**时间复杂度:** O(n)
我们能用单次遍历解决这个问题吗？请参考以下文章
[**在二叉树中打印给定节点的表兄弟|单遍历**](https://www.geeksforgeeks.org/print-cousins-of-a-given-node-in-binary-tree-single-traversal/)
本文由 **Shivam Gupta** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息