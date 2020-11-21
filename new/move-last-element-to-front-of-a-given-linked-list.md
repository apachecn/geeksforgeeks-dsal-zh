# 将最后一个元素移到给定链表

> 原文：[https://www.geeksforgeeks.org/move-last-element-to-front-of-a-given-linked-list/](https://www.geeksforgeeks.org/move-last-element-to-front-of-a-given-linked-list/)

的前面

编写一个函数，将给定的单链列表中的最后一个元素移到最前面。 例如，如果给定的链表为 1-> 2-> 3-> 4-> 5，则该函数应将列表更改为 5-> 1-> 2-> 3-> 4。

**算法**：

遍历列表直到最后一个节点。 使用两个指针：一个用于存储最后一个节点的地址，另一个用于存储倒数第二个节点的地址。 循环结束后，请执行以下操作。

i）以倒数第二为倒数（secLast- > next = NULL）。

ii）将倒数第二个设置为 head（last- > next = * head_ref）。

iii）以头为准（* head_ref = last）

## C++

```cpp

/* CPP Program to move last element  
to front in a given linked list */
#include <bits/stdc++.h> 
using namespace std; 

/* A linked list node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* We are using a double pointer 
head_ref here because we change  
head of the linked list inside  
this function.*/
void moveToFront(Node **head_ref)  
{  
    /* If linked list is empty, or  
    it contains only one node,  
    then nothing needs to be done, 
    simply return */
    if (*head_ref == NULL || (*head_ref)->next == NULL)  
        return;  

    /* Initialize second last 
    and last pointers */
    Node *secLast = NULL;  
    Node *last = *head_ref;  

    /*After this loop secLast contains 
    address of second last node and  
    last contains address of last node in Linked List */
    while (last->next != NULL)  
    {  
        secLast = last;  
        last = last->next;  
    }  

    /* Set the next of second last as NULL */
    secLast->next = NULL;  

    /* Set next of last as head node */
    last->next = *head_ref;  

    /* Change the head pointer 
    to point to last node now */
    *head_ref = last;  
}  

/* UTILITY FUNCTIONS */
/* Function to add a node  
at the beginning of Linked List */
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

/* Function to print nodes in a given linked list */
void printList(Node *node)  
{  
    while(node != NULL)  
    {  
        cout << node->data << " ";  
        node = node->next;  
    }  
}  

/* Driver code */
int main()  
{  
    Node *start = NULL;  

    /* The constructed linked list is:  
    1->2->3->4->5 */
    push(&start, 5);  
    push(&start, 4);  
    push(&start, 3);  
    push(&start, 2);  
    push(&start, 1);  

    cout<<"Linked list before moving last to front\n";  
    printList(start);  

    moveToFront(&start);  

    cout<<"\nLinked list after removing last to front\n";  
    printList(start);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

/* C Program to move last element to front in a given linked list */
#include<stdio.h> 
#include<stdlib.h> 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* We are using a double pointer head_ref here because we change 
   head of the linked list inside this function.*/
void moveToFront(struct Node **head_ref) 
{ 
    /* If linked list is empty, or it contains only one node, 
      then nothing needs to be done, simply return */
    if (*head_ref == NULL || (*head_ref)->next == NULL) 
        return; 

    /* Initialize second last and last pointers */
    struct Node *secLast = NULL; 
    struct Node *last = *head_ref; 

    /*After this loop secLast contains address of second last 
    node and last contains address of last node in Linked List */
    while (last->next != NULL) 
    { 
        secLast = last; 
        last = last->next; 
    } 

    /* Set the next of second last as NULL */
    secLast->next = NULL; 

    /* Set next of last as head node */
    last->next = *head_ref; 

    /* Change the head pointer to point to last node now */
    *head_ref = last; 
} 

/* UTILITY FUNCTIONS */
/* Function to add a node at the beginning of Linked List */
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

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while(node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function */
int main() 
{ 
    struct Node *start = NULL; 

    /* The constructed linked list is: 
     1->2->3->4->5 */
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 

    printf("\n Linked list before moving last to front\n"); 
    printList(start); 

    moveToFront(&start); 

    printf("\n Linked list after removing last to front\n"); 
    printList(start); 

    return 0; 
} 

```

## Java

```java

/* Java Program to move last element to front in a given linked list */
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

    void moveToFront() 
    { 
        /* If linked list is empty or it contains only 
           one node then simply return. */
           if(head == null || head.next == null)  
              return; 

        /* Initialize second last and last pointers */
        Node secLast = null; 
        Node last = head; 

        /* After this loop secLast contains address of  
           second last  node and last contains address of  
           last node in Linked List */
        while (last.next != null)   
        { 
           secLast = last; 
           last = last.next;  
        } 

        /* Set the next of second last as null */
        secLast.next = null; 

        /* Set the next of last as head */
        last.next = head; 

        /* Change head to point to last node. */
        head = last; 
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
        while(temp != null) 
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
        /* Constructed Linked List is 1->2->3->4->5->null */
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Linked List before moving last to front "); 
        llist.printList(); 

        llist.moveToFront(); 

        System.out.println("Linked List after moving last to front "); 
        llist.printList(); 
    } 
}  
/* This code is contributed by Rajat Mishra */ 

```

## Python3

```py

# Python3 code to move the last item to front 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 
    def __init__(self): 
        self.head = None

    # Function to add a node  
    # at the beginning of Linked List 
    def push(self, data): 
        new_node = Node(data) 
        new_node.next = self.head 
        self.head = new_node 

    # Function to print nodes in a 
    # given linked list 
    def printList(self): 
        tmp = self.head 
        while tmp is not None: 
            print(tmp.data, end=", ") 
            tmp = tmp.next
        print() 

    # Function to bring the last node to the front 
    def moveToFront(self): 
        tmp = self.head 
        sec_last = None # To maintain the track of 
                        # the second last node 

    # To check whether we have not received  
    # the empty list or list with a single node 
        if not tmp or not tmp.next:  
            return

        # Iterate till the end to get 
        # the last and second last node  
        while tmp and tmp.next : 
            sec_last = tmp 
            tmp = tmp.next

        # point the next of the second 
        # last node to None 
        sec_last.next = None

        # Make the last node as the first Node 
        tmp.next = self.head 
        self.head = tmp 

# Driver Code 
if __name__ == '__main__': 
    llist = LinkedList() 

    # swap the 2 nodes 
    llist.push(5) 
    llist.push(4) 
    llist.push(3) 
    llist.push(2) 
    llist.push(1) 
    print ("Linked List before moving last to front ") 
    llist.printList() 
    llist.moveToFront() 
    print ("Linked List after moving last to front ") 
    llist.printList() 

```

## C#

```cs

/* C# Program to move last element to front in a given linked list */
using System; 
class LinkedList  
{  
    Node head; // head of list  

    /* Linked list Node*/
    public class Node  
    {  
        public int data;  
        public Node next;  
        public Node(int d) {data = d; next = null; }  
    }  

    void moveToFront()  
    {  
        /* If linked list is empty or it contains only  
        one node then simply return. */
        if(head == null || head.next == null)  
            return;  

        /* Initialize second last and last pointers */
        Node secLast = null;  
        Node last = head;  

        /* After this loop secLast contains address of  
        second last node and last contains address of  
        last node in Linked List */
        while (last.next != null)  
        {  
        secLast = last;  
        last = last.next;  
        }  

        /* Set the next of second last as null */
        secLast.next = null;  

        /* Set the next of last as head */
        last.next = head;  

        /* Change head to point to last node. */
        head = last;  
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
        while(temp != null)  
        {  
        Console.Write(temp.data+" ");  
        temp = temp.next;  
        }  
        Console.WriteLine();  
    }  

    /* Driver program to test above functions */
    public static void Main(String []args)  
    {  
        LinkedList llist = new LinkedList();  
        /* Constructed Linked List is 1->2->3->4->5->null */
        llist.push(5);  
        llist.push(4);  
        llist.push(3);  
        llist.push(2);  
        llist.push(1);  

        Console.WriteLine("Linked List before moving last to front ");  
        llist.printList();  

        llist.moveToFront();  

        Console.WriteLine("Linked List after moving last to front ");  
        llist.printList();  
    }  
}  
// This code is contributed by Arnab Kundu 

```

**输出**：

```
 Linked list before moving last to front 
1 2 3 4 5 
 Linked list after removing last to front 
5 1 2 3 4
```

**时间复杂度**：`O(n)`，其中 n 是给定链表中的节点数。

如果您在上述代码/算法中发现任何错误，或者找到其他解决同一问题的方法，请发表评论。

