# 单链接列表

的主要节点数

给定一个包含N个节点的单链列表，任务是查找素数的总数。

**示例：**

```
Input: List = 15 -> 5 -> 6 -> 10 -> 17
Output: 2
5 and 17 are the prime nodes

Input: List = 29 -> 3 -> 4 -> 2 -> 9
Output: 3
2, 3 and 29 are the prime nodes

```

**方法：**的想法是将链表遍历到最后并检查当前节点是否为质数。 如果是，则将计数增加1并继续执行相同操作，直到遍历所有节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find count of prime numbers``// in the singly linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Node of the singly linked list``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to check if a number is prime``bool` `isPrime(` `int` `n)``{` `// Corner cases` `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;` [ `// This is checked so that we can skip` `// middle five numbers in below loop` `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` `;` `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// Function to find count of prime``// nodes in a linked list``int` `countPrime(Node** head_ref)``{` `int` `count = 0;` `Node* ptr = *head_ref;` `while` `(ptr != NULL) {` `// If current node is prime` `if` `(isPrime(ptr->data)) {` `// Update count` `count++;`​​  `}` `ptr = ptr->next;` `}`的 `return` `count;``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;`的]  `// create the linked list` `// 15 -> 5 -> 6 -> 10 -> 17` `push(&head, 17);` `push(&head, 10);` `push(&head, 6);` `push(&head, 5);` `push(&head, 15);` `// Function call to print require answer` `cout <<` `"Count of prime nodes = "` `<< countPrime(&head);`的 `return` `0;``}` |

*chevron_right**filter_none*