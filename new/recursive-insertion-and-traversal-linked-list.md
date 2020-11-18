# 递归插入和遍历链表

我们讨论了[链表插入](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的不同方法。 如何递归地创建一个链表？

**递归插入到最后：**
要使用递归创建链接列表，请按照以下步骤操作。 下面的步骤在链表的末尾递归插入一个新节点。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Function to insert a new node at the``// end of linked list using recursion.``Node* insertEnd(Node* head,` `int` `data)``{` `// If linked list is empty, create a ` `// new node (Assuming newNode() allocates` `// a new node with given data)` `if` `(head == NULL) `[  `return` `newNode(data);` `// If we have not reached end, keep traversing``else` `head->next = insertEnd(head->next, data);` `return` `head;``}` |

*chevron_right**filter_none*

**递归遍历列表：**
这个想法很简单，我们打印当前节点，然后递归其余列表。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `void` `traverse(Node* head)``{` `if` `(head == NULL)` `return` `;` `// If head is not NULL, print current node` `// and recur for remaining list   ` `cout << head->data <<` `" "` `;` `traverse(head->next);``}` |

*chevron_right**filter_none*

**完整程序：**
下面是完整的程序，用于演示插入和遍历链表的工作。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Recursive CPP program to recursively insert``// a node and recursively print the list.``#include <bits/stdc++.h>``using` `namespace` `std;``struct` `Node {` `int` `data;` `Node* next;``};`的`// Allocates a new node with given data``Node *newNode(` `int` `data)``{` `Node *new_node =` `new` `Node;` `new_node->data = data;` `new_node->next = NULL;` `return` `new_node;``}``// Function to insert a new node at the``// end of linked list using recursion.``Node* insertEnd(Node* head,` `int` `data)``{` `// If linked list is empty, create a ` `// new node (Assuming newNode() allocates` `// a new node with given data)` `if` `(head == NULL) ` `return` `newNode(data);` `// If we have not reached end, keep traversing` `// recursively.` ] `else` [ `head->next = insertEnd(head->next, data);` `return` `head;``}``void` `traverse(Node* head)``{` `if` `(head == NULL)` `return` `;` `// If head is not NULL, print current node` `// and recur for remaining list   ` `cout << head->data <<` `" "` `;` `traverse(head->next);``}``// Driver code``int` `main()``{` `Node* head = NULL;` `head = insertEnd(head, 6);` [H TG97] `head = insertEnd(head, 10);` `head = insertEnd(head, 12);` `head = insertEnd(head, 14);` `traverse(head);``}` |

*chevron_right**filter_none*