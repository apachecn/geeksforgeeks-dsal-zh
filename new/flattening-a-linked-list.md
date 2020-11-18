# 展平链接列表

给定一个链表，其中每个节点代表一个链表，并包含两个其类型的指针：
（i）指向主列表中下一个节点的指针（在下面的代码中我们称之为“正确”指针）
（ii）指向此节点为头的链接列表的指针（在下面的代码中我们称之为“向下”指针）。
所有链接列表已排序。 请参阅以下示例

```
       5 -> 10 -> 19 -> 28
       |    |     |     |
       V    V     V     V
       7    20    22    35
       |          |     |
       V          V     V
       8          50    40
       |                |
       V                V
       30               45

```

编写一个函数flatten（）以将列表展平为单个链接列表。 展平的链表也应排序。 例如，对于上面的输入列表，输出列表应为5-> 7-> 8-> 10-> 19-> 20-> 22-> 28-> 30-> 35-> 40-> 45-> 50 。

这个想法是对链接列表使用[合并排序的Merge（）过程。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/) 我们使用merge（）逐一合并列表。 我们以递归方式将当前列表与已经变平的列表合并（）。
下指针用于链接扁平化列表的节点。

以下是C和Java实现。

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C program for flattening a linked list``#include <stdio.h>``#include <stdlib.h>``// A Linked List Node``typedef` `struct` `Node``{` `int` `data;` `struct` `Node *right;` `struct` `Node *down;``} Node;``/* A utility function to insert a new node at the beginning` `of linked list */``void` `push (Node** head_ref,` `int` `new_data)``{` `/* allocate node */` ] `Node* new_node = (Node *)` `malloc` `(` `sizeof` `(Node));` `new_node->right = NULL;` [ `/* put in the data  */` `new_node->data  = new_data;`​​  `/* link the old list off the new node */` `new_node->down = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref)    = new_node;``}``/* Function to print nodes in the flattened linked list */`]`void` `printList(Node *node)``{` `while` `(node != NULL)` `{` `printf` `(` `"%d "` `, node->data);` `node = node->down;` `}``}``// A utility function to merge two sorted linked lists``Node* merge( Node* a, Node* b )``{` `// If first list is empty, the second list is result` `if` `(a == NULL)` `return` `b;` [ `// If second list is empty, the second list is result` `if` `(b == NULL)` `return` `a;` `// Compare the data members of head nodes of both lists`[HT G330]  `// and put the smaller one in result` `Node* result;` `if` `(a->data < b->data)` `{` `result = a;` `result->down = merge( a->down, b );` `}` `else` `{` `result = b;` `result->down = merge( a, b->down );` `}`[ `result->right = NULL;` `return` `result;``}``// The main function that flattens a given linked list``Node* flatten (Node* root)``{` `// Base cases` `if` `(root == NULL &#124;&#124; root->right == NULL)` `return` `root;` `// Merge this list with the list on right side`[HT G380]  `return` `merge( root, flatten(root->right) );``}``// Driver program to test above functions``int` `main()``{` `Node* root = NULL;` `/* Let us create the following linked list` ] `5 -> 10 -> 19 -> 28` `&#124;    &#124;     &#124;     &#124;` `V    V     V     V` `7    20    22    35` `&#124;          &#124;     &#124;` `V          V     V` `8          50    40` `&#124;                &#124;` `V                V` `30               45` `*/` `push( &root, 30 );` `push( &root, 8 );` `push( &root, 7 );` `push( &root, 5 );` [HT G191] `push( &( root->right ), 10 );` `push( &( root->right->right ), 50 );` `push( &( root->right->right ), 22 );` `push( &( root->right->right ), 19 );` `push( &( root->right->right->right ), 45 );` `push( &( root->right->right->right ), 40 );` ] `push( &( root->right->right->right ), 35 );` `push( &( root->right->right->right ), 20 );` `// Let us flatten the list` `root = flatten(root);` `// Let us print the flatened linked list` `printList(root);` `return` `0;``}` |

*chevron_right**filter_none*