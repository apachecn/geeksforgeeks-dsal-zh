# 在两个双链表

中查找公共节点的数量

给定两个双链表。 任务是在两个双链表中找到公共节点的总数。

**示例：**

```
Input : 
list 1 = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17 
list 2 = 15 <=> 16 <=> 45 <=> 9 <=> 6
Output : Number of common nodes: 4

Input :
list 1 = 18 <=> 30 <=> 92 <=> 46 <=> 72 <=> 1
list 2 = 12 <=> 32 <=> 45 <=> 9 <=> 6 <=> 30
Output : Number of common nodes: 1

```

**方法：**使用两个嵌套循环遍历两个列表，直到列表的末尾。 对于列表1中的每个节点，检查它是否与列表2中的任何节点匹配。如果是，则增加公共节点的数量。 最后，打印计数。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to count``// common element in given two``// doubly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Node of the doubly linked list``struct` `Node {` `int` `data;` `Node *prev, *next;``};``// Function to insert a node at the beginning``// of the Doubly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// change prev of head node to new node` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node` `(*head_ref) = new_node;``}`​​`// Count common nodes in both list1 and list 2``int` `countCommonNodes(Node** head_ref, Node** head)``{` `// head for list 1` `Node* ptr = *head_ref;` `// head for list 2` `Node* ptr1 = *head;` `// initialize count = 0` `int` `count = 0;` `// traverse list 1 till the end` `while` `(ptr != NULL) {` `// traverse list 2 till the end` `while` `(ptr1 != NULL) {` `// if node value is equal then` `// increment count` `if` `(ptr->data == ptr1->data) {` `count++;` `break` `;` `}` `// increment pointer list 2` `ptr1 = ptr1->next;` `}` `// again list 2 start with starting point` `ptr1 = *head;` `// increment pointer list 1` `ptr = ptr->next;` `}` `// return count of common nodes` `return` `count;``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `Node* head1 = NULL;` `// create the doubly linked list 1` `// 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 9);` `push(&head, 10);` `push(&head, 16);` `push(&head, 15);` `// create the doubly linked list 2` `// 15 <-> 16 <-> 45 <-> 9 <-> 6` `push(&head1, 6);` `push(&head1, 9);` `push(&head1, 45);` `push(&head1, 16);` `push(&head1, 15);` `cout <<` `"Number of common nodes:"` `<< countCommonNodes(&head, &head1);`[ `return` `0;``}` |

*chevron_right**filter_none*