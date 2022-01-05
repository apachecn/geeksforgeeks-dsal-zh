# 二叉树中所有父值为偶数的子节点之和

> 原文:[https://www . geeksforgeeks . org/二进制树中具有偶数父值的所有子节点的总和/](https://www.geeksforgeeks.org/sum-of-all-the-child-nodes-with-even-parent-values-in-a-binary-tree/)

给定一棵二叉树，任务是找到父节点为偶数的所有节点的和。
**例:**

```
Input:
       1
      / \
     3   8
        / \
       5   6
      /
     1

Output: 11
The only even nodes are 8 and 6 and 
the sum of their children is 5 + 6 = 11.

Input:
       2
      / \
     3   8
    /   / \
   2   5   6
      /     \
     1       3

Output: 25
3 + 8 + 5 + 6 + 3 = 25
```

**方法:**初始化**和= 0** 并执行树的递归遍历，检查节点是否为偶数，如果节点为偶数，则将其子节点的值加到和中。最后，打印总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return (newNode);
}

// This function visit each node in preorder fashion
// And adds the values of the children of a node with
// even value to the res variable
void calcSum(Node* root, int& res)
{
    // Base Case
    if (root == NULL)
        return;

    // If the value of the
    // current node if even
    if (root->data % 2 == 0) {

        // If the left child of the even
        // node exist then add it to the res
        if (root->left)
            res += root->left->data;

        // Do the same with the right child
        if (root->right)
            res += root->right->data;
    }

    // Visiting the left subtree and the right
    // subtree just like preorder traversal
    calcSum(root->left, res);
    calcSum(root->right, res);
}

// Function to return the sum of nodes
// whose parent has even value
int findSum(Node* root)
{
    // Initialize result
    int res = 0;

    calcSum(root, res);
    return res;
}

// Driver code
int main()
{

    // Creating the tree
    struct Node* root = newNode(2);
    root->left = newNode(3);
    root->right = newNode(8);
    root->left->left = newNode(2);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->left = newNode(1);
    root->right->right->right = newNode(3);

    // Print the required sum
    cout << findSum(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// A binary tree node
static class Node
{
    int data;
    Node left, right;
};
static int res;

// A utility function to allocate a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// This function visit each node in preorder fashion
// And adds the values of the children of a node with
// even value to the res variable
static void calcSum(Node root)
{
    // Base Case
    if (root == null)
        return;

    // If the value of the
    // current node if even
    if (root.data % 2 == 0)
    {

        // If the left child of the even
        // node exist then add it to the res
        if (root.left != null)
            res += root.left.data;

        // Do the same with the right child
        if (root.right != null)
            res += root.right.data;
    }

    // Visiting the left subtree and the right
    // subtree just like preorder traversal
    calcSum(root.left);
    calcSum(root.right);
}

// Function to return the sum of nodes
// whose parent has even value
static int findSum(Node root)
{
    // Initialize result
    res = 0;

    calcSum(root);
    return res;
}

// Driver code
public static void main(String[] args)
{

    // Creating the tree
    Node root = newNode(2);
    root.left = newNode(3);
    root.right = newNode(8);
    root.left.left = newNode(2);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.left = newNode(1);
    root.right.right.right = newNode(3);

    // Print the required sum
    System.out.print(findSum(root));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
result = 0;

# A binary tree node
class Node :
    def __init__(self,data) :
        self.data = data;
        self.left = None
        self.right = None;

# This function visit each node in preorder fashion
# And adds the values of the children of a node with
# even value to the res variable
def calcSum(root, res) :

    global result;

    # Base Case
    if (root == None) :
        return;

    # If the value of the
    # current node if even
    if (root.data % 2 == 0) :

        # If the left child of the even
        # node exist then add it to the res
        if (root.left) :
            res += root.left.data;
            result = res;

        # Do the same with the right child
        if (root.right) :
            res += root.right.data;
            result = res;

    # Visiting the left subtree and the right
    # subtree just like preorder traversal
    calcSum(root.left, res);
    calcSum(root.right, res);

# Function to return the sum of nodes
# whose parent has even value
def findSum(root) :
    res = 0;
    calcSum(root, res);
    print(result)

# Driver code
if __name__ == "__main__" :

    # Creating the tree
    root = Node(2);
    root.left = Node(3);
    root.right = Node(8);
    root.left.left = Node(2);
    root.right.left = Node(5);
    root.right.right = Node(6);
    root.right.left.left = Node(1);
    root.right.right.right = Node(3);

    # Print the required sum
    findSum(root);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// A binary tree node
class Node
{
    public int data;
    public Node left, right;
};
static int res;

// A utility function to allocate a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// This function visit each node in preorder fashion
// And adds the values of the children of a node with
// even value to the res variable
static void calcSum(Node root)
{
    // Base Case
    if (root == null)
        return;

    // If the value of the
    // current node if even
    if (root.data % 2 == 0)
    {

        // If the left child of the even
        // node exist then add it to the res
        if (root.left != null)
            res += root.left.data;

        // Do the same with the right child
        if (root.right != null)
            res += root.right.data;
    }

    // Visiting the left subtree and the right
    // subtree just like preorder traversal
    calcSum(root.left);
    calcSum(root.right);
}

// Function to return the sum of nodes
// whose parent has even value
static int findSum(Node root)
{
    // Initialize result
    res = 0;

    calcSum(root);
    return res;
}

// Driver code
public static void Main(String[] args)
{

    // Creating the tree
    Node root = newNode(2);
    root.left = newNode(3);
    root.right = newNode(8);
    root.left.left = newNode(2);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.left = newNode(1);
    root.right.right.right = newNode(3);

    // Print the required sum
    Console.Write(findSum(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// A binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

var res = 0;

// A utility function to allocate a new node
function newNode(data)
{
    var newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// This function visit each node in preorder fashion
// And adds the values of the children of a node with
// even value to the res variable
function calcSum(root)
{
    // Base Case
    if (root == null)
        return;

    // If the value of the
    // current node if even
    if (root.data % 2 == 0)
    {

        // If the left child of the even
        // node exist then add it to the res
        if (root.left != null)
            res += root.left.data;

        // Do the same with the right child
        if (root.right != null)
            res += root.right.data;
    }

    // Visiting the left subtree and the right
    // subtree just like preorder traversal
    calcSum(root.left);
    calcSum(root.right);
}

// Function to return the sum of nodes
// whose parent has even value
function findSum(root)
{
    // Initialize result
    res = 0;

    calcSum(root);
    return res;
}

// Driver code
// Creating the tree
var root = newNode(2);
root.left = newNode(3);
root.right = newNode(8);
root.left.left = newNode(2);
root.right.left = newNode(5);
root.right.right = newNode(6);
root.right.left.left = newNode(1);
root.right.right.right = newNode(3);
// Print the required sum
document.write(findSum(root));

</script>
```

**Output:** 

```
25
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。