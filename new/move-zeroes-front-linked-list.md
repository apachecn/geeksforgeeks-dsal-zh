# 将所有零移动到链接列表的前面

给定一个链表。 任务是将全0移到链接列表的前面。 重新排列后，除0以外的所有其他元素的顺序应相同。

**示例：**

```
Input : 0 1 0 1 2 0 5 0 4 0
Output :0 0 0 0 0 1 1 2 5 4

Input :1 1 2 3 0 0 0 
Output :0 0 0 1 1 2 3 

```

**简单解决方案**是将所有链接列表元素存储在数组中。 然后将数组的所有元素移到开头。 最后，将数组元素复制回链接列表。

**有效解决方案**是从第二个节点遍历链表。 对于每个值为0的节点，我们将其与当前位置断开连接，然后将节点移到最前面。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to move all zeros``// to the end of the linked list.``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node *next;``};``/* Given a reference (pointer to pointer) to``the head of a list and an int, push a new``node on the front of the list. */``void` `push(` `struct` `Node **head_ref,` `int` `new_data) {` `struct` `Node *new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* moving zeroes to the beginning in linked list */``void` `moveZeroes(` `struct` `Node **head) {` `if` `(*head == NULL)` `return` `;` `// Traverse the list from second node.` `struct` `Node *temp = (*head)->next, *prev = *head;` `while` `(temp != NULL) {` [ `// If current node is 0, move to` `// beginning of linked list` `if` `(temp->data == 0) {` `// Disconnect node from its` `// current position` `Node *curr = temp;` `temp = temp->next;` `prev->next = temp;` `// Move to beginning`​​ `curr->next = (*head);` `*head = curr;` `}` `// For non-zero values` `else` `{` `prev = temp;` `temp = temp->next;` `}` `}``}``// function to displaying nodes``void` `display(` `struct` `Node *head) {` `while` `(head != NULL) {` `cout << head->data <<` `"->"` `;` `head = head->next;` `}` `cout <<` `"NULL"` `;``}` [`/* Driver program to test above function*/``int` `main() {` `/* Start with the empty list */` `struct` `Node *head = NULL;` `/* Use push() to construct below list` `0->0->1->0->1->0->2->0->3->0 */` `push(&head, 0);` `push(&head, 3);` `push(&head, 0);` `push(&head, 2);` `push(&head, 0);` `push(&head, 1);` `push(&head, 0);` `push(&head, 1);` `push(&head, 0);` `push(&head, 0);` `// displaying list before rearrangement` `cout <<` `"Linked list before rearrangement\n"` `;`] `display(head);` `/* Check the move_zeroes function */` `moveZeroes(&head);`[ `// displaying list after rearrangement` `cout <<` `"\n Linked list after rearrangement \n"` `;` `display(head);` `return` `0;``}` |

*chevron_right**filter_none*