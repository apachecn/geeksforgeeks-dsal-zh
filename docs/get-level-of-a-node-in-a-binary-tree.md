# 获取二叉树中节点的级别

> 原文:[https://www . geesforgeks . org/get-二进制树中节点的级别/](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)

给定一棵二叉树和一个关键字，编写一个返回关键字级别的函数。
例如，考虑下面的树。如果输入键是 3，那么你的函数应该返回 1。如果输入键是 4，那么你的函数应该返回 3。对于键中不存在的键，您的函数应该返回 0。

![](img/0d1b90ad2012e8b6bbf76e2766bc71bb.png)

想法是从根开始，级别为 1。如果密钥与根的数据匹配，则返回 level。否则递归调用级别为+ 1 的左右子树。

## C++

```
// C++ program to Get Level of a
// node in a Binary Tree
#include<bits/stdc++.h>
using namespace std;

/* A tree node structure */
struct node
{
    int data;
    struct node *left;
    struct node *right;
};

/* Helper function for getLevel().
It returns level of the data if data is
present in tree, otherwise returns 0.*/
int getLevelUtil(struct node *node,
                 int data, int level)
{
    if (node == NULL)
        return 0;

    if (node -> data == data)
        return level;

    int downlevel = getLevelUtil(node -> left,
                                 data, level + 1);
    if (downlevel != 0)
        return downlevel;

    downlevel = getLevelUtil(node->right,
                             data, level + 1);
    return downlevel;
}

/* Returns level of given data value */
int getLevel(struct node *node, int data)
{
    return getLevelUtil(node, data, 1);
}

/* Utility function to create a
new Binary Tree node */
struct node* newNode(int data)
{
    struct node *temp = new struct node;
    temp -> data = data;
    temp -> left = NULL;
    temp -> right = NULL;

    return temp;
}

// Driver Code
int main()
{
    struct node *root = new struct node;
    int x;

    /* Constructing tree given in
    the above figure */
    root = newNode(3);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(4);

    for (x = 1; x <= 5; x++)
    {
        int level = getLevel(root, x);
        if (level)
            cout << "Level of "<< x << " is "
                 << getLevel(root, x) << endl;
        else
            cout << x << "is not present in tree"
                      << endl;
    }

    getchar();
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to Get Level of a node in a Binary Tree
#include<stdio.h>
#include<stdlib.h>

/* A tree node structure */
struct node
{
    int data;
    struct node *left;
    struct node *right;
};

/* Helper function for getLevel(). 
    It returns level of the data if data is
   present in tree, otherwise returns 0.*/
int getLevelUtil(struct node *node,
                 int data, int level)
{
    if (node == NULL)
        return 0;

    if (node->data == data)
        return level;

    int downlevel = getLevelUtil(node->left,
                                 data, level+1);
    if (downlevel != 0)
        return downlevel;

    downlevel = getLevelUtil(node->right,
                             data, level+1);
    return downlevel;
}

/* Returns level of given data value */
int getLevel(struct node *node, int data)
{
    return getLevelUtil(node,data,1);
}

/* Utility function to create
   a new Binary Tree node */
struct node* newNode(int data)
{
    struct node *temp = (struct node*)malloc(sizeof(struct node));
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

/* Driver code */
int main()
{
    struct node *root;
    int x;

    /* Constructing tree given
       in the above figure */
    root = newNode(3);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(4);

    for (x = 1; x <=5; x++)
    {
      int level = getLevel(root, x);
      if (level)
        printf(" Level of %d is %d\n", x, getLevel(root, x));
      else
        printf(" %d is not present in tree \n", x);

    }

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Get Level of a node in a Binary Tree
/* A tree node structure */
class Node {
    int data;
    Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinaryTree {

    Node root;

    /* Helper function for getLevel().
       It returns level of
       the data if data is present in tree,
       otherwise returns
       0.*/
    int getLevelUtil(Node node, int data, int level)
    {
        if (node == null)
            return 0;

        if (node.data == data)
            return level;

        int downlevel
            = getLevelUtil(node.left, data, level + 1);
        if (downlevel != 0)
            return downlevel;

        downlevel
            = getLevelUtil(node.right, data, level + 1);
        return downlevel;
    }

    /* Returns level of given data value */
    int getLevel(Node node, int data)
    {
        return getLevelUtil(node, data, 1);
    }

    /* Driver code */
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Constructing tree given in the above figure */
        tree.root = new Node(3);
        tree.root.left = new Node(2);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(4);
        for (int x = 1; x <= 5; x++)
        {
            int level = tree.getLevel(tree.root, x);
            if (level != 0)
                System.out.println(
                    "Level of " + x + " is "
                    + tree.getLevel(tree.root, x));
            else
                System.out.println(
                    x + " is not present in tree");
        }
    }
}

// This code has been contributed by Mayank
// Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to Get Level of a
# node in a Binary Tree

# Helper function that allocates a
# new node with the given data and
# None left and right pairs.

class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function for getLevel(). It
# returns level of the data if data is
# present in tree, otherwise returns 0

def getLevelUtil(node, data, level):
    if (node == None):
        return 0

    if (node.data == data):
        return level

    downlevel = getLevelUtil(node.left,
                             data, level + 1)
    if (downlevel != 0):
        return downlevel

    downlevel = getLevelUtil(node.right,
                             data, level + 1)
    return downlevel

# Returns level of given data value

def getLevel(node, data):

    return getLevelUtil(node, data, 1)

# Driver Code
if __name__ == '__main__':

    # Let us construct the Tree shown
    # in the above figure
    root = newNode(3)
    root.left = newNode(2)
    root.right = newNode(5)
    root.left.left = newNode(1)
    root.left.right = newNode(4)
    for x in range(1, 6):
        level = getLevel(root, x)
        if (level):
            print("Level of", x,
                  "is", getLevel(root, x))
        else:
            print(x, "is not present in tree")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to Get Level of a node in a Binary Tree
using System;

/* A tree node structure */
public class Node {
    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinaryTree {

    public Node root;

    /* Helper function for getLevel().
       It returns level of
       the data if data is present in tree,
      otherwise returns
    0.*/
    public virtual int getLevelUtil(Node node, int data,
                                    int level)
    {
        if (node == null)
        {
            return 0;
        }

        if (node.data == data)
        {
            return level;
        }

        int downlevel
            = getLevelUtil(node.left, data, level + 1);
        if (downlevel != 0)
        {
            return downlevel;
        }

        downlevel
            = getLevelUtil(node.right, data, level + 1);
        return downlevel;
    }

    /* Returns level of given data value */
    public virtual int getLevel(Node node, int data)
    {
        return getLevelUtil(node, data, 1);
    }

    /* Driver code */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Constructing tree given in the above figure */
        tree.root = new Node(3);
        tree.root.left = new Node(2);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(4);
        for (int x = 1; x <= 5; x++)
        {
            int level = tree.getLevel(tree.root, x);
            if (level != 0)
            {
                Console.WriteLine(
                    "Level of " + x + " is "
                    + tree.getLevel(tree.root, x));
            }
            else
            {
                Console.WriteLine(
                    x + " is not present in tree");
            }
        }
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // Javascript program to Get Level of
    // a node in a Binary Tree
    /* A tree node structure */

    class Node
    {
        constructor(d) {
              this.data = d;
            this.left = null;
            this.right = null;
        }
    }

    let root;

    /* Helper function for getLevel().
       It returns level of
       the data if data is present in tree,
       otherwise returns
       0.*/
    function getLevelUtil(node, data, level)
    {
        if (node == null)
            return 0;

        if (node.data == data)
            return level;

        let downlevel
            = getLevelUtil(node.left, data, level + 1);
        if (downlevel != 0)
            return downlevel;

        downlevel
            = getLevelUtil(node.right, data, level + 1);
        return downlevel;
    }

    /* Returns level of given data value */
    function getLevel(node, data)
    {
        return getLevelUtil(node, data, 1);
    }

    /* Constructing tree given in the above figure */
    root = new Node(3);
    root.left = new Node(2);
    root.right = new Node(5);
    root.left.left = new Node(1);
    root.left.right = new Node(4);
    for (let x = 1; x <= 5; x++)
    {
      let level = getLevel(root, x);
      if (level != 0)
        document.write(
          "Level of " + x + " is "
          + getLevel(root, x) + "</br>");
      else
        document.write(
          x + " is not present in tree");
    }

</script>
```

**Output**

```
Level of 1 is 3
Level of 2 is 2
Level of 3 is 1
Level of 4 is 3
Level of 5 is 2
```

getLevel()的时间复杂度是 O(n)，其中 n 是给定二叉树中的节点数。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。