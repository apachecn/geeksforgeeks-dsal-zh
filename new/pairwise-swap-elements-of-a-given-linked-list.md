# 给定链表

的成对交换元素

给定一个单链表，编写一个函数以成对交换元素。

> 输入：1-> 2-> 3-> 4-> 5-> 6-> NULL
> 输出：2- > 1- > 4- > 3- > 6- > 5- >空
> 
> 输入：1-> 2-> 3-> 4-> 5-> NULL
> 输出：2- > 1- > 4- > 3- > 5- > NULL
> 
> 输入：1-> NULL
> 输出：1- > NULL

例如，如果链接列表为1-> 2-> 3-> 4-> 5，则函数应将其更改为2-> 1-> 4-> 3-> 5，如果链接列表为 函数应将其更改为。

**方法1（迭代）**
从头节点开始，遍历列表。 在遍历每个节点的交换数据及其下一个节点的数据时。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to pairwise swap elements``// in a given linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A linked list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* Function to pairwise swap elements``of a linked list */``void` `pairWiseSwap(Node* head)``{` `Node* temp = head;` `/* Traverse further only if ` `there are at-least two nodes left */` `while` `(temp != NULL && temp->next != NULL) {` `/* Swap data of node with ` `its next node's data */` `swap(temp->data,` `temp->next->data);` `/* Move temp by 2 for the next pair */` `temp = temp->next->next;` `}``}``/* Function to add a node at the ` `beginning of Linked List */``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point `] `to the new node */` `(*head_ref) = new_node;``}``/* Function to print nodes` `in a given linked list */``void` `printList(Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `node = node->next;` `}`​​ `}` [`// Driver Code``int` `main()``{` `Node* start = NULL;` `/* The constructed linked list is: ` `1->2->3->4->5 */` `push(&start, 5);` `push(&start, 4);` `push(&start, 3);` `push(&start, 2);` `push(&start, 1);`] `cout <<` `"Linked list "` `<<` `"before calling pairWiseSwap()\n"` `;` `printList(start);` `pairWiseSwap(start);` `cout <<` `"\nLinked list "` `<<` `"after calling pairWiseSwap()\n"` `;` `printList(start);` `return` `0;``}``// This code is contributed``// by rathbhupendra` |

*chevron_right**filter_none*