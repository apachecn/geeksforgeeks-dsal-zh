# 以相等的概率从树上选择一个随机节点

> 原文:[https://www . geesforgeks . org/select-random-node-tree-equal-probability/](https://www.geeksforgeeks.org/select-random-node-tree-equal-probability/)

给定一棵带有子节点的二叉树，返回一个随机节点，该节点选择树中任意节点的概率相等。
考虑根为 1 的给定树。

```
      10
    /    \
   20     30
  / \      / \
40   50   60   70
```

**例:**

```
Input : getRandom(root);
Output : A Random Node From Tree : 3

Input : getRandom(root);
Output : A Random Node From Tree : 2
```

一个简单的解决方案是将树的有序遍历存储在一个数组中。假设节点数为 n，为了得到一个随机节点，我们生成一个从 0 到 n-1 的随机数，用这个数作为数组中的索引，并返回索引处的值。
一个**替代方案**是修改树形结构。我们在每个节点中存储子节点的数量。考虑上面的树。我们在这里也使用有序遍历。我们生成一个小于或等于节点数的数。我们遍历树并到达索引处的节点。我们使用计数来快速到达所需的节点。通过计数，我们在 0(h)时间内到达，其中 h 是树的高度。

```
      10,6
    /      \
  20,2       30,2
 /   \       /   \
40,0 50,0  60,0  70,0
The first value is node and second
value is count of children.
```

我们开始遍历树，在每个节点上，我们要么去左子树，要么去右子树，考虑子节点的数量是否小于随机数量。
如果随机计数小于儿童计数，那么我们向左走，否则我们向右走。
以下是上述算法的实现。getElements 将返回根的子节点计数，InsertChildrenCount 将子节点数据插入到每个节点，RandomNode 在实用函数 RandomNodeUtil 的帮助下返回随机节点。

## C++

```
// CPP program to Select a Random Node from a tree
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    int children;
    Node *left, *right;
};

Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    temp->children = 0;
    return temp;
}

// This is used to fill children counts.
int getElements(Node* root)
{
    if (!root)
        return 0;
    return getElements(root->left) +
          getElements(root->right) + 1;
}

// Inserts Children count for each node
void insertChildrenCount(Node*& root)
{
    if (!root)
        return;

    root->children = getElements(root) - 1;
    insertChildrenCount(root->left);
    insertChildrenCount(root->right);
}

// returns number of children for root
int children(Node* root)
{
    if (!root)
        return 0;
    return root->children + 1;
}

// Helper Function to return a random node
int randomNodeUtil(Node* root, int count)
{
    if (!root)
        return 0;

    if (count == children(root->left))
        return root->data;

    if (count < children(root->left))
        return randomNodeUtil(root->left, count);

    return randomNodeUtil(root->right,
              count - children(root->left) - 1);
}

// Returns Random node
int randomNode(Node* root)
{
    srand(time(0));

    int count = rand() % (root->children + 1);
    return randomNodeUtil(root, count);
}

int main()
{
    // Creating Above Tree
    Node* root = newNode(10);
    root->left = newNode(20);
    root->right = newNode(30);
    root->left->right = newNode(40);
    root->left->right = newNode(50);
    root->right->left = newNode(60);
    root->right->right = newNode(70);

    insertChildrenCount(root);

    cout << "A Random Node From Tree : "
         << randomNode(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Select a Random Node from a tree
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
static class Node
{
    int data;
    int children;
    Node left, right;
}

static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    temp.children = 0;
    return temp;
}

// This is used to fill children counts.
static int getElements(Node root)
{
    if (root == null)
        return 0;
    return getElements(root.left) +
        getElements(root.right) + 1;
}

// Inserts Children count for each node
static Node insertChildrenCount(Node root)
{
    if (root == null)
        return null;

    root.children = getElements(root) - 1;
    root.left = insertChildrenCount(root.left);
    root.right = insertChildrenCount(root.right);
    return root;
}

// returns number of children for root
static int children(Node root)
{
    if (root == null)
        return 0;
    return root.children + 1;
}

// Helper Function to return a random node
static int randomNodeUtil(Node root, int count)
{
    if (root == null)
        return 0;

    if (count == children(root.left))
        return root.data;

    if (count < children(root.left))
        return randomNodeUtil(root.left, count);

    return randomNodeUtil(root.right,
         count - children(root.left) - 1);
}

// Returns Random node
static int randomNode(Node root)
{

    int count = (int) Math.random() *
                     (root.children + 1);
    return randomNodeUtil(root, count);
}

// Driver Code
public static void main(String args[])
{

    // Creating Above Tree
    Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.right = newNode(40);
    root.left.right = newNode(50);
    root.right.left = newNode(60);
    root.right.right = newNode(70);

    insertChildrenCount(root);

    System.out.println( "A Random Node From Tree : " +
                                    randomNode(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to Select a
# Random Node from a tree
from random import randint

class Node:

    def __init__(self, data):
        self.data = data
        self.children = 0
        self.left = None
        self.right = None

# This is used to fill children counts.
def getElements(root):

    if root == None:
        return 0

    return (getElements(root.left) +
            getElements(root.right) + 1)

# Inserts Children count for each node
def insertChildrenCount(root):

    if root == None:
        return

    root.children = getElements(root) - 1
    insertChildrenCount(root.left)
    insertChildrenCount(root.right)

# Returns number of children for root
def children(root):

    if root == None:
        return 0
    return root.children + 1

# Helper Function to return a random node
def randomNodeUtil(root, count):

    if root == None:
        return 0

    if count == children(root.left):
        return root.data

    if count < children(root.left):
        return randomNodeUtil(root.left, count)

    return randomNodeUtil(root.right,
            count - children(root.left) - 1)

# Returns Random node
def randomNode(root):

    count = randint(0, root.children)
    return randomNodeUtil(root, count)

# Driver Code
if __name__ == "__main__":

    # Creating Above Tree
    root = Node(10)
    root.left = Node(20)
    root.right = Node(30)
    root.left.right = Node(40)
    root.left.right = Node(50)
    root.right.left = Node(60)
    root.right.right = Node(70)

    insertChildrenCount(root)

    print("A Random Node From Tree :",
           randomNode(root))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to Select a Random Node from a tree
using System;

class GFG
{

class Node
{
    public int data;
    public int children;
    public Node left, right;
}

static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    temp.children = 0;
    return temp;
}

// This is used to fill children counts.
static int getElements(Node root)
{
    if (root == null)
        return 0;
    return getElements(root.left) +
        getElements(root.right) + 1;
}

// Inserts Children count for each node
static Node insertChildrenCount(Node root)
{
    if (root == null)
        return null;

    root.children = getElements(root) - 1;
    root.left = insertChildrenCount(root.left);
    root.right = insertChildrenCount(root.right);
    return root;
}

// returns number of children for root
static int children(Node root)
{
    if (root == null)
        return 0;
    return root.children + 1;
}

// Helper Function to return a random node
static int randomNodeUtil(Node root, int count)
{
    if (root == null)
        return 0;

    if (count == children(root.left))
        return root.data;

    if (count < children(root.left))
        return randomNodeUtil(root.left, count);

    return randomNodeUtil(root.right,
        count - children(root.left) - 1);
}

// Returns Random node
static int randomNode(Node root)
{

    int count = (int) new Random().Next(0, root.children + 1);
    return randomNodeUtil(root, count);
}

// Driver Code
public static void Main(String []args)
{

    // Creating Above Tree
    Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.right = newNode(40);
    root.left.right = newNode(50);
    root.right.left = newNode(60);
    root.right.right = newNode(70);

    insertChildrenCount(root);

    Console.Write( "A Random Node From Tree : " +
                                    randomNode(root));
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to Select a Random Node from a tree

class Node
{
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
        this.children = 0;
    }
}

// This is used to fill children counts.
function getElements(root)
{
    if (root == null)
        return 0;
    return getElements(root.left) +
        getElements(root.right) + 1;
}

// Inserts Children count for each node
function insertChildrenCount(root)
{
    if (root == null)
        return null;

    root.children = getElements(root) - 1;
    root.left = insertChildrenCount(root.left);
    root.right = insertChildrenCount(root.right);
    return root;
}

// returns number of children for root
function children(root)
{
    if (root == null)
        return 0;
    return root.children + 1;
}

// Helper Function to return a random node
function randomNodeUtil(root,count)
{
    if (root == null)
        return 0;

    if (count == children(root.left))
        return root.data;

    if (count < children(root.left))
        return randomNodeUtil(root.left, count);

    return randomNodeUtil(root.right,
         count - children(root.left) - 1);
}

// Returns Random node
function randomNode(root)
{
    let count =  Math.floor(Math.random() *
                     (root.children + 1));
    return randomNodeUtil(root, count);
}

// Driver Code
// Creating Above Tree
let root = new Node(10);
root.left = new Node(20);
root.right = new Node(30);
root.left.right = new Node(40);
root.left.right = new Node(50);
root.right.left = new Node(60);
root.right.right = new Node(70);

insertChildrenCount(root);

document.write( "A Random Node From Tree : " +
                   randomNode(root)+"<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

随机节点的时间复杂度是 O(h)，其中 h 是树的高度。请注意，我们一次不是向右就是向左移动。