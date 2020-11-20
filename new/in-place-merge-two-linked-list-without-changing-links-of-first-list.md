# 就地合并两个链表，而不更改第一个列表的链接

> 原文：[https://www.geeksforgeeks.org/in-place-merge-two-linked-list-without-changing-links-of-first-list/](https://www.geeksforgeeks.org/in-place-merge-two-linked-list-without-changing-links-of-first-list/)

给定两个分别具有 n 和 m 个元素的排序的单链表，请使用恒定空间合并它们。 两个列表中的前 n 个最小元素应成为第一个列表的一部分，其余元素应成为第二个列表的一部分。 应保持排序顺序。 我们不允许更改第一个链表的指针。

例如，

```
Input:
First List: 2->4->7->8->10
Second List: 1->3->12

Output: 
First List: 1->2->3->4->7
Second List: 8->10->12

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

如果允许我们更改第一个链表的指针，问题将变得非常简单。 如果允许更改链接，我们可以简单地执行诸如 merge-sort 算法的 merge 之类的操作。 我们将前 n 个最小的元素分配给第一个链表，其中 n 是第一个链表中的元素数，其余为第二个链表。 我们可以在`O(M + N)`的时间和`O(1)`的空间中实现此目标，但是此解决方案违反了我们不能更改第一列表链接的要求。

这个问题变得有些棘手，因为我们不允许在第一个链表中更改指针。 这个想法类似于此帖子的[，但是由于我们获得了单链列表，因此我们无法向后处理 LL2 的最后一个元素。](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)

这个想法是针对 LL1 的每个元素，我们将其与 LL2 的第一个元素进行比较。 如果 LL1 的元素大于 LL2 的第一个元素，则我们交换涉及的两个元素。 为了使 LL2 保持排序，我们需要将 LL2 的第一个元素放在其正确位置。 我们可以通过一次遍历 LL2 并更正指针来发现不匹配。

以下是此想法的 C++实现。

```

// Program to merge two sorted linked lists without 
// using any extra space and without changing links 
// of first list 
#include <bits/stdc++.h> 
using namespace std; 

 /* Structure for a linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

// Function to merge two sorted linked lists 
// LL1 and LL2 without using any extra space. 
void mergeLists(struct Node *a, struct Node * &b) 
{ 
    // run till either one of a or b runs out 
    while (a && b) 
    { 
        // for each element of LL1, 
        // compare it with first element of LL2\. 
        if (a->data > b->data) 
        { 
            // swap the two elements involved 
            // if LL1 has a greater element 
            swap(a->data, b->data); 

            struct Node *temp = b; 

            // To keep LL2 sorted, place first 
            // element of LL2 at its correct place 
            if (b->next && b->data > b->next->data) 
            { 
                b = b->next; 
                struct Node *ptr= b, *prev = NULL; 

                // find mismatch by traversing the 
                // second linked list once 
                while (ptr && ptr->data < temp->data) 
                { 
                    prev = ptr; 
                    ptr = ptr -> next; 
                } 

                // correct the pointers 
                prev->next = temp; 
                temp->next = ptr; 
            } 
        } 

        // move LL1 pointer to next element 
        a = a->next; 
    } 
} 

// Code to print the linked link 
void printList(struct Node *head) 
{ 
    while (head) 
    { 
        cout << head->data << "->" ; 
        head = head->next; 
    } 
    cout << "NULL" << endl; 
} 

// Driver code 
int main() 
{ 
    struct Node *a = NULL; 
    push(&a, 10); 
    push(&a, 8); 
    push(&a, 7); 
    push(&a, 4); 
    push(&a, 2); 

    struct Node *b = NULL; 
    push(&b, 12); 
    push(&b, 3); 
    push(&b, 1); 

    mergeLists(a, b); 

    cout << "First List: "; 
    printList(a); 

    cout << "Second List: "; 
    printList(b); 

    return 0; 
} 

```

输出：

```
First List: 1->2->3->4->7->NULL
Second List: 8->10->12->NULL

```

时间复杂度：O（mn）

本文由 **Aditya Goel** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

