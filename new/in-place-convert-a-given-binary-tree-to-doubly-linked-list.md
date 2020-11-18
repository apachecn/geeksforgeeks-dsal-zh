# 将给定的二叉树转换为双链表 | 系列 1

> 原文：[https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)

给定一个二叉树（Bt），将其转换为双链表（DLL）。 节点中的左指针和右指针分别用作转换后的 DLL 中的上一个指针和下一个指针。 DLL 中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT 中最左边的节点）必须是 DLL 的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

我在一次采访中遇到了这次采访。 这篇文章中讨论了类似的问题。 这里的问题比较简单，因为我们不需要创建循环 DLL，而是创建一个简单的 DLL。 解决方案背后的想法非常简单直接。

**1\.** 如果存在左子树，则处理左子树

….. **1.a）**将左子树递归转换为 DLL。

….. **1.b）**然后在左子树中找到根的有序先行者（有序前任是左子树中的最右节点）。

….. **1.c）**将有序前任作为 root 的前任，并将 root 用作有序前任的 next。

**2\.** 如果存在右子树，请处理右子树（以下 3 个步骤类似于左子树）。

….. **2.a）**将正确的子树递归转换为 DLL。

….. **2.b）**然后在右子树中找到根的有序继任者（有序继任者是右子树中最左边的节点）。

….. **2.c）**将有序继承者作为根的下一个，并将根作为有序继承者的前一个。

**3\.** 找到最左边的节点并将其返回（最左边的节点始终是转换后的 DLL 的头）。

以下是上述算法的源代码。

## C++

```cpp

// A C++ program for in-place  
// conversion of Binary Tree to DLL  
#include <bits/stdc++.h> 
using namespace std; 

/* A binary tree node has data,  
and left and right pointers */
class node  
{  
    public: 
    int data;  
    node* left;  
    node* right;  
};  

/* This is the core function to convert  
Tree to list. This function follows  
steps 1 and 2 of the above algorithm */
node* bintree2listUtil(node* root)  
{  
    // Base case  
    if (root == NULL)  
        return root;  

    // Convert the left subtree and link to root  
    if (root->left != NULL)  
    {  
        // Convert the left subtree  
        node* left = bintree2listUtil(root->left);  

        // Find inorder predecessor. After this loop, left  
        // will point to the inorder predecessor  
        for (; left->right != NULL; left = left->right);  

        // Make root as next of the predecessor  
        left->right = root;  

        // Make predecssor as previous of root  
        root->left = left;  
    }  

    // Convert the right subtree and link to root  
    if (root->right != NULL)  
    {  
        // Convert the right subtree  
        node* right = bintree2listUtil(root->right);  

        // Find inorder successor. After this loop, right  
        // will point to the inorder successor  
        for (; right->left != NULL; right = right->left);  

        // Make root as previous of successor  
        right->left = root;  

        // Make successor as next of root  
        root->right = right;  
    }  

    return root;  
}  

// The main function that first calls  
// bintree2listUtil(), then follows step 3  
// of the above algorithm  
node* bintree2list(node *root)  
{  
    // Base case  
    if (root == NULL)  
        return root;  

    // Convert to DLL using bintree2listUtil()  
    root = bintree2listUtil(root);  

    // bintree2listUtil() returns root node of the converted  
    // DLL. We need pointer to the leftmost node which is  
    // head of the constructed DLL, so move to the leftmost node  
    while (root->left != NULL)  
        root = root->left;  

    return (root);  
}  

/* Helper function that allocates a new node with the  
given data and NULL left and right pointers. */
node* newNode(int data)  
{  
    node* new_node = new node();  
    new_node->data = data;  
    new_node->left = new_node->right = NULL;  
    return (new_node);  
}  

/* Function to print nodes in a given doubly linked list */
void printList(node *node)  
{  
    while (node != NULL)  
    {  
        cout << node->data << " ";  
        node = node->right;  
    }  
}  

/* Driver code*/
int main()  
{  
    // Let us create the tree shown in above diagram  
    node *root = newNode(10);  
    root->left = newNode(12);  
    root->right = newNode(15);  
    root->left->left = newNode(25);  
    root->left->right = newNode(30);  
    root->right->left = newNode(36);  

    // Convert to DLL  
    node *head = bintree2list(root);  

    // Print the converted list  
    printList(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// A C program for in-place conversion of Binary Tree to DLL 
#include <stdio.h> 

/* A binary tree node has data, and left and right pointers */
struct node 
{ 
    int data; 
    node* left; 
    node* right; 
}; 

/* This is the core function to convert Tree to list. This function follows 
  steps 1 and 2 of the above algorithm */
node* bintree2listUtil(node* root) 
{ 
    // Base case 
    if (root == NULL) 
        return root; 

    // Convert the left subtree and link to root 
    if (root->left != NULL) 
    { 
        // Convert the left subtree 
        node* left = bintree2listUtil(root->left); 

        // Find inorder predecessor. After this loop, left 
        // will point to the inorder predecessor 
        for (; left->right!=NULL; left=left->right); 

        // Make root as next of the predecessor 
        left->right = root; 

        // Make predecssor as previous of root 
        root->left = left; 
    } 

    // Convert the right subtree and link to root 
    if (root->right!=NULL) 
    { 
        // Convert the right subtree 
        node* right = bintree2listUtil(root->right); 

        // Find inorder successor. After this loop, right 
        // will point to the inorder successor 
        for (; right->left!=NULL; right = right->left); 

        // Make root as previous of successor 
        right->left = root; 

        // Make successor as next of root 
        root->right = right; 
    } 

    return root; 
} 

// The main function that first calls bintree2listUtil(), then follows step 3  
//  of the above algorithm 
node* bintree2list(node *root) 
{ 
    // Base case 
    if (root == NULL) 
        return root; 

    // Convert to DLL using bintree2listUtil() 
    root = bintree2listUtil(root); 

    // bintree2listUtil() returns root node of the converted 
    // DLL.  We need pointer to the leftmost node which is 
    // head of the constructed DLL, so move to the leftmost node 
    while (root->left != NULL) 
        root = root->left; 

    return (root); 
} 

/* Helper function that allocates a new node with the 
   given data and NULL left and right pointers. */
node* newNode(int data) 
{ 
    node* new_node = new node; 
    new_node->data = data; 
    new_node->left = new_node->right = NULL; 
    return (new_node); 
} 

/* Function to print nodes in a given doubly linked list */
void printList(node *node) 
{ 
    while (node!=NULL) 
    { 
        printf("%d ", node->data); 
        node = node->right; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    // Let us create the tree shown in above diagram 
    node *root        = newNode(10); 
    root->left        = newNode(12); 
    root->right       = newNode(15); 
    root->left->left  = newNode(25); 
    root->left->right = newNode(30); 
    root->right->left = newNode(36); 

    // Convert to DLL 
    node *head = bintree2list(root); 

    // Print the converted list 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to convert binary tree to double linked list 

/* A binary tree node has data, and left and right pointers */
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
    /* This is the core function to convert Tree to list. This function 
       follows steps 1 and 2 of the above algorithm */

    Node bintree2listUtil(Node node)  
    { 
        // Base case 
        if (node == null) 
            return node; 

        // Convert the left subtree and link to root 
        if (node.left != null)  
        { 
            // Convert the left subtree 
            Node left = bintree2listUtil(node.left); 

            // Find inorder predecessor. After this loop, left 
            // will point to the inorder predecessor 
            for (; left.right != null; left = left.right); 

            // Make root as next of the predecessor 
            left.right = node; 

            // Make predecssor as previous of root 
            node.left = left; 
        } 

        // Convert the right subtree and link to root 
        if (node.right != null)  
        { 
            // Convert the right subtree 
            Node right = bintree2listUtil(node.right); 

            // Find inorder successor. After this loop, right 
            // will point to the inorder successor 
            for (; right.left != null; right = right.left); 

            // Make root as previous of successor 
            right.left = node; 

            // Make successor as next of root 
            node.right = right; 
        } 

        return node; 
    } 

    // The main function that first calls bintree2listUtil(), then follows 
    // step 3 of the above algorithm 

    Node bintree2list(Node node)  
    { 
        // Base case 
        if (node == null) 
            return node; 

        // Convert to DLL using bintree2listUtil() 
        node = bintree2listUtil(node); 

        // bintree2listUtil() returns root node of the converted 
        // DLL.  We need pointer to the leftmost node which is 
        // head of the constructed DLL, so move to the leftmost node 
        while (node.left != null) 
            node = node.left; 

        return node; 
    } 

    /* Function to print nodes in a given doubly linked list */
    void printList(Node node)  
    { 
        while (node != null)  
        { 
            System.out.print(node.data + " "); 
            node = node.right; 
        } 
    } 

    /* Driver program to test above functions*/
    public static void main(String[] args)  
    { 
        BinaryTree tree = new BinaryTree(); 

        // Let us create the tree shown in above diagram 
        tree.root = new Node(10); 
        tree.root.left = new Node(12); 
        tree.root.right = new Node(15); 
        tree.root.left.left = new Node(25); 
        tree.root.left.right = new Node(30); 
        tree.root.right.left = new Node(36); 

        // Convert to DLL 
        Node head = tree.bintree2list(tree.root); 

        // Print the converted list 
        tree.printList(head); 
    } 
} 

```

## Python

```py

# Python program to convert  
# binary tree to doubly linked list 

class Node(object): 

    """Binary tree Node class has  
    data, left and right child"""
    def __init__(self, item): 
        self.data = item 
        self.left = None
        self.right = None

def BTToDLLUtil(root): 

    """This is a utility function to  
    convert the binary tree to doubly  
    linked list. Most of the core task 
    is done by this function."""
    if root is None: 
        return root 

    # Convert left subtree  
    # and link to root 
    if root.left: 

        # Convert the left subtree 
        left = BTToDLLUtil(root.left) 

        # Find inorder predecessor, After  
        # this loop, left will point to the  
        # inorder predecessor of root 
        while left.right: 
            left = left.right 

        # Make root as next of predecessor 
        left.right = root 

        # Make predecessor as  
        # previous of root 
        root.left = left 

    # Convert the right subtree 
    # and link to root 
    if root.right: 

        # Convert the right subtree 
        right = BTToDLLUtil(root.right) 

        # Find inorder successor, After  
        # this loop, right will point to  
        # the inorder successor of root 
        while right.left: 
            right = right.left 

        # Make root as previous  
        # of successor 
        right.left = root 

        # Make successor as  
        # next of root 
        root.right = right 

    return root 

def BTToDLL(root): 
    if root is None: 
        return root 

    # Convert to doubly linked  
    # list using BLLToDLLUtil 
    root = BTToDLLUtil(root) 

    # We need pointer to left most  
    # node which is head of the  
    # constructed Doubly Linked list 
    while root.left: 
        root = root.left 

    return root 

def print_list(head): 

    """Function to print the given 
       doubly linked list"""
    if head is None: 
        return
    while head: 
        print(head.data, end = " ") 
        head = head.right 

# Driver Code 
if __name__ == '__main__': 
    root = Node(10) 
    root.left = Node(12) 
    root.right = Node(15) 
    root.left.left = Node(25) 
    root.left.right = Node(30) 
    root.right.left = Node(36) 

    head = BTToDLL(root) 
    print_list(head) 

# This code is contributed  
# by viveksyngh 

```

## C#

```cs

using System; 

// C# program to convert binary tree to double linked list  

/* A binary tree node has data, and left and right pointers */
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
    /* This is the core function to convert Tree to list. This function  
       follows steps 1 and 2 of the above algorithm */

    public virtual Node bintree2listUtil(Node node) 
    { 
        // Base case  
        if (node == null) 
        { 
            return node; 
        } 

        // Convert the left subtree and link to root  
        if (node.left != null) 
        { 
            // Convert the left subtree  
            Node left = bintree2listUtil(node.left); 

            // Find inorder predecessor. After this loop, left  
            // will point to the inorder predecessor  
            for (; left.right != null; left = left.right) 
            { 
                ; 
            } 

            // Make root as next of the predecessor  
            left.right = node; 

            // Make predecssor as previous of root  
            node.left = left; 
        } 

        // Convert the right subtree and link to root  
        if (node.right != null) 
        { 
            // Convert the right subtree  
            Node right = bintree2listUtil(node.right); 

            // Find inorder successor. After this loop, right  
            // will point to the inorder successor  
            for (; right.left != null; right = right.left) 
            { 
                ; 
            } 

            // Make root as previous of successor  
            right.left = node; 

            // Make successor as next of root  
            node.right = right; 
        } 

        return node; 
    } 

    // The main function that first calls bintree2listUtil(), then follows  
    // step 3 of the above algorithm  

    public virtual Node bintree2list(Node node) 
    { 
        // Base case  
        if (node == null) 
        { 
            return node; 
        } 

        // Convert to DLL using bintree2listUtil()  
        node = bintree2listUtil(node); 

        // bintree2listUtil() returns root node of the converted  
        // DLL.  We need pointer to the leftmost node which is  
        // head of the constructed DLL, so move to the leftmost node  
        while (node.left != null) 
        { 
            node = node.left; 
        } 

        return node; 
    } 

    /* Function to print nodes in a given doubly linked list */
    public virtual void printList(Node node) 
    { 
        while (node != null) 
        { 
            Console.Write(node.data + " "); 
            node = node.right; 
        } 
    } 

    /* Driver program to test above functions*/
    public static void Main(string[] args) 
    { 
        BinaryTree tree = new BinaryTree(); 

        // Let us create the tree shown in above diagram  
        tree.root = new Node(10); 
        tree.root.left = new Node(12); 
        tree.root.right = new Node(15); 
        tree.root.left.left = new Node(25); 
        tree.root.left.right = new Node(30); 
        tree.root.right.left = new Node(36); 

        // Convert to DLL  
        Node head = tree.bintree2list(tree.root); 

        // Print the converted list  
        tree.printList(head); 
    } 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
25 12 30 10 36 15
```

本文由 **Ashish Mangla** 编写，并由 GeeksforGeeks 团队审阅。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

您可能还希望看到[将给定的二叉树转换为双链表 | 系列 2](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-doubly-linked-list-set-2/) 为另一个简单有效的解决方案。

