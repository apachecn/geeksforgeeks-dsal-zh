# 反向链接单个链表

中的 K 个节点

给定一个链表，编写一个函数以有效的方式反转每个备用 k 节点（其中 k 是函数的输入）。 给出算法的复杂性。

**示例：**

```
Inputs:   1->2->3->4->5->6->7->8->9->NULL and k = 3
Output:   3->2->1->4->5->6->9->8->7->NULL. 

```

**方法 1（处理 2k 个节点并递归调用列表的其余部分）**
此方法基本上是[此](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)文章中讨论的方法的扩展。

```
kAltReverse(struct node *head, int k)
  1)  Reverse first k nodes.
  2)  In the modified list head points to the kth node.  So change next 
       of head to (k+1)th node
  3)  Move the current pointer to skip next k nodes.
  4)  Call the kAltReverse() recursively for rest of the n - 2k nodes.
  5)  Return new head of the list.

```

## C++

```cpp

// C++ program to reverse alternate 
// k nodes in a linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Reverses alternate k nodes and  
returns the pointer to the new head node */
Node *kAltReverse(Node *head, int k)  
{  
    Node* current = head;  
    Node* next;  
    Node* prev = NULL;  
    int count = 0;  

    /*1) reverse first k nodes of the linked list */
    while (current != NULL && count < k)  
    {  
    next = current->next;  
    current->next = prev;  
    prev = current;  
    current = next;  
    count++;  
    }  

    /* 2) Now head points to the kth node.  
    So change next  of head to (k+1)th node*/
    if(head != NULL)  
    head->next = current;  

    /* 3) We do not want to reverse next k  
       nodes. So move the current  
        pointer to skip next k nodes */
    count = 0;  
    while(count < k-1 && current != NULL )  
    {  
    current = current->next;  
    count++;  
    }  

    /* 4) Recursively call for the list  
    starting from current->next. And make 
    rest of the list as next of first node */
    if(current != NULL)  
    current->next = kAltReverse(current->next, k);  

    /* 5) prev is new head of the input list */
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
    int count = 0;  
    while(node != NULL)  
    {  
        cout<<node->data<<" ";  
        node = node->next;  
        count++;  
    }  
}  

/* Driver code*/
int main(void)  
{  
    /* Start with the empty list */
    Node* head = NULL;  
    int i;  

    // create a list 1->2->3->4->5...... ->20  
    for(i = 20; i > 0; i--)  
    push(&head, i);  

    cout<<"Given linked list \n";  
    printList(head);  
    head = kAltReverse(head, 3);  

    cout<<"\n Modified Linked list \n";  
    printList(head);  
    return(0);  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Reverses alternate k nodes and 
   returns the pointer to the new head node */
struct Node *kAltReverse(struct Node *head, int k) 
{ 
    struct Node* current = head; 
    struct Node* next; 
    struct Node* prev = NULL; 
    int count = 0;    

    /*1) reverse first k nodes of the linked list */
    while (current != NULL && count < k) 
    { 
       next  = current->next; 
       current->next = prev; 
       prev = current; 
       current = next; 
       count++; 
    } 

    /* 2) Now head points to the kth node.  So change next  
       of head to (k+1)th node*/ 
    if(head != NULL) 
      head->next = current;    

    /* 3) We do not want to reverse next k nodes. So move the current  
        pointer to skip next k nodes */
    count = 0; 
    while(count < k-1 && current != NULL ) 
    { 
      current = current->next; 
      count++; 
    } 

    /* 4) Recursively call for the list starting from current->next. 
       And make rest of the list as next of first node */
    if(current !=  NULL) 
       current->next = kAltReverse(current->next, k);  

    /* 5) prev is new head of the input list */
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
    int count = 0; 
    while(node != NULL) 
    { 
        printf("%d  ", node->data); 
        node = node->next; 
        count++; 
    } 
}     

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 
    int i; 
    // create a list 1->2->3->4->5...... ->20 
    for(i = 20; i > 0; i--) 
      push(&head, i); 

     printf("\n Given linked list \n"); 
     printList(head); 
     head = kAltReverse(head, 3); 

     printf("\n Modified Linked list \n"); 
     printList(head); 

     getchar(); 
     return(0); 
} 

```

## Java

```java

// Java program to reverse alternate k nodes in a linked list 

class LinkedList { 

    static Node head; 

    class Node { 

        int data; 
        Node next; 

        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    /* Reverses alternate k nodes and 
     returns the pointer to the new head node */
    Node kAltReverse(Node node, int k) { 
        Node current = node; 
        Node next = null, prev = null; 
        int count = 0; 

        /*1) reverse first k nodes of the linked list */
        while (current != null && count < k) { 
            next = current.next; 
            current.next = prev; 
            prev = current; 
            current = next; 
            count++; 
        } 

        /* 2) Now head points to the kth node.  So change next  
         of head to (k+1)th node*/
        if (node != null) { 
            node.next = current; 
        } 

        /* 3) We do not want to reverse next k nodes. So move the current  
         pointer to skip next k nodes */
        count = 0; 
        while (count < k - 1 && current != null) { 
            current = current.next; 
            count++; 
        } 

        /* 4) Recursively call for the list starting from current->next. 
         And make rest of the list as next of first node */
        if (current != null) { 
            current.next = kAltReverse(current.next, k); 
        } 

        /* 5) prev is new head of the input list */
        return prev; 
    } 

    void printList(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    void push(int newdata) { 
        Node mynode = new Node(newdata); 
        mynode.next = head; 
        head = mynode; 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 

        // Creating the linkedlist 
        for (int i = 20; i > 0; i--) { 
            list.push(i); 
        } 
        System.out.println("Given Linked List :"); 
        list.printList(head); 
        head = list.kAltReverse(head, 3); 
        System.out.println(""); 
        System.out.println("Modified Linked List :"); 
        list.printList(head); 

    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python3

```py

# Python3 program to reverse alternate 
# k nodes in a linked list 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Reverses alternate k nodes and  
#returns the poer to the new head node  
def kAltReverse(head, k) :  
    current = head  
    next = None
    prev = None
    count = 0

    #1) reverse first k nodes of the linked list  
    while (current != None and count < k) :  
        next = current.next
        current.next = prev  
        prev = current  
        current = next
        count = count + 1; 

    # 2) Now head pos to the kth node.  
    # So change next of head to (k+1)th node 
    if(head != None):  
        head.next = current  

    # 3) We do not want to reverse next k  
    # nodes. So move the current  
    # poer to skip next k nodes  
    count = 0
    while(count < k - 1 and current != None ):  
        current = current.next
        count = count + 1

    # 4) Recursively call for the list  
    # starting from current.next. And make 
    # rest of the list as next of first node  
    if(current != None):  
        current.next = kAltReverse(current.next, k)  

    # 5) prev is new head of the input list  
    return prev  

# UTILITY FUNCTIONS  
# Function to push a node  
def push(head_ref, new_data):  

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    # new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = head_ref  

    # move the head to po to the new node  
    head_ref = new_node 

    return head_ref 

# Function to print linked list  
def prList(node):  
    count = 0
    while(node != None):  
        print(node.data, end = " ")  
        node = node.next
        count = count + 1

# Driver code 
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # create a list 1.2.3.4.5...... .20  
    for i in range(20, 0, -1): 
        head = push(head, i)  

    print("Given linked list ")  
    prList(head)  
    head = kAltReverse(head, 3)  

    print("\nModified Linked list")  
    prList(head)  

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to reverse alternate 
// k nodes in a linked list  
using System; 
class LinkedList  
{  

    static Node head;  

    public class Node  
    {  

        public int data;  
        public Node next;  

        public Node(int d) 
        {  
            data = d;  
            next = null;  
        }  
    }  

    /* Reverses alternate k nodes and  
    returns the pointer to the new head node */
    Node kAltReverse(Node node, int k)  
    {  
        Node current = node;  
        Node next = null, prev = null;  
        int count = 0;  

        /*1) reverse first k nodes of the linked list */
        while (current != null && count < k) 
        {  
            next = current.next;  
            current.next = prev;  
            prev = current;  
            current = next;  
            count++;  
        }  

        /* 2) Now head points to the kth  
        node. So change next  
        of head to (k+1)th node*/
        if (node != null)  
        {  
            node.next = current;  
        }  

        /* 3) We do not want to reverse  
        next k nodes. So move the current  
        pointer to skip next k nodes */
        count = 0;  
        while (count < k - 1 && current != null)  
        {  
            current = current.next;  
            count++;  
        }  

        /* 4) Recursively call for the  
        list starting from current->next.  
        And make rest of the list as  
        next of first node */
        if (current != null) 
        {  
            current.next = kAltReverse(current.next, k);  
        }  

        /* 5) prev is new head of the input list */
        return prev;  
    }  

    void printList(Node node)  
    {  
        while (node != null)  
        {  
            Console.Write(node.data + " ");  
            node = node.next;  
        }  
    }  

    void push(int newdata) 
    {  
        Node mynode = new Node(newdata);  
        mynode.next = head;  
        head = mynode;  
    }  

    // Driver code 
    public static void Main(String []args) 
    {  
        LinkedList list = new LinkedList();  

        // Creating the linkedlist  
        for (int i = 20; i > 0; i--)  
        {  
            list.push(i);  
        }  
        Console.WriteLine("Given Linked List :");  
        list.printList(head);  
        head = list.kAltReverse(head, 3);  
        Console.WriteLine("");  
        Console.WriteLine("Modified Linked List :");  
        list.printList(head);  
    }  
}  

// This code has been contributed by Arnab Kundu 

```

**输出：**

```
Given linked list
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
Modified Linked list
3 2 1 4 5 6 9 8 7 10 11 12 15 14 13 16 17 18 20 19

```

**时间复杂度：** O（n）

**方法 2（处理 k 个节点并递归调用列表的其余部分）**
方法 1 反转第一个 k 节点，然后将指针向前移动到 k 个节点。 因此，方法 1 使用两个 while 循环并在一个递归调用中处理 2k 个节点。
此方法在递归调用中仅处理 k 个节点。 它使用第三个布尔参数 b 来决定是反转 k 个元素还是简单地移动指针。

```
_kAltReverse(struct node *head, int k, bool b)
  1)  If b is true, then reverse first k nodes.
  2)  If b is false, then move the pointer k nodes ahead.
  3)  Call the kAltReverse() recursively for rest of the n - k nodes and link 
       rest of the modified list with end of first k nodes. 
  4)  Return new head of the list.

```

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class node  
{  
    public: 
    int data;  
    node* next;  
};  

/* Helper function for kAltReverse() */
node * _kAltReverse(node *node, int k, bool b);  

/* Alternatively reverses the given linked list  
in groups of given size k. */
node *kAltReverse(node *head, int k)  
{  
    return _kAltReverse(head, k, true);  
}  

/* Helper function for kAltReverse().   
It reverses k nodes of the list only if  
the third parameter b is passed as true,  
otherwise moves the pointer k nodes ahead 
and recursively calls iteself */
node * _kAltReverse(node *Node, int k, bool b)  
{  
    if(Node == NULL)  
        return NULL;  

    int count = 1;  
    node *prev = NULL;  
    node *current = Node;  
    node *next;  

    /* The loop serves two purposes  
        1) If b is true,  
           then it reverses the k nodes  
        2) If b is false,  
           then it moves the current pointer */
    while(current != NULL && count <= k)  
    {  
        next = current->next;  

        /* Reverse the nodes only if b is true*/
        if(b == true)  
            current->next = prev;  

        prev = current;  
        current = next;  
        count++;  
    }  

    /* 3) If b is true, then node is the kth node.  
        So attach rest of the list after node.  
        4) After attaching, return the new head */
    if(b == true)  
    {  
        Node->next = _kAltReverse(current, k, !b);  
        return prev;          
    }  

    /* If b is not true, then attach  
    rest of the list after prev.  
    So attach rest of the list after prev */
    else
    {  
        prev->next = _kAltReverse(current, k, !b);  
        return Node;      
    }  
}  

/* UTILITY FUNCTIONS */
/* Function to push a node */
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

/* Function to print linked list */
void printList(node *node)  
{  
    int count = 0;  
    while(node != NULL)  
    {  
        cout << node->data << " ";  
        node = node->next;  
        count++;  
    }  
}  

// Driver Code 
int main(void)  
{  
    /* Start with the empty list */
    node* head = NULL;  
    int i;  

    // create a list 1->2->3->4->5...... ->20  
    for(i = 20; i > 0; i--)  
    push(&head, i);  

    cout << "Given linked list \n";  
    printList(head);  
    head = kAltReverse(head, 3);  

    cout << "\nModified Linked list \n";  
    printList(head);  
    return(0);  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct node 
{ 
    int data; 
    struct node* next; 
}; 

/* Helper function for kAltReverse() */
struct node * _kAltReverse(struct node *node, int k, bool b); 

/* Alternatively reverses the given linked list in groups of  
   given size k. */
struct node *kAltReverse(struct node *head, int k) 
{ 
  return _kAltReverse(head, k, true); 
} 

/*  Helper function for kAltReverse().  It reverses k nodes of the list only if 
    the third parameter b is passed as true, otherwise moves the pointer k  
    nodes ahead and recursively calls iteself  */ 
struct node * _kAltReverse(struct node *node, int k, bool b) 
{ 
   if(node == NULL) 
       return NULL; 

   int count = 1; 
   struct node *prev = NULL; 
   struct node  *current = node; 
   struct node *next; 

   /* The loop serves two purposes 
      1) If b is true, then it reverses the k nodes  
      2) If b is false, then it moves the current pointer */
   while(current != NULL && count <= k) 
   { 
       next = current->next; 

       /* Reverse the nodes only if b is true*/
       if(b == true) 
          current->next = prev; 

       prev = current; 
       current = next; 
       count++; 
   } 

   /* 3) If b is true, then node is the kth node.  
       So attach rest of the list after node.  
     4) After attaching, return the new head */
   if(b == true) 
   { 
        node->next = _kAltReverse(current,k,!b); 
        return prev;         
   } 

   /* If b is not true, then attach rest of the list after prev.  
     So attach rest of the list after prev */    
   else
   { 
        prev->next = _kAltReverse(current, k, !b); 
        return node;        
   } 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(struct node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct node* new_node = 
            (struct node*) malloc(sizeof(struct node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Function to print linked list */
void printList(struct node *node) 
{ 
    int count = 0; 
    while(node != NULL) 
    { 
        printf("%d  ", node->data); 
        node = node->next; 
        count++; 
    } 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct node* head = NULL; 
    int i; 

    // create a list 1->2->3->4->5...... ->20 
    for(i = 20; i > 0; i--) 
      push(&head, i); 

    printf("\n Given linked list \n"); 
    printList(head); 
    head = kAltReverse(head, 3); 

    printf("\n Modified Linked list \n"); 
    printList(head); 

    getchar(); 
    return(0); 
} 

```

## Java

```java

// Java program to reverse alternate k nodes in a linked list 

class LinkedList { 

    static Node head; 

    class Node { 

        int data; 
        Node next; 

        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    /* Alternatively reverses the given linked list in groups of  
     given size k. */
    Node kAltReverse(Node head, int k) { 
        return _kAltReverse(head, k, true); 
    } 

    /*  Helper function for kAltReverse().  It reverses k nodes of the list only if 
     the third parameter b is passed as true, otherwise moves the pointer k  
     nodes ahead and recursively calls iteself  */
    Node _kAltReverse(Node node, int k, boolean b) { 
        if (node == null) { 
            return null; 
        } 

        int count = 1; 
        Node prev = null; 
        Node current = node; 
        Node next = null; 

        /* The loop serves two purposes 
         1) If b is true, then it reverses the k nodes  
         2) If b is false, then it moves the current pointer */
        while (current != null && count <= k) { 
            next = current.next; 

            /* Reverse the nodes only if b is true*/
            if (b == true) { 
                current.next = prev; 
            } 

            prev = current; 
            current = next; 
            count++; 
        } 

        /* 3) If b is true, then node is the kth node.  
         So attach rest of the list after node.  
         4) After attaching, return the new head */
        if (b == true) { 
            node.next = _kAltReverse(current, k, !b); 
            return prev; 
        } /* If b is not true, then attach rest of the list after prev.  
         So attach rest of the list after prev */ else { 
            prev.next = _kAltReverse(current, k, !b); 
            return node; 
        } 
    } 

    void printList(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    void push(int newdata) { 
        Node mynode = new Node(newdata); 
        mynode.next = head; 
        head = mynode; 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 

        // Creating the linkedlist 
        for (int i = 20; i > 0; i--) { 
            list.push(i); 
        } 
        System.out.println("Given Linked List :"); 
        list.printList(head); 
        head = list.kAltReverse(head, 3); 
        System.out.println(""); 
        System.out.println("Modified Linked List :"); 
        list.printList(head); 

    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## 蟒蛇

```

# Python code for above algorithm 

# Link list node  
class node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node = node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 

    return head_ref 

""" Alternatively reverses the given linked list  
in groups of given size k. """
def kAltReverse(head, k) : 

    return _kAltReverse(head, k, True)  

""" Helper function for kAltReverse().  
It reverses k nodes of the list only if  
the third parameter b is passed as True,  
otherwise moves the pointer k nodes ahead 
and recursively calls iteself """
def _kAltReverse(Node, k, b) : 

    if(Node == None) : 
        return None

    count = 1
    prev = None
    current = Node  
    next = None

    """ The loop serves two purposes  
        1) If b is True,  
        then it reverses the k nodes  
        2) If b is false,  
        then it moves the current pointer """
    while(current != None and count <= k) : 

        next = current.next

        """ Reverse the nodes only if b is True"""
        if(b == True) : 
            current.next = prev  

        prev = current  
        current = next
        count = count + 1

    """ 3) If b is True, then node is the kth node.  
        So attach rest of the list after node.  
        4) After attaching, return the new head """
    if(b == True) : 

        Node.next = _kAltReverse(current, k, not b)  
        return prev          

    else : 
        """ If b is not True, then attach  
        rest of the list after prev.  
        So attach rest of the list after prev """
        prev.next = _kAltReverse(current, k, not b)  
        return Node      

""" Function to print linked list """
def printList(node) : 

    count = 0
    while(node != None) : 

        print( node.data, end = " ")  
        node = node.next
        count = count + 1

# Driver Code 

""" Start with the empty list """
head = None
i = 20

# create a list 1->2->3->4->5...... ->20  
while(i > 0 ):  
    head = push(head, i)  
    i = i - 1

print( "Given linked list ")  
printList(head)  
head = kAltReverse(head, 3)  

print( "\nModified Linked list ")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# Program for converting  
// singly linked list into  
// circular linked list.  
using System; 

public class LinkedList 
{  

    static Node head;  

    public class Node  
    {  

        public int data;  
        public Node next;  

        public Node(int d)  
        {  
            data = d;  
            next = null;  
        }  
    }  

    /* Reverses alternate k nodes and  
    returns the pointer to the new head node */
    Node kAltReverse(Node node, int k)  
    {  
        Node current = node;  
        Node next = null, prev = null;  
        int count = 0;  

        /*1) reverse first k nodes of the linked list */
        while (current != null && count < k)  
        {  
            next = current.next;  
            current.next = prev;  
            prev = current;  
            current = next;  
            count++;  
        }  

        /* 2) Now head points to the kth node.  
        So change next of head to (k+1)th node*/
        if (node != null) 
        {  
            node.next = current;  
        }  

        /* 3) We do not want to reverse next  
        k nodes. So move the current  
        pointer to skip next k nodes */
        count = 0;  
        while (count < k - 1 && current != null) 
        {  
            current = current.next;  
            count++;  
        }  

        /* 4) Recursively call for the list  
        starting from current->next. And make 
         rest of the list as next of first node */
        if (current != null)  
        {  
            current.next = kAltReverse(current.next, k);  
        }  

        /* 5) prev is new head of the input list */
        return prev;  
    }  

    void printList(Node node)  
    {  
        while (node != null)  
        {  
            Console.Write(node.data + " ");  
            node = node.next;  
        }  
    }  

    void push(int newdata) 
    {  
        Node mynode = new Node(newdata);  
        mynode.next = head;  
        head = mynode;  
    }  

    public static void Main(String[] args)  
    {  
        LinkedList list = new LinkedList();  

        // Creating the linkedlist  
        for (int i = 20; i > 0; i--) 
        {  
            list.push(i);  
        }  
        Console.WriteLine("Given Linked List :");  
        list.printList(head);  
        head = list.kAltReverse(head, 3);  
        Console.WriteLine("");  
        Console.WriteLine("Modified Linked List :");  
        list.printList(head);  
    }  
}  

// This code is contributed 29AjayKumar 

```

**Output:**

```
Given linked list
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
Modified Linked list
3 2 1 4 5 6 9 8 7 10 11 12 15 14 13 16 17 18 20 19

```

**时间复杂度：** O（n）
如果您发现上述代码/算法不正确，或者找到其他解决同一问题的方法，请写注释。

