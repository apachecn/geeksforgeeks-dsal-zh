# 从给定的二叉树

创建排序的链表

给定一个二叉树，任务是将其转换为排序的链表。

**示例：**

```
Input:
     1   
   /  \  
  2    3 
Output: 1 2 3

Input:
        2
      /   \
     4     8
   /  \   / \
  7   3  5   1
Output: 1 2 3 4 5 7 8

Input:
        3   
       /  
      4 
     / 
    1
   /
  9
Output: 1 3 4 9

```

**方法：**递归地迭代给定的二叉树，并使用[插入排序](http://www.geeksforgeeks.org/insertion-sort/)将每个节点添加到结果链表中其正确位置（最初为空）。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;`​​`// A linked list node``class` `Node {``public` `:` `int` `data;` `Node* next;` `Node(` `int` `data)` `{` `this` `->data = data;` `this` `->next = NULL;` `}``};``// A binary tree node``class` `treeNode {``public` `:` `int` `data;` `treeNode* left;` `treeNode* right;` `treeNode(` `int` `data)` `{` `this` `->data = data;` `this` `->left = NULL;` `this` `->right = NULL;` `}``};``// Function to print the linked list``void` `print(Node* head)``{` `if` `(head == NULL) {` `return` `;` `}` `Node* temp = head;` `while` `(temp != NULL) {` `cout << temp->data <<` `" "` `;` `temp = temp->next;` `}``}``// Function to create Linked list from given binary tree``Node* sortedList(Node* head, treeNode* root)``{` `// return head if root is null` `if` `(root == NULL) {` `return` `head;` `}`[H TG365]  `// First make the sorted linked list` `// of the left sub-tree` `head = sortedList(head, root->left);` `Node* newNode =` `new` `Node(root->data);` `Node* temp = head;` `Node* prev = NULL;` `// If linked list is empty add the` `// node to the head` `if` `(temp == NULL) {` `head = newNode;` `}` `else` `{` `// Find the correct position of the node` `// in the given linked list` `while` `(temp != NULL) {` `if` `(temp->data > root->data) {` `break` `;` `}` `else` `{` `prev = temp;` `temp = temp->next;` `}` `}` ] `// Given node is to be attached` `// at the end of the list` `if` `(temp == NULL) {` `prev->next = newNode;` `}` `else` `{` `// Given node is to be attached` `// at the head of the list` `if` `(prev == NULL) {` `newNode->next = temp;` `head = newNode;` ] `}` `else` `{` `// Insertion in between the list` `newNode->next = temp;` `prev->next = newNode;` `}` `}` `}` `// Now add the nodes of the right sub-tree` `// to the sorted linked list` ] `head = sortedList(head, root->right);` `return` `head;``}` [`// Driver code``int` `main()``{` `/* Tree:` `10` `/  \` `15    2` `/  \` `1    5``*/`] `treeNode* root =` `new` `treeNode(10);` `root->left =` `new` `treeNode(15);` `root->right =` `new` `treeNode(2);` `root->left->left =` `new` `treeNode(1);` `root->left->right =` `new` `treeNode(5);` `Node* head = sortedList(NULL, root);` `print(head);` `return` `0;``}` |

*chevron_right**filter_none*