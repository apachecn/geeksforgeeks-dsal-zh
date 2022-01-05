# 异或链表–列表反转

> 原文:[https://www . geesforgeks . org/xor-链表-链表反转/](https://www.geeksforgeeks.org/xor-linked-list-reversal-of-a-list/)

给定一个[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)，任务是反转异或链表。

**示例:**

> **输入:**4<–>7<–>9<–>7
> **输出:**7<–>9<–>7<–>4
> **解释:**
> 反转链表将异或链表修改为 7<–>9<–>7【T25
> 
> **输入:**2<->5<->7<->4
> **输出:**4<->7<->5<->2
> **解释:**
> 反转链表将异或链表修改为 4 < - > 7 < - > 5 <

**方法:** [XOR 链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)由单个指针组成，这是在两个方向遍历 XOR 链表所需的唯一指针。所以解决这个问题的思路就是只把 XOR 链表的**最后一个节点**作为它的**头节点**。按照以下步骤解决问题:

1.  初始化一个指针变量，比如 **curr** ，指向当前被遍历的节点。
2.  将**当前磁头**指针存储在**当前**变量中。
3.  如果 **curr** 等于 **NULL** ，则返回 **NULL** 。
4.  否则，遍历到最后一个节点，使其成为[异或链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)的**头**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Structure of a node
// in XOR linked list
struct Node
{

    // Stores data value
    // of a node
    int data;

    // Stores XOR of previous
    // pointer and next pointer
    Node* nxp;
};

// Function to find the XOR of two nodes
Node* XOR(Node* a, Node* b)
{
    return (Node*)((uintptr_t)(a) ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at beginning position
Node* insert(Node** head, int value)
{

    // If XOR linked list is empty
    if (*head == NULL)
    {

        // Initialize a new Node
        Node* node
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

    // If the XOR linked list
    // is not empty
    else
    {

        // Stores the address
        // of current node
        Node* curr = *head;

        // Stores the address
        // of previous node
        Node* prev = NULL;

        // Initialize a new Node
        Node* node
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
void printList(Node** head)
{

    // Stores XOR pointer
    // in current node
    Node* curr = *head;

    // Stores XOR pointer of
    // in previous Node
    Node* prev = NULL;

    // Stores XOR pointer of
    // in next node
    Node* next;

    // Traverse XOR linked list
    while (curr != NULL)
    {

        // Print current node
        cout<<curr->data<<" ";

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
    cout << endl;
}

// Function to reverse the XOR linked list
Node* reverse(Node** head)
{

    // Stores XOR pointer
    // in current node
    Node* curr = *head;
    if (curr == NULL)
        return NULL;
    else
    {

        // Stores XOR pointer of
        // in previous Node
        Node* prev = NULL;

        // Stores XOR pointer of
        // in next node
        Node* next;
        while (XOR(prev, curr->nxp) != NULL)
        {

            // Forward traversal
            next = XOR(prev, curr->nxp);

            // Update prev
            prev = curr;

            // Update curr
            curr = next;
        }

        // Update the head pointer
        *head = curr;
        return *head;
    }
}

// Driver Code
int main()
{
    /* Create following XOR Linked List
    head-->40<-->30<-->20<-->10 */
    Node* head = NULL;
    insert(&head, 10);
    insert(&head, 20);
    insert(&head, 30);
    insert(&head, 40);

    /* Reverse the XOR Linked List to give
    head-->10<-->20<-->30<-->40 */
    cout << "XOR linked list: ";
    printList(&head);
    reverse(&head);
    cout << "Reversed XOR linked list: ";
    printList(&head);

    return 0;
}

// This code is contributed by rutvik_56.
```

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
    return (struct Node*)((uintptr_t)(a) ^ (uintptr_t)(b));
}

// Function to insert a node with
// given value at beginning position
struct Node* insert(struct Node** head, int value)
{

    // If XOR linked list is empty
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
            = (struct Node*)malloc(sizeof(struct Node));

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
        printf("%d ", curr->data);

        // Forward traversal
        next = XOR(prev, curr->nxp);

        // Update prev
        prev = curr;

        // Update curr
        curr = next;
    }
    printf("\n");
}

// Function to reverse the XOR linked list
struct Node* reverse(struct Node** head)
{

    // Stores XOR pointer
    // in current node
    struct Node* curr = *head;
    if (curr == NULL)
        return NULL;
    else {

        // Stores XOR pointer of
        // in previous Node
        struct Node* prev = NULL;

        // Stores XOR pointer of
        // in next node
        struct Node* next;
        while (XOR(prev, curr->nxp) != NULL) {

            // Forward traversal
            next = XOR(prev, curr->nxp);

            // Update prev
            prev = curr;

            // Update curr
            curr = next;
        }

        // Update the head pointer
        *head = curr;
        return *head;
    }
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

    /* Reverse the XOR Linked List to give
    head-->10<-->20<-->30<-->40 */
    printf("XOR linked list: ");
    printList(&head);
    reverse(&head);
    printf("Reversed XOR linked list: ");
    printList(&head);

    return (0);
}
```

**Output:** 

```
XOR linked list: 40 30 20 10 
Reversed XOR linked list: 10 20 30 40
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)