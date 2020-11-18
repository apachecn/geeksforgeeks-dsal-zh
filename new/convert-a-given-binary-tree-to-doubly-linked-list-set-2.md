# 将给定的二叉树转换为双链表| 设置2

给定二叉树（BT），将其转换为双链表（DLL）。 节点中的左指针和右指针分别用作转换后的DLL中的上一个指针和下一个指针。 DLL中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT中最左边的节点）必须是DLL的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

在的[中讨论了此问题的解决方案。
在这篇文章中，讨论了另一个简单有效的解决方案。 这里讨论的解决方案有两个简单的步骤。](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)

**1）*固定左指针*：**在此步骤中，我们将左指针更改为指向DLL中的先前节点。 想法很简单，我们对树进行有序遍历。 在有序遍历中，我们跟踪先前访问的节点，并将左指针更改为先前的节点。 请参见以下实现中的 *fixPrevPtr（）*。

**2）*固定右指针*：**上面的内容非常直观和简单。 如何更改指向DLL中下一个节点的右指针？ 这个想法是使用在步骤1中固定的左指针。我们从二叉树（BT）的最右边的节点开始。 最右边的节点是DLL中的最后一个节点。 由于左指针已更改为指向DLL中的上一个节点，因此我们可以使用这些指针线性遍历整个DLL。 遍历将是从最后一个节点到第一个节点。 在遍历DLL时，我们跟踪先前访问的节点，并更改指向先前节点的右指针。 请参见以下实现中的 *fixNextPtr（）*。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// A simple inorder traversal based ``// program to convert a Binary Tree to DLL ``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A tree node ``class` `node ``{ ` `public` `:` `int` `data; ` `node *left, *right; ``}; ``// A utility function to create``// a new tree node ``node *newNode(` `int` `data) ``{ ` `node *Node =` `new` `node();` `Node->data = data; ` `Node->left = Node->right = NULL; ` `return` `(Node); ``} ``// Standard Inorder traversal of tree ``void` `inorder(node *root) ``{ ` `if` `(root != NULL) ` `{ ` `inorder(root->left); ` `cout <<` `"\t"` `<< root->data; ` `inorder(root->right); ` `} ``} ``// Changes left pointers to work as ``// previous pointers in converted DLL ``// The function simply does inorder ``// traversal of Binary Tree and updates ``// left pointer using previously visited node ``void` `fixPrevPtr(node *root) ``{ ` `static` `node *pre = NULL; ` `if` `(root != NULL) ` `{ ` `fixPrevPtr(root->left); ` `root->left = pre; ` `pre = root; ` `fixPrevPtr(root->right); ` `} ``} ``// Changes right pointers to work ``// as next pointers in converted DLL ``node *fixNextPtr(node *root) ``{ ` `node *prev = NULL; ` `// Find the right most node ` `// in BT or last node in DLL ` `while` `(root && root->right != NULL) ` `root = root->right; ` `// Start from the rightmost node, ` `// traverse back using left pointers. ` `// While traversing, change right pointer of nodes. ` `while` `(root && root->left != NULL) ` `{ ` `prev = root; ` `root = root->left; ` `root->right = prev; ` `} ` `// The leftmost node is head ` `// of linked list, return it ` `return` `(root); ``} ``// The main function that converts ``// BST to DLL and returns head of DLL ``node *BTToDLL(node *root) ``{ ` `// Set the previous pointer ` `fixPrevPtr(root); ` `// Set the next pointer and return head of DLL ` `return` `fixNextPtr(root); ``} ``// Traverses the DLL from left tor right ``void` `printList(node *root) ``{ ` `while` `(root != NULL) ` `{ ` `cout<<` `"\t"` `<<root->data; ` `root = root->right; ` `} ``} ``// Driver code ``int` `main(` `void` `) ``{ ` `// Let us create the tree ` `// shown in above diagram ` `node *root = newNode(10); ` `root->left = newNode(12);` [H TG428] `root->right = newNode(15); ` `root->left->left = newNode(25); ` `root->left->right = newNode(30); ` `root->right->left = newNode(36); ` `cout<<` `"\n\t\tInorder Tree Traversal\n\n"` `; ` `inorder(root); `]  `node *head = BTToDLL(root); ` `cout <<` `"\n\n\t\tDLL Traversal\n\n"` `; ` `printList(head); ` `return` `0; ``}``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*