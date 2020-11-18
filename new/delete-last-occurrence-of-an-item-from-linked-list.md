# 从链接列表

中删除最后一次出现的项目

遍历整个列表，并使用双指针跟踪包含最后出现节点地址的节点。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `#include <stdio.h>``#include <stdlib.h>``// A linked list Node``struct` `Node {` `int` `data;` `struct` `Node* next;``};`的`// Function to delete the last occurrence``void` `deleteLast(` `struct` `Node** head,` `int` `x)``{` `struct` `Node** tmp1 = NULL;` `while` `(*head) {` `if` `((*head)->data == x) {` `tmp1 = head;` `}` `head = &(*head)->next;` `}` `if` `(tmp1) {` `struct` `Node* tmp = *tmp1;` `*tmp1 = tmp->next;` `free` `(tmp);` `}``}``/* Utility function to create a new node with``given key */``struct` `Node* newNode(` `int` `x)``{` `struct` `Node* node =` `malloc` `(` `sizeof` `(` `struct` `Node*));` `node->data = x;` `node->next = NULL;` `return` `node;``}``// This function prints contents of linked list``// starting from the given Node``void` `display(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `if` `(head == NULL) {` `printf` `(` `"NULL\n"` `);` `return` `;` `}` `while` `(temp != NULL) {` `printf` `(` `"%d --> "` `, temp->data);` `temp = temp->next;` `}` `printf` `(` `"NULL\n"` `);``}``/* Driver program to test above functions*/``int` `main()`​​ `{` `struct` `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);` `head->next->next->next = newNode(4);` `head->next->next->next->next = newNode(5);` `head->next->next->next->next->next = newNode(4);` `head->next->next->next->next->next->next = newNode(4);` `printf` `(` `"Created Linked list: "` `);` `display(head);` `deleteLast(&head, 4);` `// Pass the address of the head pointer` `printf` `(` `"List after deletion of 4: "` `);` `display(head);` `return` `0;``}` |

*chevron_right**filter_none*

给定喜欢的列表和要删除的密钥。 从链接中删除最后一次出现的密钥。 该列表可能有重复项。

例子：

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

这个想法是从头到尾遍历链表。 遍历时，请跟踪最后出现的关键字。 遍历完整列表后，通过复制下一个节点的数据并删除下一个节点来删除最后一个出现的节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// A C++ program to demonstrate deletion of last``// Node in singly linked list``#include <bits/stdc++.h>``// A linked list Node``struct` `Node {` `int` `key;` `struct` `Node* next;``};` [`void` `deleteLast(Node* head,` `int` `key)``{` `// Initialize previous of Node to be deleted` `Node* x = NULL;` `// Start from head and find the Node to be` `// deleted` `Node* temp = head;` `while` `(temp) {` `// If we found the key, update xv` `if` `(temp->key == key)` `x = temp;` `temp = temp->next;` `}` `// key occurs at-least once` `if` `(x != NULL) {` `// Copy key of next Node to x` `x->key = x->next->key;` ] `// Store and unlink next` `temp = x->next;` `x->next = x->next->next;`[ `// Free memory for next` `delete` `temp;` `}``}``/* Utility function to create a new node with` `given key */``Node* newNode(` `int` `key)``{` `Node* temp =` `new` `Node;` `temp->key = key;` `temp->next = NULL;` `return` `temp;``}``// This function prints contents of linked list``// starting from the given Node``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `" %d "` `, node->key);`​​  `node = node->next;` `}``}`[`/* Driver program to test above functions*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);` `head->next->next->next = newNode(5);` `head->next->next->next->next = newNode(2);` `head->next->next->next->next->next = newNode(10);` `puts` `(` `"Created Linked List: "` `);` `printList(head);` `deleteLast(head, 2);` `puts` `(` `"\nLinked List after Deletion of 1: "` [HTG1 48] `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*