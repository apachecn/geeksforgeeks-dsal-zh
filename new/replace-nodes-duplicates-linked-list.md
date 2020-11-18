# 用链接列表

中的重复项替换节点

给定一个链表，其中包含一些从1到n的随机整数，并且有很多重复项。 用值n + 1，n + 2，n + 3等替换链表中存在的每个重复元素（以给定链表中的从左到右开始）。

**示例：**

```
Input : 1 3 1 4 4 2 1
Output : 1 3 5 4 6 2 7
Replace 2nd occurrence of 1 with 5 i.e. (4+1)
        2nd occurrence of 4 with 6 i.e. (4+2)
        3rd occurrence of 1 with 7 i.e. (4+3)

Input : 1 1 1 4 3 2 2
Output : 1 5 6 4 3 2 7

```

**方法：**
1.遍历链表，在映射中存储链表中每个数字的频率，并找到链表中存在的最大整数，即 **maxNum** 。
2.现在，再次遍历链表，如果任意数字的频率大于1，则在第一次出现时将其值设置为-1。
3.这样做的原因是，在下一次出现此数字时，我们将找到它的值-1，这意味着此数字之前已发生，请使用maxNum + 1更改其数据并递增maxNum。

下面是想法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to replace duplicates ``// in an unsorted linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Utility function to create a new Node``struct` `Node* newNode(` `int` `data)``{` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``// Function to replace duplicates from a ``// linked list``void` `replaceDuplicates(` `struct` `Node* head)``{` `// map to store the frequency of numbers` `unordered_map<` `int` `,` `int` `> mymap;` `Node* temp = head;` `// variable to store the maximum number` `// in linked list` `int` `maxNum = 0;` `// traverse the linked list to store ` `// the frequency of every number and `​​ `// find the maximum integer` `while` `(temp) {` `mymap[temp->data]++;` `if` `(maxNum < temp->data)` `maxNum = temp->data;` `temp = temp->next;` `}` `// Traverse again the linked list` `while` `(head) {` `// Mark the node with frequency more` `// than 1 so that we can change the` `// 2nd occurrence of that number` `if` `(mymap[head->data] > 1)` [HTG1 01] `// -1 means number has occurred ` `// before change its value` `else` `if` `(mymap[head->data] == -1)` `head->data = ++maxNum;` `head = head->next;` `}``}``/* Function to print nodes in a given``linked list */``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}` `cout << endl;``}``/* Driver program to test above function */``int` `main()``{` `/* The constructed linked list is:` `1->3->1->4->4->2->1*/` `struct` `Node* head = newNode(1);` `head->next = newNode(3);` `head->next->next = newNode(1);` `head->next->next->next = newNode(4);` `head->next->next->next->next = ` `newNode(4);` `head->next->next->next->next->` `next = newNode(2);` `head->next->next->next->next->` `next->next = newNode(1);`的 `cout <<` `"Linked list before replacing"` `<<` `" duplicates\n"` `;` `printList(head);` `replaceDuplicates(head);` `cout <<` `"Linked list after replacing"` `<<` `" duplicates\n"` `;` `printList(head);` `return` `0;` [`}` |

*chevron_right**filter_none*