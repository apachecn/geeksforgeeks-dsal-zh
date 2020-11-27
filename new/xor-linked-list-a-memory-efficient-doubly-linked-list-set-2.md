# XOR 链表–内存有效的双链表 | 系列 2

> 原文：[https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)

在[的上一篇文章](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)中，我们讨论了如何在每个节点的地址字段中仅使用一个空格来创建双向链接。 在这篇文章中，我们将讨论内存高效的双向链表的实现。 我们将主要讨论以下两个简单功能。

1.  在开始处插入新节点的功能。

2.  向前遍历列表的功能。

在以下代码中， `insert()`函数在开始处插入一个新节点。 我们需要更改链表的头指针，这就是为什么要使用双指针的原因（请参见[此](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)）。 让我们首先再次讨论[以前的帖子](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)中讨论过的几件事。 我们将下一个节点和上一个节点的 XOR 与每个节点存储在一起，我们将其称为`npx`，这是每个节点唯一的地址成员。 当我们在开始处插入新节点时，新节点的`npx`将始终为`NULL`与当前头的 XOR。 并且当前头的`npx`必须更改为新节点与当前头旁边的节点的 XOR。

`printList()`向前遍历列表。 它从每个节点打印数据值。 要遍历列表，我们需要在每个点都获得指向下一个节点的指针。 通过跟踪当前节点和上一个节点，我们可以获得下一个节点的地址。 如果对`curr->npx`和`prev`进行 XOR，我们将获得下一个节点的地址。

## C++

```cpp

/* C++ Implementation of Memory 
efficient Doubly Linked List */
#include <bits/stdc++.h>
#include <cinttypes> 
using namespace std;

// Node structure of a memory 
// efficient doubly linked list 
class Node 
{ 
    public:
    int data; 
    Node* npx; /* XOR of next and previous node */
}; 

/* returns XORed value of the node addresses */
Node* XOR (Node *a, Node *b) 
{ 
    return reinterpret_cast<Node *>(
      reinterpret_cast<uintptr_t>(a) ^ 
      reinterpret_cast<uintptr_t>(b)); 
} 

/* Insert a node at the beginning of the 
XORed linked list and makes the newly 
inserted node as head */
void insert(Node **head_ref, int data) 
{ 
    // Allocate memory for new node 
    Node *new_node = new Node(); 
    new_node->data = data; 

    /* Since new node is being inserted at the 
    beginning, npx of new node will always be 
    XOR of current head and NULL */
    new_node->npx = *head_ref; 

    /* If linked list is not empty, then npx of 
    current head node will be XOR of new node 
    and node next to current head */
    if (*head_ref != NULL) 
    { 
        // *(head_ref)->npx is XOR of NULL and next. 
        // So if we do XOR of it with NULL, we get next 
        (*head_ref)->npx = XOR(new_node, (*head_ref)->npx); 
    } 

    // Change head 
    *head_ref = new_node; 
} 

// prints contents of doubly linked 
// list in forward direction 
void printList (Node *head) 
{ 
    Node *curr = head; 
    Node *prev = NULL; 
    Node *next; 

    cout << "Following are the nodes of Linked List: \n"; 

    while (curr != NULL) 
    { 
        // print current node 
        cout<<curr->data<<" "; 

        // get address of next node: curr->npx is 
        // next^prev, so curr->npx^prev will be 
        // next^prev^prev which is next 
        next = XOR (prev, curr->npx); 

        // update prev and curr for next iteration 
        prev = curr; 
        curr = next; 
    } 
} 

// Driver code 
int main () 
{ 
    /* Create following Doubly Linked List 
    head-->40<-->30<-->20<-->10 */
    Node *head = NULL; 
    insert(&head, 10); 
    insert(&head, 20); 
    insert(&head, 30); 
    insert(&head, 40); 

    // print the created list 
    printList (head); 

    return (0); 
} 

// This code is contributed by rathbhupendra

```

## C

```c

/* C Implementation of Memory 
   efficient Doubly Linked List */
#include <stdio.h>
#include <stdlib.h>
#include <inttypes.h>

// Node structure of a memory 
// efficient doubly linked list
struct Node
{
    int data;
    struct Node* npx; /* XOR of next and previous node */
};

/* returns XORed value of the node addresses */
struct Node* XOR (struct Node *a, struct Node *b)
{
    return (struct Node*) ((uintptr_t) (a) ^ (uintptr_t) (b));
}

/* Insert a node at the beginning of the 
   XORed linked list and makes the newly
   inserted node as head */
void insert(struct Node **head_ref, int data)
{
    // Allocate memory for new node
    struct Node *new_node = (struct Node *) malloc (sizeof (struct Node) );
    new_node->data = data;

    /* Since new node is being inserted at the 
       beginning, npx of new node will always be
       XOR of current head and NULL */
    new_node->npx = *head_ref;

    /* If linked list is not empty, then npx of 
       current head node will be XOR of new node
       and node next to current head */
    if (*head_ref != NULL)
    {
        // *(head_ref)->npx is XOR of NULL and next. 
        // So if we do XOR of it with NULL, we get next
        (*head_ref)->npx = XOR(new_node, (*head_ref)->npx);
    }

    // Change head
    *head_ref = new_node;
}

// prints contents of doubly linked
// list in forward direction
void printList (struct Node *head)
{
    struct Node *curr = head;
    struct Node *prev = NULL;
    struct Node *next;

    printf ("Following are the nodes of Linked List: \n");

    while (curr != NULL)
    {
        // print current node
        printf ("%d ", curr->data);

        // get address of next node: curr->npx is 
        // next^prev, so curr->npx^prev will be
        // next^prev^prev which is next
        next = XOR (prev, curr->npx);

        // update prev and curr for next iteration
        prev = curr;
        curr = next;
    }
}

// Driver program to test above functions
int main ()
{
    /* Create following Doubly Linked List
    head-->40<-->30<-->20<-->10 */
    struct Node *head = NULL;
    insert(&head, 10);
    insert(&head, 20);
    insert(&head, 30);
    insert(&head, 40);

    // print the created list
    printList (head);

    return (0);
}

```

**Output**

```
Following are the nodes of Linked List: 
40 30 20 10 
```

请注意，C/C++ 标准未定义指针的 XOR。 因此，上述实现可能无法在所有平台上都有效。

如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论

