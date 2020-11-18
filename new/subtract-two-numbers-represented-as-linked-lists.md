# 减去两个表示为链接列表的数字

给定两个表示两个大正数的链表。 从较大的数字中减去较小的数字，然后将差值作为链表返回。 请注意，输入列表可以按任何顺序排列，但是我们始终需要从较大的列表中减去较小的列表。

可以假设输入列表中没有多余的前导零。

**示例：**

```
Input: l1 = 1 -> 0 -> 0 -> NULL,  l2 = 1 -> NULL
Output: 0->9->9->NULL
Explanation: Number represented as 
lists are 100 and 1, so 100 - 1 is 099

Input: l1 = 7-> 8 -> 6 -> NULL,  l2 = 7 -> 8 -> 9 NULL
Output: 3->NULL
Explanation: Number represented as 
lists are 786 and  789, so 789 - 786 is 3, 
as the smaller value is subtracted from 
the larger one.

```

<u>**方法**</u> ：以下是步骤。

1.  计算给定两个链表的大小。
2.  如果大小不相同，则将零添加到较小的链表中。
3.  如果大小相同，请执行以下步骤：
    1.  找到价值较小的链表。
    2.  从较大的链表中逐一减去较小链表的节点。 减去时要跟踪借用。

以下是上述方法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to subtract smaller valued list from``// larger valued list and return result as a list.``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A linked List Node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// A utility which creates Node.``Node* newNode(` `int` `data)``{` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``/* A utility function to get length` `of linked list */``int` `getLength(Node* Node)``{` `int` `size = 0;` `while` `(Node != NULL) {` `Node = Node->next;` `size++;` `}` `return` `size;``}``/* A Utility that padds zeros in front of the` `Node, with the given diff */``Node* paddZeros(Node* sNode,` `int` `diff)``{` `if` `(sNode == NULL)` `return` `NULL;`的 `Node* zHead = newNode(0);` `diff--;` `Node* temp = zHead;` `while` `(diff--) {` `temp->next = newNode(0);` `temp = temp->next;` `}` `temp->next = sNode;` `return` `zHead;``}``/* Subtract LinkedList Helper is a recursive function,` `move till the last Node,  and subtract the digits and`[H TG444]  `create the Node and return the Node. If d1 < d2, we` `borrow the number from previous digit. */``Node* subtractLinkedListHelper(Node* l1, Node* l2,` `bool` `& borrow)``{` `if` `(l1 == NULL && l2 == NULL && borrow == 0)` `return` `NULL;` `Node* previous` `= subtractLinkedListHelper(` `l1 ? l1->next : NULL,` `l2 ? l2->next : NULL, borrow);` `int` `d1 = l1->data;` `int` `d2 = l2->data;` `int` `sub = 0;` `/* if you have given the value value to next digit then` `reduce the d1 by 1 */` `if` `(borrow) {` `d1--;` `borrow =` `false` `;` `}` `/* If d1 < d2, then borrow the number from previous digit.` `Add 10 to d1 and set borrow = true; */` `if` `(d1 < d2) {` `borrow =` `true` `;` `d1 = d1 + 10;` `}` `/* subtract the digits */`]  `sub = d1 - d2;` `/* Create a Node with sub value */` `Node* current = newNode(sub);` HTG515] `/* Set the Next pointer as Previous */` `current->next = previous;` `return` `current;``}``/* This API subtracts two linked lists and returns the` `linked list which shall  have the subtracted result. */``Node* subtractLinkedList(Node* l1, Node* l2)``{` `// Base Case.` `if` `(l1 == NULL && l2 == NULL)` `return` `NULL;` `// In either of the case, get the lengths of both` `// Linked list.` `int` `len1 = getLength(l1);` `int` `len2 = getLength(l2);` `Node *lNode = NULL, *sNode = NULL;` HTG557] `Node* temp1 = l1;` `Node* temp2 = l2;` `// If lengths differ, calculate the smaller Node` `// and padd zeros for smaller Node and ensure both` `// larger Node and smaller Node has equal length.` `if` `(len1 != len2) {` `lNode = len1 > len2 ? l1 : l2;` `sNode = len1 > len2 ? l2 : l1;` `sNode = paddZeros(sNode,` `abs` `(len1 - len2));` `}` `else` `{` `// If both list lengths are equal, then calculate` `// the larger and smaller list. If 5-6-7 & 5-6-8` `// are linked list, then walk through linked list` `// at last Node as 7 < 8, larger Node is 5-6-8` `// and smaller Node is 5-6-7\.` `while` `(l1 && l2) {` `if` `(l1->data != l2->data) {` `lNode = l1->data > l2->data ? temp1 : temp2;` `sNode = l1->data > l2->data ? temp2 : temp1;` `break` `;` `}` `l1 = l1->next;` `l2 = l2->next;` `}` ​​ `}` `// After calculating larger and smaller Node, call` `// subtractLinkedListHelper which returns the subtracted` `// linked list.` `bool` `borrow =` `false` `;` `return` `subtractLinkedListHelper(lNode, sNode, borrow);``}` ]`/* A utility function to print linked list */``void` `printList(` `struct` `Node* Node)`[HT G634] `{` `while` `(Node != NULL) {` `printf` `(` `"%d "` `, Node->data);` `Node = Node->next;` `}` `printf` `(` `"\n"` `);``}` [`// Driver program to test above functions``int` `main()``{` `Node* head1 = newNode(1);` `head1->next = newNode(0);` `head1->next->next = newNode(0);` `Node* head2 = newNode(1);` `Node* result = subtractLinkedList(head1, head2);` `printList(result);` ] `return` `0;``}` |

*chevron_right**filter_none*