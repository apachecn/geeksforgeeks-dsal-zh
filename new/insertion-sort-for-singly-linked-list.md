# 单链表

> 原文：[https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/](https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)

的插入排序

我们已经讨论了[数组](http://quiz.geeksforgeeks.org/insertion-sort/)的插入排序。 在本文中，讨论了相同的链表。

以下是链表的简单插入排序算法。

```
1) Create an empty sorted (or result) list
2) Traverse the given list, do following for every node.
......a) Insert current node in sorted way in sorted or result list.
3) Change head of given linked list to head of sorted (or result) list.

```

主要步骤是（2.a），已在下面的文章中介绍。

[单链表的排序插入](https://www.geeksforgeeks.org/given-a-linked-list-which-is-sorted-how-will-you-insert-in-sorted-way/)

下面是上述算法的实现

## C/C++ 

```cpp

/* C program for insertion sort on a linked list */
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// Function to insert a given node in a sorted linked list 
void sortedInsert(struct Node**, struct Node*); 

// function to sort a singly linked list using insertion sort 
void insertionSort(struct Node **head_ref) 
{ 
    // Initialize sorted linked list 
    struct Node *sorted = NULL; 

    // Traverse the given linked list and insert every 
    // node to sorted 
    struct Node *current = *head_ref; 
    while (current != NULL) 
    { 
        // Store next for next iteration 
        struct Node *next = current->next; 

        // insert current in sorted linked list 
        sortedInsert(&sorted, current); 

        // Update current 
        current = next; 
    } 

    // Update head_ref to point to sorted linked list 
    *head_ref = sorted; 
} 

/* function to insert a new_node in a list. Note that this 
  function expects a pointer to head_ref as this can modify the 
  head of the input linked list (similar to push())*/
void sortedInsert(struct Node** head_ref, struct Node* new_node) 
{ 
    struct Node* current; 
    /* Special case for the head end */
    if (*head_ref == NULL || (*head_ref)->data >= new_node->data) 
    { 
        new_node->next = *head_ref; 
        *head_ref = new_node; 
    } 
    else
    { 
        /* Locate the node before the point of insertion */
        current = *head_ref; 
        while (current->next!=NULL && 
               current->next->data < new_node->data) 
        { 
            current = current->next; 
        } 
        new_node->next = current->next; 
        current->next = new_node; 
    } 
} 

/* BELOW FUNCTIONS ARE JUST UTILITY TO TEST sortedInsert */

/* Function to print linked list */
void printList(struct Node *head) 
{ 
    struct Node *temp = head; 
    while(temp != NULL) 
    { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

/* A utility function to insert a node at the beginning of linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Node *a = NULL; 
    push(&a, 5); 
    push(&a, 20); 
    push(&a, 4); 
    push(&a, 3); 
    push(&a, 30); 

    printf("Linked List before sorting \n"); 
    printList(a); 

    insertionSort(&a); 

    printf("\nLinked List after sorting \n"); 
    printList(a); 

    return 0; 
} 

```

## Java

```java

// Java program to sort link list 
// using insertion sort 

public class LinkedlistIS  
{ 
    node head; 
    node sorted; 

    class node  
    { 
        int val; 
        node next; 

        public node(int val)  
        { 
            this.val = val; 
        } 
    } 

    void push(int val)  
    { 
        /* allocate node */
        node newnode = new node(val); 
        /* link the old list off the new node */
        newnode.next = head; 
        /* move the head to point to the new node */
        head = newnode; 
    } 

    // function to sort a singly linked list using insertion sort 
    void insertionSort(node headref)  
    { 
        // Initialize sorted linked list 
        sorted = null; 
        node current = headref; 
        // Traverse the given linked list and insert every 
        // node to sorted 
        while (current != null)  
        { 
            // Store next for next iteration 
            node next = current.next; 
            // insert current in sorted linked list 
            sortedInsert(current); 
            // Update current 
            current = next; 
        } 
        // Update head_ref to point to sorted linked list 
        head = sorted; 
    } 

    /* 
     * function to insert a new_node in a list. Note that  
     * this function expects a pointer to head_ref as this 
     * can modify the head of the input linked list  
     * (similar to push()) 
     */
    void sortedInsert(node newnode)  
    { 
        /* Special case for the head end */
        if (sorted == null || sorted.val >= newnode.val)  
        { 
            newnode.next = sorted; 
            sorted = newnode; 
        } 
        else 
        { 
            node current = sorted; 
            /* Locate the node before the point of insertion */
            while (current.next != null && current.next.val < newnode.val)  
            { 
                current = current.next; 
            } 
            newnode.next = current.next; 
            current.next = newnode; 
        } 
    } 

    /* Function to print linked list */
    void printlist(node head)  
    { 
        while (head != null)  
        { 
            System.out.print(head.val + " "); 
            head = head.next; 
        } 
    } 

    // Driver program to test above functions 
    public static void main(String[] args)  
    { 
        LinkedlistIS list = new LinkedlistIS(); 
        list.push(5); 
        list.push(20); 
        list.push(4); 
        list.push(3); 
        list.push(30); 
        System.out.println("Linked List before Sorting.."); 
        list.printlist(list.head); 
        list.insertionSort(list.head); 
        System.out.println("\nLinkedList After sorting"); 
        list.printlist(list.head); 
    } 
} 

// This code is contributed by Rishabh Mahrsee 

```

## Python

```py

# Pyhton implementation of above algorithm 

# Node class  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to sort a singly linked list using insertion sort 
def insertionSort(head_ref): 

    # Initialize sorted linked list 
    sorted = None

    # Traverse the given linked list and insert every 
    # node to sorted 
    current = head_ref 
    while (current != None): 

        # Store next for next iteration 
        next = current.next

        # insert current in sorted linked list 
        sorted = sortedInsert(sorted, current) 

        # Update current 
        current = next

    # Update head_ref to point to sorted linked list 
    head_ref = sorted
    return head_ref 

# function to insert a new_node in a list. Note that this 
# function expects a pointer to head_ref as this can modify the 
# head of the input linked list (similar to push()) 
def sortedInsert(head_ref, new_node): 

    current = None

    # Special case for the head end */ 
    if (head_ref == None or (head_ref).data >= new_node.data): 

        new_node.next = head_ref 
        head_ref = new_node 

    else: 

        # Locate the node before the point of insertion  
        current = head_ref 
        while (current.next != None and
            current.next.data < new_node.data): 

            current = current.next

        new_node.next = current.next
        current.next = new_node 

    return head_ref 

# BELOW FUNCTIONS ARE JUST UTILITY TO TEST sortedInsert  

# Function to print linked list */ 
def printList(head): 

    temp = head 
    while(temp != None): 

        print( temp.data, end = " ") 
        temp = temp.next

# A utility function to insert a node 
# at the beginning of linked list  
def push( head_ref, new_data): 

    # allocate node 
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list off the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 
    return head_ref 

# Driver program to test above functions 

a = None
a = push(a, 5) 
a = push(a, 20) 
a = push(a, 4) 
a = push(a, 3) 
a = push(a, 30) 

print("Linked List before sorting ") 
printList(a) 

a = insertionSort(a) 

print("\nLinked List after sorting ") 
printList(a) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to sort link list 
// using insertion sort 
using System; 

public class LinkedlistIS  
{ 
    public node head; 
    public node sorted; 

    public class node  
    { 
        public int val; 
        public node next; 

        public node(int val)  
        { 
            this.val = val; 
        } 
    } 

    void push(int val)  
    { 
        /* allocate node */
        node newnode = new node(val); 

        /* link the old list off the new node */
        newnode.next = head; 

        /* move the head to point to the new node */
        head = newnode; 
    } 

    // function to sort a singly  
    // linked list using insertion sort 
    void insertionSort(node headref)  
    { 
        // Initialize sorted linked list 
        sorted = null; 
        node current = headref; 

        // Traverse the given  
        // linked list and insert every 
        // node to sorted 
        while (current != null)  
        { 
            // Store next for next iteration 
            node next = current.next; 

            // insert current in sorted linked list 
            sortedInsert(current); 

            // Update current 
            current = next; 
        } 

        // Update head_ref to point to sorted linked list 
        head = sorted; 
    } 

    /* 
    * function to insert a new_node in a list. Note that  
    * this function expects a pointer to head_ref as this 
    * can modify the head of the input linked list  
    * (similar to push()) 
    */
    void sortedInsert(node newnode)  
    { 
        /* Special case for the head end */
        if (sorted == null || sorted.val >= newnode.val)  
        { 
            newnode.next = sorted; 
            sorted = newnode; 
        } 
        else
        { 
            node current = sorted; 

            /* Locate the node before the point of insertion */
            while (current.next != null &&  
                    current.next.val < newnode.val)  
            { 
                current = current.next; 
            } 
            newnode.next = current.next; 
            current.next = newnode; 
        } 
    } 

    /* Function to print linked list */
    void printlist(node head)  
    { 
        while (head != null)  
        { 
            Console.Write(head.val + " "); 
            head = head.next; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        LinkedlistIS list = new LinkedlistIS(); 
        list.push(5); 
        list.push(20); 
        list.push(4); 
        list.push(3); 
        list.push(30); 
        Console.WriteLine("Linked List before Sorting.."); 
        list.printlist(list.head); 
        list.insertionSort(list.head); 
        Console.WriteLine("\nLinkedList After sorting"); 
        list.printlist(list.head); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

