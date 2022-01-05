# 异或链表:反转链表的最后 K 个节点

> 原文:[https://www . geesforgeks . org/xor-链表-反向-链表最后 k 个节点/](https://www.geeksforgeeks.org/xor-linked-list-reverse-last-k-nodes-of-a-linked-list/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)和一个正整数 **K** ，任务是 [**反转**给定异或链表中的最后一个 **K** 节点](https://www.geeksforgeeks.org/reverse-first-k-elements-given-linked-list/)。

**示例:**

> **输入:**LL:7<–>6<–>8<–>11<–>3<–>1、K = 3
> **输出:**7<–>6<–>8<–>1<–>3<–>11
> 
> **输入:**LL:7<–>6<–>8<–>11<–>3<–>1<–>2<–>0，K = 5
> **输出:**7<–>6<–>8<–>0【T25

**方法:**按照以下步骤解决给定问题:

*   反转给定的[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)。
*   现在，[反转反向链表](https://www.geeksforgeeks.org/reverse-first-k-elements-given-linked-list/)的第一个 **K** 节点。
*   完成上述步骤后，[再次反向链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)得到结果链表。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <inttypes.h>
#include <stdio.h>
#include <stdlib.h>

// Structure of a node
// of XOR Linked List
struct Node {

    // Stores data value
    // of a node
    int data;

    // Stores XOR of previous
    // pointer and next pointer
    struct Node* nxp;
};

// Function to calculate
// Bitwise XOR of the two nodes
struct Node* XOR(struct Node* a,
                 struct Node* b)
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

        // Stores data value in the node
        node->data = value;

        // Stores XOR of previous
        // and next pointer
        node->nxp = XOR(NULL, NULL);

        // Update pointer of head node
        *head = node;
    }

    // If the XOR linked
    // list is not empty
    else {

        // Stores the address
        // of the current node
        struct Node* curr = *head;

        // Stores the address
        // of the previous node
        struct Node* prev = NULL;

        // Initialize a new Node
        struct Node* node
            = (struct Node*)malloc(
                sizeof(struct Node));

        // Update address of current node
        curr->nxp = XOR(node,
                        XOR(
                            NULL, curr->nxp));

        // Update address of the new node
        node->nxp = XOR(NULL, curr);

        // Update the head node
        *head = node;

        // Update the data
        // value of current node
        node->data = value;
    }
    return *head;
}

// Function to print elements
// of the XOR Linked List
void printList(struct Node** head)
{
    // Stores XOR pointer
    // in the current node
    struct Node* curr = *head;

    // Stores XOR pointer
    // in the previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer in the
    // next node
    struct Node* next;

    // Traverse XOR linked list
    while (curr != NULL) {

        // Print the current node
        printf("%d ", curr->data);

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update the prev pointer
        prev = curr;

        // Update the curr pointer
        curr = next;
    }
}

// Function to reverse the linked
// list in the groups of K
struct Node* reverseK(struct Node** head,
                      int K, int len)
{
    struct Node* curr = *head;

    // If head is NULL
    if (curr == NULL)
        return NULL;

    // If the size of XOR linked
    // list is less than K
    else if (len < K)
        return *head;
    else {

        int count = 0;

        // Stores the XOR pointer
        // in the previous Node
        struct Node* prev = NULL;

        // Stores the XOR pointer
        // in the next node
        struct Node* next;

        while (count < K) {

            // Forward traversal
            next = XOR(prev, curr->nxp);

            // Update the prev pointer
            prev = curr;

            // Update the curr pointer
            curr = next;

            // Count the number of
            // nodes processed
            count++;
        }

        // Remove the prev node
        // from the next node
        prev->nxp = XOR(NULL,
                        XOR(prev->nxp,
                            curr));

        // Add the head pointer with prev
        (*head)->nxp = XOR(XOR(NULL,
                               (*head)->nxp),
                           curr);

        // Add the prev with the head
        if (curr != NULL)
            curr->nxp = XOR(XOR(curr->nxp,
                                prev),
                            *head);
        return prev;
    }
}

// Function to reverse last K nodes
// of the given XOR Linked List
void reverseLL(struct Node* head,
               int N, int K)
{

    // Reverse the given XOR LL
    head = reverseK(&head, N, N);

    // Reverse the first K nodes of
    // the XOR LL
    head = reverseK(&head, K, N);

    // Reverse the given XOR LL
    head = reverseK(&head, N, N);

    // Print the final linked list
    printList(&head);
}

// Driver Code
int main()
{
    // Stores number of nodes
    int N = 6;

    // Given XOR Linked List

    struct Node* head = NULL;
    insert(&head, 1);
    insert(&head, 3);
    insert(&head, 11);
    insert(&head, 8);
    insert(&head, 6);
    insert(&head, 7);

    int K = 3;

    reverseLL(head, N, K);

    return (0);
}
```

**Output:**

```
7 6 8 1 3 11

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)