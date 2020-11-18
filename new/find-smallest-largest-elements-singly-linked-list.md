# 在单链表

中查找最小和最大元素

给定n个节点的单链列表，并在链列表中找到最小和最大的元素。

例子：

```
Input : 15 14 13 22 17
Output : Linked list are:
        17 -> 22 -> 13 -> 14 -> 15 -> NULL
        Maximum element in linked list: 22
        Minimum element in linked list: 13

Input : 20 25 23 68 54 13 45
Output : Linked list are:
        45 -> 13 -> 54 -> 68 -> 23 -> 25 -> 20 -> NULL
        Maximum element in linked list: 68
        Minimum element in linked list: 13

```

这个想法是在不等于NULL的情况下遍历链接列表，并将 **max** 和 **min** 变量分别初始化为 **INT_MIN** 和 **INT_MAX** 。 之后检查一个条件，如果最大值小于头值，则将头值分配给max或最小值，然后将头值分配给min，否则头值分配给min，否则头点指向下一个节点。 继续此过程，直到head不等于NULL。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to find smallest and largest``// elements in singly linked list.``#include <bits/stdc++.h>``using` `namespace` `std;``/* Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function that returns the largest element``// from the linked list.``int` `largestElement(` `struct` `Node* head)``{`​​  `// Declare a max variable and initialize` `// it with INT_MIN value.` `// INT_MIN is integer type and its value` `// is -32767 or less.` `int` `max = INT_MIN;` `// Check loop while head not equal to NULL` `while` `(head != NULL) {` `// If max is less then head->data then` `// assign value of head->data to max` `// otherwise node point to next node.` `if` `(max < head->data)` `max = head->data;` `head = head->next;` ] `}` `return` `max;``}` [`// Function that returns smallest element``// from the linked list.``int` `smallestElement(` `struct` `Node* head)``{` `// Declare a min variable and initialize` `// it with INT_MAX value.` `// INT_MAX is integer type and its value` `// is 32767 or greater.` `int` `min = INT_MAX;` `// Check loop while head not equal to NULL` `while` `(head != NULL) {` `// If min is greater then head->data then` `// assign value of head->data to min` `// otherwise node point to next node.` `if` `(min > head->data)` `min = head->data;` `head = head->next;` `}` `return` `min;``}``// Function that push the element in linked list.``void` `push(` `struct` `Node** head,` `int` `data)``{` `// Allocate dynamic memory for newNode.` `struct` `Node* newNode = ` `(` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// Assign the data into newNode.` `newNode->data = data;` `// newNode->next assign the address of` `// head node.` `newNode->next = (*head);` `// newNode become the headNode.` `(*head) = newNode;``}``// Display linked list.``void` `printList(` `struct` `Node* head)``{` `while` `(head != NULL) {` `printf` `(` `"%d -> "` `, head->data);` `head = head->next;` `}` `cout <<` `"NULL"` `<< endl;``}``// Driver program to test the functions``int` `main()``{` `// Start with empty list` `struct` `Node* head = NULL;` `// Using push() function to construct` `// singly linked list` `// 17->22->13->14->15` `push(&head, 15);` `push(&head, 14);` `push(&head, 13);` `push(&head, 22);` `push(&head, 17);` `cout <<` `"Linked list is : "` `<< endl;` `// Call printList() function to display` `// the linked list.` `printList(head);` `cout <<` `"Maximum element in linked list:"` `;` `// Call largestElement() function to get largest` `// element in linked list.` `cout << largestElement(head) << endl;` `cout <<` `"Minimum element in linked list:"` `;` `// Call smallestElement() function to get smallest` `// element in linked list.` `cout << smallestElement(head) << endl;` `return` `0;``}` |

*chevron_right**filter_none*