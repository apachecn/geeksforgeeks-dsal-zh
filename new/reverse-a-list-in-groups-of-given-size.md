# 以给定大小的组反向链接列表| 设置1

给定一个链表，编写一个函数以反转每k个节点（其中k是该函数的输入）。

**示例：**

> **输入**：1- > 2- > 3- > 4- > 5- > 6- > 7- > 8- > NULL， K = 3
> **输出**：3- > 2- > 1- > 6- > 5- > 4- > 8- > 7 -> NULL
> 
> **输入**：1- > 2- > 3- > 4- > 5- > 6- > 7- > 8- > NULL， K = 5
> **输出**：5- > 4- > 3- > 2- > 1- > 8- > 7- > 6 -> NULL

**算法**： *[反向](https://www.geeksforgeeks.org/reverse-a-linked-list/)（头，k）*

*   反转大小为k的第一个子列表。 反转时，跟踪下一个节点和上一个节点。 令指向下一个节点的指针为，下一个，指向上一个节点的指针为 *prev* 。 有关反向链接列表的信息，请参见此帖子的[。](https://www.geeksforgeeks.org/reverse-a-linked-list/)
*   *head- > next = reverse（next，k）*（递归调用其余列表并链接两个子列表）
*   返回*上一个*（*上一个*成为列表的新标题（请参见[的迭代方法图）](https://www.geeksforgeeks.org/reverse-a-linked-list/)）

下图显示了反向功能的工作原理：

![](img/3f1748b21788d25062bb837e8bbde98b.png)

下面是上述方法的实现：

## C++

```cpp

// CPP program to reverse a linked list 
// in groups of given size  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Reverses the linked list in groups 
of size k and returns the pointer 
to the new head node. */
Node *reverse (Node *head, int k)  
{  
    Node* current = head;  
    Node* next = NULL;  
    Node* prev = NULL;  
    int count = 0;  

    /*reverse first k nodes of the linked list */
    while (current != NULL && count < k)  
    {  
        next = current->next;  
        current->next = prev;  
        prev = current;  
        current = next;  
        count++;  
    }  

    /* next is now a pointer to (k+1)th node  
    Recursively call for the list starting from current.  
    And make rest of the list as next of first node */
    if (next != NULL)  
    head->next = reverse(next, k);  

    /* prev is new head of the input list */
    return prev;  
}  

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node = new Node(); 

    /* put in the data */
    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);      

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Function to print linked list */
void printList(Node *node)  
{  
    while (node != NULL)  
    {  
        cout<<node->data<<" ";  
        node = node->next;  
    }  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Created Linked list is 1->2->3->4->5->6->7->8->9 */
    push(&head, 9);  
    push(&head, 8);  
    push(&head, 7);  
    push(&head, 6);  
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);      

    cout<<"Given linked list \n";  
    printList(head);  
    head = reverse(head, 3);  

    cout<<"\nReversed Linked list \n";  
    printList(head);  

    return(0);  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to reverse a linked list in groups of given size 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Reverses the linked list in groups of size k and returns the  
   pointer to the new head node. */
struct Node *reverse (struct Node *head, int k) 
{ 
    struct Node* current = head; 
    struct Node* next = NULL; 
    struct Node* prev = NULL; 
    int count = 0;    

    /*reverse first k nodes of the linked list */ 
    while (current != NULL && count < k) 
    { 
        next  = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
        count++; 
    } 

    /* next is now a pointer to (k+1)th node  
       Recursively call for the list starting from current. 
       And make rest of the list as next of first node */
    if (next !=  NULL) 
       head->next = reverse(next, k);  

    /* prev is new head of the input list */
    return prev; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref);     

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Function to print linked list */
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d  ", node->data); 
        node = node->next; 
    } 
}     

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

     /* Created Linked list is 1->2->3->4->5->6->7->8->9 */
     push(&head, 9); 
     push(&head, 8); 
     push(&head, 7); 
     push(&head, 6); 
     push(&head, 5); 
     push(&head, 4); 
     push(&head, 3); 
     push(&head, 2); 
     push(&head, 1);            

     printf("\nGiven linked list \n"); 
     printList(head); 
     head = reverse(head, 3); 

     printf("\nReversed Linked list \n"); 
     printList(head); 

     return(0); 
} 

```

## Java

```java

// Java program to reverse a linked list in groups of 
// given size 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) {data = d; next = null; } 
    } 

    Node reverse(Node head, int k) 
    { 
       Node current = head; 
       Node next = null; 
       Node prev = null; 

       int count = 0; 

       /* Reverse first k nodes of linked list */
       while (count < k && current != null)  
       { 
           next = current.next; 
           current.next = prev; 
           prev = current; 
           current = next; 
           count++; 
       } 

       /* next is now a pointer to (k+1)th node  
          Recursively call for the list starting from current. 
          And make rest of the list as next of first node */
       if (next != null)  
          head.next = reverse(next, k); 

       // prev is now head of input list 
       return prev; 
    }                       

    /* Utility functions */

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Function to print linked list */
    void printList() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
           System.out.print(temp.data+" "); 
           temp = temp.next; 
        }   
        System.out.println(); 
    } 

     /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Constructed Linked List is 1->2->3->4->5->6-> 
           7->8->8->9->null */
        llist.push(9); 
        llist.push(8); 
        llist.push(7); 
        llist.push(6); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Given Linked List"); 
        llist.printList(); 

        llist.head = llist.reverse(llist.head, 3); 

        System.out.println("Reversed list"); 
        llist.printList(); 
    } 
}  
/* This code is contributed by Rajat Mishra */

```

## 蟒蛇

```

# Python program to reverse a linked list in group of given size 

# Node class  
class Node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    def reverse(self, head, k): 
        current = head  
        next  = None
        prev = None
        count = 0 

        # Reverse first k nodes of the linked list 
        while(current is not None and count < k): 
            next = current.next
            current.next = prev 
            prev = current 
            current = next 
            count += 1

        # next is now a pointer to (k+1)th node 
        # recursively call for the list starting 
        # from current. And make rest of the list as 
        # next of first node 
        if next is not None: 
            head.next = self.reverse(next, k) 

        # prev is new head of the input list 
        return prev 

    # Function to insert a new node at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Utility function to print the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print temp.data, 
            temp = temp.next

# Driver program 
llist = LinkedList() 
llist.push(9) 
llist.push(8) 
llist.push(7) 
llist.push(6) 
llist.push(5) 
llist.push(4) 
llist.push(3) 
llist.push(2) 
llist.push(1) 

print "Given linked list"
llist.printList() 
llist.head = llist.reverse(llist.head, 3) 

print "\nReversed Linked list"
llist.printList() 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# program to reverse a linked list  
// in groups of given size  
using System;  

public class LinkedList  
{  
    Node head; // head of list  

    /* Linked list Node*/
    class Node  
    {  
        public int data;  
        public Node next;  
        public Node(int d)  
        { 
            data = d;  
            next = null;  
        }  
    }  

    Node reverse(Node head, int k)  
    {  
    Node current = head;  
    Node next = null;  
    Node prev = null;  

    int count = 0;  

    /* Reverse first k nodes of linked list */
    while (count < k && current != null)  
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
        count++;  
    }  

    /* next is now a pointer to (k+1)th node  
        Recursively call for the list starting from current.  
        And make rest of the list as next of first node */
    if (next != null)  
        head.next = reverse(next, k);  

    // prev is now head of input list  
    return prev;  
    }                  

    /* Utility functions */

    /* Inserts a new Node at front of the list. */
    public void push(int new_data)  
    {  
        /* 1 & 2: Allocate the Node &  
                Put in the data*/
        Node new_node = new Node(new_data);  

        /* 3\. Make next of new Node as head */
        new_node.next = head;  

        /* 4\. Move the head to point to new Node */
        head = new_node;  
    }  

    /* Function to print linked list */
    void printList()  
    {  
        Node temp = head;  
        while (temp != null)  
        {  
        Console.Write(temp.data+" ");  
        temp = temp.next;  
        }  
        Console.WriteLine();  
    }  

    /* Driver code*/
    public static void Main(String []args)  
    {  
        LinkedList llist = new LinkedList();  

        /* Constructed Linked List is 1->2->3->4->5->6->  
        7->8->8->9->null */
        llist.push(9);  
        llist.push(8);  
        llist.push(7);  
        llist.push(6);  
        llist.push(5);  
        llist.push(4);  
        llist.push(3);  
        llist.push(2);  
        llist.push(1);  

        Console.WriteLine("Given Linked List");  
        llist.printList();  

        llist.head = llist.reverse(llist.head, 3);  

        Console.WriteLine("Reversed list");  
        llist.printList();  
    }  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Given Linked List
1 2 3 4 5 6 7 8 9 
Reversed list
3 2 1 6 5 4 9 8 7 
```

**复杂度分析：**

*   **时间复杂度：** O（n）。
    列表的遍历仅执行一次，并且包含“ n”个元素。
*   **辅助空间：** O（n / k）。
    对于大小为n的每个链接列表，将在递归过程中进行n / k或（n / k）+1调用。

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

