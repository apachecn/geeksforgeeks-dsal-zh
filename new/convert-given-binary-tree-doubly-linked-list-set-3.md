# 将给定的二叉树转换为双链表| 套装3

给定二叉树（BT），将其转换为就地双链表（DLL）。 节点中的左指针和右指针分别用作转换后的DLL中的上一个指针和下一个指针。 DLL中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT中最左边的节点）必须是DLL的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

针对此问题讨论了以下两种不同的解决方案。
[将给定的二叉树转换为双链表| 设置1](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)
[将给定的二叉树转换为双链表| 组合2](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-doubly-linked-list-set-2/)

在这篇文章中，讨论了第三个解决方案，这似乎是最简单的。 这个想法是对二叉树进行有序遍历。 在进行有序遍历时，请在变量 *prev* 中跟踪先前访问的节点。 对于每个访问的节点，将其作为 *prev* 的下一个，并将该节点的前一个作为 *prev* 的一个。

感谢rahul，wishall和所有其他读者对以上两个帖子的有用评论。

以下是此解决方案的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// A C++ program for in-place conversion of Binary Tree to DLL``#include <iostream>``using` `namespace` `std;``/* A binary tree node has data, and left and right pointers */``struct` `node``{` `int` `data;` `node* left;` `node* right;``};``// A simple recursive function to convert a given Binary tree to Doubly``// Linked List``// root --> Root of Binary Tree``// head --> Pointer to head node of created doubly linked list``void` `BinaryTree2DoubleLinkedList(node *root, node **head)``{` `// Base case` `if` `(root == NULL)` `return` `;` `// Initialize previously visited node as NULL. This is` `// static so that the same value is accessible in all recursive` `// calls` `static` `node* prev = NULL;` `BinaryTree2DoubleLinkedList(root->left, head);` `// Now convert this node` `if` `(prev == NULL)` `*head = root;` `else` `{` `root->left = prev;` `prev->right = root;` `}` `prev = root;` `// Finally convert right subtree` `BinaryTree2DoubleLinkedList(root->right, head);``}``/* Helper function that allocates a new node with the` `given data and NULL left and right pointers. */``node* newNode(` `int` `data)``{` `node* new_node =` `new` `node;` `new_node->data = data;` `new_node->left = new_node->right = NULL;` `return` `(new_node);``}`][H TG95]`void` `printList(node *node)``{` `while` `(node!=NULL)` `{` `cout << node->data <<` `" "` `;` `node = node->right;`​​  `}``}``/* Driver program to test above functions*/``int` `main()``{` HTG119] `node *root        = newNode(10);` `root->left        = newNode(12);` `root->right       = newNode(15);` `root->left->left  = newNode(25);` `root->left->right = newNode(30);` `root->right->left = newNode(36);` `// Convert to DLL` `node *head = NULL;` `BinaryTree2DoubleLinkedList(root, &head);` 7] `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*