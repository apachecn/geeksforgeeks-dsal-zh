# 具有相反重子树之和的节点之和

> 原文:[https://www . geeksforgeeks . org/具有对等式子树之和的节点之和/](https://www.geeksforgeeks.org/sum-of-nodes-having-sum-of-subtrees-of-opposite-parities/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是从给定的树中找出所有这样的节点的和，该树的左和右子树的和分别是奇数和偶数或偶数和奇数。

**示例:**

> **输入:**
> 11
> /\
> 23 44
> /\/\
> 13 9 22 7
> /\
> 6 15
> **输出:** 33
> **说明:**只有两个这样的节点:
> 
> *   节点 22 的左子树和右子树之和为 6(偶数)和 15(奇数)。
> *   节点 11 的左子树和右子树之和为 45(奇数)和 94(偶数)。
> 
> 因此，总和= 22 + 11 = 33。
> 
> **输入:**
> 11
> /
> 5
> /\
> 3 1
> **输出:** 0
> **说明:**不存在满足给定条件的节点。

**方法:**思路是[递归](https://www.geeksforgeeks.org/recursion/)计算**左子树**之和**右子树**之和，然后检查给定条件。按照以下步骤解决问题:

*   初始化一个变量**和**为 **0** 来存储所有这些节点的总和。
*   [在给定的树](https://www.geeksforgeeks.org/iterative-postorder-traversal-using-stack/)中执行后置遍历。
*   求每个节点左右子树的和，检查和是否为**非零**，检查两个和的和是否为奇数。如果发现为真，则在**和**中包含当前节点值。
*   返回每个递归调用中左子树、右子树和当前节点值的所有节点的总和。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ pprogram for the above approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {

    int data;
    Node *left, *right;   
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}
    // Stores the desired result
     int mSum;

    // Function to find the sum of nodes
    // with subtree sums of opposite parities
     int getSum(Node *root)
    {

        // Return 0, if node is NULL
        if (root == NULL)
            return 0;

        // Recursively call left and
        // right subtree
        int lSum = getSum(root->left);
        int rSum = getSum(root->right);

        // Update mSum, if one subtree
        // sum is even and another is odd
        if (lSum != 0 && rSum != 0)
            if ((lSum + rSum) % 2 != 0)
                mSum += root->data;

        // Return the sum of subtree
        return lSum + rSum + root->data;
    }

    // Driver Code
    int main()
    {
        // Given number of nodes
        int n = 9;

        // Binary tree formation
       struct Node *root = newNode(11);
        root->left =  newNode(23);
        root->right =  newNode(44);
        root->left->left =  newNode(13);
        root->left->right =  newNode(9);
        root->right->left =  newNode(22);
        root->right->right =  newNode(7);
        root->right->left->left =  newNode(6);
        root->right->left->right = newNode(15);

        // 11
        //    /     \
        // 23       44
        //  /  \     /   \
        // 13   9   22     7
        //         / \
        // 6   15

        mSum = 0;
        getSum(root);

        // Print the sum
        cout<<(mSum);
    }

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

// A binary tree node
class Node {

    int data;
    Node left, right;

    // Constructor
    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// Binary Tree Class
class BinaryTree {

    // Stores the desired result
    static int mSum;

    Node root;

    // Function to find the sum of nodes
    // with subtree sums of opposite parities
    static int getSum(Node root)
    {
        // Return 0, if node is null
        if (root == null)
            return 0;

        // Recursively call left and
        // right subtree
        int lSum = getSum(root.left);
        int rSum = getSum(root.right);

        // Update mSum, if one subtree
        // sum is even and another is odd
        if (lSum != 0 && rSum != 0)
            if ((lSum + rSum) % 2 != 0)
                mSum += root.data;

        // Return the sum of subtree
        return lSum + rSum + root.data;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given number of nodes
        int n = 9;

        BinaryTree tree = new BinaryTree();

        // Binary tree formation
        tree.root = new Node(11);
        tree.root.left = new Node(23);
        tree.root.right = new Node(44);
        tree.root.left.left = new Node(13);
        tree.root.left.right = new Node(9);
        tree.root.right.left = new Node(22);
        tree.root.right.right = new Node(7);
        tree.root.right.left.left = new Node(6);
        tree.root.right.left.right = new Node(15);

        // 11
        //    /     \
        // 23       44
        //  /  \     /   \
        // 13   9   22     7
        //         / \
        // 6   15

        mSum = 0;

        getSum(tree.root);

        // Print the sum
        System.out.println(mSum);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# A binary tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Stores the desired result
mSum = 0

# Function to find the sum of nodes
# with subtree sums of opposite parities
def getSum(root):

    global mSum

    # Return 0, if node is None
    if (root == None):
        return 0

    # Recursively call left and
    # right subtree
    lSum = getSum(root.left)
    rSum = getSum(root.right)

    # Update mSum, if one subtree
    # sum is even and another is odd
    if (lSum != 0 and rSum != 0):
        if ((lSum + rSum) % 2 != 0):
            mSum += root.data

    # Return the sum of subtree
    return lSum + rSum + root.data

# Driver Code
if __name__ == '__main__':

    # Given number of nodes
    n = 9

    # Binary tree formation
    root = Node(11)
    root.left = Node(23)
    root.right = Node(44)
    root.left.left = Node(13)
    root.left.right = Node(9)
    root.right.left = Node(22)
    root.right.right = Node(7)
    root.right.left.left = Node(6)
    root.right.left.right = Node(15)

    #     11
    #   /     \
    #  23       44
    # /  \     /   \
    #13   9   22     7
    #        / \
    #       6   15

    mSum = 0

    getSum(root)

    # Print the sum
    print(mSum)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    // Constructor
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// Binary Tree Class
class BinaryTree{

// Stores the desired result
static int mSum;

Node root;

// Function to find the sum of nodes
// with subtree sums of opposite parities
static int getSum(Node root)
{

    // Return 0, if node is null
    if (root == null)
        return 0;

    // Recursively call left and
    // right subtree
    int lSum = getSum(root.left);
    int rSum = getSum(root.right);

    // Update mSum, if one subtree
    // sum is even and another is odd
    if (lSum != 0 && rSum != 0)
        if ((lSum + rSum) % 2 != 0)
            mSum += root.data;

    // Return the sum of subtree
    return lSum + rSum + root.data;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number of nodes
    //int n = 9;

    BinaryTree tree = new BinaryTree();

    // Binary tree formation
    tree.root = new Node(11);
    tree.root.left = new Node(23);
    tree.root.right = new Node(44);
    tree.root.left.left = new Node(13);
    tree.root.left.right = new Node(9);
    tree.root.right.left = new Node(22);
    tree.root.right.right = new Node(7);
    tree.root.right.left.left = new Node(6);
    tree.root.right.left.right = new Node(15);

    //       11
    //    /     \
    //   23       44
    //  /  \     /   \
    // 13   9   22     7
    //         / \
    //        6   15
    mSum = 0;

    getSum(tree.root);

    // Print the sum
    Console.WriteLine(mSum);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// A binary tree node
class Node
{
    constructor(item)
    {
        this.left = null;
        this.right = null;
        this.data = item;
    }
}

// Stores the desired result
let mSum;

let root;

class BinaryTree
{
    constructor()
    {
        this.root = null;
    }
}

// Function to find the sum of nodes
// with subtree sums of opposite parities
function getSum(root)
{

    // Return 0, if node is null
    if (root == null)
        return 0;

    // Recursively call left and
    // right subtree
    let lSum = getSum(root.left);
    let rSum = getSum(root.right);

    // Update mSum, if one subtree
    // sum is even and another is odd
    if (lSum != 0 && rSum != 0)
        if ((lSum + rSum) % 2 != 0)
            mSum += root.data;

    // Return the sum of subtree
    return lSum + rSum + root.data;
}

// Driver code

// Given number of nodes
let n = 9;

let tree = new BinaryTree();

// Binary tree formation
tree.root = new Node(11);
tree.root.left = new Node(23);
tree.root.right = new Node(44);
tree.root.left.left = new Node(13);
tree.root.left.right = new Node(9);
tree.root.right.left = new Node(22);
tree.root.right.right = new Node(7);
tree.root.right.left.left = new Node(6);
tree.root.right.left.right = new Node(15);

//      11
//    /     \
//   23       44
//  /  \     /   \
// 13   9   22     7
//         / \
//        6   15

mSum = 0;

getSum(tree.root);

// Print the sum
document.write(mSum);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
33
```

***时间复杂度:** O(N)，其中 N 是二叉树中的节点数。*
***辅助空间:** O(1)*