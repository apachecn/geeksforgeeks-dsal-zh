# 通过更改链接

> 原文：[https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/)

成对链表的成对交换元素

给定一个单链表，编写一个函数以成对交换元素。 例如，如果链表是 1-> 2-> 3-> 4-> 5-> 6-> 7，则函数应将其更改为 2-> 1-> 4-> 3-> 6-> 5 -> 7，并且如果链表是 1-> 2-> 3-> 4-> 5-> 6，则该函数应将其更改为 2-> 1-> 4-> 3-> 6-> 5

在中已经讨论了这个问题。 那里提供的解决方案交换节点数据。 如果数据包含许多字段，将有许多交换操作。 因此，通常更改链接是一个更好的主意。 以下是一个 C 实现，它更改了链接而不是交换数据。

## C++

```cpp

/* This program swaps the nodes of 
linked list rather than swapping the 
field from the nodes. 
Imagine a case where a node contains
many fields, there will be plenty 
of unnecessary swap calls. */

#include <bits/stdc++.h>
using namespace std;

/* A linked list node */
class node {
public:
    int data;
    node* next;
};

/* Function to pairwise swap elements
of a linked list. It returns head of
the modified list, so return value 
of this node must be assigned */
node* pairWiseSwap(node* head)
{
    // If linked list is empty or 
    // there is only one node in list
    if (head == NULL || head->next == NULL)
        return head;

    // Initialize previous and current pointers
    node* prev = head;
    node* curr = head->next;

    head = curr; // Change head before proceeeding

    // Traverse the list
    while (true) {
        node* next = curr->next;
        curr->next = prev; // Change next of
        // current as previous node

        // If next NULL or next is the last node
        if (next == NULL || next->next == NULL) {
            prev->next = next;
            break;
        }

        // Change next of previous to next next
        prev->next = next->next;

        // Update previous and curr
        prev = next;
        curr = prev->next;
    }
    return head;
}

/* Function to add a node at 
the begining of Linked List */
void push(node** head_ref, int new_data)
{
    /* allocate node */
    node* new_node = new node();

    /* put in the data */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes 
in a given linked list */
void printList(node* node)
{
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
}

/* Driver code */
int main()
{
    node* start = NULL;

    /* The constructed linked list is: 
    1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    cout << "Linked list before "
      << "calling pairWiseSwap() ";
    printList(start);

    start = pairWiseSwap(start); // NOTE THIS CHANGE

    cout << "\nLinked list after calling"
      << "pairWiseSwap() ";
    printList(start);

    return 0;
}

// This code is contributed by Manoj N

```

## C

```c

/* This program swaps the nodes of linked list rather than swapping the
field from the nodes.
Imagine a case where a node contains many fields, there will be plenty
of unnecessary swap calls. */

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

/* A linked list node */
struct Node {
    int data;
    struct Node* next;
};

/* Function to pairwise swap elements of a linked list */
void pairWiseSwap(struct Node** head)
{
    // If linked list is empty or there is only one node in list
    if (*head == NULL || (*head)->next == NULL)
        return;

    // Initialize previous and current pointers
    struct Node* prev = *head;
    struct Node* curr = (*head)->next;

    *head = curr; // Change head before proceeeding

    // Traverse the list
    while (true) {
        struct Node* next = curr->next;
        curr->next = prev; // Change next of current as previous node

        // If next NULL or next is the last node
        if (next == NULL || next->next == NULL) {
            prev->next = next;
            break;
        }

        // Change next of previous to next next
        prev->next = next->next;

        // Update previous and curr
        prev = next;
        curr = prev->next;
    }
}

/* Function to add a node at the begining of Linked List */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    /* put in the data  */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in a given linked list */
void printList(struct Node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

/* Druver program to test above function */
int main()
{
    struct Node* start = NULL;

    /* The constructed linked list is:
     1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    printf("\n Linked list before calling  pairWiseSwap() ");
    printList(start);

    pairWiseSwap(&start);

    printf("\n Linked list after calling  pairWiseSwap() ");
    printList(start);

    getchar();
    return 0;
}

```

## Java

```java

// Java program to swap elements of linked list by changing links

class LinkedList {

    static Node head;

    static class Node {

        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap elements of a linked list */
    Node pairWiseSwap(Node node)
    {

        // If linked list is empty or there is only one node in list
        if (node == null || node.next == null) {
            return node;
        }

        // Initialize previous and current pointers
        Node prev = node;
        Node curr = node.next;

        node = curr; // Change head before proceeeding

        // Traverse the list
        while (true) {
            Node next = curr.next;
            curr.next = prev; // Change next of current as previous node

            // If next NULL or next is the last node
            if (next == null || next.next == null) {
                prev.next = next;
                break;
            }

            // Change next of previous to next next
            prev.next = next.next;

            // Update previous and curr
            prev = next;
            curr = prev.next;
        }
        return node;
    }

    /* Function to print nodes in a given linked list */
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {

        /* The constructed linked list is:
         1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next = new Node(7);

        System.out.println("Linked list before calling pairwiseSwap() ");
        list.printList(head);
        Node st = list.pairWiseSwap(head);
        System.out.println("");
        System.out.println("Linked list after calling pairwiseSwap() ");
        list.printList(st);
        System.out.println("");
    }
}

// This code has been contributed by Mayank Jaiswal

```

## C#

```cs

// C# program to swap elements of
// linked list by changing links
using System;

public class LinkedList {

    Node head;

    public class Node {

        public int data;
        public Node next;

        public Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap 
    elements of a linked list */
    Node pairWiseSwap(Node node)
    {

        // If linked list is empty or there
        // is only one node in list
        if (node == null || node.next == null) {
            return node;
        }

        // Initialize previous and current pointers
        Node prev = node;
        Node curr = node.next;

        // Change head before proceeeding
        node = curr;

        // Traverse the list
        while (true) {
            Node next = curr.next;

            // Change next of current as previous node
            curr.next = prev;

            // If next NULL or next is the last node
            if (next == null || next.next == null) {
                prev.next = next;
                break;
            }

            // Change next of previous to next next
            prev.next = next.next;

            // Update previous and curr
            prev = next;
            curr = prev.next;
        }
        return node;
    }

    /* Function to print nodes 
    in a given linked list */
    void printList(Node node)
    {
        while (node != null) {
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        /* The constructed linked list is: 
        1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next = new Node(7);

        Console.WriteLine("Linked list before calling pairwiseSwap() ");
        list.printList(list.head);
        Node st = list.pairWiseSwap(list.head);
        Console.WriteLine("");
        Console.WriteLine("Linked list after calling pairwiseSwap() ");
        list.printList(st);
        Console.WriteLine("");
    }
}

// This code contributed by Rajput-Ji

```

**输出**：

```
 Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
 Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7 

```

时间复杂度：上面程序的时间复杂度为`O(n)`，其中 n 是给定链表中节点的数量。 while 循环遍历给定的链表。

以下是相同方法的**递归实现**。 我们更改前两个节点，然后重复其余列表。 感谢 geek 和 omer salem 提出了这种方法。

## C++

```cpp

/* This program swaps the nodes of linked list rather than swapping the 
field from the nodes. 
Imagine a case where a node contains many fields, there will be plenty 
of unnecessary swap calls. */

#include <bits/stdc++.h>
using namespace std;

/* A linked list node */
class node {
public:
    int data;
    node* next;
};

/* Function to pairwise swap elements of a linked list. 
It returns head of the modified list, so return value 
of this node must be assigned */
node* pairWiseSwap(node* head)
{
    // Base Case: The list is empty or has only one node
    if (head == NULL || head->next == NULL)
        return head;

    // Store head of list after two nodes
    node* remaing = head->next->next;

    // Change head
    node* newhead = head->next;

    // Change next of second node
    head->next->next = head;

    // Recur for remaining list and change next of head
    head->next = pairWiseSwap(remaing);

    // Return new head of modified list
    return newhead;
}

/* Function to add a node at the begining of Linked List */
void push(node** head_ref, int new_data)
{
    /* allocate node */
    node* new_node = new node();

    /* put in the data */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in a given linked list */
void printList(node* node)
{
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
}

/* Druver program to test above function */
int main()
{
    node* start = NULL;

    /* The constructed linked list is: 
    1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    cout << "Linked list before calling pairWiseSwap() ";
    printList(start);

    start = pairWiseSwap(start); // NOTE THIS CHANGE

    cout << "\nLinked list after calling pairWiseSwap() ";
    printList(start);

    return 0;
}

// This is code is contributed by rathbhupendra

```

## C

```c

/* This program swaps the nodes of linked list rather than swapping the
field from the nodes.
Imagine a case where a node contains many fields, there will be plenty
of unnecessary swap calls. */

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

/* A linked list node */
struct node {
    int data;
    struct node* next;
};

/* Function to pairwise swap elements of a linked list.
   It returns head of the modified list, so return value
   of this node must be assigned */
struct node* pairWiseSwap(struct node* head)
{
    // Base Case: The list is empty or has only one node
    if (head == NULL || head->next == NULL)
        return head;

    // Store head of list after two nodes
    struct node* remaing = head->next->next;

    // Change head
    struct node* newhead = head->next;

    // Change next of second node
    head->next->next = head;

    // Recur for remaining list and change next of head
    head->next = pairWiseSwap(remaing);

    // Return new head of modified list
    return newhead;
}

/* Function to add a node at the begining of Linked List */
void push(struct node** head_ref, int new_data)
{
    /* allocate node */
    struct node* new_node = (struct node*)malloc(sizeof(struct node));

    /* put in the data  */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Function to print nodes in a given linked list */
void printList(struct node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

/* Druver program to test above function */
int main()
{
    struct node* start = NULL;

    /* The constructed linked list is:
     1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    printf("\n Linked list before calling  pairWiseSwap() ");
    printList(start);

    start = pairWiseSwap(start); // NOTE THIS CHANGE

    printf("\n Linked list after calling  pairWiseSwap() ");
    printList(start);

    return 0;
}

```

## Java

```java

// Java program to swap elements of linked list by changing links

class LinkedList {

    static Node head;

    static class Node {

        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap elements of a linked list.
     It returns head of the modified list, so return value
     of this node must be assigned */
    Node pairWiseSwap(Node node)
    {

        // Base Case: The list is empty or has only one node
        if (node == null || node.next == null) {
            return node;
        }

        // Store head of list after two nodes
        Node remaing = node.next.next;

        // Change head
        Node newhead = node.next;

        // Change next of second node
        node.next.next = node;

        // Recur for remaining list and change next of head
        node.next = pairWiseSwap(remaing);

        // Return new head of modified list
        return newhead;
    }

    /* Function to print nodes in a given linked list */
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {

        /* The constructed linked list is:
         1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next = new Node(7);

        System.out.println("Linked list before calling pairwiseSwap() ");
        list.printList(head);
        head = list.pairWiseSwap(head);
        System.out.println("");
        System.out.println("Linked list after calling pairwiseSwap() ");
        list.printList(head);
        System.out.println("");
    }
}

```

## C#

```cs

// C# program to swap elements
// of linked list by changing links
using System;

public class LinkedList {
    Node head;

    class Node {
        public int data;
        public Node next;

        public Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap 
        elements of a linked list.
        It returns head of the modified
        list, so return value of this
        node must be assigned */
    Node pairWiseSwap(Node node)
    {

        // Base Case: The list is empty
        // or has only one node
        if (node == null || node.next == null) {
            return node;
        }

        // Store head of list after two nodes
        Node remaing = node.next.next;

        // Change head
        Node newhead = node.next;

        // Change next of second node
        node.next.next = node;

        // Recur for remaining list
        // and change next of head
        node.next = pairWiseSwap(remaing);

        // Return new head of modified list
        return newhead;
    }

    /* Function to print nodes in a given linked list */
    void printList(Node node)
    {
        while (node != null) {
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Driver program to test above functions
    public static void Main()
    {

        /* The constructed linked list is:
        1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next = new Node(7);

        Console.WriteLine("Linked list before calling pairwiseSwap() ");
        list.printList(list.head);
        list.head = list.pairWiseSwap(list.head);
        Console.WriteLine("");
        Console.WriteLine("Linked list after calling pairwiseSwap() ");
        list.printList(list.head);
        Console.WriteLine("");
    }
}

// This code is contributed by PrinciRaj1992

```

**输出**：

```
 Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
 Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7 

```

[通过更改指针|配对交换链表的相邻节点 | 系列 2](https://www.geeksforgeeks.org/pairwise-swap-adjacent-nodes-of-a-linked-list-by-changing-pointers-set-2/)

本文由 **Gautam Kumar** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

