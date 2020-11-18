# 在另一个位置将链接列表合并到另一个链接列表中

给定两个链接列表，将第二个列表的节点插入到第一个列表的第一个列表的备用位置。
例如，如果第一个列表是 5-> 7- > 17- > 13- > 11，第二个列表是 12- > 10- > 2- > 4- > 6，第一个列表应变为 5- > 12- > 7- > 10- > 17- > 2- > 13- > 4 -> 11- > 6 和第二个列表应该为空。 仅在有可用位置时才插入第二个列表的节点。 例如，如果第一个列表是 1- > 2- > 3，第二个列表是 4- > 5- > 6- > 7- > 8，则第一个列表应变为 1- > 4- > 2- > 5- > 3- > 6，第二个是 7- > 8。

不允许使用额外的空间（不允许创建额外的节点），即，插入必须就地完成。 预期的时间复杂度为 O（n），其中 n 是第一个列表中的节点数。

这个想法是在第一个循环中有可用位置时运行一个循环，并通过更改指针插入第二个列表的节点。 以下是此方法的实现。

## C++

```cpp

// C++ program to merge a linked list into another at  
// alternate positions  
#include <bits/stdc++.h> 
using namespace std; 

// A nexted list node  
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Function to insert a node at the beginning */
void push(Node ** head_ref, int new_data)  
{  
    Node* new_node = new Node(); 
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

/* Utility function to print a singly linked list */
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

// Main function that inserts nodes of linked list q into p at  
// alternate positions. Since head of first list never changes  
// and head of second list may change, we need single pointer  
// for first list and double pointer for second list.  
void merge(Node *p, Node **q)  
{  
    Node *p_curr = p, *q_curr = *q;  
    Node *p_next, *q_next;  

    // While therre are avialable positions in p  
    while (p_curr != NULL && q_curr != NULL)  
    {  
        // Save next pointers  
        p_next = p_curr->next;  
        q_next = q_curr->next;  

        // Make q_curr as next of p_curr  
        q_curr->next = p_next; // Change next pointer of q_curr  
        p_curr->next = q_curr; // Change next pointer of p_curr  

        // Update current pointers for next iteration  
        p_curr = p_next;  
        q_curr = q_next;  
    }  

    *q = q_curr; // Update head pointer of second list  
}  

// Driver code  
int main()  
{  
    Node *p = NULL, *q = NULL;  
    push(&p, 3);  
    push(&p, 2);  
    push(&p, 1);  
    cout<<"First Linked List:\n";  
    printList(p);  

    push(&q, 8);  
    push(&q, 7);  
    push(&q, 6);  
    push(&q, 5);  
    push(&q, 4);  
    cout<<"Second Linked List:\n";  
    printList(q);  

    merge(p, &q);  

    cout<<"Modified First Linked List:\n";  
    printList(p);  

    cout<<"Modified Second Linked List:\n";  
    printList(q);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to merge a linked list into another at 
// alternate positions 
#include <stdio.h> 
#include <stdlib.h> 

// A nexted list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Function to insert a node at the beginning */
void push(struct Node ** head_ref, int new_data) 
{ 
    struct Node* new_node =  
           (struct Node*) malloc(sizeof(struct Node)); 
    new_node->data  = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref)  = new_node; 
} 

/* Utility function to print a singly linked list */
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

// Main function that inserts nodes of linked list q into p at  
// alternate positions. Since head of first list never changes  
// and head of second list  may change, we need single pointer 
// for first list and double pointer for second list. 
void merge(struct Node *p, struct Node **q) 
{ 
     struct Node *p_curr = p, *q_curr = *q; 
     struct Node *p_next, *q_next; 

     // While therre are avialable positions in p 
     while (p_curr != NULL && q_curr != NULL) 
     { 
         // Save next pointers 
         p_next = p_curr->next; 
         q_next = q_curr->next; 

         // Make q_curr as next of p_curr 
         q_curr->next = p_next;  // Change next pointer of q_curr 
         p_curr->next = q_curr;  // Change next pointer of p_curr 

         // Update current pointers for next iteration 
         p_curr = p_next; 
         q_curr = q_next; 
    } 

    *q = q_curr; // Update head pointer of second list 
} 

// Driver program to test above functions 
int main() 
{ 
     struct Node *p = NULL, *q = NULL; 
     push(&p, 3); 
     push(&p, 2); 
     push(&p, 1); 
     printf("First Linked List:\n"); 
     printList(p); 

     push(&q, 8); 
     push(&q, 7); 
     push(&q, 6); 
     push(&q, 5); 
     push(&q, 4); 
     printf("Second Linked List:\n"); 
     printList(q); 

     merge(p, &q); 

     printf("Modified First Linked List:\n"); 
     printList(p); 

     printf("Modified Second Linked List:\n"); 
     printList(q); 

     getchar(); 
     return 0; 
} 

```

## Java

```java

// Java program to merge a linked list into another at 
// alternate positions 
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
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Main function that inserts nodes of linked list q into p at 
    // alternate positions. Since head of first list never changes 
    // and head of second list/ may change, we need single pointer 
    // for first list and double pointer for second list. 
    void merge(LinkedList q) 
    { 
        Node p_curr = head, q_curr = q.head; 
        Node p_next, q_next; 

        // While there are available positions in p; 
        while (p_curr != null && q_curr != null) { 

            // Save next pointers 
            p_next = p_curr.next; 
            q_next = q_curr.next; 

            // make q_curr as next of p_curr 
            q_curr.next = p_next; // change next pointer of q_curr 
            p_curr.next = q_curr; // change next pointer of p_curr 

            // update current pointers for next iteration 
            p_curr = p_next; 
            q_curr = q_next; 
        } 
        q.head = q_curr; 
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
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 
        llist1.push(3); 
        llist1.push(2); 
        llist1.push(1); 

        System.out.println("First Linked List:"); 
        llist1.printList(); 

        llist2.push(8); 
        llist2.push(7); 
        llist2.push(6); 
        llist2.push(5); 
        llist2.push(4); 

        System.out.println("Second Linked List:"); 

        llist1.merge(llist2); 

        System.out.println("Modified first linked list:"); 
        llist1.printList(); 

        System.out.println("Modified second linked list:"); 
        llist2.printList(); 
    } 
} /* This code is contributed by Rajat Mishra */

```

## 蟒蛇

```

# Python program to merge a linked list into another at 
# alternate positions 
class LinkedList(object): 
    def __init__(self): 
    # head of list 
        self.head = None

    # Linked list Node 
    class Node(object): 
        def __init__(self, d): 
            self.data = d 
            self.next = None

    # Inserts a new Node at front of the list. 
    def push(self, new_data): 

        # 1 & 2: Allocate the Node & 
        # Put in the data 
        new_node = self.Node(new_data) 

        # 3\. Make next of new Node as head 
        new_node.next = self.head 

        # 4\. Move the head to point to new Node 
        self.head = new_node 

    # Main function that inserts nodes of linked list q into p at 
    # alternate positions. Since head of first list never changes 
    # and head of second list/ may change, we need single pointer 
    # for first list and double pointer for second list. 
    def merge(self, q): 
        p_curr = self.head 
        q_curr = q.head 

        # While there are available positions in p; 
        while p_curr != None and q_curr != None: 

            # Save next pointers 
            p_next = p_curr.next
            q_next = q_curr.next

            # make q_curr as next of p_curr 
            q_curr.next = p_next # change next pointer of q_curr 
            p_curr.next = q_curr # change next pointer of p_curr 

            # update current pointers for next iteration 
            p_curr = p_next 
            q_curr = q_next 
        q.head = q_curr 

    # Function to print linked list 
    def printList(self): 
        temp = self.head 
        while temp != None: 
            print str(temp.data), 
            temp = temp.next
        print '' 

# Driver program to test above functions 
llist1 = LinkedList() 
llist2 = LinkedList() 
llist1.push(3) 
llist1.push(2) 
llist1.push(1) 

print "First Linked List:"
llist1.printList() 

llist2.push(8) 
llist2.push(7) 
llist2.push(6) 
llist2.push(5) 
llist2.push(4) 

print "Second Linked List:"

llist2.printList() 
llist1.merge(llist2) 

print "Modified first linked list:"
llist1.printList() 

print "Modified second linked list:"
llist2.printList() 

# This code is contributed by BHAVYA JAIN 

```

## C#

```cs

// C# program to merge a linked list into 
// another at alternate positions 
using System; 

public class LinkedList  
{  
    Node head; // head of list  

    /* Linked list Node*/
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

    /* Inserts a new Node at front of the list. */
    void push(int new_data)  
    {  
        /* 1 & 2: Allocate the Node &  
                Put in the data*/
        Node new_node = new Node(new_data);  

        /* 3\. Make next of new Node as head */
        new_node.next = head;  

        /* 4\. Move the head to point to new Node */
        head = new_node;  
    }  

    // Main function that inserts nodes  
    // of linked list q into p at alternate  
    // positions. Since head of first list 
    // never changes and head of second  
    // list/ may change, we need single  
    // pointer for first list and double  
    // pointer for second list.  
    void merge(LinkedList q)  
    {  
        Node p_curr = head, q_curr = q.head;  
        Node p_next, q_next;  

        // While there are available positions in p;  
        while (p_curr != null && q_curr != null) 
        {  

            // Save next pointers  
            p_next = p_curr.next;  
            q_next = q_curr.next;  

            // make q_curr as next of p_curr  
            q_curr.next = p_next; // change next pointer of q_curr  
            p_curr.next = q_curr; // change next pointer of p_curr  

            // update current pointers for next iteration  
            p_curr = p_next;  
            q_curr = q_next;  
        }  
        q.head = q_curr;  
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

    /* Driver code*/
    public static void Main()  
    {  
        LinkedList llist1 = new LinkedList();  
        LinkedList llist2 = new LinkedList();  
        llist1.push(3);  
        llist1.push(2);  
        llist1.push(1);  

        Console.WriteLine("First Linked List:");  
        llist1.printList();  

        llist2.push(8);  
        llist2.push(7);  
        llist2.push(6);  
        llist2.push(5);  
        llist2.push(4);  

        Console.WriteLine("Second Linked List:");  

        llist1.merge(llist2);  

        Console.WriteLine("Modified first linked list:");  
        llist1.printList();  

        Console.WriteLine("Modified second linked list:");  
        llist2.printList();  
    }  
}  

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
First Linked List:
1 2 3
Second Linked List:
4 5 6 7 8
Modified First Linked List:
1 4 2 5 3 6
Modified Second Linked List:
7 8 
```

本文由 **[Chandra Prakash](https://www.facebook.com/chandra.prakash.52643?fref=ts)** 贡献。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

