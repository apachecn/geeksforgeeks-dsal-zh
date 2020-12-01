# 从单链表中删除所有偶数节点

> 原文：[https://www.geeksforgeeks.org/program-to-delete-all-even-nodes-from-a-singly-linked-list/](https://www.geeksforgeeks.org/program-to-delete-all-even-nodes-from-a-singly-linked-list/)

给定一个[**单链表**](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，包含`N`个节点，任务是从列表中删除所有偶数节点。

![](img/e510510691cefe47cf733e6f2324c9db.png)

**示例**：

> **输入**：`LL = 1 -> 4 -> 3 -> 18 -> 19`
>
> **输出**：`1 -> 3 -> 19`
>
> **输入**：`LL = 5 -> 3 -> 6 -> 8 -> 4 -> 1 -> 2 -> 9`
>
> **输出**：`5 -> 3 -> 1 -> 9`

**方法**：

*   这个想法是一个遍历单链表的节点，并获得具有偶数数据的节点的指针。 请按照[本帖子](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)中使用的方法删除那些节点。

以下是上述想法的实现：

## C++

```cpp

// C++ implementation to delete all
// even nodes from the singly linked list

#include <bits/stdc++.h>
using namespace std;

// Node of the singly linked list
struct Node 
{
    int data;
    struct Node* next;
};

// Function to insert a node at
// the beginning of the singly
// Linked List
void push(struct Node** head_ref,
          int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(
            sizeof(
                struct Node));

    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

// Function to delete a node in a
// singly Linked List.
// head_ref --> Pointer to head
// node pointer.
// key --> Node to be deleted
void deleteNode(struct Node** head_ref,
                int key)
{
    // Store head node
    struct Node *temp = *head_ref,
                *prev;

    // If head node itself holds
    // the key to be deleted
    if (temp != NULL
        && temp->data == key) {
        // Changed head
        *head_ref = temp->next;
        // Free old head
        free(temp);
        return;
    }

    // Search for the key to be
    // deleted, keep track of the
    // previous node as we need
    // to change 'prev->next'
    while (temp != NULL
           && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    // If key was not present
    // in linked list
    if (temp == NULL)
        return;

    // Unlink the node from
    // linked list
    prev->next = temp->next;

    // Free memory
    free(temp);
}

// Function to delete all the
// even nodes from the
// singly linked list
void deleteEvenNodes(Node** head_ref)
{
    Node* ptr = *head_ref;
    // Node* next;

    while (ptr != NULL) {
        // next = ptr->next;
        // If true, delete node 'ptr'
        if (ptr->data % 2 == 0)
            deleteNode(head_ref,
                       ptr->data);
        ptr = ptr->next;
    }
}

// This function prints contents
// of linked list starting from
// the given node
void printList(struct Node* node)
{
    while (node != NULL) {
        printf(" %d -> ", node->data);
        node = node->next;
    }
}

// Driver code
int main()
{
    // Start with the empty list
    Node* head = NULL;
    push(&head, 19);
    push(&head, 18);
    push(&head, 3);
    push(&head, 4);
    push(&head, 1);

    printf("Initial List: ");
    printList(head);

    deleteEvenNodes(&head);

    printf("\nFinal List: ");
    printList(head);
}

```

## Java

```java

// Java implementation to delete all
// even nodes from the singly linked list
class LinkedList{

// head of list
Node head; 

// Linked list Node
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

// Function to insert a node at 
// the beginning of the singly 
// Linked List 
public void push(int new_data)
{
    Node new_node = new Node(new_data);
    new_node.next = head;
    head = new_node;
}

// Function to delete a node in a 
// singly Linked List. 
void deleteNode(int key)
{

    // Store head node
    Node temp = head, prev = null;

    // If head node itself holds the
    // key to be deleted
    if (temp != null && temp.data == key)
    {

        // Changed head
        head = temp.next; 
        return;
    }

    // Search for the key to be deleted,
    // keep track of the previous node
    // as we need to change temp.next
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

// Function to delete all the nodes
// from linked list containing
// even numbers.
void deleteEvenNodes()
{
    Node ptr = head;

    // loop to iterate the linked list
    while(ptr != null)
    {

        // If containing element is even
        if(ptr.data % 2 == 0)
        {

            // Delete the node
            deleteNode(ptr.data);
        }
        ptr = ptr.next;
    }
}

// This function prints contents of linked
// list starting from the given node
public void printList()
{
    Node ptr = head;
    while (ptr != null)
    {
        System.out.print(ptr.data + "-> ");
        ptr = ptr.next;
    }
}

// Driver code
public static void main(String[] args)
{
    LinkedList head = new LinkedList();

    head.push(19);
    head.push(18);
    head.push(3);
    head.push(4);
    head.push(1);

    System.out.print("\nInitial List: ");
    head.printList();

    head.deleteEvenNodes(); 

    System.out.print("\nFinal List: ");
    head.printList();
}
}

// This code is contributed by Amit Mangal

```

## Python3

```py

# Python3 implementation to delete all
# even nodes from the singly linked list
# Node class 
class Node: 

    # Function to initialize the node object 
    def __init__(self, data): 

        # Assign data
        self.data = data 

        # Initialize 
        # next as null
        self.next = None

# Linked List Class
class LinkedList:

    # Function to initialize the
    # LinkedList class.
    def __init__(self):

        # Initialize head as None
        self.head = None

    # This function insert a new node at 
    # the beginning of the linked list 
    def push(self, new_data): 

        # Create a new Node 
        new_node = Node(new_data) 

        # Make next of new Node as head 
        new_node.next = self.head 

        # Move the head to point to new Node 
        self.head = new_node

    # Method to print the linked list
    def printList(self):

        # Object to iterate
        # the list
        ptr = self.head

        # Loop to iterate list
        while(ptr != None):

            print(ptr.data, '-> ', end = '')

            # Moving the iterating object
            # to next node
            ptr = ptr.next

        print()

    # Method to delete a node in
    # a singly linked list.
    def deleteNode(self, key):
        temp = self.head

        # If head node itself holds
        # the key to be deleted.
        if(temp != None and temp.data == key):

            # Changing head of list.
            self.head = temp.next
            return

        # Search for the key to be
        # deleted, keep track of the
        # previous node as we need
        # to change prev.next
        while(temp != None and temp.data != key):
            prev = temp
            temp = temp.next

        # If is not present in list
        if(temp == None):
            return

        # Unlink the node from
        # linked list
        prev.next = temp.next

    # Method to delete all the
    # even nodes from singly
    # linked list.
    def deleteEvenNodes(self):
        ptr = self.head

        # Loop to iterate the
        # linked list.
        while(ptr != None):

            # If node contains even number.
            if(ptr.data % 2 == 0):

                # Deleting the node 
                self.deleteNode(ptr.data)

            ptr = ptr.next

# Driver code
if __name__=='__main__':

    head = LinkedList()

    # Pushing elements at start 
    # of linked list.
    head.push(19)
    head.push(18)
    head.push(3)
    head.push(4)
    head.push(1)

    # Print initial linked list
    print("Initial list: ", end = '')
    head.printList()

    # Calling the function to delete
    # nodes containing even numbers.
    head.deleteEvenNodes()

    # Print the final list
    print("Final list: ", end = '')
    head.printList()

# This code is contributed by Amit Mangal

```

## C#

```cs

// C# implementation to delete all 
// even nodes from the singly linked list 
using System;
class List{ 

  // head of list 
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

  // Function to insert a node at 
  // the beginning of the singly 
  // Linked List 
  public void push(int new_data) 
  { 
    Node new_node = new Node(new_data); 
    new_node.next = head; 
    head = new_node; 
  } 

  // Function to delete a node in a 
  // singly Linked List. 
  void deleteNode(int key) 
  {     
    // Store head node 
    Node temp = head, prev = null; 

    // If head node itself holds the 
    // key to be deleted 
    if (temp != null && 
        temp.data == key) 
    {         
      // Changed head 
      head = temp.next; 
      return; 
    } 

    // Search for the key to be deleted, 
    // keep track of the previous node 
    // as we need to change temp.next 
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

    // Unlink the node from 
    // linked list
    prev.next = temp.next; 
  } 

  // Function to delete 
  // all the nodes  from 
  // linked list containing 
  // even numbers. 
  void deleteEvenNodes() 
  { 
    Node ptr = head; 

    // loop to iterate the linked list 
    while(ptr != null) 
    { 
      // If containing element is even 
      if(ptr.data % 2 == 0) 
      {             
        // Delete the node 
        deleteNode(ptr.data); 
      } 
      ptr = ptr.next; 
    } 
  } 

  // This function prints contents of linked 
  // list starting from the given node 
  public void printList() 
  { 
    Node ptr = head; 
    while (ptr != null) 
    { 
      Console.Write(ptr.data + "-> "); 
      ptr = ptr.next; 
    } 
  } 

  // Driver code 
  public static void Main(String []args) 
  { 
    List head = new List(); 

    head.push(19); 
    head.push(18); 
    head.push(3); 
    head.push(4); 
    head.push(1); 

    Console.Write("\nInitial List: "); 
    head.printList(); 

    head.deleteEvenNodes(); 

    Console.Write("\nFinal List: "); 
    head.printList(); 
  } 
} 

// This code contributed by gauravrajput1

```

**输出**： 

```
Initial List:  1 ->  4 ->  3 ->  18 ->  19 -> 
Final List:  1 ->  3 ->  19 ->

```

**时间复杂度**：`O(n)`，其中`N`是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。