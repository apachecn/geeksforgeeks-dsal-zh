# 隔离链表

中的偶数和奇数节点

给定整数链接列表，编写一个函数来修改链接列表，以使所有偶数出现在修改后的链接列表中的所有奇数之前。 另外，请保持偶数和奇数的顺序相同。

例子：

```
Input: 17->15->8->12->10->5->4->1->7->6->NULL
Output: 8->12->10->4->6->17->15->5->1->7->NULL

Input: 8->12->10->5->4->1->6->NULL
Output: 8->12->10->4->6->5->1->NULL

// If all numbers are even then do not change the list
Input: 8->12->10->NULL
Output: 8->12->10->NULL

// If all numbers are odd then do not change the list
Input: 1->3->5->7->NULL
Output: 1->3->5->7->NULL

```

**方法1**
这个想法是获得指向列表最后一个节点的指针。 然后从头节点开始遍历列表，并将奇数值节点从其当前位置移动到列表末尾。

感谢blunderboy建议这种方法。

算法：
…1）获取指向最后一个节点的指针。
…2）将所有奇数节点移到末尾。
……..a）考虑第一个偶数节点之前的所有奇数节点，并将它们移到末尾。
……..b）更改头指针，使其指向第一个偶数节点。
……..b）考虑第一个偶数节点之后的所有奇数节点，并将它们移到末尾。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to segregate even and``//  odd nodes in a Linked List ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* a node of the singly linked list */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``void` `segregateEvenOdd(Node **head_ref) ``{ ` `Node *end = *head_ref; ` `Node *prev = NULL; ` `Node *curr = *head_ref; ` [ `/* Get pointer to the last node */` `while` `(end->next != NULL) ` `end = end->next; `[ `Node *new_end = end; ` `/* Consider all odd nodes before the first ` `even node and move then after end */` `while` `(curr->data % 2 != 0 && curr != end) ` `{ ` `new_end->next = curr; ` `curr = curr->next; ` `new_end->next->next = NULL; ` `new_end = new_end->next; ` `} ` `// 10->8->17->17->15 ` `/* Do following steps only if ` `there is any even node */` `if` `(curr->data%2 == 0) ` `{ ` `/* Change the head pointer to ` `point to first even node */` `*head_ref = curr; `的 `/* now current points to` `the first even node */` `while` `(curr != end) ` `{ ` `if` `( (curr->data) % 2 == 0 ) ` `{ ` `prev = curr; ` `curr = curr->next; ` `} ` `else` `{ ` `/* break the link between` `prev and current */` `prev->next = curr->next; ` `/* Make next of curr as NULL */` `curr->next = NULL; ` `/* Move curr to end */` `new_end->next = curr; ` `/* make curr as new end of list */` `new_end = curr; ` `/* Update current pointer to` `next of the moved node */`] `curr = prev->next; ` `} ` `} ` `} ` `/* We must have prev set before executing ` `lines following this statement */` `else` `prev = curr; ` `/* If there are more than 1 odd nodes ` `and end of original list is odd then ` `move this node to end to maintain `] `same order of odd numbers in modified list */` `if` `(new_end != end && (end->data) % 2 != 0) ` `{ ` `prev->next = end->next; ` `end->next = NULL; ` `new_end->next = end; ` `} ` `return` `; ``} ``/* UTILITY FUNCTIONS */``/* Function to insert a node at the beginning */``void` `push(Node** head_ref,` `int` ] `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; `[HTG47 9]  `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``/* Function to print nodes in a given linked list */``void` `printList(Node *node) ``{` ] `while` `(node != NULL) ` `{ ` `cout << node->data <<` `" "` `; ` `node = node->next; ` `} ``} ``/* Driver code*/``int` `main() ``{ ` `/* Start with the empty list */` `Node* head = NULL; ` `/* Let us create a sample linked list as following ` `0->2->4->6->8->10->11 */`[H TG236] `push(&head, 11); ` `push(&head, 10); ` `push(&head, 8); ` `push(&head, 6); ` `push(&head, 4); ` `push(&head, 2); ` `push(&head, 0); ` `cout <<` `"Original Linked list "` `; ` `printList(head); ` `segregateEvenOdd(&head); ` `cout <<` `"\nModified Linked list "` `; ` `printList(head); ` `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*