# 给定单链表的交替拆分 | 系列 1

> 原文：[https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/](https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/)

编写一个函数`AlternatingSplit()`，该函数接受一个列表并将其节点划分为两个较小的列表`a`和`b`。 子列表应由原始列表中的交替元素组成。 因此，如果原始列表为`0 -> 1 -> 0 -> 1 -> 0 -> 1`，则一个子列表应为`0 -> 0 -> 0`，另一个子列表应为`1 -> 1 -> 1`。

**方法 1（简单）**

最简单的方法是遍历源列表，将节点拉离源，然后将其交替放置在`a`和`b`的开头（或开头）。 唯一奇怪的部分是节点的顺序与它们在源列表中出现的顺序相反。 方法 2 通过跟踪子列表中的最后一个节点在最后插入该节点。

## C++

```cpp

/* C++ Program to alternatively split 
a linked list into two halves */
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* pull off the front node of 
the source and put it in dest */
void MoveNode(Node** destRef, Node** sourceRef) ;  

/* Given the source list, split its 
nodes into two shorter lists. If we number 
the elements 0, 1, 2, ... then all the even 
elements should go in the first list, and  
all the odd elements in the second. The  
elements in the new lists may be in any order. */
void AlternatingSplit(Node* source, Node** aRef,  
                            Node** bRef)  
{  
    /* split the nodes of source  
    to these 'a' and 'b' lists */
    Node* a = NULL;  
    Node* b = NULL;  

    Node* current = source;  
    while (current != NULL)  
    {  
        MoveNode(&a, ¤t); /* Move a node to list 'a' */
        if (current != NULL)  
        {  
            MoveNode(&b, ¤t); /* Move a node to list 'b' */
        }  
    }  
    *aRef = a;  
    *bRef = b;  
}  

/* Take the node from the front of 
the source, and move it to the front 
of the dest. It is an error to call 
this with the source list empty.  

Before calling MoveNode():  
source == {1, 2, 3}  
dest == {1, 2, 3}  

Affter calling MoveNode():  
source == {2, 3}      
dest == {1, 1, 2, 3}      
*/
void MoveNode(Node** destRef, Node** sourceRef)  
{  
    /* the front source node */
    Node* newNode = *sourceRef;  
    assert(newNode != NULL);  

    /* Advance the source pointer */
    *sourceRef = newNode->next;  

    /* Link the old dest off the new node */
    newNode->next = *destRef;  

    /* Move dest to point to the new node */
    *destRef = newNode;  
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at  
the beginging of the linked list */
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
    while(node!=NULL)  
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
    Node* a = NULL;  
    Node* b = NULL;  

    /* Let us create a sorted linked list to test the functions  
    Created linked list will be 0->1->2->3->4->5 */
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);                                  
    push(&head, 0);  

    cout<<"Original linked List: ";  
    printList(head);  

    /* Remove duplicates from linked list */
    AlternatingSplit(head, &a, &b);  

    cout<<"\nResultant Linked List 'a' : ";  
    printList(a);          

    cout<<"\nResultant Linked List 'b' : ";  
    printList(b);          

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

/*Program to alternatively split a linked list into two halves */
#include<stdio.h> 
#include<stdlib.h> 
#include<assert.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* pull off the front node of the source and put it in dest */
void MoveNode(struct Node** destRef, struct Node** sourceRef) ; 

/* Given the source list, split its nodes into two shorter lists. 
  If we number the elements 0, 1, 2, ... then all the even elements 
  should go in the first list, and all the odd elements in the second. 
  The elements in the new lists may be in any order. */
void AlternatingSplit(struct Node* source, struct Node** aRef,  
                            struct Node** bRef)  
{ 
  /* split the nodes of source to these 'a' and 'b' lists */
  struct Node* a = NULL;  
  struct Node* b = NULL; 

  struct Node* current = source; 
  while (current != NULL)  
  { 
    MoveNode(&a, ¤t); /* Move a node to list 'a' */
    if (current != NULL)  
    { 
       MoveNode(&b, ¤t); /* Move a node to list 'b' */
    } 
  } 
  *aRef = a; 
  *bRef = b; 
} 

/* Take the node from the front of the source, and move it to the front of the dest. 
   It is an error to call this with the source list empty.  

   Before calling MoveNode(): 
   source == {1, 2, 3}    
   dest == {1, 2, 3} 

   Affter calling MoveNode(): 
   source == {2, 3}       
   dest == {1, 1, 2, 3}       
*/
void MoveNode(struct Node** destRef, struct Node** sourceRef)  
{ 
  /* the front source node  */
  struct Node* newNode = *sourceRef;  
  assert(newNode != NULL); 

  /* Advance the source pointer */
  *sourceRef = newNode->next; 

  /* Link the old dest off the new node */
  newNode->next = *destRef;  

  /* Move dest to point to the new node */
  *destRef = newNode;  
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginging of the linked list */
void push(struct node** head_ref, int new_data) 
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
  while(node!=NULL) 
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
  struct Node* a = NULL; 
  struct Node* b = NULL;   

  /* Let us create a sorted linked list to test the functions 
   Created linked list will be 0->1->2->3->4->5 */
  push(&head, 5); 
  push(&head, 4); 
  push(&head, 3); 
  push(&head, 2); 
  push(&head, 1);                                     
  push(&head, 0);   

  printf("\n Original linked List:  "); 
  printList(head);  

  /* Remove duplicates from linked list */
  AlternatingSplit(head, &a, &b);  

  printf("\n Resultant Linked List 'a' "); 
  printList(a);             

  printf("\n Resultant Linked List 'b' "); 
  printList(b);             

  getchar(); 
  return 0; 
} 

```

## Python

```py

# Python program to alternatively split  
# a linked list into two halves  

# Node class 
class Node: 

    def __init__(self, data, next = None): 

        self.data = data 
        self.next = None

class LinkedList: 

    def __init__(self): 

        self.head = None

    # Given the source list, split its  
    # nodes into two shorter lists. If we number  
    # the elements 0, 1, 2, ... then all the even  
    # elements should go in the first list, and  
    # all the odd elements in the second. The  
    # elements in the new lists may be in any order. 
    def AlternatingSplit(self, a, b): 

        first = self.head 
        second = first.next

        while (first is not None and 
              second is not None and 
          first.next is not None): 

              # Move a node to list 'a' 
              self.MoveNode(a, first)  

              # Move a node to list 'b' 
              self.MoveNode(b, second)  

              first = first.next.next

              if first is None: 
                break

              second = first.next

    # Pull off the front node of the  
    # source and put it in dest 
    def MoveNode(self, dest, node): 

        # Make the new node 
        new_node = Node(node.data) 

        if dest.head is None: 
            dest.head = new_node 
        else: 

            # Link the old dest off the new node  
            new_node.next = dest.head 

            # Move dest to point to the new node  
            dest.head = new_node 

    # UTILITY FUNCTIONS  
    # Function to insert a node at   
    # the beginging of the linked list  
    def push(self, data): 

        # 1 & 2 allocate the Node &  
        # put the data 

        new_node = Node(data) 

        # Make the next of new Node as head 
        new_node.next = self.head 

        # Move the head to point to new Node 
        self.head = new_node 

    # Function to print nodes  
    # in a given linked list  
    def printList(self): 

        temp = self.head 
        while temp: 
            print temp.data, 
            temp = temp.next

        print("") 

# Driver Code 
if __name__ == "__main__": 

    # Start with empty list 
    llist = LinkedList() 
    a = LinkedList() 
    b = LinkedList() 

    # Created linked list will be 
    # 0->1->2->3->4->5  
    llist.push(5) 
    llist.push(4) 
    llist.push(3) 
    llist.push(2) 
    llist.push(1) 
    llist.push(0) 

    llist.AlternatingSplit(a, b) 

    print "Original Linked List: ", 
    llist.printList() 

    print "Resultant Linked List 'a' : ", 
    a.printList() 

    print "Resultant Linked List 'b' : ", 
    b.printList() 

# This code is contributed by kevalshah5 

```

**Output:**

```
Original linked List: 0 1 2 3 4 5 
Resultant Linked List 'a' : 4 2 0 
Resultant Linked List 'b' : 5 3 1 
```

**时间复杂度**：`O(n)`，其中`n`是给定链接列表中的节点数。

**方法 2（使用虚拟节点）**

这是一种替代方法，以与源列表相同的顺序构建子列表。 该代码在构建`a`和`b`列表时使用了临时的虚拟标头节点。 每个子列表都有一个“尾”指针，该指针指向其当前的最后一个节点-这样，新节点就可以轻松地附加到每个列表的末尾。 虚拟节点为尾部指针提供一些初始指向的指针。 在这种情况下，虚拟节点是有效的，因为它们是临时的并在堆栈中分配。 或者，可以使用局部“引用指针”（始终指向列表中的最后一个指针而不是最后一个节点）来避免虚拟节点。

## C++

```cpp

void AlternatingSplit(Node* source,  
                      Node** aRef, Node** bRef)  
{  
    Node aDummy;  

    /* points to the last node in 'a' */
    Node* aTail = &aDummy;  
    Node bDummy;  

    /* points to the last node in 'b' */
    Node* bTail = &bDummy;  
    Node* current = source;  
    aDummy.next = NULL;  
    bDummy.next = NULL;  
    while (current != NULL)  
    {  
        MoveNode(&(aTail->next), ¤t); /* add at 'a' tail */
        aTail = aTail->next; /* advance the 'a' tail */
        if (current != NULL)  
        {  
            MoveNode(&(bTail->next), ¤t);  
            bTail = bTail->next;  
        }  
    }  
    *aRef = aDummy.next;  
    *bRef = bDummy.next;  
}  

// This code is contributed  
// by rathbhupendra 

```

## C

```c

void AlternatingSplit(struct Node* source, struct Node** aRef,  
                            struct Node** bRef)  
{ 
  struct Node aDummy; 
  struct Node* aTail = &aDummy; /* points to the last node in 'a' */
  struct Node bDummy; 
  struct Node* bTail = &bDummy; /* points to the last node in 'b' */
  struct Node* current = source; 
  aDummy.next = NULL; 
  bDummy.next = NULL; 
  while (current != NULL)  
  { 
    MoveNode(&(aTail->next), ¤t); /* add at 'a' tail */
    aTail = aTail->next; /* advance the 'a' tail */
    if (current != NULL)  
    { 
      MoveNode(&(bTail->next), ¤t); 
      bTail = bTail->next; 
    } 
  } 
  *aRef = aDummy.next; 
  *bRef = bDummy.next; 
} 

```

时间复杂度：`O(n)`，其中`n`是给定链表中节点的数量。

来源： [http://cslibrary.stanford.edu/105/LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)

如果您发现上述代码/算法有误，请写注释，或者找到解决同一问题的更好方法。

