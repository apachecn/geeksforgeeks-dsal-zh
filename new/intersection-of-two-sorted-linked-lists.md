# 两个排序链表的交叉

> 原文：[https://www.geeksforgeeks.org/intersection-of-two-sorted-linked-lists/](https://www.geeksforgeeks.org/intersection-of-two-sorted-linked-lists/)

给定两个按递增顺序排序的列表，请创建并返回一个新列表，该列表表示两个列表的交集。 新列表应使用自己的内存制作-原始列表不应更改。

**例如**：

```
Input: 
First linked list: 1->2->3->4->6
Second linked list be 2->4->6->8, 
Output: 2->4->6.
The elements 2, 4, 6 are common in 
both the list so they appear in the 
intersection list. 

Input: 
First linked list: 1->2->3->4->5
Second linked list be 2->3->4, 
Output: 2->3->4
The elements 2, 3, 4 are common in 
both the list so they appear in the 
intersection list.

```

**方法 1 **：使用虚拟节点。

**方法**：

的想法是在结果列表的开头使用一个临时的虚拟节点。 指针尾部始终指向结果列表中的最后一个节点，因此可以轻松添加新节点。 虚拟节点最初为尾部提供指向的存储空间。 该虚拟节点是有效的，因为它只是临时的，并且在栈中分配。 循环继续进行，从“ a”或“ b”中删除一个节点并将其添加到尾部。 当遍历给定的列表时，结果在 dummy.next 中，因为值是从哑元的下一个节点分配的。 如果两个元素相等，则将其都移除，然后将元素插入尾部。 否则，删除两个列表中较小的元素。

下面是上述方法的实现：

## C

```c

#include <stdio.h>
#include <stdlib.h>

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

void push(struct Node** head_ref, int new_data);

/*This solution uses the temporary
 dummy to build up the result list */
struct Node* sortedIntersect(
    struct Node* a,
    struct Node* b)
{
    struct Node dummy;
    struct Node* tail = &dummy;
    dummy.next = NULL;

    /* Once one or the other 
    list runs out -- we're done */
    while (a != NULL && b != NULL) {
        if (a->data == b->data) {
            push((&tail->next), a->data);
            tail = tail->next;
            a = a->next;
            b = b->next;
        }
        /* advance the smaller list */
        else if (a->data < b->data)
            a = a->next;
        else
            b = b->next;
    }
    return (dummy.next);
}

/* UTILITY FUNCTIONS */
/* Function to insert a node at 
the beginning of the linked list */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(
        sizeof(struct Node));

    /* put in the data  */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in 
   a given linked list */
void printList(struct Node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

/* Driver program to test above functions*/
int main()
{
    /* Start with the empty lists */
    struct Node* a = NULL;
    struct Node* b = NULL;
    struct Node* intersect = NULL;

    /* Let us create the first sorted 
     linked list to test the functions
     Created linked list will be 
     1->2->3->4->5->6 */
    push(&a, 6);
    push(&a, 5);
    push(&a, 4);
    push(&a, 3);
    push(&a, 2);
    push(&a, 1);

    /* Let us create the second sorted linked list 
   Created linked list will be 2->4->6->8 */
    push(&b, 8);
    push(&b, 6);
    push(&b, 4);
    push(&b, 2);

    /* Find the intersection two linked lists */
    intersect = sortedIntersect(a, b);

    printf("\n Linked list containing common items of a & b \n ");
    printList(intersect);

    getchar();
}

```

**输出**：

```
Linked list containing common items of a & b 
 2 4 6 

```

**复杂度分析**：

*   **时间复杂度**：`O(M + N)`，其中 m 和 n 分别是第一链表和第二链表中的节点数。

    仅需要遍历列表之一。

*   **辅助空间**：O（min（m，n））。

    输出列表最多可以存储 min（m，n）个节点。

**方法 2 **：使用本地引用。

**方法**：此解决方案在结构上与上述非常相似，但避免使用虚拟节点，而是维护一个结构节点**指针 lastPtrRef，该指针始终指向该指针的最后一个指针。 结果列表。 这解决了虚拟节点所做的相同情况—在结果列表为空时处理结果列表。 如果列表建立在其尾部，则可以使用虚拟节点或结构节点**“引用”策略。

下面是上述方法的实现：

## C

```c

#include <stdio.h>
#include <stdlib.h>

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

void push(struct Node** head_ref,
          int new_data);

/* This solution uses the local reference */
struct Node* sortedIntersect(
    struct Node* a,
    struct Node* b)
{
    struct Node* result = NULL;
    struct Node** lastPtrRef = &result;

    /* Advance comparing the first
     nodes in both lists.
    When one or the other list runs
     out, we're done. */
    while (a != NULL && b != NULL) {
        if (a->data == b->data) {
            /* found a node for the intersection */
            push(lastPtrRef, a->data);
            lastPtrRef = &((*lastPtrRef)->next);
            a = a->next;
            b = b->next;
        }
        else if (a->data < b->data)
            a = a->next; /* advance the smaller list */
        else
            b = b->next;
    }
    return (result);
}

/* UTILITY FUNCTIONS */
/* Function to insert a node at the
   beginging of the linked list */
void push(struct Node** head_ref,
          int new_data)
{
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(
        sizeof(struct Node));

    /* put in the data  */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in a given linked list */
void printList(struct Node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

/* Driver program to test above functions*/
int main()
{
    /* Start with the empty lists */
    struct Node* a = NULL;
    struct Node* b = NULL;
    struct Node* intersect = NULL;

    /* Let us create the first sorted 
     linked list to test the functions
   Created linked list will be 
   1->2->3->4->5->6 */
    push(&a, 6);
    push(&a, 5);
    push(&a, 4);
    push(&a, 3);
    push(&a, 2);
    push(&a, 1);

    /* Let us create the second sorted linked list 
   Created linked list will be 2->4->6->8 */
    push(&b, 8);
    push(&b, 6);
    push(&b, 4);
    push(&b, 2);

    /* Find the intersection two linked lists */
    intersect = sortedIntersect(a, b);

    printf("\n Linked list containing common items of a & b \n ");
    printList(intersect);

    getchar();
}

```

**输出**：

```
Linked list containing common items of a & b 
 2 4 6 

```

**复杂度分析**：

*   **时间复杂度**：`O(M + N)`，其中 m 和 n 分别是第一链表和第二链表中的节点数。

    仅需要遍历列表之一。

*   **辅助空间**：O（max（m，n））。

    输出列表最多可以存储 m + n 个节点。

**方法 3 **：递归解。

**方法**：

递归方法与上述两种方法非常相似。 构建一个包含两个节点并返回链表节点的递归函数。 比较两个列表的第一个元素。

*   如果它们相似，则用两个列表的下一个节点调用递归函数。 使用当前节点的数据创建一个节点，并将从递归函数返回的节点放入所创建节点的下一个指针。 返回创建的节点。

*   如果值不相等，则删除两个列表中的较小节点，然后调用递归函数。

下面是上述方法的实现：

## C

```c

#include <stdio.h>
#include <stdlib.h>

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

struct Node* sortedIntersect(
    struct Node* a,
    struct Node* b)
{
    /* base case */
    if (a == NULL || b == NULL)
        return NULL;

    /* If both lists are non-empty */

    /* advance the smaller list and call recursively */
    if (a->data < b->data)
        return sortedIntersect(a->next, b);

    if (a->data > b->data)
        return sortedIntersect(a, b->next);

    // Below lines are executed only
    // when a->data == b->data
    struct Node* temp
        = (struct Node*)malloc(
            sizeof(struct Node));
    temp->data = a->data;

    /* advance both lists and call recursively */
    temp->next = sortedIntersect(a->next, b->next);
    return temp;
}

/* UTILITY FUNCTIONS */
/* Function to insert a node at 
the beginging of the linked list */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node
        = (struct Node*)malloc(
            sizeof(struct Node));

    /* put in the data  */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in a given linked list */
void printList(struct Node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

/* Driver program to test above functions*/
int main()
{
    /* Start with the empty lists */
    struct Node* a = NULL;
    struct Node* b = NULL;
    struct Node* intersect = NULL;

    /* Let us create the first sorted
      linked list to test the functions
     Created linked list will be 
      1->2->3->4->5->6 */
    push(&a, 6);
    push(&a, 5);
    push(&a, 4);
    push(&a, 3);
    push(&a, 2);
    push(&a, 1);

    /* Let us create the second sorted linked list
     Created linked list will be 2->4->6->8 */
    push(&b, 8);
    push(&b, 6);
    push(&b, 4);
    push(&b, 2);

    /* Find the intersection two linked lists */
    intersect = sortedIntersect(a, b);

    printf("\n Linked list containing common items of a & b \n ");
    printList(intersect);

    return 0;
}

```

**输出**：

```
Linked list containing common items of a & b 
 2 4 6 

```

**复杂度分析**：

*   **时间复杂度**：`O(M + N)`，其中 m 和 n 分别是第一链表和第二链表中的节点数。

    仅需要遍历列表之一。

*   **辅助空间**：O（max（m，n））。

    输出列表最多可以存储 m + n 个节点。

如果您发现上述代码/算法有误，请写评论，或者找到解决同一问题的更好方法。

参考：

[cslibrary.stanford.edu/105/LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)

