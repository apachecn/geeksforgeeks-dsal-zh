# 计算二叉树中存在的平衡节点数

> 原文:[https://www . geesforgeks . org/count-balanced-nodes-present-in-a-a-binary-tree/](https://www.geeksforgeeks.org/count-balanced-nodes-present-in-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是统计给定树中平衡节点的数量。

> **二叉树的平衡节点**被定义为包含左右子树的节点，它们各自的节点值之和相等。

**示例:**

> **输入:**
> 
> ```
>                    9
>                  /  \
>                 2   4 
>                / \   \
>              -1   3   0
> ```
> 
> **输出:** 1
> **说明:**
> 只有节点 9 包含左子树和=右子树和= 4
> 因此，需要的输出为 1。
> 
> **输入:**
> 
> ```
>  7
>                  / \
>                 4  10
>               /  \     
>             3    3
>           / \     \
>         0    0    -3
>                   /
>                  3
> ```
> 
> **输出:** 3

**方法:**想法是递归地[遍历给定二叉树的每个节点](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)。对于每个节点，计算左右子树中节点的[和，并检查计算的和是否相等。如果发现是真的，增加**计数**。最后，完成树的遍历后，打印**计数**](https://www.geeksforgeeks.org/sum-nodes-binary-tree/)

按照以下步骤解决问题:

1.  初始化一个变量，比如 **res** ，来存储平衡节点的数量
2.  递归计算每个节点的左右子树之和。
3.  检查计算的总和是否相等。
4.  如果发现为真，则当前节点是平衡的。因此，将**静止**增加 **1**
5.  最后，在完成树的遍历后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a
// Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};

// Function to get the sum of left
// subtree and right subtree
int Sum(Node* root, int& res)
{
    // Base case
    if (root == NULL) {
        return 0;
    }

    // Store the sum of
    // left subtree
    int leftSubSum
        = Sum(root->left, res);

    // Store the sum of
    // right subtree
    int rightSubSum
        = Sum(root->right, res);

    // Check if node is balanced or not
    if (root->left and root->right
        && leftSubSum == rightSubSum)

        // Increase count of
        // balanced nodes
        res += 1;

    // Return subtree sum
    return root->data + leftSubSum
           + rightSubSum;
}

// Driver Code
int main()
{

    /*
                   9
                 /  \
                2   4
               / \   \
             -1   3   0
    */

    // Insert nodes in tree
    Node* root = new Node(9);
    root->left = new Node(2);
    root->left->left = new Node(-1);
    root->left->right = new Node(3);
    root->right = new Node(4);
    root->right->right = new Node(0);

    // Store the count of balanced nodes
    int res = 0;
    Sum(root, res);
    cout << res;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

static int res = 0;

// Structure of a
// Tree Node
static class Node
{
  int data;
  Node left;
  Node right;
  Node(int val)
  {
    data = val;
    left = right = null;
  }
};

// Function to get the sum of left
// subtree and right subtree
static int Sum(Node root)
{
  // Base case
  if (root == null)
  {
    return 0;
  }

  // Store the sum of
  // left subtree
  int leftSubSum = Sum(root.left);

  // Store the sum of
  // right subtree
  int rightSubSum = Sum(root.right);

  // Check if node is balanced or not
  if (root.left != null && root.right != null &&
      leftSubSum == rightSubSum)

    // Increase count of
    // balanced nodes
    res += 1;

  // Return subtree sum
  return root.data + leftSubSum +
         rightSubSum;
}

// Driver Code
public static void main(String[] args)
{
  /*
                   9
                 /  \
                2   4
               / \   \
             -1   3   0
    */

  // Insert nodes in tree
  Node root = new Node(9);
  root.left = new Node(2);
  root.left.left = new Node(-1);
  root.left.right = new Node(3);
  root.right = new Node(4);
  root.right.right = new Node(0);

  // Store the count of balanced nodes
  res = 0;
  Sum(root);
  System.out.print(res);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of a  Tree Node
class Node:
    def __init__(self, val):

        self.data = val
        self.left = None
        self.right = None

# Function to get the sum of left
# subtree and right subtree
def Sum(root):

    global res

    # Base case
    if (root == None):
        return 0

    # Store the sum of
    # left subtree
    leftSubSum = Sum(root.left)

    # Store the sum of
    # right subtree
    rightSubSum = Sum(root.right)

    # Check if node is balanced or not
    if (root.left and root.right and
       leftSubSum == rightSubSum):

        # Increase count of
        # balanced nodes
        res += 1

    # Return subtree sum
    return (root.data + leftSubSum +
                        rightSubSum)

# Driver Code
"""
                  9
                 / \
                2   4 
               / \   \
             -1   3   0
"""
# Insert nodes in tree
root = Node(9)
root.left = Node(2)
root.left.left = Node(-1)
root.left.right = Node(3)
root.right = Node(4)
root.right.right = Node(0)

# Store the count of balanced nodes
global res
res = 0
Sum(root)
print(res)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static int res = 0;

// Structure of a
// Tree Node
public class Node
{
  public int data;
  public Node left;
  public Node right;
  public Node(int val)
  {
    data = val;
    left = right = null;
  }
};

// Function to get the sum of left
// subtree and right subtree
static int Sum(Node root)
{
  // Base case
  if (root == null)
  {
    return 0;
  }

  // Store the sum of
  // left subtree
  int leftSubSum = Sum(root.left);

  // Store the sum of
  // right subtree
  int rightSubSum = Sum(root.right);

  // Check if node is balanced or not
  if (root.left != null && root.right != null &&
      leftSubSum == rightSubSum)

    // Increase count of
    // balanced nodes
    res += 1;

  // Return subtree sum
  return root.data + leftSubSum +
         rightSubSum;
}

// Driver Code
public static void Main(String[] args)
{
  /*
                   9
                 /  \
                2   4
               / \   \
             -1   3   0
    */

  // Insert nodes in tree
  Node root = new Node(9);
  root.left = new Node(2);
  root.left.left = new Node(-1);
  root.left.right = new Node(3);
  root.right = new Node(4);
  root.right.right = new Node(0);

  // Store the count of balanced nodes
  res = 0;
  Sum(root);
  Console.Write(res);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    let res = 0;

    // Structure of a Tree Node
    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.data = val;
        }
    }

    // Function to get the sum of left
    // subtree and right subtree
    function Sum(root)
    {
      // Base case
      if (root == null)
      {
        return 0;
      }

      // Store the sum of
      // left subtree
      let leftSubSum = Sum(root.left);

      // Store the sum of
      // right subtree
      let rightSubSum = Sum(root.right);

      // Check if node is balanced or not
      if (root.left != null && root.right != null &&
          leftSubSum == rightSubSum)

        // Increase count of
        // balanced nodes
        res += 1;

      // Return subtree sum
      return root.data + leftSubSum +
             rightSubSum;
    }

    /*
                   9
                 /  \
                2   4
               / \   \
             -1   3   0
    */

    // Insert nodes in tree
    let root = new Node(9);
    root.left = new Node(2);
    root.left.left = new Node(-1);
    root.left.right = new Node(3);
    root.right = new Node(4);
    root.right.right = new Node(0);

    // Store the count of balanced nodes
    res = 0;
    Sum(root);
    document.write(res);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)