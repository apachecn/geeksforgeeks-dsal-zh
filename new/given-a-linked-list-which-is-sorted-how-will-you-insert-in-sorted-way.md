# 给定一个已排序的链表，您将如何以已排序的方式插入

给定排序的链表和要插入的值，编写一个函数以排序的方式插入值。

初始链接列表
![SortedLinked List](img/177b10005e6b234f6f3bf2456c71f8cd.png "SortedLinked List")

插入9
![UpdatedSortedLinked List](img/c431502d296d8d30fff5dfb1be090fc2.png "UpdatedSortedLinked List")后的链接列表

**算法：**
让输入的链表按升序排序。

```
1) If Linked list is empty then make the node as
   head and return it.
2) If the value of the node to be inserted is smaller 
   than the value of the head node, then insert the node 
at the start and make it head.
3) In a loop, find the appropriate node after 
   which the input node (let 9) is to be inserted. 
   To find the appropriate node start from the head, 
   keep moving until you reach a node GN (10 in
   the below diagram) who's value is greater than 
   the input node. The node just before GN is the
appropriate node (7).
4) Insert the node (9) after the appropriate node
   (7) found in step 3.

```

**实施：**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* Program to insert in a sorted list */``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* function to insert a new_node ``in a list. Note that this ``function expects a pointer to ``head_ref as this can modify the ``head of the input linked list ``(similar to push())*/``void` `sortedInsert(Node** head_ref,` `Node* new_node)``{` `Node* current;` `/* Special case for the head end */` `if` `(*head_ref == NULL` `&#124;&#124; (*head_ref)->data` `>= new_node->data) {` `new_node->next = *head_ref;` `*head_ref = new_node;` `}` `else` `{` `/* Locate the node before the` `point of insertion */` `current = *head_ref;` `while` `(current->next != NULL ``&& current->next->data ``< new_node->data) {` `current = current->next;` `}` `new_node->next = current->next;` `current->next = new_node;` `}``}``/* BELOW FUNCTIONS ARE JUST ``UTILITY TO TEST sortedInsert */``/* A utility function to ``create a new node */``Node* newNode(` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */`​​  `new_node->data = new_data;` [HT G93] `return` `new_node;``}``/* Function to print linked list */``void` `printList(Node* head)``{` `Node* temp = head;` `while` `(temp != NULL) {` `cout << temp->data <<` `" "` `;` `temp = temp->next;` `}``}``/* Driver program to test count function*/``int` `main()``{` `/* Start with the empty list */` `Node* head = NULL;` `Node* new_node = newNode(5);` `sortedInsert(&head, new_node);` `new_node = newNode(10);` `sortedInsert(&head, new_node);` `new_node = newNode(7);` `sortedInsert(&head, new_node);` `new_node = newNode(3);` `sortedInsert(&head, new_node);` `new_node = newNode(1);` `sortedInsert(&head, new_node);` `new_node = newNode(9);` `sortedInsert(&head, new_node);` `cout <<` `"Created Linked List\n"` `;` `printList(head);` `return` `0;``}``// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*