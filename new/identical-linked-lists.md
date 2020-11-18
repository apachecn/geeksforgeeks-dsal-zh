# 相同的链接列表

> 原文：[https://www.geeksforgeeks.org/identical-linked-lists/](https://www.geeksforgeeks.org/identical-linked-lists/)

当两个链表具有相同的数据并且数据的排列也相同时，它们是相同的。 例如，链接列表 a（1-> 2-> 3）和 b（1-> 2-> 3）相同。 。 编写一个函数来检查给定的两个链表是否相同。

**方法 1（迭代）**

要确定两个列表是否相同，我们需要同时遍历两个列表，并且在遍历时需要比较数据。

## C++

```cpp

// An iterative C++ program to check if  
// two linked lists are identical or not 
#include<bits/stdc++.h> 
using namespace std; 

/* Structure for a linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Returns true if linked lists a and b  
are identical, otherwise false */
bool areIdentical(struct Node *a,  
                  struct Node *b) 
{ 
    while (a != NULL && b != NULL) 
    { 
        if (a->data != b->data) 
            return false; 

        /* If we reach here, then a and b are  
        not NULL and their data is same, so  
        move to next nodes in both lists */
        a = a->next; 
        b = b->next; 
    } 

    // If linked lists are identical, then  
    // 'a' and 'b' must be NULL at this point. 
    return (a == NULL && b == NULL); 
} 

/* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
/* Given a reference (pointer to pointer) to the  
head of a list and an int, push a new node on the  
front of the list. */
void push(struct Node** head_ref, int new_data) 
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

// Driver Code 
int main() 
{ 
    /* The constructed linked lists are : 
    a: 3->2->1 
    b: 3->2->1 */
    struct Node *a = NULL; 
    struct Node *b = NULL; 
    push(&a, 1); 
    push(&a, 2); 
    push(&a, 3); 
    push(&b, 1); 
    push(&b, 2); 
    push(&b, 3); 

    if(areIdentical(a, b)) 
        cout << "Identical"; 
    else
        cout << "Not identical"; 

    return 0; 
} 

// This code is contributed  
// by Akanksha Rai 

```

## C

```c

// An iterative C program to check if two linked lists are 
// identical or not 
#include<stdio.h> 
#include<stdlib.h> 
#include<stdbool.h> 

/* Structure for a linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Returns true if linked lists a and b are identical, 
   otherwise false */
bool areIdentical(struct Node *a, struct Node *b) 
{ 
    while (a != NULL && b != NULL) 
    { 
        if (a->data != b->data) 
            return false; 

        /* If we reach here, then a and b are not NULL and 
           their data is same, so move to next nodes in both 
           lists */
        a = a->next; 
        b = b->next; 
    } 

    // If linked lists are identical, then 'a' and 'b' must 
    // be NULL at this point. 
    return (a == NULL && b == NULL); 
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

/* Driver program to test above function */
int main() 
{ 
    /* The constructed linked lists are : 
     a: 3->2->1 
     b: 3->2->1 */
    struct Node *a = NULL; 
    struct Node *b = NULL; 
    push(&a, 1); 
    push(&a, 2); 
    push(&a, 3); 
    push(&b, 1); 
    push(&b, 2); 
    push(&b, 3); 

    areIdentical(a, b)? printf("Identical"): 
                        printf("Not identical"); 

    return 0; 
} 

```

## Java

```java

// An iterative Java program to check if two linked lists 
// are identical or not 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) { data = d; next = null; } 
    } 

    /* Returns true if linked lists a and b are identical, 
       otherwise false */
    boolean areIdentical(LinkedList listb) 
    { 
        Node a = this.head, b = listb.head; 
        while (a != null && b != null) 
        { 
            if (a.data != b.data) 
                return false; 

            /* If we reach here, then a and b are not null 
               and their data is same, so move to next nodes 
               in both lists */
            a = a.next; 
            b = b.next; 
        } 

        // If linked lists are identical, then 'a' and 'b' must 
        // be null at this point. 
        return (a == null && b == null); 
    } 

    /* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
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

        /* The constructed linked lists are : 
           llist1: 3->2->1 
           llist2: 3->2->1 */

        llist1.push(1); 
        llist1.push(2); 
        llist1.push(3); 

        llist2.push(1); 
        llist2.push(2); 
        llist2.push(3); 

        if (llist1.areIdentical(llist2) == true) 
            System.out.println("Identical "); 
        else
            System.out.println("Not identical "); 

    } 
} /* This code is contributed by Rajat Mishra */

```

## Python3

```py

# An iterative Java program to check if  
# two linked lists are identical or not  

# Linked list Node  
class Node:  
    def __init__(self, d): 
        self.data = d 
        self.next = None

class LinkedList: 
    def __init__(self): 
        self.head = None # head of list  

    # Returns true if linked lists a and b 
    # are identical, otherwise false  
    def areIdentical(self, listb):  
        a = self.head 
        b = listb.head 
        while (a != None and b != None):  
            if (a.data != b.data):  
                return False

            # If we reach here, then a and b  
            # are not null and their data is  
            # same, so move to next nodes  
            # in both lists  
            a = a.next
            b = b.next

        # If linked lists are identical,  
        # then 'a' and 'b' must be null 
        # at this point.  
        return (a == None and b == None)  

    # UTILITY FUNCTIONS TO TEST fun1() and fun2()  
    # Given a reference (pointer to pointer) to the  
    # head of a list and an int, push a new node on  
    # the front of the list.  

    def push(self, new_data): 

        # 1 & 2: Allocate the Node &  
        # Put in the data 
        new_node = Node(new_data)  

        # 3\. Make next of new Node as head  
        new_node.next = self.head  

        # 4\. Move the head to point to new Node  
        self.head = new_node 

# Driver Code 
llist1 = LinkedList()  
llist2 = LinkedList()  

# The constructed linked lists are :  
# llist1: 3->2->1  
# llist2: 3->2->1  
llist1.push(1)  
llist1.push(2)  
llist1.push(3)  
llist2.push(1)  
llist2.push(2)  
llist2.push(3)  

if (llist1.areIdentical(llist2) == True):  
    print("Identical ") 
else: 
    print("Not identical ") 

# This code is contributed by Prerna Saini 

```

## C#

```cs

// An iterative C# program to  
// check if two linked lists 
// are identical or not 
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

    /* Returns true if linked lists  
    a and b are identical, 
    otherwise false */
    bool areIdentical(LinkedList listb) 
    { 
        Node a = this.head, b = listb.head; 
        while (a != null && b != null) 
        { 
            if (a.data != b.data) 
                return false; 

            /* If we reach here, then a and b are not null 
            and their data is same, so move to next nodes 
            in both lists */
            a = a.next; 
            b = b.next; 
        } 

        // If linked lists are identical, 
        // then 'a' and 'b' must 
        // be null at this point. 
        return (a == null && b == null); 
    } 

    /* UTILITY FUNCTIONS TO TEST fun1() and fun2() */
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

    /* Driver code */
    public static void Main(String []args) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 

        /* The constructed linked lists are : 
        llist1: 3->2->1 
        llist2: 3->2->1 */

        llist1.push(1); 
        llist1.push(2); 
        llist1.push(3); 

        llist2.push(1); 
        llist2.push(2); 
        llist2.push(3); 

        if (llist1.areIdentical(llist2) == true) 
            Console.WriteLine("Identical "); 
        else
            Console.WriteLine("Not identical "); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
Identical
```

**方法 2（递归）**

递归解决方案代码比迭代代码干净得多。 不过，您可能不希望将递归版本用于生产代码，因为它会使用与列表长度成比例的堆栈空间

## C++

```cpp

// A recursive C++ function to check if two linked  
// lists are identical or not  
bool areIdentical(Node *a, Node *b)  
{  
    // If both lists are empty  
    if (a == NULL && b == NULL)  
    return true;  

    // If both lists are not empty, then data of  
    // current nodes must match, and same should  
    // be recursively true for rest of the nodes.  
    if (a != NULL && b != NULL)  
    return (a->data == b->data) &&  
            areIdentical(a->next, b->next);  

    // If we reach here, then one of the lists  
    // is empty and other is not  
    return false;  
}  

//This is code is contributed by rathbhupendra 

```

## C

```c

// A recursive C function to check if two linked 
// lists are identical or not 
bool areIdentical(struct Node *a, struct Node *b) 
{ 
    // If both lists are empty 
    if (a == NULL && b == NULL) 
       return true; 

    // If both lists are not empty, then data of 
    // current nodes must match, and same should 
    // be recursively true for rest of the nodes. 
    if (a != NULL && b != NULL) 
       return (a->data == b->data) && 
              areIdentical(a->next, b->next); 

    // If we reach here, then one of the lists 
    // is empty and other is not 
    return false; 
} 

```

## Java

```java

// A recursive Java method to check if two linked 
// lists are identical or not 
boolean areIdenticalRecur(Node a, Node b) 
{ 
    // If both lists are empty 
    if (a == null && b == null) 
        return true; 

    // If both lists are not empty, then data of 
    // current nodes must match, and same should 
    // be recursively true for rest of the nodes. 
    if (a != null && b != null) 
        return (a.data == b.data) && 
               areIdenticalRecur(a.next, b.next); 

    // If we reach here, then one of the lists 
    // is empty and other is not 
    return false; 
} 

/* Returns true if linked lists a and b are identical, 
   otherwise false */
boolean areIdentical(LinkedList listb) 
{ 
    return areIdenticalRecur(this.head, listb.head); 
} 

```

## Python3

```py

# A recursive Python3 function to check  
# if two linked lists are identical or not  
def areIdentical(a, b):  

    # If both lists are empty  
    if (a == None and b == None):  
        return True

    # If both lists are not empty,  
    # then data of current nodes must match,  
    # and same should be recursively true  
    # for rest of the nodes.  
    if (a != None and b != None):  
        return ((a.data == b.data) and 
                 areIdentical(a.next, b.next))  

    # If we reach here, then one of the lists  
    # is empty and other is not  
    return False

# This code is contributed by Princi Singh 

```

## C#

```cs

// A recursive C# method to  
// check if two linked lists  
// are identical or not  
bool areIdenticalRecur(Node a, Node b)  
{  
    // If both lists are empty  
    if (a == null && b == null)  
        return true;  

    // If both lists are not empty, then data of  
    // current nodes must match, and same should  
    // be recursively true for rest of the nodes.  
    if (a != null && b != null)  
        return (a.data == b.data) &&  
            areIdenticalRecur(a.next, b.next);  

    // If we reach here, then one of the lists  
    // is empty and other is not  
    return false;  
}  

/* Returns true if linked lists  
a and b are identical, otherwise false */
bool areIdentical(LinkedList listb)  
{  
    return areIdenticalRecur(this.head, listb.head);  
}  
} 

// This code is contributed by princiraj1992 

```

**时间复杂度：迭代和递归版本的**`O(n)`。 n 是 a 和 b 中较小列表的长度。

如果您发现上述代码/算法有误，请写评论，或者找到解决同一问题的更好方法。

