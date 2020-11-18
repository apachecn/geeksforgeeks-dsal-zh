# 将单链接列表转换为数组

给定一个单链表，任务是将其转换为数组。

**示例：**

> **输入：**列表= 1-> 2-> 3-> 4-> 5->空
> **输出：** 1 2 3 4 5
> 
> **输入：**列表= 10-> 20-> 30-> 40-> 50->空
> **输出：** 10 20 30 40 50

**方法：**在此文章的[中讨论了一种从给定数组创建链接列表的方法。 在这里，将讨论一种将给定的链表转换为数组的方法。](https://www.geeksforgeeks.org/create-linked-list-from-a-given-array/)

*   找到给定链表的长度，例如 **len** 。
*   创建一个大小为 **len** 的数组。
*   遍历给定的链表，并将元素一次存储在数组中。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;``// Singly Linked List structure``struct` `node {` `int` `data;` `node* next;``};``// Function to add a new node``// to the Linked List``node* add(` `int` `data)``{` `node* newnode =` `new` `node;` `newnode->data = data;` `newnode->next = NULL;` `return` `newnode;``}``// Function to print the array contents``void` `printArr(` `int` `a[],` `int` `n)``{` `for` `(` `int` `i = 0; i < n; i++)` `cout << a[i] <<` `" "` `;` [H TG200]`}``// Function to return the length``// of the Linked List``int` `findlength(node* head)``{` `node* curr = head;` `int` `cnt = 0;` `while` `(curr != NULL) {` `cnt++;` `curr = curr->next;` `}` `return` `cnt;``}``// Function to convert the``// Linked List to an array``void` `convertArr(node* head)``{` `// Find the length of the` `// given linked list` `int` ] `len = findlength(head);` `// Create an array of the` `// required length` `int` `arr[len];` `int` `index = 0;` `node* curr = head;` `// Traverse the Linked List and add the` `// elements to the array one by one` `while` `(curr != NULL) {` `arr[index++] = curr->data;`​​ `curr = curr->next;` `}` `// Print the created array` `printArr(arr, len);``}``// Driver code``int` `main()``{` `node* head = NULL;` `head = add(1);` `head->next = add(2);` `head->next->next = add(3);` `head->next->next->next = add(4);` `head->next->next->next->next = add(5);` `convertArr(head);` `return` `0;``}` |

*chevron_right**filter_none*