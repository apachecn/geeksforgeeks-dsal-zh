# 两个链表的并集和交点

给定两个链接列表，创建包含给定列表中元素的并集和交集的并集和交集列表。 输出列表中元素的顺序无关紧要。

**示例：**

```
Input:
   List1: 10->15->4->20
   lsit2:  8->4->2->10
Output:
   Intersection List: 4->10
   Union List: 2->8->20->4->15->10

```

**方法1（简单）**
以下是分别获取联合和相交列表的简单算法。

*交叉点（列表1，列表2）*
将结果列表初始化为NULL。 遍历list1并在list2中查找其每个元素，如果list2中存在该元素，则将其添加到结果中。

*联合（列表1，列表2）：*
将结果列表初始化为NULL。 遍历list1并将其所有元素添加到结果中。
遍历列表2。 如果结果中已经存在list2元素，则不要将其插入到result中，否则插入。

此方法假定给定列表中没有重复项。

感谢Shekhu建议这种方法。 以下是此方法的C和Java实现。

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C/C++ program to find union``// and intersection of two unsorted``// linked lists``#include <stdbool.h>``#include <stdio.h>``#include <stdlib.h>``/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* A utility function to insert a ` `node at the beginning ofa linked list*/``void` `push(` `struct` `Node** head_ref,` `int` `new_data);``/* A utility function to check if ` `given data is present in a list */``bool` `isPresent(` `struct` `Node* head,` `int` `data);``/* Function to get union of two ` `linked lists head1 and head2 */``struct` `Node* getUnion(` `struct` `Node* head1,` `struct` `Node* head2)``{` `struct` `Node* result = NULL;` `struct` `Node *t1 = head1, *t2 = head2;` `// Insert all elements of` `// list1 to the result list` `while` `(t1 != NULL) {` `push(&result, t1->data);` `t1 = t1->next;` `}` `// Insert those elements of list2` `// which are not present in result list` `while` `(t2 != NULL) {` `if` `(!isPresent(result, t2->data))` `push(&result, t2->data);` `t2 = t2->next;` `}` `return` `result;``}`[`/* Function to get intersection of ` `two linked lists head1 and head2 */``struct` `Node* getIntersection(` `struct` `Node* head1,` `struct` `Node* head2)``{` `struct` `Node* result = NULL;` `struct` `Node* t1 = head1;` `// Traverse list1 and search each element of it in` `// list2\. If the element is present in list 2, then` `// insert the element to result` `while` `(t1 != NULL) {` `if` `(isPresent(head2, t1->data))` `push(&result, t1->data);` `t1 = t1->next;` `}` `return` `result;``}``/* A utility function to insert a ` `node at the beginning of a linked list*/``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node` `= (` [HTG15 1] `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``/* A utility function to print a linked list*/``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}`] `}``/* A utility function that returns true if data is ` `present in linked list else return false */`[H TG200] `isPresent(` `struct` `Node* head,` `int` `data)``{` `struct` `Node* t = head;` `while` `(t != NULL) {` `if` `(t->data == data)` `return` `1;` `t = t->next;` `}` `return` `0;``}``/* Driver program to test above function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head1 = NULL;` `struct` `Node* head2 = NULL;` `struct` `Node* intersecn = NULL;` `struct` `Node* unin = NULL;` `/*create a linked lits 10->15->5->20 */` `push(&head1, 20);` [HTG2 52] `push(&head1, 15);` `push(&head1, 10);` `/*create a linked lits 8->4->2->10 */` `push(&head2, 10);` `push(&head2, 2);` `push(&head2, 4);` `push(&head2, 8);`]  `intersecn = getIntersection(head1, head2);` ​​ `unin = getUnion(head1, head2);` `printf` `(` `"\n First list is \n"` `);` `printList(head1);` `printf` `(` `"\n Second list is \n"` `);` `printList(head2);` `printf` `(` `"\n Intersection list is \n"` `);` ] `printList(intersecn);` `printf` `(` `"\n Union list is \n"` `);`[HTG30 3] `printList(unin);` `return` `0;``}` |

*chevron_right**filter_none*