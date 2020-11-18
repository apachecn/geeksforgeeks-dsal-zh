# 检查链接列表是否成对排序

给定一个链表。 任务是检查链接列表是否成对排序。

如果每个连续的数字对都按排序（非降序）顺序，则认为链表是成对排序的。 如果节点数为奇数，则忽略最后一个节点，并且结果基于剩余的偶数个节点。

**示例：**

```
Input: List =  10 -> 15 -> 9 -> 9 -> 1 -> 5
Output: YES

Input: List = 10 -> 15 -> 8 -> 9 -> 10 -> 5
Output: NO

```

**方法：**的想法是从左到右遍历链表。 成对比较节点，如果任何一对违反属性，则返回false。 如果没有一对违反属性，则返回True。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to check if linked list is``// pairwise sorted``#include <iostream>``using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to check if linked list is``// pairwise sorted``bool` `isPairWiseSorted(` `struct` `Node* head)``{` `bool` `flag =` `true` `;` `struct` `Node* temp = head;` `// Traverse further only if there` `// are at-least two nodes left` `while` `(temp != NULL && temp->next != NULL) {` `if` `(temp->data > temp->next->data) {` `flag =` `false` `;` `break` `;` `}` `temp = temp->next->next;` `}` `return` `flag;``}``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Driver program to test above function``int` `main()``{` `struct` `Node* start = NULL;` `/* The constructed linked list is: ` `10->15->9->9->1->5 */` `push(&start, 5);` `push(&start, 1);` `push(&start, 9);`​​ `push(&start, 9);` `push(&start, 15);` `push(&start, 10);` `if` `(isPairWiseSorted(start))` `cout <<` `"YES"` `;` `else` `cout <<` `"NO"` `;` `return` `0;``}` |

*chevron_right**filter_none*