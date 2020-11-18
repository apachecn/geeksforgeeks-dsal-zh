# 检查链接列表中的元素是否成对存在

给定一个整数的单链表。 任务是检查链接列表中的每个元素是否成对出现，即所有元素是否出现。 的时间。

**示例：**

```
Input: 1 -> 2 -> 3 -> 3 -> 1 -> 2
Output: Yes

Input: 10 -> 20 -> 30 -> 20
Output: No

```

**方法：**

*   初始化指向*头*的*临时*节点。
*   取一个变量来计算所有元素的 *XOR* 。
*   开始遍历链表，并继续使用node-> data计算XOR。
*   如果XOR为0，则返回true，否则返回false。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to check if elements of``// linked lists are present in pair``#include <bits/stdc++.h>``using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to check if elements of``// linked list are present in pair``bool` `isPair(` `struct` `Node* head)``{` `int` `xxor = 0;` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `xxor ^= temp->data;` `temp = temp->next;` `}` `return` [H TG47]`}``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Driver program to test above function``int` `main()``{` `struct` `Node* first = NULL;`[  `/* First constructed linked list is: ` `10 -> 34 -> 1 -> 10 -> 34 -> 1 */` `push(&first, 1);` `push(&first, 34);` `push(&first, 10);` `push(&first, 1);` `push(&first, 34);` `push(&first, 10);` `// Calling function to check pair elements` `if` `(!isPair(first)) {` `cout <<` `"Yes"` `<< endl;` `}` `else` `{`​​  `cout <<` `"No"` `<< endl;` `}` `return` `0;``}` |

*chevron_right**filter_none*