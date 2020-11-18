# 已对绝对值进行排序的链接列表

给定一个基于绝对值排序的链表。 根据实际值对列表进行排序。

**示例：**

```
Input :  1 -> -10 
output: -10 -> 1

Input : 1 -> -2 -> -3 -> 4 -> -5 
output: -5 -> -3 -> -2 -> 1 -> 4 

Input : -5 -> -10 
Output: -10 -> -5

Input : 5 -> 10 
output: 5 -> 10

```

资料来源：[亚马逊访谈](https://www.geeksforgeeks.org/amazon-interview-experience-set-258-for-sde1/)

一个简单的解决方案是从头到尾遍历链表。 对于每个访问的节点，请检查其是否有故障。 如果是，请将其从当前位置移除，然后插入正确的位置。 这是对链表的[插入排序的实现，此解决方案的时间复杂度为O（n * n）。](http://geeksquiz.com/insertion-sort-for-singly-linked-list/)

更好的解决方案是[使用合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对链接列表进行排序。 该解决方案的时间复杂度为O（n Log n）。

一个有效的解决方案可以在O（n）时间内工作。 一个重要的观察结果是，所有负面因素都以相反的顺序出现。 因此，我们遍历列表，每当找到不规则的元素时，便将其移到链接列表的前面。

以下是上述想法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to sort a linked list, already``// sorted by absolute values``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Linked List Node``struct` `Node``{` `Node* next;` `int` `data;``};``// Utility function to insert a node at the``// beginning``void` `push(Node** head,` `int` `data)``{` `Node* newNode =` `new` `Node;` `newNode->next = (*head);` `newNode->data = data;` `(*head) = newNode;``}``// Utility function to print a linked list``void` `printList(Node* head)``{` `while` `(head != NULL)` `{`[HTG22 5]  `cout << head->data;` `if` `(head->next != NULL)` `cout <<` `" -> "` `;` `head = head->next;` `}` `cout<<endl;``}``// To sort a linked list by actual values.``// The list is assumed to be sorted by absolute``// values.``void` `sortList(Node** head)``{` `// Initialize previous and current nodes` `Node* prev = (*head);` `Node* curr = (*head)->next;` `// Traverse list` `while` `(curr != NULL)` `{` `// If curr is smaller than prev, then` `// it must be moved to head` ] `if` `(curr->data < prev->data)`​​ `{` `// Detach curr from linked list` [ `prev->next = curr->next;` `// Move current node to beginning` `curr->next = (*head);` `(*head) = curr;` `// Update current` `curr = prev;` `}` `// Nothing to do if current element` `// is at right place` `else` `prev = curr;`[ `// Move current` `curr = curr->next;` `}``}``// Driver code``int` `main()``{` `Node* head = NULL;` `push(&head, -5);` `push(&head, 5);` `push(&head, 4);`[HTG14 0] `push(&head, 3);` `push(&head, -2);` `push(&head, 1);` `push(&head, 0);` `cout <<` `"Original list :\n"` `;` `printList(head);` `sortList(&head);` `cout <<` `"\nSorted list :\n"` `;` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*