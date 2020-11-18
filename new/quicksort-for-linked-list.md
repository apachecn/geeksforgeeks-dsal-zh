# 双链接列表

上的快速排序

以下是数组的 [QuickSort](http://en.wikipedia.org/wiki/Quicksort) 的典型递归实现。 该实现使用last元素作为枢轴。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* A typical recursive implementation of Quicksort for array*/``/* This function takes last element as pivot, places the pivot element at its` `correct position in sorted array, and places all smaller (smaller than ` `pivot) to left of pivot and all greater elements to right of pivot */``int` `partition (` `int` `arr[],` `int` `l,` `int` `h)``{` `int` `x = arr[h];` `int` `i = (l - 1);` `for` `(` `int` `j = l; j <= h- 1; j++)` `{` `if` `(arr[j] <= x)` `{` `i++;` `swap (&arr[i], &arr[j]);` `}` `}` `swap (&arr[i + 1], &arr[h]);` `return` `(i + 1);``}``/* A[] --> Array to be sorted, l  --> Starting index, h  --> Ending index */``void` `quickSort(` `int` `A[],` `int` `l,` `int` `h)``{` `if` `(l < h)` `{        ` `int` `p = partition(A, l, h);` `/* Partitioning index */` `quickSort(A, l, p - 1);  ` `quickSort(A, p + 1, h);` `}``}` |

*chevron_right**filter_none*

**我们可以对链表使用相同的算法吗？**
以下是双向链表的C ++实现。 这个想法很简单，我们首先找出指向最后一个节点的指针。 一旦有了指向最后一个节点的指针，就可以使用指向链表的第一个和最后一个节点的指针对链表进行递归排序，类似于上面的递归函数，其中传递了第一个和最后一个数组元素的索引。 链表的分区功能也类似于数组的分区。 代替返回枢轴元素的索引，它返回指向枢轴元素的指针。 在以下实现中，quickSort（）只是一个包装函数，主要的递归函数是_quickSort（），类似于数组实现的quickSort（）。

![](img/907e6783a6130c711cfa83c52cb7210e.png)

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// A C++ program to sort a linked list using Quicksort ``#include <bits/stdc++.h>``using` `namespace` `std;``/* a node of the doubly linked list */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ` `Node *prev; ``}; ``/* A utility function to swap two elements */``void` `swap (` `int` `* a,` `int` `* b ) ``{` `int` `t = *a; *a = *b; *b = t; } ` [​​ `// A utility function to find``// last node of linked list ``Node *lastNode(Node *root) ``{ ` `while` `(root && root->next) ` `root = root->next; ` `return` `root; ``} ``/* Considers last element as pivot, ``places the pivot element at its ``correct position in sorted array, ``and places all smaller (smaller than ``pivot) to left of pivot and all greater``elements to right of pivot */``Node* partition(Node *l, Node *h) ``{ ` `// set pivot as h element ` `int` `x = h->data; `的 `// similar to i = l-1 for array implementation ` `Node *i = l->prev; ` `// Similar to "for (int j = l; j <= h- 1; j++)" ` `for` `(Node *j = l; j != h; j = j->next) ` `{ ` `if` `(j->data <= x) ` `{ ` `// Similar to i++ for array ` `i = (i == NULL)? l : i->next; ` `swap(&(i->data), &(j->data)); ` `} ` `} ` `i = (i == NULL)? l : i->next;` `// Similar to i++ ` `swap(&(i->data), &(h->data)); ` [HT G95] `i; ``} ``/* A recursive implementation ``of quicksort for linked list */``void` `_quickSort(Node* l, Node *h) ``{ ` `if` `(h != NULL && l != h && l != h->next) ` `{ ` `Node *p = partition(l, h); ` `_quickSort(l, p->prev); ` `_quickSort(p->next, h); ` `} ``} ``// The main function to sort a linked list.``// It mainly calls _quickSort() ``void` `quickSort(Node *head) ``{ ` `// Find last node ` `Node *h = lastNode(head); ` `// Call the recursive QuickSort ` `_quickSort(head, h);` ]`} ``// A utility function to print contents of arr ``void` `printList(Node *head)` [H TG397]`{ ` `while` `(head) ` `{ ` `cout << head->data <<` `" "` `; ` `head = head->next; ` `} ` `cout << endl; ``} ``/* Function to insert a node at the ``beginging of the Doubly Linked List */``void` `push(Node** head_ref,` `int` `new_data) ``{ ` `Node* new_node =` `new` `Node;` `/* allocate node */` `new_node->data = new_data; `的 `/* since we are adding at the` `beginning, prev is always NULL */` `new_node->prev = NULL; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* change prev of head node to new node */` `if` `((*head_ref) != NULL) (*head_ref)->prev = new_node ; ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``}` ]`/* Driver code */``int` `main() ``{ ` `Node *a = NULL; ` `push(&a, 5); ` `push(&a, 20); ` `push(&a, 4); ` `push(&a, 3); ` `push(&a, 30); ` `cout <<` `"Linked List before sorting \n"` `; ` `printList(a); ` `quickSort(a); ` `cout <<` `"Linked List after sorting \n"` `; ` `printList(a); ` `return` `0; `[HTG4 96] `} `。`// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*