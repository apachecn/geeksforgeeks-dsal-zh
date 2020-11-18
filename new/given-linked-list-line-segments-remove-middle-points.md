# 给定线段的链接列表，请删除中间点

给定一个坐标的链表，其中相邻点形成垂直线或水平线。 从链接列表中删除水平或垂直线中间的点。

例子：

```
Input:  (0,10)->(1,10)->(5,10)->(7,10)
                                  |
                                (7,5)->(20,5)->(40,5)
Output: Linked List should be changed to following
        (0,10)->(7,10)
                  |
                (7,5)->(40,5) 
The given linked list represents a horizontal line from (0,10) 
to (7, 10) followed by a vertical line from (7, 10) to (7, 5), 
followed by a horizontal line from (7, 5) to (40, 5).

Input:     (2,3)->(4,3)->(6,3)->(10,3)->(12,3)
Output: Linked List should be changed to following
    (2,3)->(12,3) 
There is only one vertical line, so all middle points are removed.

```

资料来源： [Microsoft面试体验](https://www.geeksforgeeks.org/microsoft-interview-experience-set-41-campus/)

这个想法是跟踪当前节点，下一个节点和下一个下一个节点。 下一个节点与下一个下一个节点相同时，请继续删除下一个节点。 在这个完整的过程中，我们需要注意指针的移动并检查NULL值。

以下是上述想法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to remove intermediate points``// in a linked list that represents horizontal``// and vertical line segments ``#include <bits/stdc++.h>``using` `namespace` `std; ``// Node has 3 fields including x, y ``// coordinates and a pointer ``// to next node ``class` `Node ``{ ` `public` `:` `int` `x, y; ` `Node *next; ``}; `​​`/* Function to insert a node at the beginning */``void` `push(Node ** head_ref,` `int` `x,` `int` `y) ``{ ` `Node* new_node =` `new` `Node();` `new_node->x = x; ` `new_node->y = y; ` `new_node->next = (*head_ref); ` `(*head_ref) = new_node; ``} ``/* Utility function to print a singly linked list */``void` `printList(Node *head) ``{ ` `Node *temp = head; ` `while` `(temp != NULL) ` `{ ` `cout <<` `"("` `<< temp->x <<` `","` `<< temp->y <<` `")-> "` `; ` `temp = temp->next; ` `} ` `cout<<endl;``} ``// Utility function to remove Next from linked list ``// and link nodes after it to head ``void` `deleteNode(Node *head, Node *Next) ``{ ` `head->next = Next->next; ` `Next->next = NULL; ` `free` `(Next); ``} ``// This function deletes middle nodes in a sequence of ``// horizontal and vertical line segments represented by ``// linked list. ``Node* deleteMiddle(Node *head) ``{ ` `// If only one node or no node...Return back` [H TG346] `if` `(head == NULL &#124;&#124; head->next == NULL &#124;&#124; ` `head->next->next == NULL) ` `return` `head; ` `Node* Next = head->next; ` `Node *NextNext = Next->next ; ` `// Check if this is a vertical line or horizontal line ` `if` `(head->x == Next->x) ` `{ ` `// Find middle nodes with same x value, and delete them ` `while` `(NextNext != NULL && Next->x == NextNext->x) ` `{ ` `deleteNode(head, Next); ` `// Update Next and NextNext for next iteration ` `Next = NextNext; ` `NextNext = NextNext->next; ` `} ` `} ` `else` `if` `(head->y==Next->y)` `// If horizontal line ` `{ ` `// Find middle nodes with same y value, and delete them ` `while` `(NextNext != NULL && Next->y == NextNext->y) ` `{ ` `deleteNode(head, Next); ` `// Update Next and NextNext for next iteration ` `Next = NextNext; ` `NextNext = NextNext->next; ` `} ` ] `} ` `else` `// Adjacent points must have either same x or same y ` `{ ` `puts` `(` `"Given linked list is not valid"` `); ` `return` `NULL; ` `} ` `// Recur for next segment ` `deleteMiddle(head->next); ` `return` `head; ``} `]  [`// Driver program to tsst above functions ``int` `main() ``{ ` `Node *head = NULL; ` `push(&head, 40,5); ` `push(&head, 20,5); ` `push(&head, 10,5); ` `push(&head, 10,8); ` `push(&head, 10,10); ` `push(&head, 3,10); ` `push(&head, 1,10); ` `push(&head, 0,10); ` `cout <<` `"Given Linked List: \n"` `; ` `printList(head); ` `if` `(deleteMiddle(head) != NULL); ` `{ ` `cout <<` `"Modified Linked List: \n"` `; ` `printList(head); ` `} ` `return` `0; ``} `] [`// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*