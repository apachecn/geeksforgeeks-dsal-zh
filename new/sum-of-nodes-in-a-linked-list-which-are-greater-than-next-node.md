# 链表中大于下一节点

的节点总数

给定一个链表，任务是找到所有大于其旁边节点的节点之和。 **请注意**，对于链表的最后一个节点，该节点的旁边没有任何节点，它必须大于第一个节点，以使它有助于总和。

**示例：**

> **输入：** 9-> 2-> 3-> 5-> 4-> 6-> 8
> **输出：** 14
> 9 + 5 = 14
> 
> **输入：** 2-> 1-> 5-> 7
> **输出：** 9
> 2 + 7 = 9

**方法：**遍历整个链表，对于每个节点，如果该节点大于下一个节点，则将其添加到总和中。 对于最后一个节点，将其与链接列表的开头进行比较，如果最后一个节点大于开头，则将其添加到总和中。 最后打印总和。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;``// Represents node of the linked list``struct` `Node {` `int` `data;` `Node* next;``};`，`// Function to insert a node at the``// end of the linked list``void` `insert(Node** root,` `int` `item)``{` `Node *ptr = *root, *temp =` `new` `Node;` `temp->data = item;` `temp->next = NULL;` [ `if` `(*root == NULL)` `*root = temp;` `else` `{` `while` `(ptr->next != NULL)` `ptr = ptr->next;` `ptr->next = temp;` `}``}``// Function to return the sum of the nodes``// which are greater than the node next to them``int` `sum(Node* root)``{` `// If there are no nodes` `if` `(root == NULL)` `return` `0;` `int` `sm = 0;` `Node* ptr = root;` `while` `(ptr->next != NULL) {` `// If the node is greater than the next node` `if` `(ptr->data > ptr->next->data)` `sm += ptr->data;` `ptr = ptr->next;` `}` `// For the last node` ] `if` `(ptr->data > root->data)` `sm += ptr->data;` `// Return the sum` `return` `sm;``}``// Driver code``int` `main()``{` `Node* root = NULL;` `insert(&root, 9);` `insert(&root, 2);` `insert(&root, 3);` `insert(&root, 5);` `insert(&root, 4);` `insert(&root, 6);` `insert(&root, 8);` `cout << sum(root) << endl;` `return` `0;``}`​​ |

*chevron_right**filter_none*