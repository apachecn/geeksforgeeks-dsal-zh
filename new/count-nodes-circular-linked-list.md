# 循环链接列表

中的节点计数

给定一个循环链表，计算其中的节点数。 例如，以下列表的输出为5。

![](img/703b24f6bea34bab0d870162e6b29efb.png "cll")

我们使用[循环链表|中的概念。 集合2（Traversal）](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)。 在遍历时，我们会跟踪节点数。

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C program to count number of nodes in``// a circular linked list.``#include <stdio.h>``#include <stdlib.h>`的`/* structure for a node */``struct` `Node {` `int` `data;` `struct` `Node* next;`[`};``/* Function to insert a node at the beginning` `of a Circular linked list */``Node** head_ref,` `int` `data)``{` `struct` `Node* ptr1 = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `struct` `Node* temp = *head_ref;` `ptr1->data = data;` `ptr1->next = *head_ref;` `/* If the linked list is not NULL then set` `the next of last node */` `if` `(*head_ref != NULL) {` `while` [HTG5 4] `temp = temp->next;` `temp->next = ptr1;` `}` `else` `ptr1->next = ptr1;` `/*For the first node */` `*head_ref = ptr1;``}``/* Function to print nodes in a given Circular` `linked list */``int` `countNodes(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `int` `result = 0;` `if` `(head != NULL) {` `do` `{` `temp = temp->next;` `result++;` `}` `while` `(temp != head);` `}` [ `return` `result;``}``/* Driver program to test above functions */``int` `main()``{` `/* Initialize lists as empty */` `struct` `Node* head = NULL;` `push(&head, 12);` `push(&head, 56);` `push(&head, 2);` `push(&head, 11);` `printf` `(` `"%d"` `, countNodes(head));` `return` `0;``}` |

*chevron_right**filter_none*