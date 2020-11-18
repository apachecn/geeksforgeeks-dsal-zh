# 可被K整除的单个链接列表的节点的总和和

给定一个单链表。 任务是找到给定链表的所有节点的和和乘积，这些节点可被给定数k整除。

**范例**：

```
Input : List = 7->60->8->40->1
        k = 10 
Output : Product = 2400, Sum = 100
Product of nodes: 60 * 40 = 2400

Input : List = 15->7->3->9->11->5
        k = 5
Output : Product = 75, Sum = 20

```

**算法：**

1.  用链接列表的开头初始化指针 **ptr** ，将**乘积**变量初始化为1，将**和**变量初始化为0。
2.  使用循环开始遍历链表，直到遍历所有节点。
3.  对于每个节点：
    *   如果当前节点可被k整除，则将当前节点的值乘以乘积。
    *   如果当前节点可被k整除，则将当前节点的值加到总和上。
4.  增加指向链接列表下一个节点的指针，即ptr = ptr-> next。
5.  重复上述步骤，直到到达链表的末尾。
6.  最后，打印乘积和总和。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find the product``// and sum of nodes which are divisible by k``#include <iostream>``using` `namespace` `std;``// A Linked list node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `/* allocate node */` `struct` `Node* new_node =` `new` `Node;` `/* put in the data */` `new_node->data = new_data;` `/* link the old list to the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */`[HTG1 98]  `(*head_ref) = new_node;``}``// Function to find the product and sum of``// nodes which are divisible by k``// of the given linked list``void` `productAndSum(` `struct` `Node* head,` `int` `k)``{` `// Pointer to traverse the list` `struct` `Node* ptr = head;` `int` `product = 1;` `// Variable to store product` `int` `sum = 0;` `// Variable to store sum` `// Traverse the list and` `// calculate the product` `// and sum` `while` `(ptr != NULL) {` `if` `(ptr->data % k == 0) {` `product *= ptr->data;` `sum += ptr->data;` `}` `ptr = ptr->next;` `}` `// Print the product and sum` `cout <<` `"Product = "` `<< product << endl;` `cout <<` `"Sum = "` `<< sum;``}``// Driver Code``int` `main()``{` `struct` `Node* head = NULL;`​​  `// create linked list 70->6->8->4->10` `push(&head, 70);` `push(&head, 6);` `push(&head, 8);` `push(&head, 4);` `push(&head, 10);` `int` `k = 10;` `productAndSum(head, k);`[ `return` `0;``}` |

*chevron_right**filter_none*