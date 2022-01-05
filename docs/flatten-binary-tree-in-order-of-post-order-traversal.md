# 按照后序遍历的顺序展平二叉树

> 原文:[https://www . geesforgeks . org/flat-二叉树后序遍历/](https://www.geeksforgeeks.org/flatten-binary-tree-in-order-of-post-order-traversal/)

给定一棵二叉树，任务是按照其[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)的顺序将其展平。在展平的二叉树中，所有节点的左节点必须为空。

**示例:**

```
Input: 
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
Output: 2 4 3 6 8 7 5

Input:
      1
       \
        2
         \
          3
           \
            4
             \
              5
Output: 5 4 3 2 1
```

一个简单的方法是从二叉树的 T2 后序 T3 遍历中重建二叉树。这将占用 0(N)个额外空间，N 是 BST 中的节点数。

一个**更好的解决方案**是模拟给定二叉树的后序遍历。

1.  创建一个虚拟节点。
2.  创建名为“prev”的变量，并使其指向虚拟节点。
3.  执行顺序后遍历，并在每一步。
    *   设置前->右=当前
    *   设置前一->左=空
    *   预测集= curr

这将在最坏的情况下将空间复杂度提高到 0(H)，因为后序遍历需要 0(H)个额外空间。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function to print the flattened
// binary Tree
void print(node* parent)
{
    node* curr = parent;
    while (curr != NULL)
        cout << curr->data << " ", curr = curr->right;
}

// Function to perform post-order traversal
// recursively
void postorder(node* curr, node*& prev)
{
    // Base case
    if (curr == NULL)
        return;
    postorder(curr->left, prev);
    postorder(curr->right, prev);
    prev->left = NULL;
    prev->right = curr;
    prev = curr;
}

// Function to flatten the given binary tree
// using post order traversal
node* flatten(node* parent)
{
    // Dummy node
    node* dummy = new node(-1);

    // Pointer to previous element
    node* prev = dummy;

    // Calling post-order traversal
    postorder(parent, prev);

    prev->left = NULL;
    prev->right = NULL;
    node* ret = dummy->right;

    // Delete dummy node
    delete dummy;
    return ret;
}

// Driver code
int main()
{
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    print(flatten(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Node of the binary tree
static class node
{
    int data;
    node left;
    node right;
    node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};
static node prev;

// Function to print the flattened
// binary Tree
static void print(node parent)
{
    node curr = parent;
    while (curr != null)
    {
        System.out.print(curr.data + " ");
        curr = curr.right;
    }
}

// Function to perform post-order traversal
// recursively
static void postorder(node curr)
{
    // Base case
    if (curr == null)
        return;
    postorder(curr.left);
    postorder(curr.right);
    prev.left = null;
    prev.right = curr;
    prev = curr;
}

// Function to flatten the given binary tree
// using post order traversal
static node flatten(node parent)
{
    // Dummy node
    node dummy = new node(-1);

    // Pointer to previous element
    prev = dummy;

    // Calling post-order traversal
    postorder(parent);

    prev.left = null;
    prev.right = null;
    node ret = dummy.right;

    // Delete dummy node
    dummy = null;
    return ret;
}

// Driver code
public static void main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    print(flatten(root));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of above algorithm

# Utility class to create a node
class node:
    def __init__(self, key):
        self.data = key
        self.left = self.right = None

# Function to print the flattened
# binary Tree
def print_(parent):

    curr = parent
    while (curr != None):
        print( curr.data ,end = " ")
        curr = curr.right

prev = None

# Function to perform post-order traversal
# recursively
def postorder( curr ):

    global prev

    # Base case
    if (curr == None):
        return
    postorder(curr.left)
    postorder(curr.right)
    prev.left = None
    prev.right = curr
    prev = curr

# Function to flatten the given binary tree
# using post order traversal
def flatten(parent):

    global prev

    # Dummy node
    dummy = node(-1)

    # Pointer to previous element
    prev = dummy

    # Calling post-order traversal
    postorder(parent)

    prev.left = None
    prev.right = None
    ret = dummy.right

    return ret

# Driver code
root = node(5)
root.left = node(3)
root.right = node(7)
root.left.left = node(2)
root.left.right = node(4)
root.right.left = node(6)
root.right.right = node(8)

print_(flatten(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Node of the binary tree
public class node
{
    public int data;
    public node left;
    public node right;
    public node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};
static node prev;

// Function to print the flattened
// binary Tree
static void print(node parent)
{
    node curr = parent;
    while (curr != null)
    {
        Console.Write(curr.data + " ");
        curr = curr.right;
    }
}

// Function to perform post-order traversal
// recursively
static void postorder(node curr)
{
    // Base case
    if (curr == null)
        return;
    postorder(curr.left);
    postorder(curr.right);
    prev.left = null;
    prev.right = curr;
    prev = curr;
}

// Function to flatten the given binary tree
// using post order traversal
static node flatten(node parent)
{
    // Dummy node
    node dummy = new node(-1);

    // Pointer to previous element
    prev = dummy;

    // Calling post-order traversal
    postorder(parent);

    prev.left = null;
    prev.right = null;
    node ret = dummy.right;

    // Delete dummy node
    dummy = null;
    return ret;
}

// Driver code
public static void Main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    print(flatten(root));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of the binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

var prev = null;

// Function to print the flattened
// binary Tree
function print(parent)
{
    var curr = parent;
    while (curr != null)
    {
        document.write(curr.data + " ");
        curr = curr.right;
    }
}

// Function to perform post-order traversal
// recursively
function postorder(curr)
{

    // Base case
    if (curr == null)
        return;

    postorder(curr.left);
    postorder(curr.right);
    prev.left = null;
    prev.right = curr;
    prev = curr;
}

// Function to flatten the given binary tree
// using post order traversal
function flatten(parent)
{

    // Dummy node
    var dummy = new node(-1);

    // Pointer to previous element
    prev = dummy;

    // Calling post-order traversal
    postorder(parent);

    prev.left = null;
    prev.right = null;
    var ret = dummy.right;

    // Delete dummy node
    dummy = null;
    return ret;
}

// Driver code
var root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

print(flatten(root));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
2 4 3 6 8 7 5
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)。