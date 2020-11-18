# 交换链表中的节点而不交换数据

给定一个链表和其中的两个键，将节点交换为两个给定的键。 应通过更改链接来交换节点。 当数据包含许多字段时，在许多情况下交换节点的数据可能会很昂贵。
可以假定链接列表中的所有键都是不同的。
**范例：**

```
Input:  10->15->12->13->20->14,  x = 12, y = 20
Output: 10->15->20->13->12->14

Input:  10->15->12->13->20->14,  x = 10, y = 20
Output: 20->15->12->13->10->14

Input:  10->15->12->13->20->14,  x = 12, y = 13
Output: 10->15->13->12->20->14

```

这可能看起来很简单，但是却是一个有趣的问题，因为有以下几种情况需要处理。
1）x 和 y 可以相邻也可以不相邻。
2）x 或 y 可以是头节点。
3）x 或 y 可能是最后一个节点。
4）x 和/或 y 可能不在链接列表中。

如何编写干净的工作代码来处理上述所有可能性。

**我们强烈建议您最小化您的浏览器，然后自己尝试。**
的想法是首先在给定的链表中搜索 x 和 y。 如果其中不存在，则返回。 在搜索 x 和 y 时，请跟踪当前和先前的指针。 首先更改前一个指针的下一个，然后更改当前指针的下一个。

下面是上述方法的实现。

## C++

```cpp

/* This program swaps the nodes of linked list rather  
than swapping the field from the nodes.*/
#include <bits/stdc++.h> 
using namespace std; 

/* A linked list node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

/* Function to swap nodes x and y in linked list by  
changing links */
void swapNodes(Node **head_ref, int x, int y)  
{  
// Nothing to do if x and y are same  
if (x == y) return;  

// Search for x (keep track of prevX and CurrX  
Node *prevX = NULL, *currX = *head_ref;  
while (currX && currX->data != x)  
{  
    prevX = currX;  
    currX = currX->next;  
}  

// Search for y (keep track of prevY and CurrY  
Node *prevY = NULL, *currY = *head_ref;  
while (currY && currY->data != y)  
{  
    prevY = currY;  
    currY = currY->next;  
}  

// If either x or y is not present, nothing to do  
if (currX == NULL || currY == NULL)  
    return;  

// If x is not head of linked list  
if (prevX != NULL)  
    prevX->next = currY;  
else // Else make y as new head  
    *head_ref = currY;  

// If y is not head of linked list  
if (prevY != NULL)  
    prevY->next = currX;  
else // Else make x as new head  
    *head_ref = currX;  

// Swap next pointers  
Node *temp = currY->next;  
currY->next = currX->next;  
currX->next = temp;  
}  

/* Function to add a node at the beginning of List */
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node =new Node(); 

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
    while(node != NULL)  
    {  
        cout<<node->data<<" ";  
        node = node->next;  
    }  
}  

/* Driver program to test above function */
int main()  
{  
    Node *start = NULL;  

    /* The constructed linked list is:  
    1->2->3->4->5->6->7 */
    push(&start, 7);  
    push(&start, 6);  
    push(&start, 5);  
    push(&start, 4);  
    push(&start, 3);  
    push(&start, 2);  
    push(&start, 1);  

    cout << "Linked list before calling swapNodes() ";  
    printList(start);  

    swapNodes(&start, 4, 3);  

    cout << "\nLinked list after calling swapNodes() ";  
    printList(start);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

/* This program swaps the nodes of linked list rather 
   than swapping the field from the nodes.*/

#include<stdio.h> 
#include<stdlib.h> 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Function to swap nodes x and y in linked list by 
   changing links */
void swapNodes(struct Node **head_ref, int x, int y) 
{ 
   // Nothing to do if x and y are same 
   if (x == y) return; 

   // Search for x (keep track of prevX and CurrX 
   struct Node *prevX = NULL, *currX = *head_ref; 
   while (currX && currX->data != x) 
   { 
       prevX = currX; 
       currX = currX->next; 
   } 

   // Search for y (keep track of prevY and CurrY 
   struct Node *prevY = NULL, *currY = *head_ref; 
   while (currY && currY->data != y) 
   { 
       prevY = currY; 
       currY = currY->next; 
   } 

   // If either x or y is not present, nothing to do 
   if (currX == NULL || currY == NULL) 
       return; 

   // If x is not head of linked list 
   if (prevX != NULL) 
       prevX->next = currY; 
   else // Else make y as new head 
       *head_ref = currY;   

   // If y is not head of linked list 
   if (prevY != NULL) 
       prevY->next = currX; 
   else  // Else make x as new head 
       *head_ref = currX; 

   // Swap next pointers 
   struct Node *temp = currY->next; 
   currY->next = currX->next; 
   currX->next  = temp; 
} 

/* Function to add a node at the beginning of List */
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
    while(node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function */
int main() 
{ 
    struct Node *start = NULL; 

    /* The constructed linked list is: 
     1->2->3->4->5->6->7 */
    push(&start, 7); 
    push(&start, 6); 
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 

    printf("\n Linked list before calling swapNodes() "); 
    printList(start); 

    swapNodes(&start, 4, 3); 

    printf("\n Linked list after calling swapNodes() "); 
    printList(start); 

    return 0; 
} 

```

## Java

```java

// Java program to swap two given nodes of a linked list 

class Node 
{ 
    int data; 
    Node next; 
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

class LinkedList 
{ 
    Node head; // head of list 

    /* Function to swap Nodes x and y in linked list by 
       changing links */
    public void swapNodes(int x, int y) 
    { 
        // Nothing to do if x and y are same 
        if (x == y) return; 

        // Search for x (keep track of prevX and CurrX) 
        Node prevX = null, currX = head; 
        while (currX != null && currX.data != x) 
        { 
            prevX = currX; 
            currX = currX.next; 
        } 

        // Search for y (keep track of prevY and currY) 
        Node prevY = null, currY = head; 
        while (currY != null && currY.data != y) 
        { 
            prevY = currY; 
            currY = currY.next; 
        } 

        // If either x or y is not present, nothing to do 
        if (currX == null || currY == null) 
            return; 

        // If x is not head of linked list 
        if (prevX != null) 
            prevX.next = currY; 
        else //make y the new head 
            head = currY; 

        // If y is not head of linked list 
        if (prevY != null) 
            prevY.next = currX; 
        else // make x the new head 
            head = currX; 

        // Swap next pointers 
        Node temp = currX.next; 
        currX.next = currY.next; 
        currY.next = temp; 
    } 

    /* Function to add Node at beginning of list. */
    public void push(int new_data) 
    { 
        /* 1\. alloc the Node and put the data */
        Node new_Node = new Node(new_data); 

        /* 2\. Make next of new Node as head */
        new_Node.next = head; 

        /* 3\. Move the head to point to new Node */
        head = new_Node; 
    } 

    /* This function prints contents of linked list starting 
       from the given Node */
    public void printList() 
    { 
        Node tNode = head; 
        while (tNode != null) 
        { 
            System.out.print(tNode.data+" "); 
            tNode = tNode.next; 
        } 
    } 

    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        /* The constructed linked list is: 
            1->2->3->4->5->6->7 */
        llist.push(7); 
        llist.push(6); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        System.out.print("\n Linked list before calling swapNodes() "); 
        llist.printList(); 

        llist.swapNodes(4, 3); 

        System.out.print("\n Linked list after calling swapNodes() "); 
        llist.printList(); 
    } 
} 
// This code is contributed by Rajat Mishra 

```

## 蟒蛇

```

# Python program to swap two given nodes of a linked list 
class LinkedList(object): 
    def __init__(self): 
        self.head = None

    # head of list 
    class Node(object): 
        def __init__(self, d): 
            self.data = d 
            self.next = None

    # Function to swap Nodes x and y in linked list by 
    # changing links 
    def swapNodes(self, x, y): 

        # Nothing to do if x and y are same 
        if x == y: 
            return 

        # Search for x (keep track of prevX and CurrX) 
        prevX = None
        currX = self.head 
        while currX != None and currX.data != x: 
            prevX = currX 
            currX = currX.next

        # Search for y (keep track of prevY and currY) 
        prevY = None
        currY = self.head 
        while currY != None and currY.data != y: 
            prevY = currY 
            currY = currY.next

        # If either x or y is not present, nothing to do 
        if currX == None or currY == None: 
            return 
        # If x is not head of linked list 
        if prevX != None: 
            prevX.next = currY 
        else: #make y the new head 
            self.head = currY 

        # If y is not head of linked list 
        if prevY != None: 
            prevY.next = currX 
        else: # make x the new head 
            self.head = currX 

        # Swap next pointers 
        temp = currX.next
        currX.next = currY.next
        currY.next = temp 

    # Function to add Node at beginning of list. 
    def push(self, new_data): 

        # 1\. alloc the Node and put the data 
        new_Node = self.Node(new_data) 

        # 2\. Make next of new Node as head 
        new_Node.next = self.head 

        # 3\. Move the head to point to new Node 
        self.head = new_Node 

    # This function prints contents of linked list starting 
    # from the given Node 
    def printList(self): 
        tNode = self.head 
        while tNode != None: 
            print tNode.data, 
            tNode = tNode.next

# Driver program to test above function 
llist = LinkedList() 

# The constructed linked list is: 
# 1->2->3->4->5->6->7 
llist.push(7) 
llist.push(6) 
llist.push(5) 
llist.push(4) 
llist.push(3) 
llist.push(2) 
llist.push(1) 
print "Linked list before calling swapNodes() "
llist.printList() 
llist.swapNodes(4, 3) 
print "\nLinked list after calling swapNodes() "
llist.printList() 

# This code is contributed by BHAVYA JAIN 

```

## C#

```cs

// C# program to swap two given  
// nodes of a linked list  
using System;  

class Node  
{  
    public int data;  
    public Node next;  
    public Node(int d)  
    {  
        data = d;  
        next = null;  
    }  
}  

public class LinkedList  
{  
    Node head; // head of list  

    /* Function to swap Nodes x and y in   
    linked list by changing links */
    public void swapNodes(int x, int y)  
    {  
        // Nothing to do if x and y are same  
        if (x == y) return;  

        // Search for x (keep track of prevX and CurrX)  
        Node prevX = null, currX = head;  
        while (currX != null && currX.data != x)  
        {  
            prevX = currX;  
            currX = currX.next;  
        }  

        // Search for y (keep track of prevY and currY)  
        Node prevY = null, currY = head;  
        while (currY != null && currY.data != y)  
        {  
            prevY = currY;  
            currY = currY.next;  
        }  

        // If either x or y is not present, nothing to do  
        if (currX == null || currY == null)  
            return;  

        // If x is not head of linked list  
        if (prevX != null)  
            prevX.next = currY;  
        else //make y the new head  
            head = currY;  

        // If y is not head of linked list  
        if (prevY != null)  
            prevY.next = currX;  
        else // make x the new head  
            head = currX;  

        // Swap next pointers  
        Node temp = currX.next;  
        currX.next = currY.next;  
        currY.next = temp;  
    }  

    /* Function to add Node at beginning of list. */
    public void push(int new_data)  
    {  
        /* 1\. alloc the Node and put the data */
        Node new_Node = new Node(new_data);  

        /* 2\. Make next of new Node as head */
        new_Node.next = head;  

        /* 3\. Move the head to point to new Node */
        head = new_Node;  
    }  

    /* This function prints contents of linked list  
    starting from the given Node */
    public void printList()  
    {  
        Node tNode = head;  
        while (tNode != null)  
        {  
            Console.Write(tNode.data+" ");  
            tNode = tNode.next;  
        }  
    }  

    /* Driver code */
    public static void Main(String[] args)  
    {  
        LinkedList llist = new LinkedList();  

        /* The constructed linked list is:  
            1->2->3->4->5->6->7 */
        llist.push(7);  
        llist.push(6);  
        llist.push(5);  
        llist.push(4);  
        llist.push(3);  
        llist.push(2);  
        llist.push(1);  

        Console.Write("\n Linked list before calling swapNodes() ");  
        llist.printList();  

        llist.swapNodes(4, 3);  

        Console.Write("\n Linked list after calling swapNodes() ");  
        llist.printList();  
    }  
}  

// This code is contributed by 29AjayKumar 

```

**输出：**

```
 Linked list before calling swapNodes() 1 2 3 4 5 6 7
 Linked list after calling swapNodes() 1 2 4 3 5 6 7

```

**优化：**可以优化以上代码以单遍遍搜索 x 和 y。 两个循环用于使程序保持简单。
**更简单的方法–**

## C++

```cpp

// C++ program to swap two given nodes of a linked list 
#include <iostream> 

using namespace std; 

// A linked list node class 
class Node { 

public: 
    int data; 
    class Node* next; 

    // constructor 
    Node(int val, Node* next) 
        : data(val), next(next) 
    { 
    } 

    // print list from this 
    // to last till null 
    void printList() 
    { 

        Node* node = this; 

        while (node != NULL) { 

            cout << node->data; 
            node = node->next; 
        } 

        cout << endl; 
    } 
}; 

// Function to add a node 
// at the beginning of List 
void push(Node** head_ref, int new_data) 
{ 

    // allocate node 
    (*head_ref) = new Node(new_data, *head_ref); 
} 

void swap(Node*& a, Node*& b) 
{ 

    Node* temp = a; 
    a = b; 
    b = temp; 
} 

void swapNodes(Node** head_ref, int x, int y) 
{ 

    // Nothing to do if x and y are same 
    if (x == y) 
        return; 

    Node **a = NULL, **b = NULL; 

    // search for x and y in the linked list 
    // and store therir pointer in a and b 
    while (*head_ref) { 

        if ((*head_ref)->data == x) { 
            a = head_ref; 
        } 

        else if ((*head_ref)->data == y) { 
            b = head_ref; 
        } 

        head_ref = &((*head_ref)->next); 
    } 

    // if we have found both a and b 
    // in the linked list swap current 
    // pointer and next pointer of these 
    if (a && b) { 

        swap(*a, *b); 
        swap(((*a)->next), ((*b)->next)); 
    } 
} 

// Driver code 
int main() 
{ 

    Node* start = NULL; 

    // The constructed linked list is: 
    // 1->2->3->4->5->6->7 
    push(&start, 7); 
    push(&start, 6); 
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 

    cout << "Linked list before calling swapNodes() "; 
    start->printList(); 

    swapNodes(&start, 6, 3); 

    cout << "Linked list after calling swapNodes() "; 
    start->printList(); 
} 

```

## Java

```java

// Java program to swap two given nodes of a linked list 
class Soluiton 
{ 
// A linked list node class  
static class Node {  

    int data;  
    Node next;  

    // constructor  
    Node(int val, Node next1)  
    {   
        data=val; next=next1; 
    }  

    // print list from this  
    // to last till null  
    void printList()  
    {  

        Node node = this;  

        while (node != null) {  

            System.out.print(node.data+" ");  
            node = node.next;  
        }  
        System.out.println();  
    }  
} 

// Function to add a node  
// at the beginning of List  
static Node push(Node head_ref, int new_data)  
{  

    // allocate node  
    (head_ref) = new Node(new_data, head_ref); 
    return head_ref; 
}  

static Node swapNodes(Node head_ref, int x, int y)  
{  
    Node head=head_ref; 
    // Nothing to do if x and y are same  
    if (x == y)  
        return null;  

    Node a = null, b = null;  

    // search for x and y in the linked list  
    // and store therir pointer in a and b  
    while (head_ref.next!=null) {  

        if ((head_ref.next).data == x) {  
            a = head_ref;  
        }  

        else if ((head_ref.next).data == y) {  
            b = head_ref;  
        }  

        head_ref = ((head_ref).next);  
    }  

    // if we have found both a and b  
    // in the linked list swap current  
    // pointer and next pointer of these  
    if (a!=null&&  b!=null) {  
    Node temp = a.next;  
    a.next = b.next;  
    b.next = temp;      
    temp = a.next.next;  
    a.next.next = b.next.next;  
    b.next.next = temp;  
    }  
    return head; 
}  

//Driver code 
public static void main(String args[]) 
{  

    Node start = null;  

    // The constructed linked list is:  
    // 1.2.3.4.5.6.7  
    start=push(start, 7);  
    start=push(start, 6);  
    start=push(start, 5);  
    start=push(start, 4);  
    start=push(start, 3);  
    start=push(start, 2);  
    start=push(start, 1);  

    System.out.print("Linked list before calling swapNodes() ");  
    start.printList();  

    start=swapNodes(start, 6, 3);  

    System.out.print("Linked list after calling swapNodes() ");  
    start.printList();  
}  
} 
//contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to swap two given  
# nodes of a linked list 

# A linked list node class  
class Node : 

    # constructor  
    def __init__(self, val = None, next1 = None):  
        self.data = val  
        self.next = next1 

    # print list from this  
    # to last till None  
    def printList(self):  

        node = self

        while (node != None) : 
            print(node.data, end = " ")  
            node = node.next
        print(" ") 

# Function to add a node  
# at the beginning of List  
def push(head_ref, new_data) : 

    # allocate node  
    (head_ref) = Node(new_data, head_ref) 
    return head_ref 

def swapNodes(head_ref, x, y) : 
    head = head_ref 

    # Nothing to do if x and y are same  
    if (x == y) : 
        return None

    a = None
    b = None

    # search for x and y in the linked list  
    # and store therir pointer in a and b  
    while (head_ref.next != None) : 

        if ((head_ref.next).data == x) : 
            a = head_ref  

        elif ((head_ref.next).data == y) : 
            b = head_ref  

        head_ref = ((head_ref).next)  

    # if we have found both a and b  
    # in the linked list swap current  
    # pointer and next pointer of these  
    if (a != None and b != None) : 
        temp = a.next
        a.next = b.next
        b.next = temp      
        temp = a.next.next
        a.next.next = b.next.next
        b.next.next = temp  

    return head 

# Driver code 

start = None

# The constructed linked list is:  
# 1.2.3.4.5.6.7  
start = push(start, 7)  
start = push(start, 6)  
start = push(start, 5)  
start = push(start, 4)  
start = push(start, 3)  
start = push(start, 2)  
start = push(start, 1)  

print("Linked list before calling swapNodes() ")  
start.printList()  

start=swapNodes(start, 6, 3)  

print("Linked list after calling swapNodes() ")  
start.printList()  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to swap two  
// given nodes of a linked list 
using System; 

class GFG 
{ 
    // A linked list node class  
    public class Node  
    {  

        public int data;  
        public Node next;  

        // constructor  
        public Node(int val, Node next1)  
        {  
            data = val; next = next1; 
        }  

        // print list from this  
        // to last till null  
        public void printList()  
        {  

            Node node = this;  

            while (node != null)  
            {  
                Console.Write(node.data+" ");  
                node = node.next;  
            }  
            Console.WriteLine();  
        }  
    } 

    // Function to add a node  
    // at the beginning of List  
    static Node push(Node head_ref, int new_data)  
    {  

        // allocate node  
        (head_ref) = new Node(new_data, head_ref); 
        return head_ref; 
    }  

    static Node swapNodes(Node head_ref, int x, int y)  
    {  
        Node head=head_ref; 

        // Nothing to do if x and y are same  
        if (x == y)  
            return null;  

        Node a = null, b = null;  

        // search for x and y in the linked list  
        // and store therir pointer in a and b  
        while (head_ref.next!=null)  
        {  

            if ((head_ref.next).data == x)  
            {  
                a = head_ref;  
            }  

            else if ((head_ref.next).data == y) 
            {  
                b = head_ref;  
            }  

            head_ref = ((head_ref).next);  
        }  

        // if we have found both a and b  
        // in the linked list swap current  
        // pointer and next pointer of these  
        if (a != null && b != null)  
        {  
        Node temp = a.next;  
        a.next = b.next;  
        b.next = temp;      
        temp = a.next.next;  
        a.next.next = b.next.next;  
        b.next.next = temp;  
        }  
        return head; 
    }  

    // Driver code 
    public static void Main() 
    {  

        Node start = null;  

        // The constructed linked list is:  
        // 1.2.3.4.5.6.7  
        start=push(start, 7);  
        start=push(start, 6);  
        start=push(start, 5);  
        start=push(start, 4);  
        start=push(start, 3);  
        start=push(start, 2);  
        start=push(start, 1);  

        Console.Write("Linked list before calling swapNodes() ");  
        start.printList();  

        start=swapNodes(start, 6, 3);  

        Console.Write("Linked list after calling swapNodes() ");  
        start.printList();  
    }  
} 

/* This code contributed by PrinciRaj1992 */

```

**输出：**

```
 Linked list before calling swapNodes() 1 2 3 4 5 6 7
 Linked list after calling swapNodes() 1 2 6 4 5 3 7

```

本文由 **Gautam** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

