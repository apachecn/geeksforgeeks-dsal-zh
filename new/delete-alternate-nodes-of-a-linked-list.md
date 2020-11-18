# 删除链接列表

的备用节点

给定一个单链列表，从第二个节点开始删除它的所有备用节点。 例如，如果给定的链表为1-> 2-> 3-> 4-> 5，则您的函数应将其转换为1-> 3-> 5，并且给定的链表为1-> 2-> 3-> 4，然后将其转换为1-> 3。

**方法1（迭代）**
跟踪要删除的节点的先前节点。 首先更改上一个节点的下一个链接，然后释放为该节点分配的内存。

## C ++

```

// C++ program to remove alternate  
// nodes of a linked list  
#include <bits/stdc++.h> 
using namespace std; 

/* A linked list node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* deletes alternate nodes  
of a list starting with head */
void deleteAlt(Node *head)  
{  
    if (head == NULL)  
        return;  

    /* Initialize prev and node to be deleted */
    Node *prev = head;  
    Node *node = head->next;  

    while (prev != NULL && node != NULL)  
    {  
        /* Change next link of previous node */
        prev->next = node->next;  

        /* Free memory */
        free(node);  

        /* Update prev and node */
        prev = prev->next;  
        if (prev != NULL)  
            node = prev->next;  
    }  
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

/* Function to print nodes in a given linked list */
void printList(Node *node)  
{  
    while (node != NULL)  
    {  
        cout<< node->data<<" ";  
        node = node->next;  
    }  
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

    cout<<"List before calling deleteAlt() \n";  
    printList(head);  

    deleteAlt(head);  

    cout<<"\nList after calling deleteAlt() \n";  
    printList(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```

// C program to remove alternate nodes of a linked list 
#include<stdio.h> 
#include<stdlib.h> 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* deletes alternate nodes of a list starting with head */
void deleteAlt(struct Node *head) 
{ 
    if (head == NULL) 
        return; 

    /* Initialize prev and node to be deleted */
    struct Node *prev = head; 
    struct Node *node = head->next; 

    while (prev != NULL && node != NULL) 
    { 
        /* Change next link of previous node */
        prev->next = node->next; 

        /* Free memory */
        free(node); 

        /* Update prev and node */
        prev = prev->next; 
        if (prev != NULL) 
            node = prev->next; 
    } 
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

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
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

    printf("\nList before calling deleteAlt() \n"); 
    printList(head); 

    deleteAlt(head); 

    printf("\nList after calling deleteAlt() \n"); 
    printList(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to delete alternate nodes of a linked list 
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

    void deleteAlt() 
    { 
       if (head == null)  
          return; 

       Node prev = head; 
       Node now = head.next; 

       while (prev != null && now != null)  
       {            
           /* Change next link of previus node */
           prev.next = now.next; 

           /* Free node */
           now = null; 

           /*Update prev and now */
           prev = prev.next; 
           if (prev != null)  
              now = prev.next; 
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
        while(temp != null) 
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

        /* Constructed Linked List is 1->2->3->4->5->null */
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Linked List before calling deleteAlt() "); 
        llist.printList(); 

        llist.deleteAlt(); 

        System.out.println("Linked List after calling deleteAlt() "); 
        llist.printList(); 
    } 
}  
/* This code is contributed by Rajat Mishra */

```

## Python3

```

# Python3 program to remove alternate  
# nodes of a linked list  
import math  

# A linked list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# deletes alternate nodes  
# of a list starting with head  
def deleteAlt(head):  
    if (head == None): 
        return

    # Initialize prev and node to be deleted  
    prev = head  
    now = head.next

    while (prev != None and now != None):  

        # Change next link of previous node  
        prev.next = now.next

        # Free memory  
        now = None

        # Update prev and node  
        prev = prev.next
        if (prev != None):  
            now = prev.next

# UTILITY FUNCTIONS TO TEST fun1() and fun2()  
# Given a reference (poer to poer) to the head  
# of a list and an , push a new node on the front  
# of the list.  
def push(head_ref, new_data):  

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = head_ref  

    # move the head to po to the new node  
    head_ref = new_node  
    return head_ref 

# Function to print nodes in a given linked list  
def prList(node):  
    while (node != None):  
        print(node.data, end = " ")  
        node = node.next

# Driver code  
if __name__=='__main__':  

    # Start with the empty list  
    head = None

    # Using head=push() to construct below list  
    # 1.2.3.4.5  
    head = push(head, 5)  
    head = push(head, 4)  
    head = push(head, 3)  
    head = push(head, 2)  
    head = push(head, 1)  

    print("List before calling deleteAlt() ") 
    prList(head)  

    deleteAlt(head)  

    print("\nList after calling deleteAlt() ")  
    prList(head)  

# This code is contributed by Srathore 

```

## C＃

```

// C# program to delete alternate 
// nodes of a linked list 
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
            data = d; next = null;  

        } 
    } 

    void deleteAlt() 
    { 
        if (head == null)  
            return; 

        Node prev = head; 
        Node now = head.next; 

        while (prev != null && now != null)  
        {          
            /* Change next link of previus node */
            prev.next = now.next; 

            /* Free node */
            now = null; 

            /*Update prev and now */
            prev = prev.next; 
            if (prev != null)  
                now = prev.next; 
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
        while(temp != null) 
        { 
        Console.Write(temp.data+" "); 
        temp = temp.next; 
        }  
        Console.WriteLine(); 
    } 

    /* Driver code*/
    public static void Main(String []args) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Constructed Linked List is 
        1->2->3->4->5->null */
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        Console.WriteLine("Linked List before" +  
                            "calling deleteAlt() "); 
        llist.printList(); 

        llist.deleteAlt(); 

        Console.WriteLine("Linked List after" +  
                            "calling deleteAlt() "); 
        llist.printList(); 
    } 
} 

// This code has been contributed  
// by 29AjayKumar 

```

**Output:**

```
List before calling deleteAlt() 
1 2 3 4 5 
List after calling deleteAlt() 
1 3 5 
```

**时间复杂度：** O（n），其中n是给定链接列表中节点的数量。

**方法2（递归）**
递归代码使用与方法1相同的方法。递归代码很简单且简短，但是会导致O（n）递归函数调用大小为n的链表。

## C ++

```

/* deletes alternate nodes of a list starting with head */
void deleteAlt(Node *head)  
{  
    if (head == NULL)  
        return;  

    Node *node = head->next;  

    if (node == NULL)  
        return;  

    /* Change the next link of head */
    head->next = node->next;  

    /* free memory allocated for node */
    free(node);  

    /* Recursively call for the new next of head */
    deleteAlt(head->next);  
}  

// This code is contributed by rathbhupendra 

```

## C

```

/* deletes alternate nodes of a list starting with head */
void deleteAlt(struct Node *head) 
{ 
    if (head == NULL) 
        return; 

    struct Node *node = head->next; 

    if (node == NULL) 
        return; 

    /* Change the next link of head */
    head->next = node->next; 

    /* free memory allocated for node */
    free(node); 

    /* Recursively call for the new next of head */
    deleteAlt(head->next); 
} 

```

## 爪哇

```

/* deletes alternate nodes of a list 
starting with head */
static Node deleteAlt(Node head)  
{  
    if (head == null)  
        return;  

    Node node = head.next;  

    if (node == null)  
        return;  

    /* Change the next link of head */
    head.next = node.next;  

    /* Recursively call for the new next of head */
    head.next = deleteAlt(head.next);  
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```

# deletes alternate nodes of a list starting with head  
def deleteAlt(head):  
    if (head == None):  
        return

    node = head.next

    if (node == None):  
        return

    # Change the next link of head  
    head.next = node.next

    # free memory allocated for node  
    #free(node)  

    # Recursively call for the new next of head  
    deleteAlt(head.next)  

# This code is contributed by Srathore 

```

## C＃

```

/* deletes alternate nodes of a list 
starting with head */
static Node deleteAlt(Node head)  
{  
    if (head == null)  
        return;  

    Node node = head.next;  

    if (node == null)  
        return;  

    /* Change the next link of head */
    head.next = node.next;  

    /* Recursively call for the new next of head */
    head.next = deleteAlt(head.next);  
}  

// This code is contributed by Arnab Kundu 

```

**Time Complexity:** O(n)

如果您发现上述代码/算法有误，请写注释，或者找到解决同一问题的更好方法。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。