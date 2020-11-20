# C 程序：反转单链表

> 原文：[https://www.geeksforgeeks.org/c-program-reverse-node-value-singly-linked-list/](https://www.geeksforgeeks.org/c-program-reverse-node-value-singly-linked-list/)

中的每个节点值

[链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)是数据元素的线性集合，其中每个节点都指向下一个节点。 与数组不同，它没有上限，因此非常有用。

任务是访问链表的每个节点的值并反转它们。

**范例**：

```
Input : 56 87 12 49 35
Output :65 78 21 94 53

Input : 128 87 12433 491 33
Output :821 78 33421 194 33

```

**算法**：

该任务可以通过以下方式完成：

1.  线性遍历单链表的每个节点。

2.  反转每个节点的值。

3.  将取反的值存储在当前节点中。

```

// C program to reverse every node data in 
// singly linked list. 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// newNode function inserts the new node at 
// the right side of linked list 
struct Node* newNode(int key) 
{ 
    struct Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// reverse() will receive individual data item 
// from reverseIndividualData() and will return 
// the reversed number to calling function 
int reverse(int number) 
{ 
    int new_num = 0, rem; 

    while (number != 0) { 
        rem = number % 10; 
        new_num = new_num * 10 + rem; 
        number = number / 10; 
    } 

    return new_num; 
} 

void reverseIndividualData(struct Node* node) 
{ 

    if (node == NULL) 
        return; 

    while (node != NULL) { 

        /*  function call to reverse(), 
            reverseIndividualData(struct Node *node) 
            will send the one data item at a time to 
            reverse(node->data) function which will 
            return updated value to node->data*/

        node->data = reverse(node->data); 

        /*  updating node pointer so as to get 
            next value */

        node = node->next; 
    } 
} 

// Function to print nodes in linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Node* head = NULL; 
    head = newNode(56); 
    head->next = newNode(87); 
    head->next->next = newNode(12); 
    head->next->next->next = newNode(49); 
    head->next->next->next->next = newNode(35); 

    printf("\nList before reversing individual data item \n"); 
    printList(head); 

    reverseIndividualData(head); 

    printf("\nList after reversing individual data item\n"); 
    printList(head); 

    return 0; 
} 

```

**Output:**

```
List before reversing individual data item
56 87 12 49 35 
List after reversing individual data item
65 78 21 94 53

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。