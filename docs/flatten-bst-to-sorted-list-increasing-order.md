# 将 BST 展平至排序列表|递增顺序

> 原文:[https://www . geesforgeks . org/flat-BST-to-sorted-list-递增-order/](https://www.geeksforgeeks.org/flatten-bst-to-sorted-list-increasing-order/)

给定一个二叉查找树，任务是将其展平为一个排序列表。准确地说，每个节点的值必须小于其右侧所有节点的值，并且其左侧节点在展平后必须为空。我们必须在 O(H)的额外空间中完成，其中“H”是 BST 的高度。

**示例:**

```
Input: 
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
Output: 2 3 4 5 6 7 8
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
Output: 1 2 3 4 5
```

**方法:**一个简单的方法是从其[有序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历中重新创建 BST。这将占用 O(N)个额外空间，其中 N 是 BST 中的节点数。

为了改进这一点，我们将如下模拟二叉树的有序遍历:

1.  创建一个虚拟节点。
2.  创建一个名为“prev”的变量，并使其指向虚拟节点。
3.  执行有序遍历并在每一步。
    *   设置前->右=当前
    *   设置前一->左=空
    *   预测集= curr

这将在最坏的情况下将空间复杂度提高到 0(H)，因为有序遍历需要 0(H)个额外空间。

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

// Function to print flattened
// binary Tree
void print(node* parent)
{
    node* curr = parent;
    while (curr != NULL)
        cout << curr->data << " ", curr = curr->right;
}

// Function to perform in-order traversal
// recursively
void inorder(node* curr, node*& prev)
{
    // Base case
    if (curr == NULL)
        return;
    inorder(curr->left, prev);
    prev->left = NULL;
    prev->right = curr;
    prev = curr;
    inorder(curr->right, prev);
}

// Function to flatten binary tree using
// level order traversal
node* flatten(node* parent)
{
    // Dummy node
    node* dummy = new node(-1);

    // Pointer to previous element
    node* prev = dummy;

    // Calling in-order traversal
    inorder(parent, prev);

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

    // Calling required function
    print(flatten(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG{

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

// Function to print flattened
// binary tree
static void print(node parent)
{
  node curr = parent;
  while (curr != null)
  {
    System.out.print(curr.data + " ");
    curr = curr.right;
  }
}

static  node prev;

// Function to perform
// in-order traversal
static void Inorder(node curr)
{
  // Base case
  if (curr == null)
    return;
  Inorder(curr.left);
  prev.left = null;
  prev.right = curr;
  prev = curr;
  Inorder(curr.right);
}

// Function to flatten binary
// tree using level order
// traversal
static node flatten(node parent)
{
  // Dummy node
  node dummy = new node(-1);

  // Pointer to previous
  // element
  prev = dummy;

  // Calling in-order
  // traversal
  Inorder(parent);

  prev.left = null;
  prev.right = null;
  node ret = dummy.right;

  // Delete dummy node
  //delete dummy;
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

  // Calling required function
  print(flatten(root));
}
}

// This code is contributed by Debojyoti Mandal
```

## C#

```
// C# implementation of the
// above approach
using System;
public class Program{

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

// Function to print flattened
// binary tree
static void print(node parent)
{
  node curr = parent;
  while (curr != null)
  {
    Console.Write(curr.data + " ");
    curr = curr.right;
  }
}

static  node prev;

// Function to perform
// in-order traversal
static void Inorder(node curr)
{
  // Base case
  if (curr == null)
    return;
  Inorder(curr.left);
  prev.left = null;
  prev.right = curr;
  prev = curr;
  Inorder(curr.right);
}

// Function to flatten binary
// tree using level order
// traversal
static node flatten(node parent)
{
  // Dummy node
  node dummy = new node(-1);

  // Pointer to previous
  // element
  prev = dummy;

  // Calling in-order
  // traversal
  Inorder(parent);

  prev.left = null;
  prev.right = null;
  node ret = dummy.right;

  // Delete dummy node
  //delete dummy;
  return ret;
}

// Driver code
public static void Main(string[] args)
{
  node root = new node(5);
  root.left = new node(3);
  root.right = new node(7);
  root.left.left = new node(2);
  root.left.right = new node(4);
  root.right.left = new node(6);
  root.right.right = new node(8);

  // Calling required function
  print(flatten(root));
}
}

// This code is contributed by rrrtnx.
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
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

let prev;

// Function to print flattened
// binary Tree
function print(parent)
{
    let curr = parent;
    while (curr != null)
    {
        document.write(curr.data + " ");
        curr = curr.right;
    }
}

// Function to perform in-order traversal
// recursively
function inorder(curr)
{

    // Base case
    if (curr == null)
        return;

    inorder(curr.left);
    prev.left = null;
    prev.right = curr;
    prev = curr;
    inorder(curr.right);
}

// Function to flatten binary tree using
// level order traversal
function flatten(parent)
{

    // Dummy node
    let dummy = new node(-1);

    // Pointer to previous element
    prev = dummy;

    // Calling in-order traversal
    inorder(parent);

    prev.left = null;
    prev.right = null;
    let ret = dummy.right;

    // Delete dummy node
    return ret;
}

// Driver code
let root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

// Calling required function
print(flatten(root));

// This code is contributed by divyeshrabadiya07

</script>
```

## 蟒蛇 3

```
# Python3 implementation of the approach

global prev
# Node of the binary tree
class node :
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print flattened
# binary Tree
def printTree(parent):
    curr = parent
    while (curr != None):
        print(curr.data,end=' ')
        curr = curr.right

# Function to perform in-order traversal
# recursively
def inorder(curr):
    global prev
    # Base case
    if (curr == None):
        return
    inorder(curr.left)
    prev.left = None
    prev.right = curr
    prev = curr
    inorder(curr.right)

# Function to flatten binary tree using
# level order traversal
def flatten(parent):
    global prev
    # Dummy node
    dummy = node(-1)

    # Pointer to previous element
    prev = dummy

    # Calling in-order traversal
    inorder(parent)

    prev.left = None
    prev.right = None
    ret = dummy.right

    # Delete dummy node
    return ret

# Driver code
if __name__ == '__main__':
    root = node(5)
    root.left = node(3)
    root.right = node(7)
    root.left.left = node(2)
    root.left.right = node(4)
    root.right.left = node(6)
    root.right.right = node(8)

    # Calling required function
    printTree(flatten(root))
```

**Output:** 

```
2 3 4 5 6 7 8
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)