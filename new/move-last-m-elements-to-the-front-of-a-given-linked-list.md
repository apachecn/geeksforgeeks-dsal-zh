# 将最后m个元素移到给定链接列表

的前面

给定[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)的**头**和值 **m** ，任务是将最后m个元素移到最前面。

**示例：**

> **输入：** 4- > 5- > 6- > 1- > 2- > 3； m = 3
> **输出：** 1- > 2- > 3- > 4- > 5- > 6
> 
> **输入：** 0- > 1- > 2- > 3- > 4- > 5； m = 4
> **输出：** 2- > 3- > 4- > 5- > 0- > 1

**算法：**

1.  使用两个指针：一个用于存储最后一个节点的地址，另一个用于存储第一个节点的地址。
2.  遍历列表，直到最后m个节点中的第一个节点。
3.  保持两个指针p，q，即p作为最后m个节点的第一个节点，q保持在p的节点之前。
4.  将最后一个节点作为原始列表的头。
5.  将节点q的下一个设为NULL。
6.  将p设置为头部。

下面是上述方法的实现。

## C++

```cpp

// C++ Program to move last m elements 
// to front in a given linked list 
#include <iostream> 
using namespace std; 

// A linked list node 
struct Node  
{ 
    int data; 
    struct Node* next; 
} * first, *last; 

int length = 0; 

// Function to print nodes 
// in a given linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL)  
    { 
        cout << node->data <<" "; 
        node = node->next; 
    } 
} 

// Pointer head and p are being 
// used here because, the head 
// of the linked list is changed in this function. 
void moveToFront(struct Node* head, 
                struct Node* p, int m) 
{ 
    // If the linked list is empty, 
    // or it contains only one node, 
    // then nothing needs to be done, simply return 
    if (head == NULL) 
        return; 

    p = head; 
    head = head->next; 
    m++; 

    // if m value reaches length, 
    // the recursion will end 
    if (length == m) 
    { 

        // breaking the link 
        p->next = NULL; 

        // connecting last to first & 
        // will make another node as head 
        last->next = first; 

        // Making the first node of 
        // last m nodes as root 
        first = head; 
    } 
    else
        moveToFront(head, p, m); 
} 

// UTILITY FUNCTIONS 

// Function to add a node at 
// the beginning of Linked List 
void push(struct Node** head_ref, 
        int new_data) 
{ 
    // allocate node 
    struct Node* new_node = (struct Node*) 
        malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // move the head to point to the new node 
    (*head_ref) = new_node; 

    // making first & last nodes 
    if (length == 0) 
        last = *head_ref; 
    else
        first = *head_ref; 

    // increase the length 
    length++; 
} 

// Driver code 
int main() 
{ 
    struct Node* start = NULL; 

    // The constructed linked list is: 
    // 1->2->3->4->5 
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 
    push(&start, 0); 

    cout << "Initial Linked list\n"; 
    printList(start); 
    int m = 4; // no.of nodes to change 
    struct Node* temp; 
    moveToFront(start, temp, m); 

    cout << "\n Final Linked list\n"; 
    start = first; 
    printList(start); 

    return 0; 
} 

// This code is contributed by SHUBHAMSINGH10 

```

## C

```c

// C Program to move last m elements 
// to front in a given linked list 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
} * first, *last; 

int length = 0; 

// Function to print nodes 
// in a given linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// Pointer head and p are being 
// used here because, the head 
// of the linked list is changed in this function. 
void moveToFront(struct Node* head, 
                 struct Node* p, int m) 
{ 
    // If the linked list is empty, 
    // or it contains only one node, 
    // then nothing needs to be done, simply return 
    if (head == NULL) 
        return; 

    p = head; 
    head = head->next; 
    m++; 

    // if m value reaches length, 
    // the recursion will end 
    if (length == m) { 

        // breaking the link 
        p->next = NULL; 

        // connecting last to first & 
        // will make another node as head 
        last->next = first; 

        // Making the first node of 
        // last m nodes as root 
        first = head; 
    } 
    else
        moveToFront(head, p, m); 
} 

// UTILITY FUNCTIONS 

// Function to add a node at 
// the beginning of Linked List 
void push(struct Node** head_ref, 
          int new_data) 
{ 
    // allocate node 
    struct Node* new_node = (struct Node*) 
        malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // move the head to point to the new node 
    (*head_ref) = new_node; 

    // making first & last nodes 
    if (length == 0) 
        last = *head_ref; 
    else
        first = *head_ref; 

    // increase the length 
    length++; 
} 

// Driver code 
int main() 
{ 
    struct Node* start = NULL; 

    // The constructed linked list is: 
    // 1->2->3->4->5 
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 
    push(&start, 0); 

    printf("\n Initial Linked list\n"); 
    printList(start); 
    int m = 4; // no.of nodes to change 
    struct Node* temp; 
    moveToFront(start, temp, m); 

    printf("\n Final Linked list\n"); 
    start = first; 
    printList(start); 

    return 0; 
} 

```

## Java

```java

// Java Program to move last m elements 
// to front in a given linked list 
class GFG  
{ 
    // A linked list node 
    static class Node  
    { 
        int data; 
        Node next; 
    } 

    static Node first, last; 

    static int length = 0; 

    // Function to print nodes 
    // in a given linked list 
    static void printList(Node node) 
    { 
        while (node != null)  
        { 
            System.out.printf("%d ", node.data); 
            node = node.next; 
        } 
    } 

    // Pointer head and p are being 
    // used here because, the head 
    // of the linked list is changed in this function. 
    static void moveToFront(Node head, Node p, int m)  
    { 
        // If the linked list is empty, 
        // or it contains only one node, 
        // then nothing needs to be done, simply return 
        if (head == null) 
            return; 

        p = head; 
        head = head.next; 
        m++; 

        // if m value reaches length, 
        // the recursion will end 
        if (length == m)  
        { 

            // breaking the link 
            p.next = null; 

            // connecting last to first & 
            // will make another node as head 
            last.next = first; 

            // Making the first node of 
            // last m nodes as root 
            first = head; 
        } 
        else
            moveToFront(head, p, m); 
    } 

    // UTILITY FUNCTIONS 

    // Function to add a node at 
    // the beginning of Linked List 
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list off the new node 
        new_node.next = head_ref; 

        // move the head to point to the new node 
        head_ref = new_node; 

        // making first & last nodes 
        if (length == 0) 
            last = head_ref; 
        else
            first = head_ref; 

        // increase the length 
        length++; 
        return head_ref; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        Node start = null; 

        // The constructed linked list is: 
        // 1.2.3.4.5 
        start = push(start, 5); 
        start = push(start, 4); 
        start = push(start, 3); 
        start = push(start, 2); 
        start = push(start, 1); 
        start = push(start, 0); 

        System.out.printf("\n Initial Linked list\n"); 
        printList(start); 
        int m = 4; // no.of nodes to change 
        Node temp = new Node(); 
        moveToFront(start, temp, m); 

        System.out.printf("\n Final Linked list\n"); 
        start = first; 
        printList(start); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python Program to move last m elements 
# to front in a given linked list 

# A linked list node 
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

first = None
last = None

length = 0

# Function to print nodes 
# in a given linked list 
def printList( node): 

    while (node != None) : 
        print( node.data, end=" ") 
        node = node.next

# Pointer head and p are being 
# used here because, the head 
# of the linked list is changed in this function. 
def moveToFront( head, p, m): 

    global first 
    global last 
    global length 

    # If the linked list is empty, 
    # or it contains only one node, 
    # then nothing needs to be done, simply return 
    if (head == None): 
        return head 

    p = head 
    head = head.next
    m= m + 1

    # if m value reaches length, 
    # the recursion will end 
    if (length == m) : 

        # breaking the link 
        p.next = None

        # connecting last to first & 
        # will make another node as head 
        last.next = first 

        # Making the first node of 
        # last m nodes as root 
        first = head 

    else: 
        moveToFront(head, p, m) 

# UTILITY FUNCTIONS 

# Function to add a node at 
# the beginning of Linked List 
def push( head_ref, new_data): 

    global first 
    global last 
    global length 

    # allocate node 
    new_node = Node() 

    # put in the data 
    new_node.data = new_data 

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # move the head to point to the new node 
    (head_ref) = new_node 

    # making first & last nodes 
    if (length == 0): 
        last = head_ref 
    else: 
        first = head_ref 

    # increase the length 
    length= length + 1

    return head_ref 

# Driver code 

start = None

# The constructed linked list is: 
# 1.2.3.4.5 
start = push(start, 5) 
start = push(start, 4) 
start = push(start, 3) 
start = push(start, 2) 
start = push(start, 1) 
start = push(start, 0) 

print("\n Initial Linked list") 
printList(start) 
m = 4 # no.of nodes to change 
temp = None
moveToFront(start, temp, m) 

print("\n Final Linked list") 
start = first 
printList(start) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# Program to move last m elements 
// to front in a given linked list 
using System; 

class GFG  
{ 
    // A linked list node 
    class Node  
    { 
        public int data; 
        public Node next; 
    } 

    static Node first, last; 

    static int length = 0; 

    // Function to print nodes 
    // in a given linked list 
    static void printList(Node node) 
    { 
        while (node != null)  
        { 
            Console.Write("{0} ", node.data); 
            node = node.next; 
        } 
    } 

    // Pointer head and p are being used here 
    // because, the head of the linked list  
    // is changed in this function. 
    static void moveToFront(Node head, 
                            Node p, int m)  
    { 
        // If the linked list is empty, 
        // or it contains only one node, 
        // then nothing needs to be done,  
        // simply return 
        if (head == null) 
            return; 

        p = head; 
        head = head.next; 
        m++; 

        // if m value reaches length, 
        // the recursion will end 
        if (length == m)  
        { 

            // breaking the link 
            p.next = null; 

            // connecting last to first & 
            // will make another node as head 
            last.next = first; 

            // Making the first node of 
            // last m nodes as root 
            first = head; 
        } 
        else
            moveToFront(head, p, m); 
    } 

    // UTILITY FUNCTIONS 

    // Function to add a node at 
    // the beginning of Linked List 
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list off the new node 
        new_node.next = head_ref; 

        // move the head to point to the new node 
        head_ref = new_node; 

        // making first & last nodes 
        if (length == 0) 
            last = head_ref; 
        else
            first = head_ref; 

        // increase the length 
        length++; 
        return head_ref; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        Node start = null; 

        // The constructed linked list is: 
        // 1.2.3.4.5 
        start = push(start, 5); 
        start = push(start, 4); 
        start = push(start, 3); 
        start = push(start, 2); 
        start = push(start, 1); 
        start = push(start, 0); 

        Console.Write("Initial Linked list\n"); 
        printList(start); 
        int m = 4; // no.of nodes to change 
        Node temp = new Node(); 
        moveToFront(start, temp, m); 

        Console.Write("\nFinal Linked list\n"); 
        start = first; 
        printList(start); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Initial Linked list
0 1 2 3 4 5 
 Final Linked list
2 3 4 5 0 1

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。