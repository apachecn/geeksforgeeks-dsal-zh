# 两个链表的并集和相交| 设置 2（使用合并排序）

> 原文：[https://www.geeksforgeeks.org/union-intersection-two-linked-lists-set-2-using-merge-sort/](https://www.geeksforgeeks.org/union-intersection-two-linked-lists-set-2-using-merge-sort/)

给定两个链接列表，创建包含给定列表中元素的并集和交集的并集和交集列表。 输出列表中元素的顺序无关紧要。

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

在[帖子](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)中讨论了三种方法，并实现了方法 1。

在本文中，我们将看到方法 2 的实现，即使用[合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)。

```
Implementation:
Following are the steps to be followed to get union and intersection lists.

1) Sort both Linked Lists using merge sort.
   This step takes O(mLogm) time.

2) Linearly scan both sorted lists to get the union and intersection. 
  This step takes O(m + n) time.

```

**算法**：

1.  [使用合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对两个链表进行排序。

2.  线性扫描两个排序列表以获取并集和交集。

3.  对两个链表执行合并操作，保持指向最初指向两个链表第一个节点的指针。

4.  比较两个节点，直到和除非两个指针都不为空。

    1.  如果相等，则将其添加到相交列表和并集列表，然后移至两个指针的下一个节点

    2.  如果不相等，则将较小的指针值插入联合列表，然后移至下一个节点

5.  如果指针之一为空，则遍历另一个列表及其所有节点以合并列表。

**与方法 1 一样，此方法还假定列表中有不同的元素。**

```
// C++ program to find union and intersection of
// two unsorted linked lists in O(n Log n) time.
#include <bits/stdc++.h>
using namespace std;
/* Link list node */
struct Node {
int data;
struct Node* next;
};
/* A utility function to insert a
node at the beginning of a linked list*/
void push(struct Node** head_ref, int new_data)
{
/* allocate node */
struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
/* put in the data */
new_node->data = new_data;
/* link the old list off the new node */
new_node->next = (*head_ref);
/* move the head to point to the new node */
(*head_ref) = new_node;
}
/* UTILITY FUNCTIONS */
/* Split the nodes of the given
list into front and back halves,
and return the two lists
using the reference parameters.
If the length is odd, the
extra node should go in the
front list.
Uses the fast/slow pointer strategy. */
void FrontBackSplit(struct Node* source,
struct Node** frontRef,
struct Node** backRef)
{
struct Node* fast;
struct Node* slow;
if (source == NULL || source->next == NULL) {
/* length < 2 cases */
*frontRef = source;
*backRef = NULL;
}
else {
slow = source;
fast = source->next;
/* Advance 'fast' two nodes, and
advance 'slow' one node */
while (fast != NULL) {
fast = fast->next;
if (fast != NULL) {
slow = slow->next;
fast = fast->next;
}
}
/* 'slow' is before the midpoint in the list,
so split it in two at that point. */
*frontRef = source;
*backRef = slow->next;
slow->next = NULL;
}
}
/* See https:// www.geeksforgeeks.org/?p=3622 for details
of this function */
struct Node* SortedMerge(struct Node* a,
struct Node* b)
{
struct Node* result = NULL;
/* Base cases */
if (a == NULL)
return (b);
else if (b == NULL)
return (a);
/* Pick either a or b, and recur */
if (a->data <= b->data) {
result = a;
result->next = SortedMerge(a->next, b);
}
else {
result = b;
result->next = SortedMerge(a, b->next);
}
return (result);
}
/* sorts the linked list by changing
next pointers (not data) */
void mergeSort(struct Node** headRef)
{
struct Node* head = *headRef;
struct Node *a, *b;
/* Base case -- length 0 or 1 */
if ((head == NULL) || (head->next == NULL))
return;
/* Split head into 'a' and 'b' sublists */
FrontBackSplit(head, &a, &b);
/* Recursively sort the sublists */
mergeSort(&a);
mergeSort(&b);
/* answer = merge the two sorted lists together */
*headRef = SortedMerge(a, b);
}
/* Function to get union of two
linked lists head1 and head2 */
struct Node* getUnion(struct Node* head1,
struct Node* head2)
{
struct Node* result = NULL;
struct Node *t1 = head1, *t2 = head2;
// Traverse both lists and store the
// element in the resu1tant list
while (t1 != NULL && t2 != NULL) {
// Move to the next of first list
// if its element is smaller
if (t1->data < t2->data) {
push(&result, t1->data);
t1 = t1->next;
}
// Else move to the next of second list
else if (t1->data > t2->data) {
push(&result, t2->data);
t2 = t2->next;
}
// If same then move to the next node
// in both lists
else {
push(&result, t2->data);
t1 = t1->next;
t2 = t2->next;
}
}
/* Print remaining elements of the lists */
while (t1 != NULL) {
push(&result, t1->data);
t1 = t1->next;
}
while (t2 != NULL) {
push(&result, t2->data);
t2 = t2->next;
}
return result;
}
/* Function to get intersection of
two linked lists head1 and head2 */
struct Node* getIntersection(struct Node* head1,
struct Node* head2)
{
struct Node* result = NULL;
struct Node *t1 = head1, *t2 = head2;
// Traverse both lists and store the same element
// in the resu1tant list
while (t1 != NULL && t2 != NULL) {
// Move to the next of first
// list if smaller
if (t1->data < t2->data)
t1 = t1->next;
// Move to the next of second
// list if it is smaller
else if (t1->data > t2->data)
t2 = t2->next;
// If both are same
else {
// Store current element in the list
push(&result, t2->data);
// Move to the next node of both lists
t1 = t1->next;
t2 = t2->next;
}
}
// return the resultant list
return result;
}
/* A utility function to print a linked list*/
void printList(struct Node* node)
{
while (node != NULL) {
printf("%d ", node->data);
node = node->next;
}
}
/* Driver program to test above function*/
int main()
{
/* Start with the empty list */
struct Node* head1 = NULL;
struct Node* head2 = NULL;
struct Node* intersection_list = NULL;
struct Node* union_list = NULL;
/*create a linked list 11->10->15->4->20 */
push(&head1, 20);
push(&head1, 4);
push(&head1, 15);
push(&head1, 10);
push(&head1, 11);
/*create a linked list 8->4->2->10 */
push(&head2, 10);
push(&head2, 2);
push(&head2, 4);
push(&head2, 8);
/* Sort the above created Linked List */
mergeSort(&head1);
mergeSort(&head2);
intersection_list = getIntersection(head1, head2);
union_list = getUnion(head1, head2);
printf("First list is \n");
printList(head1);
printf("\nSecond list is \n");
printList(head2);
printf("\nIntersection list is \n");
printList(intersection_list);
printf("\nUnion list is \n");
printList(union_list);
return 0;
}
```

**输出**：

```
First list is 
4 10 11 15 20 
Second list is 
2 4 8 10 
Intersection list is 
10 4 
Union list is 
20 15 11 10 8 4 2 

```

**复杂度分析**：

*   **时间复杂度**：O（m Log m + n Log n）。

    对列表进行排序所需的时间为 n log n 和 m log m，以及查找并集和交点线性时间。

*   **辅助空间**：O（m + n）。

    如果存储了输出，则需要 O（m + n）空间。

在下一篇文章中，将讨论方法 3，即使用散列。

本文由 [**Sahil Chhabra**](https://www.facebook.com/sahil.chhabra.965) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

