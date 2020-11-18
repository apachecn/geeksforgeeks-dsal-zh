# 给定链接列表

中K个连续节点的最大和

给定一个链表，任务是找到通过将链表的任何k个连续节点相加而获得的最大和。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> NULL，K = 5
> **输出 ：** 20
> 通过将最后5个节点相加来获得最大和
> 
> **输入：** 2-> 5-> 3-> 6-> 4-> 1-> 7-> NULL，K = 4
> **输出：** 18

**方法：**这个想法是使用大小为k的滑动窗口，跟踪当前窗口的总和，并在需要时更新最大总和。 为了实现滑动窗口，可以使用两个指针来表示起点和终点。 在每个步骤中，首先从当前总和中减去由start指向的节点的值，然后将end所指向的节点的值添加到当前和。 将该总和与最大总和进行比较，并在需要时更新结果。 起始和结束指针在每一步都增加一个。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Structure of a node``struct` `Node {` `int` `data;` `Node* next;``};``// Function to create new node``Node* newNode(` `int` `data)``{` `Node* node =` `new` `Node;` `node->next = NULL;` `node->data = data;` `return` `node;``}``// Function to return the maximum sum of``// k consecutive nodes`HTG39]`{` `// To store current window sum` `int` `sum = 0;` `// To store maximum sum` `int` `maxSum = 0;` `// Pointer to the start of window` `Node* start = head;` `// Pointer to the end of window` `Node* end = head;`  `int` `i;` `// Find the sum of first k nodes` `for` `(i = 0; i < k; i++) {` `sum += end->data;` `end = end->next;` `}` `maxSum = sum;` `// Move window by one step and` `// update sum. Node pointed by` `// start is excluded from current` `// window so subtract it. Node` `// pointed by end is added to` `// current window so add its value.` `while` `(end != NULL) {` `// Subtract the starting element` `// from previous window` `sum -= start->data;` `start = start->next;` ]​​ `// Add the element next to the end` `// of previous window` `sum += end->data;` `end = end->next;` `// Update the maximum sum so far` `maxSum = max(maxSum, sum);` `}` `return` `maxSum;``}``// Driver code``int` `main()``{` `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);` `head->next->next->next = newNode(4);` `head->next->next->next->next = newNode(5);` `head->next->next->next->next->next = newNode(6);` `int` `k = 5;` `cout << findMaxSum(head, k);` ] `return` `0;``}` |

*chevron_right**filter_none*