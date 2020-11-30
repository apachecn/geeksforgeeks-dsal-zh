# 从循环双单链表

> 原文：[https://www.geeksforgeeks.org/remove-all-even-parity-nodes-from-a-doubly-and-circular-singly-linked-list/](https://www.geeksforgeeks.org/remove-all-even-parity-nodes-from-a-doubly-and-circular-singly-linked-list/)

中删除所有偶数奇偶校验节点

给定一个[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)和[循环单链表](https://www.geeksforgeeks.org/circular-linked-list/)包含`N`个节点，任务是从每个列表中删除所有奇偶校验为偶数的元素的节点 。

**示例**：

> **输入**：`CLL = 9 -> 11 -> 34 -> 6 -> 13 -> 21`
>
> **输出**：`11 -> 13 -> 21`
>
> **说明**：
>
> 循环单链表包含：
>
> `11 -> 1011`，奇偶校验为 3
>
> `9 -> 1001`，奇偶校验为 2
>
> `34 -> 100010`，奇偶校验为 2
>
> `6 -> 110`，奇偶校验为 2
>
> `13 -> 1101`，奇偶校验为 3
>
> `21 -> 10101`，奇偶校验为 3
>
> 这里，包含 9、34 和 6 的节点的奇偶校验为偶数。
>
> 因此，这些节点已删除。
> 
> **输入**：`DLL = 18 <=> 15 <=> 8 <=> 9 <=> 14`
>
> **输出**：`8 <=> 14`
>
> **说明**：
>
> 链表包含：
>
> `18 -> 10010`，奇偶校验为 2
>
> `15 -> 1111`，奇偶校验为 4
>
> `8 -> 1000`，奇偶校验为 1
>
> `9 -> 1001`，奇偶校验为 2
>
> `14 -> 1110`，奇偶校验为 3
>
> 在这里，包含 18、15 和 9 的节点的奇偶校验是偶数。
>
> 因此，这些节点已删除。

**方法**：

一种简单的方法是依次遍历列表中的节点，并首先针对每个节点，通过遍历每个位找到该节点中存在的值的奇偶校验，然后最后将其删除 奇偶校验的节点。

### 双链表

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to remove all
// the Even Parity Nodes from a
// doubly linked list

#include <bits/stdc++.h>

using namespace std;

// Node of the doubly linked list
struct Node {
    int data;
    Node *prev, *next;
};

// Function to insert a node at the beginning
// of the Doubly Linked List
void push(Node** head_ref, int new_data)
{
    // Allocate the node
    Node* new_node
        = (Node*)malloc(sizeof(struct Node));

    // Insert the data
    new_node->data = new_data;

    // Since we are adding at the beginning,
    // prev is always NULL
    new_node->prev = NULL;

    // Link the old list off the new node
    new_node->next = (*head_ref);

    // Change the prev of
    // head node to new node
    if ((*head_ref) != NULL)
        (*head_ref)->prev = new_node;

    // Move the head to point
    // to the new node
    (*head_ref) = new_node;
}

// Function that returns true if count
// of set bits in x is even
bool isEvenParity(int x)
{
    // parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to delete a node
// in a Doubly Linked List.
// head_ref --> pointer to head node pointer.
// del --> pointer to node to be deleted
void deleteNode(Node** head_ref, Node* del)
{
    // Base case
    if (*head_ref == NULL || del == NULL)
        return;

    // If the node to be
    // deleted is head node
    if (*head_ref == del)
        *head_ref = del->next;

    // Change next only if node to be
    // deleted is not the last node
    if (del->next != NULL)
        del->next->prev = del->prev;

    // Change prev only if node to be
    // deleted is not the first node
    if (del->prev != NULL)
        del->prev->next = del->next;

    // Finally, free the memory
    // occupied by del
    free(del);

    return;
}

// Function to to remove all
// the Even Parity Nodes from a
// doubly linked list
void deleteEvenParityNodes(
    Node** head_ref)
{
    Node* ptr = *head_ref;
    Node* next;

    // Iterating through
    // the linked list
    while (ptr != NULL) {
        next = ptr->next;

        // If node's data's parity
        // is even
        if (isEvenParity(ptr->data))
            deleteNode(head_ref, ptr);

        ptr = next;
    }
}

// Function to print nodes in a
// given doubly linked list
void printList(Node* head)
{
    if (head == NULL) {
        cout << "Empty list\n";
        return;
    }

    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
}

// Driver Code
int main()
{

    Node* head = NULL;

    // Create the doubly linked list
    // 18 <-> 15 <-> 8 <-> 9 <-> 14
    push(&head, 14);
    push(&head, 9);
    push(&head, 8);
    push(&head, 15);
    push(&head, 18);

    // Uncomment to view the list
    // cout << "Original List: ";
    // printList(head);

    deleteEvenParityNodes(&head);

    // Modified List
    printList(head);
}

```

**输出**： 

```
8 14

```

### 循环单链表

下面是上述方法的实现：

## C++

```cpp

// C++ program to remove all
// the Even Parity Nodes from a
// circular singly linked list

#include <bits/stdc++.h>
using namespace std;

// Structure for a node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a node at the beginning
// of a Circular linked list
void push(struct Node** head_ref, int data)
{
    // Create a new node
    // and make head as next
    // of it.
    struct Node* ptr1
        = (struct Node*)malloc(
            sizeof(struct Node));

    struct Node* temp = *head_ref;
    ptr1->data = data;
    ptr1->next = *head_ref;

    // If linked list is not NULL then
    // set the next of last node
    if (*head_ref != NULL) {

        // Find the node before head
        // and update next of it.
        while (temp->next != *head_ref)
            temp = temp->next;

        temp->next = ptr1;
    }
    else

        // Point for the first node
        ptr1->next = ptr1;

    *head_ref = ptr1;
}

// Function to delete the node from a
// Circular Linked list
void deleteNode(
    Node*& head_ref, Node* del)
{
    // If node to be deleted is head node
    if (head_ref == del)
        head_ref = del->next;

    struct Node* temp = head_ref;

    // Traverse list till not found
    // delete node
    while (temp->next != del) {
        temp = temp->next;
    }

    // Copy the address of the node
    temp->next = del->next;

    // Finally, free the memory
    // occupied by del
    free(del);

    return;
}

// Function that returns true if count
// of set bits in x is even
bool isEvenParity(int x)
{
    // parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to delete all
// the Even Parity Nodes
// from the singly circular linked list
void deleteEvenParityNodes(Node*& head)
{
    if (head == NULL)
        return;

    if (head == head->next) {
        if (isEvenParity(head->data))
            head = NULL;
        return;
    }

    struct Node* ptr = head;

    struct Node* next;

    // Traverse the list till the end
    do {
        next = ptr->next;

        // If the node's data has even parity,
        // delete node 'ptr'
        if (isEvenParity(ptr->data))
            deleteNode(head, ptr);

        // Point to the next node
        ptr = next;

    } while (ptr != head);

    if (head == head->next) {
        if (isEvenParity(head->data))
            head = NULL;
        return;
    }
}

// Function to print nodes in a
// given Circular linked list
void printList(struct Node* head)
{
    if (head == NULL) {
        cout << "Empty List\n";
        return;
    }

    struct Node* temp = head;
    if (head != NULL) {
        do {
            printf("%d ", temp->data);
            temp = temp->next;
        } while (temp != head);
    }
}

// Driver code
int main()
{
    // Initialize lists as empty
    struct Node* head = NULL;

    // Created linked list will be
    // 11->9->34->6->13->21
    push(&head, 21);
    push(&head, 13);
    push(&head, 6);
    push(&head, 34);
    push(&head, 9);
    push(&head, 11);

    deleteEvenParityNodes(head);

    printList(head);

    return 0;
}

```

## Java

```java

// Java program to remove all
// the Even Parity Nodes from a
// circular singly linked list
class GFG{

// Structure for a node
static class Node 
{
    int data;
    Node next;
};

// Function to insert a node at
// the beginning of a Circular
// linked list
static Node push(Node head_ref, int data)
{

    // Create a new node
    // and make head as next
    // of it.
    Node ptr1 = new Node();

    Node temp = head_ref;
    ptr1.data = data;
    ptr1.next = head_ref;

    // If linked list is not null then
    // set the next of last node
    if (head_ref != null)
    {

        // Find the node before head
        // and update next of it.
        while (temp.next != head_ref)
            temp = temp.next;

        temp.next = ptr1;
    }
    else

        // Point for the first node
        ptr1.next = ptr1;

    head_ref = ptr1;
    return head_ref;
}

// Function to delete the node 
// from a Circular Linked list
static void deleteNode(Node head_ref,
                       Node del)
{

    // If node to be deleted is
    // head node
    if (head_ref == del)
        head_ref = del.next;

    Node temp = head_ref;

    // Traverse list till not found
    // delete node
    while (temp.next != del)
    {
        temp = temp.next;
    }

    // Copy the address of the node
    temp.next = del.next;

    // Finally, free the memory
    // occupied by del
    System.gc();

    return;
}

// Function that returns true if count
// of set bits in x is even
static boolean isEvenParity(int x)
{

    // Parity will store the
    // count of set bits
    int parity = 0;

    while (x != 0)
    {
        if ((x & 1) != 0)
            parity++;

        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to delete all the 
// Even Parity Nodes from the
// singly circular linked list
static void deleteEvenParityNodes(Node head)
{
    if (head == null)
        return;

    if (head == head.next) 
    {
        if (isEvenParity(head.data))
            head = null;

        return;
    }

    Node ptr = head;
    Node next;

    // Traverse the list till the end
    do
    {
        next = ptr.next;

        // If the node's data has 
        // even parity, delete node 'ptr'
        if (isEvenParity(ptr.data))
            deleteNode(head, ptr);

        // Point to the next node
        ptr = next;

    } while (ptr != head);

    if (head == head.next)
    {
        if (isEvenParity(head.data))
            head = null;

        return;
    }
}

// Function to print nodes in a
// given Circular linked list
static void printList(Node head)
{
    if (head == null)
    {
        System.out.print("Empty List\n");
        return;
    }

    Node temp = head;
    if (head != null)
    {
        do
        {
            System.out.printf("%d ", temp.data);
            temp = temp.next;
        } while (temp != head);
    }
}

// Driver code
public static void main(String[] args)
{

    // Initialize lists as empty
    Node head = null;

    // Created linked list will be
    // 11.9.34.6.13.21
    head = push(head, 21);
    head = push(head, 13);
    head = push(head, 6);
    head = push(head, 34);
    head = push(head, 9);
    head = push(head, 11);

    deleteEvenParityNodes(head);

    printList(head);
}
}

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program to remove all
// the Even Parity Nodes from a
// circular singly linked list
using System;
class GFG{

// Structure for a node
public class Node 
{
  public int data;
  public Node next;
};

// Function to insert a node at
// the beginning of a Circular
// linked list
static Node push(Node head_ref, 
                 int data)
{    
  // Create a new node
  // and make head as next
  // of it.
  Node ptr1 = new Node();

  Node temp = head_ref;
  ptr1.data = data;
  ptr1.next = head_ref;

  // If linked list is not 
  // null then set the next 
  // of last node
  if (head_ref != null)
  {
    // Find the node before head
    // and update next of it.
    while (temp.next != head_ref)
      temp = temp.next;

    temp.next = ptr1;
  }
  else

    // Point for the first node
    ptr1.next = ptr1;

  head_ref = ptr1;
  return head_ref;
}

// Function to delete the node 
// from a Circular Linked list
static void deleteNode(Node head_ref,
                       Node del)
{    
  // If node to be deleted is
  // head node
  if (head_ref == del)
    head_ref = del.next;

  Node temp = head_ref;

  // Traverse list till not 
  // found delete node
  while (temp.next != del)
  {
    temp = temp.next;
  }

  // Copy the address of 
  // the node
  temp.next = del.next;

  return;
}

// Function that returns true 
// if count of set bits in x 
// is even
static bool isEvenParity(int x)
{
  // Parity will store the
  // count of set bits
  int parity = 0;

  while (x != 0)
  {
    if ((x & 1) != 0)
      parity++;

    x = x >> 1;
  }

  if (parity % 2 == 0)
    return true;
  else
    return false;
}

// Function to delete all the 
// Even Parity Nodes from the
// singly circular linked list
static void deleteEvenParityNodes(Node head)
{
  if (head == null)
    return;

  if (head == head.next) 
  {
    if (isEvenParity(head.data))
      head = null;

    return;
  }

  Node ptr = head;
  Node next;

  // Traverse the list 
  // till the end
  do
  {
    next = ptr.next;

    // If the node's data has 
    // even parity, delete node 'ptr'
    if (isEvenParity(ptr.data))
      deleteNode(head, ptr);

    // Point to the next node
    ptr = next;

  } while (ptr != head);

  if (head == head.next)
  {
    if (isEvenParity(head.data))
      head = null;

    return;
  }
}

// Function to print nodes in a
// given Circular linked list
static void printList(Node head)
{
  if (head == null)
  {
    Console.Write("Empty List\n");
    return;
  }

  Node temp = head;
  if (head != null)
  {
    do
    {
      Console.Write(temp.data + " ");
      temp = temp.next;
    } while (temp != head);
  }
}

// Driver code
public static void Main(String[] args)
{    
  // Initialize lists as empty
  Node head = null;

  // Created linked list will be
  // 11.9.34.6.13.21
  head = push(head, 21);
  head = push(head, 13);
  head = push(head, 6);
  head = push(head, 34);
  head = push(head, 9);
  head = push(head, 11);

  deleteEvenParityNodes(head);
  printList(head);
}
}

// This code is contributed by Rajput-Ji

```

**输出**： 

```
11 13 21

```

**时间复杂度**：`O(K * N)`，其中`N`是链​​表的大小，`K`是链表中最大数目的位数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。