# 在单个循环链接列表

中查找最小和最大元素

给定![N](img/19e409e13c1238e1f3ff3dbd06cdd45e.png "Rendered by QuickLaTeX.com")节点的单循环链接列表。 任务是在循环链表中找到最小和最大的元素。

**范例**：

```
Input : List = 99->11->22->33->44->55->66
Output : Minimum = 11, Maximum = 99

Input : List = 12->11->9->33->125->6->99
Output : Minimum = 6, Maximum = 125

```

这个想法是在没有到达最后一个节点的情况下遍历循环链接列表，并将 **max** 和 **min** 变量初始化为 **INT_MIN** 和 **INT_MAX** 分别。 之后检查一个条件，如果最大值小于头值，则将头值分配给max或最小值，然后将头值分配给min，否则头值分配给min，否则头点指向下一个节点。 继续此过程，直到最后一个节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find minimum and maximum``// value from singly circular linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`// structure for a node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to print minimum and maximum``// nodes of the circular linked list``void` `printMinMax(` `struct` `Node** head)``{` `// check list is empty` `if` `(*head == NULL) {` `return` `;` `}` `// pointer for traversing` `struct` `Node* current;` `// initialize head to current pointer` `current = *head;` `// initialize max int value to min` `// initialize min int value to max` `int` `min = INT_MAX, max = INT_MIN;` `// While last node is not reached` `do` `{` `// If current node data is lesser for min` `// then replace it` `if` `(current->data < min) {` `min = current->data;` `}`的 `// If current node data is greater for max` `// then replace it` `if` `(current->data > max) {` `max = current->data;` `}` `current = current->next;` `}` `while` `(current != head);` `cout <<` `"\nMinimum = "` `<< min <<` `", Maximum = "` `<< max;``}`[H TG384] `// Function to insert a node at the end of``// a Circular linked list``void` `insertNode(` `struct` `Node** head,` `int` `data)``{` `struct` `Node* current = *head;` `// Create a new node` `struct` `Node* newNode =` `new` `Node;` [ `// check node is created or not` `if` `(!newNode) {` `printf` `(` `"\nMemory Error\n"` `);` `return` `;` `}` `// insert data into newly created node` `newNode->data = data;` `// check list is empty` `// if not have any node then` `// make first node it` `if` `(*head == NULL) {` `newNode->next = newNode;` `*head = newNode;` `return` `;` `}` `// if list have already some node` `else` `{` `// move firt node to last node` `while` `(current->next != *head) {` `current = current->next;` `}` `// put first or head node address` `// in new node link` `newNode->next = *head;` `// put new node address into` `// last node link(next)` `current->next = newNode;` `}``}`的`// Function to print the Circular linked list``void` `displayList(` `struct` `Node* head)``{`[HTG4 78]  `struct` `Node* current = head;` `// if list is empty simply show message` `if` `(head == NULL) {` `printf` `(` `"\nDisplay List is empty\n"` `);` `return` `;` `}` `// traverse first to last node` `else` `{` `do` `{` `printf` `(` `"%d "` `, current->data);` `current = current->next;` `}` `while` `(current != head);` `}``}``// Driver Code``int` `main()``{` `struct` `Node* Head = NULL;` `insertNode(&Head, 99);` `insertNode(&Head, 11);` `insertNode(&Head, 22);` `insertNode(&Head, 33);` `insertNode(&Head, 44);` `insertNode(&Head, 55);` `insertNode(&Head, 66);` `cout <<` `"Initial List: "` `;`​​ `displayList(Head);` `printMinMax(&Head);` `return` `0;``}` |

*chevron_right**filter_none*