# 异或链表–在特定位置插入元素

> 原文:[https://www . geesforgeks . org/xor-link-list-insert-a-element-at-specific-position/](https://www.geeksforgeeks.org/xor-linked-list-insert-an-element-at-a-specific-position/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)和两个整数**位置**和**值**，任务是插入一个包含**值**的节点作为**异或链表**的位置<sup>第</sup>节点。

**示例**:

> **输入:**4<–>7<–>9<–>7，位置= 3，数值= 6
> **输出:**4<–>7<–>6<–>9<–>7
> **解释:**
> 在 3 <sup>rd</sup> 位置插入一个节点
> 
> **输入:**4<–>7<–>9<–>7，位置=6，值=6
> **输出:**无效位置
> **说明:**由于给定列表只包含 4 个元素，因此第 6 个位置是给定列表中的无效位置。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如**ctrl**来记录给定异或链表中遍历的节点数。
*   [遍历给定的异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)。对于异或链表的每个节点，检查当前节点的位置是否等于**位置**。如果发现为真，则在给定的异或链表中插入该节点。
*   否则，用 **1** 增加**控制**。
*   如果遍历了整个列表并且没有获得第<sup>个</sup>节点的位置，则打印**“无效位置”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include<bits/stdc++.h>
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
struct Node* XOR(struct Node* a,
                 struct Node* b)
{
    return (struct Node*)((uintptr_t)(a)^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(struct Node** head,
                    int value, int position)
{
    // If XOR linked list is empty
    if (*head == NULL) {

        // If given position
        // is equal to 1
        if (position == 1) {

            // Initialize a new Node
            struct Node* node
                = new Node();

            // Stores data value in
            // the node
            node->data = value;

            // Stores XOR of previous
            // and next pointer
            node->nxp = XOR(NULL, NULL);

            // Update pointer of head node
            *head = node;
        }

        // If required position was not found
        else {
            cout << "Invalid Position\n";
        }
    }

    // If the XOR linked list
    // is not empty
    else {

        // Stores position of a node
        // in the XOR linked list
        int Pos = 1;

        // Stores the address
        // of current node
        struct Node* curr = *head;

        // Stores the address
        // of previous node
        struct Node* prev = NULL;

        // Stores the XOR of next
        // node and previous node
        struct Node* next
            = XOR(prev, curr->nxp);

        // Traverse the XOR linked list
        while (next != NULL && Pos < position - 1) {

            // Update prev
            prev = curr;

            // Update curr
            curr = next;

            // Update next
            next = XOR(prev, curr->nxp);

            // Update Pos
            Pos++;
        }

        // If the position of the current
        // node is equal to the given position
        if (Pos == position - 1) {

            // Initialize a new Node
            struct Node* node
                = new Node();

            // Stores pointer to previous Node
            // as (prev ^ next ^ next) = prev
            struct Node* temp
                = XOR(curr->nxp, next);

            // Stores XOR of prev and new node
            curr->nxp = XOR(temp, node);

            // Connecting new node with next
            if (next != NULL) {

                // Update pointer of next
                next->nxp = XOR(node,
                                XOR(next->nxp, curr));
            }

            // Connect node with curr and
            // next curr<--node-->next
            node->nxp = XOR(curr, next);
            node->data = value;
        }

        // Insertion node at beginning
        else if (position == 1) {

            // Initialize a new Node
            struct Node* node
                = new Node();

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
        else {
            cout << "Invalid Position\n";
        }
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

// Driver Code
int main()
{
    /* Create following XOR Linked List
    head-->20<-->40<-->10<-->30 */
    struct Node* head = NULL;
    insert(&head, 10, 1);
    insert(&head, 20, 1);
    insert(&head, 30, 3);
    insert(&head, 40, 2);

    // Print the new list
    printList(&head);

    return 0;
}
```

## C

```
// C++ program to implement
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
                    int value, int position)
{
    // If XOR linked list is empty
    if (*head == NULL) {

        // If given position
        // is equal to 1
        if (position == 1) {

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

        // If required position was not found
        else {
            printf("Invalid Position\n");
        }
    }

    // If the XOR linked list
    // is not empty
    else {

        // Stores position of a node
        // in the XOR linked list
        int Pos = 1;

        // Stores the address
        // of current node
        struct Node* curr = *head;

        // Stores the address
        // of previous node
        struct Node* prev = NULL;

        // Stores the XOR of next
        // node and previous node
        struct Node* next
            = XOR(prev, curr->nxp);

        // Traverse the XOR linked list
        while (next != NULL && Pos < position - 1) {

            // Update prev
            prev = curr;

            // Update curr
            curr = next;

            // Update next
            next = XOR(prev, curr->nxp);

            // Update Pos
            Pos++;
        }

        // If the position of the current
        // node is equal to the given position
        if (Pos == position - 1) {

            // Initialize a new Node
            struct Node* node
                = (struct Node*)malloc(
                    sizeof(struct Node));

            // Stores pointer to previous Node
            // as (prev ^ next ^ next) = prev
            struct Node* temp
                = XOR(curr->nxp, next);

            // Stores XOR of prev and new node
            curr->nxp = XOR(temp, node);

            // Connecting new node with next
            if (next != NULL) {

                // Update pointer of next
                next->nxp = XOR(node,
                                XOR(next->nxp, curr));
            }

            // Connect node with curr and
            // next curr<--node-->next
            node->nxp = XOR(curr, next);
            node->data = value;
        }

        // Insertion node at beginning
        else if (position == 1) {

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
        else {
            printf("Invalid Position\n");
        }
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

// Driver Code
int main()
{
    /* Create following XOR Linked List
    head-->20<-->40<-->10<-->30 */
    struct Node* head = NULL;
    insert(&head, 10, 1);
    insert(&head, 20, 1);
    insert(&head, 30, 3);
    insert(&head, 40, 2);

    // Print the new list
    printList(&head);

    return (0);
}
```

**Output:** 

```
20 40 10 30
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)