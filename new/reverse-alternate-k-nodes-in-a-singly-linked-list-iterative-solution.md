# 反向链接单个链表中的K个节点–迭代解决方案

给定一个链表和一个整数 **K** ，任务是反转每个备用 **K** 节点。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> 9- > NULL，K = 3
> **输出：** 3 2 1 4 5 6 9 8 7
> 
> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> 9- > NULL，K = 5
> **输出：** 5 4 3 2 1 6 7 8 9

**方法：**我们已经在此处讨论了递归解决方案[。 在这篇文章中，我们将讨论上述问题的迭代解决方案。 在遍历时，我们以一个迭代处理2k个节点，并使用join和tail指针跟踪给定链表中k个节点组的第一个和最后一个节点。 反转链表的k个节点后，我们将反向列表的最后一个节点（由尾部指针指向）与原始列表的第一个节点（由连接指针指向）连接。 然后，我们移动当前指针，直到跳过接下来的k个节点。
现在，尾部成为常规列表的最后一个节点（由更新的尾部指针指向），并且联接点指向反向列表的第一个，然后将它们联接。 我们重复此过程，直到以相同方式处理所有节点。](https://www.geeksforgeeks.org/reverse-alternate-k-nodes-in-a-singly-linked-list/)

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Link list node``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* Function to reverse alternate k nodes and ``return the pointer to the new head node */``Node* kAltReverse(` `struct` `Node* head,` `int` `k)``{` `Node* prev = NULL;` `Node* curr = head;` `Node* temp = NULL;` `Node* tail = NULL;`​​  `Node* newHead = NULL;` `Node* join = NULL;` `int` `t = 0;` `// Traverse till the end of the linked list` `while` `(curr) {` `t = k;` `join = curr;` `prev = NULL;` `/* Reverse alternative group of k nodes ` `// of the given linked list */` `while` `(curr && t--) {` `temp = curr->next;` `curr->next = prev;` `prev = curr;` `curr = temp;` `}` [ `// Sets the new head of the input list` `if` `(!newHead)` `newHead = prev;` `/* Tail pointer keeps track of the last node ` `of the k-reversed linked list. The tail pointer ` `is then joined with the first node of the ` `next k-nodes of the linked list */` `if` `(tail)` `tail->next = prev;` `tail = join;` `tail->next = curr;`。 `t = k;` `/* Traverse through the next k nodes ` `which will not be reversed */` ] `while` `(curr && t--) {` `prev = curr;` `curr = curr->next;` `}`[ `/* Tail pointer keeps track of the last ` `node of the k nodes traversed above */` `tail = prev;` `}` `// newHead is new head of the modified list` `return` `newHead;``}` [`// Function to insert a node at``// the head of the linked list``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}`]`// Function to print the linked list``void` `printList(Node* node)``{` `int` `count = 0;` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `node = node->next;` `count++;` `}``}``// Driver code`]`int` `main(` `void` `)``{` `// Start with the empty list` `Node* head = NULL;` `int` `i;` ] `// Create a list 1->2->3->4->...->10` `for` `(i = 10; i > 0; i--)` `push(&head, i);` `int` `k = 3;` [ `cout <<` `"Given linked list \n"` `;` `printList(head);` `head = kAltReverse(head, k);` `cout <<` `"\n Modified Linked list \n"` `;` `printList(head);`]  [ `return` `(0);``}` |

*chevron_right**filter_none*