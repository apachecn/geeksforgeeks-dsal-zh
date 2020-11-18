# 反转双向链接列表

编写 C 函数以反转给定的双链表

例如，请参见下图。

```
 (a) Original Doubly Linked List 

```

![](img/ac986bf04212b6c02bcab8a71a5727c1.png)

```
 (b) Reversed Doubly Linked List 
```

![](img/f8570d09b2d0146b6381105d1bf628ac.png)

这是一种用于反转双链表的简单方法。 我们需要做的就是交换所有节点的 prev 和 next 指针，更改 head 的 prev（或 start），最后更改 head 的指针。

## C++

```cpp

/* C++ program to reverse a doubly linked list */
#include <bits/stdc++.h>
using namespace std;

/* a node of the doubly linked list */
class Node 
{ 
    public:
    int data; 
    Node *next; 
    Node *prev; 
}; 

/* Function to reverse a Doubly Linked List */
void reverse(Node **head_ref) 
{ 
    Node *temp = NULL; 
    Node *current = *head_ref; 

    /* swap next and prev for all nodes of 
    doubly linked list */
    while (current != NULL) 
    { 
        temp = current->prev; 
        current->prev = current->next; 
        current->next = temp;             
        current = current->prev; 
    } 

    /* Before changing the head, check for the cases like empty 
        list and list with only one node */
    if(temp != NULL ) 
        *head_ref = temp->prev; 
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the
beginging of the Doubly Linked List */
void push(Node** head_ref, int new_data) 
{ 
    /* allocate node */
    Node* new_node = new Node();

    /* put in the data */
    new_node->data = new_data; 

    /* since we are adding at the beginning, 
    prev is always NULL */
    new_node->prev = NULL; 

    /* link the old list off the new node */
    new_node->next = (*head_ref);     

    /* change prev of head node to new node */
    if((*head_ref) != NULL) 
    (*head_ref)->prev = new_node ; 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given doubly linked list 
This function is same as printList() of singly linked list */
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
    /* Start with the empty list */
    Node* head = NULL; 

    /* Let us create a sorted linked list to test the functions 
    Created linked list will be 10->8->4->2 */
    push(&head, 2); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 10); 

    cout << "Original Linked list" << endl; 
    printList(head); 

    /* Reverse doubly linked list */
    reverse(&head); 

    cout << "\nReversed Linked list" << endl; 
    printList(head);         

    return 0;
} 

// This code is contributed by rathbhupendra

```

## C

```c

/* Program to reverse a doubly linked list */
#include <stdio.h>
#include <stdlib.h>

/* a node of the doubly linked list */
struct Node
{
  int data;
  struct Node *next;
  struct Node *prev;    
};

/* Function to reverse a Doubly Linked List */
void reverse(struct Node **head_ref)
{
     struct Node *temp = NULL;  
     struct Node *current = *head_ref;

     /* swap next and prev for all nodes of 
       doubly linked list */
     while (current !=  NULL)
     {
       temp = current->prev;
       current->prev = current->next;
       current->next = temp;              
       current = current->prev;
     }      

     /* Before changing head, check for the cases like empty 
        list and list with only one node */
     if(temp != NULL )
        *head_ref = temp->prev;
}     

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging of the Doubly Linked List */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node =
            (struct Node*) malloc(sizeof(struct Node));

    /* put in the data  */
    new_node->data  = new_data;

    /* since we are adding at the beginning, 
      prev is always NULL */
    new_node->prev = NULL;

    /* link the old list off the new node */
    new_node->next = (*head_ref);    

    /* change prev of head node to new node */
    if((*head_ref) !=  NULL)
      (*head_ref)->prev = new_node ;    

    /* move the head to point to the new node */
    (*head_ref)    = new_node;
}

/* Function to print nodes in a given doubly linked list 
   This function is same as printList() of singly linked list */
void printList(struct Node *node)
{
  while(node!=NULL)
  {
   printf("%d ", node->data);
   node = node->next;
  }
} 

/* Driver code*/
int main()
{
  /* Start with the empty list */
  struct Node* head = NULL;

  /* Let us create a sorted linked list to test the functions
   Created linked list will be 10->8->4->2 */
  push(&head, 2);
  push(&head, 4);
  push(&head, 8);
  push(&head, 10);

  printf("\n Original Linked list ");
  printList(head);

  /* Reverse doubly linked list */
  reverse(&head);

  printf("\n Reversed Linked list ");
  printList(head);           

  getchar();
}

```

## Java

```java

// Java program to reverse a doubly linked list

class LinkedList {

    static Node head;

    static class Node {

        int data;
        Node next, prev;

        Node(int d)
        {
            data = d;
            next = prev = null;
        }
    }

    /* Function to reverse a Doubly Linked List */
    void reverse()
    {
        Node temp = null;
        Node current = head;

        /* swap next and prev for all nodes of
         doubly linked list */
        while (current != null) {
            temp = current.prev;
            current.prev = current.next;
            current.next = temp;
            current = current.prev;
        }

        /* Before changing head, check for the cases like
         empty list and list with only one node */
        if (temp != null) {
            head = temp.prev;
        }
    }

    /* UTILITY FUNCTIONS */
    /* Function to insert a node at the beginning of the
     * Doubly Linked List */
    void push(int new_data)
    {
        /* allocate node */
        Node new_node = new Node(new_data);

        /* since we are adding at the beginning,
         prev is always NULL */
        new_node.prev = null;

        /* link the old list off the new node */
        new_node.next = head;

        /* change prev of head node to new node */
        if (head != null) {
            head.prev = new_node;
        }

        /* move the head to point to the new node */
        head = new_node;
    }

    /* Function to print nodes in a given doubly linked list
     This function is same as printList() of singly linked
     list */
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();

        /* Let us create a sorted linked list to test the
         functions Created linked list will be 10->8->4->2
       */
        list.push(2);
        list.push(4);
        list.push(8);
        list.push(10);

        System.out.println("Original linked list ");
        list.printList(head);

        list.reverse();
        System.out.println("");
        System.out.println("The reversed Linked List is ");
        list.printList(head);
    }
}

// This code has been contributed by Mayank Jaiswal

```

## 蟒蛇

```

# Program to reverse a doubly linked list

# A node of the doubly linked list

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:
     # Constructor for empty Doubly Linked List
    def __init__(self):
        self.head = None

    # Function reverse a Doubly Linked List
    def reverse(self):
        temp = None
        current = self.head

        # Swap next and prev for all nodes of
        # doubly linked list
        while current is not None:
            temp = current.prev
            current.prev = current.next
            current.next = temp
            current = current.prev

        # Before changing head, check for the cases like
        # empty list and list with only one node
        if temp is not None:
            self.head = temp.prev

    # Given a reference to the head of a list and an
    # integer,inserts a new node on the front of list
    def push(self, new_data):

        # 1\. Allocates node
        # 2\. Put the data in it
        new_node = Node(new_data)

        # 3\. Make next of new node as head and
        # previous as None (already None)
        new_node.next = self.head

        # 4\. change prev of head node to new_node
        if self.head is not None:
            self.head.prev = new_node

        # 5\. move the head to point to the new node
        self.head = new_node

    def printList(self, node):
        while(node is not None):
            print node.data,
            node = node.next

# Driver code
dll = DoublyLinkedList()
dll.push(2)
dll.push(4)
dll.push(8)
dll.push(10)

print "\nOriginal Linked List"
dll.printList(dll.head)

# Reverse doubly linked list
dll.reverse()

print "\n Reversed Linked List"
dll.printList(dll.head)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)

```

## C#

```cs

// A C# program to reverse a doubly linked list
using System;

public class LinkedList {

    static Node head;

    class Node {

        public int data;
        public Node next, prev;

        public Node(int d)
        {
            data = d;
            next = prev = null;
        }
    }

    /* Function to reverse a Doubly Linked List */
    void reverse()
    {
        Node temp = null;
        Node current = head;

        /* swap next and prev for all nodes of
        doubly linked list */
        while (current != null) {
            temp = current.prev;
            current.prev = current.next;
            current.next = temp;
            current = current.prev;
        }

        /* Before changing head, check for
          the cases like empty list and
         list with only one node */
        if (temp != null) {
            head = temp.prev;
        }
    }

    /* UTILITY FUNCTIONS */
    /* Function to insert a node at the
    beginging of the Doubly Linked List */
    void push(int new_data)
    {

        /* allocate node */
        Node new_node = new Node(new_data);

        /* since we are adding at the beginning,
        prev is always NULL */
        new_node.prev = null;

        /* link the old list off the new node */
        new_node.next = head;

        /* change prev of head node to new node */
        if (head != null) {
            head.prev = new_node;
        }

        /* move the head to point to the new node */
        head = new_node;
    }

    /* Function to print nodes in a given
    doubly linked list This function is
    same as printList() of singly linked lsit */
    void printList(Node node)
    {
        while (node != null) {
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        LinkedList list = new LinkedList();

        /* Let us create a sorted linked list
        to test the functions Created linked
        list will be 10->8->4->2 */
        list.push(2);
        list.push(4);
        list.push(8);
        list.push(10);

        Console.WriteLine("Original linked list ");
        list.printList(head);

        list.reverse();
        Console.WriteLine("");
        Console.WriteLine("The reversed Linked List is ");
        list.printList(head);
    }
}

// This code is contributed by 29AjayKumar

```

**输出**：

```
Original linked list 
10 8 4 2 
The reversed Linked List is 
2 4 8 10 

```

**时间复杂度**：`O(n)`

我们也可以交换数据而不是指针来反转双链表。 [用于反转数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)的方法可用于交换数据。 如果数据项的大小更大，则与指针相比，交换数据的成本可能更高。

如果您发现上述任何代码/算法不正确，或者找到解决相同问题的更好方法，请发表评论。

**方法 2**：

通过使用堆栈也可以完成相同的问题。

脚步：

1.  继续将节点的数据压入堆栈。 ->`O(n)`

2.  不断弹出元素并更新双链表

## Java

```java

// Java program to reverse a doubly linked list
import java.util.*;
class LinkedList {

    static Node head;

    static class Node {

        int data;
        Node next, prev;

        Node(int d)
        {
            data = d;
            next = prev = null;
        }
    }

    /* Function to reverse a Doubly Linked List using Stacks
     */
    void reverse()
    {
        Stack<Integer> stack = new Stack<>();
        Node temp = head;
        while (temp != null)
        {
            stack.push(temp.data);
            temp = temp.next;
        } 
        // added all the elements sequemce wise in the
        // stack
        temp = head;
        while (temp != null) 
        {
            temp.data = stack.pop();
            temp = temp.next;
        } 
        // popped all the elements and the added in the
        // linked list,
        // which are in the reversed order.
    }

    /* UTILITY FUNCTIONS */
    /* Function to insert a node at the beginning of the
     * Doubly Linked List */
    void push(int new_data)
    {
        /* allocate node */
        Node new_node = new Node(new_data);

        /* since we are adding at the beginning,
         prev is always NULL */
        new_node.prev = null;

        /* link the old list off the new node */
        new_node.next = head;

        /* change prev of head node to new node */
        if (head != null)
        {
            head.prev = new_node;
        }

        /* move the head to point to the new node */
        head = new_node;
    }

    /* Function to print nodes in a given doubly linked list
     This function is same as printList() of singly linked
     list */
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();

        /* Let us create a sorted linked list to test the
         functions Created linked list will be 10->8->4->2
       */
        list.push(2);
        list.push(4);
        list.push(8);
        list.push(10);

        System.out.println("Original linked list ");
        list.printList(head);

        list.reverse();
        System.out.println("");
        System.out.println("The reversed Linked List is ");
        list.printList(head);
    }
}

// This code has been contributed by Rashita Mehta

```

**Output**

```
Original linked list 
10 8 4 2 
The reversed Linked List is 
2 4 8 10 
```

**时间复杂度**：`O(n)`

在这种方法中，我们一次遍历链表并将元素添加到堆栈中，然后再次遍历整个列表以更新所有元素。 整个过程耗时 2n，即`O(n)`的时间复杂度。

