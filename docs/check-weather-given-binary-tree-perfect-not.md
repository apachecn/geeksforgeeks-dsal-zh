# 检查给定的二叉树是否完美

> 原文:[https://www . geesforgeks . org/check-weather-given-二叉树-perfect-not/](https://www.geeksforgeeks.org/check-weather-given-binary-tree-perfect-not/)

给定一棵二叉树，写一个函数来检查给定的二叉树是否是一棵完美的二叉树。
一棵二叉树是[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，其中所有内部节点都有两个子节点，所有叶子都在同一级别。

**例:**
下面的树是一棵完美的二叉树

```
               10
           /       \  
         20         30  
        /  \        /  \
      40    50    60   70

               18
           /       \  
         15         30  
```

下面的树是**而不是**一棵完美的二叉树

```
      1
    /    \
   2       3
    \     /  \   
     4   5    6
```

高度为 h(其中高度是从根到叶的路径上的节点数)的[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)有 2 个<sup>h</sup>–1 个节点。
下面是一个检查给定二叉树是否完美的想法。

1.  找到任何节点的深度(在下面的树中，我们找到最左边节点的深度)。让这个深度为 d。
2.  现在递归遍历树，检查以下两个条件。
    *   每个内部节点都应该有两个非空的子节点
    *   所有的叶子都有深度

## C++

```
// C++ program to check whether a given
// Binary Tree is Perfect or not
#include<bits/stdc++.h>

/*  Tree node structure */
struct Node
{
    int key;
    struct Node *left, *right;
};

// Returns depth of leftmost leaf.
int findADepth(Node *node)
{
   int d = 0;
   while (node != NULL)
   {
      d++;
      node = node->left;
   }
   return d;
}

/* This function tests if a binary tree is perfect
   or not. It basically checks for two things :
   1) All leaves are at same level
   2) All internal nodes have two children */
bool isPerfectRec(struct Node* root, int d, int level = 0)
{
    // An empty tree is perfect
    if (root == NULL)
        return true;

    // If leaf node, then its depth must be same as
    // depth of all other leaves.
    if (root->left == NULL && root->right == NULL)
        return (d == level+1);

    // If internal node and one child is empty
    if (root->left == NULL || root->right == NULL)
        return false;

    // Left and right subtrees must be perfect.
    return isPerfectRec(root->left, d, level+1) &&
           isPerfectRec(root->right, d, level+1);
}

// Wrapper over isPerfectRec()
bool isPerfect(Node *root)
{
   int d = findADepth(root);
   return isPerfectRec(root, d);
}

/* Helper function that allocates a new node with the
   given key and NULL left and right pointer. */
struct Node *newNode(int k)
{
    struct Node *node = new Node;
    node->key = k;
    node->right = node->left = NULL;
    return node;
}

// Driver Program
int main()
{
    struct Node* root = NULL;
    root = newNode(10);
    root->left = newNode(20);
    root->right = newNode(30);

    root->left->left = newNode(40);
    root->left->right = newNode(50);
    root->right->left = newNode(60);
    root->right->right = newNode(70);

    if (isPerfect(root))
        printf("Yes\n");
    else
        printf("No\n");

    return(0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a given
// Binary Tree is Perfect or not
class GfG {

/* Tree node structure */
static class Node
{
    int key;
    Node left, right;
}

// Returns depth of leftmost leaf.
static int findADepth(Node node)
{
int d = 0;
while (node != null)
{
    d++;
    node = node.left;
}
return d;
}

/* This function tests if a binary tree is perfect
or not. It basically checks for two things :
1) All leaves are at same level
2) All internal nodes have two children */
static boolean isPerfectRec(Node root, int d, int level)
{
    // An empty tree is perfect
    if (root == null)
        return true;

    // If leaf node, then its depth must be same as
    // depth of all other leaves.
    if (root.left == null && root.right == null)
        return (d == level+1);

    // If internal node and one child is empty
    if (root.left == null || root.right == null)
        return false;

    // Left and right subtrees must be perfect.
    return isPerfectRec(root.left, d, level+1) && isPerfectRec(root.right, d, level+1);
}

// Wrapper over isPerfectRec()
static boolean isPerfect(Node root)
{
int d = findADepth(root);
return isPerfectRec(root, d, 0);
}

/* Helper function that allocates a new node with the
given key and NULL left and right pointer. */
static Node newNode(int k)
{
    Node node = new Node();
    node.key = k;
    node.right = null;
    node.left = null;
    return node;
}

// Driver Program
public static void main(String args[])
{
    Node root = null;
    root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);

    root.left.left = newNode(40);
    root.left.right = newNode(50);
    root.right.left = newNode(60);
    root.right.right = newNode(70);

    if (isPerfect(root) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}
```

## 蟒蛇 3

```
# Python3 program to check whether a
# given Binary Tree is Perfect or not

# Helper class that allocates a new
# node with the given key and None
# left and right pointer.
class newNode:
    def __init__(self, k):
        self.key = k
        self.right = self.left = None

# Returns depth of leftmost leaf.
def findADepth(node):
    d = 0
    while (node != None):
        d += 1
        node = node.left
    return d

# This function tests if a binary tree
# is perfect or not. It basically checks
# for two things :
# 1) All leaves are at same level
# 2) All internal nodes have two children
def isPerfectRec(root, d, level = 0):

    # An empty tree is perfect
    if (root == None):
        return True

    # If leaf node, then its depth must
    # be same as depth of all other leaves.
    if (root.left == None and root.right == None):
        return (d == level + 1)

    # If internal node and one child is empty
    if (root.left == None or root.right == None):
        return False

    # Left and right subtrees must be perfect.
    return (isPerfectRec(root.left, d, level + 1) and
            isPerfectRec(root.right, d, level + 1))

# Wrapper over isPerfectRec()
def isPerfect(root):
    d = findADepth(root)
    return isPerfectRec(root, d)

# Driver Code
if __name__ == '__main__':
    root = None
    root = newNode(10)
    root.left = newNode(20)
    root.right = newNode(30)

    root.left.left = newNode(40)
    root.left.right = newNode(50)
    root.right.left = newNode(60)
    root.right.right = newNode(70)

    if (isPerfect(root)):
        print("Yes")
    else:
        print("No")

# This code is contributed by pranchalK
```

## C#

```
// C# program to check whether a given
// Binary Tree is Perfect or not
using System;

class GfG
{

/* Tree node structure */
class Node
{
    public int key;
    public Node left, right;
}

// Returns depth of leftmost leaf.
static int findADepth(Node node)
{
    int d = 0;
    while (node != null)
    {
        d++;
        node = node.left;
    }
    return d;
}

/* This function tests if a binary tree is perfect
or not. It basically checks for two things :
1) All leaves are at same level
2) All internal nodes have two children */
static bool isPerfectRec(Node root,
                    int d, int level)
{
    // An empty tree is perfect
    if (root == null)
        return true;

    // If leaf node, then its depth must be same as
    // depth of all other leaves.
    if (root.left == null && root.right == null)
        return (d == level+1);

    // If internal node and one child is empty
    if (root.left == null || root.right == null)
        return false;

    // Left and right subtrees must be perfect.
    return isPerfectRec(root.left, d, level+1) &&
            isPerfectRec(root.right, d, level+1);
}

// Wrapper over isPerfectRec()
static bool isPerfect(Node root)
{
    int d = findADepth(root);
    return isPerfectRec(root, d, 0);
}

/* Helper function that allocates a new node with the
given key and NULL left and right pointer. */
static Node newNode(int k)
{
    Node node = new Node();
    node.key = k;
    node.right = null;
    node.left = null;
    return node;
}

// Driver code
public static void Main()
{
    Node root = null;
    root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);

    root.left.left = newNode(40);
    root.left.right = newNode(50);
    root.right.left = newNode(60);
    root.right.right = newNode(70);

    if (isPerfect(root) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

// Javascript program to check whether a given
// Binary Tree is Perfect or not

/* Tree node structure */
class Node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
}

// Returns depth of leftmost leaf.
function findADepth(node)
{
    var d = 0;

    while (node != null)
    {
        d++;
        node = node.left;
    }
    return d;
}

/* This function tests if a binary tree is perfect
or not. It basically checks for two things :
1) All leaves are at same level
2) All internal nodes have two children */
function isPerfectRec(root, d, level)
{

    // An empty tree is perfect
    if (root == null)
        return true;

    // If leaf node, then its depth must be same as
    // depth of all other leaves.
    if (root.left == null && root.right == null)
        return (d == level + 1);

    // If internal node and one child is empty
    if (root.left == null || root.right == null)
        return false;

    // Left and right subtrees must be perfect.
    return isPerfectRec(root.left, d, level + 1) &&
           isPerfectRec(root.right, d, level + 1);
}

// Wrapper over isPerfectRec()
function isPerfect(root)
{
    var d = findADepth(root);
    return isPerfectRec(root, d, 0);
}

/* Helper function that allocates a new node with the
given key and NULL left and right pointer. */
function newNode(k)
{
    var node = new Node();
    node.key = k;
    node.right = null;
    node.left = null;
    return node;
}

// Driver code
var root = null;
root = newNode(10);
root.left = newNode(20);
root.right = newNode(30);
root.left.left = newNode(40);
root.left.right = newNode(50);
root.right.left = newNode(60);
root.right.right = newNode(70);
if (isPerfect(root) == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by noob2000

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)

**方法二:利用二叉树的长度**

由于一棵完整的二叉树有 2^h-1 个节点，我们可以计算二叉树中的节点数，并确定它是否是 2 的幂。

为了有效地确定它是否是 2 的幂，我们可以使用按位运算 x &(x+1)= 0

## 蟒蛇 3

```
# Python3 program to check whether a
# given Binary Tree is Perfect or not

# Helper class that allocates a new
# node with the given key and None
# left and right pointer.
class newNode:
    def __init__(self, k):
        self.key = k
        self.right = self.left = None

#This functions gets the size of binary tree
#Basically, the number of nodes this binary tree has
def getLength(root):
  if root == None:
    return 0
  return 1 + getLength(root.left) + getLength(root.right)

#Returns True if length of binary tree is a power of 2 else False
def isPerfect(root):
  length = getLength(root)
  return length & (length+1) == 0

# Driver Code
if __name__ == '__main__':
    root = None
    root = newNode(10)
    root.left = newNode(20)
    root.right = newNode(30)

    root.left.left = newNode(40)
    root.left.right = newNode(50)
    root.right.left = newNode(60)
    root.right.right = newNode(70)

    if (isPerfect(root)):
        print("Yes")
    else:
        print("No")

# This code is contributed by beardedowl
```

本文由 **Nikhil Papisetty** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。