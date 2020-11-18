# 须藤放置[1.4] | K和

给定整数和整数k的链表的开头，您的任务是按如下方式修改链表：

*   考虑大小为k的组中的节点。 在每个组中，将第一个节点的值替换为组和。
*   另外，删除组中除第一个节点以外的元素。
*   在遍历期间，如果链表中的其余节点小于k，则也要考虑剩余节点，执行上述操作。

**示例：**

> **输入：** N = 6，K = 2
> 1- > 2- > 3- > 4- > 5- > 6
> **输出：** 3 7 11
> 
> 我们用（）表示对k个元素的分组。 （）中的元素相加。
> 1-> 2-> 3-> 4-> 5-> 6->空
> （1-> 2）-> 3 -> 4-> 5-> 6->空
> （3）-> 3-> 4-> 5-> 6-> null
> 3->（3-> 4）-> 5-> 6-> null
> 3->（7）-> 5-> 6-> null
> 3-> 7->（5-> 6）-> null
> 3-> 7->（11） -> null
> 3-> 7-> 11-> null

**方法：**将给定的节点插入“链接”列表中。 插入方法已在的[中进行了讨论。 插入节点后，从列表的开头进行迭代。 将第一个节点标记为**临时**节点。 迭代接下来的k-1个节点，并在 **sum** 变量中求和。 如果节点数少于K，则将临时节点的数据替换为sum，并将temp指向NULL。 如果存在一个由K个节点组成的组，则用sum替换临时数据，并将temp移到K个节点之后的节点。 继续上述操作，直到temp指向NULL。 一旦temp到达末尾，则意味着遍历了所有大小为K的组，并且已用大小为K的节点总和替换了该节点。一旦完成了替换操作，就可以打印由此形成的链表。 在此](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的[中已讨论了打印链接列表的方法。](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program for``// SP - K Sum``#include <iostream>``using` `namespace` `std;``// structure for linked list``struct` `Node {` `long` `long` `data;` `Node* next;``};``// allocated new node``Node* newNode(` `int` `key)``{` `Node* temp =` `new` `Node;` `temp->data = key;` `temp->next = NULL;` `return` `temp;``}` [`// function to insert node in a Linked List``Node* insertNode(Node* head,` `int` `key)``{` `if` `(head == NULL)` `head = newNode(key);` `else` `head->next = insertNode(head->next, key);` `return` `head;``}``// traverse the node``// to print it``void` `print(Node* head)``{` `// travere the linked list`​​ `while` `(head) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}` `cout << endl;``}``// function to perform the following operation``void` `KSum(Node* head,` `int` `k)``{` `// initially pointing to start` `Node* temp = head;` `// iterate till end` `while` `(temp) {` ] `// dummy variable to store k` `long` `long` `count = k;` `// summation of nodes` `long` `long` `sum = 0;` `// currently at node from` `// which itearation is done` `Node* curr = temp;` `// till k nodes are visited and` `// last node is not visited` `while` `(count-- && curr) {` `// add to sum the node data` `sum = sum + curr->data;` `// move to the next node` `curr = curr->next;` `}` [ `// change pointer's data of temp to sum` `temp->data = sum;` `// move temp to next pointer`[HTG14 3] `temp->next = curr;` [ `// move temp to the next pointer` `temp = temp->next;` `}``}``// Driver Code``int` `main()``{` `Node* head = NULL;` `// inserts nodes in the linked list` `head = insertNode(head, 1);` `head = insertNode(head, 2);` `head = insertNode(head, 3);` `head = insertNode(head, 4);` `head = insertNode(head, 5);` `head = insertNode(head, 6);` `int` `k = 2;` `// Function call to perform the` `// given operations` `KSum(head, k);` [H TG188] `print(head);` `return` `0;``}` |

*chevron_right**filter_none*