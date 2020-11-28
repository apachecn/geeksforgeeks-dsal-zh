# 从三个链表中查找一个三元组，总和等于给定数字

> 原文：[https://www.geeksforgeeks.org/find-a-triplet-from-three-linked-lists-with-sum-equal-to-a-given-number/](https://www.geeksforgeeks.org/find-a-triplet-from-three-linked-lists-with-sum-equal-to-a-given-number/)

给定三个链表（例如，`a`，`b`和`c`），从每个列表中找到一个节点，以使节点的值之和等于给定数目。

例如，如果三个链表是`12 -> 6 -> 29`、`23 -> 5 -> 8`和`90 -> 20 -> 59`，给定数字为 101，输出应为三元组`6 5 90`。

在以下解决方案中，为简化分析，假设所有三个链表的大小相同。 以下解决方案也适用于不同大小的链表。

解决此问题的一种简单方法是运行三个嵌套循环。 最外面的循环从列表`a`中选择一个元素，中间的循环从`b`中选择一个元素，最里面的循环从`c`中选择。 最里面的循环还检查`a`，`b`和`c`当前节点的值之和是否等于给定数。 该方法的时间复杂度为`O(n ^ 3)`。

可以使用排序将时间复杂度降低到`O(n * n)`。 以下是详细步骤。

1.  以升序对列表`b`进行排序，以降序对列表`c`进行排序。

2.  对`b`和`c`进行排序后，一个接一个地从列表`a`中选择一个元素，并同时遍历`b`和`c`来找到该对。 请参见以下代码中的`isSumSorted()`。 这个想法类似于[三和问题](http://en.wikipedia.org/wiki/3SUM)的二次算法。

以下代码仅实现步骤 2。 通过在此处中讨论的归并排序代码，可以轻松地为未排序列表修改解决方案。

## C++

```cpp

// C++ program to find a triplet  
// from three linked lists with  
// sum equal to a given number  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* A utility function to insert  
a node at the beginning of a  
linked list*/
void push (Node** head_ref, int new_data)  
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

/* A function to check if there are three elements in a, b  
and c whose sum is equal to givenNumber. The function  
assumes that the list b is sorted in ascending order  
and c is sorted in descending order. */
bool isSumSorted(Node *headA, Node *headB,  
                Node *headC, int givenNumber)  
{  
    Node *a = headA;  

    // Traverse through all nodes of a  
    while (a != NULL)  
    {  
        Node *b = headB;  
        Node *c = headC;  

        // For every node of list a, prick two nodes  
        // from lists b abd c  
        while (b != NULL && c != NULL)  
        {  
            // If this a triplet with given sum, print  
            // it and return true  
            int sum = a->data + b->data + c->data;  
            if (sum == givenNumber)  
            {  
            cout << "Triplet Found: " << a->data << " " <<  
                                b->data << " " << c->data;  
            return true;  
            }  

            // If sum of this triplet is smaller, look for  
            // greater values in b  
            else if (sum < givenNumber)  
                b = b->next;  
            else // If sum is greater, look for smaller values in c  
                c = c->next;  
        }  
        a = a->next; // Move ahead in list a  
    }  

    cout << "No such triplet";  
    return false;  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* headA = NULL;  
    Node* headB = NULL;  
    Node* headC = NULL;  

    /*create a linked list 'a' 10->15->5->20 */
    push (&headA, 20);  
    push (&headA, 4);  
    push (&headA, 15);  
    push (&headA, 10);  

    /*create a sorted linked list 'b' 2->4->9->10 */
    push (&headB, 10);  
    push (&headB, 9);  
    push (&headB, 4);  
    push (&headB, 2);  

    /*create another sorted  
    linked list 'c' 8->4->2->1 */
    push (&headC, 1);  
    push (&headC, 2);  
    push (&headC, 4);  
    push (&headC, 8);  

    int givenNumber = 25;  

    isSumSorted (headA, headB, headC, givenNumber);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to find a triplet from three linked lists with 
// sum equal to a given number 
#include<stdio.h> 
#include<stdlib.h> 
#include<stdbool.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* A utility function to insert a node at the beginning of a  
   linked list*/
void push (struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* A function to chech if there are three elements in a, b  
   and c whose sum is equal to givenNumber.  The function  
   assumes that the list b is sorted in ascending order  
   and c is sorted in descending order. */
bool isSumSorted(struct Node *headA, struct Node *headB,  
                 struct Node *headC, int givenNumber) 
{ 
    struct Node *a = headA; 

    // Traverse through all nodes of a 
    while (a != NULL) 
    { 
        struct Node *b = headB; 
        struct Node *c = headC; 

        // For every node of list a, prick two nodes 
        // from lists b abd c 
        while (b != NULL && c != NULL) 
        { 
            // If this a triplet with given sum, print 
            // it and return true 
            int sum = a->data + b->data + c->data; 
            if (sum == givenNumber) 
            { 
               printf ("Triplet Found: %d %d %d ", a->data, 
                                         b->data, c->data); 
               return true; 
            } 

            // If sum of this triplet is smaller, look for 
            // greater values in b 
            else if (sum < givenNumber) 
                b = b->next; 
            else // If sum is greater, look for smaller values in c 
                c = c->next; 
        } 
        a = a->next;  // Move ahead in list a 
    } 

    printf ("No such triplet"); 
    return false; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* headA = NULL; 
    struct Node* headB = NULL; 
    struct Node* headC = NULL; 

    /*create a linked list 'a' 10->15->5->20 */
    push (&headA, 20); 
    push (&headA, 4); 
    push (&headA, 15); 
    push (&headA, 10); 

    /*create a sorted linked list 'b' 2->4->9->10 */
    push (&headB, 10); 
    push (&headB, 9); 
    push (&headB, 4); 
    push (&headB, 2); 

    /*create another sorted linked list 'c' 8->4->2->1 */
    push (&headC, 1); 
    push (&headC, 2); 
    push (&headC, 4); 
    push (&headC, 8); 

    int givenNumber = 25; 

    isSumSorted (headA, headB, headC, givenNumber); 

    return 0; 
} 

```

## Java

```java

// Java program to find a triplet from three linked lists with 
// sum equal to a given number 
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

    /* A function to chech if there are three elements in a, b 
      and c whose sum is equal to givenNumber.  The function 
      assumes that the list b is sorted in ascending order and 
      c is sorted in descending order. */
   boolean isSumSorted(LinkedList la, LinkedList lb, LinkedList lc, 
                       int givenNumber) 
   { 
      Node a = la.head; 

      // Traverse all nodes of la 
      while (a != null) 
      { 
          Node b = lb.head; 
          Node c = lc.head; 

          // for every node in la pick 2 nodes from lb and lc 
          while (b != null && c!=null) 
          { 
              int sum = a.data + b.data + c.data; 
              if (sum == givenNumber) 
              { 
                 System.out.println("Triplet found " + a.data + 
                                     " " + b.data + " " + c.data); 
                 return true; 
              } 

              // If sum is smaller then look for greater value of b 
              else if (sum < givenNumber) 
                b = b.next; 

              else
                c = c.next; 
          } 
          a = a.next; 
      } 
      System.out.println("No Triplet found"); 
      return false; 
   } 

    /*  Given a reference (pointer to pointer) to the head 
       of a list and an int, push a new node on the front 
       of the list. */
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

     /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 
        LinkedList llist3 = new LinkedList(); 

        /* Create Linked List llist1 100->15->5->20 */
        llist1.push(20); 
        llist1.push(5); 
        llist1.push(15); 
        llist1.push(100); 

        /*create a sorted linked list 'b' 2->4->9->10 */
        llist2.push(10); 
        llist2.push(9); 
        llist2.push(4); 
        llist2.push(2); 

        /*create another sorted linked list 'c' 8->4->2->1 */
        llist3.push(1); 
        llist3.push(2); 
        llist3.push(4); 
        llist3.push(8); 

        int givenNumber = 25; 
        llist1.isSumSorted(llist1,llist2,llist3,givenNumber); 
    } 
} /* This code is contributed by Rajat Mishra */

```

## Python

```py

# Python program to find a triplet  
# from three linked lists with  
# sum equal to a given number  

# Link list node  
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None

# A utility function to insert  
# a node at the beginning of a  
# linked list 
def push ( head_ref, new_data) : 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = (head_ref)  

    # move the head to point to the new node  
    (head_ref) = new_node 

    return head_ref; 

# A function to check if there are three elements in a, b  
# and c whose sum is equal to givenNumber. The function  
# assumes that the list b is sorted in ascending order  
# and c is sorted in descending order.  
def isSumSorted(headA, headB,headC, givenNumber) : 

    a = headA  

    # Traverse through all nodes of a  
    while (a != None) : 

        b = headB  
        c = headC  

        # For every node of list a, prick two nodes  
        # from lists b abd c  
        while (b != None and c != None) : 

            # If this a triplet with given sum, print  
            # it and return true  
            sum = a.data + b.data + c.data  
            if (sum == givenNumber) : 

                print "Triplet Found: " , a.data , " " , b.data , " " , c.data,  
                return True

            # If sum of this triplet is smaller, look for  
            # greater values in b  
            elif (sum < givenNumber):  
                b = b.next
            else :# If sum is greater, look for smaller values in c  
                c = c.next

        a = a.next # Move ahead in list a  

    print("No such triplet")  
    return False

# Driver code 

# Start with the empty list  
headA = None
headB = None
headC = None

# create a linked list 'a' 10.15.5.20  
headA = push (headA, 20)  
headA = push (headA, 4)  
headA = push (headA, 15)  
headA = push (headA, 10)  

# create a sorted linked list 'b' 2.4.9.10  
headB = push (headB, 10)  
headB = push (headB, 9)  
headB = push (headB, 4)  
headB = push (headB, 2)  

# create another sorted  
# linked list 'c' 8.4.2.1  
headC = push (headC, 1)  
headC = push (headC, 2)  
headC = push (headC, 4)  
headC = push (headC, 8)  

givenNumber = 25

isSumSorted (headA, headB, headC, givenNumber)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find a triplet  
// from three linked lists with 
// sum equal to a given number 
using System; 

public class LinkedList 
{ 
    public Node head; // head of list 

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

    /* A function to chech if there  
    are three elements in a, b 
    and c whose sum is equal to  
    givenNumber. The function 
    assumes that the list b is  
    sorted in ascending order and 
    c is sorted in descending order. */
bool isSumSorted(LinkedList la, LinkedList lb,  
                LinkedList lc, int givenNumber) 
{ 
    Node a = la.head; 

    // Traverse all nodes of la 
    while (a != null) 
    { 
        Node b = lb.head; 
        Node c = lc.head; 

        // for every node in la pick  
        // 2 nodes from lb and lc 
        while (b != null && c!=null) 
        { 
            int sum = a.data + b.data + c.data; 
            if (sum == givenNumber) 
            { 
                Console.WriteLine("Triplet found " + a.data + 
                                    " " + b.data + " " + c.data); 
                return true; 
            } 

            // If sum is smaller then  
            // look for greater value of b 
            else if (sum < givenNumber) 
                b = b.next; 

            else
                c = c.next; 
        } 
        a = a.next; 
    } 
    Console.WriteLine("No Triplet found"); 
    return false; 
} 

    /* Given a reference (pointer to pointer) to the head 
    of a list and an int, push a new node on the front 
    of the list. */
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

    /* Driver code*/
    public static void Main(String []args) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 
        LinkedList llist3 = new LinkedList(); 

        /* Create Linked List llist1 100->15->5->20 */
        llist1.push(20); 
        llist1.push(5); 
        llist1.push(15); 
        llist1.push(100); 

        /*create a sorted linked list 'b' 2->4->9->10 */
        llist2.push(10); 
        llist2.push(9); 
        llist2.push(4); 
        llist2.push(2); 

        /*create another sorted linked list 'c' 8->4->2->1 */
        llist3.push(1); 
        llist3.push(2); 
        llist3.push(4); 
        llist3.push(8); 

        int givenNumber = 25; 
        llist1.isSumSorted(llist1,llist2,llist3,givenNumber); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Triplet Found: 15 2 8
```

**时间复杂度**：链表`b`和`c`可以使用归并排序以`O(nLogn)`时间排序（请参阅[这里](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)）。 步骤 2 花费`O(n * n)`时间。 因此，总体时间复杂度为`O(nlogn) + O(nlogn) + O(n * n) = O(n * n)`。

在这种方法中，链表`b`和`c`首先被排序，因此它们的原始顺序将丢失。 如果我们要保留`b`和`c`的原始顺序，则可以创建`b`和`c`的副本。

本文由 **Abhinav Priyadarshi** 编写，并由 GeeksforGeeks 小组审阅。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

