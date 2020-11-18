# 在链接列表中的第k个位置循环

给定一个链表和位置k。 在第k个位置循环

**示例：**

```
Input : Given linked list

Output : Modified linked list

```

**算法**
1）遍历第一个链表直到第k个点
2）备份第k个节点
3）遍历链表直到最后
4）将最后一个节点附加到第k个节点

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program for making loop at k-th index``// of given linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to make loop at k-th elements of``linked list */``void` `makeloop(` `struct` `Node** head_ref,` `int` `k)``{` `// traverse the linked list until loop` `// point not found` `struct` `Node* temp = *head_ref;` `int` `count = 1;` `while` `(count < k) {` `temp = temp->next;` `count++;` `}` `// backup the joint point ` `struct` `Node* joint_point = temp; ` `// traverse remaining nodes` `while` `(temp->next != NULL) `] `temp = temp->next;`。 `// joint the last node to k-th element` `temp->next = joint_point;``}`​​ [`/* Function to push a node */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}`[`/* Function to print linked list */``void` `printList(` `struct` `Node* head,` `int` `total_nodes)``{` [H TG105] `Node* curr = head;` `int` `count = 0;` `while` `(count < total_nodes) {` `count++;` `cout << curr->data <<` `" "` `;` `curr = curr->next;` `}``}` [`int` `countNodes(Node *ptr)``{` `int` `count = 0;` `while` `(ptr != NULL)` `{` `ptr = ptr->next;` `count++;` `}` `return` `count;``}``/* Driver program to test above function*/``int` `main()``{` `// Create a linked list 1->2->3->4->5->6->7` `struct` `Node* head = NULL;` `push(&head, 7);` `push(&head, 6);` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);`的 `// k should be less than the` `// numbers of nodes` `int` `k = 4;` `int` `total_nodes = countNodes(head);` `cout <<` `"\nGiven list\n"` `;` `printList(head, total_nodes);` `makeloop(&head, k);` `cout <<` `"\nModified list\n"` `;` `printList(head, total_nodes);` `return` `0;``}` |

*chevron_right**filter_none*