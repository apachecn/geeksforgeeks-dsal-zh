# 旋转N个节点的双链表

给定一个双向链表，将链表逆时针旋转N个节点。 N是给定的正整数，小于链表中节点的数量。
![](img/fc98432b5902440dd1c419d10877e43e.png)

N = 2

轮播名单：
![](img/1dc88401495c26072bae0563c47cdfa3.png)

**示例：**

```
Input : a  b  c  d  e  N = 2
Output : c  d  e  a  b 

Input : a  b  c  d  e  f  g  h  N = 4
Output : e  f  g  h  a  b  c  d 

```

**在** [亚马逊](https://www.geeksforgeeks.org/amazon-interview-experience-set-424-sde-2/)
中问

要旋转双链表，我们需要将第N个节点的下一个更改为NULL，将最后一个节点的下一个更改为上一个头节点，将头节点的上一个更改为最后一个节点，最后将头更改为第（N + 1）个节点，然后将上一个更改为 将新的头节点设置为NULL（双向链接列表中的头节点的上一个为NULL）

因此，我们需要掌握三个节点：第N个节点，第（N + 1）个节点和最后一个节点。 从头开始遍历列表，并在第N个节点处停止。 存储指向第N个节点的指针。 我们可以使用NthNode-> next获得第（N + 1）个节点。 继续遍历直到结束，并将指针也存储到最后一个节点。 最后，使用
PrintList功能更改上述指针，并更改“ Last Print Rotated List”的指针。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to rotate a Doubly linked `​​ `// list counter clock wise by N times``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `char` `data;` `struct` `Node* prev;` `struct` `Node* next;``};``// This function rotates a doubly linked``// list counter-clockwise and updates the ``// head. The function assumes that N is``// smallerthan size of linked list. It ``// doesn't modify the list if N is greater ``// than or equal to size``void` `rotate(` `struct` `Node** head_ref,` `int` `N)``{` `if` `(N == 0)` `return` `;` `// Let us understand the below code ` `// for example N = 2 and` `// list = a <-> b <-> c <-> d <-> e.` `struct` `Node* current = *head_ref;` `// current will either point to Nth` `// or NULL after this loop. Current ` `// will point to node 'b' in the` ] `// above example` `int` `count = 1;` `while` `(count < N && current != NULL) {` `current = current->next;` `count++;` `}` `// If current is NULL, N is greater` `// than or equal to count of nodes` `// in linked list. Don't change the ` `// list in this case` `if` `(current == NULL)` `return` `;` `// current points to Nth node. Store ` `// it in a variable. NthNode points to` `// node 'b' in the above example` `struct` `Node* NthNode = current;` `// current will point to last node`[HTG9 9] `// after this loop current will point ` `// to node 'e' in the above example` `while` `(current->next != NULL)` `current = current->next;` `// Change next of last node to previous` `// head. Next of 'e' is now changed to` `// node 'a'` `current->next = *head_ref;` `// Change prev of Head node to current` `// Prev of 'a' is now changed to node 'e'` `(*head_ref)->prev = current;`[ `// Change head to (N+1)th node` `// head is now changed to node 'c'` `*head_ref = NthNode->next;` `// Change prev of New Head node to NULL` `// Because Prev of Head Node in Doubly ` `// linked list is NULL` `(*head_ref)->prev = NULL;` `// change next of Nth node to NULL` `// next of 'b' is now NULL` 46]`}``// Function to insert a node at the``// beginning of the Doubly Linked List` `void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->prev = NULL;` `new_node->next = (*head_ref);` `if` `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` `*head_ref = new_node;``}``/* Function to print linked list */``void` `printList(` `struct` `Node* node)``{` `while` `(node->next != NULL) {` `cout << node->data <<` `" "` `<<` `"<=>"` `<<` `" "` `;` `node = node->next;` `}` `cout << node->data;``}``// Driver's Code``int` `main(` `void` `)``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `/* Let us create the doubly ` `linked list a<->b<->c<->d<->e */` `push(&head,` `'e'` `);` `push(&head,` `'d'` `);` `push(&head,` `'c'` `);` `push(&head,` `'b'` `);` `push(&head,` `'a'` `);` `int` `N = 2;` `cout <<` `"Given linked list \n"` `;`[H TG510]  `printList(head);` `rotate(&head, N);` `cout <<` `"\nRotated Linked list \n"` `;` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*