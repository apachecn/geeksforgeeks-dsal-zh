# 二叉树的反向之字形遍历

> 原文:[https://www . geeksforgeeks . org/二叉树逆向曲折遍历/](https://www.geeksforgeeks.org/reverse-zigzag-traversal-of-a-binary-tree/)

给定一棵二叉树，任务是打印树的倒锯齿形顺序。
**例:**

```
Input:
     1
   /  \
  2    3
 / \    \
4   5    6
Output: 6 5 4 2 3 1

Input:
      5
     / \
    9   3
   /     \
  6       4
 / \
8   7
Output: 7 8 6 4 3 9 5
```

**方法:**想法是以[反向水平顺序](https://www.geeksforgeeks.org/reverse-level-order-traversal/)的方式遍历树，但稍加修改。我们将使用一个变量**标记**，并将其值设置为 1。当我们完成树的反向级别顺序遍历时，从右到左，我们将把**标志**的值设置为零，这样下次我们从左到右遍历树时，当我们完成遍历时，我们把它的值设置回 1。我们将重复这整个步骤，直到我们完全遍历了二叉树。
以下是上述方法的实施:

## C++

```
// C++ program to print reverse
// zigzag order of binary tree
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct node {
    struct node* left;
    struct node* right;
    int data;
};

// Function to create a new
// Binary node
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
int HeightOfTree(struct node* root)
{
    if (root == NULL)
        return 0;

    // Compute the height of each subtree
    int lheight = HeightOfTree(root->left);
    int rheight = HeightOfTree(root->right);

    // Return the maximum of two
    return max(lheight + 1, rheight + 1);
}

// Function to Print nodes from right to left
void Print_Level_Right_To_Left(struct node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        Print_Level_Right_To_Left(root->right, level - 1);
        Print_Level_Right_To_Left(root->left, level - 1);
    }
}

// Function to Print nodes from left to right
void Print_Level_Left_To_Right(struct node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        Print_Level_Left_To_Right(root->left, level - 1);
        Print_Level_Left_To_Right(root->right, level - 1);
    }
}

// Function to print Reverse zigzag of
// a Binary tree
void PrintReverseZigZag(struct node* root)
{
    // Flag is used to mark the change
    // in level
    int flag = 1;

    // Height of tree
    int height = HeightOfTree(root);

    for (int i = height; i >= 1; i--) {

        // If flag value is one print nodes
        // from right to left
        if (flag == 1) {
            Print_Level_Right_To_Left(root, i);

            // Mark flag as zero so that next time
            // tree is traversed from left to right
            flag = 0;
        }

        // If flag is zero print nodes
        // from left to right
        else if (flag == 0) {
            Print_Level_Left_To_Right(root, i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
int main()
{
    struct node* root = newNode(5);
    root->left = newNode(9);
    root->right = newNode(3);
    root->left->left = newNode(6);
    root->right->right = newNode(4);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(7);

    PrintReverseZigZag(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print reverse
// zigzag order of binary tree
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
// Binary node
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
static int HeightOfTree(node root)
{
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = HeightOfTree(root.left);
    int rheight = HeightOfTree(root.right);

    // Return the maximum of two
    return Math.max(lheight + 1, rheight + 1);
}

// Function to Print nodes from right to left
static void Print_Level_Right_To_Left(node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        Print_Level_Right_To_Left(root.right, level - 1);
        Print_Level_Right_To_Left(root.left, level - 1);
    }
}

// Function to Print nodes from left to right
static void Print_Level_Left_To_Right(node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        Print_Level_Left_To_Right(root.left, level - 1);
        Print_Level_Left_To_Right(root.right, level - 1);
    }
}

// Function to print Reverse zigzag of
// a Binary tree
static void PrintReverseZigZag(node root)
{
    // Flag is used to mark the change
    // in level
    int flag = 1;

    // Height of tree
    int height = HeightOfTree(root);

    for (int i = height; i >= 1; i--)
    {

        // If flag value is one print nodes
        // from right to left
        if (flag == 1)
        {
            Print_Level_Right_To_Left(root, i);

            // Mark flag as zero so that next time
            // tree is traversed from left to right
            flag = 0;
        }

        // If flag is zero print nodes
        // from left to right
        else if (flag == 0)
        {
            Print_Level_Left_To_Right(root, i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    node root = newNode(5);
    root.left = newNode(9);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.right.right = newNode(4);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(7);

    PrintReverseZigZag(root);
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to print reverse
# zigzag order of binary tree

# Binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive Function to find
# height of binary tree
def HeightOfTree(root):

    if root == None:
        return 0

    # Compute the height of each subtree
    lheight = HeightOfTree(root.left)
    rheight = HeightOfTree(root.right)

    # Return the maximum of two
    return max(lheight + 1, rheight + 1)

# Function to Print nodes from right to left
def Print_Level_Right_To_Left(root, level):

    if root == None:
        return

    if level == 1:
        print(root.data, end = " ")

    elif level > 1:
        Print_Level_Right_To_Left(root.right,
                                  level - 1)
        Print_Level_Right_To_Left(root.left,
                                  level - 1)

# Function to Print nodes from left to right
def Print_Level_Left_To_Right(root, level):

    if root == None:
        return

    if level == 1:
        print(root.data, end = " ")

    elif level > 1:
        Print_Level_Left_To_Right(root.left,   
                                  level - 1)
        Print_Level_Left_To_Right(root.right,
                                  level - 1)

# Function to print Reverse
# zigzag of a Binary tree
def PrintReverseZigZag(root):

    # Flag is used to mark the
    # change in level
    flag = 1

    # Height of tree
    height = HeightOfTree(root)

    for i in range(height, 0, -1):

        # If flag value is one print
        # nodes from right to left
        if flag == 1:
            Print_Level_Right_To_Left(root, i)

            # Mark flag as zero so that next time
            # tree is traversed from left to right
            flag = 0

        # If flag is zero print nodes
        # from left to right
        elif flag == 0:
            Print_Level_Left_To_Right(root, i)

            # Mark flag as one so that next time
            # nodes are printed from right to left
            flag = 1

# Driver code
if __name__ == "__main__":

    root = Node(5)
    root.left = Node(9)
    root.right = Node(3)
    root.left.left = Node(6)
    root.right.right = Node(4)
    root.left.left.left = Node(8)
    root.left.left.right = Node(7)

    PrintReverseZigZag(root)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print reverse
// zigzag order of binary tree
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
// Binary node
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
static int HeightOfTree(node root)
{
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = HeightOfTree(root.left);
    int rheight = HeightOfTree(root.right);

    // Return the maximum of two
    return Math.Max(lheight + 1, rheight + 1);
}

// Function to Print nodes from right to left
static void Print_Level_Right_To_Left(node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write(root.data + " ");

    else if (level > 1)
    {
        Print_Level_Right_To_Left(root.right, level - 1);
        Print_Level_Right_To_Left(root.left, level - 1);
    }
}

// Function to Print nodes from left to right
static void Print_Level_Left_To_Right(node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write(root.data + " ");

    else if (level > 1)
    {
        Print_Level_Left_To_Right(root.left, level - 1);
        Print_Level_Left_To_Right(root.right, level - 1);
    }
}

// Function to print Reverse zigzag of
// a Binary tree
static void PrintReverseZigZag(node root)
{
    // Flag is used to mark the change
    // in level
    int flag = 1;

    // Height of tree
    int height = HeightOfTree(root);

    for (int i = height; i >= 1; i--)
    {

        // If flag value is one print nodes
        // from right to left
        if (flag == 1)
        {
            Print_Level_Right_To_Left(root, i);

            // Mark flag as zero so that next time
            // tree is traversed from left to right
            flag = 0;
        }

        // If flag is zero print nodes
        // from left to right
        else if (flag == 0)
        {
            Print_Level_Left_To_Right(root, i);

            // Mark flag as one so that next time
            // nodes are printed from right to left
            flag = 1;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    node root = newNode(5);
    root.left = newNode(9);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.right.right = newNode(4);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(7);

    PrintReverseZigZag(root);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript program to print reverse
    // zigzag order of binary tree

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
    // Binary node
    function newNode(data)
    {
        let temp = new node(data);
        return temp;
    }

    // Recursive Function to find height
    // of binary tree
    function HeightOfTree(root)
    {
        if (root == null)
            return 0;

        // Compute the height of each subtree
        let lheight = HeightOfTree(root.left);
        let rheight = HeightOfTree(root.right);

        // Return the maximum of two
        return Math.max(lheight + 1, rheight + 1);
    }

    // Function to Print nodes from right to left
    function Print_Level_Right_To_Left(root, level)
    {
        if (root == null)
            return;

        if (level == 1)
            document.write(root.data + " ");

        else if (level > 1)
        {
            Print_Level_Right_To_Left(root.right, level - 1);
            Print_Level_Right_To_Left(root.left, level - 1);
        }
    }

    // Function to Print nodes from left to right
    function Print_Level_Left_To_Right(root, level)
    {
        if (root == null)
            return;

        if (level == 1)
            document.write(root.data + " ");

        else if (level > 1)
        {
            Print_Level_Left_To_Right(root.left, level - 1);
            Print_Level_Left_To_Right(root.right, level - 1);
        }
    }

    // Function to print Reverse zigzag of
    // a Binary tree
    function PrintReverseZigZag(root)
    {
        // Flag is used to mark the change
        // in level
        let flag = 1;

        // Height of tree
        let height = HeightOfTree(root);

        for (let i = height; i >= 1; i--)
        {

            // If flag value is one print nodes
            // from right to left
            if (flag == 1)
            {
                Print_Level_Right_To_Left(root, i);

                // Mark flag as zero so that next time
                // tree is traversed from left to right
                flag = 0;
            }

            // If flag is zero print nodes
            // from left to right
            else if (flag == 0)
            {
                Print_Level_Left_To_Right(root, i);

                // Mark flag as one so that next time
                // nodes are printed from right to left
                flag = 1;
            }
        }
    }

    let root = newNode(5);
    root.left = newNode(9);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.right.right = newNode(4);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(7);

    PrintReverseZigZag(root);

</script>
```

**Output:** 

```
7 8 6 4 3 9 5
```

**时间复杂度** :O(N^2，其中 n 是二叉树中的节点数。
**辅助空间:** O(N)