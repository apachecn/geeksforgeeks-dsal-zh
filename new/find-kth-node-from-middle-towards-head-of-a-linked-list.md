# 从中间到链表

的开头查找第k个节点

给定链接列表和数字K。任务是从列表的中间到开头打印第K个节点的值。 如果不存在这样的元素，则打印“ -1”。

**注意**：中间节点的位置是：（n / 2）+1，其中n是列表中节点的总数。

**范例**：

```
Input :  List is 1->2->3->4->5->6->7
         K= 2 
Output : 2

Input :  list is 7->8->9->10->11->12
         K = 3
Output : 7

```

从头到尾遍历列表并计算节点总数。 现在，假设![n](img/42ce0a847b20a2f8a781c8a50bdab975.png "Rendered by QuickLaTeX.com")是列表中的节点总数。 因此，中间节点将位于位置（n / 2）+1。 现在，剩下的任务是从列表的开头打印位于[（n / 2 +1-k）位置的节点。](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to find kth node from middle``// towards Head of the Linked List``#include <bits/stdc++.h>`] `using` `namespace` `std;``// Linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Given a reference (pointer to  ` `pointer) to the head of a list ` `and an int, push a new node on ` `the front of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}`[HTG23 7] `// Function to count number of nodes``int` `getCount(` `struct` `Node* head)``{` `int` `count = 0;` `// Initialize count` `struct` `Node* current = head;` `// Initialize current` `while` `(current != NULL) {` `count++;` `current = current->next;` `}` `return` `count;``}`[`// Function to get the kth node from the mid``// towards begin of the linked list``int` `printKthfrommid(` `struct` `Node* head_ref,` `int` `k)``{` `// Get the count of total number of`​​ `// nodes in the linked list` `int` `n = getCount(head_ref);` `int` `reqNode = ((n / 2 + 1) - k);` `// If no such node exists, return -1` `if` [ `(reqNode <= 0) {` `return` `-1;` `}` `// Find node at position reqNode` `else` `{` `struct` `Node* current = head_ref;` `// the index of the` `// node we're currently` `// looking at` `int` `count = 1;` `while` `(current != NULL) {` `if` `(count == reqNode)` `return` `(current->data);` `count++;` `current = current->next;` `}` `}``}` [`// Driver code``int` `main()``{` `// start with empty list` [HTG3 32] `struct` `Node* head = NULL;` `int` `k = 2;` [ `// create linked list` `// 1->2->3->4->5->6->7` `push(&head, 7);` `push(&head, 6);` `push(&head, 5);` `push(&head, 4);` `push(&head, 3);` `push(&head, 2);` `push(&head, 1);`〔HTG358〕〔HTG359〕〔HTG177〕〔HTG178〕〔HTG360〕〔HTG361〕〔HTG179〕〔HTG362〕〔HTG363〕〔HTG180〕〕 |

*chevron_right**filter_none*