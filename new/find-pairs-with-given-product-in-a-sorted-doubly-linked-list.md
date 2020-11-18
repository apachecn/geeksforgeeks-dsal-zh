# 在排序的双链表

中查找与给定产品的对

给定**个正相异元素**的排序的双链表，任务是在双链表中查找乘积等于给定值x的对，而不使用任何额外空间。

**范例**：

```
Input : List = 1 <=> 2 <=> 4 <=> 5 <=> 6 <=> 8 <=> 9
        x = 8
Output: (1, 8), (2, 4)

Input : List = 1 <=> 2 <=> 3 <=> 4 <=> 5 <=> 6 <=> 7
        x = 6
Output: (1, 6), (2, 3)

```

解决此问题的一种简单方法**是使用两个嵌套循环遍历链表，并找到所有对，并检查乘积等于x的对。 这个问题的时间复杂度将是O（n ^ 2），n是双向链表中节点的总数。**

针对此问题的**有效解决方案**与该文章的[相同。 这是算法：](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)

*   初始化两个指针变量以在排序的双链表中找到候选元素。 首先以双向链表的开头初始化；即 **first = head** ，然后用双向链表的最后一个节点初始化**，然后初始化**；即， **second = last_node** 。
*   我们将第一个和第二个指针初始化为第一个和最后一个节点。 这里我们没有随机访问权限，因此要找到第二个指针，我们遍历列表以初始化第二个指针。
*   如果当前的第一乘积和第二乘积小于x，则我们首先向前移动。 如果第一元素和第二元素的当前乘积大于x，则我们向后移动第二个元素。
*   循环终止条件也与阵列不同。 当两个指针中的任何一个变为NULL或它们彼此交叉（第二个->下一个=第一个），或者它们变为相同（第一个==第二个）时，循环终止

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find a pair with``// given product x in sorted Doubly``// Linked List``#include <bits/stdc++.h>``using` `namespace` `std;``// Doubly Linked List Node``struct` `Node {` `int` `data;` `struct` `Node *next, *prev;``};``// Function to find pair whose product``// equal to given value x``void` `pairProduct(` `struct` `Node* head,` `int` `x)``{` `// Set two pointers,` `// first to the beginning of DLL` `// and second to the end of DLL.` `struct` `Node* first = head;` `struct` `Node* second = head;` `while` `(second->next != NULL)` `second = second->next;` `// To track if we find a pair or not` `bool` `found =` `false` `;` `// The loop terminates when either of two pointers` `// become NULL, or they cross each other (second->next` ] `// == first), or they become same (first == second)` `while` `(first != NULL && second != NULL && first != second` `&& second->next != first) {` `// pair found` `if` `((first->data * second->data) == x) {` `found =` `true` `;` `cout <<` `"("` `<< first->data <<` `", "` `<< second->data <<` `")"` `<< endl;`​​ `// move first in forward direction` `first = first->next;` `// move second in backward direction` `second = second->prev;` `}` `else` `{` `if` `((first->data * second->data) < x)` `first = first->next;` `else` `second = second->prev;` `}` `}` [ `// if pair is not present` `if` `(found ==` `false` `)` `cout <<` `"No pair found"` `;``}``// A utility function to insert a new node at the``// beginning of doubly linked list``void` `insert(` `struct` `Node** head,` `int` `data)``{` `struct` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = temp->prev = NULL;` `if` `(!(*head))` `(*head) = temp;` `else` `{` `temp->next = *head;` `(*head)->prev = temp;` `(*head) = temp;` [HTG1 58]`}``// Driver Code``int` `main()``{` `// Create Doubly Linked List` `struct` `Node* head = NULL;` `insert(&head, 9);` `insert(&head, 8);` `insert(&head, 6);` `insert(&head, 5);` `insert(&head, 4);` `insert(&head, 2);` `insert(&head, 1);` `int` `x = 8;` `pairProduct(head, x);` `return` `0;``}` |

*chevron_right**filter_none*