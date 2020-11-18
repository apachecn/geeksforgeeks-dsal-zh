# 在单遍历中查找链表的倒数第二个节点

给定一个链表。 任务是仅使用单个遍历查找链表的倒数第二个节点。

**示例：**

> **输入**：列表= 1-> 2-> 3-> 4-> 5->空
> **输出**：4
> 
> **输入**：列表= 2-> 4-> 6-> 8-> 33-> 67->空
> **输出**：33

想法是按照以下方法遍历链表：

1.  如果列表为空或包含少于2个元素，则返回false。
2.  否则，请检查当前节点是否为链表的倒数第二个节点。 也就是说，**如果（current_node- > next-next == NULL）**，则当前节点为倒数第二个节点。
3.  如果当前节点是倒数第二个节点，请打印该节点，否则移至下一个节点。
4.  重复上述两个步骤，直到到达倒数第二个节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find the second last node``// of a linked list in single traversal``#include <iostream>``using` `namespace` `std;``// Link list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to find the second last``// node of the linked list``int` `findSecondLastNode(` `struct` `Node* head)``{` `struct` `Node* temp = head;`的 `// If the list is empty or contains less` `// than 2 nodes` `if` `(temp == NULL &#124;&#124; temp->next == NULL)` `return` `-1;` `// Traverse the linked list` `while` `(temp != NULL) {`[HT G47] `// Check if the current node  is the` `// second last node or not` `if` `(temp->next->next == NULL)` `return` `temp->data;` `// If not then move to the next node` `temp = temp->next;` `}``}``// Function to push node at head``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Driver code``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` [ `/* Use push() function to construct ` `the below list 8 -> 23 -> 11 -> 29 -> 12 */` `push(&head, 12);` `push(&head, 29);` `push(&head, 11);` `push(&head, 23);` `push(&head, 8);` `cout << findSecondLastNode(head);` `return` `0;``}` |

*chevron_right**filter_none*