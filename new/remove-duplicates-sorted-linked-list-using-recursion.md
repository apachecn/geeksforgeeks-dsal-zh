# 使用递归

从排序的链表中删除重复项

编写一个removeDuplicates（）函数，该函数采用以非降序排序的列表，并从列表中删除所有重复的节点。 该列表仅应遍历一次。

例如，如果链接列表是11-> 11-> 11-> 21-> 43-> 43-> 60，则removeDuplicates（）应该将列表转换为11-> 21-> 43-> 60。

**算法：**
从头（或头）递归遍历列表，在完成递归调用后，比较下一个节点（返回的节点）和当前节点（头）。 如果两个节点的数据相等，则返回下一个**（头为>），否则返回当前**节点（头）**。**

**实现：**
除了removeDuplicates（）以外的功能仅用于创建链接链表并测试removeDuplicates（）。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* C Program to remove duplicates` `from a sorted linked list */``#include <bits/stdc++.h>``#include <stdlib.h>`]`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* The function removes duplicates from a sorted list */``struct` `Node* removeDuplicates(` `struct` `Node* head)``{` `/* if head is null then return*/` `if` `(head == NULL)` `return` `NULL;` `/* Remove duplicates from list after head */` `head->next = removeDuplicates(head->next);` `// Check if head itself is duplicate` `if` `(head->next != NULL && ` `head->next->data == head->data) {` `Node* res = head->next;` `delete` `head;` `return` `res;` `}` `return` `head;``}``/* UTILITY FUNCTIONS */``/* Function to insert a node at ` `the beginning of the linked list */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* Function to print nodes in a given linked list */``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;`[H TG101] `}``}``/* Driver program to test above functions*/``int` `main()``{`​​ `/* Start with the empty list */` `struct` `Node* head = NULL;` `/* Let us create a sorted linked list to test the functions` `Created linked list will be 11->11->11->13->13->20 */` `push(&head, 20);` `push(&head, 13);` `push(&head, 13);` `push(&head, 11);` `push(&head, 11);` `push(&head, 11);` `printf` `(` `"\n Linked list before duplicate removal "` `);` `printList(head);` `/* Remove duplicates from linked list */` `struct` `Node* h = removeDuplicates(head);` `printf` `(` `"\n Linked list after duplicate removal "` `);` `printList(h);` `return` `0;``}` |

*chevron_right**filter_none*