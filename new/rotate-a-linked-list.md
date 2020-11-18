# 旋转链接列表

给定一个单链表，将链表逆时针旋转k个节点。 其中k是给定的正整数。 例如，如果给定的链表是10-> 20-> 30-> 40-> 50-> 60且k为4，则该链表应修改为50-> 60-> 10-> 20-> 30- > 40。 假设k小于链表中节点的数量。

**<u>方法-1：</u>**
要旋转链接列表，我们需要将第k个节点的下一个更改为NULL，将最后一个节点的下一个更改为上一个头节点，最后， 将头更改为第（k + 1）个节点。 因此，我们需要掌握三个节点：第k个节点，第（k + 1）个节点和最后一个节点。
从头开始遍历列表，并在第k个节点处停止。 存储指向第k个节点的指针。 接下来我们可以使用kthNode- >获得第（k + 1）个节点。 继续遍历最后一点，并存储指向最后一个节点的指针。 最后，如上所述更改指针。

下图显示了rotate函数在代码中的工作方式：

![](img/d20bcab15c5c1bfdac020daf13ed0cb5.png)

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to rotate``// a linked list counter clock wise``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``// This function rotates a linked list``// counter-clockwise and updates the``// head. The function assumes that k is``// smaller than size of linked list.``// It doesn't modify the list if``// k is greater than or equal to size``void` `rotate(Node** head_ref,` `int` `k)``{` `if` `(k == 0)` `return` `;` `// Let us understand the below` `// code for example k = 4 and` `// list = 10->20->30->40->50->60\.`​​ `Node* current = *head_ref;` `// current will either point to` `// kth or NULL after this loop.` `// current will point to node` `// 40 in the above example` `int` `count = 1;` `while` `(count < k && current != NULL) {` `current = current->next;` `count++;` `}` `// If current is NULL, k is greater than` `// or equal to count of nodes in linked list.` `// Don't change the list in this case` `if` `(current == NULL)` `return` `;` `// current points to kth node.` `// Store it in a variable. kthNode` `// points to node 40 in the above example` `Node* kthNode = current;` `// current will point to` `// last node after this loop` ] `// node 60 in the above example` `while` `(current->next != NULL)` `current = current->next;` `// Change next of last node to previous head` `// Next of 60 is now changed to node 10` `current->next = *head_ref;` `// Change head to (k+1)th node` `// head is now changed to node 50` `*head_ref = kthNode->next;` `// change next of kth node to NULL` `// next of 40 is now NULL` `kthNode->next = NULL;``}` [`/* UTILITY FUNCTIONS */``/* Function to push a node */``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``/* Function to print linked list */``void` `printList(Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `node = node->next;` `}``}``/* Driver code*/``int` `main(` `void` `)``{` `/* Start with the empty list */` `Node* head = NULL;` `// create a list 10->20->30->40->50->60` `for` `(` `int` `i = 60; i > 0; i -= 10)` `push(&head, i);` `cout <<` `"Given linked list \n"` `;` ]  `printList(head);` `rotate(&head, 4);` `cout <<` `"\nRotated Linked list \n"` `;` `printList(head);` `return` `(0);``}``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*