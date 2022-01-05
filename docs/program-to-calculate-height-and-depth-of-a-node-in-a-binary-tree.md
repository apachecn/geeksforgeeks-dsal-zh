# 计算二叉树节点高度和深度的程序

> 原文:[https://www . geesforgeks . org/计算二叉树中节点高度和深度的程序/](https://www.geeksforgeeks.org/program-to-calculate-height-and-depth-of-a-node-in-a-binary-tree/)

给定一个由 **N** 节点和一个整数 **K** 组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是在[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)中找到值为 **K** 的节点的深度和高度。

> 节点的**深度**是从**树的根节点**到该节点的路径中存在的边的数量。
> 节点的**高度**是连接该节点和叶节点的最长路径中存在的边的数量。

**示例:**

> **输入:** K = 25，
> 5
> /\
> 10 15
> /\/\
> 20 25 30 35
> \
> 45
> **输出:**
> 节点 25 的深度= 2
> 节点 25 的高度= 1
> **解释:**
> 从根节点到节点 25 的路径中的边数是 2。因此，节点 25 的深度是 2。
> 连接节点 25 到任意叶节点的最长路径中的边数为 1。因此，节点 25 的高度为 1。
> 
> **输入:** K = 10，
> 5
> /\
> 10 15
> /\/\
> 20 25 30 35
> \
> 45
> **输出:**
> 节点 10 的深度= 1
> 节点 10 的高度= 2

**方法:**根据以下观察结果可以解决问题:

> [**节点的深度****K**](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)(指[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/) ) =将**根**连接到节点**K**=[K](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)祖先的数量(不包括 **K** 本身)。

按照以下步骤查找给定节点的深度:

*   如果树为空，打印-1。
*   否则，请执行以下步骤:
    *   初始化一个变量，说 **dist** 为 **-1** 。
    *   检查节点 **K** 是否等于给定节点。
    *   否则，通过递归地分别检查左子树和右子树，检查它是否存在于**子树、**子树中。
    *   如果发现为真，打印 **dist + 1** 的值。
    *   否则，打印**距离**。

> **节点**K**(T4 二叉树)的高度**=将 **K** 连接到任何叶节点的**最长路径**的边数。

按照以下步骤查找给定节点的高度:

*   如果树为空，打印-1。
*   否则，请执行以下步骤:
    *   递归计算左子树的高度。
    *   递归计算右子树的高度。
    *   通过将上一步中获得的两个高度的最大值加 1 来更新当前节点的高度。将高度存储在一个变量中，比如**和**。
    *   如果当前节点等于给定节点 **K，**打印 **ans** 的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Binary Tree Node
struct Node {
    int data;
    Node *left, *right;
};

// Utility function to create
// a new Binary Tree Node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find the depth of
// a given node in a Binary Tree
int findDepth(Node* root, int x)
{
    // Base case
    if (root == NULL)
        return -1;

    // Initialize distance as -1
    int dist = -1;

    // Check if x is current node=
    if ((root->data == x)

        // Otherwise, check if x is
        // present in the left subtree
        || (dist = findDepth(root->left, x)) >= 0

        // Otherwise, check if x is
        // present in the right subtree
        || (dist = findDepth(root->right, x)) >= 0)

        // Return depth of the node
        return dist + 1;

    return dist;
}

// Helper function to find the height
// of a given node in the binary tree
int findHeightUtil(Node* root, int x,
                   int& height)
{
    // Base Case
    if (root == NULL) {
        return -1;
    }

    // Store the maximum height of
    // the left and right subtree
    int leftHeight = findHeightUtil(
        root->left, x, height);

    int rightHeight
        = findHeightUtil(
            root->right, x, height);

    // Update height of the current node
    int ans = max(leftHeight, rightHeight) + 1;

    // If current node is the required node
    if (root->data == x)
        height = ans;

    return ans;
}

// Function to find the height of
// a given node in a Binary Tree
int findHeight(Node* root, int x)
{
    // Store the height of
    // the given node
    int h = -1;

    // Stores height of the Tree
    int maxHeight = findHeightUtil(root, x, h);

    // Return the height
    return h;
}

// Driver Code
int main()
{
    // Binary Tree Formation
    Node* root = newNode(5);
    root->left = newNode(10);
    root->right = newNode(15);
    root->left->left = newNode(20);
    root->left->right = newNode(25);
    root->left->right->right = newNode(45);
    root->right->left = newNode(30);
    root->right->right = newNode(35);

    int k = 25;

    // Function call to find the
    // depth of a given node
    cout << "Depth: "
         << findDepth(root, k) << "\n";

    // Function call to find the
    // height of a given node
    cout << "Height: " << findHeight(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

static int height = -1;

// Structure of a Binary Tree Node
static class Node
{
    int data;
    Node left;
    Node right;
};

// Utility function to create
// a new Binary Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the depth of
// a given node in a Binary Tree
static int findDepth(Node root, int x)
{

    // Base case
    if (root == null)
        return -1;

    // Initialize distance as -1
    int dist = -1;

    // Check if x is current node=
    if ((root.data == x)||

        // Otherwise, check if x is
        // present in the left subtree
        (dist = findDepth(root.left, x)) >= 0 ||

        // Otherwise, check if x is
        // present in the right subtree
        (dist = findDepth(root.right, x)) >= 0)

        // Return depth of the node
        return dist + 1;

    return dist;
}

// Helper function to find the height
// of a given node in the binary tree
static int findHeightUtil(Node root, int x)
{

    // Base Case
    if (root == null)
    {
        return -1;
    }

    // Store the maximum height of
    // the left and right subtree
    int leftHeight = findHeightUtil(root.left, x);

    int rightHeight = findHeightUtil(root.right, x);

    // Update height of the current node
    int ans = Math.max(leftHeight, rightHeight) + 1;

    // If current node is the required node
    if (root.data == x)
        height = ans;

    return ans;
}

// Function to find the height of
// a given node in a Binary Tree
static int findHeight(Node root, int x)
{

    // Stores height of the Tree
    findHeightUtil(root, x);

    // Return the height
    return height;
}

// Driver Code
public static void main(String []args)
{

    // Binary Tree Formation
    Node root = newNode(5);
    root.left = newNode(10);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.left.right = newNode(25);
    root.left.right.right = newNode(45);
    root.right.left = newNode(30);
    root.right.right = newNode(35);

    int k = 25;

    // Function call to find the
    // depth of a given node
    System.out.println("Depth: " + findDepth(root, k));

    // Function call to find the
    // height of a given node
    System.out.println("Height: " + findHeight(root, k));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a Binary Tree Node
class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# Function to find the depth of
# a given node in a Binary Tree
def findDepth(root, x):

    # Base case
    if (root == None):
        return -1

    # Initialize distance as -1
    dist = -1

    # Check if x is current node=
    if (root.data == x):
        return dist + 1

    dist = findDepth(root.left, x)
    if dist >= 0:
        return dist + 1
    dist = findDepth(root.right, x)
    if dist >= 0:
        return dist + 1
    return dist

# Helper function to find the height
# of a given node in the binary tree
def findHeightUtil(root, x):
    global height

    # Base Case
    if (root == None):
        return -1

    # Store the maximum height of
    # the left and right subtree
    leftHeight = findHeightUtil(root.left, x)

    rightHeight = findHeightUtil(root.right, x)

    # Update height of the current node
    ans = max(leftHeight, rightHeight) + 1

    # If current node is the required node
    if (root.data == x):
        height = ans

    return ans

# Function to find the height of
# a given node in a Binary Tree
def findHeight(root, x):
    global height

    # Stores height of the Tree
    maxHeight = findHeightUtil(root, x)

    # Return the height
    return height

# Driver Code
if __name__ == '__main__':

    # Binary Tree Formation
    height = -1
    root = Node(5)
    root.left = Node(10)
    root.right = Node(15)
    root.left.left = Node(20)
    root.left.right = Node(25)
    root.left.right.right = Node(45)
    root.right.left = Node(30)
    root.right.right = Node(35)

    k = 25

    # Function call to find the
    # depth of a given node
    print("Depth: ",findDepth(root, k))

    # Function call to find the
    # height of a given node
    print("Height: ",findHeight(root, k))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int height = -1;

// Structure of a Binary Tree Node
class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Utility function to create
// a new Binary Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the depth of
// a given node in a Binary Tree
static int findDepth(Node root, int x)
{

    // Base case
    if (root == null)
        return -1;

    // Initialize distance as -1
    int dist = -1;

    // Check if x is current node=
    if ((root.data == x)||

        // Otherwise, check if x is
        // present in the left subtree
        (dist = findDepth(root.left, x)) >= 0 ||

        // Otherwise, check if x is
        // present in the right subtree
        (dist = findDepth(root.right, x)) >= 0)

        // Return depth of the node
        return dist + 1;

    return dist;
}

// Helper function to find the height
// of a given node in the binary tree
static int findHeightUtil(Node root, int x)
{

    // Base Case
    if (root == null)
    {
        return -1;
    }

    // Store the maximum height of
    // the left and right subtree
    int leftHeight = findHeightUtil(root.left, x);

    int rightHeight = findHeightUtil(root.right, x);

    // Update height of the current node
    int ans = Math.Max(leftHeight, rightHeight) + 1;

    // If current node is the required node
    if (root.data == x)
        height = ans;

    return ans;
}

// Function to find the height of
// a given node in a Binary Tree
static int findHeight(Node root, int x)
{

    // Stores height of the Tree
    findHeightUtil(root, x);

    // Return the height
    return height;
}

// Driver Code
public static void Main()
{

    // Binary Tree Formation
    Node root = newNode(5);
    root.left = newNode(10);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.left.right = newNode(25);
    root.left.right.right = newNode(45);
    root.right.left = newNode(30);
    root.right.right = newNode(35);

    int k = 25;

    // Function call to find the
    // depth of a given node
    Console.WriteLine("Depth: " + findDepth(root, k));

    // Function call to find the
    // height of a given node
    Console.WriteLine("Height: " + findHeight(root, k));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

var height = -1;

// Structure of a Binary Tree Node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create
// a new Binary Tree Node
function newNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

// Function to find the depth of
// a given node in a Binary Tree
function findDepth(root, x)
{

    // Base case
    if (root == null)
        return -1;

    // Initialize distance as -1
    var dist = -1;

    // Check if x is current node=
    if ((root.data == x)||

        // Otherwise, check if x is
        // present in the left subtree
        (dist = findDepth(root.left, x)) >= 0 ||

        // Otherwise, check if x is
        // present in the right subtree
        (dist = findDepth(root.right, x)) >= 0)

        // Return depth of the node
        return dist + 1;

    return dist;
}

// Helper function to find the height
// of a given node in the binary tree
function findHeightUtil(root, x)
{

    // Base Case
    if (root == null)
    {
        return -1;
    }

    // Store the maximum height of
    // the left and right subtree
    var leftHeight = findHeightUtil(root.left, x);

    var rightHeight = findHeightUtil(root.right, x);

    // Update height of the current node
    var ans = Math.max(leftHeight, rightHeight) + 1;

    // If current node is the required node
    if (root.data == x)
        height = ans;

    return ans;
}

// Function to find the height of
// a given node in a Binary Tree
function findHeight(root, x)
{

    // Stores height of the Tree
    findHeightUtil(root, x);

    // Return the height
    return height;
}

// Driver Code
// Binary Tree Formation
var root = newNode(5);
root.left = newNode(10);
root.right = newNode(15);
root.left.left = newNode(20);
root.left.right = newNode(25);
root.left.right.right = newNode(45);
root.right.left = newNode(30);
root.right.right = newNode(35);
var k = 25;
// Function call to find the
// depth of a given node
document.write("Depth: " + findDepth(root, k)+"<br>");
// Function call to find the
// height of a given node
document.write("Height: " + findHeight(root, k));

</script>
```

**Output:** 

```
Depth: 2
Height: 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)