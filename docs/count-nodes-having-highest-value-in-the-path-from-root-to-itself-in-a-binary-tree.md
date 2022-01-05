# 计算二叉树中从根到自身的路径中具有最高值的节点

> 原文:[https://www . geeksforgeeks . org/count-二叉树中从根到自身路径中具有最高值的节点/](https://www.geeksforgeeks.org/count-nodes-having-highest-value-in-the-path-from-root-to-itself-in-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算二叉树中的节点数，这些节点是从根到该节点的路径中值最高的节点。

**示例:**

> **输入:**下面是给定的树:
> **3
> /\
> 2 5
> /\
> 4 6
> **输出:** 4
> **说明:**
> 根节点满足要求条件。
> 节点 5 是路径中值最高的节点(3 - > 5)。
> 节点 6 是路径中值最高的节点(3 - > 5 - > 6)。
> 节点 4 是路径中值最高的节点(3 - > 2 - > 4)。
> 因此，给定的二叉树中总共有 4 个这样的节点。**
> 
> ****输入:**下面是给定的树:
> **3
> /\
> 1 2
> /\
> 4 6
> **输出:** 3****

******方法:**想法是执行给定二叉树的[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)，并在每次[递归](https://www.geeksforgeeks.org/recursion/)调用后更新路径中迄今为止获得的最大值节点。请遵循以下步骤:****

*   ****在给定的二叉树上执行[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)****
*   ****每次递归调用后，更新从根节点到当前节点的路径中到目前为止遇到的最大值节点。****
*   ****如果该节点的值超过了路径中到目前为止的最大值节点，则将**计数**增加 **1** ，并更新到目前为止获得的最大值。****
*   ****前进到当前节点的子树。****
*   ****二叉树遍历完成后，打印得到的**计数**。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the ct of
// nodes which are maximum
// in the path from root
// to the current node
int ct = 0;

// Binary Tree Node
struct Node
{
    int val;
    Node *left, *right;

    Node(int x)
    {
        val = x;
        left = right = NULL;
    }
};

// Function that performs Inorder
// Traversal on the Binary Tree
void find(Node *root, int mx)
{

    // If root does not exist
    if (root == NULL)
      return;

    // Check if the node
    // satisfies the condition
    if (root->val >= mx)
        ct++;

    // Update the maximum value
    // and recursively traverse
    // left and right subtree
    find(root->left, max(mx, root->val));

    find(root->right, max(mx, root->val));
}

// Function that counts the good
// nodes in the given Binary Tree
int NodesMaxInPath(Node* root)
{

    // Perform inorder Traversal
    find(root, INT_MIN);

    // Return the final count
    return ct;
}

// Driver code
int main()
{

    /* A Binary Tree
              3
             / \
            2   5
           /     \
          4       6
        */
    Node* root = new Node(3);
    root->left = new Node(2);
    root->right = new Node(5);
    root->left->left = new Node(4);
    root->right->right = new Node(7);

    // Function call
    int answer = NodesMaxInPath(root);

    // Print the count of good nodes
    cout << (answer);
    return 0;
}

// This code is contributed by mohit kumar 29**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GfG {

    // Stores the count of
    // nodes which are maximum
    // in the path from root
    // to the current node
    static int count = 0;

    // Binary Tree Node
    static class Node {
        int val;
        Node left, right;
    }

    // Function that performs Inorder
    // Traversal on the Binary Tree
    static void find(Node root, int max)
    {
        // If root does not exist
        if (root == null)
            return;

        // Check if the node
        // satisfies the condition
        if (root.val >= max)
            count++;

        // Update the maximum value
        // and recursively traverse
        // left and right subtree
        find(root.left,
             Math.max(max, root.val));

        find(root.right,
             Math.max(max, root.val));
    }

    // Function that counts the good
    // nodes in the given Binary Tree
    static int NodesMaxInPath(Node root)
    {
        // Perform inorder Traversal
        find(root, Integer.MIN_VALUE);

        // Return the final count
        return count;
    }

    // Function that add the new node
    // in the Binary Tree
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.val = data;
        temp.left = null;
        temp.right = null;

        // Return the node
        return temp;
    }

    // Driver Code
    public static void main(String[] args)
    {
        /* A Binary Tree
              3
             / \
            2   5
           /     \
          4       6
        */

        Node root = null;
        root = newNode(3);
        root.left = newNode(2);
        root.right = newNode(5);
        root.left.left = newNode(4);
        root.right.right = newNode(7);

        // Function Call
        int answer = NodesMaxInPath(root);

        // Print the count of good nodes
        System.out.println(answer);
    }
}**
```

## ****蟒蛇 3****

```
**# Python 3 program for the
# above approach
import sys

# Stores the ct of
# nodes which are maximum
# in the path from root
# to the current node
ct = 0

# Binary Tree Node
class newNode:

    def __init__(self, x):

        self.val = x
        self.left = None
        self.right = None

# Function that performs Inorder
# Traversal on the Binary Tree
def find(root, mx):

    global ct

    # If root does not exist
    if (root == None):
        return

    # Check if the node
    # satisfies the condition
    if (root.val >= mx):
        ct += 1

    # Update the maximum value
    # and recursively traverse
    # left and right subtree
    find(root.left,
         max(mx, root.val))

    find(root.right,
         max(mx, root.val))

# Function that counts
# the good nodes in the
# given Binary Tree
def NodesMaxInPath(root):

    global ct

    # Perform inorder
    # Traversal
    find(root,
         -sys.maxsize-1)

    # Return the final count
    return ct

# Driver code
if __name__ == '__main__':

    '''
    /* A Binary Tree
              3
             / /
            2   5
           /     /
          4       6
        */
    '''
    root = newNode(3)
    root.left = newNode(2)
    root.right = newNode(5)
    root.left.left = newNode(4)
    root.right.right = newNode(7)

    # Function call
    answer = NodesMaxInPath(root)

    # Print the count of good nodes
    print(answer)

# This code is contributed by Surendra_Gangwar**
```

## ****C#****

```
**// C# program for
// the above approach
using System;
class GfG{

// Stores the count of
// nodes which are maximum
// in the path from root
// to the current node
static int count = 0;

// Binary Tree Node
public class Node
{
  public int val;
  public Node left,
              right;
}

// Function that performs
// Inorder Traversal on
// the Binary Tree
static void find(Node root,
                 int max)
{
  // If root does not exist
  if (root == null)
    return;

  // Check if the node
  // satisfies the condition
  if (root.val >= max)
    count++;

  // Update the maximum value
  // and recursively traverse
  // left and right subtree
  find(root.left,
  Math.Max(max, root.val));

  find(root.right,
  Math.Max(max, root.val));
}

    // Function that counts the good
    // nodes in the given Binary Tree
    static int NodesMaxInPath(Node root)
    {
        // Perform inorder Traversal
        find(root, int.MinValue);

        // Return the readonly count
        return count;
    }

// Function that add the new node
// in the Binary Tree
static Node newNode(int data)
{
  Node temp = new Node();
  temp.val = data;
  temp.left = null;
  temp.right = null;

  // Return the node
  return temp;
}

// Driver Code
public static void Main(String[] args)
{
  /* A Binary Tree
              3
             / \
            2   5
           /     \
          4       6
        */

  Node root = null;
  root = newNode(3);
  root.left = newNode(2);
  root.right = newNode(5);
  root.left.left = newNode(4);
  root.right.right = newNode(7);

  // Function Call
  int answer = NodesMaxInPath(root);

  // Print the count of good nodes
  Console.WriteLine(answer);
}
}

// This code is contributed by Princi Singh**
```

## ****java 描述语言****

```
**<script>

// Javascript program for the above approach

// Stores the count of
// nodes which are maximum
// in the path from root
// to the current node
let count = 0;

// Binary Tree Node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.val = data;
    }
}

// Function that add the new node
// in the Binary Tree
function newNode(data)
{
    let temp = new Node(data);

    // Return the node
    return temp;
}

// Function that performs Inorder
// Traversal on the Binary Tree
function find(root, max)
{

    // If root does not exist
    if (root == null)
        return;

    // Check if the node
    // satisfies the condition
    if (root.val >= max)
        count++;

    // Update the maximum value
    // and recursively traverse
    // left and right subtree
    find(root.left, Math.max(max, root.val));

    find(root.right, Math.max(max, root.val));
}

// Function that counts the good
// nodes in the given Binary Tree
function NodesMaxInPath(root)
{

    // Perform inorder Traversal
    find(root, Number.MIN_VALUE);

    // Return the final count
    return count;
}

// Driver code

/* A Binary Tree
     3
    / \
   2   5
  /     \
 4       6
*/

let root = null;
root = newNode(3);
root.left = newNode(2);
root.right = newNode(5);
root.left.left = newNode(4);
root.right.right = newNode(7);

// Function Call
let answer = NodesMaxInPath(root);

// Print the count of good nodes
document.write(answer);  

// This code is contributed by suresh07

</script>**
```

******Output:** 

```
4
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(1)****