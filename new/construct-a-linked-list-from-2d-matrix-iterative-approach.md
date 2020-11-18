# 从2D矩阵构造一个链表（迭代方法）

给定一个矩阵，任务是构造一个链表列表矩阵，其中每个节点都连接到其右下节点。

**示例：**

```
Input: [1 2 3
         4 5 6
         7 8 9]

Output:
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

[帖子](https://www.geeksforgeeks.org/construct-linked-list-2d-matrix/)中已经讨论了针对此问题的递归解决方案。 下面是该问题的迭代方法：

*   这个想法是创建m个链表（m =行数），其每个节点都存储其右节点。 每个m个链接列表的头指针都存储在节点数组中。
*   然后，遍历m个列表，对于第（i + 1）个第<sup>个</sup>列表，将第i个<sup>第</sup>个列表的每个节点的向下指针设置为其（i + 1 ）<sup>列表。</sup>

![](img/fdbc61d5b4e7159680c8e27ecf04f5c4.png)

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to construct a linked``// list from 2D matrix &#124; Iterative Approach``#include <bits/stdc++.h>``using` `namespace` `std;``// struct node of linked list``struct` `node {` `int` `data;` `node *right, *down;``};``// utility function to create a new node with given data``node* newNode(` `int` `d)``{` `node* temp =` `new` `node;` `temp->data = d;` `temp->right = temp->down = NULL;` `return` `temp;``}``// utility function to print the linked list pointed to by head pointer``void` `display(node* head)``{` `node *rp, *dp = head;` `// loop until the down pointer is not NULL` `while` `(dp) {` `rp = dp;`​​  `// loop until the right pointer is not NULL` `while` `(rp) {` `cout << rp->data <<` `" "` `;` `rp = rp->right;` `}` `cout << endl;` `dp = dp->down;` `}``}``// function which constructs the linked list` ]`// from the given matrix of size m * n``// and returns the head pointer of the linked list``node* constructLinkedMatrix(` `int` `mat[][3],` `int` `m,` `int` `n)``{` `// stores the head of the linked list` `node* mainhead = NULL;` `// stores the head of linked lists of each row` `node* head[m];` `node *righttemp, *newptr;` `// Firstly, we create m linked lists` [HT G97] `for` `(` `int` `i = 0; i < m; i++) {` `// initially set the head of ith row as NULL` `head[i] = NULL;` `for` `(` `int` `j = 0; j < n; j++) {` `newptr = newNode(mat[i][j]);`] `// stores the mat[0][0] node as` `// the mainhead of the linked list` `if` `(!mainhead)` `mainhead = newptr;` `if` `(!head[i])` `head[i] = newptr;` `else` `righttemp->right = newptr;` `righttemp = newptr;` `}` `}` `// Then, for every ith and (i+1)th list,` `// we set the down pointers of` `// every node of ith list` `// with its corresponding` `// node of (i+1)th list` `for` `(` `int` `i = 0; i < m - 1; i++) {` `node *temp1 = head[i], *temp2 = head[i + 1];` `while` `(temp1 && temp2) {`] `temp1->down = temp2;` `temp1 = temp1->right;` `temp2 = temp2->right;` `}` `}` `// return the mainhead pointer of the linked list` `return` `mainhead;``}``// Driver program to test the above function``int` `main()``{` ] `int` `m, n;` `// m = rows and n = columns` `m = 3, n = 3;`[HTG19 4] `// 2D matrix` `int` `mat[][3] = { { 1, 2, 3 },` `{ 4, 5, 6 },` `{ 7, 8, 9 } };` `node* head = constructLinkedMatrix(mat, m, n);` `display(head);` `return` `0;` ]`}` |

*chevron_right**filter_none*