# 反向链接列表中的偶数元素

给定一个链表，任务是反转连续的偶数元素并打印更新的链表。

> **输入：** 1-> 2-> 3-> 3-> 4-> 6-> 8-> 5-> NULL
> **输出：** 1 2 3 3 8 6 4 5
> 初始列表：1-> **2** -> 3-> 3-> **4-> 6-> 8** -> 5-> NULL
> 反转列表：1-> **2** -> 3 -> 3-> **8-> 6-> 4** -> 5->空
> 
> **输入：** 11-> 32-> 7->空
> **输出：** 11 32 7

**方法：**在以下情况下，反转偶数元素将不会发生：

1.  节点的值是奇数。
2.  节点的值为偶数，但相邻的值为奇数。

在其余情况下，偶数节点的连续块可以反转。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;``// Structure of a node of the linked list``struct` `node {` `int` `data;` `struct` `node* next;``};``// Function to create a new node``struct` `node* newNode(` `int` `d)``{` `struct` `node* newnode =` `new` `node();` `newnode->data = d;` `newnode->next = NULL;` `return` `newnode;``}``// Recursive function to reverse the consecutive``// even nodes of the linked list``struct` `node* reverse(` `struct` `node* head,` `struct` `node* prev)``{` `// Base case` `if` `(head == NULL)` `return` `NULL;` `struct` `node* temp;` `struct` `node* curr;` `curr = head;` `// Reversing nodes until curr node's value` `// turn odd or Linked list is fully traversed`​​  `while` `(curr != NULL && curr->data % 2 == 0) {` `temp = curr->next;` `curr->next = prev;` `prev = curr;` `curr = temp;` `}` `// If elements were reversed then head` `// pointer needs to be changed` `if` `(curr != head) {` `// Recur for the remaining linked list` `curr = reverse(curr, NULL);` `return` `prev;` `}` `// Simply iterate over the odd value nodes` `else` `{` `head->next = reverse(head->next, head);` `return` `head;` `}``}`的`// Utility function to print the``// contents of the linked list``void` `printLinkedList(` `struct` `node* head)``{` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver code``int` `main()``{` `int` `arr[] = { 1, 2, 3, 3, 4, 6, 8, 5 };` `int` `n =` `sizeof` `(arr) /` `sizeof` [HTG15 1] `struct` `node* head = NULL;` `struct` `node* p;` `// Constructing linked list` `for` `(` `int` `i = 0; i < n; i++) {` ] `if` `(head == NULL) {` `p = newNode(arr[i]);` `head = p;` `continue` `;` `}` `p->next = newNode(arr[i]);` `p = p->next;` `}` `// Head of the updated linked list` `head = reverse(head, NULL);` `// Printing the reversed linked list` `printLinkedList(head);` `return` `0;``}` |

*chevron_right**filter_none*