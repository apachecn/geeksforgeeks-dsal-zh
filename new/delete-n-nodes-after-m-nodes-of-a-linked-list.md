# 删除链表

的M个节点后的N个节点

给定一个链表和两个整数M和N。遍历链表，以便保留M个节点，然后删除下N个节点，继续相同操作，直到链表结束。

难度等级：菜鸟

例子：

```
Input:
M = 2, N = 2
Linked List: 1->2->3->4->5->6->7->8
Output:
Linked List: 1->2->5->6

Input:
M = 3, N = 2
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->2->3->6->7->8

Input:
M = 1, N = 1
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->3->5->7->9
```

问题的主要部分是维护节点之间的正确链接，确保处理所有极端情况。 以下是函数skipMdeleteN（）的C实现，该函数跳过M个节点并删除N个节点，直到列表结尾。 假定M不能为0。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to delete N nodes``// after M nodes of a linked list ``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A linked list node ``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``/* Function to insert a node at the beginning */``void` `push(Node ** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` HTG253] `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``/* Function to print linked list */`​​ `void` `printList(Node *head) ``{ ` `Node *temp = head; ` `while` `(temp != NULL) ` `{ ` `cout<<temp->data<<` `" "` `; ` `temp = temp->next; ` `} ` `cout<<endl; ``} ``// Function to skip M nodes and then``// delete N nodes of the linked list. ``void` `skipMdeleteN(Node *head,` `int` `M,` `int` `N)` ]`{ ` `Node *curr = head, *t; ` `int` `count; ` `// The main loop that traverses` `// through the whole list ` `while` `(curr) ` `{ `[H TG97] `// Skip M nodes ` `for` `(count = 1; count < M && ` `curr!= NULL; count++) ` `curr = curr->next; ` `// If we reached end of list, then return ` `if` `(curr == NULL) ` `return` `; ` [ `// Start from next node and delete N nodes ` `t = curr->next; ` `for` `(count = 1; count<=N && t!= NULL; count++) ` `{ ` `Node *temp = t; ` `t = t->next; ` `free` `(temp); ` `} ` `// Link the previous list with remaining nodes ` `curr->next = t; `] `// Set current pointer for next iteration ` `curr = t; ` `} ``} ``// Driver code ``int` `main() ``{ ` `/* Create following linked list ` `1->2->3->4->5->6->7->8->9->10 */` `Node* head = NULL; ` `int` `M=2, N=3; ` `push(&head, 10); ` `push(&head, 9); ` `push(&head, 8); ` `push(&head, 7); ` `push(&head, 6); ` `push(&head, 5); ` `push(&head, 4); ` `push(&head, 3); ` `push(&head, 2); ` `push(&head, 1); ` `cout <<` `"M = "` `<< M<<` `" N = "` `<< N <<` `"\nGiven Linked list is :\n"` `;` ] `printList(head); ` `skipMdeleteN(head, M, N); `[HT G195] `cout<<` `"\nLinked list after deletion is :\n"` `; ` `printList(head); ` `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*