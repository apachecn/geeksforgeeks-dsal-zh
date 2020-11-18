# 单链接列表

的所有主要节点的总和与乘积

给定一个包含N个节点的单链接列表，任务是从列表中查找素数所有节点的总和与乘积。

**范例**：

```
Input : List = 15 -> 16 -> 6 -> 7 -> 17
Output : Product = 119, Sum = 24
Prime nodes are 7, 17.

Input : List = 15 -> 3 -> 4 -> 2 -> 9
Output : Product = 6, Sum = 5

```

**方法：**的想法是逐个遍历单链接列表的节点，并检查当前节点是否为质数。 找到素数节点的数据之和和积。

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find sum and``// product of all of prime nodes of``// the singly linked list``#include <bits/stdc++.h>` ［HTG200］ ［HTG201］ ［HTG6］ ［HTG7］ ［HTG8］ ［HTG202］ ［HTG203］ ［HTG9］ ［HTG204］ ［HTG205］ ［HTG10］ ［HTG206］ ［HTG207］ ［HTG11］ ［HTG12］ ［ HTG208] `int` `data;` `Node* next;``};``// Function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// move the head to point to the new node` `(*head_ref) = new_node;``}``// Function to check if a number is prime``bool` `isPrime(` `int` `n)``{` `// Corner cases` `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;` `// This is checked so that we can skip`​​ `// middle five numbers in below loop` `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` `;` `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// Function to find sum and product of all``// prime nodes of the singly linked list`] `void` `sumAndProduct(Node* head_ref)``{` `int` `prod = 1;` `int` `sum = 0;`[ `Node* ptr = head_ref;` `// Traverse the linked list` `while` `(ptr != NULL) {` `// if current node is prime,` `// Find sum and product` `if` `(isPrime(ptr->data)) {` `prod *= ptr->data;` `sum += ptr->data;` `}` [ `ptr = ptr->next;` `}` `cout <<` `"Sum = "` `<< sum << endl;` `cout <<` `"Product = "` `<< prod;``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;`] `// create the linked list` `// 15 -> 16 -> 7 -> 6 -> 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 16);` `push(&head, 15);` `sumAndProduct(head);` `return` `0;``}` |

*chevron_right**filter_none*