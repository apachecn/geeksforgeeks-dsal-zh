# 双链表中所有节点的乘积，该整数可被给定数K整除

给定一个包含N个节点的双链表，并给定数字K。任务是找到所有可被K整除的节点的乘积。

**范例**：

```
Input : List = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
        K = 3
Output : Product = 810

Input : List = 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
        K = 2
Output : Product = 384

```

这个想法是遍历双向链表并一一检查节点。 如果某个节点的值可被K整除，则将该节点的值乘以到目前为止的乘积，并在未到达列表末尾的情况下继续此过程。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find product of nodes in a``// doubly linked list divisible by K``#include <iostream>``using` `namespace` `std;``// Doubly linked list node``struct` `Node {` `int` `data;` `Node *prev, *next;``};``// function to insert a node at the beginning``// of the Doubly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// allocate node` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// put in the data` `new_node->data = new_data;` `// since we are adding at the beginning,` `// prev is always NULL` `new_node->prev = NULL;` `// link the old list off the new node` `new_node->next = (*head_ref);` `// change prev of head node to new node` `if` ] `((*head_ref) != NULL)` `(*head_ref)->prev = new_node;` HTG228]`}``// Function to find the product of all the nodes from``// the doubly linked list that is divisible by K``int` `productOfNode(Node** head_ref,` `int` `K)``{` `Node* ptr = *head_ref;` `Node* next;` `int` `product = 1;` `// Travese list till last node` `while` `(ptr != NULL) {` `next = ptr->next;` `// check is node value divided by K` `// if true then add in sum` `if` `(ptr->data % K == 0)` `product *= ptr->data;` `ptr = next;` `}`​​ `// Return product of nodes which` `// are divisible by K` `return` `product;``}``// Driver Code``int` `main()``{` `// start with the empty list` `Node* head = NULL;` `// create the doubly linked list` `// 15 16 10 9 6 7 17` `push(&head, 17);` `push(&head, 7);` `push(&head, 6);` `push(&head, 9);` `push(&head, 10);` `push(&head, 16);` `push(&head, 15);` `int` `K = 3;` `return` `0;``}` |

*chevron_right**filter_none*