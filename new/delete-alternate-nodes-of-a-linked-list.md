# 删除链接列表

的备用节点

给定一个单链列表，从第二个节点开始删除它的所有备用节点。 例如，如果给定的链表为1-> 2-> 3-> 4-> 5，则您的函数应将其转换为1-> 3-> 5，并且给定的链表为1-> 2-> 3-> 4，然后将其转换为1-> 3。

**方法1（迭代）**
跟踪要删除的节点的先前节点。 首先更改上一个节点的下一个链接，然后释放为该节点分配的内存。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to remove alternate ``// nodes of a linked list ``#include <bits/stdc++.h>``using` `namespace` `std;``/* A linked list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``/* deletes alternate nodes ``of a list starting with head */``void` `deleteAlt(Node *head) ``{ ` `if` `(head == NULL) ` `return` `; ` `/* Initialize prev and node to be deleted */` `Node *prev = head; ` `Node *node = head->next; ` `while` `(prev != NULL && node != NULL) ` `{ ` `/* Change next link of previous node */` `prev->next = node->next; ` `/* Free memory */` `free` `(node); ` [ `/* Update prev and node */` `prev = prev->next; ` `if` `(prev != NULL) ` `node = prev->next; ` `} ``} ``/* UTILITY FUNCTIONS TO TEST fun1() and fun2() */``/* Given a reference (pointer to pointer) to the head ``of a list and an int, push a new node on the front ``of the list. */``void` `push(Node** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` [ `/* put in the data */` `new_node->data = new_data; `​​  `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``/* Function to print nodes in a given linked list */``void` `printList(Node *node) ``{ ` `while` `(node != NULL) ` `{ ` `cout<< node->data<<` `" "` `; ` `node = node->next; ` `} ``} ``/* Driver code */``int` `main() ``{ ` `/* Start with the empty list */` `Node* head = NULL; ` `/* Using push() to construct below list ` `1->2->3->4->5 */` `push(&head, 5); ` `push(&head, 4); ` `push(&head, 3); ` [HT G140] `push(&head, 1); ` `cout<<` `"List before calling deleteAlt() \n"` `; ` `printList(head); ` `deleteAlt(head); ` `cout<<` `"\nList after calling deleteAlt() \n"` ] `printList(head); ` `return` `0; ``} ` [`// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*