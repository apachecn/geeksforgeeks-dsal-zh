# 链表

的备用节点总和

给定一个链表，任务是打印链表的备用节点之和。

**范例**：

```
Input : 1 -> 8 -> 3 -> 10 -> 17 -> 22 -> 29 -> 42
Output : 50
Alternate nodes : 1 -> 3 -> 17 -> 29

Input : 10 -> 17 -> 33 -> 38 -> 73
Output : 116
Alternate nodes : 10 -> 33 -> 73

```

**迭代方法：**

1.  遍历整个链表。
2.  设置总和= 0且计数= 0。
3.  计数为偶数时，将节点的数据相加。
4.  访问下一个节点。

以下是此方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ code to print the sum of Alternate Nodes ``#include <iostream>``using` `namespace` `std;``/* Link list node */``struct` `Node``{ ` `int` `data; ` `struct` `Node* next; ``}; ``/* Function to get the alternate ``nodes of the linked list */``int` `sumAlternateNode(` `struct` `Node* head) ``{ ` `int` `count = 0; ` `int` `sum = 0; ` `while` `(head != NULL) ` `{ ` `// when count is even sum the nodes ` `if` `(count % 2 == 0) ` `sum += head->data; ` `// count the nodes `[HTG1 77]  `count++; ` `// move on the next node. ` `head = head->next; ` `} ` `return` `sum; ``} ``// Function to push node at head ``void` `push(` `struct` `Node** head_ref,` `int` `new_data) ``{ ` `struct` `Node* new_node = ` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node)); ` `new_node->data = new_data; ` `new_node->next = (*head_ref); ` `(*head_ref) = new_node; ``} ``// Driver code ``int` `main() ``{ ` `/* Start with the empty list */` `struct` `Node* head = NULL; `的[ `/* Use push() function to construct ` `the below list 8 -> 23 -> 11 -> 29 -> 12 */` `push(&head, 12); ` `push(&head, 29); ` `push(&head, 11); ` `push(&head, 23); ` `push(&head, 8); ` [ `cout << sumAlternateNode(head); ` `return` `0; ``} ``// This code is contributed by SHUBHAMSINGH10` |

*chevron_right**filter_none*