# 计算链接列表中的最小频率元素

给定一个包含重复元素的链表。 任务是在给定的链表中查找所有最少出现的元素的数量。 这是矩阵中频率最小的所有此类元素的计数。

**范例**：

```
Input : 1-> 2-> 2-> 3
Output : 2
Explanation:
1 and 3 are elements occurs only one time.
So, count is 2.

Input : 10-> 20-> 20-> 10-> 30
Output : 1

```

**方法**：

*   遍历链表，并使用哈希表存储链表元素的频率，以使map的键为链表元素，值为链表中其频率。
*   然后遍历哈希表以找到最小频率。
*   最后，遍历哈希表以查找元素的频率，并检查其是否与上一步中获得的最小频率匹配，如果是，则添加此频率以进行计数。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find count of minimum``// frequqncy elements in Linked list``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `key;` `struct` `Node* next;``};``/* Given a reference (pointer to pointer) to the head ``of a list and an int, push a new node on the front ``of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_key)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->key = new_key;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to count minimum frequency elements``// in the linked list``int` `countMinimum(` `struct` `Node* head)``{`[HTG20 3]  `// Store frequencies of all nodes.` `unordered_map<` `int` `,` `int` `> mp;` `struct` `Node* current = head;` `while` `(current != NULL) {` `int` `data = current->key;` `mp[data]++;` `current = current->next;` `}` `// Find min frequency` `current = head;` `int` `min_frequency = INT_MAX, countMin = 0;` `for` `(` `auto` `it = mp.begin(); it != mp.end(); it++) {` `if` `(it->second <= min_frequency) {` `min_frequency = it->second;` `}` `}` `// Find count of min frequency elements` `for` `(` `auto` `it = mp.begin(); it != mp.end(); it++) {` `if` `(it->second == min_frequency) {` [ `countMin += (it->second);` `}` `}` `return` `countMin;``}``/* Driver program to test count function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `int` `x = 21;`​​ `/* Use push() to construct below list ` `10->10->11->30->10 */` `push(&head, 10);` `push(&head, 30);` `push(&head, 11);` `push(&head, 10);` `push(&head, 10);` `cout << countMinimum(head) << endl;` `return` `0;``}` |

*chevron_right**filter_none*