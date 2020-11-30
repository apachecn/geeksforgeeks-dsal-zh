# 链表和递归的练习题

> 原文：[https://www.geeksforgeeks.org/practice-questions-for-linked-list-and-recursion/](https://www.geeksforgeeks.org/practice-questions-for-linked-list-and-recursion/)

假定链表节点的结构如下。

```

struct Node 
{ 
  int data; 
  struct Node *next; 
}; 

```

解释以下 C 函数的功能。

**1、以下功能对给定的链表有什么作用？**

## C++

```cpp

void fun1(struct Node* head) 
{ 
if(head == NULL) 
    return; 

fun1(head->next); 
cout << head->data << " "; 
} 

// This code is contributed by shubhamsingh10 

```

## C

```c

void fun1(struct Node* head) 
{ 
  if(head == NULL) 
    return; 

  fun1(head->next); 
  printf("%d  ", head->data); 
} 

```

## Java

```java

static void fun1(Node head) 
{ 
    if (head == null) 
    { 
        return; 
    } 

    fun1(head.next); 
    System.out.print(head.data + " "); 
} 

// This code is contributed by shubhamsingh10 

```

## Python

```py

def fun1(head): 
    if(head == None): 
        return
    fun1(head.next)  
    print(head.data, end = " ") 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

static void fun1(Node head) 
{ 
    if (head == null) 
    { 
        return; 
    } 

    fun1(head.next); 
    Console.Write(head.data + " "); 
} 

// This code is contributed by shubhamsingh10 

```

fun1() prints the given Linked List in reverse manner. For Linked List 1->2->3->4->5, fun1() prints 5->4->3->2->1.

**2、以下功能对给定的链表有什么作用？**

## C++

```cpp

void fun2(struct Node* head) 
{ 
    if(head == NULL) 
        return; 
    cout << head->data << " ";  

    if(head->next != NULL ) 
        fun2(head->next->next); 
    cout << head->data << " "; 
} 

// This code is contributed by shubhamsingh10 

```

## C

```c

void fun2(struct Node* head) 
{ 
  if(head == NULL) 
    return; 
  printf("%d  ", head->data);  

  if(head->next != NULL ) 
    fun2(head->next->next); 
  printf("%d  ", head->data);    
} 

```

## Java

```java

static void fun2(Node head) 
{ 
    if (head == null) 
    { 
        return; 
    } 
    System.out.print(head.data + " "); 

    if (head.next != null) 
    { 
        fun2(head.next.next); 
    } 
    System.out.print(head.data + " "); 
} 

// This code is contributed by shubhamsingh10 

```

fun2() prints alternate nodes of the given Linked List, first from head to end, and then from end to head. If Linked List has even number of nodes, then fun2() skips the last node. For Linked List 1->2->3->4->5, fun2() prints 1 3 5 5 3 1\. For Linked List 1->2->3->4->5->6, fun2() prints 1 3 5 5 3 1.

以下是测试上述功能的完整运行程序。

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

/* A linked list node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Prints a linked list in reverse manner */
void fun1(Node* head)  
{  
    if(head == NULL)  
        return;  

    fun1(head->next);  
    cout << head->data << " ";  
}  

/* prints alternate nodes of a Linked List, first  
from head to end, and then from end to head. */
void fun2(Node* start)  
{  
    if(start == NULL)  
        return;  
    cout<<start->data<<" ";  

    if(start->next != NULL )  
        fun2(start->next->next);  
    cout << start->data << " ";  
}  

/* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
/* Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. */
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

/* Driver code */
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Using push() to construct below list  
        1->2->3->4->5 */
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);  

    cout<<"Output of fun1() for list 1->2->3->4->5 \n";  
    fun1(head);  

    cout<<"\nOutput of fun2() for list 1->2->3->4->5 \n";  
    fun2(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

#include<stdio.h> 
#include<stdlib.h> 

/* A linked list node */
struct Node 
{ 
  int data; 
  struct Node *next; 
}; 

/* Prints a linked list in reverse manner */
void fun1(struct Node* head) 
{ 
  if(head == NULL) 
    return; 

  fun1(head->next); 
  printf("%d  ", head->data); 
} 

/* prints alternate nodes of a Linked List, first  
  from head to end, and then from end to head. */
void fun2(struct Node* start) 
{ 
  if(start == NULL) 
    return; 
  printf("%d  ", start->data);  

  if(start->next != NULL ) 
    fun2(start->next->next); 
  printf("%d  ", start->data); 
} 

/* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
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

/* Driver program to test above functions */
int main() 
{ 
  /* Start with the empty list */
  struct Node* head = NULL; 

  /* Using push() to construct below list 
    1->2->3->4->5  */
  push(&head, 5); 
  push(&head, 4); 
  push(&head, 3); 
  push(&head, 2); 
  push(&head, 1);    

  printf("Output of fun1() for list 1->2->3->4->5 \n"); 
  fun1(head); 

  printf("\nOutput of fun2() for list 1->2->3->4->5 \n");  
  fun2(head); 

  getchar(); 
  return 0; 
} 

```

## Java

```java

// Java code implementation for above approach 
class GFG  
{ 

    /* A linked list node */
    static class Node  
    { 
        int data; 
        Node next; 
    }; 

    /* Prints a linked list in reverse manner */
    static void fun1(Node head) 
    { 
        if (head == null) 
        { 
            return; 
        } 

        fun1(head.next); 
        System.out.print(head.data + " "); 
    } 

    /* prints alternate nodes of a Linked List, first  
    from head to end, and then from end to head. */
    static void fun2(Node start) 
    { 
        if (start == null) 
        { 
            return; 
        } 
        System.out.print(start.data + " "); 

        if (start.next != null) 
        { 
            fun2(start.next.next); 
        } 
        System.out.print(start.data + " "); 
    } 

    /* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
    /* Given a reference (pointer to pointer) to the head  
    of a list and an int, push a new node on the front  
    of the list. */
    static Node push(Node head_ref, int new_data)  
    { 
        /* allocate node */
        Node new_node = new Node(); 

        /* put in the data */
        new_node.data = new_data; 

        /* link the old list off the new node */
        new_node.next = (head_ref); 

        /* move the head to point to the new node */
        (head_ref) = new_node; 
        return head_ref; 
    } 

    /* Driver code */
    public static void main(String[] args)  
    { 
        /* Start with the empty list */
        Node head = null; 

        /* Using push() to conbelow list  
        1->2->3->4->5 */
        head = push(head, 5); 
        head = push(head, 4); 
        head = push(head, 3); 
        head = push(head, 2); 
        head = push(head, 1); 

        System.out.print("Output of fun1() for " +  
                         "list 1->2->3->4->5 \n"); 
        fun1(head); 

        System.out.print("\nOutput of fun2() for " + 
                           "list 1->2->3->4->5 \n"); 
        fun2(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

''' A linked list node '''
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

''' Prints a linked list in reverse manner '''
def fun1(head): 
    if(head == None): 
        return
    fun1(head.next)  
    print(head.data, end = " ") 

''' prints alternate nodes of a Linked List, first  
from head to end, and then from end to head. '''
def fun2(start): 

    if(start == None): 
        return
    print(start.data, end = " ") 

    if(start.next != None ): 
        fun2(start.next.next)  
    print(start.data, end = " ") 

''' UTILITY FUNCTIONS TO TEST fun1() and fun2() '''
''' Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. '''
def push( head, new_data): 

    ''' put in the data '''
    new_node = Node(new_data) 

    ''' link the old list off the new node '''
    new_node.next = head 

    ''' move the head to poto the new node '''
    head = new_node 
    return head 

''' Driver code '''
''' Start with the empty list '''
head = None

''' Using push() to construct below list  
    1.2.3.4.5 '''
head = Node(5)  
head = push(head, 4)  
head = push(head, 3)  
head = push(head, 2)  
head = push(head, 1)  

print("Output of fun1() for list 1->2->3->4->5") 
fun1(head)  

print("\nOutput of fun2() for list 1->2->3->4->5")  
fun2(head)  

# This code is contributed by SHUBHAMSINGH10 

```

## C#

```cs

// C# code implementation for above approach 
using System; 

class GFG  
{ 

    /* A linked list node */
    public class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    /* Prints a linked list in reverse manner */
    static void fun1(Node head) 
    { 
        if (head == null) 
        { 
            return; 
        } 

        fun1(head.next); 
        Console.Write(head.data + " "); 
    } 

    /* prints alternate nodes of a Linked List, first  
    from head to end, and then from end to head. */
    static void fun2(Node start) 
    { 
        if (start == null) 
        { 
            return; 
        } 
        Console.Write(start.data + " "); 

        if (start.next != null) 
        { 
            fun2(start.next.next); 
        } 
        Console.Write(start.data + " "); 
    } 

    /* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
    /* Given a reference (pointer to pointer) to the head  
    of a list and an int,.Push a new node on the front  
    of the list. */
    static Node Push(Node head_ref, int new_data)  
    { 
        /* allocate node */
        Node new_node = new Node(); 

        /* put in the data */
        new_node.data = new_data; 

        /* link the old list off the new node */
        new_node.next = (head_ref); 

        /* move the head to point to the new node */
        (head_ref) = new_node; 
        return head_ref; 
    } 

    /* Driver code */
    public static void Main(String[] args)  
    { 
        /* Start with the empty list */
        Node head = null; 

        /* Using.Push() to conbelow list  
        1->2->3->4->5 */
        head = Push(head, 5); 
        head = Push(head, 4); 
        head = Push(head, 3); 
        head = Push(head, 2); 
        head = Push(head, 1); 

        Console.Write("Output of fun1() for " +  
                        "list 1->2->3->4->5 \n"); 
        fun1(head); 

        Console.Write("\nOutput of fun2() for " + 
                        "list 1->2->3->4->5 \n"); 
        fun2(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
 Output of fun1() for list 1->2->3->4->5 
5 4 3 2 1 
Output of fun2() for list 1->2->3->4->5 
1 3 5 5 3 1 
```

如果您发现任何答案/解释不正确，或者您想分享有关上述主题的更多信息，请写评论。

