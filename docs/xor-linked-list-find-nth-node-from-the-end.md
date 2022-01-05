# 异或链表–从末尾找到第 n 个节点

> 原文:[https://www . geesforgeks . org/xor-link-list-find-n-node-from-the-end/](https://www.geeksforgeeks.org/xor-linked-list-find-nth-node-from-the-end/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)和一个整数 **N** ，任务是[从给定](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/) [**异或链表**](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/) 的**端** 打印第 **N** 个节点。

**示例:**

> **输入:**4–>6–>7–>3，N = 1
> **输出:** 3
> **说明:**从末端开始的第一个节点是 3。
> **输入:**5–>8–>9，N = 4
> **输出:**错误输入
> **说明:**给定的异或链表只包含 3 个节点。

**方法:**按照以下步骤解决问题:

*   使用指针遍历链表的第一个 **N 个**节点，比如 **curr** 。
*   使用另一个指针，比如 **curr1** ，在每次迭代后遍历[链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)将 curr 和 curr1 递增一个节点。
*   迭代直到指针 **curr** 超过列表的末尾，即**空**。到达后，打印节点 **curr1** 的值作为所需答案。

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

// Function to find the XOR of two nodes
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
        cout << curr->data << " " ;

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
}
struct Node* NthNode(struct Node** head, int N)
{
    int count = 0;

    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;
    struct Node* curr1 = *head;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;
    struct Node* prev1 = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;
    struct Node* next1;

    while (count < N && curr != NULL) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        count++;
    }

    if (curr == NULL && count < N) {
       cout << "Wrong Input\n";
        return (uintptr_t)0;
    }
    else {
        while (curr != NULL) {

            // Forward traversal
            next = XOR(prev, curr->nxp);
            next1 = XOR(prev1, curr1->nxp);

            // Update prev
            prev = curr;
            prev1 = curr1;

            // Update curr
            curr = next;
            curr1 = next1;
        }
        cout << curr1->data << " ";
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

    NthNode(&head, 3);

    return (0);
}
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

// Function to find the XOR of two nodes
struct Node* XOR(struct Node* a,
                 struct Node* b)
{
    return (struct Node*)((uintptr_t)(a)
                          ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(
    struct Node** head, int value)
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
struct Node* NthNode(struct Node** head,
                     int N)
{
    int count = 0;

    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;
    struct Node* curr1 = *head;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;
    struct Node* prev1 = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;
    struct Node* next1;

    while (count < N && curr != NULL) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        count++;
    }

    if (curr == NULL && count < N) {
        printf("Wrong Input");
        return (uintptr_t)0;
    }
    else {
        while (curr != NULL) {

            // Forward traversal
            next = XOR(prev,
                       curr->nxp);
            next1 = XOR(prev1,
                        curr1->nxp);

            // Update prev
            prev = curr;
            prev1 = curr1;

            // Update curr
            curr = next;
            curr1 = next1;
        }
        printf("%d", curr1->data);
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

    NthNode(&head, 3);

    return (0);
}
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)