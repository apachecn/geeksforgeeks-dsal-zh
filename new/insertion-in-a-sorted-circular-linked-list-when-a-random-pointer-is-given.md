# 当给出随机指针时，插入到已排序的循环链表中

给定整数数组 **arr []** 和指向圆形排序链表（最初为空）的随机节点的指针，任务是插入 **arr []** 的所有元素 在循环链接列表中。

**示例：**

> **输入：** arr [] = {12，56，2，11，1，90}
> **输出：** 1 2 11 12 56 90
> 
> **输入：** arr [] = {6，2，78，45，200}
> **输出：** 2 6 45 78200

**方法：**我们得到了一个指向圆形链表中节点的随机指针，我们必须找到圆形链表的头，才能将该节点插入已排序的链表中。
这篇文章介绍了当给出head时插入到排序的链表中。
要查找循环排序链表的标题，请执行以下操作：

*   找到链表的最后一个节点（最后一个节点将大于其后继节点，即第一个元素。
*   一旦找到链表的开头，就可以使用与上一篇文章中讨论的相同的方法来插入元素。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Node structure``struct` `Node {` `Node* next;` `int` `data;``};``// Function to create a node``Node* create()``{` `Node* new_node = (Node*)` `(` `sizeof` `(Node));` `new_node->next = NULL;` `return` `new_node;``}`​​`// Function to find and return the head``Node* find_head(Node* random)``{` `// If the list is empty` `if` `(random == NULL)` `return` `NULL;` `Node *head, *var = random;` `// Finding the last node of the linked list` `// the last node must have the highest value` `// if no such element is present then all the nodes`] `// of the linked list must be same` `while` `(!(var->data > var->next->data &#124;&#124; var->next == random)) {` `var = var->next;` `}`[ `// Return the head` `return` `var->next;``}`的`// Function to insert a new_node in the list in sorted fashion``// Note that this function expects a pointer to head node``// as this can modify the head of the input linked list``Node* sortedInsert(Node* head_ref, Node* new_node)``{` `Node* current = head_ref;` `// If the list is empty` `if` `(current == NULL) {` `new_node->next = new_node;` `head_ref = new_node;` `}` `// If the node to be inserted is the smallest` `// then it has to be the new head` `else` `if` `(current->data >= new_node->data) {` `// Find the last node of the list as it` `// will be pointing to the head` `while` `(current->next != head_ref)` `current = current->next;` `current->next = new_node;` `new_node->next = head_ref;` `head_ref = new_node;` `}` `else` `{` `// Locate the node before the point of insertion` `while` `(current->next != head_ref` `&& current->next->data < new_node->data) {` `current = current->next;` `}` `new_node->next = current->next;` `current->next = new_node;` `}` TG142] `return` `head_ref;``}``// Function to print the nodes of the linked list``void` `printList(Node* start)``{` `Node* temp;` `if` `(start != NULL) {`] `temp = start;` `do` `{` `cout << temp->data <<` `" "` `;` `temp = temp->next;` `}` `while` `(temp != start);` `}``}``// Driver code``int` `main()``{` `int` ] `int` `list_size, i;` `// Start with an empty linked list` [HTG4 40] `Node* start = NULL;` `Node* temp;` `// Create linked list from the given array` `for` `(i = 0; i < 6; i++) {` `// Move to a random node if it exists` `if` `(start != NULL)`]  `for` `(` `int` `j = 0; j < (` `rand` `() % 10); j++)` `start = start->next;` `temp = create();` `temp->data = arr[i];` `start = sortedInsert(find_head(start), temp);` `}` `// Print the contents of the created list` `printList(find_head(start));` `return` `0;``}` |

*chevron_right**filter_none*