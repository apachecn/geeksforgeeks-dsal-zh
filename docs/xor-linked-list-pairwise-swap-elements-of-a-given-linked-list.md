# 异或链表–给定链表的成对交换元素

> 原文:[https://www . geesforgeks . org/xor-链表-成对-交换-给定链表的元素/](https://www.geeksforgeeks.org/xor-linked-list-pairwise-swap-elements-of-a-given-linked-list/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)，任务是成对交换给定[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)的元素。

**示例:**

> **输入:** 4 7 9 7
> **输出:** 7 4 7 9
> **解释:**
> 第一对节点交换形成序列{4，7}，第二对节点交换形成序列{9，7}。
> 
> **输入:**1 2 3
> T3】输出: 2 1 3- > - > - > - >
> 
> ->->->->->->

**方法:**使用给定链表的[成对交换元素的概念可以解决这个问题。其思想是](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)[遍历给定的异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)并选择两个相邻的节点对并交换它们。按照以下步骤解决问题:

*   [遍历给定的异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)，同时异或链表的**当前节点**和**下一节点**不为空
*   在每次迭代中，将**当前节点**的数据与**下一个节点**交换，并更新**下一个节点**和**当前节点的指针。**
*   最后[打印异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)

下面是上述方法的实现:

## C

```
// C program to implement
// the above approach
#include <inttypes.h>
#include <stdio.h>
#include <stdlib.h>

// Structure of a node
// in XOR linked list
struct Node {

    // Stores data value
    // of a node
    int data;

    // Stores XOR of previous
    // pointer and next pointer
    struct Node* nxp;
};

void pairwiseswap(struct Node**);
void swap(int*, int*);

// Function to find the XOR of two nodes
struct Node* XOR(struct Node* a, struct Node* b)
{
    return (struct Node*)((uintptr_t)(a)
                          ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(struct Node** head,
                    int value)
{

    // If XOR linked list is empty
    if (*head == NULL) {

        // Initialize a new Node
        struct Node* node
            = (struct Node*)malloc(
                sizeof(struct Node));

        // Stores data value in
        // the node
        node->data = value;

        // Stores XOR of previous
        // and next pointer
        node->nxp = XOR(NULL, NULL);

        // Update pointer of head node
        *head = node;
    }

    // If the XOR linked list
    // is not empty
    else {

        // Stores the address
        // of current node
        struct Node* curr = *head;

        // Stores the address
        // of previous node
        struct Node* prev = NULL;

        // Initialize a new Node
        struct Node* node
            = (struct Node*)malloc(
                sizeof(struct Node));

        // Update curr node address
        curr->nxp = XOR(node,
                        XOR(NULL, curr->nxp));

        // Update new node address
        node->nxp = XOR(NULL, curr);

        // Update head
        *head = node;

        // Update data value of
        // current node
        node->data = value;
    }
    return *head;
}

// Function to pairwise swap the nodes
// of the XOR-linked list
void pairwiseswap(struct Node** head)
{

    // Stores pointer of current node
    struct Node* curr = (*head);

    // Stores pointer of previous node
    struct Node* prev = NULL;

    // Stores pointer of next node
    struct Node* next = NULL;

    // Traverse the XOR-linked list
    while (curr != NULL
           && curr->nxp != XOR(prev, NULL)) {

        next = XOR(prev, curr->nxp);
        prev = curr;
        curr = next;

        // Swap the elements
        swap(&prev->data, &curr->data);

        // Update next
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
}

// Function to swap two numbers
void swap(int* a, int* b)
{
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

// Function to print elements of
// the XOR Linked List
void printList(struct Node** head)
{
    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;

    // Traverse XOR linked list
    while (curr != NULL) {

        // Print current node
        printf("%d ", curr->data);

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
}

// Driver Code
int main()
{

    /* Create following XOR Linked List
    head -->7 –> 6 –>8 –> 11 –> 3 –> 1 –> 2 –> 0*/
    struct Node* head = NULL;

    insert(&head, 0);
    insert(&head, 2);
    insert(&head, 1);
    insert(&head, 3);
    insert(&head, 11);
    insert(&head, 8);
    insert(&head, 6);
    insert(&head, 7);

    // Swap the elements pairwise
    pairwiseswap(&head);

    // Print the new list
    printList(&head);

    return (0);
}
```

**Output:**

```
6 7 11 8 1 3 0 2

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)