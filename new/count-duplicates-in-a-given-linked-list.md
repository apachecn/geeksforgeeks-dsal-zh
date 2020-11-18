# 计算给定链接列表

中的重复项

给定一个链表。 任务是计算链接列表中重复节点的数量。
**范例：**

> **输入：** 5-> 7-> 5-> 1-> 7->空
> **输出：** 2
> 
> **输入：** 5-> 7-> 8-> 7-> 1->空
> **输出：** 1

**简单方法：**我们遍历整个链表。 对于每个节点，我们在其余列表中检查是否存在重复节点。 如果是，那么我们增加计数。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``#include <unordered_set>``using` `namespace` `std;` [`// Representation of node``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert a node at the beginning``void` `insert(Node** head,` `int` `item)``{` `Node* temp =` `new` `Node();` `temp->data = item;` `temp->next = *head;` `*head = temp;``}``// Function to count the number of``// duplicate nodes in the linked list``int` `countNode(Node* head)``{` `int` `count = 0;`的[HT G45] `while` `(head->next != NULL) {` `// Starting from the next node` `Node *ptr = head->next;` `while` `(ptr != NULL) {` `// If some duplicate node is found` `if` `(head->data == ptr->data) {` `count++;` `break` `;` `}` `ptr = ptr->next;` `}` `head = head->next;` `}` `// Return the count of duplicate nodes` `return` `count;``}``// Driver code``int` `main()``{` `Node* head = NULL;` `insert(&head, 5);`[ `insert(&head, 7);` `insert(&head, 5);` `insert(&head, 1);` `insert(&head, 7);` HTG226] `cout << countNode(head);` `return` `0;``}` |

*chevron_right**filter_none*