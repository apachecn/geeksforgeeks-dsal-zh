# 链表

中所有小于K的节点的总和和积。

给定一个链表和一个密钥K。任务是计算总和并从列表中减去小于密钥K的所有节点。

**示例：**

> **输入：** 12-> 15-> 9-> 11-> 5-> 6，K = 9
> **输出：**总和 = 11，乘积= 30
> 
> **输入：** 13-> 4-> 16-> 9-> 22-> 45-> 5-> 16-> 6， K = 10
> **输出：**总和= 24，乘积= 1080

**方法：**从头开始遍历，检查当前节点的值是否小于K。如果是，则将该节点加到总和上并乘以该节点乘积，然后在列表中向前移动。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to sum and product all the``// nodes from the list that are lesser``// than the specified value K``#include <bits/stdc++.h>``using` `namespace` `std;``// structure of a node``struct` `Node {` `int` `data;` `Node* next;``};``// function to get a new node``Node* getNode(` `int` `data)``{` `Node* newNode =` `new` `Node;` `newNode->data = data;` `newNode->next = NULL;` `return` `newNode;``}``// function to sum all the nodes from the list``// that are lesser than the specified value K``int` `sumLesserNodes(Node** head_ref,` `int` `K)``{` `Node* temp = *head_ref;`[HTG1 88]  `int` `sum = 0;` `while` `(temp != NULL) {` `if` `(temp->data < K)` `sum += temp->data;` `temp = temp->next;` `}` `return` `sum;``}``// function to product all the nodes from the list``// that are lesser than the specified value K``int` `productLesserNodes(Node** head_ref,` `int` `K)``{` `Node* temp = *head_ref;` `int` `product = 1;` `while` `(temp != NULL) {` `if` `(temp->data < K)` `product *= temp->data;` `temp = temp->next;` `}` `return` `product;``}` [ [`// Driver code``int` `main()``{` `// Create list: 12->15->9->11->5->6` `Node* head = getNode(12);` `head->next = getNode(15);` `head->next->next = getNode(9);` `head->next->next->next = getNode(11);` `head->next->next->next->next = getNode(5);` `head->next->next->next->next->next = getNode(6);` `int` `K = 9;` ] `cout <<` `"Sum = "` `<< sumLesserNodes(&head, K) << endl;` `cout <<` `"Product = "` `<< productLesserNodes(&head, K) << endl;` [​​  `return` `0;``}` |

*chevron_right**filter_none*