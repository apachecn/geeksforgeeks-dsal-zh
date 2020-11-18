# 链表的最大和最小元素，该元素可被给定数k整除

给定![N](img/19e409e13c1238e1f3ff3dbd06cdd45e.png "Rendered by QuickLaTeX.com")节点的单链接列表。 在链表中找到可被给定数字![K](img/36191961d5c0517749557e907a8f3817.png "Rendered by QuickLaTeX.com")整除的最小和最大元素。

**范例**：

> **输入**：列表= 15-> 14-> 13-> 22-> 50
> K = 5
> **输出**：
> 链表中可被K整除的最大元素：50
> 链表中可被K整除的最小元素：5
> 
> **输入**：列表= 10-> 14-> 13-> 22-> 100
> K = 10
> **输出**：
> 链表中可被K整除的最大元素：100
> 链表中可被K整除的最小元素：10

**方法**：

*   这个想法是将链表遍历到最后，并将max和min变量分别初始化为INT_MIN和INT_MAX。
*   然后检查一下条件，如果最大值小于当前节点的值并且可以被K整除，那么当前节点的值将分配给max。
*   同样，检查当前节点的值是否小于最小值，并被k整除，然后将当前节点的值分配给min。 重复以上两个步骤，直到到达列表的末尾。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Program to find the smallest and largest``// elements divisible by a given number k ``// in singly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``/* Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};`的`// Function to print max and min elements of``// linked list divisible by K``void` `findMaxMin(` `struct` `Node* head,` `int` `k)``{` `// Declare a min variable and initialize` `// it with INT_MAX value.` `// INT_MAX is integer type and its value` `// is 32767 or greater.` `int` `min = INT_MAX;` `// Declare a max variable and initialize` `// it with INT_MIN value.` `// INT_MIN is integer type and its value` `// is -32767 or less.` `int` `max = INT_MIN;` `// Check loop while head not equal to NULL` `while` `(head != NULL) {` `// If head->data is less than min and divisible` `// by k then assign value of head->data to min` `// otherwise node point to next node.` `if` `((head->data < min) && (head->data % k == 0))` `min = head->data;` `// If head->data is greater than max and divisible` `// by k then assign value of head->data to max` `// otherwise node point to next node.` `if` `((head->data > max) && (head->data % k == 0))` `max = head->data;`​​ `head = head->next;` `}` `// Print max element` `cout <<` `"Max Element : "` `<< max << endl;` `// print min element` `cout <<` `"Min Element : "` `<< min;``}``// Function that pushes the element in the linked list.``void` `push(` `struct` `Node** head,` `int` `data)``{` `// Allocate dynamic memory for newNode.` `struct` `Node* newNode = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// Assign the data into newNode.` `newNode->data = data;` `// newNode->next assign the address of` `// head node.` `newNode->next = (*head);` `// newNode become the headNode.` `(*head) = newNode;``}``// Driver Code``int` `main()``{`[HTG33 3]  `// Start with empty list` `struct` `Node* head = NULL;` `// Using push() function to construct` `// singly linked list` `// 50->5->13->14->15` `push(&head, 15);` `push(&head, 14);` `push(&head, 13);` `push(&head, 5);` `push(&head, 50);` [ `int` `k = 5;` `findMaxMin(head, k);` `return` `0;``}` |

*chevron_right**filter_none*