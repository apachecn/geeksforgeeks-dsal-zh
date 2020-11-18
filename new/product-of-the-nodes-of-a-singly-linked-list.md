# 单链接列表

的节点的乘积

给定一个单链表。 任务是找到给定链表所有节点的乘积。

**范例**：

```
Input : List = 7->6->8->4->1
Output : Product = 1344
Product of nodes: 7 * 6 * 8 * 4 * 1 = 1344

Input : List = 1->7->3->9->11->5
Output : Product = 10395

```

**算法**：

1.  使用链接列表的开头初始化指针ptr，并使用1初始化产品变量。
2.  使用循环开始遍历链表，直到遍历所有节点。
3.  将当前节点的值乘以乘积，即**乘积* = ptr->数据**。
4.  递增指向链表的下一个节点的指针，即 **ptr = ptr-> next** 。
5.  重复上述两个步骤，直到到达链表的末尾。
6.  最后，退回产品。

下面是上述算法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find the product of``// nodes of the Linked List``#include <iostream>``using` `namespace` `std;``// A Linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `new` `Node;` `/* put in the data */` `new_node->data = new_data;` `/* link the old list to the new node */` `new_node->next = (*head_ref);`[HTG1 75]  `(*head_ref) = new_node;``}``// Function to find the product of``int` `productOfNodes(` `struct` `Node* head)``{` `// Pointer to traverse the list` `struct` `Node* ptr = head;` `int` `product = 1;` `// Variable to store product` `// Traverse the list and` `// calculate the product` `while` `(ptr != NULL) {` `product *= ptr->data;` `ptr = ptr->next;` `}` `// Return the product` `return` ] `product;``}``// Driver Code``int` `main()`[ `{` `struct` `Node* head = NULL;` `// create linked list 7->6->8->4->1` `push(&head, 7);` `push(&head, 6);` `push(&head, 8);` `push(&head, 4);` `push(&head, 1);` `cout <<` `"Product = "` `<< productOfNodes(head);` `return` `0;`[`}` |

*chevron_right**filter_none*