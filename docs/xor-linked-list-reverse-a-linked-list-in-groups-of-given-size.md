# 异或链表–在给定大小的组中反转链表

> 原文:[https://www . geesforgeks . org/xor-链表-反向-给定大小的一组链表/](https://www.geeksforgeeks.org/xor-linked-list-reverse-a-linked-list-in-groups-of-given-size/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)和一个整数 **K** ，任务是反转给定**异或链表**中的每个 **K** 节点。

**示例:**

> **输入:**XLL = 7<–>6<–>8<–>11<–>3，K = 3
> **输出:**8<–>6<–>7<–>3<–>11
> T6】说明:
> 先倒 K(= 3)
> 将链表剩余节点反转为 8<–>6<–>7<–>3<–>11。
> 因此，所需输出为 8<–>6<–>7<–>3<–>11。
> 
> **输入:**XLL = 7<–>6<–>8<–>11<–>3<–>1<–>2<–>0，K = 3
> T3】输出:8<–>6<–>7<–>1【T25

**方法:**思想是递归反转一组中[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)的每个 **K** 节点，并将每组 **K** 节点的第一个节点连接到其前一组节点的最后一个节点。递归函数如下:

> RevInGrp(head，K，N)
> {
> reving(head，min(K，N))
> if(N<K){
> return head
> }
> head->next = RevInGrp(next，K，N–K)
> }

按照以下步骤解决问题:

*   反转**异或链表**的第一个 **K** 节点，递归反转一组大小 **K** 中的剩余节点。如果剩余节点数小于 **K** ，则只需反转剩余节点即可。
*   最后，将每个组的第一个节点连接到前一个组的最后一个节点。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
#include <inttypes.h>
using namespace std;

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

// Function to find the XOR of address
// of two nodes
struct Node* XOR(struct Node* a, struct Node* b)
{
    return (struct Node*)((uintptr_t)(a) ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(struct Node** head, int value)
{

    // If XOR linked list is empty
    if (*head == NULL) {

        // Initialize a new Node
        struct Node* node = new Node;

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
            = new Node();

        // Update curr node address
        curr->nxp = XOR(node, XOR(NULL, curr->nxp));

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
        cout << curr->data << " ";

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
}

// Reverse the linked list in group of K
struct Node* RevInGrp(struct Node** head, int K, int len)
{

    // Stores head node
    struct Node* curr = *head;

    // If the XOR linked
    // list is empty
    if (curr == NULL)
        return NULL;

    // Stores count of nodes
    // reversed in current group
    int count = 0;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;

    // Reverse nodes in current group
    while (count < K && count < len) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        // Update count
        count++;
    }

    // Disconnect prev node from the next node
    prev->nxp = XOR(NULL, XOR(prev->nxp, curr));

    // Disconnect curr from previous node
    if (curr != NULL)
        curr->nxp = XOR(XOR(curr->nxp, prev), NULL);

    // If the count of remaining
    // nodes is less than K
    if (len < K) {
        return prev;
    }
    else {

        // Update len
        len -= K;

        // Recursively process the next nodes
        struct Node* dummy = RevInGrp(&curr, K, len);

        // Connect the head pointer with the prev
        (*head)->nxp = XOR(XOR(NULL, (*head)->nxp), dummy);

        // Connect prev with the head
        if (dummy != NULL)
            dummy->nxp = XOR(XOR(dummy->nxp, NULL), *head);
        return prev;
    }
}

// Driver Code
int main()
{

    /* Create following XOR Linked List
    head-->7<–>6<–>8<–>11<–>3<–>1<–>2<–>0*/
    struct Node* head = NULL;
    insert(&head, 0);
    insert(&head, 2);
    insert(&head, 1);
    insert(&head, 3);
    insert(&head, 11);
    insert(&head, 8);
    insert(&head, 6);
    insert(&head, 7);

    // Function Call
    head = RevInGrp(&head, 3, 8);

    // Print the reversed list
    printList(&head);

    return (0);
}

// This code is contributed by pankajsharmagfg.
```

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

// Function to find the XOR of address
// of two nodes
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
        curr->nxp = XOR(node, XOR(NULL,
                                  curr->nxp));

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

// Reverse the linked list in group of K
struct Node* RevInGrp(struct Node** head,
                      int K, int len)
{

    // Stores head node
    struct Node* curr = *head;

    // If the XOR linked
    // list is empty
    if (curr == NULL)
        return NULL;

    // Stores count of nodes
    // reversed in current group
    int count = 0;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;

    // Reverse nodes in current group
    while (count < K && count < len) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        // Update count
        count++;
    }

    // Disconnect prev node from the next node
    prev->nxp = XOR(NULL, XOR(prev->nxp, curr));

    // Disconnect curr from previous node
    if (curr != NULL)
        curr->nxp = XOR(XOR(curr->nxp, prev), NULL);

    // If the count of remaining
    // nodes is less than K
    if (len < K) {
        return prev;
    }
    else {

        // Update len
        len -= K;

        // Recursively process the next nodes
        struct Node* dummy
            = RevInGrp(&curr, K, len);

        // Connect the head pointer with the prev
        (*head)->nxp = XOR(XOR(NULL,
                               (*head)->nxp),
                           dummy);

        // Connect prev with the head
        if (dummy != NULL)
            dummy->nxp = XOR(XOR(dummy->nxp, NULL),
                             *head);
        return prev;
    }
}

// Driver Code
int main()
{

    /* Create following XOR Linked List
    head-->7<–>6<–>8<–>11<–>3<–>1<–>2<–>0*/
    struct Node* head = NULL;
    insert(&head, 0);
    insert(&head, 2);
    insert(&head, 1);
    insert(&head, 3);
    insert(&head, 11);
    insert(&head, 8);
    insert(&head, 6);
    insert(&head, 7);

    // Function Call
    head = RevInGrp(&head, 3, 8);

    // Print the reversed list
    printList(&head);

    return (0);
}
```

**Output:** 

```
8 6 7 1 3 11 0 2
```

***时间复杂度:** O(N)*
***辅助空间:** O(N / K)*