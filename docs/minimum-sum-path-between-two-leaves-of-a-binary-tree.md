# 二叉树两片叶子之间的最小和路径

> 原文:[https://www . geesforgeks . org/二叉树两片叶子之间的最小和路径/](https://www.geeksforgeeks.org/minimum-sum-path-between-two-leaves-of-a-binary-tree/)

给定一个二叉树，其中每个节点元素包含一个数字。任务是找到从一个叶节点到另一个叶节点的最小可能和。
如果根的一边是空的，那么函数应该返回负无穷大。
**例:**

```
Input : 
    4
   /  \
  5    -6
 / \   / \
2  -3 1   8
Output : 1
The minimum sum path between two leaf nodes is:
-3 -> 5 -> 4 -> -6 -> 1

Input :
        3
       /  \
      2    4
     / \ 
    -5  1
Output : -2
```

**方法:**想法是在递归调用中维护两个值:

1.  以当前节点为根的子树的最小根到叶路径总和。
2.  叶子之间的最小路径和。

对于每个被访问的节点 X，我们在 X 的左右子树中找到最小根到叶和，我们将这两个值与 X 的数据相加，并将和与当前最小路径和进行比较。
以下是上述方法的实现:

## C++

```
// C++ program to find minimum path sum
// between two leaves of a binary tree
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to allocate memory
// for a new node
struct Node* newNode(int data)
{
    struct Node* node = new (struct Node);
    node->data = data;
    node->left = node->right = NULL;

    return (node);
}

// A utility function to find the minimum sum between
// any two leaves. This function calculates two values:
// 1\. Minimum path sum between two leaves which is stored
// in result and,
// 2\. The minimum root to leaf path sum which is returned.
// If one side of root is empty, then it returns INT_MIN
int minPathSumUtil(struct Node* root, int& result)
{
    // Base cases
    if (root == NULL)
        return 0;

    if (root->left == NULL && root->right == NULL)
        return root->data;

    // Find minimum sum in left and right sub tree. Also
    // find minimum root to leaf sums in left and right
    // sub trees and store them in ls and rs
    int ls = minPathSumUtil(root->left, result);
    int rs = minPathSumUtil(root->right, result);

    // If both left and right children exist
    if (root->left && root->right) {
        // Update result if needed
        result = min(result, ls + rs + root->data);

        // Return minimum possible value for root being
        // on one side
        return min(ls + root->data, rs + root->data);
    }

    // If any of the two children is empty, return
    // root sum for root being on one side
    if (root->left == NULL)
        return rs + root->data;
    else
        return ls + root->data;
}

// Function to return the minimum
// sum path between two leaves
int minPathSum(struct Node* root)
{
    int result = INT_MAX;
    minPathSumUtil(root, result);
    return result;
}

// Driver code
int main()
{
    struct Node* root = newNode(4);
    root->left = newNode(5);
    root->right = newNode(-6);
    root->left->left = newNode(2);
    root->left->right = newNode(-3);
    root->right->left = newNode(1);
    root->right->right = newNode(8);

    cout << minPathSum(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum path sum
// between two leaves of a binary tree
class GFG
{

// A binary tree node
static class Node
{
    int data;
    Node left;
    Node right;
};

// Utility function to allocate memory
// for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;

    return (node);
}
static int result;

// A utility function to find the minimum sum between
// any two leaves. This function calculates two values:
// 1\. Minimum path sum between two leaves which is stored
// in result and,
// 2\. The minimum root to leaf path sum which is returned.
// If one side of root is empty, then it returns INT_MIN
static int minPathSumUtil( Node root)
{
    // Base cases
    if (root == null)
        return 0;

    if (root.left == null && root.right == null)
        return root.data;

    // Find minimum sum in left and right sub tree. Also
    // find minimum root to leaf sums in left and right
    // sub trees and store them in ls and rs
    int ls = minPathSumUtil(root.left);
    int rs = minPathSumUtil(root.right);

    // If both left and right children exist
    if (root.left != null && root.right != null)
    {
        // Update result if needed
        result = Math.min(result, ls + rs + root.data);

        // Return minimum possible value for root being
        // on one side
        return Math.min(ls + root.data, rs + root.data);
    }

    // If any of the two children is empty, return
    // root sum for root being on one side
    if (root.left == null)
        return rs + root.data;
    else
        return ls + root.data;
}

// Function to return the minimum
// sum path between two leaves
static int minPathSum( Node root)
{
    result = Integer.MAX_VALUE;
    minPathSumUtil(root);
    return result;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(4);
    root.left = newNode(5);
    root.right = newNode(-6);
    root.left.left = newNode(2);
    root.left.right = newNode(-3);
    root.right.left = newNode(1);
    root.right.right = newNode(8);

    System.out.print(minPathSum(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find minimum path sum
# between two leaves of a binary tree

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to allocate memory
# for a new node
def newNode( data):

    node = Node(0)
    node.data = data
    node.left = node.right = None

    return (node)

result = -1

# A utility function to find the
# minimum sum between any two leaves.
# This function calculates two values:
# 1\. Minimum path sum between two leaves 
# which is stored in result and,
# 2\. The minimum root to leaf path sum
# which is returned.
# If one side of root is empty,
# then it returns INT_MIN
def minPathSumUtil(root) :
    global result

    # Base cases
    if (root == None):
        return 0

    if (root.left == None and
        root.right == None) :
        return root.data

    # Find minimum sum in left and right sub tree.
    # Also find minimum root to leaf sums in
    # left and right sub trees and store them
    # in ls and rs
    ls = minPathSumUtil(root.left)
    rs = minPathSumUtil(root.right)

    # If both left and right children exist
    if (root.left != None and
        root.right != None) :

        # Update result if needed
        result = min(result, ls +
                     rs + root.data)

        # Return minimum possible value for
        # root being on one side
        return min(ls + root.data,
                   rs + root.data)

    # If any of the two children is empty,
    # return root sum for root being on one side
    if (root.left == None) :
        return rs + root.data
    else:
        return ls + root.data

# Function to return the minimum
# sum path between two leaves
def minPathSum( root):
    global result
    result = 9999999
    minPathSumUtil(root)
    return result

# Driver code
root = newNode(4)
root.left = newNode(5)
root.right = newNode(-6)
root.left.left = newNode(2)
root.left.right = newNode(-3)
root.right.left = newNode(1)
root.right.right = newNode(8)

print(minPathSum(root))

# This code is contributed
# by Arnab Kundu
```

## C#

```
// C# program to find minimum path sum
// between two leaves of a binary tree
using System;

class GFG
{

// A binary tree node
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Utility function to allocate memory
// for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;

    return (node);
}
static int result;

// A utility function to find the minimum sum between
// any two leaves. This function calculates two values:
// 1\. Minimum path sum between two leaves which is stored
// in result and,
// 2\. The minimum root to leaf path sum which is returned.
// If one side of root is empty, then it returns INT_MIN
static int minPathSumUtil( Node root)
{
    // Base cases
    if (root == null)
        return 0;

    if (root.left == null && root.right == null)
        return root.data;

    // Find minimum sum in left and right sub tree. Also
    // find minimum root to leaf sums in left and right
    // sub trees and store them in ls and rs
    int ls = minPathSumUtil(root.left);
    int rs = minPathSumUtil(root.right);

    // If both left and right children exist
    if (root.left != null && root.right != null)
    {
        // Update result if needed
        result = Math.Min(result, ls + rs + root.data);

        // Return minimum possible value for root being
        // on one side
        return Math.Min(ls + root.data, rs + root.data);
    }

    // If any of the two children is empty, return
    // root sum for root being on one side
    if (root.left == null)
        return rs + root.data;
    else
        return ls + root.data;
}

// Function to return the minimum
// sum path between two leaves
static int minPathSum( Node root)
{
    result = int.MaxValue;
    minPathSumUtil(root);
    return result;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(4);
    root.left = newNode(5);
    root.right = newNode(-6);
    root.left.left = newNode(2);
    root.left.right = newNode(-3);
    root.right.left = newNode(1);
    root.right.right = newNode(8);

Console.Write(minPathSum(root));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find minimum path sum
    // between two leaves of a binary tree

    // Structure of binary tree
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Utility function to allocate memory
    // for a new node
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }
    let result;

    // A utility function to find the minimum sum between
    // any two leaves. This function calculates two values:
    // 1\. Minimum path sum between two leaves which is stored
    // in result and,
    // 2\. The minimum root to leaf path sum which is returned.
    // If one side of root is empty, then it returns INT_MIN
    function minPathSumUtil(root)
    {
        // Base cases
        if (root == null)
            return 0;

        if (root.left == null && root.right == null)
            return root.data;

        // Find minimum sum in left and right sub tree. Also
        // find minimum root to leaf sums in left and right
        // sub trees and store them in ls and rs
        let ls = minPathSumUtil(root.left);
        let rs = minPathSumUtil(root.right);

        // If both left and right children exist
        if (root.left != null && root.right != null)
        {
            // Update result if needed
            result = Math.min(result, ls + rs + root.data);

            // Return minimum possible value for root being
            // on one side
            return Math.min(ls + root.data, rs + root.data);
        }

        // If any of the two children is empty, return
        // root sum for root being on one side
        if (root.left == null)
            return rs + root.data;
        else
            return ls + root.data;
    }

    // Function to return the minimum
    // sum path between two leaves
    function minPathSum(root)
    {
        result = Number.MAX_VALUE;
        minPathSumUtil(root);
        return result;
    }

    let root = newNode(4);
    root.left = newNode(5);
    root.right = newNode(-6);
    root.left.left = newNode(2);
    root.left.right = newNode(-3);
    root.right.left = newNode(1);
    root.right.right = newNode(8);

    document.write(minPathSum(root));

</script>
```

**Output:** 

```
1
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)