# 二叉树中祖辈为偶数的所有子节点之和

> 原文:[https://www . geeksforgeeks . org/二进制树中有偶数祖父母的所有子节点总和/](https://www.geeksforgeeks.org/sum-of-all-the-child-nodes-with-even-grandparents-in-a-binary-tree/)

给定一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，计算有偶值祖父母的节点的和。
**例:**

```
Input: 
      22
    /    \
   3      8
  / \    / \
 4   8  1   9
             \
              2
Output: 24
Explanation 
The nodes 4, 8, 2, 1, 9
has even value grandparents. 
Hence sum = 4 + 8 + 1 + 9 + 2 = 24.

Input:
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
  /
 8
Output: 8
Explanation 
Only 8 has 2 as a grandparent.
```

**方法:**为了解决上面提到的问题，对于每个不为空的节点，检查它们是否有祖父母，如果它们的祖父母是偶数，则将该节点的数据相加。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to find sum
// of all the child nodes with
// even grandparents in a Binary Tree

#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data and
pointers to the right and left children*/
struct TreeNode {
    int data;
    TreeNode *left, *right;
    TreeNode(int x)
    {
        data = x;
        left = right = NULL;
    }
};

// Function to calculate the sum
void getSum(
    TreeNode* curr, TreeNode* p,
    TreeNode* gp, int& sum)
{
    // Base condition
    if (curr == NULL)
        return;

    // Check if node has a grandparent
    // if it does check
    // if they are even valued
    if (gp != NULL && gp->data % 2 == 0)
        sum += curr->data;

    // Recurse for left child
    getSum(curr->left, curr, p, sum);

    // Recurse for right child
    getSum(curr->right, curr, p, sum);
}

// Driver Program
int main()
{
    TreeNode* root = new TreeNode(22);

    root->left = new TreeNode(3);
    root->right = new TreeNode(8);

    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(8);

    root->right->left = new TreeNode(1);
    root->right->right = new TreeNode(9);
    root->right->right->right = new TreeNode(2);

    int sum = 0;
    getSum(root, NULL, NULL, sum);
    cout << sum << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum
// of all the child nodes with
// even grandparents in a Binary Tree
import java.util.*;
class GFG{

/* A binary tree node has data and
pointers to the right and left children*/
static class TreeNode
{
  int data;
  TreeNode left, right;
  TreeNode(int x)
  {
    data = x;
    left = right = null;
  }
}

static int sum = 0;

// Function to calculate the sum
static void getSum(TreeNode curr,
                   TreeNode p,
                   TreeNode gp)
{
  // Base condition
  if (curr == null)
    return;

  // Check if node has
  // a grandparent
  // if it does check
  // if they are even valued
  if (gp != null && gp.data % 2 == 0)
    sum += curr.data;

  // Recurse for left child
  getSum(curr.left, curr, p);

  // Recurse for right child
  getSum(curr.right, curr, p);
}

// Driver Program
public static void main(String[] args)
{
  TreeNode root = new TreeNode(22);

  root.left = new TreeNode(3);
  root.right = new TreeNode(8);

  root.left.left = new TreeNode(4);
  root.left.right = new TreeNode(8);

  root.right.left = new TreeNode(1);
  root.right.right = new TreeNode(9);
  root.right.right.right = new TreeNode(2);

  getSum(root, null, null);
  System.out.println(sum);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find sum
# of all the child nodes with
# even grandparents in a Binary Tree

# A binary tree node has data and
# pointers to the right and left children
class TreeNode():

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

sum = 0

# Function to calculate the sum
def getSum(curr, p, gp):

    global sum

    # Base condition
    if (curr == None):
        return

    # Check if node has a grandparent
    # if it does check
    # if they are even valued
    if (gp != None and gp.data % 2 == 0):
        sum += curr.data

    # Recurse for left child
    getSum(curr.left, curr, p)

    # Recurse for right child
    getSum(curr.right, curr, p)

# Driver code
if __name__=="__main__":

    root = TreeNode(22)

    root.left = TreeNode(3)
    root.right = TreeNode(8)

    root.left.left = TreeNode(4)
    root.left.right = TreeNode(8)

    root.right.left = TreeNode(1)
    root.right.right = TreeNode(9)
    root.right.right.right = TreeNode(2)

    getSum(root, None, None)

    print(sum)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to find sum
// of all the child nodes with
// even grandparents in a Binary Tree
using System;
class GFG{

/* A binary tree node
has data and pointers to
the right and left children*/
class TreeNode
{
  public int data;
  public TreeNode left, right;
  public TreeNode(int x)
  {
    data = x;
    left = right = null;
  }
}

static int sum = 0;

// Function to calculate the sum
static void getSum(TreeNode curr,
                   TreeNode p,
                   TreeNode gp)
{
  // Base condition
  if (curr == null)
    return;

  // Check if node has
  // a grandparent
  // if it does check
  // if they are even valued
  if (gp != null && gp.data % 2 == 0)
    sum += curr.data;

  // Recurse for left child
  getSum(curr.left, curr, p);

  // Recurse for right child
  getSum(curr.right, curr, p);
}

// Driver Program
public static void Main(String[] args)
{
  TreeNode root = new TreeNode(22);

  root.left = new TreeNode(3);
  root.right = new TreeNode(8);

  root.left.left = new TreeNode(4);
  root.left.right = new TreeNode(8);

  root.right.left = new TreeNode(1);
  root.right.right = new TreeNode(9);
  root.right.right.right = new TreeNode(2);

  getSum(root, null, null);
  Console.WriteLine(sum);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript implementation to find sum
    // of all the child nodes with
    // even grandparents in a Binary Tree

    /* A binary tree node has data and
    pointers to the right and left children*/
    class TreeNode
    {
          constructor(x) {
           this.left = null;
           this.right = null;
           this.data = x;
          }
    }

    let sum = 0;

    // Function to calculate the sum
    function getSum(curr, p, gp)
    {
      // Base condition
      if (curr == null)
        return;

      // Check if node has
      // a grandparent
      // if it does check
      // if they are even valued
      if (gp != null && gp.data % 2 == 0)
        sum += curr.data;

      // Recurse for left child
      getSum(curr.left, curr, p);

      // Recurse for right child
      getSum(curr.right, curr, p);
    }

    let root = new TreeNode(22);

    root.left = new TreeNode(3);
    root.right = new TreeNode(8);

    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(8);

    root.right.left = new TreeNode(1);
    root.right.right = new TreeNode(9);
    root.right.right.right = new TreeNode(2);

    getSum(root, null, null);
    document.write(sum);

</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N)*
***空间复杂度:** O(H)* ，递归栈使用，其中 H =树的高度。