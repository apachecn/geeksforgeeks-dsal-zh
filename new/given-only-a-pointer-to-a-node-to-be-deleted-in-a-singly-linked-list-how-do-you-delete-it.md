# 在单链列表中仅给定要删除节点的指针/引用，如何删除它？

给定要删除的节点的指针，请删除该节点。 请注意，我们没有指向头节点的指针。

**简单解决方案**是遍历链接列表，直到找到要删除的节点。 但是，此解决方案需要指向与问题陈述相矛盾的头节点的指针。

**快速解决方案**是将数据从下一个节点复制到要删除的节点，然后删除下一个节点。 像下面这样。

```
    // Find next node using next pointer
    struct Node *temp  = node_ptr->next;

    // Copy data of next node to this node
    node_ptr->data  = temp->data;

    // Unlink next node
    node_ptr->next  = temp->next;

    // Delete next node
    free(temp);

```

**程序：**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node {``public` `:` `int` `data;` `Node* next;``};``/* Given a reference (pointer to pointer) to the head ` `of a list and an int, push a new node on the front ` `of the list. */``void` `push(Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``void` `printList(Node* head)``{` `Node* temp = head;` `while` `(temp != NULL) {` `cout << temp->data <<` `" "` `;` `temp = temp->next;` `}``}``void` `deleteNode(Node* node)``{` `Node* prev;` `if` `(node == NULL)` `return` `;` `else` `{` `while` `(node->next != NULL) {` `node->data = node->next->data;` `prev = node;` `node = node->next;` `}` `prev->next = NULL;` `}``}` [[HTG25 3]`/* Driver code*/``int` `main()``{` `/* Start with the empty list */` `Node* head = NULL;` `/* Use push() to construct below list ` `1->12->1->4->1 */`​​  `push(&head, 1);` `push(&head, 4);` `push(&head, 1);` `push(&head, 12);` `push(&head, 1);`[ `cout <<` `"Before deleting \n"` `;` `printList(head);` `/* I m deleting the head itself. ` `You can check for more cases */` `deleteNode(head);` `cout <<` `"\nAfter deleting \n"` `;` `printList(head);` `return` `0;`[HTG14 6]，`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*