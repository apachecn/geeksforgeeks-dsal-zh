# 通过更改指针|配对交换链表的相邻节点| 设置2

给定一个单链表，编写一个函数以成对交换元素。

```
Input : 1->2->3->4->5->6->7
Output : 2->1->4->3->6->5->7,

Input : 1->2->3->4->5->6 
Output : 2->1->4->3->6->5
```

已经讨论了一种解决方案 [set 1](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/) 。 这里讨论一个更简单的解决方案。 我们显式地更改前两个节点的指针，然后修复其余的节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* This program swaps the nodes of linked list ` `rather than swapping the field from the nodes.` `Imagine a case where a node contains many ` `fields, there will be plenty of unnecessary ` `swap calls. */``#include<bits/stdc++.h>``using` `namespace` `std;``/* A linked list node */``struct` `Node``{` `int` `data;` `struct` `Node *next;``};``/* Function to pairwise swap elements of a` `linked list */``Node *pairWiseSwap(Node *head)``{` `// If linked list is empty or there is only` `// one node in list` `if` `(head == NULL &#124;&#124; head->next == NULL)` `return` `head;` `// Fix the head and its next explicitly to` `// avoid many if else in while loop` `Node *curr = head->next->next;` `Node *prev = head;` `head = head->next;` `head->next = prev;` `// Fix remaining nodes` `while` `(curr != NULL && curr->next != NULL)` `{` `prev->next = curr->next;` `prev = curr;` `Node *next = curr->next->next;` `curr->next->next = curr;` `curr = next;` `}` `prev->next = curr;` `return` `head;``}`​​`/* Function to add a node at the beginning of ` `Linked List */``void` `push(` ] `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;`[  `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* Function to print nodes in a given linked list */``void` `printList(` `struct` `Node *node)``{` `while` `(node != NULL)` `{` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}``}``/* Druver program to test above function */``int` `main()``{` `struct` `Node *start = NULL;` `/* The constructed linked list is:` `1->2->3->4->5->6->7 */` `push(&start, 7);` `push(&start, 6);` `push(&start, 5);` `push(&start, 4);` `push(&start, 3);` `push(&start, 2); ` `push(&start, 1);` `printf` `(` `"\n Linked list before calling pairWiseSwap() "` `);` `printList(start);` `start = pairWiseSwap(start);` [ `printf` `(` `"\n Linked list after calling pairWiseSwap() "` `);` `printList(start);`[ `return` `0;``}` |

*chevron_right**filter_none*