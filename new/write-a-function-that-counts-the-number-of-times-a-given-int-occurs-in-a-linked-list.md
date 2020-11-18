# 编写一个函数，计算一个给定的 int 在链表

> 原文：[https://www.geeksforgeeks.org/write-a-function-that-counts-the-number-of-times-a-given-int-occurs-in-a-linked-list/](https://www.geeksforgeeks.org/write-a-function-that-counts-the-number-of-times-a-given-int-occurs-in-a-linked-list/)

中出现的次数

给定一个单链表和一个键，计算给定键在链表中出现的次数。 例如，如果给定的链表为 1-> 2-> 1-> 2-> 1-> 3-> 1，且给定键为 1，则输出应为 4。

**方法 1-无递归**

**算法**：

```
1\. Initialize count as zero.
2\. Loop through each element of linked list:
     a) If element data is equal to the passed number then
        increment the count.
3\. Return count. 

```

**实施**：

## C++

```cpp

// C++ program to count occurrences in a linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

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

/* Counts the no. of occurrences of a node  
(search_for) in a linked list (head)*/
int count(Node* head, int search_for) 
{ 
    Node* current = head; 
    int count = 0; 
    while (current != NULL) { 
        if (current->data == search_for) 
            count++; 
        current = current->next; 
    } 
    return count; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    /* Use push() to construct below list  
    1->2->1->3->1 */
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 1); 

    /* Check the count function */
    cout << "count of 1 is " << count(head, 1); 
    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to count occurrences in a linked list 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Counts the no. of occurrences of a node 
   (search_for) in a linked list (head)*/
int count(struct Node* head, int search_for) 
{ 
    struct Node* current = head; 
    int count = 0; 
    while (current != NULL) { 
        if (current->data == search_for) 
            count++; 
        current = current->next; 
    } 
    return count; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
     1->2->1->3->1  */
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 1); 

    /* Check the count function */
    printf("count of 1 is %d", count(head, 1)); 
    return 0; 
} 

```

## Java

```java

// Java program to count occurrences in a linked list 
class LinkedList { 
    Node head; // head of list 

    /* Linked list Node*/
    class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

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

    /* Counts the no. of occurrences of a node 
    (search_for) in a linked list (head)*/
    int count(int search_for) 
    { 
        Node current = head; 
        int count = 0; 
        while (current != null) { 
            if (current.data == search_for) 
                count++; 
            current = current.next; 
        } 
        return count; 
    } 

    /* Driver function to test the above methods */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Use push() to construct below list 
          1->2->1->3->1  */
        llist.push(1); 
        llist.push(2); 
        llist.push(1); 
        llist.push(3); 
        llist.push(1); 

        /*Checking count function*/
        System.out.println("Count of 1 is " + llist.count(1)); 
    } 
} 
// This code is contributed by Rajat Mishra 

```

## Python

```py

# Python program to count the number of time a given 
# int occurs in a linked list 

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

    # Counts the no . of occurrences of a node 
    # (search_for) in a linked list (head) 
    def count(self, search_for): 
        current = self.head 
        count = 0
        while(current is not None): 
            if current.data == search_for: 
                count += 1
            current = current.next
        return count 

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

# Driver program 
llist = LinkedList() 
llist.push(1) 
llist.push(3) 
llist.push(1) 
llist.push(2) 
llist.push(1) 

# Check for the count function 
print "count of 1 is % d" %(llist.count(1)) 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# program to count occurrences in a linked list 
using System; 
class LinkedList { 
    Node head; // head of list 

    /* Linked list Node*/
    public class Node { 
        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

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

    /* Counts the no. of occurrences of a node  
    (search_for) in a linked list (head)*/
    int count(int search_for) 
    { 
        Node current = head; 
        int count = 0; 
        while (current != null) { 
            if (current.data == search_for) 
                count++; 
            current = current.next; 
        } 
        return count; 
    } 

    /* Driver code */
    public static void Main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Use push() to construct below list  
        1->2->1->3->1 */
        llist.push(1); 
        llist.push(2); 
        llist.push(1); 
        llist.push(3); 
        llist.push(1); 

        /*Checking count function*/
        Console.WriteLine("Count of 1 is " + llist.count(1)); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

**Output:**

```
count of 1 is 3
```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`

**方法 2-递归**

此方法由 [MY_DOOM](https://auth.geeksforgeeks.org/user/MY_DOOM) 贡献。

**算法**：

```
Algorithm
count(head, key);
if head is NULL
return frequency
if(head->data==key)
increase frequency by 1
count(head->next, key)

```

**实施**：

## C++

```cpp

// C++ program to count occurrences in 
// a linked list using recursion 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 
// global variable for counting frequeancy of 
// given element k 
int frequency = 0; 

/* Given a reference (pointer to pointer) to the head 
of a list and an int, push a new node on the front 
of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Counts the no. of occurrences of a node 
(search_for) in a linked list (head)*/
int count(struct Node* head, int key) 
{ 
    if (head == NULL) 
        return frequency; 
    if (head->data == key) 
        frequency++; 
    return count(head->next, key); 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
     1->2->1->3->1  */
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 1); 

    /* Check the count function */
    cout << "count of 1 is " << count(head, 1); 
    return 0; 
} 

```

## Java

```java

// Java program to count occurrences in 
// a linked list using recursion 
import java.io.*; 
import java.util.*; 

// Represents node of a linkedlist 
class Node { 
    int data; 
    Node next; 
    Node(int val) 
    { 
        data = val; 
        next = null; 
    } 
} 

class GFG { 

    // global variable for counting frequeancy of 
    // given element k 
    static int frequency = 0; 

    /* Given a reference (pointer to pointer) to the head  
    of a list and an int, push a new node on the front  
    of the list. */

    static Node push(Node head, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(new_data); 

        // link the old list off the new node 
        new_node.next = head; 

        // move the head to point to the new node 
        head = new_node; 

        return head; 
    } 

    /* Counts the no. of occurrences of a node  
    (search_for) in a linked list (head)*/
    static int count(Node head, int key) 
    { 
        if (head == null) 
            return frequency; 
        if (head.data == key) 
            frequency++; 
        return count(head.next, key); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        // Start with the empty list 
        Node head = null; 

        /* Use push() to construct below list  
        1->2->1->3->1 */
        head = push(head, 1); 
        head = push(head, 3); 
        head = push(head, 1); 
        head = push(head, 2); 
        head = push(head, 1); 

        /* Check the count function */
        System.out.print("count of 1 is " + count(head, 1)); 
    } 
} 

// This code is contributed by rachana soma 

```

## Python3

```py

# Python program to count the number of  
# time a given int occurs in a linked list 
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
        self.counter = 0

    # Counts the no . of occurances of a node 
    # (seach_for) in a linkded list (head) 
    def count(self, li, key):      

        # Base case  
        if(not li):  
            return self.counter 

        # If key is present in  
        # current node, return true  
        if(li.data == key):  
            self.counter = self.counter + 1

        # Recur for remaining list  
        return self.count(li.next, key)  

    # Function to insert a new node  
    # at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Utility function to print the  
    # linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print (temp.data) 
            temp = temp.next

# Driver Code 
llist = LinkedList() 
llist.push(1) 
llist.push(3) 
llist.push(1) 
llist.push(2) 
llist.push(1) 

# Check for the count function 
print ("count of 1 is", llist.count(llist.head, 1)) 

# This code is contributed by  
# Gaurav Kumar Raghav 

```

## C#

```cs

// C# program to count occurrences in 
// a linked list using recursion 
using System; 

// Represents node of a linkedlist 
public class Node { 
    public int data; 
    public Node next; 
    public Node(int val) 
    { 
        data = val; 
        next = null; 
    } 
} 

class GFG { 

    // global variable for counting frequeancy of 
    // given element k 
    static int frequency = 0; 

    /* Given a reference (pointer to pointer) to the head  
    of a list and an int, push a new node on the front  
    of the list. */

    static Node push(Node head, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(new_data); 

        // link the old list off the new node 
        new_node.next = head; 

        // move the head to point to the new node 
        head = new_node; 

        return head; 
    } 

    /* Counts the no. of occurrences of a node  
    (search_for) in a linked list (head)*/
    static int count(Node head, int key) 
    { 
        if (head == null) 
            return frequency; 
        if (head.data == key) 
            frequency++; 
        return count(head.next, key); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        // Start with the empty list 
        Node head = null; 

        /* Use push() to construct below list  
        1->2->1->3->1 */
        head = push(head, 1); 
        head = push(head, 3); 
        head = push(head, 1); 
        head = push(head, 2); 
        head = push(head, 1); 

        /* Check the count function */
        Console.Write("count of 1 is " + count(head, 1)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
count of 1 is 3
```

下面的方法可用于避免全局变量“ frequency”（在 Python 3 代码的情况下为反计数）。

## C++

```cpp

// method can be used to avoid 
// Global variable 'frequency' 

/* Counts the no. of occurrences of a node  
(search_for) in a linked list (head)*/
int count(struct Node* head, int key) 
{ 
    if (head == NULL) 
        return 0; 
    if (head->data == key) 
        return 1 + count(head->next, key); 
    return count(head->next, key); 
} 

```

## Java

```java

// method can be used to avoid 
// Global variable 'frequency' 

/* Counts the no. of occurrences of a node  
(search_for) in a linked list (head)*/
int count(Node head, int key) 
{ 
    if (head == null) 
        return 0; 
    if (head.data == key) 
        return 1 + count(head.next, key); 
    return count(head.next, key); 
} 

// This code is contributed by rachana soma 

```

## C#

```cs

// method can be used to avoid 
// Global variable 'frequency' 
using System;  

/* Counts the no. of occurrences of a node  
(search_for) in a linked list (head)*/
static int count(Node head, int key)  
{  
    if (head == null)  
        return 0;  
    if (head.data == key)  
        return 1 + count(head.next, key); 
    return count(head.next, key);  
}  

// This code is contributed by SHUBHAMSINGH10 

```

## Python3

```py

def count(self, temp, key): 

    # during the initial call, temp 
    # has the value of head 

    # Base case 
    if temp is None: 
        return 0

    # if a match is found, we  
    # increment the counter 
    if temp.data == key: 
        return 1 + count(temp.next, key) 
    return count(temp.next, key) 

# to call count, use 
# linked_list_name.count(head, key) 

```

以上方法实现了头递归。 下面给出了相同的尾部递归实现。 感谢 **Puneet Jain** 提出了这种方法：

```
int count(struct Node* head, int key)
{
    if(head == NULL)
        return 0;

   int frequency = count(head->next, key);
   if(head->data == key)
     return 1 + frequency;

    // else 
    return frequency;
}

```

**时间复杂度**：`O(n)`

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

