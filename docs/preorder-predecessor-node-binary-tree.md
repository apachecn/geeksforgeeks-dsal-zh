# 二叉树中节点的前序

> 原文:[https://www . geesforgeks . org/preorder-pretender-node-二叉树/](https://www.geeksforgeeks.org/preorder-predecessor-node-binary-tree/)

给定一棵二叉树和二叉树中的一个节点，找到给定节点的 Preorder Preorder。
**例:**

```
Consider the following binary tree
              20            
           /      \         
          10       26       
         /  \     /   \     
       4     18  24    27   
            /  \
           14   19
          /  \
         13  15
Input :  4
Output : 10
Preorder traversal of given tree is 20, 10, 4, 
18, 14, 13, 15, 19, 26, 24, 27.

Input :  19
Output : 15
```

一个**简单的解决方案**是首先将给定树的 Preorder 遍历存储在一个数组中，然后线性搜索给定节点并打印它旁边的节点。
时间复杂度:O(n)
辅助空间:O(n)
一个**高效解**基于以下观察。

1.  如果给定的节点是根，那么返回空值作为前序前置。
2.  如果节点是其父节点的左子节点，或者父节点的左子节点为空，则返回父节点作为其前序前置节点。
3.  如果节点是其父节点的右子节点，并且父节点的左子节点存在，则前置节点将是父节点的左子树的最右边的节点(最大值)。
4.  如果节点是其父节点的右子节点，并且父节点没有左子节点，则前置节点将是父节点(最大值)。

## C++

```
// CPP program to find preorder predecessor of
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

Node* preorderPredecessor(Node* root, Node* n)
{
    // Root has no predecessor in preorder
    // traversal
    if (n == root)
        return NULL;

    // If given node is left child of its
    // parent or parent's left is empty, then
    // parent is Preorder Predecessor.
    Node* parent = n->parent;
    if (parent->left == NULL || parent->left == n)
        return parent;

    // In all other cases, find the rightmost
    // child in left substree of parent.
    Node* curr = parent->left;
    while (curr->right != NULL)
        curr = curr->right;

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

    struct Node* res = preorderPredecessor(root, root->left->right->right);
    if (res)
        printf("Preorder predecessor of %d is %d\n",
               root->left->right->right->value, res->value);   
    else
        printf("Preorder predecessor of %d is NULL\n",
               root->left->right->right->value);   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find preorder predecessor of
// given node.
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

static Node preorderPredecessor(Node root, Node n)
{
    // Root has no predecessor in preorder
    // traversal
    if (n == root)
        return null;

    // If given node is left child of its
    // parent or parent's left is empty, then
    // parent is Preorder Predecessor.
    Node parent = n.parent;
    if (parent.left == null || parent.left == n)
        return parent;

    // In all other cases, find the rightmost
    // child in left substree of parent.
    Node curr = parent.left;
    while (curr.right != null)
        curr = curr.right;

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

    Node res = preorderPredecessor(root, root.left.right.right);
    if (res != null)
        System.out.println("Preorder predecessor of " + root.left.right.right.value + " is " + res.value);    
    else
        System.out.println("Preorder predecessor of " + root.left.right.right.value + " is null");

}
}
```

## 蟒蛇 3

```
"""Python3 program to find preorder
predecessor of given node."""

# A Binary Tree Node
# Utility function to create a new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.value = data
        self.left = None
        self.right = self.parent = None

def preorderPredecessor(root, n):

    # Root has no predecessor in preorder
    # traversal
    if (n == root) :
        return None

    # If given node is left child of its
    # parent or parent's left is empty, then
    # parent is Preorder Predecessor.
    parent = n.parent
    if (parent.left == None or
        parent.left == n):
        return parent

    # In all other cases, find the rightmost
    # child in left substree of parent.
    curr = parent.left
    while (curr.right != None) :
        curr = curr.right

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

    res = preorderPredecessor(root, root.left.right.right)
    if (res):
        print("Preorder predecessor of",
               root.left.right.right.value, "is", res.value)    
    else:
        print("Preorder predecessor of",
               root.left.right.right.value, "is None")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find preorder predecessor of
// given node.
using System;

class GfG
{

    class Node
    {
        public Node left, right, parent;
        public int value;
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

    static Node preorderPredecessor(Node root, Node n)
    {
        // Root has no predecessor in preorder
        // traversal
        if (n == root)
            return null;

        // If given node is left child of its
        // parent or parent's left is empty, then
        // parent is Preorder Predecessor.
        Node parent = n.parent;
        if (parent.left == null || parent.left == n)
            return parent;

        // In all other cases, find the rightmost
        // child in left substree of parent.
        Node curr = parent.left;
        while (curr.right != null)
            curr = curr.right;

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

        Node res = preorderPredecessor(root, root.left.right.right);
        if (res != null)
            Console.WriteLine("Preorder predecessor of " +
                               root.left.right.right.value +
                               " is " + res.value);    
        else
            Console.WriteLine("Preorder predecessor of " +
                                root.left.right.right.value +
                                " is null");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find preorder predecessor of
// given node.
class Node
{
    constructor()
    {
        this.left = null;
        this.right = null;
        this.parent = null;
        this.value = 0;
    }
}

// Utility function to create a new node with
// given value.
function newNode(value)
{
    var temp = new Node();
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    temp.value = value;
    return temp;
}

function preorderPredecessor(root, n)
{
    // Root has no predecessor in preorder
    // traversal
    if (n == root)
        return null;

    // If given node is left child of its
    // parent or parent's left is empty, then
    // parent is Preorder Predecessor.
    var parent = n.parent;
    if (parent.left == null || parent.left == n)
        return parent;

    // In all other cases, find the rightmost
    // child in left substree of parent.
    var curr = parent.left;
    while (curr.right != null)
        curr = curr.right;
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
var res = preorderPredecessor(root, root.left.right.right);
if (res != null)
    document.write("Preorder predecessor of " +
                       root.left.right.right.value +
                       " is " + res.value);    
else
    document.write("Preorder predecessor of " +
                        root.left.right.right.value +
                        " is null");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Preorder predecessor of 19 is 15
```

**时间复杂度:** O(h)其中 h 是给定二叉树的高度
**辅助空间:** O(1)因为没有使用数组、栈、队列。