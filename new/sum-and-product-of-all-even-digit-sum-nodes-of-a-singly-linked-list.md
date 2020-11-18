# 单链接列表

的所有偶数和节点的和与乘积

给定一个包含 **N个**节点的[单链列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从列表中找到其数据值具有偶数数字和的所有节点的和与乘积。

**示例：**

> **输入：** 15-> 16-> 8-> 6-> 13
> **输出：**
> 总和= 42
> 产品 = 9360
> **说明：**
> 链表中数字的所有位数的总和为：
> 15 = 1 + 5 = 6
> 16 = 1 + 6 = 7
> 8 = 8
> 6 = 6
> 13 = 1 + 3 = 4
> 该列表包含4个偶数和数据值15、8、6和13。
> 和= 15 + 8 + 6 + 13 = 42
> 乘积= 15 * 8 * 6 * 13 = 9360
> 
> **输入：** 5-> 3-> 4-> 2-> 9
> **输出：**
> 总和= 6
> 产品 = 8
> **说明：**
> 该列表包含2个偶数总和数据值4和2。
> 总和= 4 + 2 = 6
> 乘积= 4 * 2 = 8

**方法：**的想法是遍历给定的链表，并检查当前节点值的所有数字的[总和是否为偶数。 如果是，则将当前节点值包括到结果总和中，并将结果乘积Else检查下一个节点值。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program for the above approach``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Node of Linked List``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert a node at the``// beginning of the singly Linked List``void` `push(Node** head_ref,` `int` `new_data)``{` `// Allocate new node` `Node* new_node` `= (Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `// Insert the data` `new_node->data = new_data;` `// Link old list to the new node` `new_node->next = (*head_ref);` `// Move head to point the new node` `(*head_ref) = new_node;``}``// Function to find the digit sum``// for a number``int` `digitSum(` `int` `num)``{` `int` `sum = 0;` `while` `(num) {` `sum += (num % 10);` `num /= 10;` `}` `// Return the sum` `return` `sum;``}`的`// Function to find the required``// sum and product``void` `sumAndProduct(Node* head_ref)`​​`{`的 `// Initialise the sum and product` `// to 0 and 1 respectively` `int` `prod = 1;` `int` `sum = 0;` `Node* ptr = head_ref;` `// Traverse the given linked list` `while` `(ptr != NULL) {` `// If current node has even` `// digit sum then include it in` `// resultant sum and product` `if` `(!(digitSum(ptr->data) & 1)) {` `// Find the sum and the product` `prod *= ptr->data;` `sum += ptr->data;` `}` `ptr = ptr->next;` `}` [ `// Print the final Sum and Product` `cout <<` `"Sum = "` `<< sum << endl;` `cout <<` `"Product = "` `<< prod;``}`[HTG14 3]`int` `main()``{` `// Head of the linked list` `Node* head = NULL;` `// Create the linked list` `// 15 -> 16 -> 8 -> 6 -> 13` `push(&head, 13);` `push(&head, 6);` `push(&head, 8);` `push(&head, 16);` `push(&head, 15);`的 `// Function call` `sumAndProduct(head);` `return` `0;``}` |

*chevron_right**filter_none*