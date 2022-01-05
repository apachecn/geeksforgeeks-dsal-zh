# 异或链表:删除链表的最后一个节点

> 原文:[https://www . geesforgeks . org/xor-链表-移除-链表的最后一个节点/](https://www.geeksforgeeks.org/xor-linked-list-remove-last-node-of-the-linked-list/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)，任务是**删除[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)的**端**的节点**。

**示例:**

> **输入:**4<–>7<–>9<–>7
> T3】输出:4<–>7<–>9
> T6】说明:从末尾删除一个节点会将给定的异或链表修改为 4<–>7<–>9
> 
> **输入:** 10
> **输出:**列表为空
> **说明:**删除 XOR 链表中唯一存在的节点后，列表变为空。

**方法:**解决这个问题的思路是[遍历 XOR 链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)直到到达最后一个节点，更新其前一个节点的地址。按照以下步骤解决问题:

*   如果异或链表为空，则打印“**链表为空**”。
*   **遍历异或链表**直到到达链表的最后一个节点。
*   更新其**前一节点**的地址。
*   [**从记忆**](https://www.geeksforgeeks.org/g-fact-30/)中删除**最后一个节点**。
*   如果删除最后一个节点后列表变为空，则打印**“列表为空”**。否则，打印链表的剩余节点。

下面是上述方法的实现:

## C

```
// C program for the above approach

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
struct Node* XOR(struct Node* a, struct Node* b)
{
    return (struct Node*)((uintptr_t)(a)
                          ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(struct Node** head, int value)
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

// Function to delete the last node
// present in the XOR Linked List
struct Node* delEnd(struct Node** head)
{
    // Base condition
    if (*head == NULL)
        printf("List is empty");
    else {

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
        while (XOR(curr->nxp, prev) != NULL) {

            // Forward traversal
            next = XOR(prev, curr->nxp);

            // Update prev
            prev = curr;

            // Update curr
            curr = next;
        }
        // If the Linked List contains more than 1 node
        if (prev != NULL)
            prev->nxp = XOR(XOR(prev->nxp, curr), NULL);

        // Otherwise
        else
            *head = NULL;

        // Delete the last node from memory
        free(curr);
    }

    // Returns head of new linked list
    return *head;
}

// Driver Code
int main()
{

    /* Create the XOR Linked List
    head-->40<-->30<-->20<-->10 */
    struct Node* head = NULL;
    insert(&head, 10);
    insert(&head, 20);
    insert(&head, 30);
    insert(&head, 40);

    delEnd(&head);

    // If the list had a single node
    if (head == NULL)
        printf("List is empty");
    else
        // Print the list after deletion
        printList(&head);

    return (0);
}
```

**Output:**

```
40 30 20

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)