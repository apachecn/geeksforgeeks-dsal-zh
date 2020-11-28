# 以排序顺序合并`K`个排序的双链表

> 原文：[https://www.geeksforgeeks.org/merge-k-sorted-doubly-linked-list-in-sorted-order/](https://www.geeksforgeeks.org/merge-k-sorted-doubly-linked-list-in-sorted-order/)

给定`K`排序的双链表。 任务是将所有排序的双链表合并到单个排序的双链表中，这意味着必须对最终列表排序。

**示例**：

> **输入**：
>
> 列表 1：`2 <-> 7 <-> 8 <-> 12 <-> 15 <-> NULL`
>
> 列表 2：`4 <-> 9 <-> 10 <-> NULL`
>
> 列表 3：`5 <-> 9 <-> 11 <-> 16 <-> NULL`
>
> **输出**：`2 4 5 7 8 9 9 10 11 12 15 16`
> 
> **输入**：
>
> 列表 1：`4 <-> 7 <-> 8 <-> 10 <-> NULL`
>
> 列表 2：`4 <-> 19 <-> 20 <-> 23 <-> 27 <-> NULL`
>
> 列表 3：`3 <-> 9 <-> 12 <-> 20 <-> NULL`
>
> 列表 4：`1 <-> 19 <-> 22 <-> NULL`
>
> 列表 5：`7 <-> 16 <-> 20 <-> 21 <-> NULL`
>
> **输出**：
>
> `1 3 4 4 7 7 8 8 10 10 16 16 19 19 20 20 20 21 22 23 27`

**先决条件**：[参考算法](https://en.wikipedia.org/wiki/Merge_algorithm)

**方法**：

1.  首先按排序顺序合并两个双向链表

2.  然后按排序顺序将此列表与另一个列表合并

3.  做同样的事情，直到所有列表都没有合并

4.  请记住，您必须一次合并两个列表，然后合并的列表将被新合并

**算法**：

```
function merge(A, B) is
    inputs A, B : list
    returns list

    C := new empty list
    while A is not empty and B is not empty do
        if head(A) < head(B) then
            append head(A) to C
            drop the head of A
        else
            append head(B) to C
            drop the head of B

    // By now, either A or B is empty 
    // It remains to empty the other input list
    while A is not empty do
        append head(A) to C
        drop the head of A
    while B is not empty do
        append head(B) to C
        drop the head of B

    return C

```c

下面是上述方法的实现：

## C++

```cpp

// C++ program to merge K sorted doubly 
// linked list in sorted order 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    Node* next; 
    Node* prev; 
}; 

// Given a reference (pointer to pointer) to the head 
// Of a DLL and an int, appends a new node at the end 
void append(struct Node** head_ref, int new_data) 
{ 
    // Allocate node 
    struct Node* new_node 
        = (struct Node*)malloc(sizeof(struct Node)); 

    struct Node* last = *head_ref; 

    // Put in the data 
    new_node->data = new_data; 

    // This new node is going to be the last 
    // node, so make next of it as NULL 
    new_node->next = NULL; 

    // If the Linked List is empty, then make 
    // the new node as head */ 
    if (*head_ref == NULL) { 
        new_node->prev = NULL; 
        *head_ref = new_node; 
        return; 
    } 

    // Else traverse till the last node 
    while (last->next != NULL) 
        last = last->next; 

    // Change the next of last node 
    last->next = new_node; 

    // Make last node as previous of new node 
    new_node->prev = last; 

    return; 
} 

// Function to print the list 
void printList(Node* node) 
{ 
    Node* last; 

    // Run while loop unless node becomes null 
    while (node != NULL) { 
        cout << node->data << " "; 
        last = node; 
        node = node->next; 
    } 
} 

// Function to merge two 
// sorted doubly linked lists 
Node* mergeList(Node* p, Node* q) 
{ 
    Node* s = NULL; 

    // If any of the list is empty 
    if (p == NULL || q == NULL) { 
        return (p == NULL ? q : p); 
    } 

    // Comparison the data of two linked list 
    if (p->data < q->data) { 
        p->prev = s; 
        s = p; 
        p = p->next; 
    } 
    else { 
        q->prev = s; 
        s = q; 
        q = q->next; 
    } 

    // Store head pointer before merge the list 
    Node* head = s; 
    while (p != NULL && q != NULL) { 
        if (p->data < q->data) { 

            // Changing of pointer between 
            // Two list for merging 
            s->next = p; 
            p->prev = s; 
            s = s->next; 
            p = p->next; 
        } 
        else { 

            // Changing of pointer between 
            // Two list for merging 
            s->next = q; 
            q->prev = s; 
            s = s->next; 
            q = q->next; 
        } 
    } 

    // Condition to check if any anyone list not end 
    if (p == NULL) { 
        s->next = q; 
        q->prev = s; 
    } 
    if (q == NULL) { 
        s->next = p; 
        p->prev = s; 
    } 

    // Return head pointer of merged list 
    return head; 
} 

// Function to merge all sorted linked 
// list in sorted order 
Node* mergeAllList(Node* head[], int k) 
{ 
    Node* finalList = NULL; 
    for (int i = 0; i < k; i++) { 

        // Function call to merge two sorted 
        // doubly linked list at a time 
        finalList = mergeList(finalList, head[i]); 
    } 

    // Return final sorted doubly linked list 
    return finalList; 
} 

// Driver code 
int main() 
{ 
    int k = 3; 
    Node* head[k]; 

    // Loop to initialize all the lists to empty 
    for (int i = 0; i < k; i++) { 
        head[i] = NULL; 
    } 

    // Create first doubly linked List 
    // List1 -> 1 <=> 5 <=> 9 
    append(&head[0], 1); 

    append(&head[0], 5); 

    append(&head[0], 9); 

    // Create second doubly linked List 
    // List2 -> 2 <=> 3 <=> 7 <=> 12 
    append(&head[1], 2); 

    append(&head[1], 3); 

    append(&head[1], 7); 

    append(&head[1], 12); 

    // Create third doubly linked List 
    // List3 -> 8 <=> 11 <=> 13 <=> 18 
    append(&head[2], 8); 

    append(&head[2], 11); 

    append(&head[2], 13); 

    append(&head[2], 18); 

    // Function call to merge all sorted 
    // doubly linked lists in sorted order 
    Node* finalList = mergeAllList(head, k); 

    // Print final sorted list 
    printList(finalList); 

    return 0; 
} 

```

## Java

```java

// Java program to merge K sorted doubly 
// linked list in sorted order 
class GFG 
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
    Node prev; 
}; 

// Given a reference (pointer to pointer) to the head 
// Of a DLL and an int, appends a new node at the end 
static Node append(Node head_ref, int new_data) 
{ 
    // Allocate node 
    Node new_node = new Node(); 

    Node last = head_ref; 

    // Put in the data 
    new_node.data = new_data; 

    // This new node is going to be the last 
    // node, so make next of it as null 
    new_node.next = null; 

    // If the Linked List is empty, then make 
    // the new node as head */ 
    if (head_ref == null)  
    { 
        new_node.prev = null; 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Else traverse till the last node 
    while (last.next != null) 
        last = last.next; 

    // Change the next of last node 
    last.next = new_node; 

    // Make last node as previous of new node 
    new_node.prev = last; 

    return head_ref; 
} 

// Function to print the list 
static void printList(Node node) 
{ 
    Node last; 

    // Run while loop unless node becomes null 
    while (node != null)  
    { 
        System.out.print( node.data + " "); 
        last = node; 
        node = node.next; 
    } 
} 

// Function to merge two 
// sorted doubly linked lists 
static Node mergeList(Node p, Node q) 
{ 
    Node s = null; 

    // If any of the list is empty 
    if (p == null || q == null)  
    { 
        return (p == null ? q : p); 
    } 

    // Comparison the data of two linked list 
    if (p.data < q.data) 
    { 
        p.prev = s; 
        s = p; 
        p = p.next; 
    } 
    else
    { 
        q.prev = s; 
        s = q; 
        q = q.next; 
    } 

    // Store head pointer before merge the list 
    Node head = s; 
    while (p != null && q != null)  
    { 
        if (p.data < q.data)  
        { 

            // Changing of pointer between 
            // Two list for merging 
            s.next = p; 
            p.prev = s; 
            s = s.next; 
            p = p.next; 
        } 
        else 
        { 

            // Changing of pointer between 
            // Two list for merging 
            s.next = q; 
            q.prev = s; 
            s = s.next; 
            q = q.next; 
        } 
    } 

    // Condition to check if any anyone list not end 
    if (p == null) 
    { 
        s.next = q; 
        q.prev = s; 
    } 
    if (q == null) 
    { 
        s.next = p; 
        p.prev = s; 
    } 

    // Return head pointer of merged list 
    return head; 
} 

// Function to merge all sorted linked 
// list in sorted order 
static Node mergeAllList(Node head[], int k) 
{ 
    Node finalList = null; 
    for (int i = 0; i < k; i++)  
    { 

        // Function call to merge two sorted 
        // doubly linked list at a time 
        finalList = mergeList(finalList, head[i]); 
    } 

    // Return final sorted doubly linked list 
    return finalList; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int k = 3; 
    Node head[] = new Node[k]; 

    // Loop to initialize all the lists to empty 
    for (int i = 0; i < k; i++)  
    { 
        head[i] = null; 
    } 

    // Create first doubly linked List 
    // List1 . 1 <=> 5 <=> 9 
    head[0] = append(head[0], 1); 

    head[0] = append(head[0], 5); 

    head[0] = append(head[0], 9); 

    // Create second doubly linked List 
    // List2 . 2 <=> 3 <=> 7 <=> 12 
    head[1] = append(head[1], 2); 

    head[1] = append(head[1], 3); 

    head[1] = append(head[1], 7); 

    head[1] = append(head[1], 12); 

    // Create third doubly linked List 
    // List3 . 8 <=> 11 <=> 13 <=> 18 
    head[2] = append(head[2], 8); 

    head[2] = append(head[2], 11); 

    head[2] = append(head[2], 13); 

    head[2] = append(head[2], 18); 

    // Function call to merge all sorted 
    // doubly linked lists in sorted order 
    Node finalList = mergeAllList(head, k); 

    // Print final sorted list 
    printList(finalList); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python program to merge K sorted doubly 
# linked list in sorted order 

# A linked list node 
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None
        self.prev = None

# Given a reference (pointer to pointer) to the head 
# Of a DLL and an int, appends a new node at the end 
def append(head_ref, new_data): 

    # Allocate node 
    new_node = Node(0) 

    last = head_ref 

    # Put in the data 
    new_node.data = new_data 

    # This new node is going to be the last 
    # node, so make next of it as None 
    new_node.next = None

    # If the Linked List is empty, then make 
    # the new node as head */ 
    if (head_ref == None) : 
        new_node.prev = None
        head_ref = new_node 
        return head_ref 

    # Else traverse till the last node 
    while (last.next != None): 
        last = last.next

    # Change the next of last node 
    last.next = new_node 

    # Make last node as previous of new node 
    new_node.prev = last 

    return head_ref 

# Function to print the list 
def printList(node): 

    last = None

    # Run while loop unless node becomes None 
    while (node != None) : 

        print( node.data, end = " ") 
        last = node 
        node = node.next

# Function to merge two 
# sorted doubly linked lists 
def mergeList(p, q): 

    s = None

    # If any of the list is empty 
    if (p == None or q == None) : 

        if (p == None ): 
            return q  
        else: 
            return p 

    # Comparison the data of two linked list 
    if (p.data < q.data): 
        p.prev = s 
        s = p 
        p = p.next

    else: 
        q.prev = s 
        s = q 
        q = q.next

    # Store head pointer before merge the list 
    head = s 
    while (p != None and q != None) : 

        if (p.data < q.data) : 

            # Changing of pointer between 
            # Two list for merging 
            s.next = p 
            p.prev = s 
            s = s.next
            p = p.next

        else: 
            # Changing of pointer between 
            # Two list for merging 
            s.next = q 
            q.prev = s 
            s = s.next
            q = q.next

    # Condition to check if any anyone list not end 
    if (p == None): 
        s.next = q 
        q.prev = s 

    if (q == None): 
        s.next = p 
        p.prev = s 

    # Return head pointer of merged list 
    return head 

# Function to merge all sorted linked 
# list in sorted order 
def mergeAllList(head,k): 

    finalList = None
    i = 0
    while ( i < k ) : 

        # Function call to merge two sorted 
        # doubly linked list at a time 
        finalList = mergeList(finalList, head[i]) 
        i = i + 1

    # Return final sorted doubly linked list 
    return finalList 

# Driver code 

k = 3
head = [0] * k 
i = 0

# Loop to initialize all the lists to empty 
while ( i < k ) : 

    head[i] = None
    i = i + 1

# Create first doubly linked List 
# List1 . 1 <=> 5 <=> 9 
head[0] = append(head[0], 1) 
head[0] = append(head[0], 5) 
head[0] = append(head[0], 9) 

# Create second doubly linked List 
# List2 . 2 <=> 3 <=> 7 <=> 12 
head[1] = append(head[1], 2) 
head[1] = append(head[1], 3) 
head[1] = append(head[1], 7) 
head[1] = append(head[1], 12) 

# Create third doubly linked List 
# List3 . 8 <=> 11 <=> 13 <=> 18 
head[2] = append(head[2], 8) 
head[2] = append(head[2], 11) 
head[2] = append(head[2], 13) 
head[2] = append(head[2], 18) 

# Function call to merge all sorted 
# doubly linked lists in sorted order 
finalList = mergeAllList(head, k) 

# Print final sorted list 
printList(finalList) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to merge K sorted doubly  
// linked list in sorted order 
using System; 

class GFG  
{  

    // A linked list node  
    public class Node  
    {  
        public int data;  
        public Node next;  
        public Node prev;  
    };  

    // Given a reference (pointer to pointer)  
    // to the head of a DLL and an int,  
    // appends a new node at the end  
    static Node append(Node head_ref,  
                       int new_data)  
    {  
        // Allocate node  
        Node new_node = new Node();  

        Node last = head_ref;  

        // Put in the data  
        new_node.data = new_data;  

        // This new node is going to be the last  
        // node, so make next of it as null  
        new_node.next = null;  

        // If the Linked List is empty,  
        // then make the new node as head */  
        if (head_ref == null)  
        {  
            new_node.prev = null;  
            head_ref = new_node;  
            return head_ref;  
        }  

        // Else traverse till the last node  
        while (last.next != null)  
            last = last.next;  

        // Change the next of last node  
        last.next = new_node;  

        // Make last node as previous of new node  
        new_node.prev = last;  

        return head_ref;  
    }  

    // Function to print the list  
    static void printList(Node node)  
    {  
        Node last;  

        // Run while loop unless node becomes null  
        while (node != null)  
        {  
            Console.Write(node.data + " ");  
            last = node;  
            node = node.next;  
        }  
    }  

    // Function to merge two  
    // sorted doubly linked lists  
    static Node mergeList(Node p, Node q)  
    {  
        Node s = null;  

        // If any of the list is empty  
        if (p == null || q == null)  
        {  
            return (p == null ? q : p);  
        }  

        // Comparison the data of two linked list  
        if (p.data < q.data)  
        {  
            p.prev = s;  
            s = p;  
            p = p.next;  
        }  
        else
        {  
            q.prev = s;  
            s = q;  
            q = q.next;  
        }  

        // Store head pointer before merge the list  
        Node head = s;  
        while (p != null && q != null)  
        {  
            if (p.data < q.data)  
            {  

                // Changing of pointer between  
                // Two list for merging  
                s.next = p;  
                p.prev = s;  
                s = s.next;  
                p = p.next;  
            }  
            else
            {  

                // Changing of pointer between  
                // Two list for merging  
                s.next = q;  
                q.prev = s;  
                s = s.next;  
                q = q.next;  
            }  
        }  

        // Condition to check if 
        // any anyone list not end  
        if (p == null)  
        {  
            s.next = q;  
            q.prev = s;  
        }  
        if (q == null)  
        {  
            s.next = p;  
            p.prev = s;  
        }  

        // Return head pointer of merged list  
        return head;  
    }  

    // Function to merge all sorted linked  
    // list in sorted order  
    static Node mergeAllList(Node []head, int k)  
    {  
        Node finalList = null;  
        for (int i = 0; i < k; i++)  
        {  

            // Function call to merge two sorted  
            // doubly linked list at a time  
            finalList = mergeList(finalList,  
                                   head[i]);  
        }  

        // Return final sorted doubly linked list  
        return finalList;  
    }  

    // Driver code  
    public static void Main()  
    {  
        int k = 3;  
        Node []head = new Node[k];  

        // Loop to initialize all the lists to empty  
        for (int i = 0; i < k; i++)  
        {  
            head[i] = null;  
        }  

        // Create first doubly linked List  
        // List1 . 1 <=> 5 <=> 9  
        head[0] = append(head[0], 1);  
        head[0] = append(head[0], 5);  
        head[0] = append(head[0], 9);  

        // Create second doubly linked List  
        // List2 . 2 <=> 3 <=> 7 <=> 12  
        head[1] = append(head[1], 2);  
        head[1] = append(head[1], 3);  
        head[1] = append(head[1], 7);  
        head[1] = append(head[1], 12);  

        // Create third doubly linked List  
        // List3 . 8 <=> 11 <=> 13 <=> 18  
        head[2] = append(head[2], 8);  
        head[2] = append(head[2], 11);  
        head[2] = append(head[2], 13);  
        head[2] = append(head[2], 18);  

        // Function call to merge all sorted  
        // doubly linked lists in sorted order  
        Node finalList = mergeAllList(head, k);  

        // Print final sorted list  
        printList(finalList);  
    }  
} 

// This code is contributed by AnkitRai01 

```

**输出**：

```
1 2 3 5 7 8 9 11 12 13 18

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。