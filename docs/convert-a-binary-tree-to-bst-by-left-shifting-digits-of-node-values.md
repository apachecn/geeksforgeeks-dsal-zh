# 通过向左移动节点值的位数将二叉树转换为 BST

> 原文:[https://www . geesforgeks . org/convert-a-二叉树-BST-by-左移-数字-节点-值/](https://www.geeksforgeeks.org/convert-a-binary-tree-to-bst-by-left-shifting-digits-of-node-values/)

给定正整数的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)。任务是使用节点数字的左移操作将其转换为 **BST** 。如果无法将二叉树转换为 **BST** 则打印 **-1** 。

**示例:**

> **输入:**443
> /\
> 132 543
> /\
> 343 237
> 
> **输出:**344
> /\
> 132 435
> /\
> 433 723
> 
> **说明:** 443 →左移两次→ 344
> 132 →零档操作→ 132
> 543 →左移一次→ 435
> 343 →左移一次→ 433
> 237 →左移两次→ 723
> 
> **输入:** 43
> / \
> 56 45
> 
> **输出:** -1

**方法:**想法是在[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)上以递增的顺序执行[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)，因为 **BST** 的有序遍历总是生成排序的序列。按照以下步骤解决问题:

*   初始化一个变量，比如 **prev = -1** ，以跟踪前一个节点的值。
*   然后，[使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[顺序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)遍历树，并试图通过向左移动其数字将每个节点转换为大于前一个值的最低可能值。
*   执行这些操作后，[检查二叉树是否是 **BST** 或者不是](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-bst-simple-and-efficient-approach/)。
*   如果发现是真的，打印树。否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
struct TreeNode
{
   int val;
   TreeNode *left, *right;

    TreeNode(int key)
    {
        val = key;
        left = NULL;
        right = NULL;
    }
};

// Function to check if
// the tree is BST or not
bool isBST(TreeNode *root, TreeNode *l = NULL, TreeNode *r = NULL)
{

    // Base condition
    if (!root)
        return true;

    // Check for left child
    if (l && root->val <= l->val)
        return false;

    // Check for right child
    if (r && root->val >= r->val)
        return false;

    // Check for left and right subtrees
    return isBST(root->left, l, root) and isBST(root->right, root, r);
}

// Function to convert a tree to BST
// by left shift of its digits
void ConvTree(TreeNode *root,int &prev)
{

    // If root is NULL
    if (!root)
        return;

    // Recursively modify the
    // left subtree
    ConvTree(root->left,prev);

    // Initialise optimal element
    // to the initial element
    int optEle = root->val;

    // Convert it into a string
    string strEle = to_string(root->val);

    // For checking all the
    // left shift operations
    bool flag = true;
    for (int idx = 0; idx < strEle.size(); idx++)
    {

        // Perform left shift
        int shiftedNum = stoi(strEle.substr(idx) + strEle.substr(0, idx));

        // If the number after left shift
        // is the minimum and greater than
        // its previous element

        // first value >= prev

        // used to setup initialize optEle
        // cout<<prev<<endl;
        if (shiftedNum >= prev and flag)
        {
            optEle = shiftedNum;
            flag = false;
          }

        if (shiftedNum >= prev)
            optEle = min(optEle, shiftedNum);
      }
    root->val = optEle;
    prev = root->val;

    // Recursively solve for right
    // subtree
    ConvTree(root->right,prev);
}

// Function to print level
// order traversal of a tree
void levelOrder(TreeNode *root)
{
    queue<TreeNode*> que;
    que.push(root);
    while(true)
    {
        int length = que.size();
        if (length == 0)
            break;
        while (length)
        {
            auto temp = que.front();
            que.pop();
            cout << temp->val << " ";
            if (temp->left)
                que.push(temp->left);
            if (temp->right)
                que.push(temp->right);
            length -= 1;
          }
          cout << endl;
        }

        // new line
        cout << endl;
}

// Driver Code
int main()
{

  TreeNode *root = new TreeNode(443);
  root->left = new TreeNode(132);
  root->right = new TreeNode(543);
  root->right->left = new TreeNode(343);
  root->right->right = new TreeNode(237);

  // Converts the tree to BST
  int prev = -1;
  ConvTree(root, prev);

  // If tree is converted to a BST
  if (isBST(root, NULL, NULL))
  {
      // Print its level order traversal
      levelOrder(root);
    }
  else
  {

      // not possible
      cout << (-1);
    }
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int prev;

// Structure of a Node
static class TreeNode
{
    int val;
    TreeNode left, right;

    TreeNode(int key)
    {
        val = key;
        left = null;
        right = null;
    }
};

// Function to check if
// the tree is BST or not
static boolean isBST(TreeNode root, TreeNode l,
                     TreeNode r)
{

    // Base condition
    if (root == null)
        return true;

    // Check for left child
    if (l != null && root.val <= l.val)
        return false;

    // Check for right child
    if (r != null && root.val >= r.val)
        return false;

    // Check for left and right subtrees
    return isBST(root.left, l, root) &
           isBST(root.right, root, r);
}

// Function to convert a tree to BST
// by left shift of its digits
static void ConvTree(TreeNode root)
{

    // If root is null
    if (root == null)
        return;

    // Recursively modify the
    // left subtree
    ConvTree(root.left);

    // Initialise optimal element
    // to the initial element
    int optEle = root.val;

    // Convert it into a String
    String strEle = String.valueOf(root.val);

    // For checking all the
    // left shift operations
    boolean flag = true;

    for(int idx = 0; idx < strEle.length(); idx++)
    {

        // Perform left shift
        int shiftedNum = Integer.parseInt(
            strEle.substring(idx) +
            strEle.substring(0, idx));

        // If the number after left shift
        // is the minimum and greater than
        // its previous element

        // first value >= prev

        // used to setup initialize optEle
        // System.out.print(prev<<endl;
        if (shiftedNum >= prev && flag)
        {
            optEle = shiftedNum;
            flag = false;
        }

        if (shiftedNum >= prev)
            optEle = Math.min(optEle, shiftedNum);
    }
    root.val = optEle;
    prev = root.val;

    // Recursively solve for right
    // subtree
    ConvTree(root.right);
}

// Function to print level
// order traversal of a tree
static void levelOrder(TreeNode root)
{
    Queue<TreeNode> que = new LinkedList<GFG.TreeNode>();
    que.add(root);

    while(true)
    {
        int length = que.size();

        if (length == 0)
            break;

        while (length > 0)
        {
            TreeNode temp = que.peek();
            que.remove();
            System.out.print(temp.val + " ");

            if (temp.left != null)
                que.add(temp.left);
            if (temp.right != null)
                que.add(temp.right);

            length -= 1;
        }
        System.out.println();
    }

    // New line
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    TreeNode root = new TreeNode(443);
    root.left = new TreeNode(132);
    root.right = new TreeNode(543);
    root.right.left = new TreeNode(343);
    root.right.right = new TreeNode(237);

    // Converts the tree to BST
    prev = -1;
    ConvTree(root);

    // If tree is converted to a BST
    if (isBST(root, null, null))
    {

        // Print its level order traversal
        levelOrder(root);
    }
    else
    {

        // not possible
        System.out.print(-1);
    }
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a Node
class TreeNode:
    def __init__(self, key):
        self.val = key
        self.left = None
        self.right = None

# Function to check if
# the tree is BST or not
def isBST(root, l = None, r = None):

    # Base condition
    if not root:
        return True

    # Check for left child
    if l and root.val <= l.val:
        return False

    # Check for right child
    if r and root.val >= r.val:
        return False

    # Check for left and right subtrees
    return isBST(root.left, l, root) and isBST(root.right, root, r)

# Function to convert a tree to BST
# by left shift of its digits
def ConvTree(root):
    global prev

    # If root is NULL
    if not root:
        return

    # Recursively modify the
    # left subtree
    ConvTree(root.left)

    # Initialise optimal element
    # to the initial element
    optEle = root.val

    # Convert it into a string
    strEle = str(root.val)

    # For checking all the
    # left shift operations
    flag = True

    for idx in range(len(strEle)):

        # Perform left shift
        shiftedNum = int(strEle[idx:] + strEle[:idx])

        # If the number after left shift
        # is the minimum and greater than
        # its previous element

        # first value >= prev

        # used to setup initialize optEle
        if shiftedNum >= prev and flag:
            optEle = shiftedNum
            flag = False

        if shiftedNum >= prev:
            optEle = min(optEle, shiftedNum)

    root.val = optEle
    prev = root.val
    # Recursively solve for right
    # subtree
    ConvTree(root.right)

# Function to print level
# order traversal of a tree
def levelOrder(root):
    que = [root]
    while True:
        length = len(que)
        if not length:
            break

        while length:
            temp = que.pop(0)
            print(temp.val, end =' ')
            if temp.left:
                que.append(temp.left)
            if temp.right:
                que.append(temp.right)
            length -= 1
        # new line
        print()

# Driver Code

root = TreeNode(443)
root.left = TreeNode(132)
root.right = TreeNode(543)
root.right.left = TreeNode(343)
root.right.right = TreeNode(237)

# Initialize to
# previous element
prev = -1

# Converts the tree to BST
ConvTree(root)

# If tree is converted to a BST
if isBST(root, None, None):

    # Print its level order traversal
    levelOrder(root)
else:
    # not possible
    print(-1)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

static int prev;

// Structure of a Node
class TreeNode
{
    public int val;
    public TreeNode left, right; 
    public TreeNode(int key)
    {
        val = key;
        left = null;
        right = null;
    }
};

// Function to check if
// the tree is BST or not
static bool isBST(TreeNode root, TreeNode l,
                     TreeNode r)
{

    // Base condition
    if (root == null)
        return true;

    // Check for left child
    if (l != null && root.val <= l.val)
        return false;

    // Check for right child
    if (r != null && root.val >= r.val)
        return false;

    // Check for left and right subtrees
    return isBST(root.left, l, root) &
           isBST(root.right, root, r);
}

// Function to convert a tree to BST
// by left shift of its digits
static void ConvTree(TreeNode root)
{

    // If root is null
    if (root == null)
        return;

    // Recursively modify the
    // left subtree
    ConvTree(root.left);

    // Initialise optimal element
    // to the initial element
    int optEle = root.val;

    // Convert it into a String
    String strEle = String.Join("", root.val);

    // For checking all the
    // left shift operations
    bool flag = true;

    for(int idx = 0; idx < strEle.Length; idx++)
    {

        // Perform left shift
        int shiftedNum = Int32.Parse(
            strEle.Substring(idx) +
            strEle.Substring(0, idx));

        // If the number after left shift
        // is the minimum and greater than
        // its previous element

        // first value >= prev

        // used to setup initialize optEle
        // Console.Write(prev<<endl;
        if (shiftedNum >= prev && flag)
        {
            optEle = shiftedNum;
            flag = false;
        }

        if (shiftedNum >= prev)
            optEle = Math.Min(optEle, shiftedNum);
    }
    root.val = optEle;
    prev = root.val;

    // Recursively solve for right
    // subtree
    ConvTree(root.right);
}

// Function to print level
// order traversal of a tree
static void levelOrder(TreeNode root)
{
    Queue<TreeNode> que = new Queue<GFG.TreeNode>();
    que.Enqueue(root);

    while(true)
    {
        int length = que.Count;
        if (length == 0)
            break;     
        while (length > 0)
        {
            TreeNode temp = que.Peek();
            que.Dequeue();
            Console.Write(temp.val + " ");      
            if (temp.left != null)
                que.Enqueue(temp.left);
            if (temp.right != null)
                que.Enqueue(temp.right);       
            length -= 1;
        }
        Console.WriteLine();
    }

    // New line
    Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
    TreeNode root = new TreeNode(443);
    root.left = new TreeNode(132);
    root.right = new TreeNode(543);
    root.right.left = new TreeNode(343);
    root.right.right = new TreeNode(237);

    // Converts the tree to BST
    prev = -1;
    ConvTree(root);

    // If tree is converted to a BST
    if (isBST(root, null, null))
    {

        // Print its level order traversal
        levelOrder(root);
    }
    else
    {

        // not possible
        Console.Write(-1);
    }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

  // JavaScript program for the above approach

  let prev;

  // Structure of a Node
  class TreeNode
  {
      constructor(key) {
         this.left = null;
         this.right = null;
         this.val = key;
      }
  }

  // Function to check if
  // the tree is BST or not
  function isBST(root, l, r)
  {

      // Base condition
      if (root == null)
          return true;

      // Check for left child
      if (l != null && root.val <= l.val)
          return false;

      // Check for right child
      if (r != null && root.val >= r.val)
          return false;

      // Check for left and right subtrees
      return isBST(root.left, l, root) &
             isBST(root.right, root, r);
  }

  // Function to convert a tree to BST
  // by left shift of its digits
  function ConvTree(root)
  {

      // If root is null
      if (root == null)
          return;

      // Recursively modify the
      // left subtree
      ConvTree(root.left);

      // Initialise optimal element
      // to the initial element
      let optEle = root.val;

      // Convert it into a String
      let strEle = (root.val).toString();

      // For checking all the
      // left shift operations
      let flag = true;

      for(let idx = 0; idx < strEle.length; idx++)
      {

          // Perform left shift
          let shiftedNum = parseInt(
              strEle.substring(idx) +
              strEle.substring(0, idx));

          // If the number after left shift
          // is the minimum and greater than
          // its previous element

          // first value >= prev

          // used to setup initialize optEle
          // Console.Write(prev<<endl;
          if (shiftedNum >= prev && flag)
          {
              optEle = shiftedNum;
              flag = false;
          }

          if (shiftedNum >= prev)
              optEle = Math.min(optEle, shiftedNum);
      }
      root.val = optEle;
      prev = root.val;

      // Recursively solve for right
      // subtree
      ConvTree(root.right);
  }

  // Function to print level
  // order traversal of a tree
  function levelOrder(root)
  {
      let que = [];
      que.push(root);

      while(true)
      {
          let length = que.length;
          if (length == 0)
              break;    
          while (length > 0)
          {
              let temp = que[0];
              que.shift();
              document.write(temp.val + " ");     
              if (temp.left != null)
                  que.push(temp.left);
              if (temp.right != null)
                  que.push(temp.right);      
              length -= 1;
          }
          document.write("</br>");
      }

      // New line
      document.write("</br>");
  }

  let root = new TreeNode(443);
  root.left = new TreeNode(132);
  root.right = new TreeNode(543);
  root.right.left = new TreeNode(343);
  root.right.right = new TreeNode(237);

  // Converts the tree to BST
  prev = -1;
  ConvTree(root);

  // If tree is converted to a BST
  if (isBST(root, null, null))
  {

      // Print its level order traversal
      levelOrder(root);
  }
  else
  {

      // not possible
      document.write(-1);
  }

</script>
```

**Output:** 

```
344 
132 435 
433 723
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)