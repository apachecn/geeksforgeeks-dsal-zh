# 以相反的顺序打印链接列表的最后k个节点| 递归方法

给定一个包含 **N个**节点和正整数 **k** 的链表应小于或等于N。任务是打印该节点的最后 **k** 个节点。 以相反的顺序列出。

**示例：**

```
Input: list: 1->2->3->4->5, k = 2                       
Output: 5 4

Input: list: 3->10->6->9->12->2->8, k = 4 
Output: 8 2 12 9

```

**来源：** [校园外Amazon Interview Experience SDE](https://www.geeksforgeeks.org/amazon-interview-experience-sde-off-campus/) 。

**递归方法：**递归遍历链表。 从每个递归调用返回时，请跟踪节点编号，将最后一个节点视为编号1，将倒数第二个节点视为编号2，依此类推。 可以借助全局变量或指针变量来跟踪此计数。 借助此count变量，打印节点号小于或等于 **k** 的节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to print the last k nodes``// of linked list in reverse order``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Structure of a node``struct` `Node {` `int` `data;` `Node* next;``};``// Function to get a new node``Node* getNode(` `int` `data)``{` `// allocate space` `Node* newNode =` `new` `Node;` `// put in data` ] `newNode->data = data;` `newNode->next = NULL;` `return` `newNode;``}``// Function to print the last k nodes``// of linked list in reverse order``void` `printLastKRev(Node* head,` `int` `& count,` `int` `k)``{` `// if list is empty` `if` `(!head)` `return` `;` [ `// Recursive call with the next node` `// of the list` `printLastKRev(head->next, count, k);` `// Count variable to keep track of` `// the last k nodes` `count++;` `// Print data` `if` `(count <= k)` `cout << head->data <<` `" "` `;``}``// Driver code``int` `main()``{` `// Create list: 1->2->3->4->5` `Node* head = getNode(1);` `head->next = getNode(2);` `head->next->next = getNode(3);` `head->next->next->next = getNode(4);` `head->next->next->next->next = getNode(5);` `int` `k = 4, count = 0;` `// print the last k nodes` `printLastKRev(head, count, k);` `return` `0;``}` |

*chevron_right**filter_none*