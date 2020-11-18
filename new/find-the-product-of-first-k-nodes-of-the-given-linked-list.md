# 查找给定链接列表

的前k个节点的乘积

给定一个指向单链表头的指针和一个整数 **k** 。 任务是找到链表中第一个 **k** 个节点的乘积。

**示例：**

> **输入：** 10-> 6-> 8-> 4-> 12，k = 2
> **输出：** 60
> 10 * 6 = 60
> 
> **输入：** 15-> 7-> 9-> 5-> 16-> 14，k = 4
> **输出：** 4725
> 15 * 7 * 9 * 5 = 4725

**方法：**设置 **prod = 1** （必需产品），并且 **count = 0** （遍历的节点数）。 现在，开始从左到右遍历链表的节点，并在每个[[ **计数< k** 。 最后打印 **prod** 的值。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find the product of first``// 'k' nodes of the Linked List``#include <bits/stdc++.h>``using` `namespace` `std;``#define ll long long int``/* A Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `new` `Node;` `/* put in the data */` `new_node->data = new_data;` `/* link the old list to the new node */` `new_node->next = (*head_ref);`[HTG18 5]  `(*head_ref) = new_node;``}` [`// Function to return the product of``// first k nodes of the given linked list``ll product(` `struct` `Node* head,` `int` `k)``{` `if` `(k <= 0)` `return` `0;` `ll prod = 1;` `int` `i = 0;` `Node* node = head;` `// Traverse the list from left to right` `while` `(i < k) {` `// Update product` `prod = prod * node->data;` `// Move to the next node` `node = node->next;` `i++;` `}` [ `// Return the required product` [ `return` `prod;``}``// Driver code``int` `main()``{` `struct` `Node* head = NULL;` `// Linked list 10 -> 6 -> 8 -> 4 -> 12` `push(&head, 12);` `push(&head, 4);` `push(&head, 8);` `push(&head, 6);` `push(&head, 10);` `int` `k = 2;` `cout << product(head, k);`​​ `return` `0;``}` |

*chevron_right**filter_none*