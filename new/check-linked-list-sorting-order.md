# 检查链接列表是否已排序（迭代和递归）

给定一个链表，任务是检查链表是否以降序排序？

**示例：**

```
Input  : 8 -> 7 -> 5 -> 2 -> 1
Output : Yes
Explanation :
In given linked list, starting from head,
8 > 7 > 5 > 2 > 1\. So, it is sorted in reverse order

Input  : 24 -> 12 -> 9 -> 11 -> 8 -> 2
Output : No

```

**迭代方法：**从头到尾遍历链表。 对于每个新遇到的元素，检查**节点->数据>节点->接下来->数据**。 如果为True，则对每个节点执行相同操作，否则返回0并打印“ No”。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to check Linked List is sorted``// in descending order or not``#include <bits/stdc++.h>``using` `namespace` `std;``/* Linked list node */``struct` `Node``{` `int` `data;` `struct` `Node* next;``};``// function to Check Linked List is ``// sorted in descending order or not``bool` `isSortedDesc(` `struct` `Node *head)``{ ` `if` `(head == NULL)` `return` `true` `;` `// Traverse the list till last node and return` `// false if a node is smaller than or equal` `// its next.` `for` `(Node *t=head; t->next != NULL; t=t->next)` `if` `(t->data <= t->next->data)` `return` `false` `;`[H TG50] `return` `true` `;``}``Node *newNode(` `int` `data)``{` `Node *temp =` `new` `Node;` `temp->next = NULL;` `temp->data = data;``}``// Driver program to test above``int` `main()``{` `struct` `Node *head = newNode(7);` `head->next = newNode(5);` `head->next->next = newNode(4);` `head->next->next->next = newNode(3);` `isSortedDesc(head) ? cout <<` `"Yes"` `: ` `cout <<` `"No"` `;` ] `return` `0;``}` |

*chevron_right**filter_none*