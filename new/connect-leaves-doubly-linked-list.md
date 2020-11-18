# 提取双链表

中的二叉树的叶子

给定一棵二叉树，将其所有叶子提取到 **L** ist（DLL）的 **D** 整体 **L** 中。 请注意，需要就地创建DLL。 假设DLL和Binary Tree的节点结构相同，只是左右指针的含义不同。 在DLL中，左表示上一个指针，右表示下一个指针。

```
Let the following be input binary tree
        1
     /     \
    2       3
   / \       \
  4   5       6
 / \         / \
7   8       9   10

Output:
Doubly Linked List
785910

Modified Tree:
        1
     /     \
    2       3
   /         \
  4           6
```

我们需要遍历所有叶子，并通过更改它们的左右指针来连接它们。 我们还需要通过更改父节点中的左或右指针将它们从二叉树中删除。 有很多方法可以解决此问题。 在以下实现中，我们在当前链接列表的开头添加叶子，并使用指向head的指针更新列表的head。 由于我们在开始时插入，因此我们需要以相反的顺序处理叶子。 对于逆序，我们先遍历右侧子树，然后遍历左侧子树。 我们使用返回值来更新父节点中的左或右指针。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to extract leaves of ``// a Binary Tree in a Doubly Linked List ``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Structure for tree and linked list ``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *left, *right; ``}; ``// Main function which extracts all ``// leaves from given Binary Tree. ``// The function returns new root of ``// Binary Tree (Note that root may change ``// if Binary Tree has only one node).``// The function also sets *head_ref as ``// head of doubly linked list. left pointer ``// of tree is used as prev in DLL ``// and right pointer is used as next ``Node* extractLeafList(Node *root, Node **head_ref) ``{ ``// Base cases ``if` `(root == NULL)` `return` `NULL; ``if` `(root->left == NULL && root->right == NULL) ``{ ` `// This node is going to be added ` `// to doubly linked list of leaves,` `// set right pointer of this node ` `// as previous head of DLL. We ` `// don't need to set left pointer  ` `// as left is already NULL ` `root->right = *head_ref; `​​  `// Change left pointer of previous head ` `if` `(*head_ref != NULL) (*head_ref)->left = root; ` `// Change head of linked list ` `*head_ref = root; ` `return` `NULL;` `// Return new root ``} ``// Recur for right and left subtrees ``root->right = extractLeafList(root->right, head_ref); ``root->left = extractLeafList(root->left, head_ref); ``return` `root; ``} `]`// Utility function for allocating node for Binary Tree. ``Node* newNode(` `int` `data) ``{ ` `Node* node =` `new` `Node();` `node->data = data; ` `node->left = node->right = NULL; ` `return` `node; ``} ``// Utility function for printing tree in In-Order. ``void` `print(Node *root) ``{ ` `if` `(root != NULL) ` `{ ` `print(root->left); ` `cout<<root->data<<` `" "` `; ` `print(root->right); ` `} ``} ``// Utility function for printing double linked list. ``void` `printList(Node *head) ``{ ` `while` `(head) ` `{ ` `cout<<head->data<<` `" "` `; ` `head = head->right; ` `} ``} ``// Driver code ``int` `main() ``{ ` `Node *head = NULL; ` `Node *root = newNode(1); ` `root->left = newNode(2); ` `root->right = newNode(3); ` `root->left->left = newNode(4); ` `root->left->right = newNode(5); ` `root->right->right = newNode(6); ` `root->left->left->left = newNode(7); ` `root->left->left->right = newNode(8); ` `root->right->right->left = newNode(9); ` `root->right->right->right = newNode(10); ` `cout <<` `"Inorder Trvaersal of given Tree is:\n"` ] `; ` `print(root); ` `root = extractLeafList(root, &head); ` `cout <<` `"\nExtracted Double Linked list is:\n"` `; ` `printList(head); ` `cout <<` `"\nInorder traversal of modified tree is:\n"` `; ` `print(root); ` `return` `0; ``} `，`// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*