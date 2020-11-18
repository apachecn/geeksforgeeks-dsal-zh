# 从未排序的双向链接列表

中删除重复项

给定一个包含 **n** 个节点的未排序双向链表。 问题是从给定列表中删除重复的节点。

**示例：**

![](img/2dc04c02d3e8a66aea2f2c6c43213f4c.png)

**方法 1（天真方法）：**

这是使用两个循环的最简单方法。 外循环用于一个接一个地拾取元素，内循环将拾取的元素与其余元素进行比较。

## C++

```cpp

// C++ implementation to remove duplicates from an 
// unsorted doubly linked list 
#include <bits/stdc++.h> 

using namespace std; 

// a node of the doubly linked list 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

// Function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del  -->  pointer to node to be deleted. 
void deleteNode(struct Node** head_ref, struct Node* del) 
{ 
    // base case 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 

    // Change next only if node to be deleted 
    // is NOT the last node 
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    // Change prev only if node to be deleted 
    // is NOT the first node 
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    // Finally, free the memory occupied by del 
    free(del); 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
void removeDuplicates(struct Node** head_ref) 
{ 
    // if DLL is empty or if it contains only 
    // a single node 
    if ((*head_ref) == NULL ||  
        (*head_ref)->next == NULL) 
        return; 

    struct Node* ptr1, *ptr2; 

    // pick elements one by one 
    for (ptr1 = *head_ref; ptr1 != NULL; ptr1 = ptr1->next) { 
        ptr2 = ptr1->next; 

        // Compare the picked element with the 
        // rest of the elements 
        while (ptr2 != NULL) { 

            // if duplicate, then delete it 
            if (ptr1->data == ptr2->data) { 

                // store pointer to the node next to 'ptr2' 
                struct Node* next = ptr2->next; 

                // delete node pointed to by 'ptr2' 
                deleteNode(head_ref, ptr2); 

                // update 'ptr2' 
                ptr2 = next; 
            } 

            // else simply move to the next node 
            else
                ptr2 = ptr2->next; 
        } 
    } 
} 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node 
    struct Node* new_node =  
        (struct Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to print nodes in a given doubly  
// linked list 
void printList(struct Node* head) 
{ 
    // if list is empty 
    if (head == NULL) 
        cout << "Doubly Linked list empty"; 

    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // Create the doubly linked list: 
    // 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
    push(&head, 12); 
    push(&head, 12); 
    push(&head, 10); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 4); 
    push(&head, 8); 

    cout << "Original Doubly linked list:n"; 
    printList(head); 

    /* remove duplicate nodes */
    removeDuplicates(&head); 

    cout << "\nDoubly linked list after "
            "removing duplicates:n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to remove duplicates  
// from an unsorted doubly linked list 
class GFG 
{ 

// a node of the doubly linked list 
static class Node 
{ 
    int data; 
    Node next; 
    Node prev; 
} 

// Function to delete a node in a Doubly Linked List. 
// head_ref -. pointer to head node pointer. 
// del -. pointer to node to be deleted. 
static Node deleteNode(Node head_ref, Node del) 
{ 
    // base case 
    if (head_ref == null || del == null) 
        return head_ref; 

    // If node to be deleted is head node 
    if (head_ref == del) 
        head_ref = del.next; 

    // Change next only if node to be deleted 
    // is NOT the last node 
    if (del.next != null) 
        del.next.prev = del.prev; 

    // Change prev only if node to be deleted 
    // is NOT the first node 
    if (del.prev != null) 
        del.prev.next = del.next; 
    return head_ref; 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
static Node removeDuplicates(Node head_ref) 
{ 
    // if DLL is empty or if it contains only 
    // a single node 
    if ((head_ref) == null ||  
        (head_ref).next == null) 
        return head_ref;; 

    Node ptr1, ptr2; 

    // pick elements one by one 
    for (ptr1 = head_ref;  
         ptr1 != null; ptr1 = ptr1.next)  
    { 
        ptr2 = ptr1.next; 

        // Compare the picked element with the 
        // rest of the elements 
        while (ptr2 != null) 
        { 

            // if duplicate, then delete it 
            if (ptr1.data == ptr2.data) 
            { 

                // store pointer to the node next to 'ptr2' 
                Node next = ptr2.next; 

                // delete node pointed to by 'ptr2' 
                head_ref = deleteNode(head_ref, ptr2); 

                // update 'ptr2' 
                ptr2 = next; 
            } 

            // else simply move to the next node 
            else
                ptr2 = ptr2.next; 
        } 
    } 
    return head_ref; 
} 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    // allocate node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = new_data; 

    // since we are adding at the beginning, 
    // prev is always null 
    new_node.prev = null; 

    // link the old list off the new node 
    new_node.next = (head_ref); 

    // change prev of head node to new node 
    if ((head_ref) != null) 
        (head_ref).prev = new_node; 

    // move the head to point to the new node 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to print nodes in a  
// given doubly linked list 
static void printList( Node head) 
{ 
    // if list is empty 
    if (head == null) 
        System.out.print("Doubly Linked list empty"); 

    while (head != null) 
    { 
        System.out.print( head.data + " "); 
        head = head.next; 
    } 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    Node head = null; 

    // Create the doubly linked list: 
    // 8<.4<.4<.6<.4<.8<.4<.10<.12<.12 
    head = push(head, 12); 
    head = push(head, 12); 
    head = push(head, 10); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 4); 
    head = push(head, 6); 
    head = push(head, 4); 
    head = push(head, 4); 
    head = push(head, 8); 

    System.out.print("Original Doubly linked list:\n"); 
    printList(head); 

    /* remove duplicate nodes */
    head=removeDuplicates(head); 

    System.out.print("\nDoubly linked list after" +  
                        " removing duplicates:\n"); 
    printList(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python implementation to remove duplicates  
# from an unsorted doubly linked list  

# Node of a linked list  
class Node:  
    def __init__(self, data = None, next = None):  
        self.next = next
        self.data = data  

# Function to delete a node in a Doubly Linked List. 
# head_ref -. pointer to head node pointer. 
# del -. pointer to node to be deleted. 
def deleteNode(head_ref,del_): 

    # base case 
    if (head_ref == None or del_ == None): 
        return head_ref 

    # If node to be deleted is head node 
    if (head_ref == del_): 
        head_ref = del_.next

    # Change next only if node to be deleted 
    # is NOT the last node 
    if (del_.next != None): 
        del_.next.prev = del_.prev 

    # Change prev only if node to be deleted 
    # is NOT the first node 
    if (del_.prev != None): 
        del_.prev.next = del_.next
    return head_ref 

# function to remove duplicates from 
# an unsorted doubly linked list 
def removeDuplicates( head_ref): 

    # if DLL is empty or if it contains only 
    # a single node 
    if ((head_ref) == None or (head_ref).next == None): 
        return head_ref 

    ptr1 = head_ref 
    ptr2 = None

    # pick elements one by one 
    while(ptr1 != None) : 
        ptr2 = ptr1.next

        # Compare the picked element with the 
        # rest of the elements 
        while (ptr2 != None): 

            # if duplicate, then delete it 
            if (ptr1.data == ptr2.data): 

                # store pointer to the node next to 'ptr2' 
                next = ptr2.next

                # delete node pointed to by 'ptr2' 
                head_ref = deleteNode(head_ref, ptr2) 

                # update 'ptr2' 
                ptr2 = next

            # else simply move to the next node 
            else: 
                ptr2 = ptr2.next
        ptr1 = ptr1.next
    return head_ref 

# Function to insert a node at the beginning 
# of the Doubly Linked List 
def push( head_ref, new_data): 

    # allocate node 
    new_node = Node() 

    # put in the data 
    new_node.data = new_data 

    # since we are adding at the beginning, 
    # prev is always None 
    new_node.prev = None

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # change prev of head node to new node 
    if ((head_ref) != None): 
        (head_ref).prev = new_node 

    # move the head to point to the new node 
    (head_ref) = new_node 
    return head_ref 

# Function to print nodes in a  
# given doubly linked list 
def printList( head): 

    # if list is empty 
    if (head == None): 
        print("Doubly Linked list empty") 

    while (head != None): 
        print( head.data ,end= " ") 
        head = head.next

# Driver Code 
head = None

# Create the doubly linked list: 
# 8<.4<.4<.6<.4<.8<.4<.10<.12<.12 
head = push(head, 12) 
head = push(head, 12) 
head = push(head, 10) 
head = push(head, 4) 
head = push(head, 8) 
head = push(head, 4) 
head = push(head, 6) 
head = push(head, 4) 
head = push(head, 4) 
head = push(head, 8) 

print("Original Doubly linked list:") 
printList(head) 

# remove duplicate nodes */ 
head=removeDuplicates(head) 

print("\nDoubly linked list after removing duplicates:") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to remove duplicates  
// from an unsorted doubly linked list 
using System; 

class GFG 
{ 

// a node of the doubly linked list 
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node prev; 
} 

// Function to delete a node in a Doubly Linked List. 
// head_ref -. pointer to head node pointer. 
// del -. pointer to node to be deleted. 
static Node deleteNode(Node head_ref, Node del) 
{ 
    // base case 
    if (head_ref == null || del == null) 
        return head_ref; 

    // If node to be deleted is head node 
    if (head_ref == del) 
        head_ref = del.next; 

    // Change next only if node to be deleted 
    // is NOT the last node 
    if (del.next != null) 
        del.next.prev = del.prev; 

    // Change prev only if node to be deleted 
    // is NOT the first node 
    if (del.prev != null) 
        del.prev.next = del.next; 
    return head_ref; 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
static Node removeDuplicates(Node head_ref) 
{ 
    // if DLL is empty or if it contains only 
    // a single node 
    if ((head_ref) == null ||  
        (head_ref).next == null) 
        return head_ref;; 

    Node ptr1, ptr2; 

    // pick elements one by one 
    for (ptr1 = head_ref;  
        ptr1 != null; ptr1 = ptr1.next)  
    { 
        ptr2 = ptr1.next; 

        // Compare the picked element with the 
        // rest of the elements 
        while (ptr2 != null) 
        { 

            // if duplicate, then delete it 
            if (ptr1.data == ptr2.data) 
            { 

                // store pointer to the node next to 'ptr2' 
                Node next = ptr2.next; 

                // delete node pointed to by 'ptr2' 
                head_ref = deleteNode(head_ref, ptr2); 

                // update 'ptr2' 
                ptr2 = next; 
            } 

            // else simply move to the next node 
            else
                ptr2 = ptr2.next; 
        } 
    } 
    return head_ref; 
} 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    // allocate node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = new_data; 

    // since we are adding at the beginning, 
    // prev is always null 
    new_node.prev = null; 

    // link the old list off the new node 
    new_node.next = (head_ref); 

    // change prev of head node to new node 
    if ((head_ref) != null) 
        (head_ref).prev = new_node; 

    // move the head to point to the new node 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to print nodes in a  
// given doubly linked list 
static void printList( Node head) 
{ 
    // if list is empty 
    if (head == null) 
        Console.Write("Doubly Linked list empty"); 

    while (head != null) 
    { 
        Console.Write( head.data + " "); 
        head = head.next; 
    } 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    Node head = null; 

    // Create the doubly linked list: 
    // 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
    head = push(head, 12); 
    head = push(head, 12); 
    head = push(head, 10); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 4); 
    head = push(head, 6); 
    head = push(head, 4); 
    head = push(head, 4); 
    head = push(head, 8); 

    Console.Write("Original Doubly linked list:\n"); 
    printList(head); 

    /* remove duplicate nodes */
    head=removeDuplicates(head); 

    Console.Write("\nDoubly linked list after" +  
                     " removing duplicates:\n"); 
    printList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Original Doubly linked list:
8 4 4 6 4 8 4 10 12 12
Doubly linked list after removing duplicates:
8 4 6 10 12

```

**时间复杂度：** O（n <sup>2</sup> ）

**辅助空间：** O（1）

**方法 2（排序）：**以下是步骤：

1.  使用合并排序对双向链表中的元素进行排序。 请参阅此帖子的[。](https://www.geeksforgeeks.org/merge-sort-for-doubly-linked-list/)

2.  使用[算法在线性时间内删除重复项，以从排序的双向链表](https://www.geeksforgeeks.org/remove-duplicates-sorted-doubly-linked-list/)中删除重复项。

时间复杂度：O（nLogn）

辅助空间：O（1）

请注意，此方法不会保留元素的原始顺序。

**方法 3 高效方法（散列）：**

我们从头到尾遍历双向链表。 对于每个新遇到的元素，我们检查它是否在哈希表中：如果是，则将其删除；否则，将其删除。 否则我们将其放在哈希表中。 哈希表是使用 C++ 中的 [unordered_set 实现的。](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)

## C++

```cpp

// C++ implementation to remove duplicates from an 
// unsorted doubly linked list 
#include <bits/stdc++.h> 

using namespace std; 

// a node of the doubly linked list 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

// Function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del  -->  pointer to node to be deleted. 
void deleteNode(struct Node** head_ref, struct Node* del) 
{ 
    // base case 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 

    // Change next only if node to be deleted  
    // is NOT the last node 
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    // Change prev only if node to be deleted  
    // is NOT the first node 
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    // Finally, free the memory occupied by del 
    free(del); 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
void removeDuplicates(struct Node** head_ref) 
{ 
    // if doubly linked list is empty 
    if ((*head_ref) == NULL) 
        return; 

    // unordered_set 'us' implemented as hash table 
    unordered_set<int> us; 

    struct Node* current = *head_ref, *next; 

    // traverse up to the end of the list 
    while (current != NULL) { 

        // if current data is seen before 
        if (us.find(current->data) != us.end()) { 

            // store pointer to the node next to  
            // 'current' node 
            next = current->next; 

            // delete the node pointed to by 'current' 
            deleteNode(head_ref, current); 

            // update 'current' 
            current = next; 
        } 

        else { 

            // insert the current data in 'us' 
            us.insert(current->data); 

            // move to the next node 
            current = current->next; 
        } 
    } 
} 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node 
    struct Node* new_node =  
         (struct Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to print nodes in a given doubly  
// linked list 
void printList(struct Node* head) 
{ 
    // if list is empty 
    if (head == NULL) 
        cout << "Doubly Linked list empty"; 

    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // Create the doubly linked list: 
    // 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
    push(&head, 12); 
    push(&head, 12); 
    push(&head, 10); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 4); 
    push(&head, 8); 

    cout << "Original Doubly linked list:n"; 
    printList(head); 

    /* remove duplicate nodes */
    removeDuplicates(&head); 

    cout << "\nDoubly linked list after "
             "removing duplicates:n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java mplementation to remove duplicates  
// from an unsorted doubly linked list 
import java.util.*; 

class GFG  
{ 

// a node of the doubly linked list 
static class Node 
{ 
    int data; 
    Node next; 
    Node prev; 
}; 

// Function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del --> pointer to node to be deleted. 
static Node deleteNode(Node head_ref, Node del) 
{ 
    // base case 
    if (head_ref == null || del == null) 
        return null; 

    // If node to be deleted is head node 
    if (head_ref == del) 
        head_ref = del.next; 

    // Change next only if node to be deleted  
    // is NOT the last node 
    if (del.next != null) 
        del.next.prev = del.prev; 

    // Change prev only if node to be deleted  
    // is NOT the first node 
    if (del.prev != null) 
        del.prev.next = del.next; 

    return head_ref; 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
static Node removeDuplicates(Node head_ref) 
{ 
    // if doubly linked list is empty 
    if ((head_ref) == null) 
        return null; 

    // unordered_set 'us' implemented as hash table 
    HashSet<Integer> us = new HashSet<>(); 

    Node current = head_ref, next; 

    // traverse up to the end of the list 
    while (current != null) 
    { 

        // if current data is seen before 
        if (us.contains(current.data))  
        { 

            // store pointer to the node next to  
            // 'current' node 
            next = current.next; 

            // delete the node pointed to by 'current' 
            head_ref = deleteNode(head_ref, current); 

            // update 'current' 
            current = next; 
        } 
        else 
        { 

            // insert the current data in 'us' 
            us.add(current.data); 

            // move to the next node 
            current = current.next; 
        } 
    } 
    return head_ref; 
} 

// Function to insert a node at the  
// beginning of the Doubly Linked List 
static Node push(Node head_ref,  
                 int new_data) 
{ 
    // allocate node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = new_data; 

    // since we are adding at the beginning, 
    // prev is always null 
    new_node.prev = null; 

    // link the old list off the new node 
    new_node.next = (head_ref); 

    // change prev of head node to new node 
    if ((head_ref) != null) 
        (head_ref).prev = new_node; 

    // move the head to point to the new node 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to print nodes in a given doubly  
// linked list 
static void printList(Node head) 
{ 
    // if list is empty 
    if (head == null) 
        System.out.print("Doubly Linked list empty"); 

    while (head != null) 
    { 
        System.out.print(head.data + " "); 
        head = head.next; 
    } 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    Node head = null; 

    // Create the doubly linked list: 
    // 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
    head = push(head, 12); 
    head = push(head, 12); 
    head = push(head, 10); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 4); 
    head = push(head, 6); 
    head = push(head, 4); 
    head = push(head, 4); 
    head = push(head, 8); 

    System.out.println("Original Doubly linked list:"); 
    printList(head); 

    /* remove duplicate nodes */
    head = removeDuplicates(head); 

    System.out.println("\nDoubly linked list after " +  
                              "removing duplicates:"); 
    printList(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 implementation to remove duplicates  
# from an unsorted doubly linked list 

# a node of the doubly linked list 
class Node: 
    def __init__(self): 
        self.data = 0
        self.next = None
        self.prev = None

# Function to delete a node in a Doubly Linked List. 
# head_ref --> pointer to head node pointer. 
# del --> pointer to node to be deleted. 
def deleteNode( head_ref, del_): 

    # base case 
    if (head_ref == None or del_ == None): 
        return None

    # If node to be deleted is head node 
    if (head_ref == del_): 
        head_ref = del_.next

    # Change next only if node to be deleted  
    # is NOT the last node 
    if (del_.next != None): 
        del_.next.prev = del_.prev 

    # Change prev only if node to be deleted  
    # is NOT the first node 
    if (del_.prev != None): 
        del_.prev.next = del_.next

    return head_ref 

# function to remove duplicates from 
# an unsorted doubly linked list 
def removeDuplicates(head_ref): 

    # if doubly linked list is empty 
    if ((head_ref) == None): 
        return None

    # unordered_set 'us' implemented as hash table 
    us = set() 

    current = head_ref 
    next = None

    # traverse up to the end of the list 
    while (current != None): 

        # if current data is seen before 
        if ((current.data) in us):  

            # store pointer to the node next to  
            # 'current' node 
            next = current.next

            # delete the node pointed to by 'current' 
            head_ref = deleteNode(head_ref, current) 

            # update 'current' 
            current = next

        else: 

            # insert the current data in 'us' 
            us.add(current.data) 

            # move to the next node 
            current = current.next

    return head_ref 

# Function to insert a node at the  
# beginning of the Doubly Linked List 
def push(head_ref,new_data): 

    # allocate node 
    new_node = Node() 

    # put in the data 
    new_node.data = new_data 

    # since we are adding at the beginning, 
    # prev is always None 
    new_node.prev = None

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # change prev of head node to new node 
    if ((head_ref) != None): 
        (head_ref).prev = new_node 

    # move the head to point to the new node 
    (head_ref) = new_node 
    return head_ref 

# Function to print nodes in a given doubly  
# linked list 
def printList( head): 

    # if list is empty 
    if (head == None): 
        print("Doubly Linked list empty") 

    while (head != None): 

        print(head.data , end=" ") 
        head = head.next

# Driver Code 

head = None

# Create the doubly linked list: 
# 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
head = push(head, 12) 
head = push(head, 12) 
head = push(head, 10) 
head = push(head, 4) 
head = push(head, 8) 
head = push(head, 4) 
head = push(head, 6) 
head = push(head, 4) 
head = push(head, 4) 
head = push(head, 8) 

print("Original Doubly linked list:") 
printList(head) 

# remove duplicate nodes  
head = removeDuplicates(head) 

print("\nDoubly linked list after removing duplicates:") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# mplementation to remove duplicates  
// from an unsorted doubly linked list 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// a node of the doubly linked list 
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node prev; 
}; 

// Function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del --> pointer to node to be deleted. 
static Node deleteNode(Node head_ref, Node del) 
{ 
    // base case 
    if (head_ref == null || del == null) 
        return null; 

    // If node to be deleted is head node 
    if (head_ref == del) 
        head_ref = del.next; 

    // Change next only if node to be deleted  
    // is NOT the last node 
    if (del.next != null) 
        del.next.prev = del.prev; 

    // Change prev only if node to be deleted  
    // is NOT the first node 
    if (del.prev != null) 
        del.prev.next = del.next; 

    return head_ref; 
} 

// function to remove duplicates from 
// an unsorted doubly linked list 
static Node removeDuplicates(Node head_ref) 
{ 
    // if doubly linked list is empty 
    if ((head_ref) == null) 
        return null; 

    // unordered_set 'us' implemented as hash table 
    HashSet<int> us = new HashSet<int>(); 

    Node current = head_ref, next; 

    // traverse up to the end of the list 
    while (current != null) 
    { 

        // if current data is seen before 
        if (us.Contains(current.data))  
        { 

            // store pointer to the node next to  
            // 'current' node 
            next = current.next; 

            // delete the node pointed to by 'current' 
            head_ref = deleteNode(head_ref, current); 

            // update 'current' 
            current = next; 
        } 
        else
        { 

            // insert the current data in 'us' 
            us.Add(current.data); 

            // move to the next node 
            current = current.next; 
        } 
    } 
    return head_ref; 
} 

// Function to insert a node at the  
// beginning of the Doubly Linked List 
static Node push(Node head_ref,  
                 int new_data) 
{ 
    // allocate node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = new_data; 

    // since we are adding at the beginning, 
    // prev is always null 
    new_node.prev = null; 

    // link the old list off the new node 
    new_node.next = (head_ref); 

    // change prev of head node to new node 
    if ((head_ref) != null) 
        (head_ref).prev = new_node; 

    // move the head to point to the new node 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to print nodes in a  
// given doubly linked list 
static void printList(Node head) 
{ 
    // if list is empty 
    if (head == null) 
        Console.Write("Doubly Linked list empty"); 

    while (head != null) 
    { 
        Console.Write(head.data + " "); 
        head = head.next; 
    } 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    Node head = null; 

    // Create the doubly linked list: 
    // 8<->4<->4<->6<->4<->8<->4<->10<->12<->12 
    head = push(head, 12); 
    head = push(head, 12); 
    head = push(head, 10); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 4); 
    head = push(head, 6); 
    head = push(head, 4); 
    head = push(head, 4); 
    head = push(head, 8); 

    Console.WriteLine("Original Doubly linked list:"); 
    printList(head); 

    /* remove duplicate nodes */
    head = removeDuplicates(head); 

    Console.WriteLine("\nDoubly linked list after " +  
                             "removing duplicates:"); 
    printList(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出：**

```
Original Doubly linked list:
8 4 4 6 4 8 4 10 12 12
Doubly linked list after removing duplicates:
8 4 6 10 12

```

**时间复杂度：** O（n）

**辅助空间：** O（n）

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

