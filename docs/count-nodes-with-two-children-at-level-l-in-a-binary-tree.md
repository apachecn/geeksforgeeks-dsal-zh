# 计算二叉树中 L 级有两个孩子的节点

> 原文:[https://www . geesforgeks . org/count-nodes-with-two-level-in-l-in-a-a-二叉树/](https://www.geeksforgeeks.org/count-nodes-with-two-children-at-level-l-in-a-binary-tree/)

给定一棵二叉树，任务是计算给定级别 **L** 上有两个子节点的节点数。

**示例:**

```
Input: 
          1
         /  \
        2    3
       / \    \
      4   5    6
         /    / \
        7    8   9
L = 2
Output: 1

Input:
          20
         /   \
        8     22
       / \    / \
      5   3  4   25
     / \  / \     \
    1  10 2  14    6
L = 3
Output: 2
```

**方法:**初始化变量**计数= 0** 。以层次顺序的方式递归遍历树。如果当前级别与给定级别相同，则检查当前节点是否有两个子节点。如果它有两个孩子，那么增加变量**计数**。

下面是上述方法的实现:

## C++

```
// C++ program to find number of full nodes
// at a given level
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to allocate memory for a new node
struct Node* newNode(int data)
{
    struct Node* node = new (struct Node);
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function that returns the height of binary tree
int height(struct Node* root)
{
    if (root == NULL)
        return 0;

    int lheight = height(root->left);
    int rheight = height(root->right);

    return max(lheight, rheight) + 1;
}

// Level Order traversal to find the number of nodes
// having two children
void LevelOrder(struct Node* root, int level, int& count)
{
    if (root == NULL)
        return;

    if (level == 1 && root->left && root->right)
        count++;

    else if (level > 1) {
        LevelOrder(root->left, level - 1, count);
        LevelOrder(root->right, level - 1, count);
    }
}

// Returns the number of full nodes
// at a given level
int CountFullNodes(struct Node* root, int L)
{
    // Stores height of tree
    int h = height(root);

    // Stores count of nodes at a given level
    // that have two children
    int count = 0;

    LevelOrder(root, L, count);

    return count;
}

// Driver code
int main()
{
    struct Node* root = newNode(7);
    root->left = newNode(5);
    root->right = newNode(6);
    root->left->left = newNode(8);
    root->left->right = newNode(1);
    root->left->left->left = newNode(2);
    root->left->left->right = newNode(11);
    root->right->left = newNode(3);
    root->right->right = newNode(9);
    root->right->right->right = newNode(13);
    root->right->right->left = newNode(10);
    root->right->right->right->left = newNode(4);
    root->right->right->right->right = newNode(12);

    int L = 3;

    cout << CountFullNodes(root, L);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of full nodes
// at a given level
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

// Function that returns the height of binary tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int lheight = height(root.left);
    int rheight = height(root.right);

    return Math.max(lheight, rheight) + 1;
}

// Level Order traversal to find the number of nodes
// having two children
static void LevelOrder( Node root, int level, INT count)
{
    if (root == null)
        return;

    if (level == 1 && root.left!=null && root.right!=null)
        count.a++;

    else if (level > 1)
    {
        LevelOrder(root.left, level - 1, count);
        LevelOrder(root.right, level - 1, count);
    }
}

// Returns the number of full nodes
// at a given level
static int CountFullNodes( Node root, int L)
{
    // Stores height of tree
    int h = height(root);

    // Stores count of nodes at a given level
    // that have two children
    INT count =new INT();
    count.a = 0;

    LevelOrder(root, L, count);

    return count.a;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(7);
    root.left = newNode(5);
    root.right = newNode(6);
    root.left.left = newNode(8);
    root.left.right = newNode(1);
    root.left.left.left = newNode(2);
    root.left.left.right = newNode(11);
    root.right.left = newNode(3);
    root.right.right = newNode(9);
    root.right.right.right = newNode(13);
    root.right.right.left = newNode(10);
    root.right.right.right.left = newNode(4);
    root.right.right.right.right = newNode(12);

    int L = 3;

    System.out.print( CountFullNodes(root, L));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find number of
# full nodes at a given level

# INT class
class INT:

    def __init__(self):

        self.a = 0

# A binary tree node
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

# Utility function to allocate
# memory for a new node
def newNode(data):

    node = Node(data)

    return node

# Function that returns the
# height of binary tree
def height(root):

    if (root == None):
        return 0;

    lheight = height(root.left);
    rheight = height(root.right);

    return max(lheight, rheight) + 1;

# Level Order traversal to find the
# number of nodes having two children
def LevelOrder(root, level, count):

    if (root == None):
        return;

    if (level == 1 and
        root.left != None and
       root.right != None):
        count.a += 1

    elif (level > 1):
        LevelOrder(root.left,
                   level - 1, count);
        LevelOrder(root.right,
                   level - 1, count);

# Returns the number of full nodes
# at a given level
def CountFullNodes(root, L):

    # Stores height of tree
    h = height(root);

    # Stores count of nodes at a
    # given level that have two children
    count = INT()

    LevelOrder(root, L, count);

    return count.a

# Driver code   
if __name__=="__main__":

    root = newNode(7);
    root.left = newNode(5);
    root.right = newNode(6);
    root.left.left = newNode(8);
    root.left.right = newNode(1);
    root.left.left.left = newNode(2);
    root.left.left.right = newNode(11);
    root.right.left = newNode(3);
    root.right.right = newNode(9);
    root.right.right.right = newNode(13);
    root.right.right.left = newNode(10);
    root.right.right.right.left = newNode(4);
    root.right.right.right.right = newNode(12);

    L = 3;

    print(CountFullNodes(root, L))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find number of full nodes
// at a given level
using System;

class GFG
{

// INT class
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

// Function that returns the height of binary tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int lheight = height(root.left);
    int rheight = height(root.right);

    return Math.Max(lheight, rheight) + 1;
}

// Level Order traversal to find the number of nodes
// having two children
static void LevelOrder( Node root, int level, INT count)
{
    if (root == null)
        return;

    if (level == 1 && root.left!=null && root.right!=null)
        count.a++;

    else if (level > 1)
    {
        LevelOrder(root.left, level - 1, count);
        LevelOrder(root.right, level - 1, count);
    }
}

// Returns the number of full nodes
// at a given level
static int CountFullNodes( Node root, int L)
{
    // Stores height of tree
    int h = height(root);

    // Stores count of nodes at a given level
    // that have two children
    INT count =new INT();
    count.a = 0;

    LevelOrder(root, L, count);

    return count.a;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(7);
    root.left = newNode(5);
    root.right = newNode(6);
    root.left.left = newNode(8);
    root.left.right = newNode(1);
    root.left.left.left = newNode(2);
    root.left.left.right = newNode(11);
    root.right.left = newNode(3);
    root.right.right = newNode(9);
    root.right.right.right = newNode(13);
    root.right.right.left = newNode(10);
    root.right.right.right.left = newNode(4);
    root.right.right.right.right = newNode(12);

    int L = 3;

    Console.Write( CountFullNodes(root, L));

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find number
// of full nodes at a given level

// INT class
let a = 0;

// A binary tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Utility function to allocate memory
// for a new node
function newNode(data)
{
    let node = new Node(data);
    return (node);
}

// Function that returns the height
// of binary tree
function height(root)
{
    if (root == null)
        return 0;

    let lheight = height(root.left);
    let rheight = height(root.right);

    return Math.max(lheight, rheight) + 1;
}

// Level Order traversal to find the number
// of nodes having two children
function LevelOrder(root, level)
{
    if (root == null)
        return;

    if (level == 1 && root.left != null &&
                     root.right != null)
        a++;

    else if (level > 1)
    {
        LevelOrder(root.left, level - 1);
        LevelOrder(root.right, level - 1);
    }
}

// Returns the number of full nodes
// at a given level
function CountFullNodes(root, L)
{

    // Stores height of tree
    let h = height(root);

    LevelOrder(root, L);

    return a;
}

// Driver code
let root = newNode(7);
root.left = newNode(5);
root.right = newNode(6);
root.left.left = newNode(8);
root.left.right = newNode(1);
root.left.left.left = newNode(2);
root.left.left.right = newNode(11);
root.right.left = newNode(3);
root.right.right = newNode(9);
root.right.right.right = newNode(13);
root.right.right.left = newNode(10);
root.right.right.right.left = newNode(4);
root.right.right.right.right = newNode(12);

let L = 3;

document.write(CountFullNodes(root, L));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
2
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)