# 将第一个元素移到给定链接列表

的末尾

编写一个C函数，该函数将第一个元素移到给定的单链列表中。 例如，如果给定的链接列表为1-> 2-> 3-> 4-> 5，则该函数应将列表更改为2-> 3-> 4-> 5-> 1。

算法：
遍历列表直到最后一个节点。 使用两个指针：一个用于存储最后一个节点（last）的地址，另一个用于存储第一个节点（first）的地址。 循环结束后，请执行以下操作。
i）将head作为第二个节点（* head_ref = first- >接下来）。
ii）将first of next设置为NULL（first- > next = NULL）。
iii）将倒数第二个设为第一（倒数->下一个=第一）

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* C++ Program to move first element to end ` `in a given linked list */``#include <stdio.h>``#include <stdlib.h>`]`/* A linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* We are using a double pointer head_ref ` `here because we change head of the linked ` `list inside this function.*/``void` `moveToEnd(` `struct` `Node** head_ref)``{` `/* If linked list is empty, or it contains ` `only one node, then nothing needs to be ` `done, simply return */` `if` `(*head_ref == NULL &#124;&#124; (*head_ref)->next == NULL)` `return` `;`[ `/* Initialize first and last pointers */` `struct` `Node* first = *head_ref;` `struct` `Node* last = *head_ref;` `/*After this loop last contains address ` `of last node in Linked List */` `while` `(last->next != NULL) {` `last = last->next;` `}` `/* Change the head pointer to point ` `to second node now */`[  `*head_ref = first->next;` `/* Set the next of first as NULL */` `first->next = NULL;` `/* Set the next of last as first */` `last->next = first;``}``/* UTILITY FUNCTIONS */``/* Function to add a node at the beginning ` `of Linked List */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;`​​  `new_node->next = (*head_ref);`[HTG9 9] `(*head_ref) = new_node;``}``/* Function to print nodes in a given linked list */``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}``}` [`/* Driver program to test above function */``int` `main()``{` `struct` `Node* start = NULL;` `/* The constructed linked list is:` `1->2->3->4->5 */` `push(&start, 5);` `push(&start, 4);` `push(&start, 3);` `push(&start, 2);` `push(&start, 1);`[H TG146] `printf` `(` `"\n Linked list before moving first to end\n"` `);` `printList(start);` `moveToEnd(&start);` `printf` `(` `"\n Linked list after moving first to end\n"` `);` `printList(start);`] `return` `0;``}` |

*chevron_right**filter_none*