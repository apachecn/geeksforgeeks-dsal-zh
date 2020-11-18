# 合并两个没有重复的排序链表

合并大小为 **n1** 和 **n2** 的两个排序链表。 在最终排序的链表中，两个链表中的重复项应仅出现一次。

例子：

```
Input : list1: 1->1->4->5->7
        list2: 2->4->7->9
Output : 1 2 4 5 7 9 

```

**来源**：[Microsoft 在校园布置和面试问题上的问题](https://www.geeksforgeeks.org/microsoft-on-campus-placement-and-interview-questions/)

**方法**：以下是步骤：

1.  以排序方式合并两个排序的链表。 请参阅此帖子的[递归方法。 令最终获得的列表为**头**。](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

2.  [从排序的链表](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/) **头**中删除重复项。

```

// C++ implementation to merge two sorted linked list 
// without duplicates 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* temp = (Node*)malloc(sizeof(Node)); 

    // put in data 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// function to merge two sorted linked list 
// in a sorted manner 
Node* sortedMerge(struct Node* a, struct Node* b) 
{ 
    Node* result = NULL; 

    /* Base cases */
    if (a == NULL) 
        return (b); 
    else if (b == NULL) 
        return (a); 

    /* Pick either a or b, and recur */
    if (a->data <= b->data) { 
        result = a; 
        result->next = sortedMerge(a->next, b); 
    } 
    else { 
        result = b; 
        result->next = sortedMerge(a, b->next); 
    } 
    return (result); 
} 

/* The function removes duplicates from a sorted list */
void removeDuplicates(Node* head) 
{ 
    /* Pointer to traverse the linked list */
    Node* current = head; 

    /* Pointer to store the next pointer of a node to be deleted*/
    Node* next_next; 

    /* do nothing if the list is empty */
    if (current == NULL) 
        return; 

    /* Traverse the list till last node */
    while (current->next != NULL) { 

        /* Compare current node with next node */
        if (current->data == current->next->data) { 

            /* The sequence of steps is important*/
            next_next = current->next->next; 
            free(current->next); 
            current->next = next_next; 
        } 
        else /* This is tricky: only advance if no deletion */
        { 
            current = current->next; 
        } 
    } 
} 

// function to merge two sorted linked list 
// without duplicates 
Node* sortedMergeWithoutDuplicates(Node* head1, Node* head2) 
{ 
    // merge two linked list in sorted manner 
    Node* head = sortedMerge(head1, head2); 

    // remove duplicates from the list 'head' 
    removeDuplicates(head); 

    return head; 
} 

// function to print the linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // head1: 1->1->4->5->7 
    Node* head1 = getNode(1); 
    head1->next = getNode(1); 
    head1->next->next = getNode(4); 
    head1->next->next->next = getNode(5); 
    head1->next->next->next->next = getNode(7); 

    // head2: 2->4->7->9 
    Node* head2 = getNode(2); 
    head2->next = getNode(4); 
    head2->next->next = getNode(7); 
    head2->next->next->next = getNode(9); 

    Node* head3; 

    head3 = sortedMergeWithoutDuplicates(head1, head2); 

    printList(head3); 

    return 0; 
} 

```

输出：

```
1 2 4 5 7 9 

```

时间复杂度：O（n1 + n2）。

辅助空间：`O(1)`。

**练习**：获得最终排序的链表，一次遍历两个列表时没有重复项。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。