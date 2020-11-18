# 链表

的顺时针旋转

给定一个单链接列表和一个整数 **K** ，任务是将链接列表向右顺时针旋转 **K** 位置。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> NULL，K = 2
> **输出：** 4 -> 5-> 1-> 2-> 3->空
> 
> **输入：** 7-> 9-> 11-> 13-> 3-> 5-> NULL，K = 12
> **输出 ：** 7-> 9-> 11-> 13-> 3-> 5-> NULL

**方法：**要旋转链表，请首先检查给定的k是否大于链表中节点的数量。 遍历列表并找到链表的长度，然后将其与k进行比较，如果小于k，则继续进行，否则通过对链表的长度取模，得出链表的大小。
之后，从列表的长度中减去k的值。 现在，问题已更改为链表的左旋转，因此请执行以下步骤：

*   将第k个节点的下一个更改为NULL。
*   将最后一个节点的下一个更改为上一个头节点。
*   将头更改为第（k + 1）个节点。

为此，需要指向第k个节点，第（k + 1）个节点和最后一个节点的指针。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* A utility function to push a node */``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;`​​  `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}` [`/* A utility function to print linked list */``void` `printList(Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" -> "` `;` `node = node->next;` `}` `cout <<` `"NULL"` `;``}``// Function that rotates the given linked list``// clockwise by k and returns the updated``// head pointer`]`Node* rightRotate(Node* head,` `int` `k)``{` `// If the linked list is empty` `if` `(!head)` `return` `head;` `// len is used to store length of the linked list` `// tmp will point to the last node after this loop` `Node* tmp = head;` `int` `len = 1;` `while` `(tmp->next != NULL) {` `tmp = tmp->next;` `len++;` `}` [ `// If k is greater than the size` `// of the linked list` `if` `(k > len)` `k = k % len;`的 `// Subtract from length to convert` `// it into left rotation` `k = len - k;` `// If no rotation needed then` `// return the head node` `if` `(k == 0 &#124;&#124; k == len)` `return` `head;` `// current will either point to` `// kth or NULL after this loop` `Node* current = head;` `int` `cnt = 1;` `while` `(cnt < k && current != NULL) {` `current = current->next;` `cnt++;` `}` `// If current is NULL then k is equal to the` `// count of nodes in the list` `// Don't change the list in this case` `if` `(current == NULL)` `return` `head;` ] `// current points to the kth node` `Node* kthnode = current;` `// Change next of last node to previous head` `tmp->next = head;` `// Change head to (k+1)th node` `head = kthnode->next;` `// Change next of kth node to NULL` `kthnode->next = NULL;` `// Return the updated head pointer` `return` `head;``}``// Driver code` [HTG43 5]`int` `main()``{` `/* The constructed linked list is: ` `1->2->3->4->5 */` `Node* head = NULL;` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` ] `push(&head, 2);` `push(&head, 1);` `int` `k = 2;` `// Rotate the linked list` `Node* updated_head = rightRotate(head, k);` `// Print the rotated linked list` `printList(updated_head);` `return` `0;``}`] |

*chevron_right**filter_none*