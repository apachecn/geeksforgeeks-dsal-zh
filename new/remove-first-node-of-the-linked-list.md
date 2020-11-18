# 删除链接列表

的第一个节点

给定一个链表，任务是删除链表的第一个节点并更新链表的头指针。

例子：

```
Input : 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Output : 2 -> 3 -> 4 -> 5 -> NULL

Input : 2 -> 4 -> 6 -> 8 -> 33 -> 67 -> NULL
Output : 4 -> 6 -> 8 -> 33 -> 67 -> NULL

```

要删除第一个节点，我们需要将第二个节点设为头，并删除分配给第一个节点的内存。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to remove first node of``// linked list.``#include <iostream>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to remove the first node ` `of the linked list */``Node* removeFirstNode(` `struct` `Node* head)``{` `if` `(head == NULL)` `return` `NULL;` `// Move the head pointer to the next node` `Node* temp = head;` `head = head->next;`的 `delete` `temp;` `return` `head;``}`[HTG4 7]的`// Function to push node at head``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Driver code``int` `main()``{` `/* Start with the empty list */` `Node* head = NULL;` `/* Use push() function to construct  ` `the below list 8 -> 23 -> 11 -> 29 -> 12 */` `push(&head, 12);` `push(&head, 29);` `push(&head, 11);` `push(&head, 23);` `push(&head, 8);` `head = removeFirstNode(head);` `for` `(Node* temp = head; temp != NULL; temp = temp->next)` `cout << temp->data <<` `" "` `;` `return` `0;``}` |

*chevron_right**filter_none*