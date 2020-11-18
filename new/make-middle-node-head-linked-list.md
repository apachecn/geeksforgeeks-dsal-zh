# 将中间节点放在链接列表中

> 原文：[https://www.geeksforgeeks.org/make-middle-node-head-linked-list/](https://www.geeksforgeeks.org/make-middle-node-head-linked-list/)

给定一个单链表，找到链表的中间，并在链表的开头设置链表的中间节点。

**示例**：

```
Input  : 1 2 3 4 5 
Output : 3 1 2 4 5

Input  : 1 2 3 4 5 6
Output : 4 1 2 3 5 6 

```

![https://media.geeksforgeeks.org/wp-content/uploads/Capturedsdw.png](img/ebf5846858a076c34e437c9fea2d3986.png)

这个想法是首先[使用两个指针](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)找到一个链表的中间，第一个指针一次移动一个，第二个指针一次移动两个。 当第二个指针到达终点时，第一个指针到达中间。 我们还跟踪第一个指针的前一个，以便我们可以从中间节点的当前位置删除中间节点并使它成为头部。

## C++

```cpp

// C++ program to make middle node as head of  
// linked list.  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Function to get the middle and set at  
beginning of the linked list*/
void setMiddleHead(Node** head)  
{  
    if (*head == NULL)  
        return;  

    // To traverse list nodes one by one  
    Node* one_node = (*head);  

    // To traverse list nodes by skipping  
    // one.  
    Node* two_node = (*head);  

    // To keep track of previous of middle  
    Node* prev = NULL;  
    while (two_node != NULL && two_node->next != NULL)  
    {  

        /* for previous node of middle node */
        prev = one_node;  

        /* move one node each time*/
        two_node = two_node->next->next;  

        /* move two node each time*/
        one_node = one_node->next;  
    }  

    /* set middle node at head */
    prev->next = prev->next->next;  
    one_node->next = (*head);  
    (*head) = one_node;  
}  

// To insert a node at the beginning of linked  
// list.  
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node = new Node();  

    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

// A function to print a given linked list  
void printList(Node* ptr)  
{  
    while (ptr != NULL) 
    {  
        cout << ptr->data << " ";  
        ptr = ptr->next;  
    }  
    cout<<endl;  
}  

/* Driver code*/
int main()  
{  
    // Create a list of 5 nodes  
    Node* head = NULL;  
    int i;  
    for (i = 5; i > 0; i--)  
        push(&head, i);  

    cout << " list before: ";  
    printList(head);  

    setMiddleHead(&head);  

    cout << " list After: ";  
    printList(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to make middle node as head of 
// linked list. 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the middle and set at 
   beginning of the linked list*/
void setMiddleHead(struct Node** head) 
{ 
    if (*head == NULL) 
        return; 

    // To traverse list nodes one by one 
    struct Node* one_node = (*head); 

    // To traverse list nodes by skipping 
    // one. 
    struct Node* two_node = (*head); 

    // To keep track of previous of middle 
    struct Node* prev = NULL; 
    while (two_node != NULL && two_node->next != NULL) { 

        /* for previous node of middle node */
        prev = one_node; 

        /* move one node each time*/
        two_node = two_node->next->next; 

        /* move two node each time*/
        one_node = one_node->next; 
    } 

    /* set middle node at head */
    prev->next = prev->next->next; 
    one_node->next = (*head); 
    (*head) = one_node; 
} 

// To insert a node at the beginning of linked 
// list. 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*)malloc(sizeof(struct Node)); 

    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// A  function to print a given linked list 
void printList(struct Node* ptr) 
{ 
    while (ptr != NULL) { 
        printf("%d ", ptr->data); 
        ptr = ptr->next; 
    } 
    printf("\n"); 
} 

/* Driver function*/
int main() 
{ 
    // Create a list of 5 nodes 
    struct Node* head = NULL; 
    int i; 
    for (i = 5; i > 0; i--) 
        push(&head, i); 

    printf(" list before: "); 
    printList(head); 

    setMiddleHead(&head); 

    printf(" list After:  "); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to make middle node  
// as head of Linked list 
public class GFG  
{      
    /* Link list node */
    static class Node { 
        int data; 
        Node next; 
        Node(int data){ 
            this.data = data; 
            next = null; 
        } 
    } 

    static Node head; 

    /* Function to get the middle and  
    set at beginning of the linked list*/
    static void setMiddleHead() 
    { 
        if (head == null) 
            return; 

        // To traverse list nodes one  
        // by one 
        Node one_node = head; 

        // To traverse list nodes by  
        // skipping one. 
        Node two_node = head; 

        // To keep track of previous of middle 
        Node prev = null; 
        while (two_node != null &&  
               two_node.next != null) { 

            /* for previous node of middle node */
            prev = one_node; 

            /* move one node each time*/
            two_node = two_node.next.next; 

            /* move two node each time*/
            one_node = one_node.next; 
        } 

        /* set middle node at head */
        prev.next = prev.next.next; 
        one_node.next = head; 
        head = one_node; 
    } 

    // To insert a node at the beginning of 
    // linked list. 
    static void push(int new_data) 
    { 
        /* allocate node */
        Node new_node = new Node(new_data); 

        /* link the old list off the new node */
        new_node.next = head; 

        /* move the head to point to the new node */
        head = new_node; 
    } 

    // A  function to print a given linked list 
    static void printList(Node ptr) 
    { 
        while (ptr != null) { 
            System.out.print(ptr.data+" "); 
            ptr = ptr.next; 
        } 
        System.out.println(); 
    } 

    /* Driver function*/
    public static void main(String args[]) 
    { 
        // Create a list of 5 nodes 
        head = null; 
        int i; 
        for (i = 5; i > 0; i--) 
            push(i); 

        System.out.print(" list before: "); 
        printList(head); 

        setMiddleHead(); 

        System.out.print(" list After:  "); 
        printList(head); 

    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

# Python3 program to make middle node 
# as head of Linked list 

# Linked List node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# function to get the middle node 
# set it as the beginning of the  
# linked list 
def setMiddleHead(head): 
    if(head == None): 
        return None

    # to traverse nodes  
    # one by one 
    one_node = head 

    # to traverse nodes by  
    # skipping one 
    two_node = head 

    # to keep track of previous middle 
    prev = None

    while(two_node != None and
          two_node.next != None): 

        # for previous node of middle node 
        prev = one_node 

        # move one node each time 
        one_node = one_node.next

        # move two nodes each time 
        two_node = two_node.next.next

    # set middle node at head 
    prev.next = prev.next.next
    one_node.next = head 
    head = one_node 

    # return the modified head 
    return head 

def push(head, new_data): 

    # allocate new node 
    new_node = Node(new_data) 

    #link the old list to new node 
    new_node.next = head 

    # move the head to point the new node 
    head = new_node 

    # return the modified head 
    return head 

# A function to print a given linked list 
def printList(head): 
    temp = head 
    while (temp!=None): 

        print(str(temp.data), end = " ") 
        temp = temp.next
    print("") 

# Create a list of 5 nodes 
head = None
for i in range(5, 0, -1): 
    head = push(head, i) 

print(" list before: ", end = "") 
printList(head) 

head = setMiddleHead(head) 

print(" list After: ", end = "") 
printList(head) 

# This code is contributed 
# by Pranav Devarakonda 

```

## C#

```cs

// C# program to make middle node  
// as head of Linked list 
using System; 

public class GFG  
{      
    /* Link list node */
    class Node  
    { 
        public int data; 
        public Node next; 
        public Node(int data) 
        { 
            this.data = data; 
            next = null; 
        } 
    } 

    static Node head; 

    /* Function to get the middle and  
    set at beginning of the linked list*/
    static void setMiddleHead() 
    { 
        if (head == null) 
            return; 

        // To traverse list nodes one  
        // by one 
        Node one_node = head; 

        // To traverse list nodes by  
        // skipping one. 
        Node two_node = head; 

        // To keep track of previous of middle 
        Node prev = null; 
        while (two_node != null &&  
            two_node.next != null)  
        { 

            /* for previous node of middle node */
            prev = one_node; 

            /* move one node each time*/
            two_node = two_node.next.next; 

            /* move two node each time*/
            one_node = one_node.next; 
        } 

        /* set middle node at head */
        prev.next = prev.next.next; 
        one_node.next = head; 
        head = one_node; 
    } 

    // To insert a node at the beginning of 
    // linked list. 
    static void push(int new_data) 
    { 
        /* allocate node */
        Node new_node = new Node(new_data); 

        /* link the old list off the new node */
        new_node.next = head; 

        /* move the head to point to the new node */
        head = new_node; 
    } 

    // A function to print a given linked list 
    static void printList(Node ptr) 
    { 
        while (ptr != null) { 
            Console.Write(ptr.data + " "); 
            ptr = ptr.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code*/
    public static void Main(String []args) 
    { 
        // Create a list of 5 nodes 
        head = null; 
        int i; 
        for (i = 5; i > 0; i--) 
            push(i); 

        Console.Write(" list before: "); 
        printList(head); 

        setMiddleHead(); 

        Console.Write(" list After: "); 
        printList(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
list before: 1 2 3 4 5
list After : 3 1 2 4 5 

```

本文由 **R_Raj** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

