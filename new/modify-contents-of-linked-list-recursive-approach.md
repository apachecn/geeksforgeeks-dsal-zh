# 修改链接列表的内容-递归方法

给定一个包含 **n** 个节点的单链列表。 修改前半个节点的值，以使第一个节点的新值等于最后一个节点的值减去第一个节点的当前值，第二个节点的新值等于后一个节点的值减去第二个节点的当前值，对于前半个节点也是如此。 如果 **n** 为奇数，则中间节点的值保持不变。

**示例：**

> **输入：** 10-> 4-> 5-> 3-> 6
> **输出：** -4-> -1-> 5-> 3-> 6
> 
> **输入：** 2-> 9-> 8-> 12-> 7-> 10
> **输出：** 8-> -2-> 4-> 12-> 7-> 10

**方法：**仅对列表的后半部分使用递归遍历链接列表，而不是对整个列表进行递归，从而减少了堆栈帧。 根据列表中的节点数，我们计算列表后半部分的起点，然后将列表递归到后半部分。 一旦后半部分完全递归，就减去堆栈中存在的节点的值和当前节点的值。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to modify the contents``// of the linked list with recursion``#include <bits/stdc++.h>``using` `namespace` `std;``// Represents a Node of the linked list``struct` `Node {` `int` `data;` `Node* next;``};``// Function to create and return a new node``Node* insert(` `int` `data)``{` `Node* temp;` `temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``// Function which returns the total number of ``// node present in the list``int` `getTotalNodeCount(Node* head)`​​ `{` `int` `totalNodesCount = 0;`[HTG2 74]  `while` `(head != NULL)` `{` `totalNodesCount++;` `head = head->next;` `}` `return` `totalNodesCount;``}` [`// Function to modify the contents``// of the given linked lists``void` `modifyContents(Node** first_half , ` `Node* second_half) ``{` `if` `(second_half == NULL)` `{` `return` `;` `}` `modifyContents(first_half,second_half->next);` `(*first_half)->data = second_half->data - (*first_half)->data;` `(*first_half) = (*first_half)->next;` `return` `;``}`。`// Wrapper function which calculates the starting ``// point for second half of the list``void` `modifyContentsWrapper(Node** head)``{` `Node *ptr = NULL;` `// pointer to second half of list` `Node *temp = NULL; ` `int` `diff = 0; ` `int` `length = 0;` `// number of nodes in the list` `if` `(*head == NULL)` `{` `return` `;` `}` `length = getTotalNodeCount(*head);` `// If link list has odd number of nodes, then pointer ` `// for second half starts from (length of link list + 1).` `// Say for an example, for the list 10->4->5->3->6 pointer ` `// should start from 3\.` `// If list has even number of nodes, 10->4->5->9->6->8, ` `// pointer starts from 9\.` `diff = (length%2 == 0? (length/2) :(length/2)+1 );` TG142] `while` `(diff--)` `ptr = ptr->next;` `temp = *head;` `modifyContents(&temp,ptr);` `return` `;`] `}` [`// Function to print the contents of the linked list``void` `print(Node* nod)``{` `if` `(nod == NULL) {` `return` `;` `}`的 `cout << nod->data;` `if` `(nod->next != NULL)` `cout <<` `" -> "` `;`] `print(nod->next);``}` [HTG4 27]`// Driver code``int` `main()``{` `Node* head = insert(2);` `head->next = insert(9);` `head->next->next = insert(8);` `head->next->next->next = insert(12);` `head->next->next->next->next = insert(7);` `head->next->next->next->next->next = insert(10);` `// Modify the linked list` `modifyContentsWrapper(&head);` `// Print the modified linked list` `print(head);` `return` `0;``}` |

*chevron_right**filter_none*