# 链表中的第一个非重复

给定一个链表，找到它的第一个非重复整数元素。

例子：

```
Input : 10->20->30->10->20->40->30->NULL
Output :First Non-repeating element is 40.

Input :1->1->2->2->3->4->3->4->5->NULL
Output :First Non-repeating element is 5.

Input :1->1->2->2->3->4->3->4->NULL
Output :No NOn-repeating element is found.

```

1）创建一个哈希表，并将所有元素标记为零。

2）遍历链表并计算哈希表中所有元素的出现频率。

3）再次遍历链表，并在哈希表中查看频率为 1 的元素。

```
// C++ program to find first non-repeating
// element in a linked list
#include<bits/stdc++.h>
using namespace std;
[
/* Link list node */
struct Node
{
int data;
struct Node* next;
};
/* Function to find the first non-repeating
element in  the linked list */
int firstNonRepeating( struct Node *head)
{
// Create an empty map and insert all linked
// list elements into hash table
unordered_map< int , int > mp;
for (Node *temp=head; temp!=NULL; temp=temp->next)
mp[temp->data]++;
// Traverse the linked list again and return
// the first node whose count is 1
for (Node *temp=head; temp!=NULL; temp=temp->next)
[H TG50] if (mp[temp->data] == 1)
return temp->data;
return -1;
}
/* Function to push a node */
void push( struct Node** head_ref, int new_data)
{
struct Node* new_node =
( struct Node*) malloc ( sizeof ( struct Node));
new_node->data  = new_data;
new_node->next = (*head_ref);
(*head_ref)    = new_node;
}
/* Driver program to test above function*/
int main()
{
] // Let us create below linked list.
// 85->15->18->20->85->35->4->20->NULL
struct Node* head = NULL;
push(&head, 20);
[       [HTG1 05]
push(&head, 35);
push(&head, 85);
push(&head, 20);
push(&head, 18);
push(&head, 15);
push(&head, 85);
cout << firstNonRepeating(head);
return 0;
}
```

输出：

```
15

```

**进一步优化**：

上述解决方案需要两次遍历链接列表。 如果我们有很多重复元素，则可以通过将位置也存储在哈希表中来保存一个遍历。 请参考[的最后一种方法。给定字符串，请查找其第一个非重复字符](http://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)。



* * *

* * *



