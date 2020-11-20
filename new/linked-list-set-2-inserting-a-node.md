# 链表 | 系列 2（插入节点）

> 原文：[https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)

我们在[先前的文章](http://quiz.geeksforgeeks.org/linked-list-set-1-introduction/)中介绍了链接列表。 我们还创建了一个具有 3 个节点的简单链表，并讨论了链表遍历。

本文中讨论的所有程序均考虑以下链表的表示形式。

## C++

```cpp

// A linked list node  
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  
// This code is contributed by rathbhupendra 

```

## C

```c

// A linked list node 
struct Node 
{ 
  int data; 
  struct Node *next; 
}; 

```

## Java

```java

// Linked List Class 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Node Class */
    class Node 
    { 
        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) {data = d; next = null; } 
    } 
}

```

## Python

```py

# Node class 
class Node: 

    # Function to initialize the node object 
    def __init__(self, data): 
        self.data = data  # Assign data 
        self.next = None  # Initialize next as null 

# Linked List class 
class LinkedList: 

    # Function to initialize the Linked List object 
    def __init__(self):  
        self.head = None

```

## C#

```cs

/* Linked list Node*/
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int d) {data = d; next = null; } 
} 

```

在这篇文章中，讨论了在链表中插入新节点的方法。 可以通过三种方式添加节点。

**1）**在链表的最前面

**2）**在给定节点之后。

**3）**在链接列表的末尾。

**在最前面添加一个节点：（4 个步骤）**

新节点总是添加在给定链接列表的开头之前。 新添加的节点成为链接列表的新头。 例如，如果给定的链接列表为 10- > 15- > 20- > 25，而我们在前面添加了项目 5，则链接列表将变为 5- > 10- > 15 -> 20- > 25.让我们调用添加到列表前面的函数 push（）。 push（）必须接收一个指向 head 指针的指针，因为 push 必须将 head 指针更改为指向新节点（请参见[此](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)）。

![linkedlist_insert_at_start](img/0fcc552ce260975b170428e6877939dc.png)

以下是在最前面添加节点的 4 个步骤。

## C++

```cpp

/* Given a reference (pointer to pointer)  
to the head of a list and an int,  
inserts a new node on the front of the list. */
void push(Node** head_ref, int new_data)  
{  
    /* 1\. allocate node */
    Node* new_node = new Node();  

    /* 2\. put in the data */
    new_node->data = new_data;  

    /* 3\. Make next of new node as head */
    new_node->next = (*head_ref);  

    /* 4\. move the head to point to the new node */
    (*head_ref) = new_node;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

/* Given a reference (pointer to pointer) to the head of a list 
   and an int,  inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* 1\. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 

    /* 2\. put in the data  */
    new_node->data  = new_data; 

    /* 3\. Make next of new node as head */
    new_node->next = (*head_ref); 

    /* 4\. move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

```

## Java

```java

/* This function is in LinkedList class. Inserts a 
   new Node at front of the list. This method is  
   defined inside LinkedList class shown above */
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

```

## Python

```py

# This function is in LinkedList class 
# Function to insert a new node at the beginning 
def push(self, new_data): 

    # 1 & 2: Allocate the Node & 
    #        Put in the data 
    new_node = Node(new_data) 

    # 3\. Make next of new Node as head 
    new_node.next = self.head 

    # 4\. Move the head to point to new Node  
    self.head = new_node 

```

## C#

```cs

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

```

push（）的时间复杂度为`O(1)`，因为它要做的工作量是恒定的。

**在给定节点之后添加一个节点：（5 个步骤的过程）**

我们得到指向节点的指针，并将新节点插入给定节点之后。

![linkedlist_insert_middle](img/b6bf7ceee6de4eb0511ffb8bb649abfb.png) 

## C++

```cpp

// Given a node prev_node, insert a  
// new node after the given   
// prev_node 
void insertAfter(Node* prev_node, int new_data)   
{ 

    // 1\. Check if the given prev_node is NULL  
    if (prev_node == NULL)   
    {   
        cout << "the given previous node cannot be NULL";   
        return;   
    }  

    // 2\. Allocate new node 
    Node* new_node = new Node();  

    // 3\. Put in the data  
    new_node->data = new_data;   

    // 4\. Make next of new node as  
    // next of prev_node  
    new_node->next = prev_node->next;   

    // 5\. move the next of prev_node 
    // as new_node  
    prev_node->next = new_node;   
}  

// This code is contributed by anmolgautam818

```

## C

```c

/* Given a node prev_node, insert a new node after the given  
prev_node */
void insertAfter(struct Node* prev_node, int new_data)  
{  
    /*1\. check if the given prev_node is NULL */
    if (prev_node == NULL)  
    {  
    printf("the given previous node cannot be NULL");      
    return;  
    }  

    /* 2\. allocate new node */
    struct Node* new_node =(struct Node*) malloc(sizeof(struct Node));  

    /* 3\. put in the data */
    new_node->data = new_data;  

    /* 4\. Make next of new node as next of prev_node */
    new_node->next = prev_node->next;  

    /* 5\. move the next of prev_node as new_node */
    prev_node->next = new_node;  
}

```

## Java

```java

/* This function is in LinkedList class.  
Inserts a new node after the given prev_node. This method is  
defined inside LinkedList class shown above */
public void insertAfter(Node prev_node, int new_data)  
{  
    /* 1\. Check if the given Node is null */
    if (prev_node == null)  
    {  
        System.out.println("The given previous node cannot be null");  
        return;  
    }  

    /* 2\. Allocate the Node &  
    3\. Put in the data*/
    Node new_node = new Node(new_data);  

    /* 4\. Make next of new Node as next of prev_node */
    new_node.next = prev_node.next;  

    /* 5\. make next of prev_node as new_node */
    prev_node.next = new_node;  
}

```

## Python

```py

# This function is in LinkedList class.  
# Inserts a new node after the given prev_node. This method is  
# defined inside LinkedList class shown above */  
def insertAfter(self, prev_node, new_data):  

    # 1\. check if the given prev_node exists  
    if prev_node is None:  
        print "The given previous node must inLinkedList."
        return

    # 2\. Create new node &  
    # 3\. Put in the data  
    new_node = Node(new_data)  

    # 4\. Make next of new Node as next of prev_node  
    new_node.next = prev_node.next

    # 5\. make next of prev_node as new_node  
    prev_node.next = new_node

```

## C#

```cs

/* Inserts a new node after the given prev_node. */
public void insertAfter(Node prev_node,  
                        int new_data)  
{  
    /* 1\. Check if the given Node is null */
    if (prev_node == null)  
    {  
        Console.WriteLine("The given previous node" +  
                                " cannot be null");  
        return;  
    }  

    /* 2 & 3: Allocate the Node &  
            Put in the data*/
    Node new_node = new Node(new_data);  

    /* 4\. Make next of new Node as  
                next of prev_node */
    new_node.next = prev_node.next;  

    /* 5\. make next of prev_node  
                    as new_node */
    prev_node.next = new_node;  
}  

```

insertAfter（）的时间复杂度为`O(1)`，因为它的工作量是恒定的。

**在最后添加一个节点：（6 个步骤的过程）**

新节点总是添加在给定链接列表的最后一个节点之后。 例如，如果给定的链接列表为 5- > 10- > 15- > 20- > 25，并且我们在末尾添加了项目 30，则链接列表将变为 5- > 10 -> 15- > 20- > 25- >30。

由于链接列表通常由其开头表示，因此我们必须遍历该列表直到结尾，然后更改下一个 最后一个节点到新节点的数量。

![linkedlist_insert_last](img/428a5c975bfca4a1c08bc29cf2a6e78a.png)

以下是最后添加节点的 6 个步骤。

## C++

```cpp

// Given a reference (pointer to pointer) to the head   
// of a list and an int, appends a new node at the end  
void append(Node** head_ref, int new_data)   
{   

    // 1\. allocate node  
    Node* new_node = new Node();  

    // Used in step 5  
    Node *last = *head_ref;  

    // 2\. Put in the data  
    new_node->data = new_data;   

    // 3\. This new node is going to be   
    // the last node, so make next of   
    // it as NULL 
    new_node->next = NULL;   

    // 4\. If the Linked List is empty,  
    // then make the new node as head  
    if (*head_ref == NULL)   
    {   
        *head_ref = new_node;   
        return;   
    }   

    // 5\. Else traverse till the last node  
    while (last->next != NULL)   
        last = last->next;   

    // 6\. Change the next of last node  
    last->next = new_node;   
    return;   
}   

// This code is contributed by anmolgautam818

```

## C

```c

/* Given a reference (pointer to pointer) to the head 
   of a list and an int, appends a new node at the end  */
void append(struct Node** head_ref, int new_data) 
{ 
    /* 1\. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 

    struct Node *last = *head_ref;  /* used in step 5*/

    /* 2\. put in the data  */
    new_node->data  = new_data; 

    /* 3\. This new node is going to be the last node, so make next  
          of it as NULL*/
    new_node->next = NULL; 

    /* 4\. If the Linked List is empty, then make the new node as head */
    if (*head_ref == NULL) 
    { 
       *head_ref = new_node; 
       return; 
    }   

    /* 5\. Else traverse till the last node */
    while (last->next != NULL) 
        last = last->next; 

    /* 6\. Change the next of last node */
    last->next = new_node; 
    return;     
} 

```

## Java

```java

/* Appends a new node at the end.  This method is  
   defined inside LinkedList class shown above */
public void append(int new_data) 
{ 
    /* 1\. Allocate the Node & 
       2\. Put in the data 
       3\. Set next as null */
    Node new_node = new Node(new_data); 

    /* 4\. If the Linked List is empty, then make the 
           new node as head */
    if (head == null) 
    { 
        head = new Node(new_data); 
        return; 
    } 

    /* 4\. This new node is going to be the last node, so 
         make next of it as null */
    new_node.next = null; 

    /* 5\. Else traverse till the last node */
    Node last = head;  
    while (last.next != null) 
        last = last.next; 

    /* 6\. Change the next of last node */
    last.next = new_node; 
    return; 
} 

```

## Python

```py

# This function is defined in Linked List class 
# Appends a new node at the end.  This method is 
#  defined inside LinkedList class shown above */ 
def append(self, new_data): 

   # 1\. Create a new node 
   # 2\. Put in the data 
   # 3\. Set next as None 
   new_node = Node(new_data) 

   # 4\. If the Linked List is empty, then make the 
   #    new node as head 
   if self.head is None: 
        self.head = new_node 
        return

   # 5\. Else traverse till the last node 
   last = self.head 
   while (last.next): 
       last = last.next

   # 6\. Change the next of last node 
   last.next =  new_node 

```

## C#

```cs

/* Appends a new node at the end. This method is  
defined inside LinkedList class shown above */
public void append(int new_data) 
{ 
    /* 1\. Allocate the Node & 
    2\. Put in the data 
    3\. Set next as null */
    Node new_node = new Node(new_data); 

    /* 4\. If the Linked List is empty,  
       then make the new node as head */
    if (head == null) 
    { 
        head = new Node(new_data); 
        return; 
    } 

    /* 4\. This new node is going to be  
    the last node, so make next of it as null */
    new_node.next = null; 

    /* 5\. Else traverse till the last node */
    Node last = head;  
    while (last.next != null) 
        last = last.next; 

    /* 6\. Change the next of last node */
    last.next = new_node; 
    return; 
} 

```

append 的时间复杂度为`O(n)`，其中 n 是链表中节点的数量。 由于从头到尾都有一个循环，因此该函数可以执行`O(n)`。

还可以通过保留指向链表尾部的额外指针/

**，将该方法优化为在`O(1)`中工作，以下是使用上述所有方法创建链表的完整程序 。**

## C++

```cpp

// A complete working C++ program to demonstrate  
//  all insertion methods on Linked List  
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node  
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Given a reference (pointer to pointer) 
to the head of a list and an int, inserts 
a new node on the front of the list. */
void push(Node** head_ref, int new_data)  
{  
    /* 1\. allocate node */
    Node* new_node = new Node(); 

    /* 2\. put in the data */
    new_node->data = new_data;  

    /* 3\. Make next of new node as head */
    new_node->next = (*head_ref);  

    /* 4\. move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Given a node prev_node, insert a new node after the given  
prev_node */
void insertAfter(Node* prev_node, int new_data)  
{  
    /*1\. check if the given prev_node is NULL */
    if (prev_node == NULL)  
    {  
        cout<<"the given previous node cannot be NULL";  
        return;  
    }  

    /* 2\. allocate new node */
    Node* new_node = new Node(); 

    /* 3\. put in the data */
    new_node->data = new_data;  

    /* 4\. Make next of new node as next of prev_node */
    new_node->next = prev_node->next;  

    /* 5\. move the next of prev_node as new_node */
    prev_node->next = new_node;  
}  

/* Given a reference (pointer to pointer) to the head  
of a list and an int, appends a new node at the end */
void append(Node** head_ref, int new_data)  
{  
    /* 1\. allocate node */
    Node* new_node = new Node(); 

    Node *last = *head_ref; /* used in step 5*/

    /* 2\. put in the data */
    new_node->data = new_data;  

    /* 3\. This new node is going to be  
    the last node, so make next of  
    it as NULL*/
    new_node->next = NULL;  

    /* 4\. If the Linked List is empty, 
    then make the new node as head */
    if (*head_ref == NULL)  
    {  
        *head_ref = new_node;  
        return;  
    }  

    /* 5\. Else traverse till the last node */
    while (last->next != NULL)  
        last = last->next;  

    /* 6\. Change the next of last node */
    last->next = new_node;  
    return;  
}  

// This function prints contents of 
// linked list starting from head  
void printList(Node *node)  
{  
    while (node != NULL)  
    {  
        cout<<" "<<node->data;  
        node = node->next;  
    }  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    // Insert 6\. So linked list becomes 6->NULL  
    append(&head, 6);  

    // Insert 7 at the beginning.  
    // So linked list becomes 7->6->NULL  
    push(&head, 7);  

    // Insert 1 at the beginning.  
    // So linked list becomes 1->7->6->NULL  
    push(&head, 1);  

    // Insert 4 at the end. So  
    // linked list becomes 1->7->6->4->NULL  
    append(&head, 4);  

    // Insert 8, after 7\. So linked  
    // list becomes 1->7->8->6->4->NULL  
    insertAfter(head->next, 8);  

    cout<<"Created Linked list is: ";  
    printList(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// A complete working C program to demonstrate all insertion methods 
// on Linked List 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node 
{ 
  int data; 
  struct Node *next; 
}; 

/* Given a reference (pointer to pointer) to the head of a list and  
   an int, inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* 1\. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 

    /* 2\. put in the data  */
    new_node->data  = new_data; 

    /* 3\. Make next of new node as head */
    new_node->next = (*head_ref); 

    /* 4\. move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Given a node prev_node, insert a new node after the given  
   prev_node */
void insertAfter(struct Node* prev_node, int new_data) 
{ 
    /*1\. check if the given prev_node is NULL */
    if (prev_node == NULL) 
    { 
      printf("the given previous node cannot be NULL"); 
      return; 
    } 

    /* 2\. allocate new node */
    struct Node* new_node =(struct Node*) malloc(sizeof(struct Node)); 

    /* 3\. put in the data  */
    new_node->data  = new_data; 

    /* 4\. Make next of new node as next of prev_node */
    new_node->next = prev_node->next; 

    /* 5\. move the next of prev_node as new_node */
    prev_node->next = new_node; 
} 

/* Given a reference (pointer to pointer) to the head 
   of a list and an int, appends a new node at the end  */
void append(struct Node** head_ref, int new_data) 
{ 
    /* 1\. allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 

    struct Node *last = *head_ref;  /* used in step 5*/

    /* 2\. put in the data  */
    new_node->data  = new_data; 

    /* 3\. This new node is going to be the last node, so make next of 
          it as NULL*/
    new_node->next = NULL; 

    /* 4\. If the Linked List is empty, then make the new node as head */
    if (*head_ref == NULL) 
    { 
       *head_ref = new_node; 
       return; 
    } 

    /* 5\. Else traverse till the last node */
    while (last->next != NULL) 
        last = last->next; 

    /* 6\. Change the next of last node */
    last->next = new_node; 
    return; 
} 

// This function prints contents of linked list starting from head 
void printList(struct Node *node) 
{ 
  while (node != NULL) 
  { 
     printf(" %d ", node->data); 
     node = node->next; 
  } 
} 

/* Driver program to test above functions*/
int main() 
{ 
  /* Start with the empty list */
  struct Node* head = NULL; 

  // Insert 6.  So linked list becomes 6->NULL 
  append(&head, 6); 

  // Insert 7 at the beginning. So linked list becomes 7->6->NULL 
  push(&head, 7); 

  // Insert 1 at the beginning. So linked list becomes 1->7->6->NULL 
  push(&head, 1); 

  // Insert 4 at the end. So linked list becomes 1->7->6->4->NULL 
  append(&head, 4); 

  // Insert 8, after 7\. So linked list becomes 1->7->8->6->4->NULL 
  insertAfter(head->next, 8); 

  printf("\n Created Linked list is: "); 
  printList(head); 

  return 0; 
} 

```

## Java

```java

// A complete working Java program to demonstrate all insertion methods 
// on linked list 
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

    /* Inserts a new node after the given prev_node. */
    public void insertAfter(Node prev_node, int new_data) 
    { 
        /* 1\. Check if the given Node is null */
        if (prev_node == null) 
        { 
            System.out.println("The given previous node cannot be null"); 
            return; 
        } 

        /* 2 & 3: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 4\. Make next of new Node as next of prev_node */
        new_node.next = prev_node.next; 

        /* 5\. make next of prev_node as new_node */
        prev_node.next = new_node; 
    } 

    /* Appends a new node at the end.  This method is  
       defined inside LinkedList class shown above */
    public void append(int new_data) 
    { 
        /* 1\. Allocate the Node & 
           2\. Put in the data 
           3\. Set next as null */
        Node new_node = new Node(new_data); 

        /* 4\. If the Linked List is empty, then make the 
              new node as head */
        if (head == null) 
        { 
            head = new Node(new_data); 
            return; 
        } 

        /* 4\. This new node is going to be the last node, so 
              make next of it as null */
        new_node.next = null; 

        /* 5\. Else traverse till the last node */
        Node last = head;  
        while (last.next != null) 
            last = last.next; 

        /* 6\. Change the next of last node */
        last.next = new_node; 
        return; 
    } 

    /* This function prints contents of linked list starting from 
        the given node */
    public void printList() 
    { 
        Node tnode = head; 
        while (tnode != null) 
        { 
            System.out.print(tnode.data+" "); 
            tnode = tnode.next; 
        } 
    } 

    /* Driver program to test above functions. Ideally this function 
       should be in a separate user class.  It is kept here to keep 
       code compact */
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        LinkedList llist = new LinkedList(); 

        // Insert 6.  So linked list becomes 6->NUllist 
        llist.append(6); 

        // Insert 7 at the beginning. So linked list becomes 
        // 7->6->NUllist 
        llist.push(7); 

        // Insert 1 at the beginning. So linked list becomes 
        // 1->7->6->NUllist 
        llist.push(1); 

        // Insert 4 at the end. So linked list becomes 
        // 1->7->6->4->NUllist 
        llist.append(4); 

        // Insert 8, after 7\. So linked list becomes 
        // 1->7->8->6->4->NUllist 
        llist.insertAfter(llist.head.next, 8); 

        System.out.println("\nCreated Linked list is: "); 
        llist.printList(); 
    } 
} 
// This code is contributed by Rajat Mishra 

```

## Python

```py

# A complete working Python program to demonstrate all 
# insertion methods of linked list 

# Node class 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data  # Assign data 
        self.next = None  # Initialize next as null 

# Linked List class contains a Node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Functio to insert a new node at the beginning 
    def push(self, new_data): 

        # 1 & 2: Allocate the Node & 
        #        Put in the data 
        new_node = Node(new_data) 

        # 3\. Make next of new Node as head 
        new_node.next = self.head 

        # 4\. Move the head to point to new Node 
        self.head = new_node 

    # This function is in LinkedList class. Inserts a 
    # new node after the given prev_node. This method is 
    # defined inside LinkedList class shown above */ 
    def insertAfter(self, prev_node, new_data): 

        # 1\. check if the given prev_node exists 
        if prev_node is None: 
            print "The given previous node must inLinkedList."
            return

        #  2\. create new node & 
        #      Put in the data 
        new_node = Node(new_data) 

        # 4\. Make next of new Node as next of prev_node 
        new_node.next = prev_node.next

        # 5\. make next of prev_node as new_node 
        prev_node.next = new_node 

    # This function is defined in Linked List class 
    # Appends a new node at the end.  This method is 
    # defined inside LinkedList class shown above */ 
    def append(self, new_data): 

        # 1\. Create a new node 
        # 2\. Put in the data 
        # 3\. Set next as None 
        new_node = Node(new_data) 

        # 4\. If the Linked List is empty, then make the 
        #    new node as head 
        if self.head is None: 
            self.head = new_node 
            return

        # 5\. Else traverse till the last node 
        last = self.head 
        while (last.next): 
            last = last.next

        # 6\. Change the next of last node 
        last.next =  new_node 

    # Utility function to print the linked list 
    def printList(self): 
        temp = self.head 
        while (temp): 
            print temp.data, 
            temp = temp.next

# Code execution starts here 
if __name__=='__main__': 

    # Start with the empty list 
    llist = LinkedList() 

    # Insert 6.  So linked list becomes 6->None 
    llist.append(6) 

    # Insert 7 at the beginning. So linked list becomes 7->6->None 
    llist.push(7); 

    # Insert 1 at the beginning. So linked list becomes 1->7->6->None 
    llist.push(1); 

    # Insert 4 at the end. So linked list becomes 1->7->6->4->None 
    llist.append(4) 

    # Insert 8, after 7\. So linked list becomes 1 -> 7-> 8-> 6-> 4-> None 
    llist.insertAfter(llist.head.next, 8) 

    print 'Created linked list is:', 
    llist.printList() 

# This code is contributed by Manikantan Narasimhan 

```

## C#

```cs

// A complete working C# program to demonstrate  
// all insertion methods on linked list 
using System; 

class GFG 
{ 
    public Node head; // head of list 

    /* Linked list Node*/
    public class Node 
    { 
        public int data; 
        public Node next; 
        public Node(int d) {data = d; next = null;} 
    } 

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

    /* Inserts a new node after the given prev_node. */
    public void insertAfter(Node prev_node, int new_data) 
    { 
        /* 1\. Check if the given Node is null */
        if (prev_node == null) 
        { 
            Console.WriteLine("The given previous" +  
                              " node cannot be null"); 
            return; 
        } 

        /* 2 & 3: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 4\. Make next of new Node as 
              next of prev_node */
        new_node.next = prev_node.next; 

        /* 5\. make next of prev_node as new_node */
        prev_node.next = new_node; 
    } 

    /* Appends a new node at the end. This method is  
    defined inside LinkedList class shown above */
    public void append(int new_data) 
    { 
        /* 1\. Allocate the Node & 
        2\. Put in the data 
        3\. Set next as null */
        Node new_node = new Node(new_data); 

        /* 4\. If the Linked List is empty, 
        then make the new node as head */
        if (head == null) 
        { 
            head = new Node(new_data); 
            return; 
        } 

        /* 4\. This new node is going to be the last node,  
            so make next of it as null */
        new_node.next = null; 

        /* 5\. Else traverse till the last node */
        Node last = head;  
        while (last.next != null) 
            last = last.next; 

        /* 6\. Change the next of last node */
        last.next = new_node; 
        return; 
    } 

    /* This function prints contents of linked list  
    starting from the given node */
    public void printList() 
    { 
        Node tnode = head; 
        while (tnode != null) 
        { 
            Console.Write(tnode.data + " "); 
            tnode = tnode.next; 
        } 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        /* Start with the empty list */
        GFG llist = new GFG(); 

        // Insert 6\. So linked list becomes 6->NUllist 
        llist.append(6); 

        // Insert 7 at the beginning.  
        // So linked list becomes 7->6->NUllist 
        llist.push(7); 

        // Insert 1 at the beginning.  
        // So linked list becomes 1->7->6->NUllist 
        llist.push(1); 

        // Insert 4 at the end. So linked list becomes 
        // 1->7->6->4->NUllist 
        llist.append(4); 

        // Insert 8, after 7\. So linked list becomes 
        // 1->7->8->6->4->NUllist 
        llist.insertAfter(llist.head.next, 8); 

        Console.Write("Created Linked list is: "); 
        llist.printList(); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
 Created Linked list is:  1  7  8  6  4

```

您可能想尝试 [**在链表**](http://quiz.geeksforgeeks.org/data-structure/linked-list/)

上练习 MCQ 问题 。

