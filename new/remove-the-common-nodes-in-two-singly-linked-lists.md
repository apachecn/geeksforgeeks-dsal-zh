# 删除两个单链接列表中的公共节点

给定两个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/) **L1** 和 **L2** ，任务是从给定的两个链表中生成一个没有公共元素的新链表。

**示例：**

> **输入：** L1 = 10-> 15-> 5-> 20，L2 = 8-> 5-> 20-> 10
> **输出：** 8-> 15
> **说明：**
> 由于两个链表都有5、10和20的共同点。 因此，删除了这些元素，结果列表为8-> 15。
> 
> **输入：** L1 = 0-> 5-> 52-> 21，L2 = 21-> 5-> 0-> 52
> **输出：** []
> **说明：**
> 由于两个给定链表的所有元素都是相同的。 因此，结果链接为空。

**方法：**

1.  对于第一个链表中的每个元素（例如 **X** ）：
    *   遍历第二个链接列表并检查链接列表中是否存在 **X** 。
    *   如果不存在 **X** ，则在结果链接列表中插入 **X** ，因为这在两个链接列表中都不常见。
2.  对于第二个链表中的每个元素（例如 **Y** ）：
    *   遍历第一个链表，并检查链表中是否存在 **Y** 。
    *   如果不存在 **Y** ，则在结果链接列表中插入 **Y** ，因为这在两个链接列表中都不常见。
3.  结果链表将是必需的链表，给定两个链表中没有公共节点。

下面是上述方法的实现：

## CPP

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program for the above approach``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Link list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to print the element``// of the Linked List``void` `printList(` `struct` `Node* p)``{` `if` `(p == NULL) {`​​  `cout <<` `"[]"` `;` `}` `while` `(p != NULL) {` `cout << p->data <<` `" -> "` `;` `p = p->next;` `}``}``// Function to push the node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node` `= (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to insert unique``// elements in the new LL``void` `traverse(` `struct` `Node** head3,` `struct` `Node* temp1,` `struct` `Node* temp2)``{` `// Traverse the first linked list` `while` `(temp1 != NULL) {` `// Value of current node` `int` `val = temp1->data;` `struct` `Node* t = temp2;` `int` `x = 0;` `// Traverse the second list` `while` `(t != NULL) {` `if` `(t->data == val) {` `x = 1;` `break` `;` `}` `t = t->next;` `}` `// If element is not common` `// then insert it in the` `// resultant linked list` `if` `(x == 0) {` `push(head3, temp1->data);` `}` [ `temp1 = temp1->next;` `}``}``// Function to remove the common nodes``// in two Singly Linked Lists``void` `removeCommonNodes(` `struct` `Node* head1,` `struct` `Node* head2)``{` `// Head pointer for the resultant` `// linked list` `struct` `Node* head3 = NULL;` `// Find the node common between` `// linked list taking head1 as` `// first linked list` `traverse(&head3, head1, head2);` `// Find the node common between` `// linked list taking head2 as` `// first linked list` `traverse(&head3, head2, head1);` `// Print the resultant linked list` `printList(head3);``}``// Driver code`[H TG436] `int` `main()``{` `// First list` `struct` `Node* head1 = NULL;` `push(&head1, 20);` `push(&head1, 5);` `push(&head1, 15);` `push(&head1, 10);`[HTG213 `// Second list` `struct` `Node* head2 = NULL;` `push(&head2, 10);` `push(&head2, 20);` `push(&head2, 15);` `push(&head2, 8);` `// Function call` `removeCommonNodes(head1, head2);` `return` `0;``}` |

*chevron_right**filter_none*