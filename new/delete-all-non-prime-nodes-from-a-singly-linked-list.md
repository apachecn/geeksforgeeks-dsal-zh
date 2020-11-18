# 从单链接列表中删除所有非主要节点

给定一个包含N个节点的单链接列表，任务是从列表中删除不是素数的所有节点。

**示例：**

> **输入：**列表= 15-> 16-> 6-> 7-> 17
> **输出：**最终列表= 7-> 17
> 
> **输入：**列表= 15-> 3-> 4-> 2-> 9
> **输出：**最终列表= 3-> 2

**方法**：想法是一个遍历单链表的节点，并获得**不是素数**的节点的指针。 通过按照帖子中使用的方法删除这些节点：[从链接列表](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)中删除一个节点。

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to delete all``// non-prime nodes from the singly``// linked list``#include <bits/stdc++.h>`的`using` `namespace` `std;``// Node of the singly linked list``struct` `Node {` `int` `data;` `Node* next;``};``// function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}`[`// Function to check if a number is prime``bool` `isPrime(` `int` `n)`​​ `{` `// Corner cases`[HTG2 74]  `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;` `// This is checked so that we can skip` `// middle five numbers in below loop`]  `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` `;` `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// function to delete all non-prime nodes``// from the singly linked list``void` `deleteNonPrimeNodes(Node** head_ref)``{` `// Remove all composite nodes at the beginning` `Node* ptr = *head_ref;` [ `while` `(ptr != NULL && !isPrime(ptr->data))` `{` `Node *temp = ptr;` `ptr = ptr->next;` `delete` `(temp);` `}` `*head_ref = ptr;` `if` `(ptr == NULL)` `return` `;` `// Remove remaining nodes` `Node *curr = ptr->next;` `while` `(curr != NULL) {` `if` `(!isPrime(curr->data))` `{` `ptr->next = curr->next;` `delete` `(curr);` `curr = ptr->next;` `}` [ `else` `{` `ptr = curr;` `curr = curr->next;` `}` `}    ``}`的`// function to print nodes in a``// given singly linked list``void` `printList(Node* head)``{` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the linked list` `// 15 -> 16 -> 7 -> 6 -> 17`] `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 16);` `push(&head, 15);` `cout <<` `"Original List: "` `;`]  `printList(head);` `deleteNonPrimeNodes(&head);` `cout <<` `"\nModified List: "` `;` `printList(head);``}` |

*chevron_right**filter_none*