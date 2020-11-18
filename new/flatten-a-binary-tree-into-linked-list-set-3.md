# 将二叉树展平为链接列表| 第3组

给定一棵二叉树，将其平整就位到链表中。 不允许使用辅助数据结构。 展平后，每个节点的左侧应指向NULL，右侧应按级别顺序包含下一个节点。

**示例：**

```
Input: 
          1
        /   \
       2     5
      / \     \
     3   4     6

Output:
    1
     \
      2
       \
        3
         \
          4
           \
            5
             \
              6

Input:
        1
       / \
      3   4
         /
        2
         \
          5
Output:
     1
      \
       3
        \
         4
          \
           2
            \ 
             5

```

**方法：**以有序格式递归二叉树，在函数调用的每个阶段传递平展链表中最后一个节点的地址，以便当前节点可以使自己成为最后一个节点的右节点。
对于左孩子，其父节点是拼合列表中的最后一个节点。
对于右孩子，有两个条件：

*   如果父节点没有左子节点，则父节点是展平列表中的最后一个节点。
*   如果left child不为null，则左子树中的叶节点是扁平化列表中的最后一个节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to flatten the binary tree``// using previous node approach``using` `namespace` `std;``#include <iostream>``#include <stdlib.h>``// Structure to represent a node of the tree``struct` `Node {` `int` `data;` `struct` `Node* left;` `struct` `Node* right;``};`的`Node* AllocNode(` `int` `data)``{` `Node* temp =` `new` `Node;` `temp->left = NULL;` `temp->right = NULL;` `temp->data = data;` `return` `temp;``}``// Utility function to print the inorder``// traversal of the tree``void` `PrintInorderBinaryTree(Node* root)``{` `if` `(root == NULL)` `return` `;` `PrintInorderBinaryTree(root->left);` `std::cout << root->data <<` `" "` `;` `PrintInorderBinaryTree(root->right);``}``// Function to make current node right of``// the last node in the list` HTG236] `void` `FlattenBinaryTree(Node* root, Node** last)``{` `if` `(root == NULL)` `return` `;` `Node* left = root->left;` `Node* right = root->right;` `// Avoid first iteration where root is` ] `// the only node in the list` `if` `(root != *last) {` `(*last)->right = root;` `(*last)->left = NULL;` `*last = root;` `}` `FlattenBinaryTree(left, last);`​​ [HT G97] `FlattenBinaryTree(right, last);` `if` `(left == NULL && right == NULL)` `*last = root;``}``// Driver Code``int` `main()``{` `// Build the tree` `Node* root = AllocNode(1);` `root->left = AllocNode(2);` `root->left->left = AllocNode(3);` `root->left->right = AllocNode(4);` `root->right = AllocNode(5);` `root->right->right = AllocNode(6);` `// Print the inorder traversal of the` `// original tree` `std::cout <<` `"Original inorder traversal : "` `;` `PrintInorderBinaryTree(root);` `std::cout << std::endl;` `// Flatten a binary tree, at the beginning` `// root node is the only and last in the list` [HTG1 44] `FlattenBinaryTree(root, &last);` `// Print the inorder traversal of the flattened` `// binary tree` `std::cout <<` `"Flattened inorder traversal : "` `;` `PrintInorderBinaryTree(root);` `std::cout << std::endl;`] `return` `0;``}` |

*chevron_right**filter_none*