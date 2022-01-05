# 给定一棵二叉树，如何去掉所有的半节点？

> 原文:[https://www . geesforgeks . org/given-a-二叉树-如何移除所有的半节点/](https://www.geeksforgeeks.org/given-a-binary-tree-how-do-you-remove-all-the-half-nodes/)

给定一棵二叉树，如何移除所有的半节点(只有一个子节点)？请注意，不能触摸树叶，因为它们的两个子代都为空。
例如，考虑下面的树。

![tree1](img/ae2af2a037bc95a8e26f7645a87a1dbc.png)

节点 2 和 4 是半节点，因为它们的一个子节点为空。

其思想是使用后序遍历来有效地解决这个问题。我们首先处理左边的子节点，然后是右边的子节点，最后是节点本身。所以我们自下而上形成新的树，从叶子开始，一直到根部。当我们处理当前节点时，它的左右子树都已经被处理了。下面是这个想法的实现。

## C

```
// C program to remove all half nodes
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node* left, *right;
};

struct node* newNode(int data)
{
    struct node* node = (struct node*)
                        malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

void printInoder(struct node*root)
{
    if (root != NULL)
    {
        printInoder(root->left);
        printf("%d ",root->data);
        printInoder(root->right);
    }
}

// Removes all nodes with only one child and returns
// new root (note that root may change)
struct node* RemoveHalfNodes(struct node* root)
{
    if (root==NULL)
        return NULL;

    root->left  = RemoveHalfNodes(root->left);
    root->right = RemoveHalfNodes(root->right);

    if (root->left==NULL && root->right==NULL)
        return root;

    /* if current nodes is a half node with left
       child NULL left, then it's right child is
       returned and replaces it in the given tree */
    if (root->left==NULL)
    {
        struct node *new_root = root->right;
        free(root); // To avoid memory leak
        return new_root;
    }

    /* if current nodes is a half node with right
       child NULL right, then it's right child is
       returned and replaces it in the given tree  */
    if (root->right==NULL)
    {
        struct node *new_root = root->left;
        free(root); // To avoid memory leak
        return new_root;
    }

    return root;
}

// Driver program
int main(void)
{
    struct node*NewRoot=NULL;
    struct node *root = newNode(2);
    root->left        = newNode(7);
    root->right       = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left=newNode(1);
    root->left->right->right=newNode(11);
    root->right->right=newNode(9);
    root->right->right->left=newNode(4);

    printf("Inorder traversal of given tree \n");
    printInoder(root);

    NewRoot = RemoveHalfNodes(root);

    printf("\nInorder traversal of the modified tree \n");
    printInoder(NewRoot);
    return 0;
}
```

## C++

```
// C++ program to remove all half nodes
#include <bits/stdc++.h>
using namespace std;

struct node
{
    int data;
    struct node* left, *right;
};

struct node* newNode(int data)
{
    node* nod = new node();
    nod->data = data;
    nod->left = nod->right = NULL;
    return(nod);
}

void printInoder(struct node*root)
{
    if (root != NULL)
    {
        printInoder(root->left);
        cout<< root->data << " ";
        printInoder(root->right);
    }
}

// Removes all nodes with only one child and returns
// new root (note that root may change)
struct node* RemoveHalfNodes(struct node* root)
{
    if (root==NULL)
        return NULL;

    root->left  = RemoveHalfNodes(root->left);
    root->right = RemoveHalfNodes(root->right);

    if (root->left==NULL && root->right==NULL)
        return root;

    /* if current nodes is a half node with left
       child NULL left, then it's right child is
       returned and replaces it in the given tree */
    if (root->left==NULL)
    {
        struct node *new_root = root->right;
        free(root); // To avoid memory leak
        return new_root;
    }

    /* if current nodes is a half node with right
       child NULL right, then it's right child is
       returned and replaces it in the given tree  */
    if (root->right==NULL)
    {
        struct node *new_root = root->left;
        free(root); // To avoid memory leak
        return new_root;
    }

    return root;
}

// Driver program
int main(void)
{
    struct node*NewRoot=NULL;
    struct node *root = newNode(2);
    root->left        = newNode(7);
    root->right       = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left=newNode(1);
    root->left->right->right=newNode(11);
    root->right->right=newNode(9);
    root->right->right->left=newNode(4);

    cout<<"Inorder traversal of given tree \n";
    printInoder(root);

    NewRoot = RemoveHalfNodes(root);

    cout<<"\nInorder traversal of the modified tree \n";
    printInoder(NewRoot);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove half nodes
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    void printInorder(Node node)
    {
        if (node != null)
        {
            printInorder(node.left);
            System.out.print(node.data + " ");
            printInorder(node.right);
        }
    }

    // Removes all nodes with only one child and returns
    // new root (note that root may change)
    Node RemoveHalfNodes(Node node)
    {
        if (node == null)
            return null;

        node.left = RemoveHalfNodes(node.left);
        node.right = RemoveHalfNodes(node.right);

        if (node.left == null && node.right == null)
            return node;

        /* if current nodes is a half node with left
         child NULL left, then it's right child is
         returned and replaces it in the given tree */
        if (node.left == null)
        {
            Node new_root = node.right;
            return new_root;
        }

        /* if current nodes is a half node with right
           child NULL right, then it's right child is
           returned and replaces it in the given tree  */
        if (node.right == null)
        {
            Node new_root = node.left;
            return new_root;
        }

        return node;
    }

    // Driver program
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        Node NewRoot = null;
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);

        System.out.println("the inorder traversal of tree is ");
        tree.printInorder(tree.root);

        NewRoot = tree.RemoveHalfNodes(tree.root);

        System.out.print("\nInorder traversal of the modified tree \n");
        tree.printInorder(NewRoot);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to remove all half nodes

# A binary tree node
class Node:
    # Constructor for creating a new node
    def __init__(self , data):
        self.data = data
        self.left = None
        self.right = None

# For inorder traversal
def printInorder(root):
    if root is not None:
        printInorder(root.left)
        print root.data,
        printInorder(root.right)

# Removes all nodes with only one child and returns
# new root(note that root may change)
def RemoveHalfNodes(root):
    if root is None:
        return None

    # Recur to left tree
    root.left = RemoveHalfNodes(root.left)

    # Recur to right tree
    root.right = RemoveHalfNodes(root.right)

    # if both left and right child is None
    # the node is not a Half node
    if root.left is None and root.right is None:
        return root

    # If current nodes is a half node with left child
    # None then it's right child is returned and  
    # replaces it in the given tree
    if root.left is None:
        new_root = root.right
        temp = root
        root = None
        del(temp)
        return new_root

    if root.right is None:
        new_root = root.left
        temp = root
        root = None
        del(temp)
        return new_root

    return root

# Driver Program
root = Node(2)
root.left = Node(7)
root.right = Node(5)
root.left.right = Node(6)
root.left.right.left = Node(1)
root.left.right.right = Node(11)
root.right.right = Node(9)
root.right.right.left = Node(4)

print "Inorder traversal of given tree"
printInorder(root)

NewRoot = RemoveHalfNodes(root)

print "\nInorder traversal of the modified tree"
printInorder(NewRoot)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to remove half nodes
public class Node
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
    public Node root;

    public virtual void printInorder(Node node)
    {
        if (node != null)
        {
            printInorder(node.left);
            Console.Write(node.data + " ");
            printInorder(node.right);
        }
    }

    // Removes all nodes with only one child and returns
    // new root (note that root may change)
    public virtual Node RemoveHalfNodes(Node node)
    {
        if (node == null)
        {
            return null;
        }

        node.left = RemoveHalfNodes(node.left);
        node.right = RemoveHalfNodes(node.right);

        if (node.left == null && node.right == null)
        {
            return node;
        }

        /* if current nodes is a half node with left
         child NULL left, then it's right child is
         returned and replaces it in the given tree */
        if (node.left == null)
        {
            Node new_root = node.right;
            return new_root;
        }

        /* if current nodes is a half node with right
           child NULL right, then it's right child is
           returned and replaces it in the given tree  */
        if (node.right == null)
        {
            Node new_root = node.left;
            return new_root;
        }

        return node;
    }

    // Driver program
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        Node NewRoot = null;
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);

        Console.WriteLine("the inorder traversal of tree is ");
        tree.printInorder(tree.root);

        NewRoot = tree.RemoveHalfNodes(tree.root);

        Console.Write("\nInorder traversal of the modified tree \n");
        tree.printInorder(NewRoot);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
Java
<script>
// javascript program to remove half nodes
class Node {
    constructor(item) {
        this.data = item;
        this.left = this.right = null;
    }
}

    var root;

    function printInorder( node) {
        if (node != null) {
            printInorder(node.left);
            document.write(node.data + " ");
            printInorder(node.right);
        }
    }

    // Removes all nodes with only one child and returns
    // new root (note that root may change)
    function RemoveHalfNodes( node) {
        if (node == null)
            return null;

        node.left = RemoveHalfNodes(node.left);
        node.right = RemoveHalfNodes(node.right);

        if (node.left == null && node.right == null)
            return node;

        /*
         * if current nodes is a half node with left child NULL left, then it's right
         * child is returned and replaces it in the given tree
         */
        if (node.left == null) {
             new_root = node.right;
            return new_root;
        }

        /*
         * if current nodes is a half node with right child NULL right, then it's right
         * child is returned and replaces it in the given tree
         */
        if (node.right == null) {
             new_root = node.left;
            return new_root;
        }

        return node;
    }

    // Driver program

         NewRoot = null;
        root = new Node(2);
        root.left = new Node(7);
        root.right = new Node(5);
        root.left.right = new Node(6);
        root.left.right.left = new Node(1);
        root.left.right.right = new Node(11);
        root.right.right = new Node(9);
        root.right.right.left = new Node(4);

        document.write("the inorder traversal of tree is <br/>");
        printInorder(root);

        NewRoot = RemoveHalfNodes(root);

        document.write("<br/>Inorder traversal of the modified tree <br/>");
        printInorder(NewRoot);

// This code contributed by gauravrajput1
</script>
script
```

**输出:**

```
Inorder traversal of given tree
7 1 6 11 2 5 4 9
Inorder traversal of the modified tree
1 6 11 2 4
```

上述解决方案的时间复杂度是 O(n)，因为它对二叉树进行了简单的遍历。

本文由 **Jyoti Saini** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息