# 将链接列表的子列表从位置M向右旋转K个位置

给定一个链表和两个位置“ m”和“ n”。 任务是将子列表从位置m旋转到n，向右旋转k个位置。

**示例：**

> **输入：**列表= 1- > 2- > 3- > 4- > 5- > 6，m = 2，n = 5，k = 2
> **输出：** 1- > 4- > 5- > 2- > 3- > 6
> 将子列表2 3 4 5向右旋转2倍
> ，则修改后的列表为：1 4 5 2 3 6
> 
> **输入：**列表= 20- > 45- > 32- > 34- > 22- > 28，m = 3，n = 6，k = 3
> **输出：** 20- > 45- > 34- > 22- > 28- > 32
> 将子列表32 34 22 28向右旋转3倍
> ，则修改后的列表为：20 45 34 22 28 32

**方法：**要旋转从m到n元素的给定子列表，请将列表从（n-k + 1）<sup>第</sup>移到第<sup>第</sup>节点到 开始子列表以完成轮换。
如果k大于子列表的大小，则将其与子列表的大小取模。 因此，使用指针和计数器遍历列表，我们将保存（m-1）个<sup>第</sup>个节点，然后使其指向（n-k + 1）个<sup>第</sup>个节点，因此 将（n-k + 1）个<sup>节点</sup>移到子列表的开头（前面）。
同样，我们将保存第<sup>个</sup>节点，然后使第<sup>个</sup>节点指向该节点。 为了保持列表的其余部分不变，我们将使[n-k]个<sup>节点指向n的下一个节点（可能为NULL）。 最后，我们将获得k次正确旋转的子列表。</sup>

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the above approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Definition of node of linkedlist` ]`struct` `ListNode {`​​  `int` `data;` `struct` `ListNode* next;``};``// This function take head pointer of list, start and``// end points of sublist that is to be rotated and the``// number k and rotate the sublist to right by k places.``void` `rotateSubList(ListNode* A,` `int` `m,` `int` `n,` `int` `k)``{` `int` `size = n - m + 1;` ] `// If k is greater than size of sublist then ` `// we will take its modulo with size of sublist` `if` `(k > size) {` `k = k % size;` `}` `// If k is zero or k is equal to size or k is` `// a multiple of size of sublist then list ` `// remains intact` `if` `(k == 0 &#124;&#124; k == size) {` `ListNode* head = A;` `while` `(head != NULL) {` `cout << head->data;` `head = head->next;` `}` `return` `;` `}` `ListNode* link = NULL;` `// m-th node` `if` `(m == 1) {` `link = A;` `}` `// This loop will traverse all node till` ] `// end node of sublist.    ` `ListNode* c = A;` `// Current traversed node` `int` `count = 0;` `// Count of traversed nodes` `ListNode* end = NULL;  ` `ListNode* pre = NULL;` `// Previous of m-th node` `while` `(c != NULL) {` `count++;` `// We will save (m-1)th node and later` `// make it point to (n-k+1)th node` `if` `(count == m - 1) {` `pre = c;` `link = c->next;` `}` `if` `(count == n - k) {` `if` `(m == 1) {` `end = c;` `A = c->next;` `}` `else` `{` `end = c;` `// That is how we bring (n-k+1)th` `// node to front of sublist.` `pre->next = c->next;` `}` `}` `// This keeps rest part of list intact.` `if` `(count == n) {` `ListNode* d = c->next;` `c->next = link;` `end->next = d;` `ListNode* head = A;` `while` `(head != NULL) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}` `return` `;` `}` `c = c->next;` `}``}`[HTG180`// Function for creating and linking new nodes``void` `push(` `struct` `ListNode** head,` `int` `val)``{` `struct` `ListNode* new_node =` `new` `ListNode;` `new_node->data = val;` `new_node->next = (*head);` `(*head) = new_node;``}``// Driver code``int` `main()` [HTG4 49]`{` `struct` `ListNode* head = NULL;` `push(&head, 70);` `push(&head, 60);` `push(&head, 50);` `push(&head, 40);` `push(&head, 30);` `push(&head, 20);` `push(&head, 10);` `ListNode* tmp = head;` `cout <<` `"Given List: "` `;` `while` `(tmp != NULL) {` `cout << tmp->data <<` `" "` `;` `tmp = tmp->next;` `}` `cout << endl;` `int` `m = 3, n = 6, k = 2;` `cout <<` `"After rotation of sublist: "` `;` `rotateSubList(head, m, n, k);` `return` `0;`[HTG25 6] |

*chevron_right**filter_none*