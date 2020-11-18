# 将二叉树展平为链接列表| 第2组

给定一个二叉树，将其展平为一个链表。 展平后，每个节点的左侧应指向NULL，右侧应按级别顺序包含下一个节点。

**范例**：

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

**方法：**在先前的 [](https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list/) 中已经讨论了使用递归的方法。 这种方法暗示了使用堆栈对二叉树进行预遍历。 在此遍历中，每次将右子项推入堆栈时，都会使右子项等于左子项，并使左子项等于NULL。 如果节点的右子节点变为NULL，则会弹出堆栈，而右子节点将从堆栈中弹出。 重复上述步骤，直到堆栈的大小为零或根为NULL。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to flatten the linked ``// list using stack &#124; set-2 ``#include <iostream>``#include <stack>``using` `namespace` `std;``struct` `Node {` `int` `key;` `Node *left, *right;``};``/* utility that allocates a new Node ` `with the given key  */``Node* newNode(` `int` `key)``{` `Node* node =` `new` `Node;` `node->key = key;` `node->left = node->right = NULL;` `return` `(node);``}` [`// To find the inorder traversal``void` `inorder(` `struct` `Node* root)``{` `// base condition` `if` `(root == NULL)` `return` `;` `inorder(root->left);` `cout << root->key <<` `" "` `;` `inorder(root->right);``}``// Function to convert binary tree into``// linked list by altering the right node``// and making left node point to NULL``Node* solution(Node* A)``{` `// Declare a stack` `stack<Node*> st;` `Node* ans = A;` `// Iterate till the stack is not empty` `// and till root is Null`​​ ] `while` `(A != NULL &#124;&#124; st.size() != 0) {` `// Check for NULL` `if` `(A->right != NULL) {` `st.push(A->right);` `}` `// Make the Right Left and` `// left NULL`[H TG289]  `A->right = A->left;` `A->left = NULL;` `// Check for NULL` `if` `(A->right == NULL && st.size() != 0) {` `A->right = st.top();` `st.pop();` `}` `// Iterate` `A = A->right;` `}` `return` `ans;``}``// Driver Code``int` `main()``{` `/*    1` `/   \` `2     5` `/ \     \` `3   4     6 */` `// Build the tree` `Node* root = newNode(1);` `root->left = newNode(2);` `root->right = newNode(5);` `root->left->left = newNode(3);` `root->left->right = newNode(4);` `root->right->right = newNode(6);` `// Call the function to` `// flatten the tree` `root = solution(root);`] `cout <<` `"The Inorder traversal after "` `"flattening binary tree "` `;` `// call the function to print` `// inorder after flatenning` `inorder(root);` `return` `0;` `return` `0;``}` |

*chevron_right**filter_none*