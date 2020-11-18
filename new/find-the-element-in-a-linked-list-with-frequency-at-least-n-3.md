# 在链表中查找频率至少为N / 3的元素

给定大小为 **N** 的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，其中包含字符串作为节点值，任务是查找频率大于 **[N / 3]** 的多数字符串 ]，在链接列表中。
**注意：**确保只有一个多数字符串。

**示例：**

> **输入：**头->怪胎->怪胎-> abcd->游戏->骑士->怪胎->哈利。
> **输出：**怪胎。
> **说明：**
> 链接列表中极客字符串的频率为3，大于[7/3]，即2。
> 
> **输入：**头->热->热->冷->热->热
> **输出：**热
> [ **解释：**
> 链接列表中热字符串的频率为4，大于[5/3]，即1。

**天真的方法：**
将每个字符串的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。 遍历地图并查找频率为**≥N / 3** 的字符串。
***时间复杂度：** O（N）*
***辅助空间：** O（N）*

**有效方法：**
这个想法基于 [Moore的投票算法](https://www.geeksforgeeks.org/majority-element/)。
找到两个候选人，并检查这两个候选人中的任何一个是否实际上是多数派。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find an``// element with frequency``// of at least N / 3``// in a linked list`的`#include <bits/stdc++.h>``using` `namespace` `std;``// Structure of a node``// for the linked list``struct` `node {` `string i;` `node* next = NULL;``};``// Utility function to``// create a node``struct` `node* newnode(string s)``{` `struct` `node* temp = (` `struct` `node*)` `malloc` `(` `sizeof` `(` `struct` `node));` `temp->i = s;` `temp->next = NULL;` `return` `temp;``}``// Function to find and return``// the element with frequency``// of at least N/3``string Majority_in_linklist(node* head)``{` `// Candidates for` `// being the required` `// majority element` `string s =` `""` `, t =` `""` `;`[ `// Store the frequencies` `// of the respective candidates` `int` `p = 0, q = 0;` `node* ptr = NULL;` `// Iterate all nodes` `while` `(head != NULL) {` `if` `(s.compare(head->i) == 0) {` `// Increase frequency` `// of candidate s` `p = p + 1;` `}` `else` `{` `if` `(t.compare(head->i) == 0) {` `// Increase frequency` `// of candidate t` `q = q + 1;` `}` `else` `{` `if` `(p == 0) {` `// Set the new sting as` `// candidate for majority` `s = head->i;` `p = 1;` `}` `else` `{` `if` `(q == 0) {` `// Set the new sting as` `// second candidate` `// for majority` `t = head->i;` `q = 1;` `}` `else` `{` `// Decrease the frequency`[  `p = p - 1;` `q = q - 1;` `}` `}` `}` `}` `head = head->next;` `}` `head = ptr;` `p = 0;` `q = 0;` `// Check the frequency of two` `// final selected candidate linklist` `while` `(head != NULL) {` `if` `(s.compare(head->i) == 0) {` `// Increase the frequency` `// of first candidate` `p = 1;` `}` `else` `{` `if` `(t.compare(head->i) == 0) {` `// Increase the frequency` `// of second candidate` `q = 1;` `}` `}`[H TG200] `head = head->next;` `}` `// Return the string with` `// higher frequency` `if` `(p > q) {` `return` `s;` `}` `else` `{` `return` `t;` `}``}``// Driver Code``int` `main()``{` `node* ptr = NULL;` `node* head = newnode(` `"geeks"` `);` `head->next = newnode(` `"geeks"` `);` `head->next->next = newnode(` `"abcd"` `);` `head->next->next->next` `= newnode(` `"game"` `);` `head->next->next->next->next` `= newnode(` `"game"` `);` [HTG52 3] `head->next->next->next->next->next` `= newnode(` `"knight"` `);` `head->next->next->next->next->next->next` `= newnode(` `"harry"` `);` `head->next->next->next->next->next->next` `->next` ​​ `= newnode(` `"geeks"` `);` `cout << Majority_in_linklist(head) << endl;` `return` `0;`[`}` |

*chevron_right**filter_none*