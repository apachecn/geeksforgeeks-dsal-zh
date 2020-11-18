# 双链表中所有节点的和，可被给定数K整除

给定一个包含N个节点的双链表，并给定数字K。任务是找到所有可被K整除的节点之和。

**示例：**

```
Input: List = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
       K = 3
Output: Sum = 30

Input: List = 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
       K = 2
Output: Sum = 20

```

**方法：**想法是遍历双向链表并逐个检查节点。 如果节点的值可被K整除，则将该节点值添加到![sum](img/6956acab453be147c8390f8833632c5e.png "Rendered by QuickLaTeX.com")，否则在未到达列表末尾的情况下继续此过程。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to add``// all nodes value which is``// divided by any given number K``#include <bits/stdc++.h>`的`using` `namespace` `std;``// Node of the doubly linked list``struct` `Node {` `int` `data;` `Node *prev, *next;``};``// function to insert a node at the beginning``// of the Doubly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// change prev of head node to new node` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `// move the head to point to the new node` `(*head_ref) = new_node;``}``// function to sum all the nodes``// from the doubly linked``// list that are divided by K``int` `sumOfNode(Node** head_ref,` `int` `K)``{` `Node* ptr = *head_ref;` `Node* next;` `// variable sum=0 for add nodes value` `int` `sum = 0;` `// traves list till last node` `while` `(ptr != NULL) {` `next = ptr->next;` `// check is node value divided by K` `// if true then add in sum` [HT G97] `(ptr->data % K == 0)` `sum += ptr->data;` `ptr = next;` `}` `// return sum of nodes which is divided by K` `return` `sum;``}``// Driver program to test above`​​`int` `main()``{` `// start with the empty list` `Node* head = NULL;`的 `// create the doubly linked list` `// 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 9);` `push(&head, 10);` `push(&head, 16);` `push(&head, 15);` `int` `sum = sumOfNode(&head, 3);`144] `"Sum = "` `<< sum;``}` |

*chevron_right**filter_none*