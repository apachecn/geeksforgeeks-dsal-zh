# 反转给定链接列表

的前K个元素

给定指向链表的头节点和数字K的指针，任务是反转链表的前K个节点。 我们需要通过更改节点之间的链接来反转列表。
也检查[链表的反向](https://www.geeksforgeeks.org/reverse-a-linked-list/)

**示例：**

```
Input : 1->2->3->4->5->6->7->8->9->10->NULL
        k = 3
Output :3->2->1->4->5->6->7->8->9->10->NULL

Input :10->18->20->25->35->NULL
       k = 2
Output :18->10->20->25->35->NULL

```

方法说明：
假设链接列表为1- > 2- > 3- > 4- > 5- > NULL，并且k = 3

1）遍历链表直到第K点。
2）从第k个点将链接列表分成两部分。 分区后的链表看起来像1- > 2- > 3- > NULL & 4- > 5- > NULL
3）[反转 链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)保留第二部分，即保留为3- > 2- > 1- > NULL和4- > 5- > NULL
4）连接两个部分 链表，我们得到3- > 2- > 1- > 4- > 5- > NULL

该算法如何工作的图形表示

![](img/246bed7066049d1a1b9ea6d29c1a35b1.png)

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program for reversal of first k elements``// of given linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to reverse first k elements of linked list */``static` `void` `reverseKNodes(` `struct` `Node** head_ref,` `int` `k)``{` `// traverse the linked list until break` `// point not meet` `struct` `Node* temp = *head_ref;` `int` `count = 1;` `while` `(count < k) {` `temp = temp->next;` `count++;` `}` `// backup the joint point` `struct` `Node* joint_point = temp->next;` `temp->next = NULL;` `// break the list` `// reverse the list till break point` `struct` `Node* prev = NULL;` `struct` `Node* current = *head_ref;` `struct` `Node* next;` `while` `(current != NULL) {` `next = current->next;`​​ `current->next = prev;` `prev = current;` `current = next;` `}` `// join both parts of the linked list` `// traverse the list until NULL is not` `// found` `*head_ref = prev;` `current = *head_ref;` `while` `(current->next != NULL)` `current = current->next;` `// joint both part of the list` `current->next = joint_point;``}` [HTG3 04]`/* Function to push a node */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* Function to print linked list */``void` `printList(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `printf` `(` `"%d "` `, temp->data);` `temp = temp->next;` `}``}``/* Driver program to test above function*/`HTG156] `main()``{` `// Create a linked list 1->2->3->4->5` `struct` `Node* head = NULL;` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);` `// k should be less than the` `// numbers of nodes` `int` `k = 3;` `cout <<` `"\nGiven list\n"` `;` `printList(head);` `reverseKNodes(&head, k);` `cout <<` `"\nModified list\n"` `;` `printList(head);` [ `return` `0;``}` |

*chevron_right**filter_none*