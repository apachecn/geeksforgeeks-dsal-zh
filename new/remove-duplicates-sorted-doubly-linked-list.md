# 从排序的双向链表

> 原文：[https://www.geeksforgeeks.org/remove-duplicates-sorted-doubly-linked-list/](https://www.geeksforgeeks.org/remove-duplicates-sorted-doubly-linked-list/)

中删除重复项

给定一个包含 **n** 个节点的排序的双链表。 问题是从给定列表中删除重复的节点。

示例：

![](img/181efe33bce5e24ea889657c966ce9a2.png)

**算法**：，

```
removeDuplicates(head_ref, x)
      if head_ref == NULL
          return
      Initialize current = head_ref
      while current->next != NULL
           if current->data == current->next->data
               deleteNode(head_ref, current->next)
           else
               current = current->next

```

在此帖子的[中讨论了 **deleteNode（head_ref，current）**（使用指向该节点的指针删除该节点）的算法。](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/) 

## C++

```cpp

/* C++ implementation to remove duplicates from a  
   sorted doubly linked list */
#include <bits/stdc++.h> 

using namespace std; 

/* a node of the doubly linked list */
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

/* Function to delete a node in a Doubly Linked List. 
   head_ref --> pointer to head node pointer. 
   del  -->  pointer to node to be deleted. */
void deleteNode(struct Node** head_ref, struct Node* del) 
{ 
    /* base case */
    if (*head_ref == NULL || del == NULL) 
        return; 

    /* If node to be deleted is head node */
    if (*head_ref == del) 
        *head_ref = del->next; 

    /* Change next only if node to be deleted  
        is NOT the last node */
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    /* Change prev only if node to be deleted  
       is NOT the first node */
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    /* Finally, free the memory occupied by del*/
    free(del); 
} 

/* function to remove duplicates from a  
   sorted doubly linked list */
void removeDuplicates(struct Node** head_ref) 
{ 
    /* if list is empty */
    if ((*head_ref) == NULL) 
        return; 

    struct Node* current = *head_ref; 
    struct Node* next; 

    /* traverse the list till the last node */
    while (current->next != NULL) { 

        /* Compare current node with next node */
        if (current->data == current->next->data) 

            /* delete the node pointed to by 
              'current->next' */
            deleteNode(head_ref, current->next); 

        /* else simply move to the next node */
        else
            current = current->next; 
    } 
} 

/* Function to insert a node at the beginning  
   of the Doubly Linked List */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node =  
           (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* since we are adding at the begining, 
    prev is always NULL */
    new_node->prev = NULL; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* change prev of head node to new node */
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given doubly linked list */
void printList(struct Node* head) 
{ 
    /* if list is empty */
    if (head == NULL) 
        cout << "Doubly Linked list empty"; 

    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Create the doubly linked list: 
     4<->4<->4<->4<->6<->8<->8<->10<->12<->12 */
    push(&head, 12); 
    push(&head, 12); 
    push(&head, 10); 
    push(&head, 8); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 4); 
    push(&head, 4); 
    push(&head, 4); 

    cout << "Original Doubly linked list:n"; 
    printList(head); 

    /* remove duplicate nodes */
    removeDuplicates(&head); 

    cout << "\nDoubly linked list after"
             " removing duplicates:n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

/* Java implementation to remove duplicates from a   
   sorted doubly linked list */
public class removeDuplicatesFromSortedList { 

    /* function to remove duplicates from a   
   sorted doubly linked list */
    public static void removeDuplicates(Node head)  
    {  
        /* if list is empty */
        if (head== null)  
            return;  

        Node current = head;  

        /* traverse the list till the last node */
        while (current.next != null)  
        {  
            /* Compare current node with next node */
            if (current.data == current.next.data)  
                /* delete the node pointed to by  
              ' current->next' */
                deleteNode(head, current.next);  

            /* else simply move to the next node */
            else
                current = current.next;  
        }   

    }  

    /* Function to delete a node in a Doubly Linked List.  
    head_ref --> pointer to head node pointer.  
    del  -->  pointer to node to be deleted. */
    public static void deleteNode(Node head, Node del) 
    { 
         /* base case */
        if(head==null || del==null) 
        { 
            return ; 
        } 
        /* If node to be deleted is head node */
        if(head==del) 
        { 
            head=del.next; 
        } 
        /* Change next only if node to be deleted   
        is NOT the last node */
        if(del.next!=null) 
        { 
            del.next.prev=del.prev; 
        } 
        /* Change prev only if node to be deleted   
       is NOT the first node */
        if (del.prev != null)  
            del.prev.next = del.next;  

    } 

    /* Function to insert a node at the beginning   
    of the Doubly Linked List */
    public static Node push(Node head, int data) 
    { 
        /* allocate node */
        Node newNode=new Node(data); 
        /* since we are adding at the begining,  
        prev is always NULL */
        newNode.prev=null; 
        /* link the old list off the new node */
        newNode.next =head;  
        /* change prev of head node to new node */
        if(head!=null) 
        { 
            head.prev=newNode; 
        } 
        head=newNode; 
        return head; 
    } 

    /* Function to print nodes in a given doubly linked list */
    public static void printList(Node head) 
    { 
        if (head == null)  
            System.out.println("Doubly Linked list empty"); 

        while (head != null)  
        {  
            System.out.print(head.data+" ") ; 
            head = head.next;  
        } 
    } 

    public static void main(String args[]) { 
        Node head=null; 
        head=push(head, 12);  
        head=push(head, 12);  
        head=push(head, 10);  
        head=push(head, 8);  
        head=push(head, 8);  
        head=push(head, 6);  
        head=push(head, 4);  
        head=push(head, 4);  
        head=push(head, 4);  
        head=push(head, 4); 

        System.out.println("Original Doubly LinkedList"); 
        printList(head);  

        /* remove duplicate nodes */
        removeDuplicates(head);  
        System.out.println("\nDoubly linked list after removing duplicates:"); 
        printList(head); 
    } 
} 
class Node 
{ 
    int data; 
    Node next,prev; 

    Node(int data) 
    { 
        this.data=data; 
        next=null; 
        prev=null; 
    } 
} 
//This code is contributed by Gaurav Tiwari 

```

## Python

```py

# Python implementation to remove duplicates from a  
# sorted doubly linked list  

# A linked list node 
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None
        self.prev = None

# Function to _delete a node in a Doubly Linked List. 
# head_ref -. pointer to head node pointer. 
# _del -. pointer to node to be _deleted.  
def _deleteNode(head_ref, _del): 

    # base case  
    if (head_ref == None or _del == None): 
        return

    # If node to be _deleted is head node  
    if (head_ref == _del): 
        head_ref = _del.next

    # Change next only if node to be _deleted  
    # is NOT the last node  
    if (_del.next != None): 
        _del.next.prev = _del.prev 

    # Change prev only if node to be _deleted  
    # is NOT the first node  
    if (_del.prev != None): 
        _del.prev.next = _del.next

    return head_ref 

# function to remove duplicates from a  
# sorted doubly linked list  
def removeDuplicates(head_ref): 

    # if list is empty  
    if ((head_ref) == None): 
        return None

    current = head_ref 
    next = None

    # traverse the list till the last node  
    while (current.next != None) : 

        # Compare current node with next node  
        if (current.data == current.next.data): 

            # _delete the node pointed to by 
            # 'current.next'  
            _deleteNode(head_ref, current.next) 

        # else simply move to the next node  
        else: 
            current = current.next

    return head_ref 

# Function to insert a node at the beginning  
# of the Doubly Linked List  
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # since we are adding at the begining, 
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

# Function to print nodes in a given doubly linked list  
def printList(head): 

    # if list is empty  
    if (head == None): 
        print("Doubly Linked list empty") 

    while (head != None) : 
        print(head.data, end = " ") 
        head = head.next

# Driver program to test above functions 

# Start with the empty list  
head = None

# Create the doubly linked list: 
# 4<->4<->4<->4<->6<->8<->8<->10<->12<->12  
head = push(head, 12) 
head = push(head, 12) 
head = push(head, 10) 
head = push(head, 8) 
head = push(head, 8) 
head = push(head, 6) 
head = push(head, 4) 
head = push(head, 4) 
head = push(head, 4) 
head = push(head, 4) 

print( "Original Doubly linked list:\n") 
printList(head) 

# remove duplicate nodes  
head = removeDuplicates(head) 

print("\nDoubly linked list after removing duplicates:") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

/* C# implementation to remove duplicates from a  
sorted doubly linked list */
using System;  

public class removeDuplicatesFromSortedList  
{  

    /* function to remove duplicates from a  
    sorted doubly linked list */
    public static void removeDuplicates(Node head)  
    {  
        /* if list is empty */
        if (head == null)  
            return;  

        Node current = head;   

        /* traverse the list till the last node */
        while (current.next != null)  
        {  

            /* Compare current node with next node */
            if (current.data == current.next.data)  

            /* delete the node pointed to by  
            'current->next' */
                deleteNode(head, current.next);  

            /* else simply move to the next node */
            else
                current = current.next;  
        }  
    }  

    /* Function to delete a node in a Doubly Linked List.  
    head_ref --> pointer to head node pointer.  
    del --> pointer to node to be deleted. */
    public static void deleteNode(Node head, Node del)  
    {  
        /* base case */
        if(head == null || del == null)  
        {  
            return ;  
        }  

        /* If node to be deleted is head node */
        if(head == del)  
        {  
            head = del.next;  
        }  

        /* Change next only if node to be deleted  
        is NOT the last node */
        if(del.next != null)  
        {  
            del.next.prev = del.prev;  
        }  

        /* Change prev only if node to be deleted  
        is NOT the first node */
        if (del.prev != null)  
            del.prev.next = del.next;  

    }  

    /* Function to insert a node at the beginning  
    of the Doubly Linked List */
    public static Node push(Node head, int data)  
    {  
        /* allocate node */
        Node newNode = new Node(data);  

        /* since we are adding at the begining,  
        prev is always NULL */
        newNode.prev = null;  

        /* link the old list off the new node */
        newNode.next = head;  

        /* change prev of head node to new node */
        if(head != null)  
        {  
            head.prev = newNode;  
        }  
        head = newNode;  
        return head;  
    }  

    /* Function to print nodes in a given doubly linked list */
    public static void printList(Node head)  
    {  
        if (head == null)  
            Console.WriteLine("Doubly Linked list empty");  

        while (head != null)  
        {  
            Console.Write(head.data + " ") ;  
            head = head.next;  
        }  
    }  

    // Driver code 
    public static void Main(String []args)  
    {  
        Node head = null;  
        head = push(head, 12);  
        head = push(head, 12);  
        head = push(head, 10);  
        head = push(head, 8);  
        head = push(head, 8);  
        head = push(head, 6);  
        head = push(head, 4);  
        head = push(head, 4);  
        head = push(head, 4);  
        head = push(head, 4);  

        Console.WriteLine("Original Doubly LinkedList");  
        printList(head);  

        /* remove duplicate nodes */
        removeDuplicates(head);  
        Console.WriteLine("\nDoubly linked list after" +  
                            "removing duplicates:");  
        printList(head);  
    }  
}  

public class Node  
{  
    public int data;  
    public Node next,prev;  

    public Node(int data)  
    {  
        this.data = data;  
        next = null;  
        prev = null;  
    }  
}  

// This code is contributed by 29AjayKumar. 

```

**输出**：

```
Original Doubly linked list:
4 4 4 4 6 8 8 10 12 12
Doubly linked list after removing duplicates:
4 6 8 10 12

```

**时间复杂度**：`O(n)`

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，也可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄到 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

