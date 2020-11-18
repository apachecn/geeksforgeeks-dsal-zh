# 在链接列表中找到第二大元素

给定整数数据的链接列表。 任务是编写一个程序，以有效地找到链表中存在的第二大元素。

**范例**：

```
Input : List = 12 -> 35 -> 1 -> 10 -> 34 -> 1
Output : The second largest element is 34.

Input : List = 10 -> 5 -> 10
Output : The second largest element is 5.

```

**简单解决方案**将首先[按降序对链表](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)排序，然后从排序的链表中打印第二个元素。 该解决方案的时间复杂度为O（nlogn）。

**更好的解决方案**是遍历链接列表两次。 在第一个遍历中找到最大元素。 在第二遍历中找到小于在第一遍历中获得的元素的最大元素。 该解决方案的时间复杂度为O（n）。

一种更有效的**解决方案**是在单个遍历中查找第二大元素。
以下是完成此操作的完整算法：

```
1) Initialize two variables first and second to INT_MIN as,
   first = second = INT_MIN
2) Start traversing the Linked List,
   a) If the current element in Linked List say list[i] is greater
      than first. Then update first and second as,
      second = first
      first = list[i]
   b) If the current element is in between first and second,
      then update second to store the value of current variable as
      second = list[i]
3) Return the value stored in second node.

```

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to print second largest``// value in a linked list``#include <climits>``#include <iostream>`的`using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));`的 `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Function to count size of list``int` `listSize(` `struct` `Node* node)``{` `int` `count = 0;` `while` `(node != NULL) {`​​ `count++;` `node = node->next;` `}` `return` `count;``}``// Function to print the second``// largest element``void` `print2largest(` `struct` `Node* head)``{` `int` `i, first, second;` `int` `list_size = listSize(head);`[ HTG3 01]  [ `/* There should be atleast two elements */` `if` `(list_size < 2) {` `cout <<` `"Invalid Input"` `;` `return` `;` `}` `first = second = INT_MIN;` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `if` `(temp->data > first) {` `second = first;` `first = temp->data;` `}` `// If current node's data is in between` `// first and second then update second` `else` `if` `(temp->data > second && temp->data != first)` `second = temp->data;` `temp = temp->next;` `}` `if` `(second == INT_MIN)` `cout <<` `"There is no second largest element\n"` `;` `else` `cout <<` `"The second largest element is "` `<< second;``}``// Driver program to test above function``int` `main()``{` `struct` `Node* start = NULL;` `/* The constructed linked list is: ` `12 -> 35 -> 1 -> 10 -> 34 -> 1 */` `push(&start, 1);` `push(&start, 34);` `push(&start, 10);` `push(&start, 1);` `push(&start, 35);` `push(&start, 12);` `print2largest(start);` `return` `0;` ]`}` |

*chevron_right**filter_none*