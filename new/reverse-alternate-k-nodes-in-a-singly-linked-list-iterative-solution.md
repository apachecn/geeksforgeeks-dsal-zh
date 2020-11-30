# 反向链接单链表中的`K`个节点–迭代解决方案

> 原文：[https://www.geeksforgeeks.org/reverse-alternate-k-nodes-in-a-singly-linked-list-iterative-solution/](https://www.geeksforgeeks.org/reverse-alternate-k-nodes-in-a-singly-linked-list-iterative-solution/)

给定一个链表和一个整数`K`，任务是反转每个备用`K`节点。

**示例**：

> **输入**：`1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> NULL, K = 3`
>
> **输出**：`3 2 1 4 5 6 9 8 7`
> 
> **输入**：`1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> NULL, K = 5`
>
> **输出**：`5 4 3 2 1 6 7 8 9`

**方法**：我们已经在此处讨论了递归解决方案。 在这篇文章中，我们将讨论上述问题的迭代解决方案。 在遍历时，我们以一个迭代处理`2k`个节点，并使用连接和尾指针跟踪给定链表中`k`个节点组的第一个和最后一个节点。 反转链表的`k`个节点后，我们将反向列表的最后一个节点（由尾部指针指向）与原始列表的第一个节点（由连接指针指向）连接。 然后，我们移动当前指针，直到跳过接下来的`k`个节点。

现在，尾部成为常规列表的最后一个节点（由更新的尾部指针指向），并且联接点指向反向列表的第一个，然后将它们联接。 我们重复此过程，直到以相同方式处理所有节点。](https://www.geeksforgeeks.org/reverse-alternate-k-nodes-in-a-singly-linked-list/)

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Link list node 
class Node { 
public: 
    int data; 
    Node* next; 
}; 

/* Function to reverse alternate k nodes and  
return the pointer to the new head node */
Node* kAltReverse(struct Node* head, int k) 
{ 
    Node* prev = NULL; 
    Node* curr = head; 
    Node* temp = NULL; 
    Node* tail = NULL; 
    Node* newHead = NULL; 
    Node* join = NULL; 
    int t = 0; 

    // Traverse till the end of the linked list 
    while (curr) { 
        t = k; 
        join = curr; 
        prev = NULL; 

        /* Reverse alternative group of k nodes  
        // of the given linked list */
        while (curr && t--) { 
            temp = curr->next; 
            curr->next = prev; 
            prev = curr; 
            curr = temp; 
        } 

        // Sets the new head of the input list 
        if (!newHead) 
            newHead = prev; 

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. The tail pointer  
        is then joined with the first node of the  
        next k-nodes of the linked list */
        if (tail) 
            tail->next = prev; 

        tail = join; 
        tail->next = curr; 

        t = k; 

        /* Traverse through the next k nodes  
        which will not be reversed */
        while (curr && t--) { 
            prev = curr; 
            curr = curr->next; 
        } 

        /* Tail pointer keeps track of the last  
        node of the k nodes traversed above */
        tail = prev; 
    } 

    // newHead is new head of the modified list 
    return newHead; 
} 

// Function to insert a node at 
// the head of the linked list 
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

// Function to print the linked list 
void printList(Node* node) 
{ 
    int count = 0; 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
        count++; 
    } 
} 

// Driver code 
int main(void) 
{ 

    // Start with the empty list 
    Node* head = NULL; 
    int i; 

    // Create a list 1->2->3->4->...->10 
    for (i = 10; i > 0; i--) 
        push(&head, i); 

    int k = 3; 

    cout << "Given linked list \n"; 
    printList(head); 
    head = kAltReverse(head, k); 

    cout << "\n Modified Linked list \n"; 
    printList(head); 

    return (0); 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG  
{ 

// Link list node 
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head; 

/* Function to reverse alternate k nodes and  
return the pointer to the new head node */
static Node kAltReverse(Node head, int k) 
{ 
    Node prev = null; 
    Node curr = head; 
    Node temp = null; 
    Node tail = null; 
    Node newHead = null; 
    Node join = null; 
    int t = 0; 

    // Traverse till the end of the linked list 
    while (curr != null)  
    { 
        t = k; 
        join = curr; 
        prev = null; 

        /* Reverse alternative group of k nodes  
        // of the given linked list */
        while (curr != null && t-- >0)  
        { 
            temp = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = temp; 
        } 

        // Sets the new head of the input list 
        if (newHead == null) 
            newHead = prev; 

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. The tail pointer  
        is then joined with the first node of the  
        next k-nodes of the linked list */
        if (tail != null) 
            tail.next = prev; 

        tail = join; 
        tail.next = curr; 

        t = k; 

        /* Traverse through the next k nodes  
        which will not be reversed */
        while (curr != null && t-- >0) 
        { 
            prev = curr; 
            curr = curr.next; 
        } 

        /* Tail pointer keeps track of the last  
        node of the k nodes traversed above */
        tail = prev; 
    } 

    // newHead is new head of the modified list 
    return newHead; 
} 

// Function to insert a node at 
// the head of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

// Function to print the linked list 
static void printList(Node node) 
{ 
    int count = 0; 
    while (node != null) 
    { 
        System.out.print(node.data + " "); 
        node = node.next; 
        count++; 
    } 
} 

// Driver code 
public static void main(String[] args)  
{ 
    // Start with the empty list 
    head = null; 
    int i; 

    // Create a list 1->2->3->4->...->10 
    for (i = 10; i > 0; i--) 
        push(head, i); 

    int k = 3; 

    System.out.print("Given linked list \n"); 
    printList(head); 
    head = kAltReverse(head, k); 

    System.out.print("\n Modified Linked list \n"); 
    printList(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python

```py

# Python implementation of the approach 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data # Assign data  
        self.next = None

head = None

# Function to reverse alternate k nodes and  
# return the pointer to the new head node  
def kAltReverse(head, k): 

    prev = None
    curr = head 
    temp = None
    tail = None
    newHead = None
    join = None
    t = 0

    # Traverse till the end of the linked list 
    while (curr != None) : 

        t = k 
        join = curr 
        prev = None

        # Reverse alternative group of k nodes  
        # of the given linked list  
        while (curr != None and t > 0):  

            t = t - 1
            temp = curr.next
            curr.next = prev 
            prev = curr 
            curr = temp 

        # Sets the new head of the input list 
        if (newHead == None): 
            newHead = prev 

        # Tail pointer keeps track of the last node  
        # of the k-reversed linked list. The tail pointer  
        # is then joined with the first node of the  
        # next k-nodes of the linked list  
        if (tail != None): 
            tail.next = prev 

        tail = join 
        tail.next = curr 

        t = k 

        # Traverse through the next k nodes  
        # which will not be reversed  
        while (curr != None and t > 0): 
            t = t - 1
            prev = curr 
            curr = curr.next

        # Tail pointer keeps track of the last  
        # node of the k nodes traversed above  
        tail = prev 

    # newHead is new head of the modified list 
    return newHead 

# Function to insert a node at 
# the head of the linked list 
def push(head_ref, new_data): 

    global head 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list off the new node  
    new_node.next = head_ref 

    # move the head to point to the new node  
    head_ref = new_node 
    head = head_ref 

# Function to print the linked list 
def printList(node): 

    count = 0
    while (node != None): 

        print(node.data ,end= " ") 
        node = node.next
        count = count + 1

# Driver code 

# Start with the empty list 
head = None
i = 10

# Create a list 1->2->3->4->...->10 
while ( i > 0 ): 
    push(head, i) 
    i = i - 1

k = 3

print("Given linked list ") 
printList(head) 
head = kAltReverse(head, k) 

print("\n Modified Linked list ") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG  
{ 

// Link list node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head; 

/* Function to reverse alternate k nodes and  
return the pointer to the new head node */
static Node kAltReverse(Node head, int k) 
{ 
    Node prev = null; 
    Node curr = head; 
    Node temp = null; 
    Node tail = null; 
    Node newHead = null; 
    Node join = null; 
    int t = 0; 

    // Traverse till the end of the linked list 
    while (curr != null)  
    { 
        t = k; 
        join = curr; 
        prev = null; 

        /* Reverse alternative group of k nodes  
        // of the given linked list */
        while (curr != null && t-- >0)  
        { 
            temp = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = temp; 
        } 

        // Sets the new head of the input list 
        if (newHead == null) 
            newHead = prev; 

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. The tail pointer  
        is then joined with the first node of the  
        next k-nodes of the linked list */
        if (tail != null) 
            tail.next = prev; 

        tail = join; 
        tail.next = curr; 

        t = k; 

        /* Traverse through the next k nodes  
        which will not be reversed */
        while (curr != null && t-- >0) 
        { 
            prev = curr; 
            curr = curr.next; 
        } 

        /* Tail pointer keeps track of the last  
        node of the k nodes traversed above */
        tail = prev; 
    } 

    // newHead is new head of the modified list 
    return newHead; 
} 

// Function to insert a node at 
// the head of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

// Function to print the linked list 
static void printList(Node node) 
{ 
    int count = 0; 
    while (node != null) 
    { 
        Console.Write(node.data + " "); 
        node = node.next; 
        count++; 
    } 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    // Start with the empty list 
    head = null; 
    int i; 

    // Create a list 1->2->3->4->...->10 
    for (i = 10; i > 0; i--) 
        push(head, i); 

    int k = 3; 

    Console.Write("Given linked list \n"); 
    printList(head); 
    head = kAltReverse(head, k); 

    Console.Write("\nModified Linked list \n"); 
    printList(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Given linked list 
1 2 3 4 5 6 7 8 9 10 
 Modified Linked list 
3 2 1 4 5 6 9 8 7 10

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。