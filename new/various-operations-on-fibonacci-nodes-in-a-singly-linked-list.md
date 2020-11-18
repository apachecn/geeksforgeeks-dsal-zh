# 单链接列表

中的斐波纳契节点上的各种操作

给定包含 **N个**节点的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是对其中存在的斐波纳契节点执行以下操作：

1.  打印[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)中存在的所有Fibonacci节点。
2.  查找[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)中存在的斐波纳契节点总数。
3.  找到最小和最大斐波那契节点。
4.  从[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)中删除所有Fibonacci节点。

**示例：**

> **输入：** LL = 15-> 16-> 8-> 6-> 13
> **输出：**
> 斐波那契节点= 8， 13
> 斐波那契节点数= 2
> 列表中的最小斐波那契节点= 8
> 列表中的最大斐波那契节点= 13
> 删除斐波那契节点后的列表= 15-> 16-> 6
> 
> **输入：** LL = 5-> 3-> 4-> 2-> 9
> **输出：**
> 斐波那契节点= 5， 3，2
> 斐波那契节点数= 3
> 列表中的最小斐波那契节点= 2
> 列表中的最大斐波那契节点= 5
> 删除斐波那契节点后的列表= 4-> 9

**方法：**的想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波纳契节点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)到链表中的最大值，以使检查变得容易和高效（ 在O（1）时间内）。

1.  遍历整个单链列表，并在列表中获得最大值。
2.  现在，构建一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于单链接列表中最大值的Fibonacci节点。

完成上述预计算后，我们可以在固定时间内检查数字是否为斐波那契。 因此，为了执行上述操作，使用了以下方法：

1.  **打印Fibonacci节点：**遍历链接列表，并检查数字是否为Fibonacci值。 如果是，则打印它。
2.  **计算Fibonacci节点的数量：**要计算链接列表中的Fibonacci节点的数量，我们遍历链接列表并检查该数量是否为Fibonacci值。
3.  **Find the minimum and the maximum Fibonacci nodes:** Traverse through the linked list and check if the value at a node is a Fibonacci or not. If yes:
    *   如果当前节点的值大于 **max** ，则将当前节点的值分配给max。
    *   如果当前节点的值小于 **min** ，则将当前节点的值分配给min。

    最后，max和min变量包含链表中存在的最大和最小斐波那契节点。

4.  **删除斐波那契节点：**为了删除斐波那契值，请遍历链接列表，如果数据为斐波那契，则使用[这种方法](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)删除包含数据的节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to perform the``// operations on Fibonacci nodes``// of a Singly Linked list``#include <bits/stdc++.h>``using` `namespace` `std;``set<``int``> hashmap;``// Node of the singly linked list``struct` `Node {``int` `data;``Node* next;``};``// Function to insert a node at the beginning``// of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{``// Allocate a new node``Node* new_node =` `new` `Node;``// Insert the data``new_node->data = new_data;``new_node->next = (*head_ref);``// Move the head to point the new node``(*head_ref) = new_node;``}``// Function to delete a node in a SLL``// head_ref --> pointer to head node pointer.``// del --> pointer to node to be deleted``void` `deleteNode(Node** head_ref, Node* del)``{``// Base case``struct` `Node* temp = *head_ref;``if` `(*head_ref == NULL &#124;&#124; del == NULL)``return``;``// If the node to be deleted is``// the head node``if` `(*head_ref == del)``*head_ref = del->next;``// Traverse list till not found``// delete node``while` `(temp->next != del) {``temp = temp->next;``}``// Copy address of node``temp->next = del->next;``// Finally, free the memory``// occupied by del``free``(del);``return``;``}``// Function that returns the largest element``// from the linked list.``int` `largestElement(``struct` `Node* head_ref)``{``// Declare a max variable and``// initialize it with INT_MIN value.``// INT_MIN is integer type and``// its value is -32767 or less.``int` `max = INT_MIN;``Node* head = head_ref;``// Loop to iterate the linked list``while` `(head != NULL) {``// If max is less than head->data then``// assign value of head->data to max``// otherwise node point to next node.``if` `(max < head->data)``max = head->data;``head = head->next;``}``return` `max;``}``// Function to create a hash table``// to check Fibonacci nodes``void` `createHash(``int` `maxElement)``{``// Insert the first two``// elements in the hash``int` `prev = 0, curr = 1;``hashmap.insert(prev);``hashmap.insert(curr);``// Add the elements until the max element``// by using the previous two numbers``while` `(curr <= maxElement) {``int` `temp = curr + prev;``hashmap.insert(temp);``prev = curr;``curr = temp;``}``}``// Function to print the Fibonacci``// nodes in a linked list``int` `printFibonacci(Node** head_ref)``{``int` `count = 0;``Node* ptr = *head_ref;``cout <<` `"Fibonacci nodes = "``;``while` `(ptr != NULL) {``// If current node is Fibonacci``if` `(hashmap.find(ptr->data)``!= hashmap.end()) {``// Update count``cout << ptr->data <<` `" "``;``}``ptr = ptr->next;``}``cout << endl;``return` `0;``}``// Function to find the count of Fibonacci``// nodes in a linked list``int` `countFibonacci(Node** head_ref)``{``int` `count = 0;``Node* ptr = *head_ref;``while` `(ptr != NULL) {``// If current node is Fibonacci``if` `(hashmap.find(ptr->data)``!= hashmap.end()) {``// Update count``count++;``}``ptr = ptr->next;``}``return` `count;``}``// Function to find maximum and minimum``// fibonacci nodes in a linked list``void` `minmaxFibonacciNodes(Node** head_ref)``{``// Find the largest node value``// in Singly Linked List``int` `maxEle = largestElement(*head_ref);``// Creating a set containing``// all the Fibonacci nodes``// upto the maximum data value``// in the Singly Linked List``// set<int> hash;``// createHash(hash, maxEle);``int` `minimum = INT_MAX;``int` `maximum = INT_MIN;``Node* ptr = *head_ref;``while` `(ptr != NULL) {``// If current node is fibonacci``if` `(hashmap.find(ptr->data)``!= hashmap.end()) {``// Update minimum``minimum``= min(minimum, ptr->data);``// Update maximum``maximum``= max(maximum, ptr->data);``}``ptr = ptr->next;``}``cout <<` `"Minimum Fibonacci node: "``<< minimum << endl;``cout <<` `"Maximum Fibonacci node: "``<< maximum << endl;``}``// Function to delete all the``// fibonacci nodes from the``// singly linked list``void` `deleteFibonacciNodes(Node** head_ref)``{``Node* ptr = *head_ref;``Node* next;``// Iterating through the linked list``while` `(ptr != NULL) {``next = ptr->next;``// If the node's data is fibonacci,``// delete node 'ptr'``if` `(hashmap.find(ptr->data) != hashmap.end())``deleteNode(head_ref, ptr);``ptr = next;``}``}``// Function to print nodes in a``// given singly linked list``void` `printList(Node* head)``{``while` `(head != NULL) {``cout << head->data <<` `" "``;``head = head->next;``}``}``void` `operations(``struct` `Node* head)``{``// Find the largest node value``// in Singly Linked List``int` `maxEle = largestElement(head);``// Creating a set containing``// all Fibonacci nodes``// upto the maximum data value``// in the Singly Linked List``createHash(maxEle);``// Print all Fibonacci nodes``printFibonacci(&head);``// Count of Fibonacci nodes``cout <<` `"Count of Fibonacci nodes = "``<< countFibonacci(&head) << endl;``// Minimum and maximum Fibonacci nodes``minmaxFibonacciNodes(&head);``// Delete Fibonacci nodes``deleteFibonacciNodes(&head);``cout <<` `"List after deletion: "``;``printList(head);``}``// Driver program``int` `main()``{``// Start with the empty list``Node* head = NULL;``// Create the linked list``// 15 -> 16 -> 8 -> 6 -> 13``push(&head, 13);``push(&head, 6);``push(&head, 8);``push(&head, 16);``push(&head, 15);``operations(head);``return` `0;``}` |

*chevron_right**filter_none*