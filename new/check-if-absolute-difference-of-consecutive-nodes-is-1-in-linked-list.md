# 检查链接列表

中连续节点的绝对差是否为1

给定一个单链表。 任务是检查链接列表中连续节点之间的绝对差是否为1。

**示例：**

> **输入：**列表= 2- > 3- > 4- > 5- > 4- > 3- > 2- > 1- > NULL
> **输出：**是
> **说明：**列表中相邻节点之间的差为1。因此，给定的列表是一个跳线序列。
> 
> **输入：**列表= 2- > 3- > 4- > 5- > 3- > 4- >空
> **输出：[** 否

**简单方法**：

1.  用一个临时指针遍历列表。
2.  将标志变量初始化为true，指示连续节点的绝对差为1。
3.  开始遍历列表。
4.  检查连续节点的绝对差是否为1。
5.  如果是，则继续遍历，否则将标志变量更新为零并停止进一步遍历。
    返回标志。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to check if absolute difference``// of consecutive nodes is 1 in Linked List``#include <bits/stdc++.h>``using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Utility function to create a new Node``Node* newNode(` `int` `data)``{` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``// Function to check if absolute difference``// of consecutive nodes is 1 in Linked List``bool` `isConsecutiveNodes(Node* head)``{` `// Create a temporary pointer`[HT G45] `// to traverse the list` `Node* temp = head;` `// Initialize a flag variable` `int` `f = 1;` `// Traverse through all the nodes` `// in the list` `while` `(temp) {` `if` `(!temp->next)` `break` `;` `// count the number of jumper sequence` `if` `(` `abs` `((temp->data) - (temp->next->data)) != 1) {` `f = 0;` `break` `;` `}` `temp = temp->next;` `}` `// return flag` `return` `f;``}` [`// Driver code``int` `main()``{` `// creating the linked list` `Node* head = newNode(2);` `head->next = newNode(3);` `head->next->next = newNode(4);` `head->next->next->next = newNode(5);` `head->next->next->next->next = newNode(4);` `head->next->next->next->next->next = newNode(3);` `head->next->next->next->next->next->next = newNode(2);` `head->next->next->next->next->next->next->next = newNode(1);`​​  `if` `(isConsecutiveNodes(head))` `cout <<` `"YES"` `;` `else` `cout <<` `"NO"` `;` `return` `0;``}`[ |

*chevron_right**filter_none*