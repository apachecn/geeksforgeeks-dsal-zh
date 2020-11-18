# 编写删除链接列表的功能

**用于C / C ++的算法：**遍历链接列表，并一一删除所有节点。 这里的要点是，如果删除了当前指针，则不要访问当前指针的下一个指针。

在 **Java** 中，会发生自动垃圾收集，因此删除链接列表很容易。 我们只需要将head更改为null。

**实施：**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to delete a linked list ``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next; ``}; ``/* Function to delete the entire linked list */``void` `deleteList(Node** head_ref) ``{ ``/* deref head_ref to get the real head */``Node* current = *head_ref; ``Node* next; ` [`while` `(current != NULL) ``{ ` `next = current->next;` HTG35] `(current); ` `current = next; ``} ``/* deref head_ref to affect the real head back ` [HT G43]`*head_ref = NULL; ``} ``/* Given a reference (pointer to pointer) to the head ``of a list and an int, push a new node on the front ``of the list. */``void` `push(Node** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``/* Driver code*/``int` `main()` ]`{ ` `/* Start with the empty list */` `Node* head = NULL; `[  `/* Use push() to construct below list ` `1->12->1->4->1 */` `push(&head, 1); ` `push(&head, 4); ` `push(&head, 1); ` `push(&head, 12); ` `push(&head, 1); ` `cout <<` `"Deleting linked list"` [ `; ` `deleteList(&head); ` `cout <<` `"\nLinked list deleted"` `; ``} ` [`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*