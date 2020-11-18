# 在给定约束下删除链接列表中的给定节点

给定一个单链列表，编写一个删除给定节点的函数。 您的函数必须遵循以下约束：
1）它必须接受指向起始节点的指针作为第一个参数，并接受要删除的节点作为第二个参数，即，指向头节点的指针不是全局的。
2）它不应返回指向头节点的指针。
3）它不应接受指向头节点的指针。

您可以假定“链接列表”永远不会为空。

让函数名称为deleteNode（）。 在一个简单的实现中，当要删除的节点是第一个节点时，该函数需要修改头指针。 如[上一篇文章](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)所讨论的，当函数修改头指针时，该函数必须使用给定方法的[中的一种，此处我们无法使用任何一种方法。](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)

**解决方案**
我们明确处理要删除的节点是第一个节点的情况，我们将下一个节点的数据复制到头部，然后删除下一个节点。 可以通过找到上一个节点并更改下一个下一个节点来正常处理被删除节点不是头节点的情况。 以下是实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to delete a given node``// in linked list under given constraints``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* structure of a linked list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``void` `deleteNode(Node *head, Node *n) ``{ ` `// When node to be deleted is head node `​​ `if` `(head == n) ` `{ ` `if` `(head->next == NULL) ` `{ ` `cout <<` `"There is only one node."` `<<` `" The list can't be made empty "` `; ` `return` `; ` `} ` [HTG5 0] `head->data = head->next->data; ` `// store address of next node ` `n = head->next; ` `// Remove the link of next node ` `head->next = head->next->next; ` `// free memory` ] `free` `(n); ` `return` `; ` `} ` `// When not first node, follow ` `// the normal deletion process ` `// find the previous node ` `Node *prev = head; ` `while` `(prev->next != NULL && prev->next != n) ` `prev = prev->next; ` `// Check if node really exists in Linked List ` `if` `(prev->next == NULL) ` `{ ` `cout <<` `"\nGiven node is not present in Linked List"` `; ` `return` `; ` `} ` `// Remove node from Linked List ` `prev->next = prev->next->next; ` `// Free memory ` `free` `(n); ` `return` `; ``} ``/* Utility function to insert a node at the beginning */``void` `push(Node **head_ref,` `int` `new_data) ``{ ` `Node *new_node =` `new` `Node();` `new_node->data = new_data; ` `new_node->next = *head_ref; ` `*head_ref = new_node; ``} ``/* Utility function to print a linked list */``void` `printList(Node *head) ``{ ` `while` `(head!=NULL) ` `{ ` `cout<<head->data<<` `" "` `; ` `head=head->next; ` `} ` `cout<<endl;``} ``/* Driver code */``int` `main() ``{ ` `Node *head = NULL; `[HTG170 `/* Create following linked list ` `12->15->10->11->5->6->2->3 */` `push(&head,3); ` `push(&head,2); ` `push(&head,6); ` `push(&head,5); ` `push(&head,11); ` `push(&head,10); ` `push(&head,15); ` `push(&head,12); ` `cout<<` `"Given Linked List: "` `; ` `printList(head); ` `/* Let us delete the node with value 10 */` `cout<<` `"\nDeleting node "` `<< head->next->next->data<<` `" "` `; ` `deleteNode(head, head->next->next); ` `cout<<` `"\nModified Linked List: "` `; ` `printList(head); ` `/* Let us delete the first node */` `cout<<` `"\nDeleting first node "` `; ` `deleteNode(head, head); ` `cout<<` `"\nModified Linked List: "` `; ` `printList(head); ` `return` `0; ``} ` [`// This code is contributed by rathbhupendra`[ |

*chevron_right**filter_none*