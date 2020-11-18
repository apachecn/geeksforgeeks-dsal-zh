# 将最后m个元素移到给定链接列表

的前面

给定[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)的**头**和值 **m** ，任务是将最后m个元素移到最前面。

**示例：**

> **输入：** 4- > 5- > 6- > 1- > 2- > 3； m = 3
> **输出：** 1- > 2- > 3- > 4- > 5- > 6
> 
> **输入：** 0- > 1- > 2- > 3- > 4- > 5； m = 4
> **输出：** 2- > 3- > 4- > 5- > 0- > 1

**算法：**

1.  使用两个指针：一个用于存储最后一个节点的地址，另一个用于存储第一个节点的地址。
2.  遍历列表，直到最后m个节点中的第一个节点。
3.  保持两个指针p，q，即p作为最后m个节点的第一个节点，q保持在p的节点之前。
4.  将最后一个节点作为原始列表的头。
5.  将节点q的下一个设为NULL。
6.  将p设置为头部。

下面是上述方法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to move last m elements``// to front in a given linked list``#include <iostream>``using` `namespace` `std;` [`// A linked list node``struct` `Node ``{` `int` `data;` `struct` `Node* next;``} * first, *last;``int` `length = 0;``// Function to print nodes``// in a given linked list``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) ` `{`​​  `cout << node->data <<` `" "` `;` `node = node->next;` `}``}``// Pointer head and p are being``// used here because, the head`[HTG2 84] `// of the linked list is changed in this function.``void` `moveToFront(` `struct` `Node* head,` `struct` `Node* p,` `int` `m)``{` `// If the linked list is empty,` `// or it contains only one node,` `// then nothing needs to be done, simply return` `if` `(head == NULL)` `return` `;` `p = head;` `head = head->next;` `m++;` `// if m value reaches length,` `// the recursion will end` `if` `(length == m)` `{` `// breaking the link` `p->next = NULL;` `// connecting last to first &` `// will make another node as head` `last->next = first;`[H TG334]  `// Making the first node of` `// last m nodes as root` `first = head;` `}` `else` `moveToFront(head, p, m);``}``// UTILITY FUNCTIONS``// Function to add a node at``// the beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `// allocate node` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` [ `// link the old list off the new node` `new_node->next = (*head_ref);` `// move the head to point to the new node` `(*head_ref) = new_node;` [ `// making first & last nodes` `if` `(length == 0)` `last = *head_ref;` `else` `first = *head_ref;` `// increase the length` `length++;``}``// Driver code``int` `main()``{` `struct` `Node* start = NULL;` `// The constructed linked list is:` `// 1->2->3->4->5` `push(&start, 5);` `push(&start, 4);` `push(&start, 3);` [HTG19 2] `push(&start, 1);` `push(&start, 0);` `cout <<` `"Initial Linked list\n"` `;` `printList(start);` `int` `m = 4;` `// no.of nodes to change` `struct` `Node* temp;` `moveToFront(start, temp, m);` `cout <<` `"\n Final Linked list\n"` `;` `start = first;` `printList(start);` `return` `0;``}``// This code is contributed by SHUBHAMSINGH10` |

*chevron_right**filter_none*