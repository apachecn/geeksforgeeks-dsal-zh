# 查找链接列表的长度（迭代和递归）

编写一个函数以计算给定单链列表中的节点数。

[![linkedlist_find_length](img/e38a7cce1aae90394ef3ebc5cd8323c1.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2015/03/Linkedlist_find_length.png)

例如，对于链接列表1-> 3-> 1-> 2-> 1，该函数应返回5。

**迭代解决方案**

```
1) Initialize count as 0 
2) Initialize a node pointer, current = head.
3) Do following while current is not NULL
     a) current = current -> next
     b) count++;
4) Return count 
```

以下是上述算法的实现，以找到节点数。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Iterative C++ program to find length ``// or count of nodes in a linked list ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next; ``}; ``/* Given a reference (pointer to pointer) to the head ``of a list and an int, push a new node on the front ``of the list. */``void` `push(Node** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); `[HTG17 0]  `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``/* Counts no. of nodes in linked list */``int` `getCount(Node* head) ``{ ` `int` `count = 0;` `// Initialize count ` `Node* current = head;` `// Initialize current ` `while` `(current != NULL) ` `{ ` `count++; ` `current = current->next; ` `} ` `return` `count; ``} `的`/* Driver program to test count function*/``int` `main() ``{ ` `/* Start with the empty list */` `Node* head = NULL; ` `/* Use push() to construct below list ` `1->2->1->3->1 */` `push(&head, 1); `[ `push(&head, 3); ` `push(&head, 1); ` `push(&head, 2); ` `push(&head, 1); `的 `/* Check the count function */` `cout<<` `"count of nodes is "` `<< getCount(head); ` `return` `0; ``} `，`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*