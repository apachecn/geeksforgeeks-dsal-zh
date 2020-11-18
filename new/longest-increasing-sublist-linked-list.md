# 链表中最长的子列表

给定一个单链表，我们要计算不断增加的元素并打印出不断增加的链表。

**示例：**

```
Input  : 8 -> 5 -> 7 -> 10 -> 9 -> 11 -> 12 -> 13 -> NULL
Output : Number of continuously increasing elements = 4      
         Increasing linked list : 9 11 12 13

Input : 5 -> 12 -> 18 -> 7 -> 12 -> 15 -> NULL
Output : Number of continuously increasing elements = 3
         Increasing linked list = 5 12 18

```

这个想法是遍历单链表，并比较curr-> data和curr-> next-> data，其中curr是要遍历的当前节点。 如果curr-> data较小，则curr-> next-> data则curr指针指向curr-> next，并将长度（连续增加的元素）加1。 如果条件为假，则将长度与max进行比较，如果max小于len，则将len值分配给max。 继续此过程，直到head不等于NULL。 还要找到连续增加元素的起始指标。 接下来遍历链表，并在链表中显示连续增加的元素。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Program to count maximum number of continuous``// increasing element in linked list and display``// the elements of linked list.``#include <bits/stdc++.h>``using` `namespace` `std;``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function that count maximum number of continuous`​​ `// increasing elements in linked list and display``// the list.``void` `countIncreasingElements(` `struct` `Node *head)``{` `// Traverse the list and keep track of max increasing` `// and current increasing lengths` `int` `curr_len = 1, max_len = 1;` `int` `total_count = 1, res_index = 0;` `for` `(Node *curr=head; curr->next!=NULL; curr=curr->next)` `{` `// Compare head->data with head->next->data` `if` `(curr->data < curr->next->data)` `curr_len++;` `else` `{` `// compare maximum length with len.` `if` `(max_len < curr_len)` `{` `max_len = curr_len;` `res_index = total_count - curr_len;` `}`的 `curr_len = 1;` `}` `total_count++;` `}`[ `if` `(max_len < curr_len)` `{` `max_len = curr_len;` `res_index = total_count - max_len;` `}` `// Print the maximum number of continuous elements` `// in linked list.` `cout <<` `"Number of continuously increasing element"` `" in list : "` `;` `cout << max_len << endl;` [ `// Traverse the list again to print longest increasing` `// sublist` `int` `i = 0;` `cout <<` `"Increasing linked list"` `<< endl;` `for` `(Node* curr=head; curr!=NULL; curr=curr->next)` `{` `// compare with starting index and index of` `// maximum increasing elements if both are` `// equals then execute it.` `if` `(i == res_index)` `{` `// loop until max greater then 0\.` `while` `(max_len > 0)` `{` `// Display the list and temp point` `// to the next element.` `cout << curr->data <<` `" "` `;` `curr = curr->next;` `max_len--;` `}` `break` `;` `}`[H `i++;` `}``}``// Function to insert an element at the beginning``void` `push(` `struct` `Node** head,` `int` `data)``{` `struct` `Node* newNode =` `new` `Node;` `newNode->data = data;` `newNode->next = (*head);` `(*head) = newNode;``}``// Display linked list.``void` `printList(` `struct` `Node* node)``{` `while` `(node != NULL) {` `cout << node->data <<` `" "` `;` `node = node->next;` `}` `cout << endl;``}`[HTG44 0] `// Driver functions``int` `main()``{` `// Create a node and initialize with NULL` `struct` `Node* head = NULL;` `// push() insert node in linked list.` `// 15 -> 18 -> 5 -> 8 -> 11 -> 12` `push(&head, 12);` `push(&head, 11);` `push(&head, 8);` `push(&head, 5);` `push(&head, 18);` `push(&head, 15);` `cout <<` `"Linked list:"` `<< endl;` `printList(head);` `// Function call countIncreasingElements(head)` `// cout << countIncreasingElements(head) << endl;` `countIncreasingElements(head);` `return` `0;`]`}` |

*chevron_right**filter_none*