# 单链接列表的最小和最大素数

给定一个包含N个节点的单链列表，任务是查找最小和最大素数。

**示例：**

```
Input : List = 15 -> 16 -> 6 -> 7 -> 17
Output : Minimum : 7
         Maximum : 17

Input : List = 15 -> 3 -> 4 -> 2 -> 9
Output : Minimum : 2
         Maximum : 3

```

**方法：**

1.  这个想法是将链表遍历到最后，并将max和min变量分别初始化为INT_MIN和INT_MAX。
2.  检查当前节点是否为素数。 如是：
    *   如果当前节点的值大于max，则将当前节点的值分配给max。
    *   如果当前节点的值小于min，则将当前节点的值分配给min。
3.  重复上述步骤，直到到达列表末尾。

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find minimum``// and maximum prime number of``// the singly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Node of the singly linked list``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}`[`// Function to check if a number is prime``bool` `isPrime(` `int` `n)``{` `// Corner cases`[HTG2 26]  `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;` `// This is checked so that we can skip` `// middle five numbers in below loop` `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` `;` `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// Function to find maximum and minimum``// prime nodes in a linked list``void` `minmaxPrimeNodes(Node** head_ref)``{` `int` `minimum = INT_MAX;`​​  [ `int` `maximum = INT_MIN;` `Node* ptr = *head_ref;` `while` `(ptr != NULL) {` `// If current node is prime` `if` `(isPrime(ptr->data)) {` `// Update minimum` `minimum = min(minimum, ptr->data);` `// Update maximum` `maximum = max(maximum, ptr->data);` `}` `ptr = ptr->next;` `}` ]`}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the linked list` `// 15 -> 16 -> 7 -> 6 -> 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 16);` `push(&head, 15);` `minmaxPrimeNodes(&head);` `return` `0;``}` |

*chevron_right**filter_none*