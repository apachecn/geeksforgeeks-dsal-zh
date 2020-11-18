# 删除链表

的M个节点后的N个节点

给定一个链表和两个整数M和N。遍历链表，以便保留M个节点，然后删除下N个节点，继续相同操作，直到链表结束。

难度等级：菜鸟

例子：

```
Input:
M = 2, N = 2
Linked List: 1->2->3->4->5->6->7->8
Output:
Linked List: 1->2->5->6

Input:
M = 3, N = 2
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->2->3->6->7->8

Input:
M = 1, N = 1
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->3->5->7->9
```

问题的主要部分是维护节点之间的正确链接，确保处理所有极端情况。 以下是函数skipMdeleteN（）的C实现，该函数跳过M个节点并删除N个节点，直到列表结尾。 假定M不能为0。

## C++

```cpp

// C++ program to delete N nodes 
// after M nodes of a linked list  
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node  
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Function to insert a node at the beginning */
void push(Node ** head_ref, int new_data)  
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
void printList(Node *head)  
{  
    Node *temp = head;  
    while (temp != NULL)  
    {  
        cout<<temp->data<<" ";  
        temp = temp->next;  
    }  
    cout<<endl;  
}  

// Function to skip M nodes and then 
// delete N nodes of the linked list.  
void skipMdeleteN(Node *head, int M, int N)  
{  
    Node *curr = head, *t;  
    int count;  

    // The main loop that traverses 
    // through the whole list  
    while (curr)  
    {  
        // Skip M nodes  
        for (count = 1; count < M &&  
                curr!= NULL; count++)  
            curr = curr->next;  

        // If we reached end of list, then return  
        if (curr == NULL)  
            return;  

        // Start from next node and delete N nodes  
        t = curr->next;  
        for (count = 1; count<=N && t!= NULL; count++)  
        {  
            Node *temp = t;  
            t = t->next;  
            free(temp);  
        }  

        // Link the previous list with remaining nodes  
        curr->next = t;  

        // Set current pointer for next iteration  
        curr = t;  
    }  
}  

// Driver code  
int main()  
{  
    /* Create following linked list  
    1->2->3->4->5->6->7->8->9->10 */
    Node* head = NULL;  
    int M=2, N=3;  
    push(&head, 10);  
    push(&head, 9);  
    push(&head, 8);  
    push(&head, 7);  
    push(&head, 6);  
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);  

    cout << "M = " << M<< " N = " << N << "\nGiven Linked list is :\n";  
    printList(head);  

    skipMdeleteN(head, M, N);  

    cout<<"\nLinked list after deletion is :\n";  
    printList(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to delete N nodes after M nodes of a linked list 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Function to insert a node at the beginning */
void push(struct Node ** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)  = new_node; 
} 

/* Function to print linked list */
void printList(struct Node *head) 
{ 
    struct Node *temp = head; 
    while (temp != NULL) 
    { 
        printf("%d ", temp->data); 
        temp = temp->next; 
    } 
    printf("\n"); 
} 

// Function to skip M nodes and then delete N nodes of the linked list. 
void skipMdeleteN(struct Node  *head, int M, int N) 
{ 
    struct Node *curr = head, *t; 
    int count; 

    // The main loop that traverses through the whole list 
    while (curr) 
    { 
        // Skip M nodes 
        for (count = 1; count<M && curr!= NULL; count++) 
            curr = curr->next; 

        // If we reached end of list, then return 
        if (curr == NULL) 
            return; 

        // Start from next node and delete N nodes 
        t = curr->next; 
        for (count = 1; count<=N && t!= NULL; count++) 
        { 
            struct Node *temp = t; 
            t = t->next; 
            free(temp); 
        } 
        curr->next = t; // Link the previous list with remaining nodes 

        // Set current pointer for next iteration 
        curr = t; 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    /* Create following linked list 
      1->2->3->4->5->6->7->8->9->10 */
    struct Node* head = NULL; 
    int M=2, N=3; 
    push(&head, 10); 
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    printf("M = %d, N = %d \nGiven Linked list is :\n", M, N); 
    printList(head); 

    skipMdeleteN(head, M, N); 

    printf("\nLinked list after deletion is :\n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to delete N nodes  
// after M nodes of a linked list  
import java.util.*; 

class GFG 
{ 

// A linked list node  
static class Node  
{  
    int data;  
    Node next;  
};  

/* Function to insert a node at the beginning */
static Node push( Node head_ref, int new_data)  
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

/* Function to print linked list */
static void printList( Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        System.out.printf("%d ", temp.data);  
        temp = temp.next;  
    }  
    System.out.printf("\n");  
}  

// Function to skip M nodes and then 
// delete N nodes of the linked list.  
static void skipMdeleteN( Node head, int M, int N)  
{  
    Node curr = head, t;  
    int count;  

    // The main loop that traverses 
    // through the whole list  
    while (curr!=null)  
    {  
        // Skip M nodes  
        for (count = 1; count < M && curr != null; count++)  
            curr = curr.next;  

        // If we reached end of list, then return  
        if (curr == null)  
            return;  

        // Start from next node and delete N nodes  
        t = curr.next;  
        for (count = 1; count <= N && t != null; count++)  
        {  
            Node temp = t;  
            t = t.next;  
        }  

        // Link the previous list with remaining nodes  
        curr.next = t;  

        // Set current pointer for next iteration  
        curr = t;  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    /* Create following linked list  
    1.2.3.4.5.6.7.8.9.10 */
    Node head = null;  
    int M=2, N=3;  
    head=push(head, 10);  
    head=push(head, 9);  
    head=push(head, 8);  
    head=push(head, 7);  
    head=push(head, 6);  
    head=push(head, 5);  
    head=push(head, 4);  
    head=push(head, 3);  
    head=push(head, 2);  
    head=push(head, 1);  

    System.out.printf("M = %d, N = %d \nGiven" +  
                        "Linked list is :\n", M, N);  
    printList(head);  

    skipMdeleteN(head, M, N);  

    System.out.printf("\nLinked list after deletion is :\n");  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python program to delete M nodes after N nodes 

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

    # Utility function to prit the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print temp.data, 
            temp = temp.next

    def skipMdeleteN(self, M, N): 
        curr = self.head 

        # The main loop that traverses through the 
        # whole list 
        while(curr): 
            # Skip M nodes 
            for count in range(1, M): 
                if curr is None: 
                    return 
                curr = curr.next

            if curr is None : 
                return 

            # Start from next node and delete N nodes 
            t = curr.next 
            for count in range(1, N+1): 
                if t is None: 
                    break
                t = t.next

            # Link the previous list with reamining nodes 
            curr.next = t 
            # Set Current pointer for next iteration 
            curr = t  

# Driver program to test above function 

# Create following linked list 
# 1->2->3->4->5->6->7->8->9->10 
llist = LinkedList() 
M = 2 
N = 3
llist.push(10) 
llist.push(9) 
llist.push(8) 
llist.push(7) 
llist.push(6) 
llist.push(5) 
llist.push(4) 
llist.push(3) 
llist.push(2) 
llist.push(1) 

print "M = %d, N = %d\nGiven Linked List is:" %(M, N) 
llist.printList() 
print 

llist.skipMdeleteN(M, N) 

print "\nLinked list after deletion is"
llist.printList() 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# program to delete N nodes  
// after M nodes of a linked list  
using System; 

class GFG  
{  

// A linked list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to insert a node at the beginning */
static Node push( Node head_ref, int new_data)  
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

/* Function to print linked list */
static void printList( Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        Console.Write("{0} ", temp.data);  
        temp = temp.next;  
    }  
    Console.Write("\n");  
}  

// Function to skip M nodes and then  
// delete N nodes of the linked list.  
static void skipMdeleteN( Node head, int M, int N)  
{  
    Node curr = head, t;  
    int count;  

    // The main loop that traverses  
    // through the whole list  
    while (curr!=null)  
    {  
        // Skip M nodes  
        for (count = 1; count < M &&  
                curr != null; count++)  
            curr = curr.next;  

        // If we reached end of list, then return  
        if (curr == null)  
            return;  

        // Start from next node and delete N nodes  
        t = curr.next;  
        for (count = 1; count <= N && t != null; count++)  
        {  
            Node temp = t;  
            t = t.next;  
        }  

        // Link the previous list with remaining nodes  
        curr.next = t;  

        // Set current pointer for next iteration  
        curr = t;  
    }  
}  

// Driver code  
public static void Main(String []args)  
{  
    /* Create following linked list  
    1.2.3.4.5.6.7.8.9.10 */
    Node head = null;  
    int M=2, N=3;  
    head=push(head, 10);  
    head=push(head, 9);  
    head=push(head, 8);  
    head=push(head, 7);  
    head=push(head, 6);  
    head=push(head, 5);  
    head=push(head, 4);  
    head=push(head, 3);  
    head=push(head, 2);  
    head=push(head, 1);  

    Console.Write("M = {0}, N = {1} \nGiven" +  
                        "Linked list is :\n", M, N);  
    printList(head);  

    skipMdeleteN(head, M, N);  

    Console.Write("\nLinked list after deletion is :\n");  
    printList(head);  
}  
}  

// This code contributed by Rajput-Ji 

```

**Output:**

```
M = 2, N = 3
Given Linked list is :
1 2 3 4 5 6 7 8 9 10

Linked list after deletion is :
1 2 6 7
```

**时间复杂度：** O（n），其中n是链表中的节点数。

本文由 **[Chandra Prakash](https://www.facebook.com/chandra.prakash.52643)** 贡献。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

