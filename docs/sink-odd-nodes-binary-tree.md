# 在二叉树中下沉奇数节点

> 原文:[https://www.geeksforgeeks.org/sink-odd-nodes-binary-tree/](https://www.geeksforgeeks.org/sink-odd-nodes-binary-tree/)

给定一个具有奇数和偶数元素的二叉树，接收它所有的奇数节点，这样没有一个具有奇数值的节点可以是具有偶数值的节点的父节点。给定的树可以有多个输出，我们需要打印其中一个。转换树总是可能的(注意，具有偶数节点和所有奇数节点的节点遵循该规则)

```
Input : 
       1
    /    \
   2      3
Output
       2            2
    /    \   OR   /   \
   1      3      3     1 

Input : 
       1
     /    \
    5       8
  /  \     /  \
 2    4   9    10
Output :
    2                 4
  /    \            /    \     
 4       8    OR   2      8    OR .. (any tree with 
/  \    /  \      /  \   / \          same keys and 
5   1  9   10    5    1 9   10        no odd is parent
                                      of even)

```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**

基本上，我们需要将节点的奇数值与其后代之一的偶数值交换。这个想法是以后置的方式遍历树。由于我们以后置顺序处理，对于遇到的每个奇数节点，它的左右子树已经平衡(下沉)，我们检查它是否是奇数节点，它的左右子树是否有一个偶数值。如果找到偶数值，我们用偶数子节点的数据交换节点的数据，并调用偶数子节点上的过程来平衡子树。如果两个子代的值都是奇数，这意味着它的所有后代都是奇数。

下面是这个想法的实现。

## C++

```
// Program to sink odd nodes to the bottom of
// binary tree
#include<bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node
{
    int data;
    Node* left, *right;
};

// Helper function to allocates a new node
Node* newnode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Helper function to check if node is leaf node
bool isLeaf(Node *root)
{
    return (root->left == NULL && root->right == NULL);
}

// A recursive method to sink a tree with odd root
// This method assumes that the subtrees are already
// sinked. This method is similar to Heapify of
// Heap-Sort
void sink(Node *&root)
{
    // If NULL or is a leaf, do nothing
    if (root == NULL || isLeaf(root))
        return;

    // if left subtree exists and left child is even
    if (root->left && !(root->left->data & 1))
    {
        // swap root's data with left child and
        // fix left subtree
        swap(root->data, root->left->data);
        sink(root->left);
    }

    // if right subtree exists and right child is even
    else if(root->right && !(root->right->data & 1))
    {
        // swap root's data with right child and
        // fix right subtree
        swap(root->data, root->right->data);
        sink(root->right);
    }
}

// Function to sink all odd nodes to the bottom of binary
// tree. It does a postorder traversal and calls sink()
// if any odd node is found
void sinkOddNodes(Node* &root)
{
    // If NULL or is a leaf, do nothing
    if (root == NULL || isLeaf(root))
        return;

    // Process left and right subtrees before this node
    sinkOddNodes(root->left);
    sinkOddNodes(root->right);

    // If root is odd, sink it
    if (root->data & 1)
        sink(root);
}

// Helper function to do Level Order Traversal of
// Binary Tree level by level. This function is used
// here only for showing modified tree.
void printLevelOrder(Node* root)
{
    queue<Node*> q;
    q.push(root);

    // Do Level order traversal
    while (!q.empty())
    {
        int nodeCount = q.size();

        // Print one level at a time
        while (nodeCount)
        {
            Node *node = q.front();
            printf("%d ", node->data);
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;
        }

        // Line separator for levels
        printf("\n");
    }
}

// Driver program to test above functions
int main()
{
    /* Constructed binary tree is
            1
          /   \
         5      8
        / \   /  \
       2   4 9   10     */

    Node *root = newnode(1);
    root->left = newnode(5);
    root->right    = newnode(8);
    root->left->left = newnode(2);
    root->left->right = newnode(4);
    root->right->left = newnode(9);
    root->right->right = newnode(10);

    sinkOddNodes(root);

    printf("Level order traversal of modified tree\n");
    printLevelOrder(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to sink odd nodes 
# to the bottom of binary tree 

# A binary tree node 
# Helper function to allocates a new node 
class newnode: 

    # Constructor to create a new node 
    def __init__(self, key): 
        self.data = key 
        self.left = None
        self.right = None

# Helper function to check 
# if node is leaf node 
def isLeaf(root):
    return (root.left == None and 
            root.right == None) 

# A recursive method to sink a tree with odd root 
# This method assumes that the subtrees are 
# already sinked. This method is similar to 
# Heapify of Heap-Sort 
def sink(root):

    # If None or is a leaf, do nothing 
    if (root == None or isLeaf(root)):
        return

    # if left subtree exists and 
    # left child is even 
    if (root.left and not(root.left.data & 1)):

        # swap root's data with left child  
        # and fix left subtree 
        root.data, \
        root.left.data = root.left.data, \
                         root.data
        sink(root.left) 

    # if right subtree exists and 
    # right child is even 
    elif(root.right and not(root.right.data & 1)):

        # swap root's data with right child 
        # and fix right subtree 
        root.data, \
        root.right.data = root.right.data, \
                          root.data
        sink(root.right) 

# Function to sink all odd nodes to 
# the bottom of binary tree. It does 
# a postorder traversal and calls sink() 
# if any odd node is found 
def sinkOddNodes(root):

    # If None or is a leaf, do nothing 
    if (root == None or isLeaf(root)):
        return

    # Process left and right subtrees 
    # before this node 
    sinkOddNodes(root.left) 
    sinkOddNodes(root.right) 

    # If root is odd, sink it 
    if (root.data & 1):
        sink(root) 

# Helper function to do Level Order Traversal 
# of Binary Tree level by level. This function 
# is used here only for showing modified tree. 
def printLevelOrder(root):
    q = []
    q.append(root) 

    # Do Level order traversal 
    while (len(q)):

        nodeCount = len(q)

        # Print one level at a time 
        while (nodeCount):
            node = q[0] 
            print(node.data, end = " ")
            q.pop(0)
            if (node.left != None):
                q.append(node.left) 
            if (node.right != None):
                q.append(node.right) 
            nodeCount -= 1

        # Line separator for levels 
        print()

# Driver Code 
""" Constructed binary tree is 
            1 
        / \ 
        5 8 
        / \ / \ 
    2 4 9 10     """
root = newnode(1) 
root.left = newnode(5) 
root.right = newnode(8) 
root.left.left = newnode(2) 
root.left.right = newnode(4) 
root.right.left = newnode(9) 
root.right.right = newnode(10) 

sinkOddNodes(root) 

print("Level order traversal of modified tree") 
printLevelOrder(root)

# This code is contributed by SHUBHAMSINGH10
```

**Output :**

```
Level order traversal of modified tree
2 
4 8 
5 1 9 10 
```

本文由**阿迪蒂亚·戈尔**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论