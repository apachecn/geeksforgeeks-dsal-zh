# 使用任意指针指向链表中的下一个较高值的节点

给定单链表，每个节点都有一个额外的“任意”指针，该指针当前指向NULL。 需要使“任意”指针指向下一个较高值的节点。

[![listwithArbit](img/8169f1fd5a3a7a6cf9da279cda5846a5.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/listwithArbit1.png)

**我们强烈建议您最小化您的浏览器，然后先尝试一下。**

一种**简单解决方案**是一个遍历所有节点，对于每个节点，查找当前节点中具有下一个更大值的节点，并更改下一个指针。 该解决方案的时间复杂度为O（n <sup>2</sup> ）。

有效的**解决方案**的工作时间为O（nLogn）。 这个想法是对链接列表使用[合并排序。
1）遍历输入列表，并将下一个指针复制到每个节点的仲裁指针。
2）对由仲裁指针形成的链表进行合并排序。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

以下是上述想法的实现。 所有合并排序功能均取自[这里](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)。 在此修改了采用的函数，以便它们在仲裁指针上工作，而不是在下一个指针上工作。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to populate arbit pointers ``// to next higher value using merge sort ``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next, *arbit; ``}; ``/* function prototypes */``Node* SortedMerge(Node* a, Node* b); ``void` `FrontBackSplit(Node* source, ` `Node** frontRef, Node** backRef); ``/* sorts the linked list formed by arbit pointers` ]`(does not change next pointer or data) */``void` `MergeSort(Node** headRef) ``{ ` `Node* head = *headRef; ` `Node* a, *b; ` `/* Base case -- length 0 or 1 */` `if` `((head == NULL) &#124;&#124; (head->arbit == NULL)) ` `return` `; ` `/* Split head into 'a' and 'b' sublists */` `FrontBackSplit(head, &a, &b); ` HTG52] `/* Recursively sort the sublists */` `MergeSort(&a); ` `MergeSort(&b); ` `/* answer = merge the two sorted lists together */` `*headRef = SortedMerge(a, b); ``} ``/* See [https://www.geeksforgeeks.org/?p=3622](https://www.geeksforgeeks.org/?p=3622) for  ``details of this function */`]`Node* SortedMerge(Node* a, Node* b) ``{ ` `Node* result = NULL; ` `/* Base cases */` `if` `(a == NULL) ` `return` `(b); ` `else` `if` `(b == NULL) ` `return` `(a); ` `/* Pick either a or b, and recur */` `if` `(a->data <= b->data) `] [HTG4 41]  `{ ` `result = a; ` `result->arbit = SortedMerge(a->arbit, b); ` `} ` `else` `{ ` `result = b; ` `result->arbit = SortedMerge(a, b->arbit); ` `} ` `return` `(result); ``} ``/* Split the nodes of the given list into front ``and back halves, and return the two lists using ``the reference parameters. If the length is odd, ``the extra node should go in the front list. ``Uses the fast/slow pointer strategy. */``void` `FrontBackSplit(Node* source, ` `Node** frontRef, Node** backRef) ``{ ` `Node* fast, *slow; ` `if` `(source == NULL &#124;&#124; source->arbit == NULL) ` `{ ` `/* length < 2 cases */` `*frontRef = source; ` `*backRef = NULL; ` `return` `; ` `} ` [ `slow = source, fast = source->arbit; ` `/* Advance 'fast' two nodes, and ` `advance 'slow' one node */` `while` `(fast != NULL) ` `{ ` `fast = fast->arbit; ` `if` `(fast != NULL) ` `{ ` `slow = slow->arbit; ` `fast = fast->arbit; ` `} ` `} ` `/* 'slow' is before the midpoint in the list, ` `so split it in two at that point. */` `*frontRef = source; ` `*backRef = slow->arbit; ` `slow->arbit = NULL; ``} ``/* Function to insert a node at the``beginging of the linked list */``void` `push(Node** head_ref,` `int` `new_data) ``{` ] `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `new_node->arbit = NULL; ` `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} ``// Utility function to print result linked list ``void` `printListafter(Node *node, Node *anode) ``{ ` `cout<<` `"Traversal using Next Pointer\n"` `; ` `while` `(node!=NULL) ` `{ ` `cout << node->data <<` `", "` `; ` `node = node->next; ` `} ` `printf` `(` `"\nTraversal using Arbit Pointer\n"` `); ` `while` `(anode!=NULL) ` `{ ` `cout << anode->data <<` `", "` `; ` `anode = anode->arbit; ` `} ``} ``// This function populates arbit pointer in every node to the ``// next higher value. And returns pointer to the node with ``// minimum value ``Node* populateArbit(Node *head) ``{ ` `// Copy next pointers to arbit pointers ` `Node *temp = head;` ​​ `while` `(temp != NULL) ` `{ ` `temp->arbit = temp->next; ` `temp = temp->next; ``/* sorts the linked list formed by arbit pointers` 0] `} ` `// Do merge sort for arbitrary pointers ` `MergeSort(&head); ` `// Return head of arbitrary pointer linked list ` `return` `head; ``} ``/* Driver program to test above functions*/``int` `main() ``{ ` `/* Start with the empty list */` `Node* head = NULL; ` `/* Let us create the list shown above */` `push(&head, 3); ` `push(&head, 2); ` `push(&head, 10); ` `push(&head, 5); ` `/* Sort the above created Linked List */` `Node *ahead = populateArbit(head); ` `cout <<` `"Result Linked List is: \n"` `; ` `printListafter(head, ahead); `[H TG693]  `return` `0; ``} ``// This is code is contributed by rathbhupendra` |

*chevron_right**filter_none*