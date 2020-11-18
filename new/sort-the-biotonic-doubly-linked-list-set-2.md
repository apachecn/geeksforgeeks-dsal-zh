# 排序生物群落双链表| 第2组

对给定的生物张力双链表进行排序。 双调双向链表是一个双向链表，它先增加然后减小。 严格增加或严格减少的列表也是生物群落双链表。

**示例：**

```
Input : 2 5 7 12 10 6 4 1
Output : 1 2 4 5 6 7 10 12

Input : 20 17 14 8 3
Output : 3 8 14 17 20

```

 [### 推荐：请首先在IDE上尝试您的方法，然后查看解决方案。](https://ide.geeksforgeeks.org) 

[](https://ide.geeksforgeeks.org)

在[先前的帖子](https://www.geeksforgeeks.org/sort-biotonic-doubly-linked-list/)中，我们拆分了双音双链表，将后半部分反转，然后将两半合并。 在这篇文章中，讨论了另一种替代方法。 想法是维护两个指针，一个指针最初指向双向链接列表的head元素，另一个指向双向链接列表的最后一个元素。 比较这两个元素并添加较小的元素以得到一个列表。 该元素指向下一个相邻元素的前进指针。 重复此过程，直到输入双链表的所有元素都添加到列表中。

下面是上述算法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to sort the biotonic``// doubly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// structure of node of the doubly linked list``struct` `Node {` `int` `data;` `struct` `Node* next;` `struct` `Node* prev;``};``// function to sort a biotonic doubly linked list``struct` `Node* sort(` `struct` `Node* head)``{` `// If number of elements are less than or` `// equal to 1 then return.` `if` `(head == NULL &#124;&#124; head->next == NULL) {` `return` `head;` `}` `// Pointer to first element of doubly` `// linked list.` `Node* front = head;`[HTG36 3]  `// Pointer to last element of doubly` `// linked list.` `Node* last = head;` `// Dummy node to which resultant` `// sorted list is added.` `Node* res =` `new` `Node;` `// Node after which next element` `// of sorted list is added.` `Node* resEnd = res;`的 `// Node to store next element to` `// which pointer is moved after` `// element pointed by that pointer` `// is added to result list.` `Node* next;` `// Find last element of input list.` `while` `(last->next != NULL) {` `last = last->next;` `}` `// Compare first and last element` `// until both pointers are not equal.` [ `while` `(front != last) {` `// If last element data is less than` `// or equal to front element data,` `// then add last element to` `// result list and change the` `// last pointer to its previous` `// element.` `if` `(last->data <= front->data) {` `resEnd->next = last;` `next = last->prev;` `last->prev->next = NULL;` `last->prev = resEnd;` `last = next;` `resEnd = resEnd->next;` `}` `// If front element is smaller, then` `// add it to result list and change` `// front pointer to its next element.` `else` `{` `resEnd->next = front;` `next = front->next;` `front->next = NULL;` `front->prev = resEnd;`[HTG46 3]  `front = next;` `resEnd = resEnd->next;` `}` `}` `// Add the single element left to the` `// result list.` `resEnd->next = front;` `front->prev = resEnd;` ] `// The head of required sorted list is` `// next to dummy node res.` `return` `res->next;``}``// Function to insert a node at the beginning``// of the Doubly Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `// allocate node` `struct` `Node* new_node = (` `struct` `Node*)` ] `malloc` `(` `sizeof` `(` `struct` `Node));` G508] `new_node->data = new_data;` `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` ] `// change prev of head node to new node` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node` `(*head_ref) = new_node;``}` [`// Function to print nodes in a given doubly``// linked list``void` `printList(` `struct` `Node* head)``{` `// if list is empty` `if` `(head == NULL)` `cout <<` `"Doubly Linked list empty"` `;` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver program to test above``int` `main()``{` `struct` `Node* head = NULL;` `// Create the doubly linked list:` `// 2<->5<->7<->12<->10<->6<->4<->1`​​ `push(&head, 1);` `push(&head, 4);` `push(&head, 6);` `push(&head, 10);` `push(&head, 12);` `push(&head, 7);` `push(&head, 5);` `push(&head, 2);` `cout <<` `"Original Doubly linked list:\n"` `;` `printList(head);`]  `// sort the biotonic DLL` `head = sort(head);` `cout <<` `"\nDoubly linked list after sorting:\n"` `;` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*