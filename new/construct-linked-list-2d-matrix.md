# 从2D矩阵

构造一个链表

给定一个矩阵。 将其转换为链接列表矩阵，以便每个节点都连接到其下一个右节点和下一个节点。

**示例：**

```
Input : 2D matrix 
1 2 3
4 5 6
7 8 9

Output :
1 -> 2 -> 3 -> NULL
|    |    |
v    v    v
4 -> 5 -> 6 -> NULL
|    |    |
v    v    v
7 -> 8 -> 9 -> NULL
|    |    |
v    v    v
NULL NULL NULL

```

**问题来源：** [事实访谈经验| 设置9](https://www.geeksforgeeks.org/factset-interview-experience-set-9-campus-full-time/)

这个想法是为矩阵的每个元素构造一个新节点，并递归地创建其下和右节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to construct a linked list``// from given 2D matrix``#include <bits/stdc++.h>``using` `namespace` `std;` [`// struct node of linked list``struct` `Node {` `int` `data;` `Node* right, *down;``};``// returns head pointer of linked list``// constructed from 2D matrix``Node* construct(` `int` `arr[][3],` `int` `i,` `int` `j, ` `int` `m,` `int` `n)``{` `// return if i or j is out of bounds` `if` `(i > n - 1 &#124;&#124; j > m - 1)` `return` `NULL;` `// create a new node for current i and j` `// and recursively allocate its down and` `// right pointers` `Node* temp =` `new` `Node();` [H TG52] `temp->right = construct(arr, i, j + 1, m, n);` `temp->down  = construct(arr, i + 1, j, m, n);` `return` `temp;``}``// utility function for displaying``// linked list data``void` `display(Node* head)``{` `// pointer to move right` `Node* Rp;` `// pointer to move down` `Node* Dp = head;` `// loop till node->down is not NULL` `while` `(Dp) {` `Rp = Dp;` `// loop till node->right is not NULL` `while` `(Rp) {` `cout << Rp->data <<` `" "` `;` `Rp = Rp->right;` `}` `cout <<` `"\n"` `;` [[HTG23 8]  `Dp = Dp->down;` `}``}` [`// driver program``int` `main()``{` `// 2D matrix` `int` `arr[][3] = {` `{ 1, 2, 3 },` `{ 4, 5, 6 },` `{ 7, 8, 9 }` `};`[ `int` `m = 3, n = 3;` `Node* head = construct(arr, 0, 0, m, n);`​​  `display(head);` `return` `0;``}` |

*chevron_right**filter_none*