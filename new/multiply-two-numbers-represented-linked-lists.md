# 将两个数字乘以链接列表

给定两个由链表表示的数字，编写一个函数返回两个链表的乘积。

**示例：**

```
Input : 9->4->6
        8->4
Output : 79464

Input : 3->2->1
        1->2
Output : 3852

```

**解决方案**：
遍历两个列表并生成要相乘的所需数字，然后返回两个数字的相乘值。
从链表表示中生成数字的算法：

```
1) Initialize a variable to zero
2) Start traversing the linked list
3) Add the value of first node to this variable
4) From the second node, multiply the variable by 10
   first and then add the value of the node to this 
   variable.
5) Repeat step 4 until we reach the last node of the list. 

```

将上述算法与两个链表一起使用以生成数字。
下面是将两个数字相乘的程序，它们表示为链表：

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C program to Multiply two numbers``// represented as linked lists``#include<stdio.h>``#include<stdlib.h>`的`// Linked list node``struct` `node``{` `int` `data;` `struct` `node* next;``};``// Function to create a new node ``// with given data``struct` `node *newNode(` `int` `data)``{` `struct` `node *new_node = (` `struct` `node *)` `malloc` `(` `sizeof` `(` `struct` `node));` `new_node->data = data;` `new_node->next = NULL;` `return` `new_node;``}``// Function to insert a node at the ``// beginning of the Linked List``void` `push(` `struct` `node** head_ref,` `int` `new_data)` [H TG268]`{`​​ `// allocate node ` `struct` `node* new_node = newNode(new_data);` `// link the old list off the new node ` `new_node->next = (*head_ref);` `// move the head to point to the new node ` `(*head_ref) = new_node;` ]`}``// Multiply contents of two linked lists``long` `multiplyTwoLists (` `struct` `node* first,` `struct` `node* second)``{` `int` `num1 = 0, num2 = 0;` `// Generate numbers from linked lists` `while` `(first &#124;&#124; second)` `{` `if` `(first)` `{` `num1 = num1*10 + first->data;` `first = first->next;` `}` `if` [ `(second)` [HT G318] `{` `num2 = num2*10 + second->data;` `second = second->next;` `}` `}` `// Return multiplication of ` `// two numbers` `return` `num1*num2;``}` [`// A utility function to print a linked list``void` `printList(` `struct` `node *node)``{` `while` `(node != NULL)` `{` `printf` `(` `"%d"` `, node->data);` `if` `(node->next)` `printf` `(` `"->"` `);` `node = node->next;` `}` `printf` `(` `"\n"` `);` [HTG36 2]`}``// Driver program to test above function``int` `main(` `void` `)``{` `struct` `node* first = NULL;` `struct` `node* second = NULL;` `// create first list 9->4->6` `push(&first, 6);` `push(&first, 4);` `push(&first, 9);` `printf` `(` `"First List is: "` `);` `printList(first);` `// create second list 8->4` `push(&second, 4);` `push(&second, 8);` `printf` `(` `"Second List is: "` `);` `printList(second);` `// Multiply the two lists and see result` `printf` `(` `"Result is: "` [HTG20 7] `printf` `(` `"%ld"` `, multiplyTwoLists(first, second));` `return` `0;``}` |

*chevron_right**filter_none*