# 程序使用堆栈

来反向链接列表

给定一个链表。 任务是使用辅助堆栈反转链表元素的顺序。

**示例：**

```
Input : List = 3 -> 2 -> 1
Output : 1 -> 2 -> 3

Input : 9 -> 7 -> 4 -> 2
Output : 2 -> 4 -> 7 -> 9 

```

**算法**：

1.  遍历列表并将其所有节点压入堆栈。
2.  再次遍历头节点的列表，并从堆栈顶部弹出一个值，然后以相反的顺序连接它们。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C/C++ program to reverse linked list``// using stack``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Given a reference (pointer to pointer) to` `the head of a list and an int, push a new ` `node on the front of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to reverse linked list``Node *reverseList(Node* head)`[HTG4 7] `// Stack to store elements of list` `stack<Node *> stk;` `// Push the elements of list to stack` `Node* ptr = head;` `while` `(ptr->next != NULL) {` `stk.push(ptr);` `ptr = ptr->next;` `}` `// Pop from stack and replace` `// current nodes value'` `head = ptr;` `while` `(!stk.empty()) {` `ptr->next = stk.top();` `ptr = ptr->next;` `stk.pop();` `}` `ptr->next = NULL;` `return` `head;``}``// Function to print the Linked list` [`void` `printList(Node* head)``{` `while` `(head) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver Code`​​`int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `/* Use push() to construct below list ` `1->2->3->4->5 */` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);` `head = reverseList(head);` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*