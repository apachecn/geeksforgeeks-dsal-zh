# 检查二叉树是否为 BST 的迭代方法

> 原文:[https://www . geesforgeks . org/迭代方法检查二叉树是否为 BST/](https://www.geeksforgeeks.org/iterative-approach-to-check-if-a-binary-tree-is-bst-or-not/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是检查给定的二叉树是否是[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)。如果发现属实，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**
> 
> ```
>              9
>             / \
>            6   10
>           / \   \
>          4   7   11
>         / \   \
>        3  5   8
> ```
> 
> **输出:** YES
> **说明:**由于树的每个节点的左子树由较小值的节点组成，而树的每个节点的右子树由较大值的节点组成。因此，要求的输出是“是”。
> 
> **输入:**
> 
> ```
>              5
>             / \
>            6   3
>           / \   \
>          4   9   2
> ```
> 
> **输出:**否

**递归方法:**参考[之前的帖子](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)用递归解决这个问题。
***时间复杂度:** O(N)其中 N 是二叉树中节点的个数。*
***辅助空间:** O(N)*

**迭代方式:**迭代解决问题，使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)。按照以下步骤解决问题:

*   初始化一个[栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)来存储节点及其左子树。
*   初始化一个变量，比如 **prev** ，来存储二叉树的前一个访问节点。
*   [遍历树](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)、[将每个节点的根节点和左子树推入栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)中，检查 **prev** 节点的数据值是否大于等于当前访问节点的数据值。如果发现是真的，则打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node
struct TreeNode {

    // Stores data value of a node
    int data;

    // Stores left subtree
    // of a tree node
    TreeNode* left;

    // Stores right subtree
    // of a tree node
    TreeNode* right;

    // Initialization of
    // a tree node
    TreeNode(int val)
    {
        // Update data
        data = val;

        // Update left and right
        left = right = NULL;
    }
};

// Function to check if a binary tree
// is binary search tree or not
bool checkTreeIsBST(TreeNode *root)
{
    // Stores root node and left
   // subtree of each node
    stack<TreeNode* > Stack;

    // Stores previous visited node
    TreeNode* prev = NULL;

    // Traverse the binary tree
    while (!Stack.empty() ||
               root != NULL) {

        // Traverse left subtree
        while (root != NULL) {

            // Insert root into Stack
            Stack.push(root);

            // Update root
            root = root->left;
        }

        // Stores top element of Stack
        root = Stack.top();

        // Remove the top element of Stack
        Stack.pop();

        // If data value of root node less
        // than data value of left subtree
        if(prev != NULL &&
               root->data <= prev->data) {
            return false;
        }

        // Update prev
        prev = root;

        // Traverse right subtree
        // of the tree
        root = root->right;
    }
    return true;
}

// Driver Code
int main()
{
      /* 
             9
            / \
           6   10
          / \   \
         4   7   11
        / \   \
       3  5   8

     */

    // Initialize binary tree
    TreeNode *root = new TreeNode(9);
    root->left = new TreeNode(6);
    root->right = new TreeNode(10);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(7);
    root->right->right = new TreeNode(11);
    root->left->left->left = new TreeNode(3);
    root->left->left->right = new TreeNode(5);
    root->left->right->right = new TreeNode(8);

    if (checkTreeIsBST(root)) {
        cout<<"YES";
    }
    else {
        cout<<"NO";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of a tree node
static class TreeNode {

    // Stores data value of a node
    int data;

    // Stores left subtree
    // of a tree node
    TreeNode left;

    // Stores right subtree
    // of a tree node
    TreeNode right;

    // Initialization of
    // a tree node
    TreeNode(int val)
    {
        // Update data
        data = val;

        // Update left and right
        left = right = null;
    }
};

// Function to check if a binary tree
// is binary search tree or not
static boolean checkTreeIsBST(TreeNode root)
{
    // Stores root node and left
   // subtree of each node
    Stack<TreeNode > Stack = new Stack<TreeNode >();

    // Stores previous visited node
    TreeNode prev = null;

    // Traverse the binary tree
    while (!Stack.isEmpty() ||
               root != null) {

        // Traverse left subtree
        while (root != null) {

            // Insert root into Stack
            Stack.add(root);

            // Update root
            root = root.left;
        }

        // Stores top element of Stack
        root = Stack.peek();

        // Remove the top element of Stack
        Stack.pop();

        // If data value of root node less
        // than data value of left subtree
        if(prev != null &&
               root.data <= prev.data) {
            return false;
        }

        // Update prev
        prev = root;

        // Traverse right subtree
        // of the tree
        root = root.right;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
      /* 
             9
            / \
           6   10
          / \   \
         4   7   11
        / \   \
       3  5   8

     */

    // Initialize binary tree
    TreeNode root = new TreeNode(9);
    root.left = new TreeNode(6);
    root.right = new TreeNode(10);
    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(7);
    root.right.right = new TreeNode(11);
    root.left.left.left = new TreeNode(3);
    root.left.left.right = new TreeNode(5);
    root.left.right.right = new TreeNode(8);

    if (checkTreeIsBST(root)) {
        System.out.print("YES");
    }
    else {
        System.out.print("NO");
    }
}
}
// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of a tree node
class TreeNode:

    def __init__(self, data: int) -> None:

        # Stores data value of a node
        self.data = data

        # Stores left subtree
        # of a tree node
        self.left = None

        # Stores right subtree
        # of a tree node
        self.right = None

# Function to check if a binary tree
# is binary search tree or not
def checkTreeIsBST(root: TreeNode) -> bool:

    # Stores root node and left
    # subtree of each node
    Stack = []

    # Stores previous visited node
    prev = None

    # Traverse the binary tree
    while (Stack or root):

        # Traverse left subtree
        while root:

            # Insert root into Stack
            Stack.append(root)

            # Update root
            root = root.left

        # Stores top element of Stack
        # Remove the top element of Stack
        root = Stack.pop()

        # If data value of root node less
        # than data value of left subtree
        if (prev and root.data <= prev.data):
            return False

        # Update prev
        prev = root

        # Traverse right subtree
        # of the tree
        root = root.right

    return True

# Driver Code
if __name__ == "__main__":

    '''
             9
            / \
           6   10
          / \   \
         4   7   11
        / \   \
       3  5   8

    '''

    # Initialize binary tree
    root = TreeNode(9)
    root.left = TreeNode(6)
    root.right = TreeNode(10)
    root.left.left = TreeNode(4)
    root.left.right = TreeNode(7)
    root.right.right = TreeNode(11)
    root.left.left.left = TreeNode(3)
    root.left.left.right = TreeNode(5)
    root.left.right.right = TreeNode(8)

    if checkTreeIsBST(root):
        print("YES")
    else:
        print("NO")

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Structure of a tree node
class TreeNode
{

    // Stores data value of a node
    public int data;

    // Stores left subtree
    // of a tree node
    public TreeNode left;

    // Stores right subtree
    // of a tree node
    public TreeNode right;

    // Initialization of
    // a tree node
    public TreeNode(int val)
    {

        // Update data
        data = val;

        // Update left and right
        left = right = null;
    }
};

// Function to check if a binary tree
// is binary search tree or not
static bool checkTreeIsBST(TreeNode root)
{

    // Stores root node and left
   // subtree of each node
    Stack<TreeNode > Stack = new Stack<TreeNode >();

    // Stores previous visited node
    TreeNode prev = null;

    // Traverse the binary tree
    while (Stack.Count!=0 ||
               root != null)
    {

        // Traverse left subtree
        while (root != null)
        {

            // Insert root into Stack
            Stack.Push(root);

            // Update root
            root = root.left;
        }

        // Stores top element of Stack
        root = Stack.Peek();

        // Remove the top element of Stack
        Stack.Pop();

        // If data value of root node less
        // than data value of left subtree
        if(prev != null &&
               root.data <= prev.data)
        {
            return false;
        }

        // Update prev
        prev = root;

        // Traverse right subtree
        // of the tree
        root = root.right;
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
      /* 
             9
            / \
           6   10
          / \   \
         4   7   11
        / \   \
       3  5   8

     */

    // Initialize binary tree
    TreeNode root = new TreeNode(9);
    root.left = new TreeNode(6);
    root.right = new TreeNode(10);
    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(7);
    root.right.right = new TreeNode(11);
    root.left.left.left = new TreeNode(3);
    root.left.left.right = new TreeNode(5);
    root.left.right.right = new TreeNode(8);

    if (checkTreeIsBST(root))
    {
        Console.Write("YES");
    }
    else
    {
        Console.Write("NO");
    }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Structure of a tree node
class TreeNode
{
    constructor(val)
    {

        // Stores left subtree
        // of a tree node
        this.left = null;

        // Stores right subtree
        // of a tree node
        this.right = null;

        // Stores data value of a node
        this.data = val;
    }
}

// Function to check if a binary tree
// is binary search tree or not
function checkTreeIsBST(root)
{

    // Stores root node and left
    // subtree of each node
    let Stack = [];

    // Stores previous visited node
    let prev = null;

    // Traverse the binary tree
    while (Stack.length > 0 || root != null)
    {

        // Traverse left subtree
        while (root != null)
        {

            // Insert root into Stack
            Stack.push(root);

            // Update root
            root = root.left;
        }

        // Stores top element of Stack
        root = Stack[Stack.length - 1];

        // Remove the top element of Stack
        Stack.pop();

        // If data value of root node less
        // than data value of left subtree
        if (prev != null &&
            root.data <= prev.data)
        {
            return false;
        }

        // Update prev
        prev = root;

        // Traverse right subtree
        // of the tree
        root = root.right;
    }
    return true;
}

// Driver code
/*
         9
        / \
       6   10
      / \   \
     4   7   11
    / \   \
   3  5   8

 */

// Initialize binary tree
let root = new TreeNode(9);
root.left = new TreeNode(6);
root.right = new TreeNode(10);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(7);
root.right.right = new TreeNode(11);
root.left.left.left = new TreeNode(3);
root.left.left.right = new TreeNode(5);
root.left.right.right = new TreeNode(8);

if (checkTreeIsBST(root))
{
    document.write("YES");
}
else
{
    document.write("NO");
}

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N)，其中 N 为二叉树*
***节点数辅助空间:** O(N)*