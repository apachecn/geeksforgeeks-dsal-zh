# 删除链接列表

的每个第k个节点

给定一个单链表，您的任务是删除链表的第K个节点。 假定K始终小于或等于链接列表的长度。

**示例：**

```
Input : 1->2->3->4->5->6->7->8  
        k = 3
Output : 1->2->4->5->7->8
As 3 is the k-th node after its deletion list 
would be 1->2->4->5->6->7->8
And now 4 is the starting node then from it, 6 
would be the k-th node. So no other kth node 
could be there.So, final list is:
1->2->4->5->7->8.

Input: 1->2->3->4->5->6  
       k = 1
Output: Empty list 
All nodes need to be deleted

```

这个想法是从头开始遍历列表，并跟踪上次删除后访问的节点。 每当计数变为k时，删除当前节点并将计数重置为0。

```
(1) Traverse list and do following
   (a) Count node before deletion.
   (b) If (count == k) that means current 
        node is to be deleted.
      (i)  Delete current node i.e. do

          //  assign address of next node of 
          // current node to the previous node
          // of the current node.
          prev->next = ptr->next i.e.

       (ii) Reset count as 0, i.e., do count = 0.
   (c) Update prev node if count != 0 and if
       count is 0 that means that node is a
       starting point.
   (d) Update ptr and continue until all 
       k-th node gets deleted.

```

下面是实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to delete every k-th Node of``// a singly linked list.``#include<bits/stdc++.h>``using` `namespace` `std;` [`/* Linked list Node */``struct` `Node``{` `int` `data;` `struct` `Node* next;``};``// To remove complete list (Needed for``// case when k is 1)``void` `freeList(Node *node)``{` `while` `(node != NULL)` `{` `Node *next = node->next;` `delete` `(node);` `node  = next;` `}``}`​​ `// Deletes every k-th node and returns head``// of modified list.``Node *deleteKthNode(` `struct` `Node *head,` `int` `k)``{` `// If linked list is empty` `if` `(head == NULL)` `return` `NULL;` `if` `(k == 1)` `{` `freeList(head);` `return` `NULL;` `}` `// Initialize ptr and prev before starting` `// traversal.` `struct` `Node *ptr = head, *prev = NULL;` `// Traverse list and delete every k-th node` `int` `count = 0;` `while` `(ptr != NULL)` `{` `// increment Node count` `count++;` `// check if count is equal to k` `// if yes, then delete current Node` ] `if` [H TG99] `{` `// put the next of current Node in` `// the next of previous Node` `delete` `(prev->next);` `prev->next = ptr->next;` `// set count = 0 to reach further` `// k-th Node` `count = 0;` `}` `// update prev if count is not 0` `if` `(count != 0)` `prev = ptr;` `ptr = prev->next;` `}` `return` `head;``}``/* Function to print linked list */``void` `displayList(` `struct` `Node *head)``{` `struct` `Node *temp = head;` `while` `(temp != NULL)` `{` `cout<<temp->data<<` `" "` `;` `temp = temp->next;` `}``}``// Utility function to create a new node.``struct` `Node *newNode(` `int` `x)``{` `Node *temp =` `new` `Node;` `temp->data = x;` `temp->next = NULL;` `return` `temp;``}`]  [`/* Driver program to test count function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);`[HTG4 24]  `head->next->next->next = newNode(4);` `head->next->next->next->next = newNode(5);` `head->next->next->next->next->next = newNode(6);` `head->next->next->next->next->next->next =` `newNode(7);` `head->next->next->next->next->next->next->next =` `newNode(8);` `int` `k = 3;` `head = deleteKthNode(head, k);` `displayList(head);` `return` `0;``}` |

*chevron_right**filter_none*