# 循环链表 | 系列 2（遍历）

> 原文：[https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)

我们在上一则关于循环链表的文章中讨论了[循环链表的介绍和应用，](http://quiz.geeksforgeeks.org/circular-linked-list/ "Permanent link to Circular Linked List | Set 1 (Introduction and Applications)") 。 在这篇文章中，讨论了遍历操作。

![](img/ff7f30aebf5dc865587c7829dcf4233c.png "cll")

在常规的链表中，我们从头节点遍历该列表，并在到达`NULL`时停止遍历。 在循环链表中，当再次到达第一个节点时，我们将停止遍历。 以下是用于链表遍历的 C 代码。

```

/* Function to traverse a given Circular linked list and print nodes */
void printList(struct Node *first) 
{ 
    struct Node *temp = first;  

    // If linked list is not empty 
    if (first != NULL)  
    { 
        // Keep printing nodes till we reach the first node again 
        do
        { 
            printf("%d ", temp->data); 
            temp = temp->next; 
        } 
        while (temp != first); 
    } 
} 

```

**演示遍历的完整程序。** 以下是演示遍历循环链表的完整程序。

## C++

```cpp

// C++ program to implement  
// the above approach  
#include <bits/stdc++.h> 
using namespace std; 

/* structure for a node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Function to insert a node at the beginning  
of a Circular linked list */
void push(Node **head_ref, int data)  
{  
    Node *ptr1 = new Node(); 
    Node *temp = *head_ref;  
    ptr1->data = data;  
    ptr1->next = *head_ref;  

    /* If linked list is not NULL then  
    set the next of last node */
    if (*head_ref != NULL)  
    {  
        while (temp->next != *head_ref)  
            temp = temp->next;  
        temp->next = ptr1;  
    }  
    else
        ptr1->next = ptr1; /*For the first node */

    *head_ref = ptr1;  
}  

/* Function to print nodes in  
a given Circular linked list */
void printList(Node *head)  
{  
    Node *temp = head;  
    if (head != NULL)  
    {  
        do
        {  
            cout << temp->data << " ";  
            temp = temp->next;  
        }  
        while (temp != head);  
    }  
}  

/* Driver program to test above functions */
int main()  
{  
    /* Initialize lists as empty */
    Node *head = NULL;  

    /* Created linked list will be 11->2->56->12 */
    push(&head, 12);  
    push(&head, 56);  
    push(&head, 2);  
    push(&head, 11);  

    cout << "Contents of Circular Linked List\n ";  
    printList(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to implement 
// the above approach 
#include<stdio.h> 
#include<stdlib.h> 

/* structure for a node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Function to insert a node at the beginning of a Circular 
   linked list */
void push(struct Node **head_ref, int data) 
{ 
    struct Node *ptr1 = (struct Node *)malloc(sizeof(struct Node)); 
    struct Node *temp = *head_ref; 
    ptr1->data = data; 
    ptr1->next = *head_ref; 

    /* If linked list is not NULL then set the next of last node */
    if (*head_ref != NULL) 
    { 
        while (temp->next != *head_ref) 
            temp = temp->next; 
        temp->next = ptr1; 
    } 
    else
        ptr1->next = ptr1; /*For the first node */

    *head_ref = ptr1; 
} 

/* Function to print nodes in a given Circular linked list */
void printList(struct Node *head) 
{ 
    struct Node *temp = head; 
    if (head != NULL) 
    { 
        do
        { 
            printf("%d ", temp->data); 
            temp = temp->next; 
        } 
        while (temp != head); 
    } 
} 

/* Driver program to test above functions */
int main() 
{ 
    /* Initialize lists as empty */
    struct Node *head = NULL; 

    /* Created linked list will be 11->2->56->12 */
    push(&head, 12); 
    push(&head, 56); 
    push(&head, 2); 
    push(&head, 11); 

    printf("Contents of Circular Linked List\n "); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
class GFG 
{ 

// node  
static class Node 
{ 
    int data; 
    Node next; 
}; 

/* Function to insert a node 
at the beginning of a Circular 
linked list */
static Node push(Node head_ref,  
                 int data) 
{ 
    Node ptr1 = new Node(); 
    Node temp = head_ref; 
    ptr1.data = data; 
    ptr1.next = head_ref; 

    /* If linked list is not null  
    then set the next of last node */
    if (head_ref != null) 
    { 
        while (temp.next != head_ref) 
            temp = temp.next; 
        temp.next = ptr1; 
    } 
    else
        ptr1.next = ptr1;  

    head_ref = ptr1; 

    return head_ref; 
} 

/* Function to print nodes in a  
given Circular linked list */
static void printList(Node head) 
{ 
    Node temp = head; 
    if (head != null) 
    { 
        do
        { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        while (temp != head); 
    } 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    /* Initialize lists as empty */
    Node head = null; 

    /* Created linked list will 
       be 11.2.56.12 */
    head = push(head, 12); 
    head = push(head, 56); 
    head = push(head, 2); 
    head = push(head, 11); 

    System.out.println("Contents of Circular " +  
                                "Linked List:"); 
    printList(head); 
} 
} 

// This code is contributed 
// by Arnab Kundu 

```

## Python

```py

# Python program to demonstrate  
# circular linked list traversal  

# Structure for a Node 
class Node: 

    # Constructor to create  a new node 
    def __init__(self, data): 
        self.data = data  
        self.next = None

class CircularLinkedList: 

    # Constructor to create a empty circular linked list 
    def __init__(self): 
        self.head = None

    # Function to insert a node at the beginning of a 
    # circular linked list 
    def push(self, data): 
        ptr1 = Node(data) 
        temp = self.head 

        ptr1.next = self.head 

        # If linked list is not None then set the next of 
        # last node 
        if self.head is not None: 
            while(temp.next != self.head): 
                temp = temp.next 
            temp.next = ptr1 

        else: 
            ptr1.next = ptr1 # For the first node 

        self.head = ptr1  

    # Function to print nodes in a given circular linked list 
    def printList(self): 
        temp = self.head 
        if self.head is not None: 
            while(True): 
                print "%d" %(temp.data), 
                temp = temp.next
                if (temp == self.head): 
                    break 

# Driver program to test above function 

# Initialize list as empty 
cllist = CircularLinkedList() 

# Created linked list will be 11->2->56->12 
cllist.push(12) 
cllist.push(56) 
cllist.push(2) 
cllist.push(11) 

print "Contents of circular Linked List"
cllist.printList() 

# This code is contributed by  
# Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# program to implement  
// the above approach  
using System; 
class GFG  
{  

// node  
class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to insert a node  
at the beginning of a Circular  
linked list */
static Node push(Node head_ref,  
                int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    /* If linked list is not null  
    then set the next of last node */
    if (head_ref != null)  
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
    }  
    else
        ptr1.next = ptr1;  

    head_ref = ptr1;  

    return head_ref;  
}  

/* Function to print nodes in a  
given Circular linked list */
static void printList(Node head)  
{  
    Node temp = head;  
    if (head != null)  
    {  
        do
        {  
            Console.Write(temp.data + " ");  
            temp = temp.next;  
        }  
        while (temp != head);  
    }  
}  

// Driver Code  
static public void Main(String []args)  
{  
    /* Initialize lists as empty */
    Node head = null;  

    /* Created linked list will  
    be 11.2.56.12 */
    head = push(head, 12);  
    head = push(head, 56);  
    head = push(head, 2);  
    head = push(head, 11);  

    Console.WriteLine("Contents of Circular " +  
                                "Linked List:");  
    printList(head);  
}  
}  

// This code is contributed  
// by Arnab Kundu  

```

**输出**：

```
Contents of Circular Linked List
11 2 56 12

```

**您可能想在循环链表**

[上将以下帖子分为两半](https://www.geeksforgeeks.org/split-a-circular-linked-list-into-two-halves/)

[循环链表](https://www.geeksforgeeks.org/sorted-insert-for-circular-linked-list/)的插入内容

我们将很快讨论循环链表的插入删除操作的实现。

如果您发现上述代码/算法中的任何错误，或找到其他解决相同问题的方法，请发表评论

