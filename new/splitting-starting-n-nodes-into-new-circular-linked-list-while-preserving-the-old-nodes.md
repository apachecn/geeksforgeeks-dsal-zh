# 在保留旧节点的同时将起始N个节点拆分为新的循环链接列表

给定一个具有 **N** 个节点和整数 **K** 的循环链表，其中 **0 < K < N** ，任务是拆分第一个 **将**个节点K放入一个新列表中，同时将其余的节点保留在原始循环链接列表中。

**示例：**

> **输入：** 2-> 3-> 4-> 5-> 6-> 7-> 8，K = 3
> **输出 ：**
> 原始列表：
> 2 3 4 5 6 7 8
> 新列表是：
> 2 3 4
> 5 6 7 8
> 
> **输入：** 2-> 4-> 6-> 8- > 10-> 12，N = 4
> **输出：** [
> 原始列表：
> 2 4 6 8 10 12
> 新列表为：
> 2 4 6 8
> 10 12

**方法：**

*   遍历迭代器，直到所需的节点，即 **K <sup>第</sup>** 节点。
*   将 **K <sup>第</sup>** 节点之前的节点指向原始列表的开头。
*   将原始列表的最后一个节点指向 **K <sup>th</sup>** 节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include<bits/stdc++.h>``using` `namespace` `std;``class` `CircularLinkedList``{` `public` `:` `struct` `Node ` `{` `int` `data;` `Node* next;` `};` `Node* last;` `// Function to add a node to the empty list` `Node* addToEmpty(` `int` ] `data)` `{` `// If not empty` `if` `(last != NULL)` `return` `last;` `// Creating a node dynamically` `Node *temp =` `new` `Node();` [HT G395] `// Assigning the data` `temp->data = data;` `last = temp;` `// Creating the link` `last->next = last;` `return` `last;` ] `}` `// Function to add a node to the` `// beginning of the list` `Node* addBegin(` `int` `data)` `{` `// If list is empty` `if` `(last == NULL)` `return` `addToEmpty(data);` `// Create node` `Node *temp =` ] `new` `Node();` `// Assign data` `temp->data = data;` [ `temp->next = last->next;` [HTG4 45] `last->next = temp;` `return` `last;` `}` `// Function to traverse and print the list` `void` `traverse()` `{` `Node* p;` [ `// If list is empty` `if` `(last == NULL)` `{` `cout<<(` `"List is empty."` `);` `return` `;` `}` `// Pointing to the first Node of the list` `p = last->next;` `// Traversing the list` `do` `{` `cout << p->data <<` [HT G152] `;` `p = p->next;` `}` `while` `(p != last->next);` `cout << endl;` `}` `// Function to find the length of the CircularLinkedList` `int` `length()`]  `{` `// Stores the length` `int` `x = 0;` `// List is empty` `if` `(last == NULL)` `return` `x;` `// Iterator Node to traverse the List` `Node* itr = last->next;` `while` `(itr->next != last->next) ` `{` `x++;` `itr = itr->next;` `}` `// Return the length of the list` `return` `(x + 1);` `}` ] `// Function to split the first k nodes into` `// a new CircularLinkedList and the remaining` `// nodes stay in the original CircularLinkedList` `Node* split(` `int` `k)` `{` `// Empty Node for reference` `Node* pass =` `new` `Node();` `// Check if the list is empty` `// If yes, then return NULL` `if` `(last == NULL)` `return` `last;` `// NewLast will contain the last node of` `// the new split list` `// itr to iterate the node till` `// the required node` `Node* newLast, *itr = last;` `for` `(` `int` `i = 0; i < k; i++) ` `{` `itr = itr->next;` `}` `// Update NewLast to the required node and` `// link the last to the start of rest of the list` `newLast = itr;`​​ `pass->next = itr->next;` `newLast->next = last->next;` `last->next = pass->next;` `// Return the last node of the required list` `return` `newLast;` `}``};` `// Driver code``int` `main()``{` `CircularLinkedList* clist =` `new` `CircularLinkedList();` `clist->last = NULL;` `clist->addToEmpty(12);` `clist->addBegin(10);`[HTG6 34]  `clist->addBegin(8);` `clist->addBegin(6);` `clist->addBegin(4);` `clist->addBegin(2);` `cout<<(` `"Original list:"` `);` `clist->traverse();` `int` `k = 4;` `// Create a new list for the starting k nodes` `CircularLinkedList* clist2 =` `new` `CircularLinkedList();`HTG658]  `// Append the new last node into the new list` `clist2->last = clist->split(k);` `// Print the new lists` `cout<<(` `"The new lists are:"` `);` `clist2->traverse();` `clist->traverse();``}`的`// This code is contributed by Arnab Kundu` |

*chevron_right**filter_none*