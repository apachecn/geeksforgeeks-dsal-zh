# 使用双向链表

的优先级队列

给定具有优先级的节点，请使用双向链表实现优先级队列。

**前提条件：** [优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)

**Operations on Priority Queue :**

*   push（）：此函数用于将新数据插入队列。
*   pop（）：此函数从队列中删除优先级最低的元素。
*   peek（）/ top（）：此函数用于获取队列中优先级最低的元素，而不将其从队列中删除。

**方法：**
1.创建一个双向链接列表，其中包含字段info（保存节点的信息），优先级（保存节点的优先级），prev（指向上一个节点），next（ 指向下一个节点）。
2.在节点中插入元素和优先级。
3.按优先级的升序排列节点。

以下是上述步骤的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP code to implement priority``// queue using doubly linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Linked List Node``struct` `Node {` `int` `info;` `int` `priority;` `struct` `Node *prev, *next;``};``// Function to insert a new Node``void` `push(Node** fr, Node** rr,` `int` `n,` `int` `p)``{` `Node* news = (Node*)` `malloc` `(` `sizeof` `(Node));` `news->info = n;` `news->priority = p;` `// If linked list is empty` `if` `(*fr == NULL) {` `*fr = news;` `*rr = news;` `news->next = NULL;` `}` `else` `{` `// If p is less than or equal front` `// node's priority, then insert at` `// the front.` `if` `(p <= (*fr)->priority) {` `news->next = *fr;` `(*fr)->prev = news->next;` `*fr = news;` `}` `// If p is more rear node's priority, ` `// then insert after the rear.` `else` `if` `(p > (*rr)->priority) {`​​ `news->next = NULL;` `(*rr)->next = news;` `news->prev = (*rr)->next;` `*rr = news;` `}` `// Handle other cases` `else` `{` `// Find position where we need to` `// insert.`[ `Node* start = (*fr)->next;` `while` `(start->priority > p) ` `start = start->next;            ` `(start->prev)->next = news;` `news->next = start->prev;` `news->prev = (start->prev)->next;` `start->prev = news->next;` `}` `}``}``// Return the value at rear``int` `peek(Node *fr)``{` `return` `fr->info;``}``bool` `isEmpty(Node *fr)``{` `return` `(fr == NULL);``}` [`// Removes the element with the``// least priority value form the list``int` `pop(Node** fr, Node** rr)``{` `Node* temp = *fr;` `int` `res = temp->info;` `(*fr) = (*fr)->next;` `free` `(temp);` `if` `(*fr == NULL) ` `*rr = NULL;` `return` `res;``}` [`// Driver code``int` `main()``{` `Node *front = NULL, *rear = NULL;` `push(&front, &rear, 2, 3);` `push(&front, &rear, 3, 4);` `push(&front, &rear, 4, 5);` `push(&front, &rear, 5, 6);` `push(&front, &rear, 6, 7);` `push(&front, &rear, 1, 2);` `cout << pop(&front, &rear) << endl;` `cout << peek(front);` [ `return` `0;``}` |

*chevron_right**filter_none*