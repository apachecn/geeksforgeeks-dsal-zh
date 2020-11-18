# 在链接列表

中查找峰元素

给定一个整数链接列表。 任务是在其中找到一个峰值元素。 如果列表中的一个元素不小于其相邻元素，则称该元素为**峰**。 对于拐角元素，我们只需要考虑一个邻居。 例如：

*   如果输入列表为{5-> 10-> 20-> 15}，则20是唯一的峰元素。
*   对于输入列表{10-> 20-> 15-> 2-> 23-> 90-> 67}，有两个峰元素：20和90。请注意，需要返回任何一个峰元素。

以下一些极端情况可以更好地解决这个问题：

1.  如果输入列表严格按升序排序，则最后一个元素始终是峰值元素。 例如，50是{10-> 20-> 30-> 40-> 50}中的峰值元素。
2.  如果输入列表按严格降序排序，则第一个元素始终是峰值元素。 100是{100-> 80-> 60-> 50-> 20}中的峰值元素。
3.  如果输入列表的所有元素都相同，则每个元素都是峰值元素。

**范例**：

```
Input : List =  {1 -> 6 -> 8 -> 4 -> 12}
Output : 8

Input : List = {10 -> 20 -> 15 -> 2 -> 23 -> 90 -> 67}
Output : 90

```

想法是遍历链表，并检查当前元素是否为峰元素。 如果是，则返回当前元素，否则在列表中向前移动。

如果当前元素大于其上一个和下一个元素，则它将是一个峰值元素。

下面的程序说明了上述方法：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation to find the peak``// element in the Linked List``#include <bits/stdc++.h>``using` `namespace` `std;` [`/* A Linked list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// function to insert a node at the``// beginning of the linked list``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to find the peak element``int` `findPeak(` `struct` `Node* head)``{` `// Return -1 to indicate that` `// peak does not exist` `if` `(head == NULL)` `return` `-1;` `// If there is only one node` `if` `(head->next == NULL)` `return` `head->data;` `// Traverse till last node (starting from` `// second node)` `int` `prev = head->data;` `Node *curr;` `for` `(curr = head->next; curr->next != NULL;` `curr = curr->next) {` `// check if current node is greater` `// than both neighbours` `if` `(curr->data > curr->next->data` `&& curr->data > prev)` `return` `curr->data;`[ `prev = curr->data;` `}` `// We reach here when curr is last node` `if` `(curr->data > prev)` `return` `curr->data;` `// Peak does not exists` `else` `return` `-1;``}``// Driver program``int` `main()``{`​​ `struct` `Node* head = NULL;` `// create linked list 1->6->8->4->12` `push(&head, 12);` `push(&head, 4);` `push(&head, 8);` `push(&head, 6);` `push(&head, 1);` `cout <<` `"Peak element is: "` `<< findPeak(head);` `return` `0;``}`[HTG2 99] |

*chevron_right**filter_none*