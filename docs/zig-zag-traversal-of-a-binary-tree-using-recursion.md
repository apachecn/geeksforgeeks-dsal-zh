# 使用递归对二叉树进行之字形遍历

> 原文:[https://www . geesforgeks . org/zig-zag-遍历二叉树-使用递归/](https://www.geeksforgeeks.org/zig-zag-traversal-of-a-binary-tree-using-recursion/)

给定一棵二叉树，任务是打印树的之字形顺序。
**例:**

```
Input : 
          7
         / \
        6   5
       /   /
      4   3
     /     \
    2       1
Output : 7 5 6 4 3 1 2

Input :
      1
     / \
    2   3
   / \    
  4   5
Output : 1 3 2 4 5
```

我们已经讨论了使用迭代方法的[之字形遍历](https://www.geeksforgeeks.org/?p=166840)，在这篇文章中，我们将使用递归来解决它。
**递归方法:**想法是以[级顺序](https://www.geeksforgeeks.org/level-order-tree-traversal/)的方式遍历树，但方式略有不同。我们将使用一个变量**标记**，并最初将其值设置为零。当我们完成树的级别顺序遍历时，从右到左，我们将把**标志**的值设置为 1，这样下次我们可以从左到右遍历树，当我们完成遍历时，我们将把它的值设置回零。我们将重复这整个步骤，直到我们完全遍历了二叉树。
以下是上述方法的实施:

## C++

```
// C++ program to print zigzag
// traversal of a binary tree
// using Recursion

#include<bits/stdc++.h>
using namespace std;

// Binary tree node
struct node
{
    struct node* left;
    struct node* right;
    int data;
};

// Function to create a new
// Binary Tree Node
struct node* newNode(int data)
{
    struct node* temp = new node;

    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// Recursive Function to find height
// of binary tree
int heightOfTree(struct node* root)
{
    if(root == NULL)
    return 0;

    int lheight = heightOfTree(root->left);
    int rheight = heightOfTree(root->right);

    return max(lheight + 1 ,rheight + 1);
}

// Function to print nodes from right to left
void printRightToLeft(struct node* root ,int level)
{
    if(root == NULL)
    return;

    if(level == 1)
    cout << root->data << " " ;

    else if(level > 1)
    {
        printRightToLeft(root->right ,level - 1);
        printRightToLeft(root->left ,level - 1);
    }
}

// Function to print nodes from left to right
void printLeftToRight(struct node* root ,int level)
{
    if(root == NULL)
    return;

    if(level == 1)
    cout << root->data << " " ;

    else if(level > 1)
    {
        printLeftToRight(root->left ,level - 1);
        printLeftToRight(root->right ,level - 1);
    }
}

// Function to print Reverse ZigZag of
// a Binary tree
void printZigZag(struct node* root )
{
    // Flag is used to mark the change
    // in level
    int flag = 0;

    // Height of tree
    int height = heightOfTree(root);

    for(int i = 1 ; i <= height ; i++)
    {
        // If flag value is one print nodes
        // from right to left
        if(flag == 1)
        {
            printRightToLeft(root ,i);

            // Mark flag as zero so that next time
            // nodes are printed from left to right
            flag = 0;
        }
        // If flag is zero print nodes
        // from left to right
        else if(flag == 0)
        {
            printLeftToRight(root ,i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
int main()
{
    struct node* root = newNode(7);
    root->left = newNode(4);
    root->right = newNode(5);
    root->left->left = newNode(9);
    root->right->right = newNode(10);
    root->left->left->left = newNode(6);
    root->left->left->right = newNode(11);

    printZigZag(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print zigzag
// traversal of a binary tree
// using Recursion

class GfG
{

// Binary tree node
static class node
{
    node left;
    node right;
    int data;
}

// Function to create a new
// Binary Tree Node
static node newNode(int data)
{
    node temp = new node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Recursive Function to find height
// of binary tree
static int heightOfTree(node root)
{
    if(root == null)
    return 0;

    int lheight = heightOfTree(root.left);
    int rheight = heightOfTree(root.right);

    return Math.max(lheight + 1 ,rheight + 1);
}

// Function to print nodes from right to left
static void printRightToLeft(node root ,int level)
{
    if(root == null)
    return;

    if(level == 1)
    System.out.print(root.data + " ") ;

    else if(level > 1)
    {
        printRightToLeft(root.right ,level - 1);
        printRightToLeft(root.left ,level - 1);
    }
}

// Function to print nodes from left to right
static void printLeftToRight(node root ,int level)
{
    if(root == null)
    return;

    if(level == 1)
    System.out.print(root.data + " ") ;

    else if(level > 1)
    {
        printLeftToRight(root.left ,level - 1);
        printLeftToRight(root.right ,level - 1);
    }
}

// Function to print Reverse ZigZag of
// a Binary tree
static void printZigZag(node root )
{
    // Flag is used to mark the change
    // in level
    int flag = 0;

    // Height of tree
    int height = heightOfTree(root);

    for(int i = 1 ; i <= height ; i++)
    {
        // If flag value is one print nodes
        // from right to left
        if(flag == 1)
        {
            printRightToLeft(root ,i);

            // Mark flag as zero so that next time
            // nodes are printed from left to right
            flag = 0;
        }
        // If flag is zero print nodes
        // from left to right
        else if(flag == 0)
        {
            printLeftToRight(root ,i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    node root = newNode(7);
    root.left = newNode(4);
    root.right = newNode(5);
    root.left.left = newNode(9);
    root.right.right = newNode(10);
    root.left.left.left = newNode(6);
    root.left.left.right = newNode(11);

    printZigZag(root);
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to print zigzag traversal
# of a binary tree using Recursion

# Binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive Function to find height
# of binary tree
def heightOfTree(root):

    if root == None:
        return 0

    lheight = heightOfTree(root.left)
    rheight = heightOfTree(root.right)

    return max(lheight + 1, rheight + 1)

# Function to print nodes from right to left
def printRightToLeft(root, level):

    if root == None:
        return

    if level == 1:
        print(root.data, end = " ")

    elif level > 1:

        printRightToLeft(root.right, level - 1)
        printRightToLeft(root.left, level - 1)

# Function to print nodes from left to right
def printLeftToRight(root, level):

    if root == None:
        return

    if level == 1:
        print(root.data, end = " ")

    elif level > 1:

        printLeftToRight(root.left, level - 1)
        printLeftToRight(root.right, level - 1)

# Function to print Reverse ZigZag of
# a Binary tree
def printZigZag(root):

    # Flag is used to mark the
    # change in level
    flag = 0

    # Height of tree
    height = heightOfTree(root)

    for i in range(1, height + 1):

        # If flag value is one print nodes
        # from right to left
        if flag == 1:

            printRightToLeft(root, i)

            # Mark flag as zero so that next time
            # nodes are printed from left to right
            flag = 0

        # If flag is zero print nodes
        # from left to right
        elif flag == 0:

            printLeftToRight(root, i)

            # Mark flag as one so that next time
            # nodes are printed from right to left
            flag = 1

# Driver code
if __name__ == "__main__":

    root = Node(7)
    root.left = Node(4)
    root.right = Node(5)
    root.left.left = Node(9)
    root.right.right = Node(10)
    root.left.left.left = Node(6)
    root.left.left.right = Node(11)

    printZigZag(root)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print zigzag
// traversal of a binary tree
// using Recursion
using System;

class GfG
{

// Binary tree node
public class node
{
    public node left;
    public node right;
    public int data;
}

// Function to create a new
// Binary Tree Node
static node newNode(int data)
{
    node temp = new node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Recursive Function to find height
// of binary tree
static int heightOfTree(node root)
{
    if(root == null)
    return 0;

    int lheight = heightOfTree(root.left);
    int rheight = heightOfTree(root.right);

    return Math.Max(lheight + 1 ,rheight + 1);
}

// Function to print nodes from right to left
static void printRightToLeft(node root ,int level)
{
    if(root == null)
    return;

    if(level == 1)
    Console.Write(root.data + " ") ;

    else if(level > 1)
    {
        printRightToLeft(root.right ,level - 1);
        printRightToLeft(root.left ,level - 1);
    }
}

// Function to print nodes from left to right
static void printLeftToRight(node root ,int level)
{
    if(root == null)
    return;

    if(level == 1)
    Console.Write(root.data + " ") ;

    else if(level > 1)
    {
        printLeftToRight(root.left ,level - 1);
        printLeftToRight(root.right ,level - 1);
    }
}

// Function to print Reverse ZigZag of
// a Binary tree
static void printZigZag(node root )
{
    // Flag is used to mark the change
    // in level
    int flag = 0;

    // Height of tree
    int height = heightOfTree(root);

    for(int i = 1 ; i <= height ; i++)
    {
        // If flag value is one print nodes
        // from right to left
        if(flag == 1)
        {
            printRightToLeft(root, i);

            // Mark flag as zero so that next time
            // nodes are printed from left to right
            flag = 0;
        }
        // If flag is zero print nodes
        // from left to right
        else if(flag == 0)
        {
            printLeftToRight(root, i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
public static void Main()
{
    node root = newNode(7);
    root.left = newNode(4);
    root.right = newNode(5);
    root.left.left = newNode(9);
    root.right.right = newNode(10);
    root.left.left.left = newNode(6);
    root.left.left.right = newNode(11);

    printZigZag(root);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript program to print zigzag
    // traversal of a binary tree
    // using Recursion

    // Binary tree node
    class node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create a new
    // Binary Tree Node
    function newNode(data)
    {
        let temp = new node(data);
        return temp;
    }

    // Recursive Function to find height
    // of binary tree
    function heightOfTree(root)
    {
        if(root == null)
            return 0;

        let lheight = heightOfTree(root.left);
        let rheight = heightOfTree(root.right);

        return Math.max(lheight + 1 ,rheight + 1);
    }

    // Function to print nodes from right to left
    function printRightToLeft(root, level)
    {
        if(root == null)
            return;

        if(level == 1)
            document.write(root.data + " ") ;

        else if(level > 1)
        {
            printRightToLeft(root.right ,level - 1);
            printRightToLeft(root.left ,level - 1);
        }
    }

    // Function to print nodes from left to right
    function printLeftToRight(root, level)
    {
        if(root == null)
            return;

        if(level == 1)
            document.write(root.data + " ") ;

        else if(level > 1)
        {
            printLeftToRight(root.left ,level - 1);
            printLeftToRight(root.right ,level - 1);
        }
    }

    // Function to print Reverse ZigZag of
    // a Binary tree
    function printZigZag(root)
    {
        // Flag is used to mark the change
        // in level
        let flag = 0;

        // Height of tree
        let height = heightOfTree(root);

        for(let i = 1 ; i <= height ; i++)
        {
            // If flag value is one print nodes
            // from right to left
            if(flag == 1)
            {
                printRightToLeft(root ,i);

                // Mark flag as zero so that next time
                // nodes are printed from left to right
                flag = 0;
            }
            // If flag is zero print nodes
            // from left to right
            else if(flag == 0)
            {
                printLeftToRight(root ,i);

                // Mark flag as one so that next time
                // nodes are printed from right to left
                flag = 1;
            }
        }
    }

    let root = newNode(7);
    root.left = newNode(4);
    root.right = newNode(5);
    root.left.left = newNode(9);
    root.right.right = newNode(10);
    root.left.left.left = newNode(6);
    root.left.left.right = newNode(11);

    printZigZag(root);

</script>
```

**Output:** 

```
7 5 4 9 10 11 6        
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)