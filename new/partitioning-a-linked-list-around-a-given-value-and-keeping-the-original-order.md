# 根据给定值对链表进行分区，并保持原始顺序

给定一个链表和一个值x，对它进行分区，以使所有小于x的节点排在最前面，然后是所有值等于x的节点，最后是值大于或等于x的节点。 三个分区中每个分区中节点的原始相对顺序都应保留。 分区必须就地工作。

例子：

```
Input : 1->4->3->2->5->2->3, 
        x = 3
Output: 1->2->2->3->3->4->5

Input : 1->4->2->10 
        x = 3
Output: 1->2->4->10

Input : 10->4->20->10->3 
        x = 3
Output: 3->10->4->20->10 

```

为了解决此问题，我们可以使用[快速排序](https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)的**分区方法**，但这不会保留两个分区中每个分区中节点的原始相对顺序。

以下是解决此问题的算法：

*   将以下三个链接列表的第一个和最后一个节点初始化为NULL。
    1.  小于x的值的链接列表。
    2.  链接的值列表等于x。
    3.  大于x的值的链接列表。
*   现在遍历原始链表。 如果节点的值小于x，则将其附加在较小列表的末尾。 如果值等于x，则在等于列表的末尾。 如果值更大，则在更大列表的末尾。
*   现在连接三个列表。

以下是上述想法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to partition a linked list around a``// given value.``#include<bits/stdc++.h>``using` `namespace` `std;` [`/* Link list Node */``struct` `Node``{` `int` `data;` `struct` `Node* next;``};``// A utility function to create a new node``Node *newNode(` `int` `data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data  = data;` `new_node->next = NULL;` `return` `new_node;``}``// Function to make two separate lists and return``// head after concatinating``struct` `Node *partition(` `struct` `Node *head,` `int` `x)``{` `/* Let us initialize first and last nodes of` `three linked lists` `1) Linked list of values smaller than x.` `2) Linked list of values equal to x.` `3) Linked list of values greater than x.*/` `struct` `Node *smallerHead = NULL, *smallerLast = NULL;` `struct` `Node *greaterLast = NULL, *greaterHead = NULL;` `struct` `Node *equalHead = NULL, *equalLast = NULL;` HTG346] `// Now iterate original list and connect nodes` `// of appropriate linked lists.` `while` `(head != NULL)` `{` `// If current node is equal to x, append it` `// to the list of x values` `if` `(head->data == x)` `{` `if` `(equalHead == NULL)` `equalHead = equalLast = head;` `else` `{` `equalLast->next = head;` `equalLast = equalLast->next;` `}` `}` [ `// If current node is less than X, append` `// it to the list of smaller values` `else` `if` `(head->data < x)` `{` `if` `(smallerHead == NULL)` `smallerLast = smallerHead = head;` `else` `{` `smallerLast->next = head;` `smallerLast = head;` `}` `}` `else` `// Append to the list of greater values` `{` `if` `(greaterHead == NULL)` `greaterLast = greaterHead = head;` `else` `{` `greaterLast->next  = head;` `greaterLast = head;` `}` `}` `head = head->next;` `}` `// Fix end of greater linked list to NULL if this` `// list has some nodes` `if` `(greaterLast != NULL)` `greaterLast->next = NULL;` `// Connect three lists` `// If smaller list is empty` `if` `(smallerHead == NULL)` `{` `if` `(equalHead == NULL)` `return` `greaterHead;` `equalLast->next = greaterHead;` `return` `equalHead;` `}` `// If smaller list is not empty` `// and equal list is empty` `if` `(equalHead == NULL)` `{`[HT G201] `smallerLast->next = greaterHead;` `return` `smallerHead;` `}` `// If both smaller and equal list` `// are non-empty` `smallerLast->next = equalHead;` `equalLast->next = greaterHead;` `return` `smallerHead;``}``/* Function to print linked list */``void` `printList(` `struct` `Node *head)``{` `struct` `Node *temp = head;` `while` `(temp != NULL)` `{` `printf` `(` `"%d  "` `, temp->data);` `temp = temp->next;` `}`] `}`。`// Driver program to run the case``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = newNode(10);` `head->next = newNode(4);` ] `head->next->next = newNode(5);` `head->next->next->next = newNode(30);` `head->next->next->next->next = newNode(2);` `head->next->next->next->next->next = newNode(50);` `int` `x = 3;`​​ `head = partition(head, x);` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*