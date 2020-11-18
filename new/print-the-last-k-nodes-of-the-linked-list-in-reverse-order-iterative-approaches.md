# 以相反的顺序打印链接列表的最后k个节点| 迭代方法

给定一个包含N个节点和正整数K的链表，其中K应当小于或等于N。任务是按相反的顺序打印列表的最后K个节点。

**示例：**

```
Input : list: 1->2->3->4->5, K = 2
Output : 5 4

Input : list: 3->10->6->9->12->2->8, K = 4
Output : 8 2 12 9

```

[先前的文章](https://www.geeksforgeeks.org/print-the-last-k-nodes-of-the-linked-list-in-reverse-order/)中讨论的解决方案使用递归方法。 下面的文章讨论了解决上述问题的三种迭代方法。

**方法1：**的想法是使用堆栈数据结构。 推送所有链接的列表节点数据值以堆叠并弹出前K个元素并打印它们。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to print the last k nodes``// of linked list in reverse order``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Structure of a node``struct` `Node {` `int` `data;` `Node* next;``};``// Function to get a new node``Node* getNode(` `int` `data)``{` `// allocate space` `Node* newNode =` `new` `Node;` `// put in data` `newNode->data = data;` `newNode->next = NULL;` `return` `newNode;``}``// Function to print the last k nodes``// of linked list in reverse order``void` `printLastKRev(Node* head,` `int` `k)``{` `// if list is empty` `if` `(!head)` `return` `;`的 `// Stack to store data value of nodes.` `stack<` `int` `> st;` `// Push data value of nodes to stack` `while` `(head) {` `st.push(head->data);` `head = head->next;` `}` `int` `cnt = 0;` `// Pop first k elements of stack and` `// print them.` `while` `(cnt < k) {` `cout << st.top() <<` `" "` `;` `st.pop();` `cnt++;` `}``}``// Driver code` [HTG2 32]`int` `main()``{` `// Create list: 1->2->3->4->5` `Node* head = getNode(1);` `head->next = getNode(2);` `head->next->next = getNode(3);` `head->next->next->next = getNode(4);` `head->next->next->next->next = getNode(5);` [ `int` `k = 4;` `// print the last k nodes` `printLastKRev(head, k);` `return` `0;``}` |

*chevron_right**filter_none*