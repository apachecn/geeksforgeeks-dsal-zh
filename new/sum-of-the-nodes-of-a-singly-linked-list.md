# 单链接列表

的节点总和

给定一个单链表。 任务是找到给定链表的节点总数。

![](img/d97a233bf3c89e80c46e6a3193e851d6.png)

任务是做A + B + C +D。

**Examples:**

```
Input: 7->6->8->4->1
Output: 26
Sum of nodes:
7 + 6 + 8 + 4 + 1 = 26

Input: 1->7->3->9->11->5
Output: 36

```

**递归解决方案：**

*   通过传递head和变量来存储总和来调用函数。
    *   然后通过传递当前节点的下一个和求和变量来递归调用该函数。
        *   将当前节点的值加到总和上。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find the sum of``// nodes of the Linked List``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `new` `Node;` `/* put in the data */` `new_node->data = new_data;` `/* link the old list to the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// function to recursively find the sum of``// nodes of the given linked list``void` `sumOfNodes(` `struct` `Node* head,` `int` `* sum)``{` `// if head = NULL` `if` `(!head)` `return` `;` `// recursively traverse the remaining nodes` `sumOfNodes(head->next, sum);` `// accumulate sum` `*sum = *sum + head->data;``}``// utility function to find the sum of  nodes` ]`int` `sumOfNodesUtil(` `struct` `Node* head)``{` [ `int` `sum = 0;` `// find the sum of  nodes` `sumOfNodes(head, &sum);`[HTG9 6] `// required sum` `return` `sum;``}` [`// Driver program to test above``int` `main()``{` `struct` `Node* head = NULL;` `// create linked list 7->6->8->4->1` `push(&head, 7);` `push(&head, 6);` `push(&head, 8);` `push(&head, 4);` `push(&head, 1);`​​  `cout <<` `"Sum of nodes = "` `<< sumOfNodesUtil(head);` `return` `0;``}` |

*chevron_right**filter_none*