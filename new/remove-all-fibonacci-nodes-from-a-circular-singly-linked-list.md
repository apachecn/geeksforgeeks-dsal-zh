# 从循环单链接列表

中删除所有斐波那契节点

给定一个包含 **N个**节点的[循环单链列表](https://www.geeksforgeeks.org/circular-linked-list/)，任务是从包含[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)数据值的列表中删除所有节点。

**示例：**

> **输入：** CLL = 9-> 11-> 34-> 6-> 13-> 20
> **输出：** 9-> 11-> 6-> 20
> **说明：**
> 该列表包含2个斐波那契数据值32和13。
> 因此，包含此数据的节点已被删除。 已删除
> 
> **输入：** 5-> 11-> 16-> 21-> 17-> 10
> **输出：** 11-> 16-> 17-> 10
> **说明：**
> 该列表包含2个斐波那契数据值5和21。
> 因此，删除了包含此数据的节点

**方法：**的想法是使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)来预先计算并存储[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，然后检查节点是否在O（1）时间中包含斐波那契值 。

1.  遍历整个圆形单链列表，并在列表中获得最大值。
2.  现在，为了检查斐波那契数，建立一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于圆单链接列表中最大值的斐波那契数。
3.  最后，逐个遍历循环单链列表的节点，并检查该节点是否包含斐波那契数作为其数据值。 删除具有斐波那契值的节点。

以下是上述想法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to delete all the``// Fibonacci nodes from the``// circular singly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Structure for a node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to insert a node at the beginning``// of a Circular linked list``void` `push(` `struct` `Node** head_ref,` `int` `data)``{` `// Create a new node and make head as next` `// of it.` `struct` `Node* ptr1` `= (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `struct` `Node* temp = *head_ref;` `ptr1->data = data;`[H TG52] `ptr1->next = *head_ref;` `// If linked list is not NULL then` `// set the next of last node` `if` `(*head_ref != NULL) {` `// Find the node before head` `// and update next of it.` `while` `(temp->next != *head_ref)` `temp = temp->next;` `temp->next = ptr1;` `}` `else` `// Point for the first node` `ptr1->next = ptr1;` `*head_ref = ptr1;``}``// Delete the node from a Circular Linked list``void` `deleteNode(Node* head_ref, Node* del)` ]`{` `struct` `Node* temp = head_ref;` `// If node to be deleted is head node` `if` `(head_ref == del)` `head_ref = del->next;` `// Traverse list till not found` `// delete node` `while` `(temp->next != del) {` `temp = temp->next;` `}` `// Copy the address of the node` `temp->next = del->next;` `// Finally, free the memory` `// occupied by del` `free` `(del);` `return` `;``}``// Function to find the maximum``// node of the circular linked list``int` `largestElement(` `struct` `Node* head_ref)``{` `// Pointer for traversing` `struct` `Node* current;` `// Initialize head to the current pointer` `current = head_ref;` `// Initialize min int value to max` `int` `maxEle = INT_MIN;`） `// While the last node is not reached` `do` `{` `// If current node data is` `// greater for max then replace it` `if` `(current->data > maxEle) {` `maxEle = current->data;` `}` `current = current->next;` `}` `while` `(current != head_ref);` `return` `maxEle;``}``// Function to create hash table to``// check Fibonacci numbers``void` `createHash(set<` `int` `>& hash,` `int` `maxElement)``{` `int` `prev = 0, curr = 1;` ]的 `// Adding the first two elements` `// to the hash` `hash.insert(prev);` `hash.insert(curr);` `// Inserting the Fibonacci numbers` `// into the hash` `while` `(curr <= maxElement) {` `int` `temp = curr + prev;` `hash.insert(temp);` `prev = curr;` `curr = temp;` `}``}``// Function to delete all the Fibonacci nodes``// from the singly circular linked list``void` `deleteFibonacciNodes(Node* head)``{` `// Find the largest node value` `// in Circular Linked List` `int` `maxEle = largestElement(head);` `// Creating a hash containing` `// all the Fibonacci numbers` `// upto the maximum data value` `// in the circular linked list` `set<` `int` `> hash;` `createHash(hash, maxEle);` `struct` `Node* ptr = head;` `struct` `Node* next;` ] `// Traverse the list till the end`​​ `do` `{` `// If the node's data is Fibonacci,` `// delete node 'ptr'` `if` `(hash.find(ptr->data)` `!= hash.end())` `deleteNode(head, ptr);` `// Point to the next node` [H TG289] `ptr = next;` `}` `while` `(ptr != head);``}``// Function to print nodes in a` ] `{` `struct` `Node* temp = head;` `if` `(head != NULL) {` `do` `{` `printf` `(` `"%d "` `, temp->data);` `temp = temp->next;` `}` `while` `(temp != head);` `}``}``// Driver code``int` `main()``{` `// Initialize lists as empty` `struct` `Node* head = NULL;` `// Created linked list will be` `// 9->11->34->6->13->20` `push(&head, 20);` `push(&head, 13);` `push(&head, 6);` `push(&head, 34);` `push(&head, 11);` `push(&head, 9);` `deleteFibonacciNodes(head);` `printList(head);` [ `return` `0;``}` |

*chevron_right**filter_none*