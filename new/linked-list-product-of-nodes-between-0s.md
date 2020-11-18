# 节点之间的链接列表乘积为0

给定一个链表，其中包含一系列用“ 0”分隔的数字。 生产它们并就地存储在链接列表中。

**注意：**输入中不会存在连续的零。

**范例**：

```
Input  : 1->2->3->0->5->4->0->3->2->0
Output : 6->20->6

Input  : 1->2->3->4
Output : 1->2->3->4

```

**方法**：

1.  开始遍历链表的节点。
2.  在temp.data！= 0时进行迭代，并将这些数据乘积为变量“ prod”。
3.  当您遇到0作为节点数据时，请更改先前节点的指针。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to in-place product linked list``// nodes between 0s``#include<bits/stdc++.h>``using` `namespace` `std;` [`// Linked List Node``struct` `Node ``{` `int` `data;` `Node* next;` `Node(` `int` `d)` `{` `data = d;` `next = NULL;` `}``};``// Function to traverse and print Linked List` `void` `printList(Node* head)` `{` `while` `(head->next != NULL) ` `{` `cout<<head->data <<` `"-> "` `;` `head = head->next;` `}` [HTG5 0] `"\n"` `;` `}``// Function to in-place product linked list``// nodes between 0s` `// Function to store numbers till 0` `void` `inPlaceStore(Node* head)` `{` `if` `(head->data == 0) ` `{` `head = head->next;`​​ `}` `// To store modified list` `Node* res = head;` `// Traverse linked list and keep` `// adding nodes between 0s.` `Node* temp = head;` `int` `prod = 1;` `while` `(temp != NULL)` `{` `if` `(temp->data != 0)` `{` `prod *= temp->data;` `temp = temp->next;` `}` `// If we encounters 0, we need` `// to update next pointers` `else` `{` `res->data = prod;` `res->next = temp->next;` `temp = temp->next;` `res = res->next;` `prod = 1;` `}` `}` `// For the last segment` `res->data = prod;` `res->next = temp;` `printList(head);` `}` `// Driver Code` `int` `main()` `{` `Node *head =` `new` `Node(3);` `head->next =` `new` `Node(2);` `head->next->next =` `new` `Node(0);` `head->next->next->next =` `new` `Node(4);` `head->next->next->next->next =` `new` `Node(5);` `head->next->next->next->next->next =` `new` `Node(0);` `head->next->next->next->next->next->next =` `new` `Node(6);` `head->next->next->next->next->next->next->next =` `new` `Node(7);` `inPlaceStore(head);` `return` `0;` `}``// This code is contributed by Arnab Kundu` |

*chevron_right**filter_none*