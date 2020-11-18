# 以相反的顺序打印双向链接列表

给定正整数的双链表。 任务是按照相反的顺序打印给定的双向链表数据。

**范例**：

```
Input: List = 1 <=> 2 <=>  3 <=>  4 <=>  5
Output: 5  4  3  2  1

Input: 10 <=> 20 <=> 30 <=> 40
Output: 40  30  20  10

```

**方法：**

*   用指针指向双向链表的头部。
*   现在，开始遍历链接列表，直到最后。
*   到达最后一个节点后，开始向后移动并同时打印该节点->数据。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to print doubly  
// linked list in reverse order  
#include <bits/stdc++.h> 
using namespace std; 

// Doubly linked list node 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

// Function to print nodes of Doubly  
// Linked List in reverse order  
void reversePrint(struct Node** head_ref) 
{ 
    struct Node* tail = *head_ref; 

    // Traversing till tail of the linked list 
    while (tail->next != NULL) { 
        tail = tail->next; 
    } 

    // Traversing linked list from tail 
    // and printing the node->data 
    while (tail != *head_ref) { 
        cout << tail->data << " "; 
        tail = tail->prev; 
    } 
    cout << tail->data << endl; 
} 

/* UTILITY FUNCTIONS */
// Function to insert a node at the  
// beginging of the Doubly Linked List  
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node  
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

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

// Driver Code 
int main() 
{ 
    // Start with the empty list  
    struct Node* head = NULL; 

    // Let us create a sorted linked list 
    // to test the functions  
    // Created linked list will be 10->8->4->2  
    push(&head, 2); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 10); 

    cout << "Linked List elements in reverse order : " << endl; 

    reversePrint(&head); 

    return 0; 
} 

```

## Java

```java

// Java Program to print doubly  
// linked list in reverse order  
class Sol 
{ 

// Doubly linked list node  
static class Node 
{  
    int data;  
    Node next;  
    Node prev;  
};  

// Function to print nodes of Doubly  
// Linked List in reverse order  
static void reversePrint( Node head_ref)  
{  
    Node tail = head_ref;  

    // Traversing till tail of the linked list  
    while (tail.next != null) 
    {  
        tail = tail.next;  
    }  

    // Traversing linked list from tail  
    // and printing the node.data  
    while (tail != head_ref) 
    {  
        System.out.print( tail.data + " ");  
        tail = tail.prev;  
    }  
    System.out.println( tail.data );  
}  

// UTILITY FUNCTIONS / 
// Function to insert a node at the  
// beginging of the Doubly Linked List  
static Node push( Node head_ref, int new_data)  
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

// Driver Code  
public static void main(String args[]) 
{  
    // Start with the empty list  
    Node head = null;  

    // Let us create a sorted linked list  
    // to test the functions  
    // Created linked list will be 10.8.4.2  
    head = push(head, 2);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 10);  

    System.out.print( "Linked List elements in reverse order : " );  

    reversePrint(head);  
}  
} 

// This code is contributed by Arnab Kundu  

```

## Python3

```py

# Python3 Program to print doubly  
# linked list in reverse order  
import math 

# Doubly linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to print nodes of Doubly  
# Linked List in reverse order  
def reversePrint(head_ref): 
    tail = head_ref 

    # Traversing till tail of the linked list 
    while (tail.next != None): 
        tail = tail.next

    # Traversing linked list from tail 
    # and pring the node.data 
    while (tail != head_ref): 
        print(tail.data, end = " ") 
        tail = tail.prev 

    print(tail.data) 

# UTILITY FUNCTIONS  
# Function to insert a node at the  
# beginging of the Doubly Linked List  
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    new_node.data = new_data 

    # since we are adding at the beginning,  
    # prev is always None  
    new_node.prev = None

    # link the old list off the new node  
    new_node.next = head_ref 

    # change prev of head node to new node  
    if (head_ref != None): 
        head_ref.prev = new_node 

    # move the head to po to the new node  
    head_ref = new_node 
    return head_ref 

# Driver Code 
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # Let us create a sorted linked list 
    # to test the functions  
    # Created linked list will be 10.8.4.2  
    head = push(head, 2)  
    head = push(head, 4)  
    head = push(head, 8)  
    head = push(head, 10) 

    print("Linked List elements in reverse order : ") 

    reversePrint(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# Program to print doubly  
// linked list in reverse order 
using System;      

class Sol 
{ 

// Doubly linked list node  
public class Node 
{  
    public int data;  
    public Node next;  
    public Node prev;  
};  

// Function to print nodes of Doubly  
// Linked List in reverse order  
static void reversePrint( Node head_ref)  
{  
    Node tail = head_ref;  

    // Traversing till tail of the linked list  
    while (tail.next != null) 
    {  
        tail = tail.next;  
    }  

    // Traversing linked list from tail  
    // and printing the node.data  
    while (tail != head_ref) 
    {  
        Console.Write( tail.data + " ");  
        tail = tail.prev;  
    }  
    Console.WriteLine( tail.data );  
}  

// UTILITY FUNCTIONS / 
// Function to insert a node at the  
// beginging of the Doubly Linked List  
static Node push( Node head_ref, int new_data)  
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

// Driver Code  
public static void Main(String []args) 
{  
    // Start with the empty list  
    Node head = null;  

    // Let us create a sorted linked list  
    // to test the functions  
    // Created linked list will be 10.8.4.2  
    head = push(head, 2);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 10);  

    Console.Write( "Linked List elements in reverse order : " );  

    reversePrint(head);  
}  
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
Linked List elements in reverse order : 
2 4 8 10

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。