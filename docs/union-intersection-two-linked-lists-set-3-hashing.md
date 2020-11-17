# 两个链表的并集和交集 | 系列 3（哈希）

> 原文：[https://www.geeksforgeeks.org/union-intersection-two-linked-lists-set-3-hashing/](https://www.geeksforgeeks.org/union-intersection-two-linked-lists-set-3-hashing/)

给定两个链表，创建包含给定列表中元素的并集和交集的并集和交集列表。 输出列表中元素的顺序无关紧要。

**示例**：

```
Input:
   List1: 10 -> 15 -> 4 -> 20
   List2: 8 -> 4 -> 2 -> 10
Output:
   Intersection List: 4 -> 10
   Union List: 2 -> 8 -> 20 -> 4 -> 15 -> 10
Explanation: In this two lists 4 and 10 nodes 
are common. The union lists contains 
all the nodes of both the lists.

Input:
   List1: 1 -> 2 -> 3 -> 4
   List2: 3 -> 4 -> 8 -> 10
Output:
   Intersection List: 3 -> 4
   Union List: 1 -> 2 -> 3 -> 4 -> 8 -> 10
Explanation: In this two lists 4 and 3 nodes 
are common. The union lists contains 
all the nodes of both the lists.

```

我们已经讨论了该问题的[方法 1](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/) 和[方法 2](https://www.geeksforgeeks.org/union-intersection-two-linked-lists-set-2-using-merge-sort/) 。

在这篇文章中，讨论了方法 3（使用哈希），其时间复杂度为`O(m + n)`，即比前面讨论的两种方法都更好。

```
Implementation:
1- Start traversing both the lists.
   a) Store the current element of both lists
      with its occurrence in the map.
2- For Union: Store all the elements of the map 
   in the resultant list.
3- For Intersection: Store all the elements only 
   with an occurrence of 2 as 2 denotes that 
   they are present in both the lists.

```

以下是上述步骤的 C++ 实现。

```
// C++ program to find union and intersection of
// two unsorted linked lists in O(m+n) time.
#include <bits/stdc++.h>
using namespace std;
[
/* Link list node */
struct Node {
int data;
struct Node* next;
};
/* A utility function to insert a node at the
beginning of a linked list*/
void push( struct Node** head_ref, int new_data)
{
/* allocate node */
struct Node* new_node = ( struct Node*) malloc (
sizeof ( struct Node));
/* put in the data */
new_node->data = new_data;
/* link the old list off the new node */
new_node->next = (*head_ref);
[H TG52]
/* move the head to point to the new node */
(*head_ref) = new_node;
}
/* Utility function to store the
elements of both list */
void storeEle( struct Node* head1, struct Node* head2,
unordered_map< int , int >& eleOcc)
{
struct Node* ptr1 = head1;
struct Node* ptr2 = head2;
// Traverse both lists
while (ptr1 != NULL || ptr2 != NULL) {
// store element in the map
if (ptr1 != NULL) {
eleOcc[ptr1->data]++;
ptr1 = ptr1->next;
}
// store element in the map
if (ptr2 != NULL) {
eleOcc[ptr2->data]++; [
ptr2 = ptr2->next;
}
}
}
/* Function to get the union of two
linked lists head1 and head2 */
struct Node* getUnion(
unordered_map< int , int > eleOcc)
{
struct Node* result = NULL;
// Push all the elements into
// the resultant list
for ( auto it = eleOcc.begin(); it != eleOcc.end(); it++)
push(&result, it->first);
return result;
}
/* Function to get the intersection of
two linked lists head1 and head2 */
struct Node* getIntersection(
unordered_map< int , int > eleOcc)
{
struct Node* result = NULL;
// Push a node with an element
// having occurrence of 2 as that
// means the current element is
// present in both the lists
for ( auto it = eleOcc.begin();
it != eleOcc.end(); it++)
if (it->second == 2)
push(&result, it->first);
// return resultant list
return result;
}
/* A utility function to print a linked list*/
void printList( struct Node* node)
{
while (node != NULL) {
printf ( "%d " , node->data);
node = node->next;
}
}
// Prints union and intersection of
// lists with head1 and head2.
void printUnionIntersection(Node* head1,
Node* head2)
{
// Store all the elements of
// both lists in the map
unordered_map< int , int > eleOcc;
storeEle(head1, head2, eleOcc);
Node* intersection_list = getIntersection(eleOcc);
Node* union_list = getUnion(eleOcc);
printf ( "\nIntersection list is \n" );
printList(intersection_list);
printf ( "\nUnion list is \n" );
printList(union_list);
}
/* Driver program to test above function*/
int [HTG25 5]
{
/* Start with the empty list */
struct Node* head1 = NULL;
struct Node* head2 = NULL;
/* create a linked list 11->10->15->4->20 */
push(&head1, 1);
push(&head1, 2);
]
push(&head1, 3);
push(&head1, 4);
push(&head1, 5);
/* create a linked list 8->4->2->10 */
push(&head2, 1);
push(&head2, 3);
push(&head2, 5);
push(&head2, 6);
printf ( "First list is \n" );
printList(head1);
printf ( "\nSecond list is \n" );
printList(head2);
[HTG59 8]
printUnionIntersection(head1, head2);
return 0;
}
```

**输出**：

```
First list is 
5 4 3 2 1 
Second list is 
6 5 3 1 
Intersection list is 
3 5 1 
Union list is 
3 4 6 5 2 1 

```

我们还可以通过为两个列表维护单独的哈希来处理重复项。

**复杂度分析**：

*   **时间复杂度**：`O(m + n)`。

    这里的`m`和`n`分别是第一和第二列表中存在的元素数。

    **原因**：

    对于并集：遍历两个列表，将元素存储在哈希映射中并更新各自的计数。

    对于交集：检查哈希映射中元素的计数是否为 2。

*   **辅助空间**：`O(m + n)`。

    使用哈希映射数据结构存储值。

本文由 [**Sahil Chhabra**](https://www.facebook.com/sahil.chhabra.965) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

