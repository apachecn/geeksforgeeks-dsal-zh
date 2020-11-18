# 检查二叉树的有序遍历是否是回文

给定[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和任务，以检查其[有序序列](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)是否是回文。

**示例：**

> **输入：**
> ![](img/38794aac18f0127ecf2abcd9bdda2a98.png)
> **输出：** True
> **说明：**
> 树的顺序为“ bbaaabb” 这是回文字符串。
> 
> **输入：**
> ![](img/787020686d40d89902c5e489a8572ccb.png)
> **输出：**错误
> **说明：**
> 树的顺序为“ bbdaabb” 这不是回文字符串。

**方法：**
要解决此问题，请参考以下步骤：

*   [将给定的二叉树转换为双链表](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)。
*   这将问题减少到[。检查字符的双向链接列表是否是回文](https://www.geeksforgeeks.org/check-doubly-linked-list-characters-palindrome-not/)。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to check if``// the Inorder sequence of a``// Binary Tree is a palindrome``#include <bits/stdc++.h>``using` `namespace` `std;``// Define node of tree``struct` `node {` `char` `val;` `node* left;` `node* right;``};`的`// Function to create the node``node* newnode(` `char` `i)``{` `node* temp = NULL;` `temp =` `new` `node();` `temp->val = i;` `temp->left = NULL;` `temp->right = NULL;` `return` `temp;``}``// Function to convert the tree``// to the double linked list``node* conv_tree(node* root,` `node* shoot)``{` `if` `(root->left != NULL)` `shoot = conv_tree(root->left,` `shoot);` `root->left = shoot;` `if` `(shoot != NULL)` `shoot->right = root;`​​ `shoot = root;` ] `if` `(root->right != NULL)` `shoot = conv_tree(root->right,` `shoot);` `return` `shoot;``}``// Function for checking linked``// list is palindrom or not``int` `checkPalin(node* root)``{` `node* voot = root;` `// Count the nodes` ] `// form the back` `int` `j = 0;` `// Set the pointer at the` `// very first node of the` `// linklist and count the` `// length of the linklist` `while` `(voot->left != NULL) {` `j = j + 1;` `voot = voot->left;` `}` `int` `i = 0;` `while` `(i < j) {` `// Check if the value matches` `if` `(voot->val != root->val)` `return` `0;` `else` `{` `i = i + 1;` `j = j - 1;` `voot = voot->right;` `root = root->left;` `}` `}` `return` `1;``}` ]`// Driver Program``int` `main()``{` `node* root = newnode(` `'b'` `);` `root->left = newnode(` `'b'` `);` `root->right = newnode(` `'a'` `);` `root->left->right = newnode(` `'b'` `);` `root->left->left = newnode(` `'a'` `);` `node* shoot = conv_tree(root, NULL);` `if` `(checkPalin(shoot))` `cout <<` `"True"` `<< endl;` `else` `cout <<` `"False"` `<< endl;``}` |

*chevron_right**filter_none*