# 打印有孙子的二叉树节点

> 原文:[https://www . geeksforgeeks . org/print-the-nodes-of-二叉树-生孙子/](https://www.geeksforgeeks.org/print-the-nodes-of-binary-tree-having-a-grandchild/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印有孙子的节点。

**示例:**

> **输入:**
> 
> ![](img/ae078ad8076f4037455e36c727f3a716.png)
> 
> **输出:** 20 8
> **说明:**
> 20 和 8 是 4、12 和 10、14 的祖辈。
> 
> **输入:**
> 
> ![](img/a56a97a94d1494cb6ff074f8191f123a.png)
> 
> **输出:** 1
> **说明:**
> 1 是 4、5 的祖父母。

**方法:**思路采用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  在每个节点遍历给定的树。
2.  检查每个节点是否有子节点。
3.  对于任何树节点(比如 **temp** )，如果下面的节点之一存在，那么当前节点就是祖父节点:
    *   temp->左侧->左侧。
    *   temp->左->右。
    *   temp->右->左。
    *   temp->right->right。
4.  如果任何节点 **temp** 存在上述任何一种情况，则节点 **temp** 是祖父母节点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct node {
    struct node *left, *right;
    int key;
};

// Function to create new tree node
node* newNode(int key)
{
    node* temp = new node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to print the nodes of
// the Binary Tree having a grandchild
void cal(struct node* root)
{
    // Base case to check
    // if the tree exists

    if (root == NULL)
        return;

    else {

        // Check if there is a left and
        // right child of the curr node
        if (root->left != NULL
            && root->right != NULL) {

            // Check for grandchildren
            if (root->left->left != NULL
                || root->left->right != NULL
                || root->right->left != NULL
                || root->right->right != NULL) {

                // Print the node's key
                cout << root->key << " ";
            }
        }

        // Check if the left child
        // of node is not null
        else if (root->left != NULL) {

            // Check for grandchildren
            if (root->left->left != NULL
                || root->left->right != NULL) {
                cout << root->key << " ";
            }
        }

        // Check if the right child
        // of node is not null
        else if (root->right != NULL) {

            // Check for grandchildren
            if (root->right->left != NULL
                || root->right->right != NULL) {
                cout << root->key << " ";
            }
        }

        // Recursive call on left and
        // right subtree
        cal(root->left);
        cal(root->right);
    }
}

// Driver Code
int main()
{
    // Given Tree
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    // Function Call
    cal(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// A Binary Tree Node
static class node
{
    node left, right;
    int key;
};

// Function to create new tree node
static node newNode(int key)
{
    node temp = new node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
}

// Function to print the nodes of
// the Binary Tree having a grandchild
static void cal(node root)
{

    // Base case to check
    // if the tree exists
    if (root == null)
        return;

    else
    {

        // Check if there is a left and
        // right child of the curr node
        if (root.left != null &&
           root.right != null)
        {

            // Check for grandchildren
            if (root.left.left != null ||
               root.left.right != null ||
               root.right.left != null ||
              root.right.right != null)
            {

                // Print the node's key
                System.out.print(root.key + " ");
            }
        }

        // Check if the left child
        // of node is not null
        else if (root.left != null)
        {

            // Check for grandchildren
            if (root.left.left != null ||
               root.left.right != null)
            {
                System.out.print(root.key + " ");
            }
        }

        // Check if the right child
        // of node is not null
        else if (root.right != null)
        {

            // Check for grandchildren
            if (root.right.left != null ||
               root.right.right != null)
            {
                System.out.print(root.key + " ");
            }
        }

        // Recursive call on left and
        // right subtree
        cal(root.left);
        cal(root.right);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Tree
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    // Function call
    cal(root);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# A Binary Tree Node
class newNode:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to print the nodes
# of the Binary Tree having a
# grandchild
def cal(root):

    # Base case to check
    # if the tree exists
    if (root == None):
        return

    else:
        # Check if there is a left
        # and right child of the
        # curr node
        if (root.left != None and
            root.right != None):

            # Check for grandchildren
            if (root.left.left != None or
                root.left.right != None or
                root.right.left != None or
                root.right.right != None):

                # Print the node's key
                print(root.key, end = " ")

        # Check if the left child
        # of node is not None
        elif (root.left != None):

            # Check for grandchildren
            if (root.left.left != None or
                root.left.right != None):
                print(root.key, end = " ")

        # Check if the right child
        # of node is not None
        elif(root.right != None):

            # Check for grandchildren
            if (root.right.left != None or
                root.right.right != None):
                print(root.key, end = " ")

        # Recursive call on left and
        # right subtree
        cal(root.left)
        cal(root.right)

# Driver Code
if __name__ == '__main__':

    # Given Tree
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)

    # Function Call
    cal(root)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// A Binary Tree Node
public class node
{
  public node left, right;
  public int key;
};

// Function to create new
// tree node
static node newNode(int key)
{
  node temp = new node();
  temp.key = key;
  temp.left = temp.right = null;
  return temp;
}

// Function to print the
// nodes of the Binary Tree
// having a grandchild
static void cal(node root)
{
  // Base case to check
  // if the tree exists
  if (root == null)
    return;

  else
  {
    // Check if there is a left and
    // right child of the curr node
    if (root.left != null &&
        root.right != null)
    {
      // Check for grandchildren
      if (root.left.left != null ||
          root.left.right != null ||
          root.right.left != null ||
          root.right.right != null)
      {
        // Print the node's key
        Console.Write(root.key + " ");
      }
    }

    // Check if the left child
    // of node is not null
    else if (root.left != null)
    {
      // Check for grandchildren
      if (root.left.left != null ||
          root.left.right != null)
      {
        Console.Write(root.key + " ");
      }
    }

    // Check if the right child
    // of node is not null
    else if (root.right != null)
    {
      // Check for grandchildren
      if (root.right.left != null ||
          root.right.right != null)
      {
        Console.Write(root.key + " ");
      }
    }

    // Recursive call on left and
    // right subtree
    cal(root.left);
    cal(root.right);
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given Tree
  node root = newNode(1);
  root.left = newNode(2);
  root.right = newNode(3);
  root.left.left = newNode(4);
  root.left.right = newNode(5);

  // Function call
  cal(root);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // A Binary Tree Node
    class node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Function to create new tree node
    function newNode(key)
    {
        let temp = new node(key);
        return temp;
    }

    // Function to print the nodes of
    // the Binary Tree having a grandchild
    function cal(root)
    {

        // Base case to check
        // if the tree exists
        if (root == null)
            return;

        else
        {

            // Check if there is a left and
            // right child of the curr node
            if (root.left != null &&
               root.right != null)
            {

                // Check for grandchildren
                if (root.left.left != null ||
                   root.left.right != null ||
                   root.right.left != null ||
                  root.right.right != null)
                {

                    // Print the node's key
                    document.write(root.key + " ");
                }
            }

            // Check if the left child
            // of node is not null
            else if (root.left != null)
            {

                // Check for grandchildren
                if (root.left.left != null ||
                   root.left.right != null)
                {
                    document.write(root.key + " ");
                }
            }

            // Check if the right child
            // of node is not null
            else if (root.right != null)
            {

                // Check for grandchildren
                if (root.right.left != null ||
                   root.right.right != null)
                {
                    document.write(root.key + " ");
                }
            }

            // Recursive call on left and
            // right subtree
            cal(root.left);
            cal(root.right);
        }
    }

    // Given Tree
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    // Function call
    cal(root);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
1
```

**时间复杂度:** *O(N)* ，其中 N 为节点数。
**辅助空间:** *O(N)*