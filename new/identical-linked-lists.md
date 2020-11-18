# 相同的链接列表

当两个链表具有相同的数据并且数据的排列也相同时，它们是相同的。 例如，链接列表a（1-> 2-> 3）和b（1-> 2-> 3）相同。 。 编写一个函数来检查给定的两个链表是否相同。

**方法1（迭代）**
要确定两个列表是否相同，我们需要同时遍历两个列表，并且在遍历时需要比较数据。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// An iterative C++ program to check if ``// two linked lists are identical or not``#include<bits/stdc++.h>``using` `namespace` `std;` [`/* Structure for a linked list node */``struct` `Node``{` `int` `data;` `struct` `Node *next;``};``/* Returns true if linked lists a and b ``are identical, otherwise false */``bool` `areIdentical(` `struct` `Node *a, ` `struct` `Node *b)``{` `while` ] `(a != NULL && b != NULL)` `{` `if` `(a->data != b->data)` `return` `false` `;` `/* If we reach here, then a and b are ` `not NULL and their data is same, so ` `move to next nodes in both lists */` `a = a->next;` `b = b->next;` `}` `// If linked lists are identical, then ` `// 'a' and 'b' must be NULL at this point.` `return` `(a == NULL && b == NULL);``}``/* UTILITY FUNCTIONS TO TEST fun1() and fun2() */``/* Given a reference (pointer to pointer) to the ``head of a list and an int, push a new node on the ``front of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);`[HT G101] `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Driver Code``int` `main()`​​ `{` `/* The constructed linked lists are :` `a: 3->2->1` `b: 3->2->1 */` `struct` `Node *a = NULL;` `struct` `Node *b = NULL;` `push(&a, 1);` `push(&a, 2);` `push(&a, 3);` `push(&b, 1);` `push(&b, 2);` `push(&b, 3);` `if` `(areIdentical(a, b))` `cout <<` `"Identical"` `;` `else` `cout <<` `"Not identical"` `;`[HT G150] `return` `0;``}` [`// This code is contributed ``// by Akanksha Rai` |

*chevron_right**filter_none*