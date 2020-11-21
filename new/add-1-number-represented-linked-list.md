# 将链表表示的数字加 1

> 原文：[https://www.geeksforgeeks.org/add-1-number-represented-linked-list/](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)

数字在链表中表示，因此每个数字都对应于链表中的一个节点。 加 1。 例如，1999 表示为（`1 -> 9 -> 9 -> 9`），将其添加 1 应该将其更改为（`2 -> 0 -> 0 -> 0`）

步骤如下：

1.  反转给定的链表。 例如，将`1 -> 9 -> 9 -> 9`转换为`9 -> 9 -> 9 -> 1`。

2.  从最左边的节点开始遍历链表，并向其添加 1。 如果有进位，请移至下一个节点。 有进位时继续移动到下一个节点。

3.  反向修改链表和返回头。

下面是上述步骤的实现。

## C++

```cpp

// C++ program to add 1 to a linked list  
#include <bits/stdc++.h> 
using namespace std; 

/* Linked list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Function to create a new node with given data */
Node *newNode(int data)  
{  
    Node *new_node = new Node;  
    new_node->data = data;  
    new_node->next = NULL;  
    return new_node;  
}  

/* Function to reverse the linked list */
Node *reverse(Node *head)  
{  
    Node * prev = NULL;  
    Node * current = head;  
    Node * next;  
    while (current != NULL)  
    {  
        next = current->next;  
        current->next = prev;  
        prev = current;  
        current = next;  
    }  
    return prev;  
}  

/* Adds one to a linked lists and return the head  
node of resultant list */
Node *addOneUtil(Node *head)  
{  
    // res is head node of the resultant list  
    Node* res = head;  
    Node *temp, *prev = NULL;  

    int carry = 1, sum;  

    while (head != NULL) //while both lists exist  
    {  
        // Calculate value of next digit in resultant list.  
        // The next digit is sum of following things  
        // (i) Carry  
        // (ii) Next digit of head list (if there is a  
        // next digit)  
        sum = carry + head->data;  

        // update carry for next calulation  
        carry = (sum >= 10)? 1 : 0;  

        // update sum if it is greater than 10  
        sum = sum % 10;  

        // Create a new node with sum as data  
        head->data = sum;  

        // Move head and second pointers to next nodes  
        temp = head;  
        head = head->next;  
    }  

    // if some carry is still there, add a new node to  
    // result list.  
    if (carry > 0)  
        temp->next = newNode(carry);  

    // return head of the resultant list  
    return res;  
}  

// This function mainly uses addOneUtil().  
Node* addOne(Node *head)  
{  
    // Reverse linked list  
    head = reverse(head);  

    // Add one from left to right of reversed  
    // list  
    head = addOneUtil(head);  

    // Reverse the modified list  
    return reverse(head);  
}  

// A utility function to print a linked list  
void printList(Node *node)  
{  
    while (node != NULL)  
    {  
        cout << node->data;  
        node = node->next;  
    }  
    cout<<endl; 
}  

/* Driver program to test above function */
int main(void)  
{  
    Node *head = newNode(1);  
    head->next = newNode(9);  
    head->next->next = newNode(9);  
    head->next->next->next = newNode(9);  

    cout << "List is ";  
    printList(head);  

    head = addOne(head);  

    cout << "\nResultant list is ";  
    printList(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to add 1 to a linked list 
#include<bits/stdc++.h> 

/* Linked list node */
struct Node 
{ 
    int data; 
    Node* next; 
}; 

/* Function to create a new node with given data */
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

/* Function to reverse the linked list */
Node *reverse(Node *head) 
{ 
    Node * prev   = NULL; 
    Node * current = head; 
    Node * next; 
    while (current != NULL) 
    { 
        next  = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 
    return prev; 
} 

/* Adds one to a linked lists and return the head 
   node of resultant list */
Node *addOneUtil(Node *head) 
{ 
    // res is head node of the resultant list 
    Node* res = head; 
    Node *temp, *prev = NULL; 

    int carry = 1, sum; 

    while (head != NULL) //while both lists exist 
    { 
        // Calculate value of next digit in resultant list. 
        // The next digit is sum of following things 
        // (i) Carry 
        // (ii) Next digit of head list (if there is a 
        //     next digit) 
        sum = carry + head->data; 

        // update carry for next calulation 
        carry = (sum >= 10)? 1 : 0; 

        // update sum if it is greater than 10 
        sum = sum % 10; 

        // Create a new node with sum as data 
        head->data = sum; 

        // Move head and second pointers to next nodes 
        temp = head; 
        head = head->next; 
    } 

    // if some carry is still there, add a new node to 
    // result list. 
    if (carry > 0) 
        temp->next = newNode(carry); 

    // return head of the resultant list 
    return res; 
} 

// This function mainly uses addOneUtil(). 
Node* addOne(Node *head) 
{ 
    // Reverse linked list 
    head = reverse(head); 

    // Add one from left to right of reversed 
    // list 
    head = addOneUtil(head); 

    // Reverse the modified list 
    return reverse(head); 
} 

// A utility function to print a linked list 
void printList(Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d", node->data); 
        node = node->next; 
    } 
    printf("\n"); 
} 

/* Driver program to test above function */
int main(void) 
{ 
    Node *head = newNode(1); 
    head->next = newNode(9); 
    head->next->next = newNode(9); 
    head->next->next->next = newNode(9); 

    printf("List is "); 
    printList(head); 

    head = addOne(head); 

    printf("\nResultant list is "); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to add 1 to a linked list  
class GfG  
{ 

/* Linked list node */
static class Node  
{  
    int data;  
    Node next;  
} 

/* Function to create a new node with given data */
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

/* Function to reverse the linked list */
static Node reverse(Node head)  
{  
    Node prev = null;  
    Node current = head;  
    Node next = null;  
    while (current != null)  
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
    }  
    return prev;  
}  

/* Adds one to a linked lists and return the head  
node of resultant list */
static Node addOneUtil(Node head)  
{  
    // res is head node of the resultant list  
    Node res = head;  
    Node temp = null, prev = null;  

    int carry = 1, sum;  

    while (head != null) //while both lists exist  
    {  
        // Calculate value of next digit in resultant list.  
        // The next digit is sum of following things  
        // (i) Carry  
        // (ii) Next digit of head list (if there is a  
        // next digit)  
        sum = carry + head.data;  

        // update carry for next calulation  
        carry = (sum >= 10)? 1 : 0;  

        // update sum if it is greater than 10  
        sum = sum % 10;  

        // Create a new node with sum as data  
        head.data = sum;  

        // Move head and second pointers to next nodes  
        temp = head;  
        head = head.next;  
    }  

    // if some carry is still there, add a new node to  
    // result list.  
    if (carry > 0)  
        temp.next = newNode(carry);  

    // return head of the resultant list  
    return res;  
}  

// This function mainly uses addOneUtil().  
static Node addOne(Node head)  
{  
    // Reverse linked list  
    head = reverse(head);  

    // Add one from left to right of reversed  
    // list  
    head = addOneUtil(head);  

    // Reverse the modified list  
    return reverse(head);  
}  

// A utility function to print a linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data);  
        node = node.next;  
    }  
    System.out.println();  
}  

/* Driver code */
public static void main(String[] args)  
{  
    Node head = newNode(1);  
    head.next = newNode(9);  
    head.next.next = newNode(9);  
    head.next.next.next = newNode(9);  

    System.out.print("List is ");  
    printList(head);  

    head = addOne(head);  
    System.out.println(); 
    System.out.print("Resultant list is ");  
    printList(head);  
} 
}  

// This code is contributed by prerna saini 

```

## Python3

```py

# Python3 program to add 1 to a linked list  
import sys 
import math 

# Linked list node 
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Function to create a new node with given data */ 
def newNode(data): 
    return Node(data) 

# Function to reverse the linked list */ 
def reverseList(head): 
    if not head: 
        return
    curNode = head 
    prevNode = head 
    nextNode = head.next
    curNode.next = None

    while(nextNode): 
        curNode = nextNode 
        nextNode = nextNode.next
        curNode.next = prevNode 
        prevNode = curNode 

    return curNode 

# Adds one to a linked lists and return the head  
#node of resultant list 
def addOne(head): 

    # Reverse linked list  
    head = reverseList(head) 
    temp = head 
    carry = 1
    while(temp): 
        temp.data += carry 
        if temp.data % 10 == 0: 
            # update carry for next calulation  
            carry = 1
            temp.data = 0
        else: 
            # update carry for next calulation  
            carry = 0
        temp = temp.next

    # Reverse the modified list              
    return reverseList(head) 

# A utility function to print a linked list  
def printList(head): 
    if not head: 
        return
    while(head): 
        print("{}".format(head.data),end="") 
        head=head.next

# Driver code 
if __name__=='__main__': 
    head = newNode(1) 
    head.next = newNode(9) 
    head.next.next = newNode(9) 
    head.next.next.next = newNode(9) 

    print("List is: ",end = "") 
    printList(head) 

    head = addOne(head) 

    print("\nResultant list is: ",end="") 
    printList(head) 

# This code is contributed by Vikash Kumar 37 

```

## C#

```cs

// C# program to add 1 to a linked list 
using System; 

class GfG  
{ 

/* Linked list node */
public class Node  
{  
    public int data;  
    public Node next;  
} 

/* Function to create a new node with given data */
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

/* Function to reverse the linked list */
static Node reverse(Node head)  
{  
    Node prev = null;  
    Node current = head;  
    Node next = null;  
    while (current != null)  
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
    }  
    return prev;  
}  

/* Adds one to a linked lists and return the head  
node of resultant list */
static Node addOneUtil(Node head)  
{  
    // res is head node of the resultant list  
    Node res = head;  
    Node temp = null, prev = null;  

    int carry = 1, sum;  

    while (head != null) //while both lists exist  
    {  
        // Calculate value of next digit in resultant list.  
        // The next digit is sum of following things  
        // (i) Carry  
        // (ii) Next digit of head list (if there is a  
        // next digit)  
        sum = carry + head.data;  

        // update carry for next calulation  
        carry = (sum >= 10)? 1 : 0;  

        // update sum if it is greater than 10  
        sum = sum % 10;  

        // Create a new node with sum as data  
        head.data = sum;  

        // Move head and second pointers to next nodes  
        temp = head;  
        head = head.next;  
    }  

    // if some carry is still there, add a new node to  
    // result list.  
    if (carry > 0)  
        temp.next = newNode(carry);  

    // return head of the resultant list  
    return res;  
}  

// This function mainly uses addOneUtil().  
static Node addOne(Node head)  
{  
    // Reverse linked list  
    head = reverse(head);  

    // Add one from left to right of reversed  
    // list  
    head = addOneUtil(head);  

    // Reverse the modified list  
    return reverse(head);  
}  

// A utility function to print a linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(node.data);  
        node = node.next;  
    }  
    Console.WriteLine();  
}  

/* Driver code */
public static void Main(String[] args)  
{  
    Node head = newNode(1);  
    head.next = newNode(9);  
    head.next.next = newNode(9);  
    head.next.next.next = newNode(9);  

    Console.Write("List is ");  
    printList(head);  

    head = addOne(head);  
    Console.WriteLine(); 
    Console.Write("Resultant list is ");  
    printList(head);  
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
List is 1999

Resultant list is 2000
```

**递归实现**：

我们可以递归地到达最后一个节点，并向前进位到先前的节点。 递归解决方案不需要反向链表。 我们还可以使用栈代替递归来临时保存节点。

下面是递归解决方案的实现。

## C++

```cpp

// Recursive C++ program to add 1 to a linked list 
#include<bits/stdc++.h> 

/* Linked list node */
struct Node 
{ 
    int data; 
    Node* next; 
}; 

/* Function to create a new node with given data */
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Recursively add 1 from end to beginning and returns 
// carry after all nodes are processed. 
int addWithCarry(Node *head) 
{ 
    // If linked list is empty, then 
    // return carry 
    if (head == NULL) 
        return 1; 

    // Add carry returned be next node call 
    int res = head->data + addWithCarry(head->next); 

    // Update data and return new carry 
    head->data = (res) % 10; 
    return (res) / 10; 
} 

// This function mainly uses addWithCarry(). 
Node* addOne(Node *head) 
{ 
    // Add 1 to linked list from end to beginning 
    int carry = addWithCarry(head); 

    // If there is carry after processing all nodes, 
    // then we need to add a new node to linked list 
    if (carry) 
    { 
        Node *newNode = new Node; 
        newNode->data = carry; 
        newNode->next = head; 
        return newNode; // New node becomes head now 
    } 

    return head; 
} 

// A utility function to print a linked list 
void printList(Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d", node->data); 
        node = node->next; 
    } 
    printf("\n"); 
} 

/* Driver program to test above function */
int main(void) 
{ 
    Node *head = newNode(1); 
    head->next = newNode(9); 
    head->next->next = newNode(9); 
    head->next->next->next = newNode(9); 

    printf("List is "); 
    printList(head); 

    head = addOne(head); 

    printf("\nResultant list is "); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Recursive Java program to add 1 to a linked list 
class GfG { 

    /* Linked list node */
    static class Node 
    { 
        int data; 
        Node next; 
    } 

    /* Function to create a new node with given data */
    static Node newNode(int data)  
    { 
        Node new_node = new Node(); 
        new_node.data = data; 
        new_node.next = null; 
        return new_node; 
    } 

    // Recursively add 1 from end to beginning and returns 
    // carry after all nodes are processed. 
    static int addWithCarry(Node head) 
    { 

        // If linked list is empty, then 
        // return carry 
        if (head == null) 
            return 1; 

        // Add carry returned be next node call 
        int res = head.data + addWithCarry(head.next); 

        // Update data and return new carry 
        head.data = (res) % 10; 
        return (res) / 10; 
    } 

    // This function mainly uses addWithCarry().  
    static Node addOne(Node head) 
    { 

        // Add 1 to linked list from end to beginning 
        int carry = addWithCarry(head); 

        // If there is carry after processing all nodes, 
        // then we need to add a new node to linked list 
        if (carry > 0) 
        { 
            Node newNode = newNode(carry); 
            newNode.next = head; 
            return newNode; // New node becomes head now 
        } 

        return head; 
    } 

    // A utility function to print a linked list 
    static void printList(Node node) 
    { 
        while (node != null) 
        { 
            System.out.print(node.data); 
            node = node.next; 
        } 
        System.out.println(); 
    } 

    /* Driver code */
    public static void main(String[] args) 
    { 
        Node head = newNode(1); 
        head.next = newNode(9); 
        head.next.next = newNode(9); 
        head.next.next.next = newNode(9); 

        System.out.print("List is "); 
        printList(head); 

        head = addOne(head); 
        System.out.println(); 
        System.out.print("Resultant list is "); 
        printList(head); 
    } 
} 

// This code is contributed by shubham96301 

```

## Python

```py

# Recursive Python program to add 1 to a linked list 

# Node class  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to create a new node with given data  
def newNode(data): 

    new_node = Node(0) 
    new_node.data = data 
    new_node.next = None
    return new_node 

# Recursively add 1 from end to beginning and returns 
# carry after all nodes are processed. 
def addWithCarry(head): 

    # If linked list is empty, then 
    # return carry 
    if (head == None): 
        return 1

    # Add carry returned be next node call 
    res = head.data + addWithCarry(head.next) 

    # Update data and return new carry 
    head.data = int((res) % 10) 
    return int((res) / 10) 

# This function mainly uses addWithCarry(). 
def addOne(head): 

    # Add 1 to linked list from end to beginning 
    carry = addWithCarry(head) 

    # If there is carry after processing all nodes, 
    # then we need to add a new node to linked list 
    if (carry != 0): 

        newNode = Node(0) 
        newNode.data = carry 
        newNode.next = head 
        return newNode # New node becomes head now 

    return head 

# A utility function to print a linked list 
def printList(node): 

    while (node != None): 

        print( node.data,end = "") 
        node = node.next

    print("\n") 

# Driver program to test above function  

head = newNode(1) 
head.next = newNode(9) 
head.next.next = newNode(9) 
head.next.next.next = newNode(9) 

print("List is ") 
printList(head) 

head = addOne(head) 

print("\nResultant list is ") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// Recursive C# program to add 1 to a linked list  
using System;  

class GfG  
{  

    /* Linked list node */
    public class Node  
    {  
        public int data;  
        public Node next;  
    }  

    /* Function to create a new node with given data */
    public static Node newNode(int data)  
    {  
        Node new_node = new Node();  
        new_node.data = data;  
        new_node.next = null;  
        return new_node;  
    }  

    // Recursively add 1 from end to beginning and returns  
    // carry after all nodes are processed.  
    public static int addWithCarry(Node head)  
    {  

        // If linked list is empty, then  
        // return carry  
        if (head == null)  
            return 1;  

        // Add carry returned be next node call  
        int res = head.data + addWithCarry(head.next);  

        // Update data and return new carry  
        head.data = (res) % 10;  
        return (res) / 10;  
    }  

    // This function mainly uses addWithCarry().  
    public static Node addOne(Node head)  
    {  

        // Add 1 to linked list from end to beginning  
        int carry = addWithCarry(head);  
        Node newNodes = null; 

        // If there is carry after processing all nodes,  
        // then we need to add a new node to linked list  
        if (carry > 0)  
        {  
            newNodes = newNode(carry);  
            newNodes.next = head;  
            return newNodes; // New node becomes head now  
        }  

        return head;  
    }  

    // A utility function to print a linked list  
    public static void printList(Node node)  
    {  
        while (node != null)  
        {  
            Console.Write(node.data);  
            node = node.next;  
        }  
        Console.WriteLine();  
    }  

    /* Driver code */
    public static void Main(String[] args)  
    {  
        Node head = newNode(1);  
        head.next = newNode(9);  
        head.next.next = newNode(9);  
        head.next.next.next = newNode(9);  

        Console.Write("List is ");  
        printList(head);  

        head = addOne(head);  
        Console.WriteLine();  
        Console.Write("Resultant list is ");  
        printList(head);  
    }  
}  

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
List is 1999

Resultant list is 2000
```

本文由 **Aditya Goel** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

