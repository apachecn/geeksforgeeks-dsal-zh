# 双链表

中所有主要节点的乘积

给定一个包含N个节点的双链表。 任务是找到所有主要节点的乘积。

**示例：**

> **输入：**列表= 15 < = > 16 < = > 6 < = > 7 < = > 17
> **输出 ：**主节点乘积：119
> 
> **输入：**列表= 5 < = > 3 < = > 4 < = > 2 < = > 9
> **输出 ：**主节点乘积：30

**方法：**

*   用链接列表的开头初始化一个指针temp，并用1初始化一个product变量。
*   使用循环开始遍历链表，直到遍历所有节点。
*   如果节点值是质数，则将当前节点的值乘以乘积，即乘积* = current_node->数据。
*   递增指向链接列表的下一个节点的指针，即temp = temp-> next。
*   退货。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to product all``// prime nodes from the doubly``// linked list``#include <bits/stdc++.h>`的`using` `namespace` `std;``// Node of the doubly linked list``struct` `Node {` `int` `data;` `Node *prev, *next;``};``// function to insert a node at the beginning``// of the Doubly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// change prev of head node to new node` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node`​​ `(*head_ref) = new_node;``}``// Function to check if a number is prime``bool` `isPrime(` `int` `n)``{` `// Corner cases` `if` `(n <= 1)` `return` `false` `;` `if` `(n <= 3)` `return` `true` `;`的 `// This is checked so that we can skip` `// middle five numbers in below loop` `if` `(n % 2 == 0 &#124;&#124; n % 3 == 0)` `return` `false` [HT G101] `for` `(` `int` `i = 5; i * i <= n; i = i + 6)` `if` `(n % i == 0 &#124;&#124; n % (i + 2) == 0)` `return` `false` `;` `return` `true` `;``}``// function to product all prime nodes``// from the doubly linked list``int` `prodOfPrime(Node** head_ref)``{` `Node* ptr = *head_ref;` `Node* next;` `// variable prod = 1 for multiplying nodes value` `int` `prod = 1;` `// travese list till last node` `while` `(ptr != NULL) {` `next = ptr->next;` `// if number is prime then` `// multiply to product` `if` `(isPrime(ptr->data))` `prod = prod * ptr->data;` `ptr = next;` `}` `// return product` `return` `prod;``}``// Driver program``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the doubly linked list` `// 15 <-> 16 <-> 7 <-> 6 <-> 17` `push(&head, 17);` `push(&head, 6);` `push(&head, 7);` `push(&head, 16);` `push(&head, 15);` `int` `prod = prodOfPrime(&head);`的 `cout <<` `"Product of Prime Nodes : "` `<< prod;` `return` [HT G198]`}` |

*chevron_right**filter_none*