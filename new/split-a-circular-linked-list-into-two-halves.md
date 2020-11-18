# 将循环链表分为两半

![](img/379c0de15efa5a6852d3ac11017b3ad1.png "cll")

```
                         Original Linked List  
```

![](img/da9bff9e299fa2b4990c708095bb40c7.png "cll")

```
                         Result Linked List 1  
```

![](img/5b0ba4becbcff5f699ef164068cc21f1.png "cll")

```
                         Result Linked List 2  
```

如果**个奇数节点**，则第一个列表应包含一个额外的节点。

感谢 [Geek4u](https://www.geeksforgeeks.org/forum/topic/splitting-a-circular-doubly-linked-list#post-335) 提出了该算法。
1）使用乌龟和野兔算法存储循环链表的中间和最后一个指针。
2）将后半部分做成圆形。
3）使前半部分变成圆形。
4）设置两个链接列表的开头（或开始）指针。

在下面的实现中，如果给定的循环链接列表中有奇数个节点，则第一个结果列表的节点多于第二个结果列表的节点。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Program to split a circular linked list``// into two halves ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* structure for a node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ``}; ``/* Function to split a list (starting with head) ``into two lists. head1_ref and head2_ref are ``references to head nodes of the two resultant ``linked lists */``void` `splitList(Node *head, Node **head1_ref,`​​  `Node **head2_ref) ``{ ` `Node *slow_ptr = head; ` `Node *fast_ptr = head; ` `if` `(head == NULL) ` `return` `; ` `/* If there are odd nodes in the circular list then ` `fast_ptr->next becomes head and for even nodes ` `fast_ptr->next->next becomes head */` `while` `(fast_ptr->next != head && ` `fast_ptr->next->next != head) ` `{ ` `fast_ptr = fast_ptr->next->next; ` `slow_ptr = slow_ptr->next; ` `} ` `/* If there are even elements in list` `then move fast_ptr */` `if` `(fast_ptr->next->next == head) ` `fast_ptr = fast_ptr->next; ` `/* Set the head pointer of first half */` `*head1_ref = head; ` `/* Set the head pointer of second half */` ] `if` `(head->next != head) ` `*head2_ref = slow_ptr->next; ` [ `/* Make second half circular */` `fast_ptr->next = slow_ptr->next; ` `/* Make first half circular */` `slow_ptr->next = head; ``} ` [`/* UTILITY FUNCTIONS */``/* Function to insert a node at  ``the beginning of a Circular linked list */``void` `push(Node **head_ref,` `int` `data) ``{ ` `Node *ptr1 =` `new` `Node();` `Node *temp = *head_ref; ` `ptr1->data = data; ` `ptr1->next = *head_ref; ` `/* If linked list is not NULL then ` `set the next of last node */` `if` `(*head_ref != NULL) ` `{ ` `while` `(temp->next != *head_ref) ` `temp = temp->next;     ` `temp->next = ptr1; ` `} ` `else` `ptr1->next = ptr1;` `/*For the first node */` `*head_ref = ptr1; ``} ``/* Function to print nodes in ``a given Circular linked list */``void` `printList(Node *head) ``{ ` `Node *temp = head; ` `if` `(head != NULL) ` `{ ` `cout << endl; ` `do` `{ ` `cout << temp->data <<` `" "` `; ` `temp = temp->next; ` `}` `while` `(temp != head); ` `} ``} ``// Driver Code``int` `main() ``{ ` `int` `list_size, i; ` `/* Initialize lists as empty */` `Node *head = NULL; ` `Node *head1 = NULL; ` `Node *head2 = NULL; ` `/* Created linked list will be 12->56->2->11 */` `push(&head, 12); ` `push(&head, 56); ` `push(&head, 2); ` `push(&head, 11); ` `cout <<` `"Original Circular Linked List"` `; ` `printList(head);     ` `/* Split the list */` `splitList(head, &head1, &head2); ` `cout <<` `"\nFirst Circular Linked List"` `; ` `printList(head1); ` `cout <<` `"\nSecond Circular Linked List"` `; ` `printList(head2); ` `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*