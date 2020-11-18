# 循环链表

的节点总和

给定一个[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)。 任务是找到给定链表的节点总数。

![](img/462afffb8d425a09fa443768f1676313.png)

对于上述通告列表，sum = 2 + 5 + 7 + 8 + 10 = 32

**示例：**

```
Input: 11->2->56->12
Output: Sum of Circular linked list is = 81

Input: 2-> 5 -> 7 -> 8 -> 10
Output: Sum of Circular linked list is = 32   

```

**方法：**

1.  使用链接列表的开头和0的sum变量初始化指针temp。
2.  Start traversing the linked list using a loop until all the nodes get traversed.
    *   将当前节点的值添加到总和，即总和+ = temp->数据。
    *   递增指向链接列表的下一个节点的指针，即temp = temp-> next。
3.  返回总和。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to find the sum of all nodes``// of a Circular linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Structure for a node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to insert a node at the beginning``// of a Circular linked list``void` `push(` `struct` `Node** head_ref,` `int` `data)``{` `struct` `Node* ptr1 = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `struct` `Node* temp = *head_ref;` `ptr1->data = data;` `ptr1->next = *head_ref;` `// If linked list is not NULL then` `// set the next of last node` `if` `(*head_ref != NULL) {` [HT G186] `while` `(temp->next != *head_ref)` `temp = temp->next;` `temp->next = ptr1;` `}` `else` `ptr1->next = ptr1;` `// For the first node` `*head_ref = ptr1;``}``// Function to find sum of the given``// Circular linked list``int` `sumOfList(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `int` `sum = 0;` `if` `(head != NULL) {` `do` `{` `temp = temp->next;` `sum += temp->data;` `}` `while` `(temp != head);` `}` `return` `sum;`[H TG235] `}``// Driver code``int` `main()``{` `// Initialize lists as empty` `struct` `Node* head = NULL;` `// Created linked list will be 11->2->56->12` `push(&head, 12);` `push(&head, 56);` `push(&head, 2);` `push(&head, 11);` `cout <<` `"Sum of Circular linked list is = "` `<< sumOfList(head);` `return` `0;``}`​​ |

*chevron_right**filter_none*