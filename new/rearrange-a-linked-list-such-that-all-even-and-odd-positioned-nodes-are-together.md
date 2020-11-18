# 重新排列链接列表，以便所有偶数和奇数定位的节点都在一起

重新排列链表，使所有奇数位置节点都在一起，而所有偶数位置节点都在一起，

**示例：**

```
Input:   1->2->3->4
Output:  1->3->2->4

Input:   10->22->30->43->56->70
Output:  10->30->56->22->43->70

```

这个问题的重点是确保处理以下所有情况
1）空链表
2）仅具有一个节点的链表
3）仅具有两个节点的链表
4）节点数为奇数的链表
5）节点数为偶数的链表

下面的程序将当前节点的两个指针“奇数”和“偶数”分别维持在奇数和偶数位置。 我们还存储偶数链接列表的第一个节点，以便在将所有奇数和偶数节点连接到两个不同的列表中之后，可以将偶数列表附加到奇数列表的末尾。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to rearrange a linked list in such a ``// way that all odd positioned node are stored before ``// all even positioned nodes ``#include<bits/stdc++.h> ``using` `namespace` `std; ``// Linked List Node ``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next; ``}; ``// A utility function to create a new node ``Node* newNode(` `int` `key) ``{ ` `Node *temp =` `new` `Node; ` `temp->data = key; ` `temp->next = NULL; ` `return` `temp; ``} ``// Rearranges given linked list such that all even ``// positioned nodes are before odd positioned. ``// Returns new head of linked List. ``Node *rearrangeEvenOdd(Node *head) ``{ ` `// Corner case ` `if` `(head == NULL) ` `return` `NULL; ` HTG263] `// Initialize first nodes of even and ` `// odd lists ` `Node *odd = head; `​​  `Node *even = head->next; ` `// Remember the first node of even list so ` `// that we can connect the even list at the ` `// end of odd list. ` ] `Node *evenFirst = even; ` `while` `(1) ` `{ ` `// If there are no more nodes, then connect ` `// first node of even list to the last node ` `// of odd list ` `if` `(!odd &#124;&#124; !even &#124;&#124; !(even->next)) ` `{ ` `odd->next = evenFirst; ` `break` `; ` `} ` `// Connecting odd nodes ` `odd->next = even->next; ` `odd = even->next; ` `// If there are NO more even nodes after ` `// current odd. ` `if` `(odd->next == NULL) ` `{ ` `even->next = NULL; ` `odd->next = evenFirst; ` `break` `; ` `} `[ `// Connecting even nodes ` `even->next = odd->next; ` `even = odd->next; ` `} ` `return` `head; ``} ``// A utility function to print a linked list ``void` `printlist(Node * node) ``{ ` `while` `(node != NULL) `[HTG3 56]  `{ ` `cout << node->data <<` `"->"` `; ` `node = node->next; ` `} ` `cout <<` `"NULL"` `<< endl; ``} ``// Driver code ``int` `main(` `void` `) ``{ ` `Node *head = newNode(1); ` `head->next = newNode(2); ` `head->next->next = newNode(3); ` `head->next->next->next = newNode(4); ` `head->next->next->next->next = newNode(5); ` `cout <<` `"Given Linked List\n"` `; ` `printlist(head); ` `head = rearrangeEvenOdd(head); ` ] `cout <<` `"Modified Linked List\n"` `; ` `printlist(head); ` [HTG4 03] `return` `0; ``} ``// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*