# 具有头和尾指针的双向链表中的排序插入

> 原文：[https://www.geeksforgeeks.org/create-doubly-linked-list-using-double-pointer-inserting-nodes-list-remains-ascending-order/](https://www.geeksforgeeks.org/create-doubly-linked-list-using-double-pointer-inserting-nodes-list-remains-ascending-order/)

[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)是由一组顺序链接的记录（称为节点）组成的链表。 每个节点包含两个字段，这些字段引用节点序列中的上一个节点和下一个节点。

任务是通过插入节点来创建双向链表，以使列表在打印时从左到右保持升序。 同样，我们需要维护两个指针，头（指向第一个节点的点）和尾（指向最后一个节点的点）。

**示例**：

```
Input : 40 50 10 45 90 100 95
Output :10 40 45 50 90 95 100

Input : 30 10 50 43 56 12
Output :10 12 30 43 50 56

```

**算法**：

该任务可以通过以下方式完成：

1.  如果“链表”为空，则使左指针和右指针都指向要插入的节点，并使它的上一个和下一个字段指向 NULL。

2.  如果要插入的节点的值小于链表的第一个节点的值，则从第一个节点的前一个字段连接该节点。

3.  如果要插入的节点的值大于链表的最后一个节点的值，则从最后一个节点的下一个字段连接该节点。

4.  如果要插入的节点的值在第一个节点与最后一个节点的值之间，则检查适当的位置并建立连接。

## C++

```cpp

/* C++ program to insetail nodes in doubly  
linked list such that list remains in  
ascending order on printing from left  
to right */
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node  
class Node  
{  
    public: 
    Node *prev;  
    int info;  
    Node *next;  
};  

// Function to insetail new node  
void nodeInsetail(Node **head,  
                Node **tail,  
                int key)  
{  

    Node *p = new Node();  
    p->info = key;  
    p->next = NULL;  

    // If first node to be insetailed in doubly  
    // linked list  
    if ((*head) == NULL)  
    {  
        (*head) = p;  
        (*tail) = p;  
        (*head)->prev = NULL;  
        return;  
    }  

    // If node to be insetailed has value less  
    // than first node  
    if ((p->info) < ((*head)->info))  
    {  
        p->prev = NULL;  
        (*head)->prev = p;  
        p->next = (*head);  
        (*head) = p;  
        return;  
    }  

    // If node to be insetailed has value more  
    // than last node  
    if ((p->info) > ((*tail)->info))  
    {  
        p->prev = (*tail);  
        (*tail)->next = p;  
        (*tail) = p;  
        return;  
    }  

    // Find the node before which we need to  
    // insert p.  
    Node *temp = (*head)->next;  
    while ((temp->info) < (p->info))  
        temp = temp->next;  

    // Insert new node before temp  
    (temp->prev)->next = p;  
    p->prev = temp->prev;  
    temp->prev = p;  
    p->next = temp;  
}  

// Function to print nodes in from left to right  
void printList(Node *temp)  
{  
    while (temp != NULL)  
    {  
        cout << temp->info << " ";  
        temp = temp->next;  
    }  
}  

// Driver program to test above functions  
int main()  
{  
    Node *left = NULL, *right = NULL;  
    nodeInsetail(&left, &right, 30);  
    nodeInsetail(&left, &right, 50);  
    nodeInsetail(&left, &right, 90);  
    nodeInsetail(&left, &right, 10);  
    nodeInsetail(&left, &right, 40);  
    nodeInsetail(&left, &right, 110);  
    nodeInsetail(&left, &right, 60);  
    nodeInsetail(&left, &right, 95);  
    nodeInsetail(&left, &right, 23);  

    cout<<"Doubly linked list on printing"
        " from left to right\n";  
    printList(left);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

/* C program to insetail nodes in doubly 
linked list such that list remains in 
ascending order on printing from left 
to right */
#include<stdio.h> 
#include<stdlib.h> 

// A linked list node 
struct Node 
{ 
    struct Node *prev; 
    int info; 
    struct Node *next; 
}; 

// Function to insetail new node 
void nodeInsetail(struct Node **head, 
                  struct Node **tail, 
                  int key) 
{ 

    struct Node *p = new Node; 
    p->info = key; 
    p->next = NULL; 

    // If first node to be insetailed in doubly 
    // linked list 
    if ((*head) == NULL) 
    { 
        (*head) = p; 
        (*tail) = p; 
        (*head)->prev = NULL; 
        return; 
    } 

    // If node to be insetailed has value less 
    // than first node 
    if ((p->info) < ((*head)->info)) 
    { 
        p->prev = NULL; 
        (*head)->prev = p; 
        p->next = (*head); 
        (*head) = p; 
        return; 
    } 

    // If node to be insetailed has value more 
    // than last node 
    if ((p->info) > ((*tail)->info)) 
    { 
        p->prev = (*tail); 
        (*tail)->next = p; 
        (*tail) = p; 
        return; 
    } 

    // Find the node before which we need to 
    // insert p. 
    temp = (*head)->next; 
    while ((temp->info) < (p->info)) 
        temp = temp->next; 

    // Insert new node before temp 
    (temp->prev)->next = p; 
    p->prev = temp->prev; 
    temp->prev = p; 
    p->next = temp; 
} 

// Function to print nodes in from left to right 
void printList(struct Node *temp) 
{ 
    while (temp != NULL) 
    { 
        printf("%d ", temp->info); 
        temp = temp->next; 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Node *left = NULL, *right = NULL; 
    nodeInsetail(&left, &right, 30); 
    nodeInsetail(&left, &right, 50); 
    nodeInsetail(&left, &right, 90); 
    nodeInsetail(&left, &right, 10); 
    nodeInsetail(&left, &right, 40); 
    nodeInsetail(&left, &right, 110); 
    nodeInsetail(&left, &right, 60); 
    nodeInsetail(&left, &right, 95); 
    nodeInsetail(&left, &right, 23); 

    printf("\nDoubly linked list on printing"
           " from left to right\n"); 
    printList(left); 

    return 0; 
} 

```

## Java

```java

/* Java program to insetail nodes in doubly  
linked list such that list remains in  
ascending order on printing from left  
to right */

import java.io.*; 
import java.util.*; 

// A linked list node 
class Node 
{ 
    int info; 
    Node prev, next; 
} 

class GFG 
{ 

    static Node head, tail; 

    // Function to insetail new node  
    static void nodeInsetail(int key) 
    { 
        Node p = new Node(); 
        p.info = key; 
        p.next = null; 

        // If first node to be insetailed in doubly  
        // linked list 
        if (head == null) 
        { 
            head = p; 
            tail = p; 
            head.prev = null; 
            return; 
        } 

        // If node to be insetailed has value less  
        // than first node  
        if (p.info < head.info) 
        { 
            p.prev = null; 
            head.prev = p; 
            p.next = head; 
            head = p; 
            return; 
        } 

        // If node to be insetailed has value more  
        // than last node  
        if (p.info > tail.info) 
        { 
            p.prev = tail; 
            tail.next = p; 
            tail = p; 
            return; 
        } 

        // Find the node before which we need to  
        // insert p. 
        Node temp = head.next; 
        while (temp.info < p.info) 
                temp = temp.next; 

        // Insert new node before temp  
        (temp.prev).next = p; 
        p.prev = temp.prev; 
        temp.prev = p; 
        p.next = temp; 
    } 

    // Function to print nodes in from left to right 
    static void printList(Node temp) 
    { 
        while (temp != null) 
        { 
                System.out.print(temp.info + " "); 
                temp = temp.next; 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        head = tail = null; 
        nodeInsetail(30); 
        nodeInsetail(50); 
        nodeInsetail(90); 
        nodeInsetail(10); 
        nodeInsetail(40); 
        nodeInsetail(110); 
        nodeInsetail(60); 
        nodeInsetail(95); 
        nodeInsetail(23); 

        System.out.println("Doubly linked list on printing from left to right"); 
        printList(head);  
    } 
} 

// This code is contributed by rachana soma 

```

## Python

```py

# Python program to insetail nodes in doubly  
# linked list such that list remains in  
# ascending order on printing from left  
# to right  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.info = data  
        self.next = None
        self.prev = None

head = None
tail = None

# Function to insetail new node  
def nodeInsetail( key) : 

    global head 
    global tail 

    p = Node(0)  
    p.info = key  
    p.next = None

    # If first node to be insetailed in doubly  
    # linked list  
    if ((head) == None) : 
        (head) = p  
        (tail) = p  
        (head).prev = None
        return

    # If node to be insetailed has value less  
    # than first node  
    if ((p.info) < ((head).info)) : 
        p.prev = None
        (head).prev = p  
        p.next = (head)  
        (head) = p  
        return

    # If node to be insetailed has value more  
    # than last node  
    if ((p.info) > ((tail).info)) : 

        p.prev = (tail)  
        (tail).next = p  
        (tail) = p  
        return

    # Find the node before which we need to  
    # insert p.  
    temp = (head).next
    while ((temp.info) < (p.info)) : 
        temp = temp.next

    # Insert new node before temp  
    (temp.prev).next = p  
    p.prev = temp.prev  
    temp.prev = p  
    p.next = temp  

# Function to print nodes in from left to right  
def printList(temp) : 

    while (temp != None) : 

        print( temp.info, end = " ")  
        temp = temp.next

# Driver program to test above functions  
nodeInsetail( 30)  
nodeInsetail( 50)  
nodeInsetail( 90)  
nodeInsetail( 10)  
nodeInsetail( 40)  
nodeInsetail( 110)  
nodeInsetail( 60)  
nodeInsetail( 95)  
nodeInsetail( 23)  

print("Doubly linked list on printing from left to right\n" ) 

printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

/* C# program to insetail nodes in doubly  
linked list such that list remains in  
ascending order on printing from left  
to right */
using System;  

// A linked list node  
public class Node  
{  
    public int info;  
    public Node prev, next;  
}  

class GFG  
{  

    static Node head, tail;  

    // Function to insetail new node  
    static void nodeInsetail(int key)  
    {  
        Node p = new Node();  
        p.info = key;  
        p.next = null;  

        // If first node to be insetailed in doubly  
        // linked list  
        if (head == null)  
        {  
            head = p;  
            tail = p;  
            head.prev = null;  
            return;  
        }  

        // If node to be insetailed has value less  
        // than first node  
        if (p.info < head.info)  
        {  
            p.prev = null;  
            head.prev = p;  
            p.next = head;  
            head = p;  
            return;  
        }  

        // If node to be insetailed has value more  
        // than last node  
        if (p.info > tail.info)  
        {  
            p.prev = tail;  
            tail.next = p;  
            tail = p;  
            return;  
        }  

        // Find the node before which we need to  
        // insert p.  
        Node temp = head.next;  
        while (temp.info < p.info)  
            temp = temp.next;  

        // Insert new node before temp  
        (temp.prev).next = p;  
        p.prev = temp.prev;  
        temp.prev = p;  
        p.next = temp;  
    }  

    // Function to print nodes in from left to right  
    static void printList(Node temp)  
    {  
        while (temp != null)  
        {  
            Console.Write(temp.info + " ");  
            temp = temp.next;  
        }  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        head = tail = null;  
        nodeInsetail(30);  
        nodeInsetail(50);  
        nodeInsetail(90);  
        nodeInsetail(10);  
        nodeInsetail(40);  
        nodeInsetail(110);  
        nodeInsetail(60);  
        nodeInsetail(95);  
        nodeInsetail(23);  

        Console.WriteLine("Doubly linked list on printing from left to right");  
        printList(head);  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Doubly linked list on printing from left to right
10 23 30 40 50 60 90 95 110

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。