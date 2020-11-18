# 链表

的备用节点的产品

给定一个链表，任务是打印给定链表的备用节点的乘积。

**范例**：

```
Input : 1 -> 8 -> 3 -> 10 -> 17 -> 22 -> 29 -> 42
Output : 1479
Alternate nodes : 1 -> 3 -> 17 -> 29

Input : 10 -> 17 -> 33 -> 38 -> 73
Output : 24090 
Alternate nodes : 10 -> 33 -> 73

```

**迭代方法：**

1.  遍历整个链表。
2.  设置prod = 1并且count = 0。
3.  当计数为偶数时，将节点的数据乘以prod。
4.  访问下一个节点。

以下是此方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ code to print the product of Alternate Nodes``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Function to get the product of alternate``nodes of the linked list */``int` `productAlternateNode(` `struct` `Node* head)``{` `int` `count = 0;` `int` `prod = 1;`的 `while` `(head != NULL) {` `// when count is even product the data of node` `if` `(count % 2 == 0)` `prod *= head->data;` `// count the nodes` `count++;` `// move on the next node.` `head = head->next;` `}` `return` `prod;``}``// Function to push node at head``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Driver code``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;`] `/* Use push() function to construct ` `the below list 8 -> 23 -> 11 -> 29 -> 12 */` `push(&head, 12);` `push(&head, 29);`[ `push(&head, 11);` `push(&head, 23);` `push(&head, 8);` `cout << productAlternateNode(head);` `return` `0;``}``// This code is contributed by shivani singh` [ |

*chevron_right**filter_none*