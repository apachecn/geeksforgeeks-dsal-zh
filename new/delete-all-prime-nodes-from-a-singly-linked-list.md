# 从单个链接列表中删除所有主要节点

给定一个包含N个节点的单链接列表，任务是从列表中删除所有素数的节点。

**示例：**

> **输入：**列表= 15-> 16-> 6-> 7-> 17
> **输出：**最终列表= 15-> 16-> 6
> 
> **输入：**列表= 15-> 3-> 4-> 2-> 9
> **输出：**最终列表= 15-> 4-> 9

**方法**：想法是逐个遍历单链接列表的节点并获得素数节点的指针。 通过遵循帖子中使用的方法删除那些节点：[从链接列表](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)中删除一个节点。

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to delete all``// prime nodes from the singly``// linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Node of the singly linked list``struct` `Node {` `int` `data;` `Node* next;``};`​​ `// function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` ] `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// move the head to point to the new node` `(*head_ref) = new_node;``}``// Function to check if a number is prime``bool` `isPrime(` `int` `n)``{` `// Corner cases` `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;` `// This is checked so that we can skip` `// middle five numbers in below loop` `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` `;` `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// function to delete a node in a singly Linked List.``// head_ref --> pointer to head node pointer.``// del --> pointer to node to be deleted``void` `deleteNode(Node** head_ref, Node* del)``{` `// base case` `struct` `Node* temp = *head_ref;` `if` `(*head_ref == NULL &#124;&#124; del == NULL)` `return` `;` `// If node to be deleted is head node` `if` `(*head_ref == del)` `*head_ref = del->next;` `// traverse list till not found` `// delete node` `while` `(temp->next != del) {` `temp = temp->next;` `}` `// copy address of node` `temp->next = del->next;` `// Finally, free the memory occupied by del` `free` `(del);` `return` `;``}``// function to delete all prime nodes`] `// from the singly linked list``void` `deletePrimeNodes(Node** head_ref)``{` `Node* ptr = *head_ref;` `Node* next;` `while` `(ptr != NULL) {` `next = ptr->next;` `// if true, delete node 'ptr'` `if` `(isPrime(ptr->data))` `deleteNode(head_ref, ptr);` `ptr = next;` `}``}``// function to print nodes in a``// given singly linked list``void` `printList(Node* head)``{` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` [HTG4 43] `head = head->next;` `}``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the linked list` `// 15 -> 16 -> 7 -> 6 -> 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 16);` `push(&head, 15);`的 `cout <<` `"Original List: "` `;` `printList(head);` `deletePrimeNodes(&head);`] `cout <<` `"\nModified List: "` `;` `printList(head);`[HT G494] `}` |

*chevron_right**filter_none*