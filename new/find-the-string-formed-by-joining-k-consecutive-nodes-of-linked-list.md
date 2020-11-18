# 查找通过链接链接列表

的k个连续节点形成的字符串

给定一个整数 **K** 和一个链表，其中每个节点都存储一个字符。 任务是加入链表的每个 **K** 个连续节点，以形成一个单词。 最后，打印通过连接这些单词获得的字符串（以空格分隔）。

**示例：**

> **输入：**列表='a'->'b'->'c'->'d'->'e'-> NULL，k = 3
> **输出：** abc de
> 前三个节点形成第一个单词“ abc”
> ，后两个节点形成第二个单词“ de”。
> 
> **输入：**列表='a'->'b'->'c'->'d'->'e'->'f'-> NULL，k = 2
> **输出：** ab cd ef

**方法：**想法是遍历链表，并在每个结点处添加字符，直到到目前为止形成的单词。 跟踪遍历的节点数，当计数等于k时，将到目前为止形成的单词添加到结果字符串中，将单词重置为空字符串，并将计数重置为零。 重复此操作，直到没有遍历整个链表。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Structure of a node``struct` `Node {` `char` `data;` `Node* next;``};``// Function to get a new node``Node* getNode(` `char` `data)``{` `// Allocate space` `Node* newNode =` `new` `Node;` `// Put in data` `newNode->data = data;` `newNode->next = NULL;` `return` `newNode;``}` HTG225]`// Function to find string formed by joining words``// obtained by joining k consecutive nodes of``// linked list.``string findKWordString(Node* head,` `int` `k)``{`[HTG23 6]  `// Stores the final string` `string ans =` `""` `;` `// Keep track of the number of` `// nodes traversed` `int` `cnt = 0;` `// Stores the word formed by k consecutive` `// nodes of the linked list` `string word =` `""` `;` `while` `(head) {` `// Check if k nodes are traversed` `// If yes then add the word obtained` `// to the result string` `if` `(cnt == k) {`​​  `if` `(ans !=` `""` `) {` `ans = ans +` `" "` `;` `}` `ans = ans + word;` `word =` `""` `;` [ `cnt = 0;` `}` `// Add the current character to the word` `// formed so far and increase the count` `word = word + string(1, head->data);` `cnt++;` `head = head->next;` `}` `// Add the final word to the result` `// Length of the final word can be less than k` `if` `(ans !=` `" "` `) {` `ans = ans +` `" "` `;` `}` `ans = ans + word;` `return` `ans;``}``// Driver code``int` `main()``{` `// Create list: a -> b -> c -> d -> e`[HTG3 32]  `Node* head = getNode(` `'a'` `);` `head->next = getNode(` `'b'` `);` `head->next->next = getNode(` `'c'` `);` `head->next->next->next = getNode(` `'d'` `);` `head->next->next->next->next = getNode(` `'e'` `);` `int` `k = 3;` `cout << findKWordString(head, k);` [ `return` `0;``}` |

*chevron_right**filter_none*