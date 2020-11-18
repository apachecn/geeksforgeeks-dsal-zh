# 仅使用2个指针迭代反向链接列表（一种有趣的方法）

给定指向链表头节点的指针，任务是反转链表。

例子：

```
Input : Head of following linked list  
       1->2->3->4->NULL
Output : Linked list should be changed to,
       4->3->2->1->NULL

Input : Head of following linked list  
       1->2->3->4->5->NULL
Output : Linked list should be changed to,
       5->4->3->2->1->NULL

```

在文章[反向链接列表](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)中，我们已经看到了如何反向链接列表。 在**迭代方法**中，我们使用了3个指针 **prev，cur** 和 **next** 。 下面是一种仅使用两个指针的有趣方法。 这个想法是使用XOR交换指针。

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to reverse a linked list using two pointers.``#include <bits/stdc++.h>``using` `namespace` `std;``typedef` `uintptr_t` `ut;``/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to reverse the linked list using 2 pointers */``void` `reverse(` `Node** head_ref)``{` `struct` `Node* prev = NULL;` `struct` `Node* current = *head_ref;`[HTG32 `// at last prev points to new head` `while` `(current != NULL) {` `// This expression evaluates from left to right` `// current->next = prev, changes the link fron` `// next to prev node` `// prev = current, moves prev to current node for` `// next reversal of node` `// This example of list will clear it more 1->2->3->4` `// initially prev = 1, current = 2` `// Final expression will be current = 1^2^3^2^1,` `// as we know that bitwise XOR of two same` `// numbers will always be 0 i.e; 1^1 = 2^2 = 0` `// After the evaluation of expression current = 3 that` `// means it has been moved by one node from its` `// previous position` `current = (` `struct` `Node*)((ut)prev ^ (ut)current ^ (ut)(current->next) ^ (ut)(current->next = prev) ^ (ut)(prev = current));` `}` `*head_ref = prev;``}``/* Function to push a node */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));`的 `/* put in the data  */` `new_node->data = new_data;`​​  `/* link the old list off the new node */` [HTG1 05] `/* move the head to point to the new node */` `(*head_ref) = new_node;``}` [`/* Function to print linked list */``void` `printList(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `printf` `(` `"%d  "` `, temp->data);` `temp = temp->next;` `}``}``/* Driver program to test above function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;`] `push(&head, 20);` `push(&head, 4);` `push(&head, 15);` `push(&head, 85);` `printf` `(` `"Given linked list\n"` `);` `printList(head);`] `reverse(&head);` `printf` `(` `"\nReversed Linked list \n"` `);` `printList(head);`[  `return` `0;``}` |

*chevron_right**filter_none*