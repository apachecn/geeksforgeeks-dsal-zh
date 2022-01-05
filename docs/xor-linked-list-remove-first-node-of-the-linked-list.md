# 异或链表-移除链表的第一个节点

> 原文:[https://www . geesforgeks . org/xor-链表-移除-链表的第一个节点/](https://www.geeksforgeeks.org/xor-linked-list-remove-first-node-of-the-linked-list/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)，任务是移除异或链表的第一个节点。

**示例:**

> **输入:**XLL = 4<–>7<–>9<–>7
> T3】输出:7<–>9<–>7
> T6】解释:
> 删除 XOR 链表的第一个节点将 XLL 修改为 7<–>9<–>7
> 
> **输入:** XLL =空
> T3】输出:列表为空

**方法:**思路是将[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)的头节点更新为[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)的第二个节点，删除分配给第一个节点的内存。按照以下步骤解决问题:

*   检查[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)是否为空。如果发现是真的，则打印**“列表为空”**。
*   否则，将异或链表的头节点更新为链表的第二个节点。
*   从内存中删除第一个节点。

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

// Function to find the XOR
// of address two nodes
struct Node* XOR(struct Node* a,
                 struct Node* b)
{
    return (struct Node*)((uintptr_t)(a) ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at given position
struct Node* insert(struct Node** head,
                    int value)
{

    // Check If XOR linked list
    // is empty
    if (*head == NULL) {

        // Initialize a new Node
        struct Node* node
            = (struct Node*)malloc(sizeof(struct Node));

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

// Function to remove the first node form
// the given linked list
struct Node* delBeginning(struct Node** head)
{

    // If list is empty
    if (*head == NULL)
        printf("List Is Empty");
    else {

        // Store the node to be deleted
        struct Node* temp = *head;

        // Update the head pointer
        *head = XOR(NULL, temp->nxp);

        // When the linked list
        // contains only one node
        if (*head != NULL) {

            // Update head node address
            (*head)->nxp
                = XOR(NULL, XOR(temp,
                                (*head)->nxp));
        }

        free(temp);
    }
    return *head;
}

// Driver Code
int main()
{

    /* Create following XOR Linked List
    head-->40<-->30<-->20<-->10 */
    struct Node* head = NULL;
    insert(&head, 10);
    insert(&head, 20);
    insert(&head, 30);
    insert(&head, 40);

    // Delete the first node
    delBeginning(&head);

    /* Print the following XOR Linked List
    head-->30<-->20<-->10 */
    printList(&head);

    return (0);
}
```

**Output:**

```
30 20 10

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)