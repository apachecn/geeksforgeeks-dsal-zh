# 在链表

中偶数位置节点的末尾反向附加奇数位置节点

给定一个链表。 任务是以这样一种方式隔离其偶数和奇数位置节点：奇数位置节点出现在偶数位置的节点之前，所有偶数位置的节点必须以相反的顺序出现。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6->空
> **输出：** 1-> 3-> 5-> 6-> 4-> 2-> NULL
> 
> **输入：** 1-> 2-> 3-> 4-> 5->空
> **输出：** 1-> 3-> 5-> 4-> 2->空

**来源：** [微软访谈](https://www.geeksforgeeks.org/microsoft-interview-experience-set-133-campus-internship/)

**方法：**在给定的[链接](https://www.geeksforgeeks.org/rearrange-a-linked-list-such-that-all-even-and-odd-positioned-nodes-are-together/)中讨论了类似的问题，但偶数部分未反转。 对于当前节点，分别在奇数和偶数位置维护两个指针**奇数**和**甚至**。 还存储偶数链接列表的第一个节点，以便在将所有奇数和偶数节点连接到两个不同的列表中之后，我们可以将偶数列表附加到奇数列表的末尾。 偶数列表分离后，我们只需要反转即可。 在此处可以找到反向链接列表。 一旦偶数列表反向，将其附加到奇数链接列表。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to Append odd position nodes``// in reverse at the end of even``// positioned nodes in a Linked List``#include <bits/stdc++.h>``using` `namespace` `std;``// Linked List Node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// A utility function to create a new node``Node* newNode(` `int` `key)``{` `Node* temp =` `new` `Node;` `temp->data = key;` `temp->next = NULL;` `return` `temp;``}` [`// Rearranges given linked list such that all even``// positioned nodes are before odd positioned ``// in a reverse``Node* rearrangeEvenOdd(Node* head)``{` `// Corner case` `if` `(head == NULL)` `return` `NULL;` `// Initialize first nodes of even and` HTG54] `Node* odd = head;` `Node* even = head->next;` `// Remember the first node of even list so` `// that we can connect the even list at the` `// end of odd list.` `Node* evenFirst = even;` ] `while` `(1) {` `// If there are no more nodes, then connect` `// first node of even list to the last node` `// of odd list` `if` `(!odd &#124;&#124; !even &#124;&#124; !(even->next)) {` `break` `;` `}` ［HTG306］ ［HTG307］ ［HTG88］ ［HTG89］ ［HTG308］ ［HTG309］ ［HTG90］ ［HTG91］ ［HTG310］ ［HTG311］ ［HTG92］ ［HTG93］ ［HTG312］ ［HTG313］ ［HTG94］ ［HTG314 ] `// If there are NO more even nodes after` `// current odd.` `if` `(odd->next == NULL) {` `even->next = NULL;` `break` `;` `}` `// Connecting evenevenFirs nodes` `even->next = odd->next;` `even = odd->next;` `}` `// Reversal of even linked list` `Node* current = evenFirst;` `Node* prev = NULL;` `Node* front = NULL;` `// Iterate in the complete linked list` `while` `(current != NULL) {` `front = current->next;` `current->next = prev;` `prev = current;` `current = front;` `}`的[HTG3 64] `evenFirst = prev;` `// Attach the reversed even linked` `// list to odd linked list` `odd->next = evenFirst;` `return` `head;``}``// A utility function to print a linked list``void` `printlist(Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" -> "` `;` `node = node->next;` `}` `cout <<` `"NULL"` `<< endl;``}``// Driver code``int` `main(` `void` `)``{`] `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);`[H TG191] `head->next->next->next = newNode(4);` `head->next->next->next->next = newNode(5);` `head->next->next->next->next->next = newNode(6);` `head = rearrangeEvenOdd(head);` `printlist(head);` `return` `0;`] `}` |

*chevron_right**filter_none*