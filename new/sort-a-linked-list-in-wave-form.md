# 以波形形式

对链接列表进行排序

给定未排序的整数链接列表。 任务是将“链表”分类为“线”之类的波形。 如果排序后的列表采用以下形式，则称链接列表按Wave形式排序：

```
list[0] >= list[1] <= list[2] >= …..

```

其中list [i]表示链表的第i个节点处的数据。

**范例**：

```
Input : List = 2 -> 4 -> 6 -> 8 -> 10 -> 20
Output : 4 -> 2 -> 8 -> 6 -> 20 -> 10

Input : List = 3 -> 6 -> 5 -> 10 -> 7 -> 20
Output : 6 -> 3 -> 10 -> 5 -> 20 -> 7

```

**简单解决方案**将使用排序。 首先对输入链表进行排序，然后交换所有相邻元素。

例如，让输入列表为 **3-> 6-> 5-> 10-> 7-> 20** 。 排序后，我们得到 **3-> 5-> 6-> 7-> 10-> 20** 。 交换相邻元素后，我们得到 **5-> 3-> 7-> 6-> 20-> 10** ，这是波形的必需列表。

**时间复杂度**：O（N * logN），其中N是列表中的数字节点。

**高效解决方案**：这可以通过一次遍历给定列表在O（n）时间内完成。 这个想法基于这样一个事实，即如果我们确保所有偶数定位（索引0、2、4，..）的元素都大于其相邻的奇数元素，那么我们就不必担心奇数位置的元素。 以下是简单的步骤。

**注意**：假定列表中的索引从零开始。 也就是说，list [0]代表链接列表的前几个元素。

遍历输入链表的所有偶数定位元素，然后执行以下操作。

*   如果当前元素小于前一个奇数元素，则交换前一个和当前元素。
*   如果当前元素小于下一个奇数元素，则交换下一个和当前元素。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to sort linked list``// in wave form``#include <climits>``#include <iostream>``using` `namespace` `std;``// A linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to add a node at the``// beginning of Linked List``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));`的​​ `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Function get size of the list``int` `listSize(` `struct` `Node* node)``{` `int` `c = 0;` `while` `(node != NULL) {` `c++;` `node = node->next;` `}` `return` `c;``}``// Function to print the list``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` [ `node = node->next;` `}``}``/* UTILITY FUNCTIONS */``/* Function to swap two integers */``void` `swap(` `int` `* a,` `int` `* b)``{` `int` `temp;` `temp = *a;` `*a = *b;` `*b = temp;``}``// Function to sort linked list in``// wave form``void` `sortInWave(` `struct` `Node* head)``{` `struct` `Node* current = head;` `struct` `Node* prev = NULL;` `// Variable to track even position`[ `int` `i = 0;` `// Size of list`[H TG147] `int` `n = listSize(head);` `// Traverse all even positioned nodes` `while` `(i < n) {` `if` `(i % 2 == 0) {` `// If current even element is` `// smaller than previous` `if` `(i > 0 && (prev->data > current->data))` `swap(&(current->data), &(prev->data));` `// If current even element is` `// smaller than next` `if` `(i < n - 1 && (current->data < current->next->data))` `swap(&(current->data), &(current->next->data));` `}` `i++;` `prev = current;` `current = current->next;` `}``}``// Driver program to test above function`[HTG43 1] `int` `main()``{` `struct` `Node* start = NULL;` `/* The constructed linked list is: ` `10, 90, 49, 2, 1, 5, 23*/` `push(&start, 23);` `push(&start, 5);` `push(&start, 1);` `push(&start, 2);` `push(&start, 49);` `push(&start, 90);` `push(&start, 10);` `sortInWave(start);` `printList(start);` `return` `0;``}` |

*chevron_right**filter_none*