# 从三个链表中查找一个三元组，总和等于给定数字

给定三个链接列表（例如，a，b和c），从每个列表中找到一个节点，以使节点的值之和等于给定数目。
例如，如果三个链接列表是12- > 6- > 29、23- > 5- > 8和90- > 20- > 59 ，给定数字为101，输出应为三元组“ 6 5 90”。

在以下解决方案中，为简化分析，假设所有三个链表的大小相同。 以下解决方案也适用于不同大小的链表。

解决此问题的一种简单方法是运行三个嵌套循环。 最外面的循环从列表a中选择一个元素，中间的循环从b中选择一个元素，最里面的循环从c中选择。 最里面的循环还检查a，b和c当前节点的值之和是否等于给定数。 该方法的时间复杂度为O（n ^ 3）。

可以使用排序将时间复杂度降低到O（n * n）。 以下是详细步骤。
1）以升序对列表b进行排序，以降序对列表c进行排序。
2）对b和c进行排序后，一个接一个地从列表a中选择一个元素，并同时遍历b和c来找到该对。 请参见以下代码中的isSumSorted（）。 这个想法类似于 [3和问题](http://en.wikipedia.org/wiki/3SUM)的二次算法。

以下代码仅实现步骤2。 通过在此处中讨论的合并排序代码，可以轻松地为未排序列表修改解决方案。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to find a triplet ``// from three linked lists with ``// sum equal to a given number ``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `Node ``{ ` `public` `:` `int` `data; ` `Node* next; ``}; ``/* A utility function to insert ``a node at the beginning of a ``linked list*/``void` `push (Node** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); ` [ `/* move the head to point to the new node */`​​ `(*head_ref) = new_node; ``} ``/* A function to check if there are three elements in a, b ``and c whose sum is equal to givenNumber. The function ``assumes that the list b is sorted in ascending order ``and c is sorted in descending order. */``bool` `isSumSorted(Node *headA, Node *headB, ` `Node *headC,` `int` `givenNumber) ``{ ` `Node *a = headA; ` ] `// Traverse through all nodes of a ` `while` `(a != NULL) ` `{ ` `Node *b = headB; ` `Node *c = headC; ` `// For every node of list a, prick two nodes ` `// from lists b abd c ` `while` `(b != NULL && c != NULL) ` `{ ` `// If this a triplet with given sum, print ` `// it and return true ` `int` `sum = a->data + b->data + c->data; ` `if` `(sum == givenNumber) ` `{ ` `cout <<` `"Triplet Found: "` `<< a->data <<` `" "` `<< ` `b->data <<` `" "` `<< c->data; ` `return` `true` `; ` `} ` `// If sum of this triplet is smaller, look for ` `// greater values in b ` `else` `if` `(sum < givenNumber) ` `b = b->next; ` `else` `// If sum is greater, look for smaller values in c ` `c = c->next; ` `} ` `a = a->next;` `// Move ahead in list a ` `} ` `cout <<` `"No such triplet"` `; ` `return` `false` `; ``} ` [HT G362] [`/* Driver code*/``int` `main() ``{ ` `/* Start with the empty list */` `Node* headA = NULL; ` `Node* headB = NULL; ` `Node* headC = NULL; ` `/*create a linked list 'a' 10->15->5->20 */` `push (&headA, 20); ` `push (&headA, 4); ` `push (&headA, 15); ` `push (&headA, 10); ` `/*create a sorted linked list 'b' 2->4->9->10 */` `push (&headB, 10); ` `push (&headB, 9); ` `push (&headB, 4); ` `push (&headB, 2); ` `/*create another sorted `]  `linked list 'c' 8->4->2->1 */` `push (&headC, 1); ` `push (&headC, 2); ` [H TG195] `push (&headC, 8); ` `int` `givenNumber = 25; ` `isSumSorted (headA, headB, headC, givenNumber); ` `return` `0; ``} ` ] [`// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*