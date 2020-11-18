# 在另一个位置将链接列表合并到另一个链接列表中

给定两个链接列表，将第二个列表的节点插入到第一个列表的第一个列表的备用位置。
例如，如果第一个列表是5-> 7- > 17- > 13- > 11，第二个列表是12- > 10- > 2- > 4- > 6，第一个列表应变为5- > 12- > 7- > 10- > 17- > 2- > 13- > 4 -> 11- > 6和第二个列表应该为空。 仅在有可用位置时才插入第二个列表的节点。 例如，如果第一个列表是1- > 2- > 3，第二个列表是4- > 5- > 6- > 7- > 8，则第一个列表应变为 1- > 4- > 2- > 5- > 3- > 6，第二个是7- > 8。

不允许使用额外的空间（不允许创建额外的节点），即，插入必须就地完成。 预期的时间复杂度为O（n），其中n是第一个列表中的节点数。

这个想法是在第一个循环中有可用位置时运行一个循环，并通过更改指针插入第二个列表的节点。 以下是此方法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to merge a linked list into another at ``// alternate positions ``#include <bits/stdc++.h>``using` `namespace` `std;`[HTG6`// A nexted list node ``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``/* Function to insert a node at the beginning */``void` `push(Node ** head_ref,` `int` `new_data) ``{ ` `Node* new_node =` `new` `Node();` `new_node->data = new_data; ` `new_node->next = (*head_ref); ` `(*head_ref) = new_node; ``} ` HTG214]`/* Utility function to print a singly linked list */``void` `printList(Node *head) ``{ ` `Node *temp = head; ` `while` `(temp != NULL) ` `{ ` `cout<<temp->data<<` `" "` `; ` `temp = temp->next; ` `} ` `cout<<endl;``} ``// Main function that inserts nodes of linked list q into p at ``// alternate positions. Since head of first list never changes ``// and head of second list may change, we need single pointer ``// for first list and double pointer for second list. ``void` `merge(Node *p, Node **q) ``{ ` `Node *p_curr = p, *q_curr = *q; ` `Node *p_next, *q_next; ` `// While therre are avialable positions in p ` `while` `(p_curr != NULL && q_curr != NULL) ` `{ ` `// Save next pointers ` `p_next = p_curr->next; ` `q_next = q_curr->next; `​​ `// Make q_curr as next of p_curr ` `q_curr->next = p_next;` `// Change next pointer of q_curr ` `p_curr->next = q_curr;` `// Change next pointer of p_curr `[HTG2 77]  `// Update current pointers for next iteration ` `p_curr = p_next; ` `q_curr = q_next; ` `} ` `*q = q_curr;` `// Update head pointer of second list ``} ``// Driver code ``int` `main() ``{ ` `Node *p = NULL, *q = NULL; ` `push(&p, 3); ` `push(&p, 2); ` `push(&p, 1); ` `cout<<` `"First Linked List:\n"` `; ` `printList(p); ` `push(&q, 8); ` `push(&q, 7); ` `push(&q, 6); ` `push(&q, 5); ` `push(&q, 4); ` `cout<<` `"Second Linked List:\n"` `; ` `printList(q); ` `merge(p, &q); ` `cout<<` ] `"Modified First Linked List:\n"` `; ` `printList(p); ` `cout<<` `"Modified Second Linked List:\n"` `; ` `printList(q); ` `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*