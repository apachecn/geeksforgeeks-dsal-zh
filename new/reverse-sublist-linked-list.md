# 反向链接列表的子列表

我们得到了一个链表以及位置m和n。 我们需要将链接列表从位置m反向到n。

例子：

```
Input : 10->20->30->40->50->60->70->NULL
        m = 3, n = 6
Output : 10->20->60->50->40->30->70->NULL

Input :  1->2->3->4->5->6->NULL 
         m = 2, n = 4
Output : 1->4->3->2->5->6->NULL

```

要将链接列表从位置m反转为n，我们通过运行循环来找到链接列表的开始和结束位置的地址，然后将其与列表的其余部分取消链接，然后使用常规的[链接列表 反向功能](https://www.geeksforgeeks.org/reverse-a-linked-list/)，我们之前已使用它来反转完整的链表，并使用它来反转链表中需要反转的部分。 反转后，我们再次将反转的部分附加到主列表。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C program to reverse a linked list``// from position m to position n``#include <stdio.h>``#include <stdlib.h>`的`// Linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// the standard reverse function used``// to reverse a linked list``struct` `Node* reverse(` `struct` `Node* head)``{` `struct` `Node* prev = NULL;    ` `struct` `Node* curr = head;` `while` `(curr) {` `struct` `Node* next = curr->next;` `curr->next = prev;` `prev = curr;`​​  `curr = next;` `}` `return` `prev;``}``// function used to reverse a linked list``// from position m to n which uses reverse``// function``Node* reverseBetween(Node* head,` `int` `m,` `int` `n)` ]`{` `if` `(m == n)` `return` `head;`的 `// revs and revend is start and end respectively` `// of the portion of the linked list which` `// need to be reversed. revs_prev is previous` `// of starting position and revend_next is next` `// of end of list to be reversed.` `Node* revs = NULL, *revs_prev = NULL;` `Node* revend = NULL, *revend_next = NULL;` `// Find values of above pointers.` `int` `i = 1;` `Node* curr = head;` `while` `(curr && i <= n) {` `if` `(i < m)` `revs_prev = curr;` `if` `(i == m)`[H TG99] `revs = curr;` `if` `(i == n) {` `revend = curr;` `revend_next = curr->next;` `}` `curr = curr->next;` `i++;` `}` `revend->next = NULL;` `// Reverse linked list starting with` `// revs.` `revend = reverse(revs);` `// If starting position was not head` `if` `(revs_prev)` `revs_prev->next = revend;` `// If starting position was head` `else` `head = revend;` `revs->next = revend_next;` `return` `head;``}``void` `print(` `struct` `Node* head)``{` `while` `(head != NULL) {` `printf` `(` `"%d "` `, head->data);` `head = head->next;` `}` `printf` `(` `"\n"` `);``}``// function to add a new node at the``// beginning of the list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Driver code`[HTG4 24] `int` `main()``{` `struct` `Node* head = NULL;` `push(&head, 70);` `push(&head, 60);` `push(&head, 50);` `push(&head, 40);` `push(&head, 30);` `push(&head, 20);` `push(&head, 10);` `reverseBetween(head, 3, 6);` `print(head);` `return` `0;``}` |

*chevron_right**filter_none*

输出：

```
10 20 60 50 40 30 70 
```

本文由 **Akshit Agarwal** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。