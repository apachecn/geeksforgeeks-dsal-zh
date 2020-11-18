# 以给定大小的组反向链接列表（迭代方法）

给定一个链表和一个整数 **K** ，任务是反转给定链表的每个 **K** 个节点。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> NULL， K = 3
> **输出：** 3 2 1 6 5 4 8 7
> 
> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> NULL， K = 5
> **输出：** 5 4 3 2 1 8 7 6

**方法：**我们已经在帖子 [Set 1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/) 和 [Set 2](https://www.geeksforgeeks.org/reverse-linked-list-groups-given-size-set-2/) 中讨论了递归解决方案。 在这篇文章中，我们将讨论上述问题的迭代解决方案。 与上述解决方案不同，我们不使用任何形式的堆栈来实现我们的解决方案。 我们反转链表的前k个节点。 反转时，我们使用join和tail指针跟踪k反转链表的第一个和最后一个节点。 反转链表的k个节点后，我们连接由尾指针指向的节点，并连接并更新它们。 我们重复此过程，直到所有节点组都被反转为止。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Link list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to reverse the linked list in groups of ``size k and return the pointer to the new head node. */``Node* reverse(` `struct` `Node* head,` `int` `k)``{` `Node* prev = NULL;` `Node* curr = head;` `Node* temp = NULL;` `Node* tail = NULL;` `Node* newHead = NULL;` `Node* join = NULL;` `int` `t = 0;` `// Traverse till the end of the linked list` `while` `(curr) {` `t = k;` `join = curr;` [H TG263] `prev = NULL;` `// Reverse group of k nodes of the linked list`​​  `while` `(curr && t--) {` `temp = curr->next;` `curr->next = prev;` `prev = curr;` `curr = temp;` `}` `// Sets the new head of the input list` `if` `(!newHead)` `newHead = prev;` `/* Tail pointer keeps track of the last node ` `of the k-reversed linked list. We join the ` `tail pointer with the head of the next ` `k-reversed linked list's head */` `if` `(tail)` `tail->next = prev;`的 `/* The tail is then updated to the last node ` `of the next k-reverse linked list */` `tail = join;` `}`[ `/* newHead is new head of the input list */` `return` `newHead;``}``// Function to insert a node at``// the head of the linked list``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);`]  `/* move the head to point to the new node */` `(*head_ref) = new_node;``}` [`// Function to print the linked list``void` `printList(Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `node = node->next;` `}``}``// Driver code``int` `main()``{` ] `// Start with the empty list` `Node* head = NULL;` `// Created Linked list is` `// 1->2->3->4->5->6->7->8->9` `push(&head, 9);` `push(&head, 8);` `push(&head, 7);` `push(&head, 6);` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);` `int` `k = 3;` `cout <<` `"Given linked list \n"` `;` `printList(head);` `head = reverse(head, k);` `cout <<` `"\nReversed Linked list \n"` `;` `printList(head);` [ `return` `(0);``}` |

*chevron_right**filter_none*