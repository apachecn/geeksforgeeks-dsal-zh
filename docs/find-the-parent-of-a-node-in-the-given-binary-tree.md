# 在给定的二叉树中找到一个节点的父节点

> 原文:[https://www . geesforgeks . org/find-给定二叉树中节点的父节点/](https://www.geeksforgeeks.org/find-the-parent-of-a-node-in-the-given-binary-tree/)

给定一棵树和一个节点，任务是在树中找到给定节点的父节点。如果给定节点是根节点，则打印-1。
**例:**

```
Input: Node = 3
     1
   /   \
  2     3
 / \
4   5
Output: 1

Input: Node = 1
     1
   /   \
  2     3
 /       \
4         5
         /
        6
Output: -1
```

**方法:**编写一个递归函数，以当前节点及其父节点为参数(根节点以-1 作为其父节点传递)。如果当前节点等于所需节点，则打印其父节点并返回，否则为其子节点递归调用该函数，并将当前节点作为父节点。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

/* A binary tree node has data, pointer
to left child and a pointer
to right child */
struct Node {
    int data;
    struct Node *left, *right;
    Node(int data)
    {
        this->data = data;
        left = right = NULL;
    }
};

// Recursive function to find the
// parent of the given node
void findParent(struct Node* node,
                int val, int parent)
{
    if (node == NULL)
        return;

    // If current node is the required node
    if (node->data == val) {

        // Print its parent
        cout << parent;
    }
    else {

        // Recursive calls for the children
        // of the current node
        // Current node is now the new parent
        findParent(node->left, val, node->data);
        findParent(node->right, val, node->data);
    }
}

// Driver code
int main()
{
    struct Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    int node = 3;

    findParent(root, node, -1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

/* A binary tree node has data, pointer
to left child and a pointer
to right child */
static class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        this.data = data;
        left = right = null;
    }
};

// Recursive function to find the
// parent of the given node
static void findParent(Node node,
                       int val, int parent)
{
    if (node == null)
        return;

    // If current node is the required node
    if (node.data == val)
    {

        // Print its parent
        System.out.print(parent);
    }
    else
    {

        // Recursive calls for the children
        // of the current node
        // Current node is now the new parent
        findParent(node.left, val, node.data);
        findParent(node.right, val, node.data);
    }
}

// Driver code
public static void main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    int node = 3;

    findParent(root, node, -1);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

''' A binary tree node has data, pointer
to left child and a pointer
to right child '''
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Recursive function to find the
# parent of the given node
def findParent(node : Node,
               val : int,
               parent : int) -> None:
    if (node is None):
        return

    # If current node is
    # the required node
    if (node.data == val):

        # Print its parent
        print(parent)
    else:

        # Recursive calls
        # for the children
        # of the current node
        # Current node is now
        # the new parent
        findParent(node.left,
                   val, node.data)
        findParent(node.right,
                   val, node.data)

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    node = 3
    findParent(root, node, -1)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

/* A binary tree node has data, pointer
to left child and a pointer
to right child */
public class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
};

// Recursive function to find the
// parent of the given node
static void findParent(Node node,
                         int val, int parent)
{
    if (node == null)
        return;

    // If current node is the required node
    if (node.data == val)
    {

        // Print its parent
        Console.Write(parent);
    }
    else
    {

        // Recursive calls for the children
        // of the current node
        // Current node is now the new parent
        findParent(node.left, val, node.data);
        findParent(node.right, val, node.data);
    }
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    int node = 3;

    findParent(root, node, -1);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

/* A binary tree node has data, pointer
to left child and a pointer
to right child */
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Recursive function to find the
// parent of the given node
function findParent(node, val, parent)
{
    if (node == null)
        return;

    // If current node is the required node
    if (node.data == val)
    {

        // Print its parent
        document.write(parent);
    }
    else
    {

        // Recursive calls for the children
        // of the current node
        // Current node is now the new parent
        findParent(node.left, val, node.data);
        findParent(node.right, val, node.data);
    }
}

// Driver code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
var node = 3;

findParent(root, node, -1);

</script>
```

**Output:** 

```
1
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。