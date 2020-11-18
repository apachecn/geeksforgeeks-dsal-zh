# 将所有出现的元素移到链表

中

给定一个链表和链表中的一个键，任务是将所有出现的给定键移动到链表的末尾，同时保持所有其他元素的顺序相同。

例子：

```
Input  : 1 -> 2 -> 2 -> 4 -> 3
         key = 2 
Output : 1 -> 4 -> 3 -> 2 -> 2

Input  : 6 -> 6 -> 7 -> 6 -> 3 -> 10
         key = 6
Output : 7 -> 3 -> 10 -> 6 -> 6 -> 6
```

一个**简单解决方案**是一个一个地找到链接列表中所有给定密钥的出现。 对于每个发现的事件，将其插入末尾。 直到所有出现的给定键都移到结尾为止。

时间复杂度：O（n <sup>2</sup> ）

**高效解决方案1：**保留两个指针：
**pCrawl** = >用来遍历整个列表的指针。
**pKey** = >如果找到了密钥，则指向发生密钥的指针。 其他与pCrawl相同。

我们从链接列表的开头开始上述两个指针。 仅当 **pKey** 未指向键时，才移动 **pKey** 。 我们总是移动 **pCrawl** 。 因此，当 **pCrawl** 和 **pKey** 不相同时，我们必须找到一个位于 **pCrawl** 之前的密钥，因此我们交换 **pCrawl** 的数据 和 **pKey** ，然后将 **pKey** 移动到下一个位置。 循环不变是交换数据后，从 **pKey** 到 **pCrawl** 的所有元素都是键。

下面是此方法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to move all occurrences of a``// given key to end.``#include <bits/stdc++.h>``// A Linked list Node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// A urility function to create a new node.``struct` `Node* newNode(` `int` `x)``{` `Node* temp =` `new` `Node;` `temp->data = x;` `temp->next = NULL;``}` [`// Utility function to print the elements``// in Linked list``void` `printList(Node* head)``{` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `printf` `(` `"%d "` `, temp->data);` `temp = temp->next;` `}` `printf` `(` `"\n"` `);``}``// Moves all occurrences of given key to``// end of linked list.``void` `moveToEnd(Node* head,` `int` `key)``{` `// Keeps track of locations where key` `// is present.` `struct` `Node* pKey = head;` `// Traverse list` `struct` `Node* pCrawl = head;` `while` `(pCrawl != NULL) {` `// If current pointer is not same as pointer` `// to a key location, then we must have found` `// a key in linked list. We swap data of pCrawl` `// and pKey and move pKey to next position.` `if` `(pCrawl != pKey && pCrawl->data != key) {` `pKey->data = pCrawl->data;` `pCrawl->data = key;` `pKey = pKey->next;` `}` `// Find next position where key is present` `if` `(pKey->data != key)` `pKey = pKey->next;`​​ `// Moving to next Node` `pCrawl = pCrawl->next;` `}``}` HTG282]`// Driver code``int` `main()``{` `Node* head = newNode(10);` `head->next = newNode(20);` `head->next->next = newNode(10);` `head->next->next->next = newNode(30);` `head->next->next->next->next = newNode(40);` `head->next->next->next->next->next = newNode(10);` `head->next->next->next->next->next->next = newNode(60);` `printf` `(` `"Before moveToEnd(), the Linked list is\n"` `);` `printList(head);` `int` `key = 10;` 8] `printf` `(` `"\nAfter moveToEnd(), the Linked list is\n"` `);` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*