# 给定链接列表

中的双音点

给定具有不同元素的链表，任务是在给定链表中找到[双音点](https://www.geeksforgeeks.org/find-bitonic-point-given-bitonic-sequence/)。 如果没有该点，则打印 **-1** 。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 3-> 2-> 1->空
> **输出：** 4
> 1-> 2-> 3-> 4严格增加。
> 4-> 3-> 2-> 1-> NULL严格减少。
> 
> **输入：** 97-> 98-> 99-> 91->空
> **输出：** 99

**方法：**双音点是双音序列中的一个点，在该点之前元素严格增加，而在元素之后严格减少。 如果数组仅在减少或仅在增加，则不存在双音点。 因此，找到第一个节点，使其旁边的节点的值严格较小。 从该节点开始遍历链表，如果每个其他节点都严格小于其先前的节点，则找到的节点处于重音序列之外，否则给定的链表不包含有效的重音序列。 **注意**空列表或具有单个节点的列表并不代表有效的双音序列。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Node for linked list``class` `Node {``public` `:` `int` `data;` `Node* next;``};``// Function to insert a node at``// the head of the linked list``Node* push(Node** head_ref,` `int` `data)``{` `Node* new_node =` `new` `Node;` `new_node->data = data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to return the bitonic``// of the given linked list``int` `bitonic_point(Node* node)``{` `// If list is empty` `if` `(node == NULL)` `return` `-1;` `// If list contains only` `// a single node` `if` `(node->next == NULL)` `return` `-1;` `// Invalid bitonic sequence` `if` `(node->data > node->next->data)` `return` `-1;` `while` `(node->next != NULL) {` `// If current node is the bitonic point` `if` `(node->data > node->next->data)` `break` `;` `// Get to the next node in the list` `node = node->next;` `}` `int` `bitonicPoint = node->data;` `// Nodes must be in descending` `// starting from here` `while` `(node->next != NULL) {` `// Out of order node` `if` `(node->data < node->next->data)` `return` `-1;` `// Get to the next node in the list` `node = node->next;`​​  `}`] `return` `bitonicPoint;``}``// Driver code``int` `main()``{` `Node* head = NULL;` `push(&head, 100);` `push(&head, 201);` `push(&head, 399);` `push(&head, 490);` `push(&head, 377);` `push(&head, 291);` `push(&head, 100);`[HTG30 6]  `cout << bitonic_point(head);` `return` `0;``}` |

*chevron_right**filter_none*