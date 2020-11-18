# 以相反的顺序打印双向链接列表

给定正整数的双链表。 任务是按照相反的顺序打印给定的双向链表数据。

**范例**：

```
Input: List = 1 <=> 2 <=>  3 <=>  4 <=>  5
Output: 5  4  3  2  1

Input: 10 <=> 20 <=> 30 <=> 40
Output: 40  30  20  10

```

**方法：**

*   用指针指向双向链表的头部。
*   现在，开始遍历链接列表，直到最后。
*   到达最后一个节点后，开始向后移动并同时打印该节点->数据。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to print doubly ``// linked list in reverse order ``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Doubly linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;` `struct` `Node* prev;``};``// Function to print nodes of Doubly ``// Linked List in reverse order ``void` `reversePrint(` `struct` `Node** head_ref)``{` `struct` `Node* tail = *head_ref;` [ `// Traversing till tail of the linked list` `while` `(tail->next != NULL) {` `tail = tail->next;` `}` `// Traversing linked list from tail` `// and printing the node->data` `while` `(tail != *head_ref) {` `cout << tail->data <<` `" "` `;` `tail = tail->prev;` `}` `cout << tail->data << endl;``}``/* UTILITY FUNCTIONS */``// Function to insert a node at the ``// beginging of the Doubly Linked List ``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `// allocate node ` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data ` `new_node->data = new_data;` `// since we are adding at the beginning, ` `// prev is always NULL ` `new_node->prev = NULL;` `// link the old list off the new node ` `new_node->next = (*head_ref);`[HT G254]  `// change prev of head node to new node ` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node ` `(*head_ref) = new_node;``}`​​ `// Driver Code``int` `main()``{` `// Start with the empty list ` `struct` `Node* head = NULL;`[ `// Let us create a sorted linked list` `// to test the functions ` `// Created linked list will be 10->8->4->2 ` `push(&head, 2);` `push(&head, 4);` `push(&head, 8);` `push(&head, 10);` `cout <<` `"Linked List elements in reverse order : "` `<< endl;` `reversePrint(&head);` `return` `0;``}` |

*chevron_right**filter_none*