# 排序的链表包含从1到N的值

给定大小为N的链接列表，其中包含从1到N的所有值。任务是按递增顺序对链接列表进行排序。

**示例：**

```
Input : List = 3 -> 5 -> 4 -> 6 -> 1 -> 2
Output : 1 -> 2 -> 3 -> 4 -> 5 -> 6

Input : List = 5 -> 4 -> 3 -> 2 -> 1
Output : 1 -> 2 -> 3 -> 4 -> 5

```

**天真的方法**：最简单的方法是使用任何类型的[排序方法](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对该链表进行排序。 最少需要O（N * logN）个时间。

**有效方法**：一种有效方法是观察链表包含总共N个元素，并且元素从1到N进行编号。遍历链表并将每个元素替换为其位置。

以下是此方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to sort linked list containing``// values from 1 to N``#include <iostream>``using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to sort linked list``bool` `sortList(` `struct` `Node* head)``{` `int` `startVal = 1;` `while` ] `(head != NULL) {` `head->data = startVal;` `startVal++;` `head = head->next;` `}``}``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// This function prints contents of``// linked list starting from``// the given node``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;`的[ `node = node->next;` `}``}` [`// Driver program to test above function``int` `main()``{` `struct` `Node* start = NULL;` `/* The constructed linked list is: ` `3->5->4->6->1->2 */` `push(&start, 2);` `push(&start, 1);` `push(&start, 6);`​​ `push(&start, 4);` `push(&start, 5);` `push(&start, 3);` `sortList(start);` `printList(start);` `return` `0;``}` |

*chevron_right**filter_none*