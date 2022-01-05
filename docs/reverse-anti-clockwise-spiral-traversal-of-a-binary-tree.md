# 二叉树的反逆时针螺旋遍历

> 原文:[https://www . geesforgeks . org/reverse-逆时针-螺旋-遍历二叉树/](https://www.geeksforgeeks.org/reverse-anti-clockwise-spiral-traversal-of-a-binary-tree/)

给定一棵二叉树，任务是以反逆时针螺旋方式打印树的节点。

**示例:**

```
Input : 
          1
         /  \
        2    3
       / \    \
      4   5    6
         /    / \
        7    8   9
Output : 7 8 9 1 4 5 6 3 2

Input :
           20
         /   \
        8     22
      /   \  /   \
     5     3 4    25
          / \
         10  14
Output : 10 14 20 5 3 4 25 22 8
```

**方法:**想法是用两个变量 I 初始化为 1，j 初始化为树高，运行一个 while 循环，直到我变得大于 j 才会中断。我们将使用另一个变量**标记**并将其初始化为 1。现在在 while 循环中，我们将检查一个条件，如果**标志**等于 1，我们将从左到右遍历树并将**标志**标记为 0，以便下次我们从右到左遍历树，然后递减 j 的值，以便下次我们访问刚好在当前级别之上的级别。同样，当我们从顶部遍历级别时，我们将把**标记**标记为 1，以便下次我们从左向右遍历树，然后增加 I 的值，以便下次我们访问当前级别之下的级别。重复整个过程，直到二叉树被完全遍历。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    struct Node* left;
    struct Node* right;
    int data;

    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Recursive Function to find height
// of binary tree
int height(struct Node* root)
{
    // Base condition
    if (root == NULL)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root->left);
    int rheight = height(root->right);

    // Return the maximum of two
    return max(1 + lheight, 1 + rheight);
}

// Function to Print Nodes from left to right
void leftToRight(struct Node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        leftToRight(root->left, level - 1);
        leftToRight(root->right, level - 1);
    }
}

// Function to Print Nodes from right to left
void rightToLeft(struct Node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        rightToLeft(root->right, level - 1);
        rightToLeft(root->left, level - 1);
    }
}

// Function to print Reverse anti clockwise spiral
// traversal of a binary tree
void ReverseAntiClockWiseSpiral(struct Node* root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 1;
    while (i <= j) {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0) {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
int main()
{
    struct Node* root = new Node(20);
    root->left = new Node(8);
    root->right = new Node(22);
    root->left->left = new Node(5);
    root->left->right = new Node(3);
    root->right->left = new Node(4);
    root->right->right = new Node(25);
    root->left->right->left = new Node(10);
    root->left->right->right = new Node(14);

    ReverseAntiClockWiseSpiral(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Binary tree node
static class Node
{
    Node left;
    Node right;
    int data;

    Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Recursive Function to find height
// of binary tree
static int height(Node root)
{
    // Base condition
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root.left);
    int rheight = height(root.right);

    // Return the maximum of two
    return Math.max(1 + lheight, 1 + rheight);
}

// Function to Print Nodes from left to right
static void leftToRight(Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);
    }
}

// Function to Print Nodes from right to left
static void rightToLeft( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print Reverse anti clockwise spiral
// traversal of a binary tree
static void ReverseAntiClockWiseSpiral(Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 1;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else
        {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(20);
    root.left = new Node(8);
    root.right = new Node(22);
    root.left.left = new Node(5);
    root.left.right = new Node(3);
    root.right.left = new Node(4);
    root.right.right = new Node(25);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(14);

    ReverseAntiClockWiseSpiral(root);

}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Binary tree node
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

# Recursive Function to find height
# of binary tree
def height(root):

    # Base condition
    if (root == None):
        return 0;

    # Compute the height of each subtree
    lheight = height(root.left)
    rheight = height(root.right)

    # Return the maximum of two
    return max(1 + lheight, 1 + rheight)

# Function to Print Nodes
# from left to right
def leftToRight(root, level):

    if (root == None):
        return

    if (level == 1):
        print(root.data, end = " ")

    elif (level > 1):
        leftToRight(root.left, level - 1)
        leftToRight(root.right, level - 1)

# Function to Print Nodes from
# right to left
def rightToLeft(root, level):

    if (root == None):
        return

    if (level == 1):
        print(root.data, end = " ")

    elif(level > 1):
        rightToLeft(root.right, level - 1)
        rightToLeft(root.left, level - 1)

# Function to print Reverse anti clockwise
# spiral traversal of a binary tree
def ReverseAntiClockWiseSpiral(root):

    i = 1
    j = height(root)

    # Flag to mark a change in the
    # direction of printing nodes
    flag = 1;

    while (i <= j):

        # If flag is zero print nodes
        # from right to left
        if (flag == 0):
            rightToLeft(root, i)

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from left to right
            flag = 1

            # Increment i
            i += 1

        # If flag is one print nodes
        # from left to right
        else:
            leftToRight(root, j)

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from right to left
            flag = 0

            # Decrement j
            j -= 1

# Driver code
if __name__=="__main__":

    root = Node(20)
    root.left = Node(8)
    root.right = Node(22)
    root.left.left = Node(5)
    root.left.right = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(25)
    root.left.right.left = Node(10)
    root.left.right.right = Node(14)

    ReverseAntiClockWiseSpiral(root)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

// Binary tree node
public class Node
{
    public Node left;
    public Node right;
    public int data;

    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Recursive Function to find height
// of binary tree
static int height(Node root)
{
    // Base condition
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root.left);
    int rheight = height(root.right);

    // Return the maximum of two
    return Math.Max(1 + lheight, 1 + rheight);
}

// Function to Print Nodes from left to right
static void leftToRight(Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write(root.data + " ");

    else if (level > 1)
    {
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);
    }
}

// Function to Print Nodes from right to left
static void rightToLeft( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write(root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print Reverse anti clockwise spiral
// traversal of a binary tree
static void ReverseAntiClockWiseSpiral(Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 1;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else
        {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    Node root = new Node(20);
    root.left = new Node(8);
    root.right = new Node(22);
    root.left.left = new Node(5);
    root.left.right = new Node(3);
    root.right.left = new Node(4);
    root.right.right = new Node(25);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(14);

    ReverseAntiClockWiseSpiral(root);

}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Recursive Function to find height
    // of binary tree
    function height(root)
    {
        // Base condition
        if (root == null)
            return 0;

        // Compute the height of each subtree
        let lheight = height(root.left);
        let rheight = height(root.right);

        // Return the maximum of two
        return Math.max(1 + lheight, 1 + rheight);
    }

    // Function to Print Nodes from left to right
    function leftToRight(root, level)
    {
        if (root == null)
            return;

        if (level == 1)
            document.write(root.data + " ");

        else if (level > 1)
        {
            leftToRight(root.left, level - 1);
            leftToRight(root.right, level - 1);
        }
    }

    // Function to Print Nodes from right to left
    function rightToLeft(root, level)
    {
        if (root == null)
            return;

        if (level == 1)
            document.write(root.data + " ");

        else if (level > 1)
        {
            rightToLeft(root.right, level - 1);
            rightToLeft(root.left, level - 1);
        }
    }

    // Function to print Reverse anti clockwise spiral
    // traversal of a binary tree
    function ReverseAntiClockWiseSpiral(root)
    {
        let i = 1;
        let j = height(root);

        // Flag to mark a change in the direction
        // of printing nodes
        let flag = 1;
        while (i <= j)
        {

            // If flag is zero print nodes
            // from right to left
            if (flag == 0)
            {
                rightToLeft(root, i);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from left to right
                flag = 1;

                // Increment i
                i++;
            }

            // If flag is one print nodes
            // from left to right
            else
            {
                leftToRight(root, j);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from right to left
                flag = 0;

                // Decrement j
                j--;
            }
        }
    }

    let root = new Node(20);
    root.left = new Node(8);
    root.right = new Node(22);
    root.left.left = new Node(5);
    root.left.right = new Node(3);
    root.right.left = new Node(4);
    root.right.right = new Node(25);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(14);

    ReverseAntiClockWiseSpiral(root);

</script>
```

**Output:** 

```
10 14 20 5 3 4 25 22 8    
```

**时间复杂度** : O(N^2)，其中 n 是二叉树中节点的总数。
**辅助空间:** O(N)