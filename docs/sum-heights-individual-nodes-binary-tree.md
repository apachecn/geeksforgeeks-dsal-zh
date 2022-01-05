# 二叉树中所有单个节点的高度之和

> 原文:[https://www . geesforgeks . org/sum-heights-individual-nodes-二叉树/](https://www.geeksforgeeks.org/sum-heights-individual-nodes-binary-tree/)

给定一棵二叉树，求树中所有单个节点的高度之和。

**示例:**

![Binary Tree](img/ef5f584cbb9229f28c6d9971eb7718ef.png)

```
For this tree:
1). Height of Node 1 - 3
2). Height of Node 2 - 2
3). Height of Node 3 - 1
4). Height of Node 4 - 1
5). Height of Node 5 - 1

Adding all of them = 8
```

**先决条件:-** [二叉树高度](https://www.geeksforgeeks.org/iterative-method-to-find-height-of-binary-tree/)

**简单解决方案:**

我们通过以下任何一种方法解析树来获得所有单个节点的高度，即 inorder、后置、前置(我执行了 Inorder 树遍历)，并使用 *getHeigh* t 函数获得它们的高度，该函数检查左右子树并返回它们的最大值。最后，我们把所有的个体高度加起来。

## C++

```
// C++ program to find sum of heights of all
// nodes in a binary tree
#include <bits/stdc++.h>

/* A binary tree Node has data, pointer to
    left child and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Compute the "maxHeight" of a particular Node*/
int getHeight(struct Node* Node)
{
    if (Node == NULL)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = getHeight(Node->left);
        int rHeight = getHeight(Node->right);

        /* use the larger one */
        if (lHeight > rHeight)
            return (lHeight + 1);
        else
            return (rHeight + 1);
    }
}

/* Helper function that allocates a new Node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* Node = (struct Node*)
        malloc(sizeof(struct Node));
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;

    return (Node);
}

/* Function to sum of heights of individual Nodes
   Uses Inorder traversal */
int getTotalHeight(struct Node* root)
{
    if (root == NULL)
        return 0;

    return getTotalHeight(root->left) +
           getHeight(root) +
           getTotalHeight(root->right);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    printf("Sum of heights of all Nodes = %d",   
                        getTotalHeight(root));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of heights of all
// nodes in a binary tree
class GfG {

/* A binary tree Node has data, pointer to
    left child and a pointer to right child */
static class Node {
    int data;
    Node left;
    Node right;
}

/* Compute the "maxHeight" of a particular Node*/
static int getHeight(Node Node)
{
    if (Node == null)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = getHeight(Node.left);
        int rHeight = getHeight(Node.right);

        /* use the larger one */
        if (lHeight > rHeight)
            return (lHeight + 1);
        else
            return (rHeight + 1);
    }
}

/* Helper function that allocates a new Node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node Node = new Node();
    Node.data = data;
    Node.left = null;
    Node.right = null;

    return (Node);
}

/* Function to sum of heights of individual Nodes
Uses Inorder traversal */
static int getTotalHeight( Node root)
{
    if (root == null)
        return 0;

    return getTotalHeight(root.left) + getHeight(root) + getTotalHeight(root.right);
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    System.out.println("Sum of heights of all Nodes = " + getTotalHeight(root));
}
}
```

## 蟒蛇 3

```
# Python3 program to find sum of heights
# of all nodes in a binary tree

# Helper class that allocates a new Node
# with the given data and None left and
# right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Compute the "maxHeight" of a
# particular Node
def getHeight(Node):
    if (Node == None):
        return 0
    else:

        # compute the height of each subtree
        lHeight = getHeight(Node.left)
        rHeight = getHeight(Node.right)

        # use the larger one
        if (lHeight > rHeight):
            return (lHeight + 1)
        else:
            return (rHeight + 1)

# Function to sum of heights of
# individual Nodes Uses Inorder traversal
def getTotalHeight(root):
    if (root == None):
        return 0

    return (getTotalHeight(root.left) +
            getHeight(root) +
            getTotalHeight(root.right))

# Driver code
if __name__ == '__main__':
    root = newNode(1)

    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
print("Sum of heights of all Nodes =",
                 getTotalHeight(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find sum of heights of all
// nodes in a binary tree
using System;

class GfG
{

/* A binary tree Node has data, pointer to
    left child and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
}

/* Compute the "maxHeight" of a particular Node*/
static int getHeight(Node Node)
{
    if (Node == null)
        return 0;
    else
    {
        /* compute the height of each subtree */
        int lHeight = getHeight(Node.left);
        int rHeight = getHeight(Node.right);

        /* use the larger one */
        if (lHeight > rHeight)
            return (lHeight + 1);
        else
            return (rHeight + 1);
    }
}

/* Helper function that allocates a new Node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node Node = new Node();
    Node.data = data;
    Node.left = null;
    Node.right = null;

    return (Node);
}

/* Function to sum of heights of individual Nodes
Uses Inorder traversal */
static int getTotalHeight( Node root)
{
    if (root == null)
        return 0;

    return getTotalHeight(root.left) +
                    getHeight(root) +
                    getTotalHeight(root.right);
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    Console.Write("Sum of heights of all Nodes = " + getTotalHeight(root));
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to find sum of heights of all
// nodes in a binary tree

/* A binary tree Node has data, pointer to
left child and a pointer to right child */
class Node
{
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
    }
}

/* Compute the "maxHeight" of a particular Node*/
function getHeight(Node)
{
    if (Node == null)
        return 0;
    else {
        /* compute the height of each subtree */
        let lHeight = getHeight(Node.left);
        let rHeight = getHeight(Node.right);

        /* use the larger one */
        if (lHeight > rHeight)
            return (lHeight + 1);
        else
            return (rHeight + 1);
    }
}

/* Function to sum of heights of individual Nodes
Uses Inorder traversal */
function getTotalHeight(root)
{
    if (root == null)
        return 0;

    return getTotalHeight(root.left) + getHeight(root) + getTotalHeight(root.right);
}

// Driver code
let root = new Node(1);

root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
document.write("Sum of heights of all Nodes = " + getTotalHeight(root));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Sum of heights of all Nodes = 8
```

**时间复杂度:** O(nh)其中 n 是节点总数，h 是二叉树的高度。

**高效解决方案:**

这个想法是计算高度，并在同一个递归调用中对它们求和。

## C++

```
// C++ program to find sum of heights of all
// nodes in a binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree Node has data, pointer to
    left child and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new Node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* Node = (struct Node*)
        malloc(sizeof(struct Node));
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;

    return (Node);
}

/* Function to sum of heights of individual Nodes
   Uses Inorder traversal */
int getTotalHeightUtil(struct Node* root, int &sum)
{
    if (root == NULL)
        return 0;

    int lh = getTotalHeightUtil(root->left, sum);
    int rh = getTotalHeightUtil(root->right, sum);
    int h = max(lh, rh) + 1;

    sum = sum + h;
    return h;
}

int getTotalHeight(Node *root)
{
    int sum = 0;
    getTotalHeightUtil(root, sum);
    return sum;
}

// Driver code
int main()
{
    struct Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    printf("Sum of heights of all Nodes = %d",   
                        getTotalHeight(root));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of heights of all
// nodes in a binary tree
class GFG
{

    /* A binary tree Node has data, pointer to
    left child and a pointer to right child */
    static class Node
    {
        int data;
        Node left;
        Node right;
    };
    static int sum;

    /* Helper function that allocates a new Node with the
    given data and null left and right pointers. */
    static Node newNode(int data)
    {
        Node Node = new Node();
        Node.data = data;
        Node.left = null;
        Node.right = null;

        return (Node);
    }

    /* Function to sum of heights of individual Nodes
    Uses Inorder traversal */
    static int getTotalHeightUtil(Node root)
    {
        if (root == null)
        {
            return 0;
        }

        int lh = getTotalHeightUtil(root.left);
        int rh = getTotalHeightUtil(root.right);
        int h = Math.max(lh, rh) + 1;

        sum = sum + h;
        return h;
    }

    static int getTotalHeight(Node root)
    {
        sum = 0;
        getTotalHeightUtil(root);
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        Node root = newNode(1);

        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        System.out.printf("Sum of heights of all Nodes = %d",
                                       getTotalHeight(root));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find sum of heights
# of all nodes in a binary tree

# A binary tree Node has data, pointer to
# left child and a pointer to right child
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

sum = 0

# Function to sum of heights of individual
# Nodes Uses Inorder traversal
def getTotalHeightUtil(root):

    global sum

    if (root == None):
        return 0

    lh = getTotalHeightUtil(root.left)
    rh = getTotalHeightUtil(root.right)
    h = max(lh, rh) + 1

    sum = sum + h
    return h

def getTotalHeight(root):

    getTotalHeightUtil(root)

    return sum

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    print("Sum of heights of all Nodes =",
           getTotalHeight(root))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find sum of heights of
// all nodes in a binary tree
using System;
using System.Collections.Generic;

class GFG
{

    /* A binary tree Node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        public int data;
        public Node left;
        public Node right;
    };
    static int sum;

    /* Helper function that allocates
    a new Node with the given data and
    null left and right pointers. */
    static Node newNode(int data)
    {
        Node Node = new Node();
        Node.data = data;
        Node.left = null;
        Node.right = null;

        return (Node);
    }

    /* Function to sum of heights of
    individual Nodes Uses Inorder traversal */
    static int getTotalHeightUtil(Node root)
    {
        if (root == null)
        {
            return 0;
        }

        int lh = getTotalHeightUtil(root.left);
        int rh = getTotalHeightUtil(root.right);
        int h = Math.Max(lh, rh) + 1;

        sum = sum + h;
        return h;
    }

    static int getTotalHeight(Node root)
    {
        sum = 0;
        getTotalHeightUtil(root);
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(1);

        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        Console.Write("Sum of heights of all Nodes = {0}",
                                    getTotalHeight(root));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find sum of heights of all
// nodes in a binary tree

/* A binary tree Node has data, pointer to
    left child and a pointer to right child */
class Node
{
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
    }
}

let sum;
/* Function to sum of heights of individual Nodes
    Uses Inorder traversal */
function  getTotalHeightUtil(root)
{
    if (root == null)
        {
            return 0;
        }

        let lh = getTotalHeightUtil(root.left);
        let rh = getTotalHeightUtil(root.right);
        let h = Math.max(lh, rh) + 1;

        sum = sum + h;
        return h;
}

function getTotalHeight(root)
{
    sum = 0;
        getTotalHeightUtil(root);
        return sum;
}

// Driver code
let root = new Node(1);

root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
document.write("Sum of heights of all Nodes = ",
                  getTotalHeight(root));

// This code is contributed by unknown2108

</script>

```

**Output:** 

```
Sum of heights of all Nodes = 8
```

**时间复杂度:** O(n)，其中 n 为二叉树的节点总数。