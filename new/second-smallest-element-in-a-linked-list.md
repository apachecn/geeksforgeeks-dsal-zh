# 链表中第二小的元素

给定整数数据的链接列表。 任务是编写一个程序，以有效地找到链表中存在的第二个最小元素。

**示例：**

```
Input : List = 12 -> 35 -> 1 -> 10 -> 34 -> 1
Output : The second smallest element is 10.

Input : List = 10 -> 5 -> 10
Output : The second largest element is 10.

```

**简单解决方案**将是首先按升序对链表进行排序，然后从排序的链表中打印第二个元素。 该解决方案的时间复杂度为O（nlogn）。

**更好的解决方案**是遍历链接列表两次。 在第一个遍历中找到最小元素。 在第二遍历中找到比在第一遍历中获得的元素更大的最小元素。 该解决方案的时间复杂度为O（n）。

更有效的**解决方案**是在单个遍历中查找第二小的元素。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to print second smallest``// value in a linked list``#include <climits>``#include <iostream>`的`using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to print the second``// smallest element``void` `print2smallest(` `struct` `Node* head)`[HTG1 86] `{` `int` `first = INT_MAX, second = INT_MAX;` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `if` `(temp->data < first) {` `second = first;` `first = temp->data;` `}` `// If current node's data is in between` `// first and second then update second` `else` `if` `(temp->data < second && temp->data != first)` `second = temp->data;` `temp = temp->next;` `}` `if` `(second == INT_MAX)` ] `"There is no second smallest element\n"` `;` `else` `cout <<` `"The second smallest element is "` `<< second;``}``// Driver program to test above function``int` `main()``{` `struct` `Node* start = NULL;` [ `/* The constructed linked list is:  ` `12 -> 35 -> 1 -> 10 -> 34 -> 1 */` `push(&start, 1);` `push(&start, 34);` `push(&start, 10);` `push(&start, 1);` `push(&start, 35);` `push(&start, 12);` `print2smallest(start);` `return` `0;``}` |

*chevron_right**filter_none*