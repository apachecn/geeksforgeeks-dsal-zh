# BST 中大于或等于 N 的最小数

> 原文:[https://www . geesforgeks . org/BST 中最小的大于或等于 n 的数字/](https://www.geeksforgeeks.org/smallest-number-in-bst-which-is-greater-than-or-equal-to-n/)

给定一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)和一个数字 N，任务是找到二叉查找树中大于或等于 N 的最小数字。如果元素存在，则打印该元素的值，否则打印-1。

**示例:**

> 输入:N = 20
> 输出:21
> 说明:21 是大于 20 的最小元素。
> 
> 输入:N = 18
> 输出:19
> 说明:19 是大于 18 的最小元素。

**方法:**
思路是按照递归的方法求解问题，即从根开始搜索元素。

*   如果有一个叶节点的值小于 N，则元素不存在，并返回-1。
*   否则，如果节点的值大于或等于 N，并且左子节点为空或小于 N，则返回节点值。
*   否则，如果节点的值小于 N，则在右子树中搜索该元素。
*   否则，通过根据左或右值递归调用函数，在左子树中搜索元素。

## C++

```
// C++ program to find the smallest value
// greater than or equal to N
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
};

// To create new BST Node
Node* createNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;

    return temp;
}

// To add a new node in BST
Node* add(Node* node, int key)
{
    // if tree is empty return new node
    if (node == NULL)
        return createNode(key);

    // if key is less then or greater then
    // node value then recur down the tree
    if (key < node->data)
        node->left = add(node->left, key);
    else if (key > node->data)
        node->right = add(node->right, key);

    // return the (unchanged) node pointer
    return node;
}

// function to find min value less then N
int findMinforN(Node* root, int N)
{
    // If leaf node reached and is smaller than N
    if (root->left == NULL && root->right == NULL
                                && root->data < N)
        return -1;

    // If node's value is greater than N and left value
    // is NULL or smaller then return the node value
    if ((root->data >= N && root->left == NULL)
        || (root->data >= N && root->left->data < N))
        return root->data;

    // if node value is smaller than N search in the
    // right subtree
    if (root->data <= N)
        return findMinforN(root->right, N);

    // if node value is greater than N search in the
    // left subtree
    else
        return findMinforN(root->left, N);
}

// Drivers code
int main()
{
    /*    19
        /    \
       7     21
     /   \
    3     11
         /   \
         9    14
          */

    Node* root = NULL;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int N = 18;
    cout << findMinforN(root, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest value
// greater than or equal to N
import java.util.*;
class GFG
{
static class Node
{
    int data;
    Node left, right;
};

// To create new BST Node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;

    return temp;
}

// To add a new node in BST
static Node add(Node node, int key)
{
    // if tree is empty return new node
    if (node == null)
        return createNode(key);

    // if key is less then or greater then
    // node value then recur down the tree
    if (key < node.data)
        node.left = add(node.left, key);
    else if (key > node.data)
        node.right = add(node.right, key);

    // return the (unchanged) node pointer
    return node;
}

// function to find min value less then N
static int findMinforN(Node root, int N)
{
    // If leaf node reached and is smaller than N
    if (root.left == null &&
        root.right == null && root.data < N)
        return -1;

    // If node's value is greater than N and left value
    // is null or smaller then return the node value
    if ((root.data >= N && root.left == null) ||
        (root.data >= N && root.left.data < N))
        return root.data;

    // if node value is smaller than N search in the
    // right subtree
    if (root.data <= N)
        return findMinforN(root.right, N);

    // if node value is greater than N search in the
    // left subtree
    else
        return findMinforN(root.left, N);
}

// Driver Code
public static void main(String[] args)
{
    /* 19
        / \
    7     21
    / \
    3     11
        / \
        9 14
        */

    Node root = null;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int N = 18;
    System.out.println(findMinforN(root, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find the smallest value
# greater than or equal to N

class Node:
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# To create new BST Node
def createNode(item: int):
    temp = Node()
    temp.data = item
    temp.left = temp.right = None
    return temp

# To add a new node in BST
def add(node: Node, key: int):

    # if tree is empty return new node
    if node is None:
        return createNode(key)

    # if key is less then or greater then
    # node value then recur down the tree
    if key < node.data:
        node.left = add(node.left, key)
    elif key > node.data:
        node.right = add(node.right, key)

    # return the (unchanged) node pointer
    return node

# function to find min value less then N
def findMinforN(root: Node, N: int):

    # If leaf node reached and is smaller than N
    if root.left is None and root.right is None and root.data < N:
        return -1

    # If node's value is greater than N and left value
    # is NULL or smaller then return the node value
    if root.data >= N and root.left is None or root.data >= N and root.left.data < N:
        return root.data

    # if node value is smaller than N search in the
    # right subtree
    if root.data <= N:
        return findMinforN(root.right, N)

    # if node value is greater than N search in the
    # left subtree
    else:
        return findMinforN(root.left, N)

# Driver Code
if __name__ == "__main__":

    '''
            19
        / \
        7     21
        / \
    3 11
        / \
        9 14
    '''
    root = Node()
    root = add(root, 19)
    root = add(root, 7)
    root = add(root, 3)
    root = add(root, 11)
    root = add(root, 9)
    root = add(root, 13)
    root = add(root, 21)

    N = 18
    print(findMinforN(root, N))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find the smallest value
// greater than or equal to N
using System;

class GFG
{
class Node
{
    public int data;
    public Node left, right;
};

// To create new BST Node
static Node createNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;

    return temp;
}

// To add a new node in BST
static Node add(Node node, int key)
{
    // if tree is empty return new node
    if (node == null)
        return createNode(key);

    // if key is less then or greater then
    // node value then recur down the tree
    if (key < node.data)
        node.left = add(node.left, key);
    else if (key > node.data)
        node.right = add(node.right, key);

    // return the (unchanged) node pointer
    return node;
}

// function to find min value less then N
static int findMinforN(Node root, int N)
{
    // If leaf node reached and is smaller than N
    if (root.left == null &&
        root.right == null && root.data < N)
        return -1;

    // If node's value is greater than N and left value
    // is null or smaller then return the node value
    if ((root.data >= N && root.left == null) ||
        (root.data >= N && root.left.data < N))
        return root.data;

    // if node value is smaller than N search in the
    // right subtree
    if (root.data <= N)
        return findMinforN(root.right, N);

    // if node value is greater than N search in the
    // left subtree
    else
        return findMinforN(root.left, N);
}

// Driver Code
public static void Main(String[] args)
{
    /* 19
        / \
    7     21
    / \
    3     11
        / \
        9 14
        */

    Node root = null;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int N = 18;
    Console.WriteLine(findMinforN(root, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript program to find the smallest value
// greater than or equal to N

class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// To create new BST Node
function createNode(item)
{
    var temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;

    return temp;
}

// To add a new node in BST
function add(node, key)
{
    // if tree is empty return new node
    if (node == null)
        return createNode(key);

    // if key is less then or greater then
    // node value then recur down the tree
    if (key < node.data)
        node.left = add(node.left, key);
    else if (key > node.data)
        node.right = add(node.right, key);

    // return the (unchanged) node pointer
    return node;
}

// function to find min value less then N
function findMinforN(root, N)
{
    // If leaf node reached and is smaller than N
    if (root.left == null &&
        root.right == null && root.data < N)
        return -1;

    // If node's value is greater than N and left value
    // is null or smaller then return the node value
    if ((root.data >= N && root.left == null) ||
        (root.data >= N && root.left.data < N))
        return root.data;

    // if node value is smaller than N search in the
    // right subtree
    if (root.data <= N)
        return findMinforN(root.right, N);

    // if node value is greater than N search in the
    // left subtree
    else
        return findMinforN(root.left, N);
}

// Driver Code
/* 19
    / \
7     21
/ \
3     11
    / \
    9 14
    */
var root = null;
root = add(root, 19);
root = add(root, 7);
root = add(root, 3);
root = add(root, 11);
root = add(root, 9);
root = add(root, 13);
root = add(root, 21);
var N = 18;
document.write(findMinforN(root, N));

// This code is contributed by famously.
</script>
```

**Output:** 

```
19
```