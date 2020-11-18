# 链表

中所有奇数频率节点的总和

给定一个链表，任务是从给定的链表中找到所有奇数频率节点的总和。

**示例：**

> **输入：** 8-> 8-> 1-> 4-> 1-> 2-> 8->空
> **输出：** 30
> freq（8）= 3
> freq（1）= 2
> freq（4）= 1
> freq（2）= 1
> 8、4和2 出现奇数次（8 * 3）+（4 * 1）+（2 * 1）= 30
> 
> **输入：** 6-> 2-> 2-> 6-> 2-> 1->空
> **输出：** 7

**方法：**此问题可以通过[散列](http://www.geeksforgeeks.org/hashing-data-structure/)解决，

1.  创建一个散列来存储节点的频率。
2.  遍历[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)并更新哈希变量中节点的频率。
3.  现在，再次遍历链表，对出现奇数次的每个节点，将其值加到运行总和中。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of above approach``#include<bits/stdc++.h>``using` `namespace` `std;``// Node class``struct` `Node``{` `int` `data;` `Node* next;` `Node(` `int` `d)` `{` `data = d;` `next = NULL;` `} ``} ;``// Function to push the new node ``// to head of the linked list``Node* push(Node* head,` `int` `data)``{` `// If head is null return new node as head` `if` `(!head)` `return` `new` `Node(data);` `Node* temp =` `new` `Node(data);` `temp->next = head;`[H TG50] `head = temp;` `return` `head;``}``// Function to find the sum of all odd ``// frequency nodes of the linked list``int` `sumOfOddFreqEle(Node* head)``{` `// Hash to store the frequencies of ` `// the nodes of the linked list` ] `map<` `int` `,` `int` `> mp ;` `Node* temp = head;` `while` `(temp)` `{` `int` `d = temp->data;` `mp[d]++;` `temp = temp->next;` `}` `// Initialize total_sum as zero ` `int` `total_sum = 0;` `// Traverse through the map to get the sum` `for` `(` `auto` `i : mp) `[  `{ ` `// If it appears for odd number of ` `// times then add it to the sum` `if` `(i.second % 2 == 1)` `total_sum+=(i.second * i.first);` `}` `return` `total_sum;``}`[​​ `// Driver code``int` `main()``{` `Node* head = NULL;` `head = push(head, 8);` `head = push(head, 2);` `head = push(head, 1);` `head = push(head, 4);`]  `head = push(head, 1);` `head = push(head, 8);` `head = push(head, 8);` `cout<<(sumOfOddFreqEle(head));` [ `return` `0;``}`[HTG3 02]  [`// This code is contributed by Arnab Kundu` |

*chevron_right**filter_none*