# 异或链表–找到中间节点

> 原文:[https://www . geesforgeks . org/xor-链表-查找中间节点/](https://www.geeksforgeeks.org/xor-linked-list-find-the-middle-node/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)，任务是找到给定 [**异或链表**](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/) 的**中间节点**。

**示例:**

> **输入:**4–>7–>5
> **输出:** 7
> **说明:**
> 给定异或列表的中间节点为 7。
> 
> **输入:**4–>7–>5–>1
> **输出:** 7 5
> **说明:**
> 偶数节点的异或链表中间两个节点是 7 和 5。

**方法:**按照以下步骤解决问题:

*   遍历链表的第**(长度/ 2)** <sup>节点。</sup>
*   如果发现节点数为奇数，则打印**(长度+ 1) / 2 <sup>第</sup>个**节点作为唯一中间节点。
*   如果发现节点数为偶数，则打印**长度/ 2 <sup>第</sup>T3】节点和**(长度/ 2) + 1 <sup>第</sup>T7】节点作为中间节点。****

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

// Function to print the middle node
int printMiddle(struct Node** head, int len)
{
    int count = 0;

    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;

    int middle = (int)len / 2;

    // Traverse XOR linked list
    while (count != middle) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        count++;
    }

    // If the length of the
    // linked list is odd
    if (len & 1) {
        cout << curr->data << " ";
    }

    // If the length of the
    // linked list is even
    else {
        cout << prev->data << " " << curr->data << " ";
    }
}

// Driver Code
int main()
{
    /* Create following XOR Linked List
    head --> 4 –> 7 –> 5 */
    struct Node* head = NULL;
    insert(&head, 4);
    insert(&head, 7);
    insert(&head, 5);

    printMiddle(&head, 3);

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
        curr->nxp = XOR(
            node, XOR(NULL, curr->nxp));

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

// Function to print the middle node
int printMiddle(struct Node** head, int len)
{
    int count = 0;

    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;

    // Stores XOR pointer of
    // in previous Node
    struct Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    struct Node* next;

    int middle = (int)len / 2;

    // Traverse XOR linked list
    while (count != middle) {

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;

        count++;
    }

    // If the length of the
    // linked list is odd
    if (len & 1) {
        printf("%d", curr->data);
    }

    // If the length of the
    // linked list is even
    else {
        printf("%d %d", prev->data,
               curr->data);
    }
}

// Driver Code
int main()
{
    /* Create following XOR Linked List
    head --> 4 –> 7 –> 5 */
    struct Node* head = NULL;
    insert(&head, 4);
    insert(&head, 7);
    insert(&head, 5);

    printMiddle(&head, 3);

    return (0);

}
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)