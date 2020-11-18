# 反转链接列表节点

中的每个单词

给定一个字符串链接列表，我们需要反转给定链接列表中字符串的每个单词。

例子：

```
Input: geeksforgeeks a computer science portal for geeks 
Output: skeegrofskeeg a retupmoc ecneics latrop rof skeeg

Input: Publish your own articles on geeksforgeeks
Output: hsilbuP ruoy nwo selcitra no skeegrofskeeg 

```

使用循环将列表迭代到null，然后从每个节点获取字符串并反转字符串。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to reverse each word``// in a linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Linked list Node structure``struct` `Node {` `string c;` `struct` `Node* next;``};``// Function to create newNode``// in a linked list``struct` `Node* newNode(string c)``{` `Node* temp =` `new` `Node;` `temp->c = c;` `temp->next = NULL;` `return` `temp;``};``// reverse each node data``void` `reverse_word(string& str)``{` `reverse(str.begin(), str.end());``}``void` `reverse(` `struct` `Node* head)``{` `struct` `Node* ptr = head;` `// iterate each node and call reverse_word` `// for each node data` `while` `(ptr != NULL) {` `reverse_word(ptr->c);` `ptr = ptr->next;` ] `}``}``// printing linked list``void` `printList(` `struct` `Node* head)``{` `while` `(head != NULL) {` `cout << head->c <<` `" "` `;` `head = head->next;` `}``}``// Driver program``int` `main()``{` `Node* head = newNode(` `"Geeksforgeeks"` `);` [ `head->next = newNode(` `"a"` `);` `head->next->next = newNode(` `"computer"` `);` `head->next->next->next = newNode(` `"science"` `);` `head->next->next->next->next = newNode(` `"portal"` `);` `head->next->next->next->next->next = newNode(` `"for"` `);` `head->next->next->next->next->next->next = newNode(` `"geeks"` `);` `cout <<` `"List before reverse: \n"` `;` `printList(head);` `reverse(head);` `cout <<` `"\n\nList after reverse: \n"` `;`​​ `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*