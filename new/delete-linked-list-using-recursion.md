# 使用递归

删除链接列表

使用递归删除给定的链表

**方法**
1）如果head等于NULL，则链表为空，我们简单地返回。
2）递归删除头节点之后的链表。
3）删除头节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to recursively delete a linked list``#include <bits/stdc++.h>` ] `int` `data;` `struct` `Node* next;``};`的`/* Recursive Function to delete the entire linked list */``void` `deleteList(` `struct` `Node* head)``{` `if` `(head == NULL)` `return` `;` `deleteList(head->next); ` `free` `(head);``}``/* Given a reference (pointer to pointer) to ` `the head of a list and an int, push a new` `node on the front of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` [HTG1 48] `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* Driver program to test count function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `/* Use push() to construct below list` `1->12->1->4->1 */` `push(&head, 1);` `push(&head, 4);` `push(&head, 1);` `push(&head, 12);` `push(&head, 1);` `printf` `(` `"\n Deleting linked list"` `);` `deleteList(head);` `printf` `(` `"\nLinked list deleted"` `);` `return` `0;``}` |

*chevron_right**filter_none*