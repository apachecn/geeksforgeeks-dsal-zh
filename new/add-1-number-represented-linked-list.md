# 将1加到以链表

表示的数字

数字在链接列表中表示，因此每个数字都对应于链接列表中的一个节点。 加1。 例如，1999表示为（1-> 9-> 9-> 9），将其添加1应该将其更改为（2-> 0-> 0-> 0）

步骤如下：

1.  反转给定的链表。 例如，将1-> 9-> 9-> 9转换为9-> 9-> 9-> 1。
2.  从最左边的节点开始遍历链表，并向其添加1。 如果有进位，请移至下一个节点。 有进位时继续移动到下一个节点。
3.  反向修改链表和返回头。

下面是上述步骤的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to add 1 to a linked list ``#include <bits/stdc++.h>``using` `namespace` `std;``/* Linked list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next; ``}; ``/* Function to create a new node with given data */``Node *newNode(` `int` `data) ``{ ` `Node *new_node =` `new` `Node; ` `new_node->data = data; ` `new_node->next = NULL; ` `return` `new_node; ``} ``/* Function to reverse the linked list */``Node *reverse(Node *head) ``{ `​​  `Node * prev = NULL; ` `Node * current = head; ` `Node * next; ` `while` `(current != NULL) ` `{ ` `next = current->next; ` `current->next = prev; ` `prev = current; ` `current = next; ` `} ` `return` `prev; ``} ``/* Adds one to a linked lists and return the head ``node of resultant list */``Node *addOneUtil(Node *head) ``{ ` `// res is head node of the resultant list ` `Node* res = head; ` `Node *temp, *prev = NULL; `] `int` `carry = 1, sum; ` `while` `(head != NULL)` `//while both lists exist ` `{ ` `// Calculate value of next digit in resultant list. ` `// The next digit is sum of following things ` `// (i) Carry ` `// (ii) Next digit of head list (if there is a `[HTG3 28]  `// next digit) ` `sum = carry + head->data; ` `// update carry for next calulation ` `carry = (sum >= 10)? 1 : 0; ` `// update sum if it is greater than 10 ` `sum = sum % 10; `]  `// Create a new node with sum as data ` `head->data = sum; ` `// Move head and second pointers to next nodes ` `temp = head; ` `head = head->next; ` `} ` `// if some carry is still there, add a new node to ` `// result list. ` `if` `(carry > 0) ` `temp->next = newNode(carry); ` `// return head of the resultant list ` `return` `res; ``} ` [HTG3 79]`// This function mainly uses addOneUtil(). ``Node* addOne(Node *head) ``{ ` `// Reverse linked list ` `head = reverse(head); ` `// Add one from left to right of reversed ` `// list ` `head = addOneUtil(head); ` [ `// Reverse the modified list ` `return` `reverse(head); ``} `的`// A utility function to print a linked list ``void` `printList(Node *node) ``{ ` `while` `(node != NULL) ` `{ ` `cout << node->data; ` `node = node->next; ` `} ` `cout<<endl;``} ``/* Driver program to test above function */``int` `main(` `void` `) ``{ ` `Node *head = newNode(1); ` `head->next = newNode(9); ` `head->next->next = newNode(9); ` `head->next->next->next = newNode(9); ` `cout <<` `"List is "` `; ` `printList(head); ` `head = addOne(head); ` `cout <<` `"\nResultant list is "` `; ` `printList(head); ` `return` `0; ``} `，`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*