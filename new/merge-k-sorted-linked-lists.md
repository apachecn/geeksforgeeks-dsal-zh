# 合并K个排序的链表| 设置1

给定K个大小均为N的排序链表，将它们合并并打印排序后的输出。

**示例：**

```
Input: k = 3, n =  4
list1 = 1->3->5->7->NULL
list2 = 2->4->6->8->NULL
list3 = 0->9->10->11->NULL

Output: 0->1->2->3->4->5->6->7->8->9->10->11
Merged lists in a sorted order 
where every element is greater 
than the previous element.

Input: k = 3, n =  3
list1 = 1->3->7->NULL
list2 = 2->4->8->NULL
list3 = 9->10->11->NULL

Output: 1->2->3->4->7->8->9->10->11
Merged lists in a sorted order 
where every element is greater 
than the previous element.

```

 <u>**方法1（简单）**</u>
**方法：**
一个简单的解决方案是将结果初始化为第一列表。 现在从第二个列表开始遍历所有列表。 以排序的方式将当前遍历列表的每个节点插入到结果中。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to merge k sorted``// arrays of size n each``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A Linked List node``struct` `Node {` `int` `data;` `Node* next;``};``/* Function to print nodes in ` `a given linked list */``void` `printList(Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}``}`​​  [`// The main function that``// takes an array of lists``// arr[0..last] and generates``// the sorted output``Node* mergeKLists(Node* arr[],` `int` `last)``{` `// Traverse form second list to last` `for` `(` `int` `i = 1; i <= last; i++) {` `while` `(` `true` `) {` `// head of both the lists,` `// 0 and ith list.` `Node *head_0 = arr[0], *head_i = arr[i];` `// Break if list ended` `if` `(head_i == NULL)` `break` `;` `// Smaller than first element` `if` `(head_0->data >= head_i->data) {` `arr[i] = head_i->next;` `head_i->next = head_0;` `arr[0] = head_i;` `}` `else` `// Traverse the first list` `while` `(head_0->next != NULL) {` `// Smaller than next element` `if` `(head_0->next->data` `>= head_i->data) {` `arr[i] = head_i->next;` `head_i->next = head_0->next;` `head_0->next = head_i;` `break` `;` `}` `// go to next node` `head_0 = head_0->next;` `// if last node` `if` `(head_0->next == NULL) {` `arr[i] = head_i->next;` `head_i->next = NULL;` `head_0->next = head_i;` `head_0->next->next = NULL;` `break` `;` `}` `}` `}` `}` `return` `arr[0];``}``// Utility function to create a new node.``Node* newNode(` `int` `data)``{` `struct` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``// Driver program to test``// above functions``int` `main()``{` `// Number of linked lists` `int` `k = 3;` `// Number of elements in each list` `int` `n = 4;`]  `// an array of pointers storing the` `// head nodes of the linked lists` `Node* arr[k];` `arr[0] = newNode(1);` `arr[0]->next = newNode(3);` `arr[0]->next->next = newNode(5);`[HT G430]  `arr[0]->next->next->next = newNode(7);` `arr[1] = newNode(2);` `arr[1]->next = newNode(4);` `arr[1]->next->next = newNode(6);` `arr[1]->next->next->next = newNode(8);` `arr[2] = newNode(0);` `arr[2]->next = newNode(9);`] `arr[2]->next->next = newNode(10);` `arr[2]->next->next->next = newNode(11);` `// Merge all lists` `Node* head = mergeKLists(arr, k - 1);` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none***Output:**

```
0 1 2 3 4 5 6 7 8 9 10 11

```

**复杂度分析：**

*   **时间复杂度：** O（N <sup>2</sup> ），其中N是节点总数，即N = kn。
*   **辅助空间：** O（1）。
    由于不需要额外的空间。

 <u>**方法2**</u> ： [**最小堆**](https://www.geeksforgeeks.org/min-heap-in-java/) 。
更好的解决方案是使用基于Min Heap的解决方案，在此处讨论了基于数组的解决方案。 该解决方案的时间复杂度为 **O（nk Log k）**

 <u>**方法3**</u> ： [**分而治之**](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/) 。
在这篇文章中，讨论了**分而治之**方法。 这种方法不需要额外的堆空间，可以在O（nk Log k）中使用

众所周知，可以在O（n）时间和O（1）空间（对于数组需要O（n）空间）中完成两个链表的[合并。](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

1.  这个想法是将K个列表配对并使用O（1）空间在线性时间内合并每对。
2.  在第一个循环之后，剩下的K / 2个列表的大小均为2 * N。 在第二个循环之后，剩下的K / 4个列表的大小均为4 * N，依此类推。
3.  重复该过程，直到只剩下一个列表。

以下是上述想法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to merge k sorted``// arrays of size n each``#include <bits/stdc++.h>``using` `namespace` `std;` [`// A Linked List node``struct` `Node {` `int` `data;` `Node* next;``};``/* Function to print nodes in ` `a given linked list */``void` `printList(Node* node)``{` `while` `(node != NULL) {` `printf` `(` `"%d "` `, node->data);` `node = node->next;` `}``}` [`/* Takes two lists sorted in increasing order, and merge` `their nodes together to make one big sorted list. Below` `function takes O(Log n) extra space for recursive calls,` `but it can be easily modified to work with same time and`​​ `O(1) extra space  */``Node* SortedMerge(Node* a, Node* b)``{` `Node* result = NULL;` `/* Base cases */` `if` ] `(a == NULL)` `return` `(b);` `else` `if` `(b == NULL)` `return` `(a);` `/* Pick either a or b, and recur */` `if` `(a->data <= b->data) {` `result = a;` `result->next = SortedMerge(a->next, b);` `}` `else` `{` `result = b;` `result->next = SortedMerge(a, b->next);` `}` `return` `result;``}``// The main function that takes an array of lists``// arr[0..last] and generates the sorted output``Node* mergeKLists(Node* arr[],` `int` `last)`[HT G325] `{` `// repeat until only one list is left` `while` `(last != 0) {` `int` `i = 0, j = last;` `// (i, j) forms a pair` `while` `(i < j) {` `// merge List i with List j and store` `// merged list in List i` `arr[i] = SortedMerge(arr[i], arr[j]);` `// consider next pair` `i++, j--;` `// If all pairs are merged, update last` `if` `(i >= j)` `last = j;` `}` `}` `return` `arr[0];``}``// Utility function to create a new node.``Node* newNode(` `int` `data)``{` `struct` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}` [`// Driver program to test above functions``int` `main()``{` `int` `k = 3;` `// Number of linked lists` `int` `n = 4;` `// Number of elements in each list` `// an array of pointers storing the head nodes` `// of the linked lists` `Node* arr[k];`] `arr[0] = newNode(1);` `arr[0]->next = newNode(3);` `arr[0]->next->next = newNode(5);` `arr[0]->next->next->next = newNode(7);` `arr[1] = newNode(2);` 2] `arr[1]->next->next = newNode(6);` `arr[1]->next->next->next = newNode(8);` `arr[2] = newNode(0);` `arr[2]->next = newNode(9);` `arr[2]->next->next = newNode(10);` `arr[2]->next->next->next = newNode(11);` `// Merge all lists` ] `Node* head = mergeKLists(arr, k - 1);` `printList(head);`[  `return` `0;``}` |

*chevron_right**filter_none*