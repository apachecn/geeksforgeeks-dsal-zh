# 减去链表

的备用节点

给定一个链表。 任务是打印第一个奇数位置的节点与所有其他奇数位置的节点之和之间的差。

**示例：**

> **输入：** 1-> 8-> 3-> 10-> 17-> 22-> 29-> 42
> **输出：** -48
> **备用节点：** 1-> 3-> 17-> 29
> 1 –（3 + 17 + 29）= -48
> 
> **输入：** 10-> 17-> 33-> 38-> 73
> **输出：** -96
> **备用节点 ：** 10-> 33-> 73
> 10 –（33 + 73）= -96

我们已经讨论了链表的替代节点的[总和](https://www.geeksforgeeks.org/sum-of-the-alternate-nodes-of-linked-list/)

**迭代方法：**

1.  遍历整个链表。
2.  设置差异= 0，计数= 0。
3.  当计数为偶数时，从差中减去节点的数据。
4.  访问下一个节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to print the difference ``// of Alternate Nodes ``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Link list node ``struct` `Node { ` `int` `data; ` `struct` `Node* next; ``}; ``// Function to get the alternate ``// nodes of the linked list ``int` `subtractAlternateNode(` `struct` `Node* head) ``{ ` `int` `count = 0; ` `int` `difference = 0; ` `while` `(head != NULL) { ` `// When count is even subtract the nodes ` `if` `(count % 2 == 0)` `if` `(difference == 0){` `difference = head->data;` `}` `else` `{` `difference -= head->data; ` `} ` `// Count the nodes ` `count++; ` `// Move on the next node. ` `head = head->next; ` `} ` `return` `difference; ``} ``// Function to push node at head ``void` `push(` `struct` `Node** head_ref,` `int` `new_data) ``{ ` `struct` `Node* new_node =` `new` `Node; ` `new_node->data = new_data; ` `new_node->next = (*head_ref); ` `(*head_ref) = new_node; ``} ``// Driver code ``int` `main() ``{ ` `// Start with the empty list ` `struct` `Node* head = NULL;` [H TG227] `// Use push() function to construct ` `// the below list 8 -> 23 -> 11 -> 29 -> 12 ` `push(&head, 12); ` `push(&head, 29); ` `push(&head, 11); ` `push(&head, 23); ` `push(&head, 8); ` [ `cout << subtractAlternateNode(head); ` `return` `0; ``}`的[`// This code is contributed by shubhamsingh10` |

*chevron_right**filter_none*