# 以给定大小的组反向链接列表| 设置2

给定一个链表，编写一个函数以反转每k个节点（其中k是该函数的输入）。

**示例：**

```
Inputs:  1->2->3->4->5->6->7->8->NULL and k = 3 
Output:  3->2->1->6->5->4->8->7->NULL. 

Inputs:   1->2->3->4->5->6->7->8->NULL and k = 5
Output:  5->4->3->2->1->8->7->6->NULL.

```

我们已经在下面的
[中按给定大小的组反向链接列表了。 设置1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)

在本文中，我们使用了一个堆栈，该堆栈将存储给定链接列表的节点。 首先，将链接列表的k个元素压入堆栈。 现在一一弹出元素，并跟踪先前弹出的节点。 将上一个节点的下一个指针指向堆栈的顶部元素。 重复此过程，直到达到NULL。

该算法使用O（k）额外空间。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to reverse a linked list in groups``// of given size``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Reverses the linked list in groups of size k` `and returns the pointer to the new head node. */``struct` `Node* Reverse(` `struct` `Node* head,` `int` `k)``{` `// Create a stack of Node*` `stack<Node*> mystack;` `struct` `Node* current = head;` `struct` `Node* prev = NULL;` [ `while` `(current != NULL) {` `// Terminate the loop whichever comes first` `// either current == NULL or count >= k`​​ `int` `count = 0;` `while` `(current != NULL && count < k) {` `mystack.push(current);` `current = current->next;` `count++;` `}` `// Now pop the elements of stack one by one` `while` `(mystack.size() > 0) {`[ `// If final list has not been started yet.` `if` `(prev == NULL) {` `prev = mystack.top();` `head = prev;` `mystack.pop();` `}` `else` `{` `prev->next = mystack.top();` `prev = prev->next;` `mystack.pop();` `}` `}` `}` `// Next of last element will point to NULL.` `prev->next = NULL;`[HTG1 01] `return` `head;``}` [`/* UTILITY FUNCTIONS */``/* Function to push a node */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = ` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` HTG344] `/* put in the data  */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}` [`/* Function to print linked list */``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d  "` `, node->data);` `node = node->next;` `}``}``/* Driver program to test above function*/``int` `main(` `void` `)``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `/* Created Linked list is 1->2->3->4->5->6->7->8->9 */` `push(&head, 9);` `push(&head, 8);` `push(&head, 7);` `push(&head, 6);` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);` `printf` `(` `"\nGiven linked list \n"` `);` `printList(head);` `head = Reverse(head, 3);` `printf` `(` `"\nReversed Linked list \n"` `);` `printList(head);` [ `return` `0;``}` |

*chevron_right**filter_none*