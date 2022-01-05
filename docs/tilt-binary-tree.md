# 二叉树的倾斜

> 原文:[https://www.geeksforgeeks.org/tilt-binary-tree/](https://www.geeksforgeeks.org/tilt-binary-tree/)

给定一棵二叉树，返回整棵树的倾斜度。树节点的倾斜度定义为所有左侧子树节点值之和与所有右侧子树节点值之和之间的绝对差值。空节点被分配为零的倾斜度。因此，整个树的倾斜被定义为所有节点的倾斜之和。
**例:**

```
Input :
    1
   / \
  2   3
Output : 1
Explanation: 
Tilt of node 2 : 0
Tilt of node 3 : 0
Tilt of node 1 : |2-3| = 1
Tilt of binary tree : 0 + 0 + 1 = 1

Input :
    4
   / \
  2   9
 / \   \
3   5   7
Output : 15
Explanation: 
Tilt of node 3 : 0
Tilt of node 5 : 0
Tilt of node 7 : 0
Tilt of node 2 : |3-5| = 2
Tilt of node 9 : |0-7| = 7
Tilt of node 4 : |(3+5+2)-(9+7)| = 6
Tilt of binary tree : 0 + 0 + 0 + 2 + 7 + 6 = 15
```

这个想法是递归遍历树。在遍历时，我们跟踪两件事，当前节点下的子树的根的总和，当前节点的倾斜。需要求和来计算父母的倾斜。

## C++

```
// CPP Program to find Tilt of Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to
left child and a pointer to right child */
struct Node {
    int val;
    struct Node *left, *right;
};

/* Recursive function to calculate Tilt of
  whole tree */
int traverse(Node* root, int* tilt)
{
    if (!root)
        return 0;

    // Compute tilts of left and right subtrees
    // and find sums of left and right subtrees
    int left = traverse(root->left, tilt);
    int right = traverse(root->right, tilt);

    // Add current tilt to overall
    *tilt += abs(left - right);

    // Returns sum of nodes under current tree
    return left + right + root->val;
}

/* Driver function to print Tilt of whole tree */
int Tilt(Node* root)
{
    int tilt = 0;
    traverse(root, &tilt);
    return tilt;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->val = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver code
int main()
{
    /* Let us construct a Binary Tree
        4
       / \
      2   9
     / \   \
    3   5   7 */

    Node* root = NULL;
    root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(9);
    root->left->left = newNode(3);
    root->left->right = newNode(8);
    root->right->right = newNode(7);
    cout << "The Tilt of whole tree is " << Tilt(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Tilt of Binary Tree
import java.util.*;
class GfG {

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node {
    int val;
    Node left, right;
}

/* Recursive function to calculate Tilt of
whole tree */
static class T{
    int tilt = 0;
}
static int traverse(Node root, T t )
{
    if (root == null)
        return 0;

    // Compute tilts of left and right subtrees
    // and find sums of left and right subtrees
    int left = traverse(root.left, t);
    int right = traverse(root.right, t);

    // Add current tilt to overall
    t.tilt += Math.abs(left - right);

    // Returns sum of nodes under current tree
    return left + right + root.val;
}

/* Driver function to print Tilt of whole tree */
static int Tilt(Node root)
{
    T t = new T();
    traverse(root, t);
    return t.tilt;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void main(String[] args)
{
    /* Let us construct a Binary Tree
        4
    / \
    2 9
    / \ \
    3 5 7 */

    Node root = null;
    root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(9);
    root.left.left = newNode(3);
    root.left.right = newNode(8);
    root.right.right = newNode(7);
    System.out.println("The Tilt of whole tree is " + Tilt(root));
}
}
```

## 蟒蛇 3

```
# Python3 Program to find Tilt of
# Binary Tree

# class that allocates a new node
# with the given data and
# None left and right pointers.
class newNode:
    def __init__(self, data):
        self.val = data
        self.left = self.right = None

# Recursive function to calculate
# Tilt of whole tree
def traverse(root, tilt):
    if (not root):
        return 0

    # Compute tilts of left and right subtrees
    # and find sums of left and right subtrees
    left = traverse(root.left, tilt)
    right = traverse(root.right, tilt)

    # Add current tilt to overall
    tilt[0] += abs(left - right)

    # Returns sum of nodes under
    # current tree
    return left + right + root.val

# Driver function to print Tilt
# of whole tree
def Tilt(root):
    tilt = [0]
    traverse(root, tilt)
    return tilt[0]

# Driver code
if __name__ == '__main__':

    # Let us construct a Binary Tree
    #     4
    # / \
    # 2 9
    # / \ \
    # 3 5 7
    root = None
    root = newNode(4)
    root.left = newNode(2)
    root.right = newNode(9)
    root.left.left = newNode(3)
    root.left.right = newNode(8)
    root.right.right = newNode(7)
    print("The Tilt of whole tree is",
                           Tilt(root))

# This code is contributed by PranchalK
```

## C#

```
// C# Program to find Tilt of Binary Tree
using System;

class GfG
{

/* A binary tree node has data, pointer to
left child and a pointer to right child */
public class Node
{
    public int val;
    public Node left, right;
}

/* Recursive function to calculate Tilt of
whole tree */
public class T
{
    public int tilt = 0;
}
static int traverse(Node root, T t )
{
    if (root == null)
        return 0;

    // Compute tilts of left and right subtrees
    // and find sums of left and right subtrees
    int left = traverse(root.left, t);
    int right = traverse(root.right, t);

    // Add current tilt to overall
    t.tilt += Math.Abs(left - right);

    // Returns sum of nodes under current tree
    return left + right + root.val;
}

/* Driver function to print Tilt of whole tree */
static int Tilt(Node root)
{
    T t = new T();
    traverse(root, t);
    return t.tilt;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void Main(String[] args)
{
    /* Let us construct a Binary Tree
        4
    / \
    2 9
    / \ \
    3 5 7 */

    Node root = null;
    root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(9);
    root.left.left = newNode(3);
    root.left.right = newNode(8);
    root.right.right = newNode(7);
    Console.WriteLine("The Tilt of whole tree is " + Tilt(root));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript Program to find Tilt of Binary Tree

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.val = data;
        }
    }

    /* Recursive function to calculate Tilt of
    whole tree */
      let tilt = 0;

    function traverse(root)
    {
        if (root == null)
            return 0;

        // Compute tilts of left and right subtrees
        // and find sums of left and right subtrees
        let left = traverse(root.left, tilt);
        let right = traverse(root.right, tilt);

        // Add current tilt to overall
        tilt += Math.abs(left - right);

        // Returns sum of nodes under current tree
        return left + right + root.val;
    }

    /* Driver function to print Tilt of whole tree */
    function Tilt(root)
    {
        traverse(root);
        return tilt;
    }

    /* Helper function that allocates a
    new node with the given data and
    NULL left and right pointers. */
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    /* Let us construct a Binary Tree
        4
    / \
    2 9
    / \ \
    3 5 7 */

    let root = null;
    root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(9);
    root.left.left = newNode(3);
    root.left.right = newNode(8);
    root.right.right = newNode(7);
    document.write("The Tilt of whole tree is " + Tilt(root));

</script>
```

**输出:**

```
The Tilt of whole tree is 15
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为二叉树中的节点数。
*   **辅助空间:** O(n)最差情况下，二叉树深度将为 n。