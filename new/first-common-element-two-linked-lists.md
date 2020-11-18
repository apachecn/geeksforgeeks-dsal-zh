# 两个链接列表中的第一个公共元素

给定两个链表，找到给定链表之间的第一个公共元素，即我们需要找到第一个链表的第一个节点，该节点也存在于第二个链表中。
**范例：**

```
Input :  
   List1: 10->15->4->20
   Lsit2:  8->4->2->10
Output : 10

Input : 
   List1: 1->2->3->4
   Lsit2:  5->6->3->8
Output : 3

```

我们遍历第一个列表，对于每个节点，我们在第二个列表中搜索它。 一旦在第二个列表中找到一个元素，就将其返回。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find first common element in``// two unsorted linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* A utility function to insert a node at the ` `beginning of a linked list*/``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node = ` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``/* Returns the first repeating element in linked list*/``int` `firstCommon(` `struct` `Node* head1,` `struct` `Node* head2)``{` `// Traverse through every node of first list` `for` `(; head1 != NULL; head1=head1->next)` `// If current node is present in second list` `for` `(Node *p = head2; p != NULL; p = p->next)` `if` `(p->data == head1->data)` `return` `head1->data;` `// If no common node` `return` `0;``}``// Driver code``int` `main()``{` `struct` `Node* head1 = NULL;` `push(&head1, 20);` `push(&head1, 5);` `push(&head1, 15);` `push(&head1, 10);` `struct` `Node* head2 = NULL;` `push(&head2, 10);` `push(&head2, 2);` [H TG214] `push(&head2, 15);` `push(&head2, 8);` `cout << firstCommon(head1, head2);` `return` `0;``}` |

*chevron_right**filter_none*