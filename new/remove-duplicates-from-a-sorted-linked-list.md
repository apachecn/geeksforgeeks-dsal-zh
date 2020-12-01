# 从排序的链表中删除重复项

> 原文：[https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)

编写一个函数，该函数采用以非降序排列的列表，并从列表中删除所有重复的节点。 该列表仅应遍历一次。

例如，如果链表是`11 -> 11 -> 11 -> 21 -> 43 -> 43 -> 60`，则`removeDuplicates()`应该将列表转换为`11 -> 21 -> 43 -> 60`。

**算法**：

从头（或起始）节点遍历列表。 遍历时，将每个节点与其下一个节点进行比较。 如果下一个节点的数据与当前节点相同，则删除下一个节点。 在删除节点之前，我们需要存储该节点的下一个指针

**实现**：

除了`removeDuplicates()`之外的其他功能仅用于创建链接链表并测试`removeDuplicates()`。

## C++

```cpp

/* C++ Program to remove duplicates from a sorted linked list */
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* The function removes duplicates from a sorted list */
void removeDuplicates(Node* head)  
{  
    /* Pointer to traverse the linked list */
    Node* current = head;  

    /* Pointer to store the next pointer of a node to be deleted*/
    Node* next_next;  

    /* do nothing if the list is empty */
    if (current == NULL)  
    return;  

    /* Traverse the list till last node */
    while (current->next != NULL)  
    {  
    /* Compare current node with next node */
    if (current->data == current->next->data)  
    {  
        /* The sequence of steps is important*/        
        next_next = current->next->next;  
        free(current->next);  
        current->next = next_next;  
    }  
    else /* This is tricky: only advance if no deletion */
    {  
        current = current->next;  
    }  
    }  
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging of the linked list */
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
    while (node!=NULL)  
    {  
        cout<<" "<<node->data;  
        node = node->next;  
    }  
}  

/* Driver program to test above functions*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Let us create a sorted linked list to test the functions  
    Created linked list will be 11->11->11->13->13->20 */
    push(&head, 20);  
    push(&head, 13);  
    push(&head, 13);  
    push(&head, 11);  
    push(&head, 11);  
    push(&head, 11);                                      

    cout<<"Linked list before duplicate removal ";  
    printList(head);  

    /* Remove duplicates from linked list */
    removeDuplicates(head);  

    cout<<"\nLinked list after duplicate removal ";      
    printList(head);              

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

/* C Program to remove duplicates from a sorted linked list */
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* The function removes duplicates from a sorted list */
void removeDuplicates(struct Node* head) 
{ 
    /* Pointer to traverse the linked list */
    struct Node* current = head; 

    /* Pointer to store the next pointer of a node to be deleted*/
    struct Node* next_next;  

    /* do nothing if the list is empty */
    if (current == NULL)  
       return;  

    /* Traverse the list till last node */
    while (current->next != NULL)  
    { 
       /* Compare current node with next node */
       if (current->data == current->next->data)  
       { 
           /* The sequence of steps is important*/               
           next_next = current->next->next; 
           free(current->next); 
           current->next = next_next;   
       } 
       else /* This is tricky: only advance if no deletion */
       { 
          current = current->next;  
       } 
    } 
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging of the linked list */
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
    while (node!=NULL) 
    { 
       printf("%d ", node->data); 
       node = node->next; 
    } 
}  

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create a sorted linked list to test the functions 
     Created linked list will be 11->11->11->13->13->20 */
    push(&head, 20); 
    push(&head, 13); 
    push(&head, 13);   
    push(&head, 11); 
    push(&head, 11); 
    push(&head, 11);                                     

    printf("\n Linked list before duplicate removal  "); 
    printList(head);  

    /* Remove duplicates from linked list */
    removeDuplicates(head);  

    printf("\n Linked list after duplicate removal ");          
    printList(head);             

    return 0; 
} 

```

## Java

```java

// Java program to remove duplicates from a sorted linked list 
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

    void removeDuplicates() 
    { 
        /*Another reference to head*/
        Node curr = head; 

        /* Traverse list till the last node */
        while (curr != null) { 
             Node temp = curr; 
            /*Compare current node with the next node and  
            keep on deleting them until it matches the current  
            node data */
            while(temp!=null && temp.data==curr.data) { 
                temp = temp.next; 
            } 
            /*Set current node next to the next different  
            element denoted by temp*/
            curr.next = temp; 
            curr = curr.next; 
        } 
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
        llist.push(20); 
        llist.push(13); 
        llist.push(13); 
        llist.push(11); 
        llist.push(11); 
        llist.push(11); 

        System.out.println("List before removal of duplicates"); 
        llist.printList(); 

        llist.removeDuplicates(); 

        System.out.println("List after removal of elements"); 
        llist.printList(); 
    } 
}  
/* This code is contributed by Rajat Mishra */    

```

## Python 3

```

# Python3 program to remove duplicate 
# nodes from a sorted linked list  

# Node class  
class Node:  

    # Constructor to initialize  
    # the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

class LinkedList:  

    # Function to initialize head  
    def __init__(self):  
        self.head = None

    # Function to insert a new node  
    # at the beginning  
    def push(self, new_data):  
        new_node = Node(new_data)  
        new_node.next = self.head  
        self.head = new_node  

    # Given a reference to the head of a  
    # list and a key, delete the first  
    # occurence of key in linked list  
    def deleteNode(self, key):  

        # Store head node  
        temp = self.head  

        # If head node itself holds the  
        # key to be deleted  
        if (temp is not None):  
            if (temp.data == key):  
                self.head = temp.next
                temp = None
                return

        # Search for the key to be deleted,  
        # keep track of the previous node as 
        # we need to change 'prev.next'  
        while(temp is not None):  
            if temp.data == key:  
                break
            prev = temp  
            temp = temp.next

        # if key was not present in  
        # linked list  
        if(temp == None):  
            return

        # Unlink the node from linked list  
        prev.next = temp.next

        temp = None

    # Utility function to print the  
    # linked LinkedList  
    def printList(self):  
        temp = self.head  
        while(temp):  
            print(temp.data , end = ' ') 
            temp = temp.next

    # This function removes duplicates  
    # from a sorted list          
    def removeDuplicates(self): 
        temp = self.head 
        if temp is None: 
            return
        while temp.next is not None: 
            if temp.data == temp.next.data: 
                new = temp.next.next
                temp.next = None
                temp.next = new 
            else: 
                temp = temp.next
        return self.head 

# Driver Code  
llist = LinkedList()  

llist.push(20)  
llist.push(13)  
llist.push(13) 
llist.push(11) 
llist.push(11) 
llist.push(11) 
print ("Created Linked List: ") 
llist.printList()  
print() 
print("Linked List after removing",  
             "duplicate elements:") 
llist.removeDuplicates() 
llist.printList()  

# This code is contributed by  
# Dushyant Pathak. 

```

## C#

```cs

// C# program to remove duplicates 
// from a sorted linked list 
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
            data = d; next = null; 
        } 
    } 

    void removeDuplicates() 
    { 
        /*Another reference to head*/
        Node current = head; 

        /* Pointer to store the next  
        pointer of a node to be deleted*/
        Node next_next; 

        /* do nothing if the list is empty */
        if (head == null)  
            return; 

        /* Traverse list till the last node */
        while (current.next != null)  
        { 

            /*Compare current node with the next node */
            if (current.data == current.next.data)  
            { 
                next_next = current.next.next; 
                current.next = null; 
                current.next = next_next; 
            } 
            else // advance if no deletion 
                current = current.next; 
        } 
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

    /* Driver code */
    public static void Main(String []args) 
    { 
        LinkedList llist = new LinkedList(); 
        llist.push(20); 
        llist.push(13); 
        llist.push(13); 
        llist.push(11); 
        llist.push(11); 
        llist.push(11); 

        Console.WriteLine("List before removal of duplicates"); 
        llist.printList(); 

        llist.removeDuplicates(); 

        Console.WriteLine("List after removal of elements"); 
        llist.printList(); 
    } 
}  

/* This code is contributed by 29AjayKumar */

```

**输出**：

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20

```

**时间复杂度**：`O(n)`，其中`n`是给定链表中的节点数。

**递归方法**：

## C++

```cpp

/* C++ Program to remove duplicates 
from a sorted linked list */
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* The function removes duplicates  
from a sorted list */
void removeDuplicates(Node* head)  
{  
    /* Pointer to store the pointer of a node to be deleted*/
    Node* to_free;  

    /* do nothing if the list is empty */
    if (head == NULL)  
        return;  

    /* Traverse the list till last node */
    if (head->next != NULL)  
    {  

        /* Compare head node with next node */
        if (head->data == head->next->data)  
        {  
            /* The sequence of steps is important. 
              to_free pointer stores the next of head 
             pointer which is to be deleted.*/    
            to_free = head->next;  
        head->next = head->next->next; 
        free(to_free); 
        removeDuplicates(head); 
        }  
        else /* This is tricky: only  
        advance if no deletion */
        {  
            removeDuplicates(head->next); 
        }  
    }  
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the 
beginging of the linked list */
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

/* Function to print nodes  
in a given linked list */
void printList(Node *node)  
{  
    while (node!=NULL)  
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

    /* Let us create a sorted linked 
    list to test the functions  
    Created linked list will be  
    11->11->11->13->13->20 */
    push(&head, 20);  
    push(&head, 13);  
    push(&head, 13);  
    push(&head, 11);  
    push(&head, 11);  
    push(&head, 11);                                      

    cout<<"Linked list before duplicate removal ";  
    printList(head);  

    /* Remove duplicates from linked list */
    removeDuplicates(head);  

    cout<<"\nLinked list after duplicate removal ";      
    printList(head);              

    return 0;  
}  
// This code is contributed by Ashita Gupta 

```

## C

```c

/* C recursive Program to remove duplicates from a sorted linked list */
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 
/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging of the linked list */
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
    while (node!=NULL) 
    { 
       printf("%d ", node->data); 
       node = node->next; 
    } 
}  

 Node* deleteDuplicates(Node* head) { 
        if (head == nullptr) return nullptr; 
        if (head->next == nullptr) return head; 

        if (head->data == head->next->data) { 
            Node *tmp; 
            // If find next element duplicate, preserve the next pointer to be deleted,  
            // skip it, and then delete the stored one. Return head 
            tmp = head->next; 
            head->next = head->next->next; 
            free(tmp); 
            return deleteDuplicates(head); 
        } 

        else { 

            // if doesn't find next element duplicate, leave head  
            // and check from next element 
            head->next = deleteDuplicates(head->next); 
            return head; 
        } 
    } 

int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create a sorted linked list to test the functions 
     Created linked list will be 11->11->11->13->13->20 */
    push(&head, 20); 
    push(&head, 13); 
    push(&head, 13);   
    push(&head, 11); 
    push(&head, 11); 
    push(&head, 11);                                     

    printf("\n Linked list before duplicate removal  "); 
    printList(head);  

    /* Remove duplicates from linked list */
    head = deleteDuplicates(head);  

    printf("\n Linked list after duplicate removal ");          
    printList(head);             

    return 0; 
} 
/* This code is contributed by Yogesh shukla */   

```

## Java

```java

// Java Program to remove duplicates 
// from a sorted linked list  
class GFG 
{ 
/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
};  

// The function removes duplicates 
// from a sorted list  
static Node removeDuplicates(Node head)  
{  
    /* Pointer to store the pointer 
    of a node to be deleted*/
    Node to_free;  

    /* do nothing if the list is empty */
    if (head == null)  
        return null;  

    /* Traverse the list till last node */
    if (head.next != null)  
    {  

        /* Compare head node with next node */
        if (head.data == head.next.data)  
        {  
            /* The sequence of steps is important. 
            to_free pointer stores the next of head 
            pointer which is to be deleted.*/
            to_free = head.next;  
            head.next = head.next.next; 
            removeDuplicates(head); 
        }  

        /* This is tricky: only advance if no deletion */
        else 
        {  
            removeDuplicates(head.next); 
        }  
    }  
    return head; 
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging 
of the linked list */
static Node push(Node head_ref, 
                 int new_data)  
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

/* Function to print nodes in a given linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(" " + node.data);  
        node = node.next;  
    }  
}  

/* Driver code*/
public static void main(String args[]) 
{  
    /* Start with the empty list */
    Node head = null;  

    /* Let us create a sorted linked list 
    to test the functions  
    Created linked list will be 11.11.11.13.13.20 */
    head = push(head, 20);  
    head = push(head, 13);  
    head = push(head, 13);  
    head = push(head, 11);  
    head = push(head, 11);  
    head = push(head, 11);                                      

    System.out.println("Linked list before" +  
                      " duplicate removal ");  
    printList(head);  

    /* Remove duplicates from linked list */
    head = removeDuplicates(head);  

    System.out.println("\nLinked list after" +  
                       " duplicate removal ");      
    printList(head);              
} 
}   

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 Program to remove duplicates 
# from a sorted linked list  
import math 

# Link list node  
class Node:  
    def __init__(self,data):  
        self.data = data  
        self.next = None

# The function removes duplicates  
# from a sorted list  
def removeDuplicates(head):  

    # Pointer to store the pointer of a node  
    # to be deleted to_free  

    # do nothing if the list is empty  
    if (head == None):  
        return

    # Traverse the list till last node  
    if (head.next != None):  

        # Compare head node with next node  
        if (head.data == head.next.data):  

            # The sequence of steps is important.  
            # to_free pointer stores the next of head  
            # pointer which is to be deleted.  
            to_free = head.next
            head.next = head.next.next

            # free(to_free)  
            removeDuplicates(head)  

        # This is tricky: only advance if no deletion 
        else:  
            removeDuplicates(head.next)  

    return head 

# UTILITY FUNCTIONS  
# Function to insert a node at the  
# beginging of the linked list  
def push(head_ref, new_data):  

    # allocate node  
    new_node = Node(new_data)  

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = head_ref      

    # move the head to point to the new node  
    head_ref = new_node 
    return head_ref 

# Function to print nodes in a given linked list  
def printList(node):  
    while (node != None):  
        print(node.data, end = " ")  
        node = node.next

# Driver code 
if __name__=='__main__':  

    # Start with the empty list  
    head = None

    # Let us create a sorted linked list 
    # to test the functions  
    # Created linked list will be 11.11.11.13.13.20  
    head = push(head, 20)  
    head = push(head, 13)  
    head = push(head, 13)  
    head = push(head, 11)  
    head = push(head, 11)  
    head = push(head, 11)                                  

    print("Linked list before duplicate removal ", 
                                         end = "")  
    printList(head)  

    # Remove duplicates from linked list  
    removeDuplicates(head)  

    print("\nLinked list after duplicate removal ", 
                                          end = "")  
    printList(head)          

# This code is contributed by Srathore 

```

## C#

```cs

// C# Program to remove duplicates 
// from a sorted linked list  
using System; 

class GFG 
{ 
/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

// The function removes duplicates 
// from a sorted list  
static Node removeDuplicates(Node head)  
{  
    /* Pointer to store the pointer 
    of a node to be deleted*/
    Node to_free;  

    /* do nothing if the list is empty */
    if (head == null)  
        return null;  

    /* Traverse the list till last node */
    if (head.next != null)  
    {  

        /* Compare head node with next node */
        if (head.data == head.next.data)  
        {  
            /* The sequence of steps is important. 
            to_free pointer stores the next of head 
            pointer which is to be deleted.*/
            to_free = head.next;  
            head.next = head.next.next; 
            removeDuplicates(head); 
        }  

        /* This is tricky: only advance if no deletion */
        else
        {  
            removeDuplicates(head.next); 
        }  
    }  
    return head; 
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging 
of the linked list */
static Node push(Node head_ref, 
                 int new_data)  
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

/* Function to print nodes in  
a given linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(" " + node.data);  
        node = node.next;  
    }  
}  

// Driver code 
public static void Main(String []args) 
{  
    /* Start with the empty list */
    Node head = null;  

    /* Let us create a sorted linked list 
    to test the functions  
    Created linked list will be 11.11.11.13.13.20 */
    head = push(head, 20);  
    head = push(head, 13);  
    head = push(head, 13);  
    head = push(head, 11);  
    head = push(head, 11);  
    head = push(head, 11);                                      

    Console.Write("Linked list before" +  
                  " duplicate removal ");  
    printList(head);  

    /* Remove duplicates from linked list */
    head = removeDuplicates(head);  

    Console.Write("\nLinked list after" +  
                  " duplicate removal ");      
    printList(head);              
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20

```

**另一种方法**：创建一个指向每个元素的第一个出现的指针和另一个将迭代到每个元素的`temp`指针，并且当前一个指针的值不等于`temp`指针时，我们将前一个指针的指针设置为另一个节点的第一个匹配项。

下面是上述方法的实现：

## Java

```java

// Java program to remove duplicates 
// from a sorted linked list 
class LinkedList 
{ 
    // head of list 
    Node head; 

    // Linked list Node 
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) { 
          data = d;  
          next = null;  
        } 
    } 

    // Function to remove duplicates 
    // from the given linked list 
    void removeDuplicates() 
    { 
        // Two references to head 
        // temp will iterate to the 
        // whole Linked List 
        // prev will point towards  
        // the first occurence of every element 
        Node temp = head,prev=head; 

        // Traverse list till the last node 
        while (temp != null) { 

           // Compare values of both pointers 
           if(temp.data!=prev.data) 
           { 
             /* if the value of prev is  
             not equal to the value of  
             temp that means there are no 
             more occruences of the prev data. 
             So we can set the next of  
             prev to the temp node.*/
             prev.next=temp; 
             prev=temp; 
           } 
            /*Set the temp to the next node*/
            temp=temp.next; 
        } 
      /*This is the edge case if there 
      are more than one occurrences  
      of the last element*/
      if(prev!=temp){ 
            prev.next=null; 
        } 
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
        llist.push(20); 
        llist.push(13); 
        llist.push(13); 
        llist.push(11); 
        llist.push(11); 
        llist.push(11); 

        System.out.print("List before "); 
        System.out.println("removal of duplicates"); 
        llist.printList(); 

        llist.removeDuplicates(); 

        System.out.println("List after removal of elements"); 
        llist.printList(); 
    } 
}  
/* This code is contributed by Arshita */    

```

**输出**：

```
List before removal of duplicates
11 11 11 13 13 20 
List after removal of elements
11 13 20 

```

**相关文章**：

[从排序的链表中删除所有重复项](https://www.geeksforgeeks.org/remove-occurrences-duplicates-sorted-linked-list/)

**参考**：

[cslibrary.stanford.edu /105/LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)

