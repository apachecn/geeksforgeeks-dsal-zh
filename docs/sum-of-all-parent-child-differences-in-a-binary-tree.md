# 二叉树中所有父子差异的总和

> 原文:[https://www . geeksforgeeks . org/所有二进制树中父子差异之和/](https://www.geeksforgeeks.org/sum-of-all-parent-child-differences-in-a-binary-tree/)

给定一棵二叉树，求给定二叉树的所有非叶节点的所有父子差异之和。
**注意**父子差为**(父节点的值–(子节点的值之和))。**
**例:**

```
Input: 
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
          \
           8
Output: -23
1st parent-child difference = 1 -(2 + 3) = -4
2nd parent-child difference = 2 -(4 + 5) = -7
3rd parent-child difference = 3 -(6 + 7) = -10
4th parent-child difference = 6 - 8 = -2
Total sum = -23

Input: 
        1
      /   \
     2     3
      \   /
       5 6
Output: -10
```

**天真方法:**想法是以任何方式遍历树，检查节点是否是叶节点。如果节点是非叶节点，则将(节点数据–子节点数据之和)添加到结果中。
**有效方法:**在最终结果中，仔细分析表明，每个内部节点(既不是根也不是叶的节点)曾经被视为子节点，并且曾经被视为父节点，因此它们在最终结果中的贡献为零。此外，根仅被视为父节点一次，并且以类似的方式，所有叶节点被视为子节点一次。因此，最终结果是**(根的值–所有叶节点的总和)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure for a binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Returns a new node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
}

// Utility function which calculates
// the sum of all leaf nodes
void leafSumFunc(Node* root, int* leafSum)
{
    if (!root)
        return;

    // Add root data to sum if
    // root is a leaf node
    if (!root->left && !root->right)
        *leafSum += root->data;

    // Recursively check in the left
    // and the right sub-tree
    leafSumFunc(root->left, leafSum);
    leafSumFunc(root->right, leafSum);
}

// Function to return the required result
int sumParentChildDiff(Node* root)
{

    // If root is null
    if (!root)
        return 0;

    // If only node is the root node
    if (!root->left && !root->right)
        return root->data;

    // Find the sum of all the leaf nodes
    int leafSum = 0;
    leafSumFunc(root, &leafSum);

    // Root - sum of all the leaf nodes
    return (root->data - leafSum);
}

// Driver code
int main()
{
    // Construct binary tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right = newNode(3);
    root->right->right = newNode(7);
    root->right->left = newNode(6);

    cout << sumParentChildDiff(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Structure for a binary tree node
static class Node
{
    int data;
    Node left, right;
};

// Returns a new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}
static int leafSum;

// Utility function which calculates
// the sum of all leaf nodes
static void leafSumFunc(Node root )
{
    if (root == null)
        return;

    // Add root data to sum if
    // root is a leaf node
    if (root.left == null && root.right == null)
        leafSum += root.data;

    // Recursively check in the left
    // and the right sub-tree
    leafSumFunc(root.left);
    leafSumFunc(root.right);
}

// Function to return the required result
static int sumParentChildDiff(Node root)
{

    // If root is null
    if (root == null)
        return 0;

    // If only node is the root node
    if (root.left == null && root.right == null)
        return root.data;

    // Find the sum of all the leaf nodes
    leafSum = 0;
    leafSumFunc(root);

    // Root - sum of all the leaf nodes
    return (root.data - leafSum);
}

// Driver code
public static void main(String args[])
{
    // Construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);

    System.out.println( sumParentChildDiff(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Structure for a binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function which calculates
# the sum of all leaf nodes
def leafSumFunc(root, leafSum):

    if not root:
        return 0

    # Add root data to sum
    # if root is a leaf node
    if not root.left and not root.right:
        leafSum += root.data

    # Recursively check in the
    # left and the right sub-tree
    leafSum = max(leafSumFunc(root.left,
                              leafSum), leafSum)
    leafSum = max(leafSumFunc(root.right,
                              leafSum), leafSum)
    return leafSum

# Function to return the required result
def sumParentChildDiff(root):

    # If root is None
    if not root:
        return 0

    # If only node is the root node
    if not root.left and not root.right:
        return root.data

    # Find the sum of all the leaf nodes
    leafSum = leafSumFunc(root, 0)

    # Root - sum of all the leaf nodes
    return root.data - leafSum

# Driver code
if __name__ == "__main__":

    # Construct binary tree
    root = Node(1)
    root.left = Node(2)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right = Node(3)
    root.right.right = Node(7)
    root.right.left = Node(6)

    print(sumParentChildDiff(root))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Structure for a binary tree node
public class Node
{
    public int data;
    public Node left, right;
};

// Returns a new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}
static int leafSum;

// Utility function which calculates
// the sum of all leaf nodes
static void leafSumFunc(Node root )
{
    if (root == null)
        return;

    // Add root data to sum if
    // root is a leaf node
    if (root.left == null && root.right == null)
        leafSum += root.data;

    // Recursively check in the left
    // and the right sub-tree
    leafSumFunc(root.left);
    leafSumFunc(root.right);
}

// Function to return the required result
static int sumParentChildDiff(Node root)
{

    // If root is null
    if (root == null)
        return 0;

    // If only node is the root node
    if (root.left == null && root.right == null)
        return root.data;

    // Find the sum of all the leaf nodes
    leafSum = 0;
    leafSumFunc(root);

    // Root - sum of all the leaf nodes
    return (root.data - leafSum);
}

// Driver code
public static void Main(String []args)
{
    // Construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);

    Console.WriteLine( sumParentChildDiff(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Structure for a binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Returns a new node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }
    let leafSum;

    // Utility function which calculates
    // the sum of all leaf nodes
    function leafSumFunc(root)
    {
        if (root == null)
            return;

        // Add root data to sum if
        // root is a leaf node
        if (root.left == null && root.right == null)
            leafSum += root.data;

        // Recursively check in the left
        // and the right sub-tree
        leafSumFunc(root.left);
        leafSumFunc(root.right);
    }

    // Function to return the required result
    function sumParentChildDiff(root)
    {

        // If root is null
        if (root == null)
            return 0;

        // If only node is the root node
        if (root.left == null && root.right == null)
            return root.data;

        // Find the sum of all the leaf nodes
        leafSum = 0;
        leafSumFunc(root);

        // Root - sum of all the leaf nodes
        return (root.data - leafSum);
    }

    // Construct binary tree
    let root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);

    document.write( sumParentChildDiff(root));

</script>
```

**Output:** 

```
-21
```