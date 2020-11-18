# 从双向链表中删除所有小于给定值的节点

给定一个包含N个节点和数字K的双向链表，任务是从列表中删除所有小于给定值K的节点。

**示例：**

```
Input: 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
       K = 10
Output: 15 <=> 16 <=> 10 <=> 17

Input: 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
       K = 4 
Output: 5 <=> 6 <=> 8 <=> 4 <=> 9

```

**方法：**遍历双向链接列表的节点，并获得数据值小于 **K** 的节点的指针。 请参阅[从双链表](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)中删除节点的文章以删除节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to delete all``// the nodes from the doubly``// linked list that are smaller than``// the specified value K``#include <bits/stdc++.h>``using` `namespace` `std;``// Node of the doubly linked list``struct` `Node {` `int` `data;` `Node *prev, *next;``};`的`// function to insert a node at the beginning``// of the Doubly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;`​​ `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// change prev of head node to new node` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node` `(*head_ref) = new_node;``}``// function to delete a node in a Doubly Linked List.``// head_ref --> pointer to head node pointer.``// del  -->  pointer to node to be deleted``void` `deleteNode(Node** head_ref, Node* del)``{` `// base case` `if` `(*head_ref == NULL &#124;&#124; del == NULL)` `return` `;` `// If node to be deleted is head node` `if` `(*head_ref == del)` `*head_ref = del->next;` `// Change next only if node to be` `// deleted is NOT the last node` `if` `(del->next != NULL)` `del->next->prev = del->prev;` `// Change prev only if node to be` ] `// deleted is NOT the first node` `if` `(del->prev != NULL)` `del->prev->next = del->next;` `// Finally, free the memory occupied by del` `free` `(del);` `return` `;``}``// function to delete all the nodes``// from the doubly linked``// list that are smaller than the``// specified value K``void` `deletesmallerNodes(Node** head_ref,` `int` `K)``{` `Node* ptr = *head_ref;` `Node* next;` `while` `(ptr != NULL) {` `// if true, delete node 'ptr'` `if` `(ptr->data < K)` `deleteNode(head_ref, ptr);` `ptr = next;` `}``}``// function to print nodes in a``// given doubly linked list``void` `printList(Node* head)``{` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}`] `// Driver program to test above``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the doubly linked list` `// 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17`6] `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 9);` `push(&head, 10);` `push(&head, 16);` `push(&head, 15);` `int` `K = 10;` `cout <<` `"Original List: "` `;` `printList(head);` `deletesmallerNodes(&head, K);` `cout <<` `"\nModified List: "` `;` `printList(head);``}` |

*chevron_right**filter_none*