# 将给定的二叉树转换为双链表| 设置1

给定一个二叉树（Bt），将其转换为双链表（DLL）。 节点中的左指针和右指针分别用作转换后的DLL中的上一个指针和下一个指针。 DLL中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT中最左边的节点）必须是DLL的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

我在一次采访中遇到了这次采访。 这篇文章中讨论了类似的问题。 这里的问题比较简单，因为我们不需要创建循环DLL，而是创建一个简单的DLL。 解决方案背后的想法非常简单直接。

**1\.** 如果存在左子树，则处理左子树
….. **1.a）**将左子树递归转换为DLL。
….. **1.b）**然后在左子树中找到根的有序先行者（有序前任是左子树中的最右节点）。
….. **1.c）**将有序前任作为root的前任，并将root用作有序前任的next。
**2\.** 如果存在右子树，请处理右子树（以下3个步骤类似于左子树）。
….. **2.a）**将正确的子树递归转换为DLL。
….. **2.b）**然后在右子树中找到根的有序继任者（有序继任者是右子树中最左边的节点）。
….. **2.c）**将有序继承者作为根的下一个，并将根作为有序继承者的前一个。
**3\.** 找到最左边的节点并将其返回（最左边的节点始终是转换后的DLL的头）。

以下是上述算法的源代码。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// A C++ program for in-place ``// conversion of Binary Tree to DLL ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A binary tree node has data, ``and left and right pointers */``class` `node ``{ ` `public` `:` `int` `data; ` `node* left; ` `node* right; ``}; ``/* This is the core function to convert ``Tree to list. This function follows ``steps 1 and 2 of the above algorithm */``node* bintree2listUtil(node* root) ``{ ` `// Base case ` `if` `(root == NULL) ` `return` `root; ` `// Convert the left subtree and link to root ` `if` `(root->left != NULL) ` `{ ` `// Convert the left subtree ` `node* left = bintree2listUtil(root->left); ` ] `for` `(; left->right != NULL; left = left->right); ` `// Make root as next of the predecessor ` `left->right = root; ` `// Make predecssor as previous of root ` `root->left = left; ` `} ` `// Convert the right subtree and link to root ` `if` `(root->right != NULL) ` `{ ` `// Convert the right subtree ` `node* right = bintree2listUtil(root->right); ` `// Find inorder successor. After this loop, right ` `// will point to the inorder successor ` `for` `(; right->left != NULL; right = right->left); ` `// Make root as previous of successor ` `right->left = root; ` `// Make successor as next of root ` `root->right = right; ` `} ` `return` `root; ``} ``// The main function that first calls ``// bintree2listUtil(), then follows step 3 `] `// of the above algorithm ``node* bintree2list(node *root) ``{ ` `// Base case ` `if` `(root == NULL) ` `return` `root; ` `// Convert to DLL using bintree2listUtil() ` `root = bintree2listUtil(root); ` `// bintree2listUtil() returns root node of the converted ` `// DLL. We need pointer to the leftmost node which is ` `// head of the constructed DLL, so move to the leftmost node ` `while` `(root->left != NULL) ` `root = root->left; ` `return` `(root); ``} ``/* Helper function that allocates a new node with the ``given data and NULL left and right pointers. */``node* newNode(` `int` ] `data) ``{ ` `node* new_node =` `new` `node(); ` `new_node->data = data; ` `new_node->left = new_node->right = NULL; ` `return` `(new_node); ``} ``/* Function to print nodes in a given doubly linked list */``void` `printList(node *node) ``{ ` `while` `(node != NULL) ` `{ ` `cout << node->data <<` `" "` `; ` `node = node->right; ` `} ``} ``/* Driver code*/``int` `main() ``{ `27]  `// Let us create the tree shown in above diagram ` `node *root = newNode(10); ` `root->left = newNode(12); ` `root->right = newNode(15); ` `root->left->left = newNode(25); ` `root->left->right = newNode(30); ` `root->right->left = newNode(36); ` `// Convert to DLL ` `node *head = bintree2list(root); ` `// Print the converted list ` `printList(head); ` `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*