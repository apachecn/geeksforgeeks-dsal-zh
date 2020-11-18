# 将节点插入到链表

的中间

给定一个包含 **n** 个节点的链表。 问题是在列表中间插入一个新节点，其数据为 **x** 。 如果 **n** 是偶数，则在第**（n / 2）**个节点后插入新节点，否则在**（n + 1）/ 2 [** th节点。

**示例：**

```
Input : list: 1->2->4->5
        x = 3
Output : 1->2->3->4->5

Input : list: 5->10->4->32->16
        x = 41
Output : 5->10->4->41->32->16

```

**方法1（使用链接列表的长度）：**
使用一个遍历查找节点数或链接的长度。 设为**等于**。 如果 **len** 是偶数，则计算 **c** =（len / 2），否则，如果 **len** ，则计算 **c** =（len + 1）/ 2 ]很奇怪。 再次遍历第一个 **c** 节点，并在第 **c** 个节点之后插入新节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to insert node at the middle``// of the linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// structure of a node``struct` `Node {` `int` `data;` `Node* next;``};``// function to create and return a node``Node* getNode(` `int` `data)``{` `// allocating space` `Node* newNode = (Node*)` `malloc` `(` `sizeof` `(Node));` `// inserting the required data` `newNode->data = data;` `newNode->next = NULL;` `return` `newNode;``}``// function to insert node at the middle``// of the linked list``void` `insertAtMid(Node** head_ref,` `int` `x)``{` `// if list is empty` `if` `(*head_ref == NULL)` `*head_ref = getNode(x);` `else` `{` `// get a new node` `Node* newNode = getNode(x);` `Node* ptr = *head_ref;` `int` `len = 0;` `// calculate length of the linked list` `//, i.e, the number of nodes` `while` `(ptr != NULL) {` `len++;` `ptr = ptr->next;` `}`​​ `// 'count' the number of nodes after which` `//  the new node is to be inserted` `int` `count = ((len % 2) == 0) ? (len / 2) :` `(len + 1) / 2;` `ptr = *head_ref;`[H TG283]  `// 'ptr' points to the node after which ` `// the new node is to be inserted` `while` `(count-- > 1)` `ptr = ptr->next;` `// insert the 'newNode' and adjust the` `// required links` `newNode->next = ptr->next;` `ptr->next = newNode;` `}``}``// function to display the linked list``void` `display(Node* head)``{` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver program to test above``int` `main()``{` `// Creating the list 1->2->4->5` [H TG144] `head = getNode(1);` `head->next = getNode(2);` `head->next->next = getNode(4);` `head->next->next->next = getNode(5);` `cout <<` `"Linked list before insertion: "` `;` `display(head);` `int` `x = 3;` `insertAtMid(&head, x);` `cout <<` `"\nLinked list after insertion: "` `;` `display(head);` `return` `0;``}` |

*chevron_right**filter_none*