# 二叉树的逆时针螺旋遍历

> 原文:[https://www . geesforgeks . org/逆向-顺时针-螺旋-遍历二叉树/](https://www.geeksforgeeks.org/reverse-clockwise-spiral-traversal-of-a-binary-tree/)

给定一棵二叉树。任务是打印给定二叉树的循环反向顺时针螺旋顺序遍历。
逆时针遍历是指从底部而不是顶部根节点开始，以顺时针方向螺旋遍历树。
**举例:**

```
Input : 
          1
         /  \
        2    3
       / \    \
      4   5    6
         /    / \
        7    8   9
Output : 9 8 7 1 6 5 4 2 3

Input :
           20
         /   \
        8     22
      /   \  /   \
     5     3 4    25
          / \
         10  14
Output : 14 10 20 25 4 3 5 8 22
```

**方法:**想法是使用初始化为 1 的两个变量 **i** 和初始化为树高的 **j** ，运行一个 while 循环，直到 *i 大于 j* 为止。

*   使用另一个变量**标记**，并将其初始化为 0。现在在 while 循环中，检查一个条件，如果**标志**等于 0，则从右向左遍历树，并将**标志**标记为 1，以便下次我们从左向右遍历树时，这样做是为了保持螺旋顺时针遍历顺序。
*   然后递减 j 的值，以便下次访问刚好在当前级别之上的级别。
*   此外，当我们从顶部遍历级别时，我们将标记**标志**为 0，以便下次我们从右向左遍历树，然后增加 I 的值，以便下次我们访问当前级别以下的级别。
*   重复整个过程，直到二叉树被完全遍历。

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

// Function to print reverse clockwise spiral
// traversal of a binary tree
void ReverseClockWiseSpiral(struct Node* root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j) {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0) {
            rightToLeft(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Decrement j
            j--;
        }

        // If flag is one print nodes
        // from left to right
        else {
            leftToRight(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Increment i
            i++;
        }
    }
}

// Driver code
int main()
{
    struct Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(6);
    root->right->right = new Node(7);
    root->left->right = new Node(5);

    ReverseClockWiseSpiral(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
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
};

// Recursive Function to find height
// of binary tree
static int height( Node root)
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
static void leftToRight( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print( root.data + " ");

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
        System.out.print( root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print reverse clockwise spiral
// traversal of a binary tree
static void ReverseClockWiseSpiral( Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Decrement j
            j--;
        }

        // If flag is one print nodes
        // from left to right
        else
        {
            leftToRight(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Increment i
            i++;
        }
    }
}

// Driver code
public static void main(String args[])
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.right = new Node(5);

    ReverseClockWiseSpiral(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Binary tree node
class Node:

    def __init__(self,data):

        self.left = None
        self.right = None
        self.data = data;

# Recursive Function to find height
# of binary tree
def height(root):

    # Base condition
    if (root == None):
        return 0;

    # Compute the height of each subtree
    lheight = height(root.left);
    rheight = height(root.right);

    # Return the maximum of two
    return max(1 + lheight, 1 + rheight);

# Function to Print Nodes from
# left to right
def leftToRight(root, level):

    if (root == None):
        return;

    if (level == 1):
        print(root.data, end = " ")

    elif (level > 1):
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);

# Function to Print Nodes
# from right to left
def rightToLeft(root, level):

    if (root == None):
        return;

    if (level == 1):
        print(root.data, end = " ")

    elif (level > 1):
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);

# Function to print Reverse clockwise
# spiral traversal of a binary tree
def ReverseClockWiseSpiral(root):

    i = 1;
    j = height(root);

    # Flag to mark a change in the
    # direction of printing nodes
    flag = 0;

    while (i <= j):

        # If flag is zero print nodes
        # from right to left
        if (flag == 0):
            rightToLeft(root, j);

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from left to right
            flag = 1;

            # Increment i
            j -= 1;

        # If flag is one print nodes
        # from left to right
        else:
            leftToRight(root, i);

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from right to left
            flag = 0;

            # Decrement j
            i += 1;

# Driver code
if __name__=="__main__":

    root = Node(1);
    root.left = Node(2);
    root.right = Node(3);
    root.left.left = Node(4);
    root.right.left = Node(6);
    root.right.right = Node(7);
    root.left.right = Node(5);

    ReverseClockWiseSpiral(root);

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the approach
using System;

class GFG
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
};

// Recursive Function to find height
// of binary tree
static int height( Node root)
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
static void leftToRight( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write( root.data + " ");

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
        Console.Write( root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print reverse clockwise spiral
// traversal of a binary tree
static void ReverseClockWiseSpiral( Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Decrement j
            j--;
        }

        // If flag is one print nodes
        // from left to right
        else
        {
            leftToRight(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Increment i
            i++;
        }
    }
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.right = new Node(5);

    ReverseClockWiseSpiral(root);
}
}

// This code contributed by Rajput-Ji
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
            document.write( root.data + " ");

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
            document.write( root.data + " ");

        else if (level > 1)
        {
            rightToLeft(root.right, level - 1);
            rightToLeft(root.left, level - 1);
        }
    }

    // Function to print reverse clockwise spiral
    // traversal of a binary tree
    function ReverseClockWiseSpiral(root)
    {
        let i = 1;
        let j = height(root);

        // Flag to mark a change in the direction
        // of printing nodes
        let flag = 0;
        while (i <= j)
        {

            // If flag is zero print nodes
            // from right to left
            if (flag == 0)
            {
                rightToLeft(root, j);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from left to right
                flag = 1;

                // Decrement j
                j--;
            }

            // If flag is one print nodes
            // from left to right
            else
            {
                leftToRight(root, i);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from right to left
                flag = 0;

                // Increment i
                i++;
            }
        }
    }

    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.right = new Node(5);

    ReverseClockWiseSpiral(root);

</script>
```

**Output:** 

```
7 6 5 4 1 3 2    
```

**时间复杂度** : O(N^2)，其中 n 是二叉树中节点的总数。
**辅助空间:** O(N)