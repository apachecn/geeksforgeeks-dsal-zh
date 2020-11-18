# 循环链接列表| 第2组（Traversal）

我们在上一则关于循环链接列表的文章中讨论了[循环链接列表的介绍和应用，](http://quiz.geeksforgeeks.org/circular-linked-list/ "Permanent link to Circular Linked List | Set 1 (Introduction and Applications)") 。 在这篇文章中，讨论了遍历操作。

![](img/ff7f30aebf5dc865587c7829dcf4233c.png "cll")

在常规的链表中，我们从头节点遍历该列表，并在到达NULL时停止遍历。 在循环链表中，当再次到达第一个节点时，我们将停止遍历。 以下是用于链表遍历的C代码。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* Function to traverse a given Circular linked list and print nodes */``void` `printList(` `struct` `Node *first)``{` `struct` `Node *temp = first; ` `// If linked list is not empty` `if` `(first != NULL) ` `{` `// Keep printing nodes till we reach the first node again` `do` `{` `printf` `(` `"%d "` `, temp->data);` `temp = temp->next;` `}` `while` `(temp != first);` `}``}` |

*chevron_right**filter_none*

**演示遍历的完整程序。** 以下是演示遍历循环链表的完整程序。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to implement ``// the above approach ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* structure for a node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``/* Function to insert a node at the beginning ``of a Circular linked list */``void` `push(Node **head_ref,` `int` `data) ``{ ` `Node *ptr1 =` `new` `Node();` `Node *temp = *head_ref; ` `ptr1->data = data; ` `ptr1->next = *head_ref; `的 `/* If linked list is not NULL then ` `set the next of last node */` `if` `(*head_ref != NULL) ` `{ ` `while` `(temp->next != *head_ref) ` `temp = temp->next; ` `temp->next = ptr1; ` `} ` `else` `ptr1->next = ptr1;` `/*For the first node */` `*head_ref = ptr1; ``} ``/* Function to print nodes in ``a given Circular linked list */``void` `printList(Node *head) ``{ ` `Node *temp = head; ` `if` `(head != NULL) ` `{ ` `do` `{ ` `cout << temp->data <<` `" "` `; ` `temp = temp->next; ` `} ` `while` `(temp != head); ` `} ``} ``/* Driver program to test above functions */``int` `main() ``{ ` `/* Initialize lists as empty */` `Node *head = NULL; ` `/* Created linked list will be 11->2->56->12 */` `push(&head, 12); ` `push(&head, 56); ` `push(&head, 2); ` `push(&head, 11); ` `cout <<` `"Contents of Circular Linked List\n "` `; `]  `printList(head); ` [ `return` `0; ``} `​​  [`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*