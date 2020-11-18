# 编写一个函数，计算一个给定的int在链表

中出现的次数

给定一个单链表和一个键，计算给定键在链表中出现的次数。 例如，如果给定的链表为1-> 2-> 1-> 2-> 1-> 3-> 1，且给定键为1，则输出应为4。

**方法1-无递归**
**算法：**

```
1\. Initialize count as zero.
2\. Loop through each element of linked list:
     a) If element data is equal to the passed number then
        increment the count.
3\. Return count. 

```

**实施：**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to count occurrences in a linked list``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* Given a reference (pointer to pointer) to the head ``of a list and an int, push a new node on the front ``of the list. */``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``/* Counts the no. of occurrences of a node ``(search_for) in a linked list (head)*/``int` `count(Node* head,` `int` `search_for)``{` `Node* current = head;` `int` `count = 0;` `while` `(current != NULL) {` `if` `(current->data == search_for)` `count++;` `current = current->next;` `}` `return` `count;``}``/* Driver program to test count function*/``int` `main()``{` `/* Start with the empty list */` `Node* head = NULL;` HTG212] `/* Use push() to construct below list ` `1->2->1->3->1 */` `push(&head, 1);` `push(&head, 3);` `push(&head, 1);` `push(&head, 2);` `push(&head, 1);` `/* Check the count function */` `cout <<` `"count of 1 is "` `<< count(head, 1);` `return` `0;``}`的`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*