# 通过在每个位置选择最大元素，从两个链表创建一个链表

给定两个大小相等的链表，任务是使用这些链表创建新的链表，其中在每个步骤中，选择两个链表中两个元素的最大值，然后跳过另一个元素。

**示例：**

> **输入：**
> list1 = 5-> 2-> 3-> 8-> NULL
> list2 = 1-> 7-> 4 -> 5->空
> **输出：** 5-> 7-> 4-> 8->空
> 
> **输入：**
> list1 = 2-> 8-> 9-> 3-> NULL
> list2 = 5-> 3-> 6 -> 4->空
> **输出：** 5-> 8-> 9-> 4->空

**方法：**我们同时遍历两个链表，并比较两个链表中的节点。 其中更大的节点将被添加到新的链表中。 我们对每个节点执行此操作，然后打印生成的链接列表的节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;``// Representation of node``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert node in a linked list``void` `insert(Node** root,` `int` `item)``{` `Node *ptr, *temp;` `temp =` `new` `Node;` `temp->data = item;` `temp->next = NULL;` `if` `(*root == NULL)` `*root = temp;` `else` `{` `ptr = *root;` `while` `(ptr->next != NULL)` `ptr = ptr->next;`的 `ptr->next = temp;` `}``}``// Function to print the``// nodes of a linked list` ]`void` `display(Node* root)``{` `while` `(root != NULL) {` `cout << root->data <<` `" -> "` `;`​​  `root = root->next;` `}` `cout <<` `"NULL"` `;``}``// Function to generate the required``// linked list and return its head``Node* newList(Node* root1, Node* root2)``{` ] `Node *ptr1 = root1, *ptr2 = root2;` `Node* root = NULL;` `// While there are nodes left` `while` `(ptr1 != NULL) {` `// Maximum node at current position` `int` `currMax = ((ptr1->data < ptr2->data)`[H TG97] `? ptr2->data` `: ptr1->data);` `// If current node is the first node` `// of the newly linked list being` `// generated then assign it to the root` `if` `(root == NULL) {` `Node* temp =` `new` `Node;` `temp->data = currMax;` `temp->next = NULL;` `root = temp;` `}`[ `// Else insert the newly` `// created node in the end` `else` `{` `insert(&root, currMax);` `}` `// Get to the next nodes` `ptr1 = ptr1->next;` `ptr2 = ptr2->next;` `}` `// Return the head of the` `// generated linked list` `return` `root;``}``// Driver code``int` `main()``{` `Node *root1 = NULL, *root2 = NULL, *root = NULL;`的 `// First linked list` `insert(&root1, 5);` `insert(&root1, 2);` `insert(&root1, 3);` `insert(&root1, 8);` `// Second linked list` `insert(&root2, 1);` `insert(&root2, 7);` `insert(&root2, 4);` `insert(&root2, 5);` `// Generate the new linked list` `// and get its head` `root = newList(root1, root2);` `// Display the nodes of the generated list` `display(root);` `return` `0;``}` |

*chevron_right**filter_none*