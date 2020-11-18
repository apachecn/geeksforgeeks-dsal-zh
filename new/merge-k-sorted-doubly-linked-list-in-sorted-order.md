# 以排序顺序合并K个排序的双链表

给定 **K** 排序的双链表。 任务是将所有排序的双链表合并到单个排序的双链表中，这意味着必须对最终列表进行排序。

**示例：**

> **输入：**
> 列表1：2 <-> 7 <-> 8 <-> 12 <-> 15 < ->空
> 清单2：4 <-> 9 <-> 10 <->空
> 清单3：5 <-> 9 <-> 11 <-> 16 <->空
> **输出：** 2 4 5 7 8 9 9 10 11 12 15 16
> 
> **输入：**
> 列表1：4 <-> 7 <-> 8 <-> 10 <-> NULL
> 清单2：4 <-> 19 <-> 20 <-> 23 <-> 27 <->空
> 清单3： 3 <-> 9 <-> 12 <-> 20 <-> NULL
> 清单4：1 <-> 19 <-> 22 <->空
> 清单5：7 <-> 16 <-> 20 <-> 21 <-[ > NULL
> **输出：**
> 1 3 4 4 7 7 8 8 10 10 16 16 19 19 20 20 20 21 22 23 27

**先决条件：** [参考算法](https://en.wikipedia.org/wiki/Merge_algorithm)
**方法：**

1.  首先按排序顺序合并两个双向链表
2.  然后按排序顺序将此列表与另一个列表合并
3.  做同样的事情，直到所有列表都没有合并
4.  请记住，您必须一次合并两个列表，然后合并的列表将被新合并

**算法：**

```
function merge(A, B) is
    inputs A, B : list
    returns list

    C := new empty list
    while A is not empty and B is not empty do
        if head(A) < head(B) then
            append head(A) to C
            drop the head of A
        else
            append head(B) to C
            drop the head of B

    // By now, either A or B is empty 
    // It remains to empty the other input list
    while A is not empty do
        append head(A) to C
        drop the head of A
    while B is not empty do
        append head(B) to C
        drop the head of B

    return C

```

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to merge K sorted doubly``// linked list in sorted order``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A linked list node``struct` `Node {` `int` `data;` `Node* next;` `Node* prev;``};``// Given a reference (pointer to pointer) to the head``// Of a DLL and an int, appends a new node at the end``void` `append(` `struct` `Node** head_ref,` `int` `new_data)``{` `// Allocate node` `struct` `Node* new_node` `= (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `struct` `Node* last = *head_ref;` `// Put in the data` `new_node->data = new_data;`[H `// This new node is going to be the last` `// node, so make next of it as NULL` `new_node->next = NULL;` `// If the Linked List is empty, then make` `// the new node as head */` `if` `(*head_ref == NULL) {` `new_node->prev = NULL;` `*head_ref = new_node;` `return` `;` `}` `// Else traverse till the last node` `while` `(last->next != NULL)` `last = last->next;` `// Change the next of last node` `last->next = new_node;` `// Make last node as previous of new node` `new_node->prev = last;` ] `return` `;``}`[ `// Function to print the list` [HTG4 56]`void` `printList(Node* node)``{` `Node* last;` `// Run while loop unless node becomes null` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `last = node;` `node = node->next;` `}``}``// Function to merge two``// sorted doubly linked lists``Node* mergeList(Node* p, Node* q)``{` `Node* s = NULL;` `// If any of the list is empty` `if` `(p == NULL &#124;&#124; q == NULL) {` `return` `(p == NULL ? q : p);` `}` `// Comparison the data of two linked list` `if` `(p->data < q->data) {` `p->prev = s;` `s = p;` `p = p->next;` `}` `else` `{` `q->prev = s;` `s = q;` `q = q->next;` `}` `// Store head pointer before merge the list` `Node* head = s;` `while` `(p != NULL && q != NULL) {` `if` `(p->data < q->data) {` `// Changing of pointer between` `// Two list for merging` `s->next = p;` `p->prev = s;` `s = s->next;` `p = p->next;` `}` `else` `{`的 `// Changing of pointer between` `// Two list for merging` `s->next = q;` `q->prev = s;`]  `s = s->next;` `q = q->next;` `}` `}`[ `// Condition to check if any anyone list not end` `if` `(p == NULL) {` `s->next = q;` `q->prev = s;` `}` `if` `(q == NULL) {` `s->next = p;` `p->prev = s;` `}` `// Return head pointer of merged list` `return` [ `head;``}``// Function to merge all sorted linked``// list in sorted order``Node* mergeAllList(Node* head[],` `int` `k)``{` `Node* finalList = NULL;` `for` `(` `int` `i = 0; i < k; i++) {` `// Function call to merge two sorted` `// doubly linked list at a time` `finalList = mergeList(finalList, head[i]);` `}` `// Return final sorted doubly linked list` `return` `finalList;``}`​​`// Driver code``int` `main()``{` `int` `k = 3;` `Node* head[k];` `// Loop to initialize all the lists to empty` `for` `(` `int` `i = 0; i < k; i++) {` `head[i] = NULL;` `}` [HT G652] `// Create first doubly linked List` `// List1 -> 1 <=> 5 <=> 9` `append(&head[0], 1);` `append(&head[0], 5);` `append(&head[0], 9);`]  `// Create second doubly linked List` `// List2 -> 2 <=> 3 <=> 7 <=> 12` `append(&head[1], 2);` `append(&head[1], 3);` `append(&head[1], 7);` `append(&head[1], 12);` `// Create third doubly linked List` `// List3 -> 8 <=> 11 <=> 13 <=> 18` `append(&head[2], 8);` `append(&head[2], 11);` `append(&head[2], 13);`[HTG33 4] `append(&head[2], 18);` `// Function call to merge all sorted` `// doubly linked lists in sorted order` `Node* finalList = mergeAllList(head, k);` `// Print final sorted list` `printList(finalList);` ] [ `return` `0;``}` |

*chevron_right**filter_none*