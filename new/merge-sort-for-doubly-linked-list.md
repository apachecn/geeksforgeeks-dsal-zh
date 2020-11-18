# 合并双链表

的排序

给定一个双向链表，编写一个函数使用合并排序以递增顺序对双向链表进行排序。

例如，以下双向链接列表应更改为24810

![](img/61dcfe5f15a4317c70a1bea6d144f1b2.png)

[单链表](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)的合并排序已经讨论过。 此处的重要更改是在合并两个列表时还要修改先前的指针。

以下是双向链表的合并排序的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program for merge sort on doubly linked list ``#include <bits/stdc++.h>``using` `namespace` `std;``class` `Node ``{ ` `public` `:`​​ `int` `data; ` `Node *next, *prev; ``}; ``Node *split(Node *head); ``// Function to merge two linked lists ``Node *merge(Node *first, Node *second) ``{ ` `// If first linked list is empty ` `if` `(!first) ` `return` `second; ` `// If second linked list is empty ` `if` `(!second) ` `return` `first; ` `// Pick the smaller value ` `if` `(first->data < second->data) ` `{ ` `first->next = merge(first->next,second); ` `first->next->prev = first; ` `first->prev = NULL; ` `return` `first; ` `} ` `else` `{ ` `second->next = merge(first,second->next); ` `second->next->prev = second; ` `second->prev = NULL; ` `return` `second; ` `} ``} ``// Function to do merge sort ``Node *mergeSort(Node *head) ``{ ` `if` `(!head &#124;&#124; !head->next) ` `return` `head; ` `Node *second = split(head); ` `// Recur for left and right halves ` `head = mergeSort(head); ` `second = mergeSort(second); ` `// Merge the two sorted halves ` `return` `merge(head,second); ``} ` [`// A utility function to insert a new node at the ``// beginning of doubly linked list ``void` `insert(Node **head,` `int` `data) ``{ ` `Node *temp =` `new` `Node();` `temp->data = data; ` `temp->next = temp->prev = NULL; ` `if` `(!(*head)) ` `(*head) = temp; ` `else` `{ ` `temp->next = *head; ` `(*head)->prev = temp; ` `(*head) = temp; ` `} ``} ``// A utility function to print a doubly linked list in ``// both forward and backward directions ``void` `print(Node *head) ``{ ` `Node *temp = head; ` `cout<<` `"Forward Traversal using next poitner\n"` `; ` `while` `(head) ` `{ ` `cout << head->data <<` `" "` `; ` `temp = head; ` `head = head->next; ` `} ` `cout  <<` ] `"\nBackward Traversal using prev pointer\n"` `; ` `while` `(temp) ` `{ ` `cout << temp->data <<` `" "` `; ` `temp = temp->prev; ` `} ``} ``// Utility function to swap two integers ``void` `swap(` `int` `*A,` `int` `*B) ``{ ` `int` `temp = *A;` ] `*A = *B; ` `*B = temp; ``} `[HTG1 97]的`// Split a doubly linked list (DLL) into 2 DLLs of ``// half sizes ``Node *split(Node *head) ``{ ` `Node *fast = head,*slow = head; ` `while` `(fast->next && fast->next->next) ` `{ ` `fast = fast->next->next; ` `slow = slow->next; ` `} ` `Node *temp = slow->next; ` `slow->next = NULL; ` `return` `temp; ``} ``// Driver program ``int` `main(` `void` `) ``{ ` `Node *head = NULL; ` `insert(&head, 5); ` `insert(&head, 20); ` `insert(&head, 4); ` `insert(&head, 3); ` `insert(&head, 30); ` `insert(&head, 10);` [HTG5 08] `head = mergeSort(head); ` `cout <<` `"Linked List after sorting\n"` `; ` `print(head); ` `return` `0; ``}` |

*chevron_right**filter_none*