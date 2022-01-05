# 检查二叉树是否是完全树|集合 2(递归求解)

> 原文:[https://www . geesforgeks . org/check-when-二叉树-complete-not-set-2-递归-solution/](https://www.geeksforgeeks.org/check-whether-binary-tree-complete-not-set-2-recursive-solution/)

完全二叉树是除了最后一层以外的所有层都被完全填充，最后一层的所有叶子都在左边的二叉树。关于完全二叉树的更多信息可以在[这里](http://courses.cs.vt.edu/%7Ecs3114/Fall09/wmcquain/Notes/T03a.BinaryTreeTheorems.pdf)找到。

例如:-
树下面是一个完整的二叉树(直到第二个最后一个节点的所有节点都被填充，所有的叶子都在左边)

![complete1](img/ef5f584cbb9229f28c6d9971eb7718ef.png)

这个问题的迭代解决方案将在下面的帖子中讨论。
[检查给定的二叉树是否完整|集合 1(使用级别顺序遍历)](https://www.geeksforgeeks.org/check-if-a-given-binary-tree-is-complete-tree-or-not/)
在这篇文章中讨论了递归解决方案。

在二叉树的数组表示中，如果给父节点分配一个“I”的索引，给左子节点分配一个“2*i + 1”的索引，而给右子节点分配一个“2*i + 2”的索引。如果我们将上面的二叉树表示为一个数组，将相应的索引从上到下、从左到右分配给树的不同节点。

因此，我们以下面的方式来检查二叉树是否是完整的二叉树。

1.  计算二叉树中的节点数(计数)。
2.  从二叉树的根节点开始递归二叉树，索引(I)设置为 0，二进制中的节点数(计数)。
3.  如果被检查的当前节点为空，则该树是一个完整的二叉树。回归真实。
4.  如果当前节点的索引(I)大于或等于二叉树中的节点数(count)，即(i>= count)，则该树不是完整的二进制。返回 false。
5.  递归检查二叉树的左右子树是否存在相同的情况。对于左边的子树，使用索引为(2*i + 1)，而对于右边的子树，使用索引为(2*i + 2)。

上述算法的时间复杂度为 O(n)。下面是检查二叉树是否是完整二叉树的代码。

## C++

```
/* C++ program to checks if a binary tree complete ot not */
#include<bits/stdc++.h>
#include<stdbool.h>
using namespace std;

/* Tree node structure */
class Node
{
    public:
    int key;
    Node *left, *right;

    Node *newNode(char k)
    {
        Node *node = ( Node*)malloc(sizeof( Node));
        node->key = k;
        node->right = node->left = NULL;
        return node;
    }

};

/* Helper function that allocates a new node with the
given key and NULL left and right pointer. */

/* This function counts the number of nodes
in a binary tree */
unsigned int countNodes(Node* root)
{
    if (root == NULL)
        return (0);
    return (1 + countNodes(root->left) +
            countNodes(root->right));
}

/* This function checks if the binary tree
is complete or not */
bool isComplete ( Node* root, unsigned int index,
                    unsigned int number_nodes)
{
    // An empty tree is complete
    if (root == NULL)
        return (true);

    // If index assigned to current node is more than
    // number of nodes in tree, then tree is not complete
    if (index >= number_nodes)
        return (false);

    // Recur for left and right subtrees
    return (isComplete(root->left, 2*index + 1, number_nodes) &&
            isComplete(root->right, 2*index + 2, number_nodes));
}

// Driver code
int main()
{
    Node n1;

    // Let us create tree in the last diagram above
    Node* root = NULL;
    root = n1.newNode(1);
    root->left = n1.newNode(2);
    root->right = n1.newNode(3);
    root->left->left = n1.newNode(4);
    root->left->right = n1.newNode(5);
    root->right->right = n1.newNode(6);

    unsigned int node_count = countNodes(root);
    unsigned int index = 0;

    if (isComplete(root, index, node_count))
        cout << "The Binary Tree is complete\n";
    else
        cout << "The Binary Tree is not complete\n";
    return (0);
}

// This code is contributed by SoumikMondal
```

## C

```
/* C program to checks if a binary tree complete ot not */
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

/*  Tree node structure */
struct Node
{
    int key;
    struct Node *left, *right;
};

/* Helper function that allocates a new node with the
   given key and NULL left and right pointer. */
struct Node *newNode(char k)
{
    struct Node *node = (struct Node*)malloc(sizeof(struct Node));
    node->key = k;
    node->right = node->left = NULL;
    return node;
}

/* This function counts the number of nodes in a binary tree */
unsigned int countNodes(struct Node* root)
{
    if (root == NULL)
        return (0);
    return (1 + countNodes(root->left) + countNodes(root->right));
}

/* This function checks if the binary tree is complete or not */
bool isComplete (struct Node* root, unsigned int index,
                 unsigned int number_nodes)
{
    // An empty tree is complete
    if (root == NULL)
        return (true);

    // If index assigned to current node is more than
    // number of nodes in tree, then tree is not complete
    if (index >= number_nodes)
        return (false);

    // Recur for left and right subtrees
    return (isComplete(root->left, 2*index + 1, number_nodes) &&
            isComplete(root->right, 2*index + 2, number_nodes));
}

// Driver program
int main()
{
    // Le us create tree in the last diagram above
    struct Node* root = NULL;
    root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(6);

    unsigned int node_count = countNodes(root);
    unsigned int index = 0;

    if (isComplete(root, index, node_count))
        printf("The Binary Tree is complete\n");
    else
        printf("The Binary Tree is not complete\n");
    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if binary tree is complete or not

/*  Tree node structure */
class Node
{
    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* This function counts the number of nodes in a binary tree */
    int countNodes(Node root)
    {
        if (root == null)
            return (0);
        return (1 + countNodes(root.left) + countNodes(root.right));
    }

    /* This function checks if the binary tree is complete or not */
    boolean isComplete(Node root, int index, int number_nodes)
    {
        // An empty tree is complete
        if (root == null)       
           return true;

        // If index assigned to current node is more than
        // number of nodes in tree, then tree is not complete
        if (index >= number_nodes)
           return false;

        // Recur for left and right subtrees
        return (isComplete(root.left, 2 * index + 1, number_nodes)
            && isComplete(root.right, 2 * index + 2, number_nodes));

    }

    // Driver program
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        // Le us create tree in the last diagram above
        Node NewRoot = null;
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.left.left = new Node(4);
        tree.root.right.right = new Node(6);

        int node_count = tree.countNodes(tree.root);
        int index = 0;

        if (tree.isComplete(tree.root, index, node_count))
            System.out.print("The binary tree is complete");
        else
            System.out.print("The binary tree is not complete");
    }
}

// This code is contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to check if a binary tree complete or not

# Tree node structure
class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# This function counts the number of nodes in a binary tree
def countNodes(root):
    if root is None:
        return 0
    return (1+ countNodes(root.left) + countNodes(root.right))

# This function checks if binary tree is complete or not
def isComplete(root, index, number_nodes):

    # An empty is complete
    if root is None:
        return True

    # If index assigned to current nodes is more than
    # number of nodes in tree, then tree is not complete
    if index >= number_nodes :
        return False

    # Recur for left and right subtress
    return (isComplete(root.left , 2*index+1 , number_nodes)
        and isComplete(root.right, 2*index+2, number_nodes)
          )

# Driver Program

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(6)

node_count = countNodes(root)
index = 0

if isComplete(root, index, node_count):
    print "The Binary Tree is complete"
else:
    print "The Binary Tree is not complete"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to check if binary
// tree is complete or not
using System;

/* Tree node structure */
class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    Node root;

    /* This function counts the number
    of nodes in a binary tree */
    int countNodes(Node root)
    {
        if (root == null)
            return (0);
        return (1 + countNodes(root.left) +
                    countNodes(root.right));
    }

    /* This function checks if the
    binary tree is complete or not */
    bool isComplete(Node root, int index,
                    int number_nodes)
    {
        // An empty tree is complete
        if (root == null)    
        return true;

        // If index assigned to current node is more than
        // number of nodes in tree, then tree is not complete
        if (index >= number_nodes)
        return false;

        // Recur for left and right subtrees
        return (isComplete(root.left, 2 * index + 1, number_nodes)
            && isComplete(root.right, 2 * index + 2, number_nodes));

    }

    // Driver code
    public static void Main()
    {
        BinaryTree tree = new BinaryTree();

        // Let us create tree in the last diagram above
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.left.left = new Node(4);
        tree.root.right.right = new Node(6);

        int node_count = tree.countNodes(tree.root);
        int index = 0;

        if (tree.isComplete(tree.root, index, node_count))
            Console.WriteLine("The binary tree is complete");
        else
            Console.WriteLine("The binary tree is not complete");
    }
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

// JavaScript program to check if
// binary tree is complete or not

/*  Tree node structure */
class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

    var root;

    /* This function counts the number of
    nodes in a binary tree */
    function countNodes(root) {
        if (root == null)
            return (0);
        return (1 + countNodes(root.left) + countNodes(root.right));
    }

    /* This function checks if the binary tree is complete or not */
    function isComplete(root , index , number_nodes) {
        // An empty tree is complete
        if (root == null)
            return true;

        // If index assigned to current node is more than
        // number of nodes in tree, then tree is not complete
        if (index >= number_nodes)
            return false;

        // Recur for left and right subtrees
        return (isComplete(root.left, 2 * index + 1, number_nodes)
            && isComplete(root.right, 2 * index + 2, number_nodes));

    }

    // Driver program

        // Le us create tree in the last diagram above
        var NewRoot = null;
        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.right = new Node(5);
        root.left.left = new Node(4);
        root.right.right = new Node(6);

        var node_count = countNodes(root);
        var index = 0;

        if (isComplete(root, index, node_count))
            document.write("The binary tree is complete");
        else
            document.write("The binary tree is not complete");

// This code contributed by umadevi9616

</script>
```

**输出:**

```
The Binary Tree is not complete 
```

本文由**高拉夫·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。