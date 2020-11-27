# 从单链表中选择一个随机节点

> 原文：[https://www.geeksforgeeks.org/select-a-random-node-from-a-singly-linked-list/](https://www.geeksforgeeks.org/select-a-random-node-from-a-singly-linked-list/)

给定一个单链列表，请从链列表中选择一个随机节点（如果列表中有`N`个节点，则选择一个节点的概率应为`1 / N`）。 您将获得一个随机数生成器。

以下是一个简单的解决方案

1.  通过遍历列表来计算节点数。

2.  再次遍历列表，并以`1 / N`的概率选择每个节点。 可以通过为第`i`个节点生成一个从 0 到`N-i`的随机数，然后仅在生成的数字等于 0（或从 0 到`N-i`的任何其他固定数）的情况下选择第`i`个节点来完成选择。

通过以上方案，我们得到了统一的概率。

```
i = 1, probability of selecting first node = 1/N
i = 2, probability of selecting second node =
                   [probability that first node is not selected] * 
                   [probability that second node is selected]
                  = ((N-1)/N)* 1/(N-1)
                  = 1/N  
```

同样，其他选择其他节点的概率为`1 / N`

上述解决方案需要两次遍历链表。

**如何选择只允许一个遍历的随机节点？**

这个想法是使用[储层采样](https://www.geeksforgeeks.org/reservoir-sampling/)。 以下是步骤。 这是[储层采样](https://www.geeksforgeeks.org/reservoir-sampling/)的简单版本，因为我们只需要选择一个键即可，而不是`k`个键。

```
(1) Initialize result as first node
   result = head->key 
(2) Initialize n = 2
(3) Now one by one consider all nodes from 2nd node onward.
    (3.a) Generate a random number from 0 to n-1\. 
         Let the generated random number is j.
    (3.b) If j is equal to 0 (we could choose other fixed number 
          between 0 to n-1), then replace result with current node.
    (3.c) n = n+1
    (3.d) current = current->next
```

下面是上述算法的实现。

## C++

```cpp

/* C++ program to randomly select a node from a singly 
linked list */
#include<stdio.h> 
#include<stdlib.h> 
#include <time.h> 
#include<iostream> 
using namespace std; 

/* Link list node */
class Node 
{ 
    public: 
    int key; 
    Node* next; 
    void printRandom(Node*); 
    void push(Node**, int); 

}; 

// A reservoir sampling based function to print a 
// random node from a linked list 
void Node::printRandom(Node *head) 
{ 
    // IF list is empty 
    if (head == NULL) 
    return; 

    // Use a different seed value so that we don't get 
    // same result each time we run this program 
    srand(time(NULL)); 

    // Initialize result as first node 
    int result = head->key; 

    // Iterate from the (k+1)th element to nth element 
    Node *current = head; 
    int n; 
    for (n = 2; current != NULL; n++) 
    { 
        // change result with probability 1/n 
        if (rand() % n == 0) 
        result = current->key; 

        // Move to next node 
        current = current->next; 
    } 

    cout<<"Randomly selected key is \n"<< result; 
} 

/* BELOW FUNCTIONS ARE JUST UTILITY TO TEST */

/* A utility function to create a new node */
Node* newNode(int new_key) 
{ 
    // allocate node  
    Node* new_node = (Node*) malloc(sizeof( Node)); 

    /// put in the key  
    new_node->key = new_key; 
    new_node->next = NULL; 

    return new_node; 
} 

/* A utility function to insert a node at the beginning 
of linked list */
void Node:: push(Node** head_ref, int new_key) 
{ 
    /* allocate node */
    Node* new_node = new Node; 

    /* put in the key */
    new_node->key = new_key; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Driver program to test above functions 
int main() 
{ 
    Node n1; 
    Node *head = NULL; 
    n1.push(&head, 5); 
    n1.push(&head, 20); 
    n1.push(&head, 4); 
    n1.push(&head, 3); 
    n1.push(&head, 30); 

    n1.printRandom(head); 

    return 0; 
} 

// This code is contributed by SoumikMondal 

```

## C

```c

/* C program to randomly select a node from a singly 
   linked list */
#include<stdio.h> 
#include<stdlib.h> 
#include <time.h> 

/* Link list node */
struct Node 
{ 
    int key; 
    struct Node* next; 
}; 

// A reservoir sampling based function to print a 
// random node from a linked list 
void printRandom(struct Node *head) 
{ 
    // IF list is empty 
    if (head == NULL) 
       return; 

    // Use a different seed value so that we don't get 
    // same result each time we run this program 
    srand(time(NULL)); 

    // Initialize result as first node 
    int result = head->key; 

    // Iterate from the (k+1)th element to nth element 
    struct Node *current = head; 
    int n; 
    for (n=2; current!=NULL; n++) 
    { 
        // change result with probability 1/n 
        if (rand() % n == 0) 
           result = current->key; 

        // Move to next node 
        current = current->next; 
    } 

    printf("Randomly selected key is %d\n", result); 
} 

/* BELOW FUNCTIONS ARE JUST UTILITY TO TEST  */

/* A utility function to create a new node */
struct Node *newNode(int new_key) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the key  */
    new_node->key  = new_key; 
    new_node->next =  NULL; 

    return new_node; 
} 

/* A utility function to insert a node at the beginning 
  of linked list */
void push(struct Node** head_ref, int new_key) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the key  */
    new_node->key  = new_key; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Node *head = NULL; 
    push(&head, 5); 
    push(&head, 20); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 30); 

    printRandom(head); 

    return 0; 
} 

```

## Java

```java

// Java program to select a random node from singly linked list 

import java.util.*; 

// Linked List Class 
class LinkedList { 

    static Node head;  // head of list 

    /* Node Class */
    static class Node { 

        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    // A reservoir sampling based function to print a 
    // random node from a linked list 
    void printrandom(Node node) { 

        // If list is empty 
        if (node == null) { 
            return; 
        } 

        // Use a different seed value so that we don't get 
        // same result each time we run this program 
        Math.abs(UUID.randomUUID().getMostSignificantBits()); 

        // Initialize result as first node 
        int result = node.data; 

        // Iterate from the (k+1)th element to nth element 
        Node current = node; 
        int n; 
        for (n = 2; current != null; n++) { 

            // change result with probability 1/n 
            if (Math.random() % n == 0) { 
                result = current.data; 
            } 

            // Move to next node 
            current = current.next; 
        } 

        System.out.println("Randomly selected key is " + result); 
    } 

    // Driver program to test above functions 
    public static void main(String[] args) { 

        LinkedList list = new LinkedList(); 
        list.head = new Node(5); 
        list.head.next = new Node(20); 
        list.head.next.next = new Node(4); 
        list.head.next.next.next = new Node(3); 
        list.head.next.next.next.next = new Node(30); 

        list.printrandom(head); 

    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python

```py

# Python program to randomly select a node from singly 
# linked list  

import random 

# Node class  
class Node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data= data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # A reservoir sampling based function to print a 
    # random node from a linkd list 
    def printRandom(self): 

        # If list is empty  
        if self.head is None: 
            return
        if self.head and not self.head.next: 
           print "Randomly selected key is %d" %(self.head.data) 

        # Use a different seed value so that we don't get  
        # same result each time we run this program 
        random.seed() 

        # Initialize result as first node 
        result = self.head.data 

        # Iterate from the (k+1)th element nth element 
        # because we iterate from (k+1)th element, or  
        # the first node will be picked more easily  
        current = self.head.next 
        n = 2 
        while(current is not None): 

            # change result with probability 1/n 
            if (random.randrange(n) == 0 ): 
                result = current.data  

            # Move to next node 
            current = current.next
            n += 1

        print "Randomly selected key is %d" %(result) 

    # Function to insert a new node at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Utility function to print the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print temp.data, 
            temp = temp.next

# Driver program to test above function 
llist = LinkedList() 
llist.push(5) 
llist.push(20) 
llist.push(4) 
llist.push(3) 
llist.push(30) 
llist.printRandom() 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# program to select a random node  
// from singly linked list 
using System; 

// Linked List Class 
public class LinkedList  
{ 
    Node head; // head of list 

    /* Node Class */
    public class Node 
    { 
        public int data; 
        public Node next; 

        // Constructor to create a new node 
        public Node(int d)  
        { 
            data = d; 
            next = null; 
        } 
    } 

    // A reservoir sampling based function to print a 
    // random node from a linked list 
    void printrandom(Node node)  
    { 

        // If list is empty 
        if (node == null)  
        { 
            return; 
        } 

        // Use a different seed value so that we don't get 
        // same result each time we run this program 
        //Math.abs(UUID.randomUUID().getMostSignificantBits()); 

        // Initialize result as first node 
        int result = node.data; 

        // Iterate from the (k+1)th element to nth element 
        Node current = node; 
        int n; 
        for (n = 2; current != null; n++)  
        { 

            // change result with probability 1/n 
            if (new Random().Next() % n == 0)  
            { 
                result = current.data; 
            } 

            // Move to next node 
            current = current.next; 
        } 

        Console.WriteLine("Randomly selected key is " +  
                                               result); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(5); 
        list.head.next = new Node(20); 
        list.head.next.next = new Node(4); 
        list.head.next.next.next = new Node(3); 
        list.head.next.next.next.next = new Node(30); 

        list.printrandom(list.head); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

请注意，以上程序基于随机函数的结果，可能会产生不同的输出。

**这是如何工作的？**

列表中总共有`N`个节点。 从最后一个节点更容易理解。

最后一个节点仅是结果`1 / N`的概率[对于最后一个或第`N`个节点，我们生成一个介于 0 到`N-1`之间的随机数，如果生成的数目为 0（或任何其他固定数），则将最后一个节点作为结果

倒数第二个节点为结果的概率也应为`1 / N`。

```
The probability that the second last node is result 
          = [Probability that the second last node replaces result] X 
            [Probability that the last node doesn't replace the result] 
          = [1 / (N-1)] * [(N-1)/N]
          = 1/N
```

类似地，我们可以显示最后 3 个节点和其他节点的概率。

本文由 **Rajeev** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

