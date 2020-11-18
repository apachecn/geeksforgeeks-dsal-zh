# 删除左侧

值较小的链表节点

给定一个单链列表，任务是删除左侧值较小的所有节点。

**示例：**

```
Input: 12->15->10->11->5->6->2->3
Output: Modified Linked List = 12 -> 10 -> 5 -> 2 

Input: 25->15->6->48->12->5->16->14
Output: Modified Linked List = 25 -> 15 -> 6 -> 5   

```

**方法：**

1.  用头节点初始化变量*最大值*。
2.  遍历列表。
3.  检查下一个节点是否小于max_node。 如果是，则移至下一个节点。
4.  否则，则更新max_node的值并删除下一个节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of above approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Structure of a linked list node` ]`struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to Delete nodes which have``// greater value node(s) on right side``void` `delNodes(` `struct` `Node* head)``{` `struct` `Node* current = head;` `// Initialize max` ] `struct` `Node* maxnode = head;` `struct` `Node* temp;` `while` `(current != NULL && current->next != NULL) {` `// If current is greater than max,` `// then update max and move current` `if` `(current->next->data <= maxnode->data) {` `current = current->next;` `maxnode = current;` `}` `// If current is smaller than max, then delete current` `else` `{` `temp = current->next;` `current->next = temp->next;` `free` `(temp);` `}` `}``}``/* Utility function to insert a node at the beginning */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = *head_ref;` `*head_ref = new_node;``}``/* Utility function to print a linked list */``void` `printList(` `struct` `Node* head)``{`]  `while` `(head != NULL) {`​​  `cout << head->data <<` `" "` `;` `head = head->next;` `}` `cout << endl;``}``/* Driver program to test above functions */``int` `main()`]`{` `struct` `Node* head = NULL;` `/* Create following linked list ` `12->15->10->11->5->6->2->3 */` `push(&head, 3);` `push(&head, 2);` `push(&head, 6);` `push(&head, 5);` `push(&head, 11);` `push(&head, 10);` `push(&head, 15);` `push(&head, 12);` `printf` `(` `"Given Linked List: "` `);` `printList(head);` `delNodes(head);` `printf` `(` `"\nModified Linked List: "` `);` `printList(head);` `return` `0;``}`] |

*chevron_right**filter_none*