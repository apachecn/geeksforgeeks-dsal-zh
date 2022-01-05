# 二叉树中节点的后置后继

> 原文:[https://www . geesforgeks . org/post order-后继-节点-二叉树/](https://www.geeksforgeeks.org/postorder-successor-node-binary-tree/)

给定一棵二叉树和二叉树中的一个节点，找到给定节点的后置后继节点。

```
Examples: Consider the following binary tree
              20            
           /      \         
          10       26       
         /  \     /   \     
       4     18  24    27   
            /  \
           14   19
          /  \
         13  15

Postorder traversal of given tree is 4, 13, 15, 14,
19, 18, 10, 24, 27, 26, 20.

Input :  24
Output : 27

Input : 4
Output : 13
```

一个**简单的解决方案**是首先将给定树的后序遍历存储在一个数组中，然后线性搜索给定节点并打印它旁边的节点。
时间复杂度:O(n)
辅助空间:O(n)
一个**高效解**基于以下观察。

1.  如果给定的节点是根，则后序后继节点为空，因为根是后序遍历中的最后一个节点
2.  如果给定节点是父节点的右子节点，或者父节点的右子节点为空，则父节点是后序后继节点。
3.  如果给定节点是父节点的左子节点，而父节点的右子节点不为空，则后序后继节点是父节点右子树的最左侧节点

## C++

```
// CPP program to find postorder successor of
// given node.
#include <iostream>
using namespace std;

struct Node {
    struct Node *left, *right, *parent;
    int value;
};

// Utility function to create a new node with
// given value.
struct Node* newNode(int value)
{
    Node* temp = new Node;
    temp->left = temp->right = temp->parent = NULL;
    temp->value = value;
    return temp;
}

Node* postorderSuccessor(Node* root, Node* n)
{
    // Root has no successor in postorder
    // traversal
    if (n == root)
        return NULL;

    // If given node is right child of its
    // parent or parent's right is empty, then
    // parent is postorder successor.
    Node* parent = n->parent;
    if (parent->right == NULL || parent->right == n)
        return parent;

    // In all other cases, find the leftmost
    // child in right substree of parent.
    Node* curr = parent->right;
    while (curr->left != NULL)
        curr = curr->left;

    return curr;
}

// Driver code
int main()
{
    struct Node* root = newNode(20);
    root->parent = NULL;
    root->left = newNode(10);
    root->left->parent = root;
    root->left->left = newNode(4);
    root->left->left->parent = root->left;
    root->left->right = newNode(18);
    root->left->right->parent = root->left;
    root->right = newNode(26);
    root->right->parent = root;
    root->right->left = newNode(24);
    root->right->left->parent = root->right;
    root->right->right = newNode(27);
    root->right->right->parent = root->right;
    root->left->right->left = newNode(14);
    root->left->right->left->parent = root->left->right;
    root->left->right->left->left = newNode(13);
    root->left->right->left->left->parent = root->left->right->left;
    root->left->right->left->right = newNode(15);
    root->left->right->left->right->parent = root->left->right->left;
    root->left->right->right = newNode(19);
    root->left->right->right->parent = root->left->right;

    struct Node* res = postorderSuccessor(root, root->left->right->right);
    if (res)
        printf("Postorder successor of %d is %d\n",
               root->left->right->right->value, res->value);   
    else
        printf("Postorder successor of %d is NULL\n",
               root->left->right->right->value);   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find postorder successor of
// given node.
import java.util.*;
class GfG {

static class Node {
    Node left, right, parent;
    int value;
}

// Utility function to create a new node with
// given value.
static Node newNode(int value)
{
    Node temp = new Node();
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    temp.value = value;
    return temp;
}

static Node postorderSuccessor(Node root, Node n)
{
    // Root has no successor in postorder
    // traversal
    if (n == root)
        return null;

    // If given node is right child of its
    // parent or parent's right is empty, then
    // parent is postorder successor.
    Node parent = n.parent;
    if (parent.right == null || parent.right == n)
        return parent;

    // In all other cases, find the leftmost
    // child in right substree of parent.
    Node curr = parent.right;
    while (curr.left != null)
        curr = curr.left;

    return curr;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(20);
    root.parent = null;
    root.left = newNode(10);
    root.left.parent = root;
    root.left.left = newNode(4);
    root.left.left.parent = root.left;
    root.left.right = newNode(18);
    root.left.right.parent = root.left;
    root.right = newNode(26);
    root.right.parent = root;
    root.right.left = newNode(24);
    root.right.left.parent = root.right;
    root.right.right = newNode(27);
    root.right.right.parent = root.right;
    root.left.right.left = newNode(14);
    root.left.right.left.parent = root.left.right;
    root.left.right.left.left = newNode(13);
    root.left.right.left.left.parent = root.left.right.left;
    root.left.right.left.right = newNode(15);
    root.left.right.left.right.parent = root.left.right.left;
    root.left.right.right = newNode(19);
    root.left.right.right.parent = root.left.right;

    Node res = postorderSuccessor(root, root.left.right.right);
    if (res != null)
        System.out.println("Postorder successor of "+
        root.left.right.right.value + " is "+ res.value);
    else
        System.out.println("Postorder successor of " +
        root.left.right.right.value + " is NULL");
}
}
```

## 蟒蛇 3

```
""" Python3 program to find postorder
successor of a node in Binary Tree."""

# A Binary Tree Node
# Utility function to create a new tree node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.value = data
        self.left = None
        self.right = None
        self.parent=None

def postorderSuccessor(root, n) :

    # Root has no successor in postorder
    # traversal
    if (n == root):
        return None

    # If given node is right child of its
    # parent or parent's right is empty,
    # then parent is postorder successor.
    parent = n.parent
    if (parent.right == None or parent.right == n):
        return parent

    # In all other cases, find the leftmost
    # child in right substree of parent.
    curr = parent.right
    while (curr.left != None):
        curr = curr.left

    return curr

# Driver Code
if __name__ == '__main__':
    root = newNode(20)
    root.parent = None
    root.left = newNode(10)
    root.left.parent = root
    root.left.left = newNode(4)
    root.left.left.parent = root.left
    root.left.right = newNode(18)
    root.left.right.parent = root.left
    root.right = newNode(26)
    root.right.parent = root
    root.right.left = newNode(24)
    root.right.left.parent = root.right
    root.right.right = newNode(27)
    root.right.right.parent = root.right
    root.left.right.left = newNode(14)
    root.left.right.left.parent = root.left.right
    root.left.right.left.left = newNode(13)
    root.left.right.left.left.parent = root.left.right.left
    root.left.right.left.right = newNode(15)
    root.left.right.left.right.parent = root.left.right.left
    root.left.right.right = newNode(19)
    root.left.right.right.parent = root.left.right
    res = postorderSuccessor(root, root.left.right.right)

    if (res) :
        print("postorder successor of",
               root.left.right.right.value,
               "is", res.value)

    else:
        print("postorder successor of",
               root.left.right.right.value,
                                 "is None")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find postorder successor of
// given node.
using System;

class GfG
{

class Node
{
    public Node left, right, parent;
    public int value;
}

// Utility function to create 
// a new node with given value.
static Node newNode(int value)
{
    Node temp = new Node();
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    temp.value = value;
    return temp;
}

static Node postorderSuccessor(Node root, Node n)
{
    // Root has no successor in 
    // postorder traversal
    if (n == root)
        return null;

    // If given node is right child of its
    // parent or parent's right is empty, then
    // parent is postorder successor.
    Node parent = n.parent;
    if (parent.right == null || parent.right == n)
        return parent;

    // In all other cases, find the leftmost
    // child in right substree of parent.
    Node curr = parent.right;
    while (curr.left != null)
        curr = curr.left;

    return curr;
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(20);
    root.parent = null;
    root.left = newNode(10);
    root.left.parent = root;
    root.left.left = newNode(4);
    root.left.left.parent = root.left;
    root.left.right = newNode(18);
    root.left.right.parent = root.left;
    root.right = newNode(26);
    root.right.parent = root;
    root.right.left = newNode(24);
    root.right.left.parent = root.right;
    root.right.right = newNode(27);
    root.right.right.parent = root.right;
    root.left.right.left = newNode(14);
    root.left.right.left.parent = root.left.right;
    root.left.right.left.left = newNode(13);
    root.left.right.left.left.parent = root.left.right.left;
    root.left.right.left.right = newNode(15);
    root.left.right.left.right.parent = root.left.right.left;
    root.left.right.right = newNode(19);
    root.left.right.right.parent = root.left.right;

    Node res = postorderSuccessor(root, root.left.right.right);
    if (res != null)
        Console.WriteLine("Postorder successor of "+
        root.left.right.right.value + " is "+ res.value);
    else
        Console.WriteLine("Postorder successor of " +
        root.left.right.right.value + " is NULL");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to find postorder successor of
// given node.

class Node
{
    constructor()
    {
        this.value = 0;
        this.left = null;
        this.right = null;
        this.parent = null;
    }
}

// Utility function to create 
// a new node with given value.
function newNode(value)
{
    var temp = new Node();
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    temp.value = value;
    return temp;
}

function postorderSuccessor(root, n)
{
    // Root has no successor in 
    // postorder traversal
    if (n == root)
        return null;

    // If given node is right child of its
    // parent or parent's right is empty, then
    // parent is postorder successor.
    var parent = n.parent;
    if (parent.right == null || parent.right == n)
        return parent;

    // In all other cases, find the leftmost
    // child in right substree of parent.
    var curr = parent.right;
    while (curr.left != null)
        curr = curr.left;

    return curr;
}

// Driver code
var root = newNode(20);
root.parent = null;
root.left = newNode(10);
root.left.parent = root;
root.left.left = newNode(4);
root.left.left.parent = root.left;
root.left.right = newNode(18);
root.left.right.parent = root.left;
root.right = newNode(26);
root.right.parent = root;
root.right.left = newNode(24);
root.right.left.parent = root.right;
root.right.right = newNode(27);
root.right.right.parent = root.right;
root.left.right.left = newNode(14);
root.left.right.left.parent = root.left.right;
root.left.right.left.left = newNode(13);
root.left.right.left.left.parent = root.left.right.left;
root.left.right.left.right = newNode(15);
root.left.right.left.right.parent = root.left.right.left;
root.left.right.right = newNode(19);
root.left.right.right.parent = root.left.right;
var res = postorderSuccessor(root, root.left.right.right);
if (res != null)
    document.write("Postorder successor of "+
    root.left.right.right.value + " is "+ res.value);
else
    document.write("Postorder successor of " +
    root.left.right.right.value + " is NULL");

// This code is contributed by famously.

</script>
```

**Output:** 

```
Postorder successor of 19 is 18
```

**时间复杂度:** O(h)其中 h 是给定二叉树的高度
**辅助空间:** O(1)因为没有使用数组、栈、队列。