# 计算一个乘积等于给定值x的双链表中的三胞胎

给定一个不同节点的排序双链表（没有两个节点具有相同的数据）和一个值x。 任务是对列表中的三元组进行计数，直到达到给定值x。

**示例：**

> **输入：**列表= 1- > 2- > 4- > 5- > 6- > 8- > 9，x = 8
> **输出：** 1
> 三元组是（1、2、4）
> 
> **输入：**列表= 1- > 2- > 4- > 5- > 6- > 8- > 9，x = 120
> **输出：** 1
> 三元组是（4，5，6）

**天真的方法：**使用三个嵌套循环生成所有三元组，并检查三元组乘积中的元素是否等于x。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to count triplets``// in a sorted doubly linked list``// whose product is equal to a given value 'x'``#include <bits/stdc++.h>``using` `namespace` `std;``// structure of node of doubly linked list``struct` `Node {` `int` `data;` `struct` `Node *next, *prev;``};``// function to count triplets in a sorted doubly linked list``// whose product is equal to a given value 'x'``int` `countTriplets(` `struct` `Node* head,` `int` `x)``{` `struct` `Node *ptr1, *ptr2, *ptr3;` `int` `count = 0;` `// generate all possible triplets` `for` `(ptr1 = head; ptr1 != NULL; ptr1 = ptr1->next)` `for` `(ptr2 = ptr1->next; ptr2 != NULL; ptr2 = ptr2->next)` `for` `(ptr3 = ptr2->next; ptr3 != NULL; ptr3 = ptr3->next)` `// if elements in the current triplet product up to 'x'` `if` `((ptr1->data * ptr2->data * ptr3->data) == x)` `// increment count` `count++;` HTG207] `// required count of triplets` `return` `count;``}` `// A utility function to insert a new node at the``// beginning of doubly linked list``void` `insert(` `struct` `Node** head,` `int` `data)``{` `// allocate node` `struct` `Node* temp =` `new` `Node();` [ `// put in the data` `temp->data = data;` `temp->next = temp->prev = NULL;` `if` `((*head) == NULL)` `(*head) = temp;` `else` `{` `temp->next = *head;` `(*head)->prev = temp;` `(*head) = temp;` `}``}``// Driver program to test above``int` `main()``{` `// start with an empty doubly linked list` `struct` `Node* head = NULL;`[ `// insert values in sorted order`​​  `insert(&head, 9);` `insert(&head, 8);` `insert(&head, 6);` `insert(&head, 5);` `insert(&head, 4);` `insert(&head, 2);` `insert(&head, 1);` `int` `x = 8;` `cout <<` `"Count = "` `<< countTriplets(head, x);` `return` `0;``}` |

*chevron_right**filter_none*