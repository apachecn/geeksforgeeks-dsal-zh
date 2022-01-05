# 检查二叉树是否包含大小为 K 的平衡 BST

> 原文:[https://www . geesforgeks . org/check-if-the-binary-tree-contains-a-balanced-BST-of-size-k/](https://www.geeksforgeeks.org/check-if-the-binary-tree-contains-a-balanced-bst-of-size-k/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和一个正整数 **K** 。任务是检查给定二叉树中是否存在大小为 **K** 的平衡 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 。如果存在，则打印“**是”**否则打印“**否”**。

**示例:**

```
Input: K = 4,
Below is the given Tree:
         15
       /    \
      10     26
     /  \     / \
    5   12  25  40
           /   /  \
          20  35   50
                 \
                  60
Output: Yes
Explanation: 
Subtree of the given tree with
size k is given below:
        40
       /  \
      35   50
             \
             60

Input: K = 4,
Below is the given Tree:
            18
            /  
           9    
          / \
         7   10
Output: No
Explanation:
There is no subtree of size K
which forms a balanced BT.
```

**方法:**思路是使用[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。以下是解决问题的步骤:

1.  对给定的树执行后顺序遍历，检查每个节点的 **BST 条件** n，其中左侧子树中的**最大值**应小于当前值，右侧子树中的**较小值**应大于当前值。
2.  然后检查 BST 是否平衡，即左右子树的绝对差值应该是 **0 或 1** 。
3.  然后将从子树返回的值传递给父树。
4.  对所有节点执行上述步骤，取布尔变量*和*，初始标记为假，用于检查平衡的 BST 是否存在。
5.  如果找到大小为 **K** 的平衡 BST，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// A tree node
struct node {
    int data;
    node* left;
    node* right;
};

// Structure of temporary variable
struct minMax {
    bool isBST;
    bool balanced;
    int size;
    int height;
    int min;
    int max;
};

// Function to create the node
node* createNode(int value)
{
    node* temp = new node();
    temp->left = NULL;
    temp->right = NULL;
    temp->data = value;
}

// Utility function to find Balanced
// BST of size k
minMax findBalancedBstUtil(node* root,
                           int k, bool& ans)
{
    // Base condition
    if (root == NULL)
        return { true, true, 0, 0,
                 INT_MAX, INT_MIN };

    // Temporary variable
    minMax temp;

    // Recursive call for left sub-tree
    minMax lsTree
        = findBalancedBstUtil(root->left,
                              k, ans);

    if (ans == true)
        return temp;

    // Recursive call for right sub-tree
    minMax rsTree
        = findBalancedBstUtil(root->right,
                              k, ans);

    if (ans == true)
        return temp;

    // Check those conditions which
    // violated the rules of BST
    if (!lsTree.isBST || !rsTree.isBST
        || lsTree.max > root->data
        || rsTree.min < root->data) {
        temp.isBST = false;
        return temp;
    }

    // Check whether the Bst is
    // height balanced or not
    if (abs(lsTree.height
            - rsTree.height)
            == 1
        || abs(lsTree.height
               - rsTree.height)
               == 0)

        temp.balanced = true;

    else
        temp.balanced = false;

    // Make the variable true
    // as sub-tree is BST
    temp.isBST = true;

    // Store the size
    temp.size = 1 + lsTree.size
                + rsTree.size;

    // Store the height
    temp.height = max(lsTree.height,
                     rsTree.height)
                 + 1;

    // Store the minimum of BST
    temp.min = root->left != NULL
                   ? lsTree.min
                   : root->data;

    // Store the maximum of BST
    temp.max = root->right != NULL
                   ? rsTree.max
                   : root->data;

    // Condition to check whether the
    // size of Balanced BST is K or not
    if (temp.balanced == true
        && temp.size == k) {
        ans = true;
    }

    // Return the temporary variable
    // with updated data
    return temp;
}

// Function to find the Balanced
// BST of size k
string findBalancedBst(node* root,
                       int k)
{
    bool ans = false;

    // Utility function call
    findBalancedBstUtil(root, k, ans);
    return ans == true ? "Yes" : "No";
}

// Driver Code
int main()
{
    // Given Binary Tree
    node* root = createNode(15);
    root->left = createNode(10);
    root->right = createNode(26);
    root->left->left = createNode(5);
    root->left->right = createNode(12);
    root->right->left = createNode(25);
    root->right->left->left = createNode(20);
    root->right->right = createNode(40);
    root->right->right->left = createNode(35);
    root->right->right->right = createNode(50);
    root->right->right->right->right = createNode(60);

    int k = 4;

    // Function Call
    cout << findBalancedBst(root, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static boolean ans;

// A tree node
static class node
{
    int data;
    node left;
    node right;
};

// Structure of temporary variable
static class minMax
{
    boolean isBST;
    boolean balanced;
    int size;
    int height;
    int min;
    int max;

    public minMax(boolean isBST, boolean balanced,
                  int size, int height, int min,
                  int max)
    {
        super();
        this.isBST = isBST;
        this.balanced = balanced;
        this.size = size;
        this.height = height;
        this.min = min;
        this.max = max;
    }
    public minMax()
    {
        // TODO Auto-generated constructor stub
    }
};

// Function to create the node
static node createNode(int value)
{
    node temp = new node();
    temp.left = null;
    temp.right = null;
    temp.data = value;
    return temp;
}

// Utility function to find Balanced
// BST of size k
static minMax findBalancedBstUtil(node root,
                                  int k)
{

    // Base condition
    if (root == null)
        return new minMax(true, true, 0, 0,
                          Integer.MAX_VALUE,
                          Integer.MIN_VALUE );

    // Temporary variable
    minMax temp = new minMax();

    // Recursive call for left sub-tree
    minMax lsTree = findBalancedBstUtil(root.left,
                                        k);

    if (ans == true)
        return temp;

    // Recursive call for right sub-tree
    minMax rsTree = findBalancedBstUtil(root.right,
                                        k);

    if (ans == true)
        return temp;

    // Check those conditions which
    // violated the rules of BST
    if (!lsTree.isBST || !rsTree.isBST ||
         lsTree.max > root.data ||
         rsTree.min < root.data)
    {
        temp.isBST = false;
        return temp;
    }

    // Check whether the Bst is
    // height balanced or not
    if (Math.abs(lsTree.height -
                 rsTree.height) == 1 ||
        Math.abs(lsTree.height -
                 rsTree.height) == 0)
        temp.balanced = true;

    else
        temp.balanced = false;

    // Make the variable true
    // as sub-tree is BST
    temp.isBST = true;

    // Store the size
    temp.size = 1 + lsTree.size +
                    rsTree.size;

    // Store the height
    temp.height = Math.max(lsTree.height,
                          rsTree.height) + 1;

    // Store the minimum of BST
    temp.min = root.left != null ?
               lsTree.min : root.data;

    // Store the maximum of BST
    temp.max = root.right != null ?
               rsTree.max : root.data;

    // Condition to check whether the
    // size of Balanced BST is K or not
    if (temp.balanced == true &&
            temp.size == k)
    {
        ans = true;
    }

    // Return the temporary variable
    // with updated data
    return temp;
}

// Function to find the Balanced
// BST of size k
static String findBalancedBst(node root,
                              int k)
{
    ans = false;

    // Utility function call
    findBalancedBstUtil(root, k);
    return ans == true ? "Yes" : "No";
}

// Driver Code
public static void main(String[] args)
{

    // Given Binary Tree
    node root = createNode(15);
    root.left = createNode(10);
    root.right = createNode(26);
    root.left.left = createNode(5);
    root.left.right = createNode(12);
    root.right.left = createNode(25);
    root.right.left.left = createNode(20);
    root.right.right = createNode(40);
    root.right.right.left = createNode(35);
    root.right.right.right = createNode(50);
    root.right.right.right.right = createNode(60);

    int k = 4;

    // Function call
    System.out.print(findBalancedBst(root, k));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

ans = False

# A tree node
class createNode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Structure of temporary variable
class newMinMax:

    def __init__(self, isBST, balanced, size,
                 height, mn, mx):

        self.isBST = isBST
        self.balanced = balanced
        self.size = size
        self.height = height
        self.mn = mn
        self.mx = mx

# Utility function to find Balanced
# BST of size k
def findBalancedBstUtil(root, k):

    global ans

    # Base condition
    if (root == None):
        return newMinMax(True, True, 0, 0,
                         sys.maxsize,
                        -sys.maxsize - 1)

    # Temporary variable
    temp = newMinMax(True, True, 0, 0,
                     sys.maxsize,
                    -sys.maxsize - 1)

    # Recursive call for left sub-tree
    lsTree = findBalancedBstUtil(root.left, k)

    if (ans == True):
        return temp

    # Recursive call for right sub-tree
    rsTree = findBalancedBstUtil(root.right, k)

    if (ans == True):
        return temp

    # Check those conditions which
    # violated the rules of BST
    if (lsTree.isBST == False or
        rsTree.isBST == False or
        lsTree.mx > root.data or
        rsTree.mn < root.data):
        temp.isBST = False
        return temp

    # Check whether the Bst is
    # height balanced or not
    if (abs(lsTree.height - rsTree.height) == 1 or
        abs(lsTree.height - rsTree.height) == 0):
        temp.balanced = True
    else:
        temp.balanced = False

    # Make the variable true
    # as sub-tree is BST
    temp.isBST = True

    # Store the size
    temp.size = 1 + lsTree.size + rsTree.size

    # Store the height
    temp.height  = max(lsTree.height ,
                       rsTree.height) + 1

    # Store the minimum of BST
    if root.left != None:
        temp.mn = lsTree.mn
    else:
        temp.mn = root.data

    # Store the maximum of BST
    if root.right != None:
        temp.mx = rsTree.mx
    else:
        temp.mx = root.data

    # Condition to check whether the
    # size of Balanced BST is K or not
    if (temp.balanced == True and
        temp.size == k):
        ans = True

    # Return the temporary variable
    # with updated data
    return temp

# Function to find the Balanced
# BST of size k
def findBalancedBst(root, k):

    global ans

    # Utility function call
    findBalancedBstUtil(root, k)
    if ans == True:
        return "Yes"
    else:
        return "No"

# Driver Code
if __name__ == '__main__':

    # Given Binary Tree
    root = createNode(15)
    root.left = createNode(10)
    root.right = createNode(26)
    root.left.left = createNode(5)
    root.left.right = createNode(12)
    root.right.left = createNode(25)
    root.right.left.left = createNode(20)
    root.right.right = createNode(40)
    root.right.right.left = createNode(35)
    root.right.right.right = createNode(50)
    root.right.right.right.right = createNode(60)

    k = 4

    # Function Call
    print(findBalancedBst(root, k))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

static bool ans;

// A tree node
public class node
{
  public int data;
  public node left;
  public node right;
};

// Structure of temporary
// variable
public class minMax
{
  public bool isBST;
  public bool balanced;
  public int size;
  public int height;
  public int min;
  public int max;   
  public minMax(bool isBST, bool balanced,
                int size, int height, int min,
                int max)
  {
    this.isBST = isBST;
    this.balanced = balanced;
    this.size = size;
    this.height = height;
    this.min = min;
    this.max = max;
  }

  public minMax()
  {
    // TODO Auto-generated constructor stub
  }
};

// Function to create the node
static node createNode(int value)
{
  node temp = new node();
  temp.left = null;
  temp.right = null;
  temp.data = value;
  return temp;
}

// Utility function to find Balanced
// BST of size k
static minMax findBalancedBstUtil(node root,
                                  int k)
{
  // Base condition
  if (root == null)
    return new minMax(true, true, 0, 0,
                      int.MaxValue,
                      int.MinValue);

  // Temporary variable
  minMax temp = new minMax();

  // Recursive call for left sub-tree
  minMax lsTree =
         findBalancedBstUtil(root.left, k);

  if (ans == true)
    return temp;

  // Recursive call for right sub-tree
  minMax rsTree =
         findBalancedBstUtil(root.right, k);

  if (ans == true)
    return temp;

  // Check those conditions which
  // violated the rules of BST
  if (!lsTree.isBST || !rsTree.isBST ||
      lsTree.max > root.data ||
      rsTree.min < root.data)
  {
    temp.isBST = false;
    return temp;
  }

  // Check whether the Bst is
  // height balanced or not
  if (Math.Abs(lsTree.height -
               rsTree.height) == 1 ||
      Math.Abs(lsTree.height -
               rsTree.height) == 0)
    temp.balanced = true;

  else
    temp.balanced = false;

  // Make the variable true
  // as sub-tree is BST
  temp.isBST = true;

  // Store the size
  temp.size = 1 + lsTree.size +
                  rsTree.size;

  // Store the height
  temp.height = Math.Max(lsTree.height,
                        rsTree.height) + 1;

  // Store the minimum of BST
  temp.min = root.left != null ?
             lsTree.min : root.data;

  // Store the maximum of BST
  temp.max = root.right != null ?
             rsTree.max : root.data;

  // Condition to check whether the
  // size of Balanced BST is K or not
  if (temp.balanced == true &&
      temp.size == k)
  {
    ans = true;
  }

  // Return the temporary
  // variable with updated data
  return temp;
}

// Function to find the Balanced
// BST of size k
static String findBalancedBst(node root,
                              int k)
{
  ans = false;

  // Utility function call
  findBalancedBstUtil(root, k);
  return ans == true ? "Yes" : "No";
}

// Driver Code
public static void Main(String[] args)
{
  // Given Binary Tree
  node root = createNode(15);
  root.left = createNode(10);
  root.right = createNode(26);
  root.left.left = createNode(5);
  root.left.right = createNode(12);
  root.right.left = createNode(25);
  root.right.left.left = createNode(20);
  root.right.right = createNode(40);
  root.right.right.left = createNode(35);
  root.right.right.right = createNode(50);
  root.right.right.right.right = createNode(60);

  int k = 4;

  // Function call
  Console.Write(findBalancedBst(root, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program for the above approach
    let ans = false;

    // A tree Node
    class node
    {
        constructor(value) {
           this.left = null;
           this.right = null;
           this.data = value;
        }
    }

    // Structure of temporary variable
    class minMax
    {
        constructor(isBST, balanced, size, height, min, max)
        {
               this.isBST = isBST;
            this.balanced = balanced;
            this.size = size;
            this.height = height;
            this.min = min;
            this.max = max;
        }
    }

    // Function to create the node
    function createNode(value)
    {
        let temp = new node(value);
        return temp;
    }

    // Utility function to find Balanced
    // BST of size k
    function findBalancedBstUtil(root, k)
    {

        // Base condition
        if (root == null)
            return new minMax(true, true, 0, 0,
                              Number.MAX_VALUE,
                              Number.MIN_VALUE );

        // Temporary variable
        let temp = new minMax();

        // Recursive call for left sub-tree
        let lsTree = findBalancedBstUtil(root.left,
                                            k);

        if (ans == true)
            return temp;

        // Recursive call for right sub-tree
        let rsTree = findBalancedBstUtil(root.right,
                                            k);

        if (ans == true)
            return temp;

        // Check those conditions which
        // violated the rules of BST
        if (!lsTree.isBST || !rsTree.isBST ||
             lsTree.max > root.data ||
             rsTree.min < root.data)
        {
            temp.isBST = false;
            return temp;
        }

        // Check whether the Bst is
        // height balanced or not
        if (Math.abs(lsTree.height -
                     rsTree.height) == 1 ||
            Math.abs(lsTree.height -
                     rsTree.height) == 0)
            temp.balanced = true;

        else
            temp.balanced = false;

        // Make the variable true
        // as sub-tree is BST
        temp.isBST = true;

        // Store the size
        temp.size = 1 + lsTree.size +
                        rsTree.size;

        // Store the height
        temp.height = Math.max(lsTree.height,
                              rsTree.height) + 1;

        // Store the minimum of BST
        temp.min = root.left != null ?
                   lsTree.min : root.data;

        // Store the maximum of BST
        temp.max = root.right != null ?
                   rsTree.max : root.data;

        // Condition to check whether the
        // size of Balanced BST is K or not
        if (temp.balanced == true &&
                temp.size == k)
        {
            ans = true;
        }

        // Return the temporary variable
        // with updated data
        return temp;
    }

    // Function to find the Balanced
    // BST of size k
    function findBalancedBst(root, k)
    {
        ans = false;

        // Utility function call
        findBalancedBstUtil(root, k);
        return ans == true ? "Yes" : "No";
    }

    // Given Binary Tree
    let root = createNode(15);
    root.left = createNode(10);
    root.right = createNode(26);
    root.left.left = createNode(5);
    root.left.right = createNode(12);
    root.right.left = createNode(25);
    root.right.left.left = createNode(20);
    root.right.right = createNode(40);
    root.right.right.left = createNode(35);
    root.right.right.right = createNode(50);
    root.right.right.right.right = createNode(60);

    let k = 4;

    // Function call
    document.write(findBalancedBst(root, k));

 // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*