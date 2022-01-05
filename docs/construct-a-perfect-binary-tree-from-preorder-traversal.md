# 通过前序遍历

构建一棵完美的二叉树

> 原文:[https://www . geeksforgeeks . org/construct-a-perfect-二叉树-from-preorder-遍历/](https://www.geeksforgeeks.org/construct-a-perfect-binary-tree-from-preorder-traversal/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **pre[]** ，表示由 **N 个**节点组成的[完美二叉树](https://www.geeksforgeeks.org/check-weather-given-binary-tree-perfect-not/)的[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，任务是根据给定的[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)构造一个**完美二叉树**，并返回树根。

**示例:**

> **输入:** pre[] = {1，2，4，5，3，6，7}
> **输出:**
> 1
> /\
> /\
> 2 3
> /\/\
> /\
> 4 5 6 7
> 
> **输入:** pre[] = {1，2，3}
> **输出:**
> 1
> / \
> / \
> 2 3

一般来说，要构造一棵二叉树，我们不能只使用前序遍历，但这里给出了一个额外的条件，即二叉树是完美二叉树。我们可以利用这个额外条件。

对于完美二叉树，每个节点都有 2 或 0 个子节点，并且所有叶节点都在同一级别。二叉树的前序遍历首先包含根，然后是左子树的前序遍历，然后是右子树的前序遍历。因此，对于完美二叉树，根应该在两个子树中具有相同数量的子树，所以在预序遍历中根之后的元素数量(比如说，n)应该是偶数(2 *一个子树中的节点数量，因为它是完美二叉树)。并且由于完美二叉树的每个子树的节点数相等，所以我们可以找到左子树的前序遍历(在整棵树的前序遍历中是根后数组的一半)，并且我们知道右子树的前序遍历一定是在左子树的前序遍历之后，所以剩下的一半就是右子树的前序遍历。

所以前序遍历的第一个元素是根，我们会用这个元素构建一个节点作为根，然后我们就可以很容易的找到根的左右子树的前序遍历，我们会递归的构建根的左右子树。

**方法:**给定的问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决。按照以下步骤解决问题:

*   创建一个函数，说 **BuildPerfectBT_helper** ，参数为 **preStart** 、 **preEnd** 、 **pre[]** ，其中 **preStart** 代表数组的起始索引 **pre[]** 、 **preEnd** 代表数组的结束索引 **pre[]** ，执行以下步骤:
    *   如果**预启动**的值大于**预启动**，则返回**空值**。
    *   将**根**初始化为**预【预启动】**。
    *   如果**预置**的值与**预置**相同，则返回**根**。
    *   初始化 4 个变量，说**左预启动**为**预启动+ 1** 、**右预启动**为**左预启动+(preEnd–左预启动+1)/2** 、**左预启动**为**右预启动-1**、**右预启动**为 **preEnd** 。
    *   通过递归调用函数 **buildPerfectBT_helper()** 并使用参数 **leftPreStart** 、 **leftPreEnd** 和**pre【】**修改**根- >左侧**的值。
    *   通过递归调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **用参数 **rightPreStart** 、 **rightPreEnd** 和 **pre[]** 来修改**根- >右**的值。**
    *   执行上述步骤后，返回**根**。
*   创建完美二叉树后，打印[以便遍历树](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)。

下面是上面讨论的步骤的图示:

> **步骤 1:** 构建([1，2，4，5，3，6，7])
> 
> **第 2 步:**
> 1
> / \
> / \
> 构建([2，4，5])构建([3，6，7])
> 
> 现在第一个元素(这里是 1)是根，然后第一个元素之后的子数组(这里是[2，4，5，3，6，7])包含左右子树的前序遍历。并且我们知道左子树的前序遍历是前半部分，即[2，4，5]，右子树的前序遍历是后半部分，即[3，6，7]。现在递归地构建左右子树。
> 
> **第三步:**
> 1
> 
> ___________|_________________
> 
> / \
> 
> / \
> 
>                       2                                                          3
> 
> ______/___________ _______\____________
> 
> / \ / \
> 
> / \ / \
> 
> build([4])build([5])build([6])build([7])
> 
> **Step 4:**
> 1
> /\
> /\
> 2 3
> /\/\
> /\
> 4 5 6 7

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of the tree
struct Node {
    int data;
    Node *left, *right;

    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};

// Function to create a new node with
// the value val
Node* getNewNode(int val)
{
    Node* newNode = new Node(val);
    newNode->data = val;
    newNode->left = newNode->right = NULL;

    // Return the newly created node
    return newNode;
}

// Function to create the Perfect
// Binary Tree
Node* buildPerfectBT_helper(int preStart,
                            int preEnd,
                            int pre[])
{
    // If preStart > preEnd return NULL
    if (preStart > preEnd)
        return NULL;

    // Initialize root as pre[preStart]
    Node* root = getNewNode(pre[preStart]);
    ;

    // If the only node is left,
    // then return node
    if (preStart == preEnd)
        return root;

    // Parameters for further recursion
    int leftPreStart = preStart + 1;
    int rightPreStart = leftPreStart
                        + (preEnd - leftPreStart + 1) / 2;
    int leftPreEnd = rightPreStart - 1;
    int rightPreEnd = preEnd;

    // Recursive Call to build the
    // subtree of root node
    root->left = buildPerfectBT_helper(
        leftPreStart, leftPreEnd, pre);

    root->right = buildPerfectBT_helper(
        rightPreStart, rightPreEnd, pre);

    // Return the created root
    return root;
}

// Function to build Perfect Binary Tree
Node* buildPerfectBT(int pre[], int size)
{
    return buildPerfectBT_helper(0, size - 1, pre);
}

// Function to print the Inorder of
// the given Tree
void printInorder(Node* root)
{
    // Base Case
    if (!root)
        return;

    // Left Recursive Call
    printInorder(root->left);

    // Print the data
    cout << root->data << " ";

    // Right Recursive Call
    printInorder(root->right);
}

// Driver Code
int main()
{
    int pre[] = { 1, 2, 4, 5, 3, 6, 7 };
    int N = sizeof(pre) / sizeof(pre[0]);

    // Function Call
    Node* root = buildPerfectBT(pre, N);

    // Print Inorder Traversal
    cout << "\nInorder traversal of the tree: ";
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class Main
{
    // Structure of the tree
    static class Node {

        public int data;
        public Node left, right;

        public Node(int val)
        {
            data = val;
            left = right = null;
        }
    }

    // Function to create a new node with
    // the value val
    static Node getNewNode(int val)
    {
        Node newNode = new Node(val);

        // Return the newly created node
        return newNode;
    }

    // Function to create the Perfect
    // Binary Tree
    static Node buildPerfectBT_helper(int preStart, int preEnd, int[] pre)
    {
        // If preStart > preEnd return NULL
        if (preStart > preEnd)
            return null;

        // Initialize root as pre[preStart]
        Node root = getNewNode(pre[preStart]);

        // If the only node is left,
        // then return node
        if (preStart == preEnd)
            return root;

        // Parameters for further recursion
        int leftPreStart = preStart + 1;
        int rightPreStart = leftPreStart + (preEnd - leftPreStart + 1) / 2;
        int leftPreEnd = rightPreStart - 1;
        int rightPreEnd = preEnd;

        // Recursive Call to build the
        // subtree of root node
        root.left = buildPerfectBT_helper(
            leftPreStart, leftPreEnd, pre);

        root.right = buildPerfectBT_helper(
            rightPreStart, rightPreEnd, pre);

        // Return the created root
        return root;
    }

    // Function to build Perfect Binary Tree
    static Node buildPerfectBT(int[] pre, int size)
    {
        return buildPerfectBT_helper(0, size - 1, pre);
    }

    // Function to print the Inorder of
    // the given Tree
    static void printInorder(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Left Recursive Call
        printInorder(root.left);

        // Print the data
        System.out.print(root.data + " ");

        // Right Recursive Call
        printInorder(root.right);
    }

    public static void main(String[] args) {
        int[] pre = { 1, 2, 4, 5, 3, 6, 7 };
        int N = pre.length;

        // Function Call
        Node root = buildPerfectBT(pre, N);

        // Print Inorder Traversal
        System.out.print("Inorder traversal of the tree: ");
        printInorder(root);
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of the tree
class Node:
    def __init__(self, val):
        self.data = val
        self.left = None
        self.right = None

# Function to create a new node with
# the value val
def getNewNode(val):
    newNode = Node(val)

    # Return the newly created node
    return newNode

# Function to create the Perfect
# Binary Tree
def buildPerfectBT_helper(preStart, preEnd, pre):

    # If preStart > preEnd return NULL
    if (preStart > preEnd):
        return None

    # Initialize root as pre[preStart]
    root = getNewNode(pre[preStart])

    # If the only node is left,
    # then return node
    if (preStart == preEnd):
        return root

    # Parameters for further recursion
    leftPreStart = preStart + 1
    rightPreStart = leftPreStart + int((preEnd - leftPreStart + 1) / 2)
    leftPreEnd = rightPreStart - 1
    rightPreEnd = preEnd

    # Recursive Call to build the
    # subtree of root node
    root.left = buildPerfectBT_helper(leftPreStart, leftPreEnd, pre)

    root.right = buildPerfectBT_helper(rightPreStart, rightPreEnd, pre)

    # Return the created root
    return root

# Function to build Perfect Binary Tree
def buildPerfectBT(pre, size):
    return buildPerfectBT_helper(0, size - 1, pre)

# Function to print the Inorder of
# the given Tree
def printInorder(root):

    # Base Case
    if (root == None):
        return

    # Left Recursive Call
    printInorder(root.left)

    # Print the data
    print(root.data, "", end = "")

    # Right Recursive Call
    printInorder(root.right)

pre = [ 1, 2, 4, 5, 3, 6, 7 ]
N = len(pre)

# Function Call
root = buildPerfectBT(pre, N)

# Print Inorder Traversal
print("Inorder traversal of the tree: ", end = "")
printInorder(root)

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Structure of the tree
    class Node {

        public int data;
        public Node left, right;

        public Node(int val)
        {
            data = val;
            left = right = null;
        }
    }

    // Function to create a new node with
    // the value val
    static Node getNewNode(int val)
    {
        Node newNode = new Node(val);
        // Return the newly created node
        return newNode;
    }

    // Function to create the Perfect
    // Binary Tree
    static Node buildPerfectBT_helper(int preStart, int preEnd, int[] pre)
    {
        // If preStart > preEnd return NULL
        if (preStart > preEnd)
            return null;

        // Initialize root as pre[preStart]
        Node root = getNewNode(pre[preStart]);

        // If the only node is left,
        // then return node
        if (preStart == preEnd)
            return root;

        // Parameters for further recursion
        int leftPreStart = preStart + 1;
        int rightPreStart = leftPreStart + (preEnd - leftPreStart + 1) / 2;
        int leftPreEnd = rightPreStart - 1;
        int rightPreEnd = preEnd;

        // Recursive Call to build the
        // subtree of root node
        root.left = buildPerfectBT_helper(
            leftPreStart, leftPreEnd, pre);

        root.right = buildPerfectBT_helper(
            rightPreStart, rightPreEnd, pre);

        // Return the created root
        return root;
    }

    // Function to build Perfect Binary Tree
    static Node buildPerfectBT(int[] pre, int size)
    {
        return buildPerfectBT_helper(0, size - 1, pre);
    }

    // Function to print the Inorder of
    // the given Tree
    static void printInorder(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Left Recursive Call
        printInorder(root.left);

        // Print the data
        Console.Write(root.data + " ");

        // Right Recursive Call
        printInorder(root.right);
    }

  static void Main() {
    int[] pre = { 1, 2, 4, 5, 3, 6, 7 };
    int N = pre.Length;

    // Function Call
    Node root = buildPerfectBT(pre, N);

    // Print Inorder Traversal
    Console.Write("Inorder traversal of the tree: ");
    printInorder(root);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Structure of the tree
    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.data = val;
        }
    }

    // Function to create a new node with
    // the value val
    function getNewNode(val)
    {
        let newNode = new Node(val);
        // Return the newly created node
        return newNode;
    }

    // Function to create the Perfect
    // Binary Tree
    function buildPerfectBT_helper(preStart, preEnd, pre)
    {
        // If preStart > preEnd return NULL
        if (preStart > preEnd)
            return null;

        // Initialize root as pre[preStart]
        let root = getNewNode(pre[preStart]);

        // If the only node is left,
        // then return node
        if (preStart == preEnd)
            return root;

        // Parameters for further recursion
        let leftPreStart = preStart + 1;
        let rightPreStart = leftPreStart
                            + parseInt((preEnd - leftPreStart + 1) / 2);
        let leftPreEnd = rightPreStart - 1;
        let rightPreEnd = preEnd;

        // Recursive Call to build the
        // subtree of root node
        root.left = buildPerfectBT_helper(
            leftPreStart, leftPreEnd, pre);

        root.right = buildPerfectBT_helper(
            rightPreStart, rightPreEnd, pre);

        // Return the created root
        return root;
    }

    // Function to build Perfect Binary Tree
    function buildPerfectBT(pre, size)
    {
        return buildPerfectBT_helper(0, size - 1, pre);
    }

    // Function to print the Inorder of
    // the given Tree
    function printInorder(root)
    {
        // Base Case
        if (root == null)
            return;

        // Left Recursive Call
        printInorder(root.left);

        // Print the data
        document.write(root.data + " ");

        // Right Recursive Call
        printInorder(root.right);
    }

    let pre = [ 1, 2, 4, 5, 3, 6, 7 ];
    let N = pre.length;

    // Function Call
    let root = buildPerfectBT(pre, N);

    // Print Inorder Traversal
    document.write("Inorder traversal of the tree: ");
    printInorder(root);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
Inorder traversal of the tree: 4 2 5 1 6 3 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)