# 将单链接列表转换为XOR链接列表

**前提条件**：

*   [XOR链表–内存有效的双链表| 设置1](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)
*   [XOR链表–内存有效的双链表| 设置2](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)

**XOR链接列表**是一种内存有效的双向链接列表，其中每个节点的下一个指针存储上一个和下一个节点的地址的XOR。

给定一个单链表，任务是将给定的单链表转换为XOR链表。

**方法**：由于在 **XOR** 链表中，每个下一个指针都存储**上一个**的 **XOR** 和下一个节点的**。 因此，想法是遍历给定的单链表，并在指针 *prev* 中跟踪先前的节点。**

现在，遍历列表时，将每个节点的下一个指针更改为：

```
current -> next = XOR(prev, current->next) 

```

**打印XOR链接列表**：
在打印XOR链接列表时，我们每次必须找到下一个节点的确切地址。 正如我们在上面看到的，每个节点的下一个指针存储prev与下一个节点的地址的XOR值。 因此，可以通过在XOR链接列表中找到prev的XOR和当前节点的next指针来获得下一个节点的地址。

因此，要打印XOR链接列表，请通过维护存储上一个节点地址的prev指针来遍历它，并找到下一个节点，计算prev与当前节点的下一个XOR。

下面是上述方法的实现：

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to Convert a Singly Linked``// List to XOR Linked List``#include <bits/stdc++.h>``using` `namespace` `std;``// Linked List node``struct` `Node {` `int` `data;` `struct` `Node* next;``};``// Utiltity function to create new node``Node* newNode(` `int` `data)``{` `Node* temp =` `new` `Node;` `temp->data = data;` `temp->next = NULL;` `return` `temp;``}``// Print singly linked list before conversion``void` `print(Node* head)``{` `while` `(head) {`[H TG249] 〔 `// print current node` `cout << head->data <<` `" "` `;` `head = head->next;` `}` `cout << endl;``}``// Function to find XORed value of``// the node addresses`​​`Node* XOR(Node* a, Node* b)``{` `return` `(Node*)((` `uintptr_t` `)(a) ^ (` `uintptr_t` `)(b));``}``// Function to convert singly linked``// list to XOR linked list``void` `convert(Node* head)``{` `Node* curr = head;` `Node* prev = NULL;` `Node* next = curr->next;` `while` `(curr) {` [ `// store curr->next in next` [[HT G303]  `next = curr->next;` `// cahnge curr->next to XOR of prev and next` `curr->next = XOR(prev, next);` `// prev wil change to curr for next iteration` `prev = curr;` `// curr is now pointing to next for next iteration` `curr = next;` `}``}` [`// Function to print XORed liked list``void` `printXOR(Node* head)``{` `Node* curr = head;` `Node* prev = NULL;` `while` `(curr) {` `// print current node` `cout << curr->data <<` `" "` ] `;` `Node* temp = curr;` `/* compute curr as prev^curr->next as` `it is previously set as prev^curr->next so` `this time curr would be prev^prev^curr->next ` `which is curr->next */` `curr = XOR(prev, curr->next);` `prev = temp;` `}` `cout << endl;``}``// Driver Code``int` `main()``{` `// Create following singly linked list` `// 1->2->3->4` `Node* head = newNode(1);` `head->next = newNode(2);` `head->next->next = newNode(3);` `head->next->next->next = newNode(4);` `cout <<` `"Before Conversion : "` ] `<< endl;` `print(head);` HTG407]  `cout <<` `"After Conversion : "` `<< endl;` `printXOR(head);` `return` `0;``}` |

*chevron_right**filter_none***Output:**

```
Before Conversion : 
1 2 3 4 
After Conversion : 
1 2 3 4

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。