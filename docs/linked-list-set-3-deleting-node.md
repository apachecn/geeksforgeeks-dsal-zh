# 链表 | 系列 3（删除节点）

> 原文：[https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)

在单链表的先前帖子中，我们已经讨论了[链表简介](http://quiz.geeksforgeeks.org/linked-list-set-1-introduction/)和[链表插入](http://quiz.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。

让我们制定问题陈述以了解删除过程。 给定一个“键”，请在链表中删除该键的第一个匹配项。

要从链表中删除节点，我们需要执行以下步骤。

1.  查找要删除的节点的上一个节点。

2.  更改上一个节点的下一个。

3.  删除节点的可用内存。

![linkedlist_deletion](img/fe3a6a2699fb99ae5429afd588e89619.png)

由于链表的每个节点都是使用 C 语言中的`malloc()`动态分配的，因此我们需要调用[`free()`](http://www.cplusplus.com/reference/cstdlib/free/)来释放为要删除的节点分配的内存。

## C++

```cpp

// A complete working C++ program to 
// demonstrate deletion in singly  
// linked list with class  
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
class Node{ 
public: 
    int data; 
    Node* next; 
}; 

// Given a reference (pointer to pointer) 
// to the head of a list and an int,  
// inserts a new node on the front of the 
// list.  
void push(Node** head_ref, int new_data) 
{ 
    Node* new_node = new Node(); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Given a reference (pointer to pointer) 
// to the head of a list and a key, deletes 
// the first occurrence of key in linked list  
void deleteNode(Node** head_ref, int key) 
{ 

    // Store head node 
    Node* temp = *head_ref; 
    Node* prev = NULL; 

    // If head node itself holds 
    // the key to be deleted 
    if (temp != NULL && temp->data == key) 
    { 
        *head_ref = temp->next; // Changed head 
        delete temp;            // free old head 
        return; 
    } 

    // Else Search for the key to be deleted,  
    // keep track of the previous node as we 
    // need to change 'prev->next' */ 
    while (temp != NULL && temp->data != key) 
    { 
        prev = temp; 
        temp = temp->next; 
    } 

    // If key was not present in linked list 
    if (temp == NULL) 
        return; 

    // Unlink the node from linked list 
    prev->next = temp->next; 

    // Free memory 
    delete temp; 
} 

// This function prints contents of 
// linked list starting from the  
// given node  
void printList(Node* node) 
{ 
    while (node != NULL)  
    { 
        cout << node->data << " "; 
        node = node->next; 
    } 
} 

// Driver code 
int main() 
{ 

    // Start with the empty list  
    Node* head = NULL; 

    // Add elements in linked list 
    push(&head, 7); 
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 2); 

    puts("Created Linked List: "); 
    printList(head); 

    deleteNode(&head, 1); 
    puts("\nLinked List after Deletion of 1: "); 

    printList(head); 

    return 0; 
} 

// This code is contributed by ac121102

```

## C

```c

// A complete working C program  
// to demonstrate deletion in  
// singly linked list 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Given a reference (pointer to pointer) to the head of a list 
   and an int, inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 
    new_node->data  = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref)    = new_node; 
} 

/* Given a reference (pointer to pointer) to the head of a list 
   and a key, deletes the first occurrence of key in linked list */
void deleteNode(struct Node **head_ref, int key) 
{ 
    // Store head node 
    struct Node* temp = *head_ref, *prev; 

    // If head node itself holds the key to be deleted 
    if (temp != NULL && temp->data == key) 
    { 
        *head_ref = temp->next;   // Changed head 
        free(temp);               // free old head 
        return; 
    } 

    // Search for the key to be deleted, keep track of the 
    // previous node as we need to change 'prev->next' 
    while (temp != NULL && temp->data != key) 
    { 
        prev = temp; 
        temp = temp->next; 
    } 

    // If key was not present in linked list 
    if (temp == NULL) return; 

    // Unlink the node from linked list 
    prev->next = temp->next; 

    free(temp);  // Free memory 
} 

// This function prints contents of linked list starting from  
// the given node 
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf(" %d ", node->data); 
        node = node->next; 
    } 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    push(&head, 7); 
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 2); 

    puts("Created Linked List: "); 
    printList(head); 
    deleteNode(&head, 1); 
    puts("\nLinked List after Deletion of 1: "); 
    printList(head); 
    return 0; 
}

```

## Java

```java

// A complete working Java program to demonstrate deletion in singly 
// linked list 
class LinkedList 
{ 
    Node head; // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    /* Given a key, deletes the first occurrence of key in linked list */
    void deleteNode(int key) 
    { 
        // Store head node 
        Node temp = head, prev = null; 

        // If head node itself holds the key to be deleted 
        if (temp != null && temp.data == key) 
        { 
            head = temp.next; // Changed head 
            return; 
        } 

        // Search for the key to be deleted, keep track of the 
        // previous node as we need to change temp.next 
        while (temp != null && temp.data != key) 
        { 
            prev = temp; 
            temp = temp.next; 
        }     

        // If key was not present in linked list 
        if (temp == null) return; 

        // Unlink the node from linked list 
        prev.next = temp.next; 
    } 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
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

    /* Drier program to test above functions. Ideally this function 
    should be in a separate user class. It is kept here to keep 
    code compact */
    public static void main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        llist.push(7); 
        llist.push(1); 
        llist.push(3); 
        llist.push(2); 

        System.out.println("\nCreated Linked list is:"); 
        llist.printList(); 

        llist.deleteNode(1); // Delete node with data 1 

        System.out.println("\nLinked List after Deletion of 1:"); 
        llist.printList(); 
    } 
} 

```

## Python3

```py

# A complete working Python3 program to 
# demonstrate deletion in singly  
# linked list with class  

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

    # Function to insert a new node at the beginning  
    def push(self, new_data):  
        new_node = Node(new_data)  
        new_node.next = self.head  
        self.head = new_node  

    # Given a reference to the head of a list and a key,  
    # delete the first occurence of key in linked list  
    def deleteNode(self, key):  

        # Store head node  
        temp = self.head  

        # If head node itself holds the key to be deleted  
        if (temp is not None):  
            if (temp.data == key):  
                self.head = temp.next
                temp = None
                return

        # Search for the key to be deleted, keep track of the  
        # previous node as we need to change 'prev.next'  
        while(temp is not None):  
            if temp.data == key:  
                break
            prev = temp  
            temp = temp.next

        # if key was not present in linked list  
        if(temp == None):  
            return

        # Unlink the node from linked list  
        prev.next = temp.next

        temp = None

    # Utility function to print the linked LinkedList  
    def printList(self):  
        temp = self.head  
        while(temp):  
            print (" %d" %(temp.data)),  
            temp = temp.next

# Driver program  
llist = LinkedList()  
llist.push(7)  
llist.push(1)  
llist.push(3)  
llist.push(2)  

print ("Created Linked List: ") 
llist.printList()  
llist.deleteNode(1)  
print ("\nLinked List after Deletion of 1:") 
llist.printList()  

# This code is contributed by Nikhil Kumar Singh (nickzuck_007)  

```

## C#

```cs

// A complete working C# program  
// to demonstrate deletion in  
// singly linked list 
using System; 
class GFG{ 

// Head of list 
Node head;  

// Linked list Node 
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

// Given a key, deletes the first 
// occurrence of key in linked list 
void deleteNode(int key) 
{ 
  // Store head node 
  Node temp = head, prev = null; 

  // If head node itself holds  
  // the key to be deleted 
  if (temp != null &&  
      temp.data == key) 
  { 
    // Changed head 
    head = temp.next;  
    return; 
  } 

  // Search for the key to be  
  // deleted, keep track of the 
  // previous node as we need  
  // to change temp.next 
  while (temp != null &&  
         temp.data != key) 
  { 
    prev = temp; 
    temp = temp.next; 
  }     

  // If key was not present  
  // in linked list 
  if (temp == null)  
    return; 

  // Unlink the node from linked list 
  prev.next = temp.next; 
} 

// Inserts a new Node at  
// front of the list. 
public void Push(int new_data) 
{ 
  Node new_node = new Node(new_data); 
  new_node.next = head; 
  head = new_node; 
} 

// This function prints contents  
// of linked list starting from 
// the given node  
public void printList() 
{ 
  Node tnode = head; 
  while (tnode != null) 
  { 
    Console.Write(tnode.data + " "); 
    tnode = tnode.next; 
  } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
  GFG llist = new GFG(); 

  llist.Push(7); 
  llist.Push(1); 
  llist.Push(3); 
  llist.Push(2); 

  Console.WriteLine("\nCreated Linked list is:"); 
  llist.printList(); 

  // Delete node with data 1 
  llist.deleteNode(1);  

  Console.WriteLine("\nLinked List after Deletion of 1:"); 
  llist.printList(); 
} 
} 

// This code is contributed by Rajput-Ji

```

**输出**：

```
Created Linked List: 
 2  3  1  7 
Linked List after Deletion of 1: 
 2  3  7 

```

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

