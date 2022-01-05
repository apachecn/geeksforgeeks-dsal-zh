# 树遍历(顺序、前序和后序)

> 原文:[https://www . geeksforgeeks . org/tree-traversals-in order-preorder-and-post order/](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

与线性数据结构(数组、链表、队列、堆栈等)只有一种逻辑方式遍历不同，树可以用不同的方式遍历。以下是遍历树的常用方法。

![Example Tree](img/34a0f18bcfea93de93a6282740c0a4b6.png)

深度优先遍历:
(a)顺序(左、根、右):4 2 5 1 3
(b)顺序前(根、左、右):1 2 4 5 3
(c)顺序后(左、右、根):4 5 2 3 1
宽度优先或级别顺序遍历:1 2 3 4 5
宽度优先遍历请参见[本](https://www.geeksforgeeks.org/level-order-tree-traversal/)帖子。

**有序穿越(** [**练习**](https://practice.geeksforgeeks.org/problems/inorder-traversal/1) **):**

```
Algorithm Inorder(tree)
   1\. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2\. Visit the root.
   3\. Traverse the right subtree, i.e., call Inorder(right-subtree)
```

在二分搜索法树的情况下，有序遍历以非递减的顺序给出节点。为了以非递增的顺序获得 BST 的节点，可以使用一种有序遍历的变体，其中有序遍历是反向的。
示例:按照遍历顺序，上面给出的图是 4 2 5 1 3。

**前序遍历(** [**练习**](https://practice.geeksforgeeks.org/problems/preorder-traversal/1) **):**

```
Algorithm Preorder(tree)
   1\. Visit the root.
   2\. Traverse the left subtree, i.e., call Preorder(left-subtree)
   3\. Traverse the right subtree, i.e., call Preorder(right-subtree) 
```

使用 Preorder
Preorder 遍历用于创建树的副本。前序遍历也用于获取表达式树上的前缀表达式。请看[http://en.wikipedia.org/wiki/Polish_notation](http://en.wikipedia.org/wiki/Polish_notation)知道前缀表达为什么有用。
示例:上面给出的图的 Preorder 遍历是 1 2 4 5 3。

**后序遍历(** [**练习**](https://practice.geeksforgeeks.org/problems/postorder-traversal/1) **):**

```
Algorithm Postorder(tree)
   1\. Traverse the left subtree, i.e., call Postorder(left-subtree)
   2\. Traverse the right subtree, i.e., call Postorder(right-subtree)
   3\. Visit the root.
```

后序的使用
后序遍历用于删除树。详见[关于删除一棵树的问题](https://www.geeksforgeeks.org/write-a-c-program-to-delete-a-tree/)。后序遍历对于获取表达式树的后缀表达式也很有用。后缀表达式的用法见[http://en.wikipedia.org/wiki/Reverse_Polish_notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation)。

示例:上面给出的图的后置遍历是 4 5 2 3 1。

## C++

```
// C++ program for different tree traversals
#include <iostream>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node *left, *right;
};

//Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

/* Given a binary tree, print its nodes according to the
"bottom-up" postorder traversal. */
void printPostorder(struct Node* node)
{
    if (node == NULL)
        return;

    // first recur on left subtree
    printPostorder(node->left);

    // then recur on right subtree
    printPostorder(node->right);

    // now deal with the node
    cout << node->data << " ";
}

/* Given a binary tree, print its nodes in inorder*/
void printInorder(struct Node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    cout << node->data << " ";

    /* now recur on right child */
    printInorder(node->right);
}

/* Given a binary tree, print its nodes in preorder*/
void printPreorder(struct Node* node)
{
    if (node == NULL)
        return;

    /* first print data of node */
    cout << node->data << " ";

    /* then recur on left subtree */
    printPreorder(node->left);

    /* now recur on right subtree */
    printPreorder(node->right);
}

/* Driver program to test above functions*/
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    cout << "\nPreorder traversal of binary tree is \n";
    printPreorder(root);

    cout << "\nInorder traversal of binary tree is \n";
    printInorder(root);

    cout << "\nPostorder traversal of binary tree is \n";
    printPostorder(root);

    return 0;
}
```

## C

```
// C program for different tree traversals
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node
        = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

/* Given a binary tree, print its nodes according to the
  "bottom-up" postorder traversal. */
void printPostorder(struct node* node)
{
    if (node == NULL)
        return;

    // first recur on left subtree
    printPostorder(node->left);

    // then recur on right subtree
    printPostorder(node->right);

    // now deal with the node
    printf("%d ", node->data);
}

/* Given a binary tree, print its nodes in inorder*/
void printInorder(struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    printInorder(node->right);
}

/* Given a binary tree, print its nodes in preorder*/
void printPreorder(struct node* node)
{
    if (node == NULL)
        return;

    /* first print data of node */
    printf("%d ", node->data);

    /* then recur on left subtree */
    printPreorder(node->left);

    /* now recur on right subtree */
    printPreorder(node->right);
}

/* Driver program to test above functions*/
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    printf("\nPreorder traversal of binary tree is \n");
    printPreorder(root);

    printf("\nInorder traversal of binary tree is \n");
    printInorder(root);

    printf("\nPostorder traversal of binary tree is \n");
    printPostorder(root);

    getchar();
    return 0;
}
```

## 计算机编程语言

```
# Python program to for tree traversals

# A class that represents an individual node in a
# Binary Tree

class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key

# A function to do inorder tree traversal
def printInorder(root):

    if root:

        # First recur on left child
        printInorder(root.left)

        # then print the data of node
        print(root.val),

        # now recur on right child
        printInorder(root.right)

# A function to do postorder tree traversal
def printPostorder(root):

    if root:

        # First recur on left child
        printPostorder(root.left)

        # the recur on right child
        printPostorder(root.right)

        # now print the data of node
        print(root.val),

# A function to do preorder tree traversal
def printPreorder(root):

    if root:

        # First print the data of node
        print(root.val),

        # Then recur on left child
        printPreorder(root.left)

        # Finally recur on right child
        printPreorder(root.right)

# Driver code
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
print "Preorder traversal of binary tree is"
printPreorder(root)

print "\nInorder traversal of binary tree is"
printInorder(root)

print "\nPostorder traversal of binary tree is"
printPostorder(root)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for different tree traversals

/* Class containing left and right child of current
   node and key value*/
class Node {
    int key;
    Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

class BinaryTree {
    // Root of Binary Tree
    Node root;

    BinaryTree() { root = null; }

    /* Given a binary tree, print its nodes according to the
      "bottom-up" postorder traversal. */
    void printPostorder(Node node)
    {
        if (node == null)
            return;

        // first recur on left subtree
        printPostorder(node.left);

        // then recur on right subtree
        printPostorder(node.right);

        // now deal with the node
        System.out.print(node.key + " ");
    }

    /* Given a binary tree, print its nodes in inorder*/
    void printInorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        System.out.print(node.key + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    /* Given a binary tree, print its nodes in preorder*/
    void printPreorder(Node node)
    {
        if (node == null)
            return;

        /* first print data of node */
        System.out.print(node.key + " ");

        /* then recur on left subtree */
        printPreorder(node.left);

        /* now recur on right subtree */
        printPreorder(node.right);
    }

    // Wrappers over above recursive functions
    void printPostorder() { printPostorder(root); }
    void printInorder() { printInorder(root); }
    void printPreorder() { printPreorder(root); }

    // Driver method
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println(
            "Preorder traversal of binary tree is ");
        tree.printPreorder();

        System.out.println(
            "\nInorder traversal of binary tree is ");
        tree.printInorder();

        System.out.println(
            "\nPostorder traversal of binary tree is ");
        tree.printPostorder();
    }
}
```

## C#

```
// C# program for different
// tree traversals
using System;

/* Class containing left and
right child of current
node and key value*/
class Node {
    public int key;
    public Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

class BinaryTree {
    // Root of Binary Tree
    Node root;

    BinaryTree() { root = null; }

    /* Given a binary tree, print
       its nodes according to the
       "bottom-up" postorder traversal. */
    void printPostorder(Node node)
    {
        if (node == null)
            return;

        // first recur on left subtree
        printPostorder(node.left);

        // then recur on right subtree
        printPostorder(node.right);

        // now deal with the node
        Console.Write(node.key + " ");
    }

    /* Given a binary tree, print
       its nodes in inorder*/
    void printInorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        Console.Write(node.key + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    /* Given a binary tree, print
       its nodes in preorder*/
    void printPreorder(Node node)
    {
        if (node == null)
            return;

        /* first print data of node */
        Console.Write(node.key + " ");

        /* then recur on left subtree */
        printPreorder(node.left);

        /* now recur on right subtree */
        printPreorder(node.right);
    }

    // Wrappers over above recursive functions
    void printPostorder() { printPostorder(root); }
    void printInorder() { printInorder(root); }
    void printPreorder() { printPreorder(root); }

    // Driver Code
    static public void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        Console.WriteLine("Preorder traversal "
                          + "of binary tree is ");
        tree.printPreorder();

        Console.WriteLine("\nInorder traversal "
                          + "of binary tree is ");
        tree.printInorder();

        Console.WriteLine("\nPostorder traversal "
                          + "of binary tree is ");
        tree.printPostorder();
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// javascript program for different tree traversals

/* Class containing left and right child of current
   node and key value*/
class Node {
    constructor(val) {
        this.key = val;
        this.left = null;
        this.right = null;
    }
}

    // Root of Binary Tree
    var root = null;

    /*
     * Given a binary tree, print its nodes according to the "bottom-up" postorder
     * traversal.
     */
    function printPostorder(node) {
        if (node == null)
            return;

        // first recur on left subtree
        printPostorder(node.left);

        // then recur on right subtree
        printPostorder(node.right);

        // now deal with the node
        document.write(node.key + " ");
    }

    /* Given a binary tree, print its nodes in inorder */
    function printInorder(node) {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        document.write(node.key + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    /* Given a binary tree, print its nodes in preorder */
    function printPreorder(node) {
        if (node == null)
            return;

        /* first print data of node */
        document.write(node.key + " ");

        /* then recur on left subtree */
        printPreorder(node.left);

        /* now recur on right subtree */
        printPreorder(node.right);

    }

    // Driver method

        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);

        document.write("Preorder traversal of binary tree is <br/>");
        printPreorder(root);

        document.write("<br/>Inorder traversal of binary tree is <br/>");
        printInorder(root);

        document.write("<br/>Postorder traversal of binary tree is <br/>");
        printPostorder(root);

// This code is contributed by aashish1995
</script>
```

**输出:**

```
Preorder traversal of binary tree is
1 2 4 5 3 
Inorder traversal of binary tree is
4 2 5 1 3 
Postorder traversal of binary tree is
4 5 2 3 1
```

**再举一个例子:**

![](img/e507f18fefa0539dbba04aa7212cb01c.png)

**时间复杂度:** O(n)
让我们看看不同的角例。
复杂度函数 T(n)——对于所有涉及树遍历的问题——可以定义为:
T(n)= T(k)+T(n–k–1)+c
其中 k 是根的一侧的节点数，n-k-1 是另一侧的节点数。
我们来分析一下边界条件
情况 1:斜树(其中一个子树为空，另一个子树为非空)
这种情况下 k 为 0。
T(n)= T(0)+T(n-1)+c
T(n)= 2T(0)+T(n-2)+2c
T(n)= 3T(0)+T(n-3)+3c
T(n)= 4T(0)+T(n-4)+4c
…………………………………………………………………………………………………………………………………………………………
T(n)=(n-1)T(0)+T(1)+(n-1)c
T(n)= nT(0)+(n)c
T(0)的值将是某个常数比如 d(遍历一棵空树将花费一些常数时间)
T(n)= n(c+d)
T(n)=θ(n)(θof n)
情况 2:左右子树的节点数相等。
T(n) = 2T(|_n/2_|) + c
这个递归函数是主方法[http://en.wikipedia.org/wiki/Master_theorem](http://en.wikipedia.org/wiki/Master_theorem)的标准形式(T(n) = aT(n/b) + (-)(n))。如果用主方法求解，我们得到(-)(n)

**辅助空间:**如果我们不考虑函数调用的堆栈大小，那么 O(1)否则 O(h)其中 h 是树的高度。

偏斜树的高度为 n(元素数量)，因此最差的空间复杂度为 O(n)，平衡树的高度为(Log n)，因此最佳空间复杂度为 O(Log n)。