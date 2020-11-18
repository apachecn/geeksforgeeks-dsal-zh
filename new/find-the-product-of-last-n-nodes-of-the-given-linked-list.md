# 查找给定链接列表

的最后N个节点的乘积

给定一个链表和一个数字N。找到链表的最后n个节点的乘积。

**约束：** 0 < = N < =链表中的节点数。

**范例**：

```
Input : List = 10->6->8->4->12, N = 2
Output : 48
Explanation : Product of last two nodes:
              12 * 4 = 48

Input : List = 15->7->9->5->16->14, N = 4
Output : 10080
Explanation : Product of last four nodes:
              9 * 5 * 16 * 14 = 10080

```

**方法1 ：（使用用户定义的堆栈的迭代方法）**从左到右遍历节点。 遍历时将节点推送到用户定义的堆栈。 然后从堆栈中弹出前n个值，并找到其乘积。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find the product of last``// 'n' nodes of the Linked List``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `new` `Node;` `/* put in the data  */` `new_node->data = new_data;` `/* link the old list to the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// utility function to find the product of last 'n' nodes``int` `productOfLastN_NodesUtil(` `struct` `Node* head,` `int` `n)``{` `// if n == 0` `if` `(n <= 0)` `return` `0;` `stack<` `int` `> st;` `int` `prod = 1;` `// traverses the list from left to right` `while` `(head != NULL) {` `// push the node's data onto the stack 'st'` `st.push(head->data);` `// move to next node` `head = head->next;` `}` `// pop 'n' nodes from 'st' and` `// add them` `while` `(n--) {` `prod *= st.top();` `st.pop();` `}` `// required product` `return` `prod;``}``// Driver program to test above``int` `main()``{`​​  `struct` `Node* head = NULL;` `// create linked list 10->6->8->4->12` `push(&head, 12);` `push(&head, 4);` `push(&head, 8);` `push(&head, 6);` `push(&head, 10);` `int` `n = 2;` `cout << productOfLastN_NodesUtil(head, n);` `return` `0;``}` |

*chevron_right**filter_none*