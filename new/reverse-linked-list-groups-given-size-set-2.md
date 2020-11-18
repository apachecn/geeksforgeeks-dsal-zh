# 以给定大小的组反向链接列表| 设置 2

给定一个链表，编写一个函数以反转每 k 个节点（其中 k 是该函数的输入）。

**示例：**

```
Inputs:  1->2->3->4->5->6->7->8->NULL and k = 3 
Output:  3->2->1->6->5->4->8->7->NULL. 

Inputs:   1->2->3->4->5->6->7->8->NULL and k = 5
Output:  5->4->3->2->1->8->7->6->NULL.

```

我们已经在下面的

[中按给定大小的组反向链接列表了。 设置 1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)

在本文中，我们使用了一个堆栈，该堆栈将存储给定链接列表的节点。 首先，将链接列表的 k 个元素压入堆栈。 现在一一弹出元素，并跟踪先前弹出的节点。 将上一个节点的下一个指针指向堆栈的顶部元素。 重复此过程，直到达到 NULL。

该算法使用 O（k）额外空间。

## C++

```cpp

// C++ program to reverse a linked list in groups 
// of given size 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Reverses the linked list in groups of size k 
   and returns the pointer to the new head node. */
struct Node* Reverse(struct Node* head, int k) 
{ 
    // Create a stack of Node* 
    stack<Node*> mystack; 
    struct Node* current = head; 
    struct Node* prev = NULL; 

    while (current != NULL) { 

        // Terminate the loop whichever comes first 
        // either current == NULL or count >= k 
        int count = 0; 
        while (current != NULL && count < k) { 
            mystack.push(current); 
            current = current->next; 
            count++; 
        } 

        // Now pop the elements of stack one by one 
        while (mystack.size() > 0) { 

            // If final list has not been started yet. 
            if (prev == NULL) { 
                prev = mystack.top(); 
                head = prev; 
                mystack.pop(); 
            } else { 
                prev->next = mystack.top(); 
                prev = prev->next; 
                mystack.pop(); 
            } 
        } 
    } 

    // Next of last element will point to NULL. 
    prev->next = NULL; 

    return head; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node =  
          (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d  ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Created Linked list is 1->2->3->4->5->6->7->8->9 */
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    printf("\nGiven linked list \n"); 
    printList(head); 
    head = Reverse(head, 3); 

    printf("\nReversed Linked list \n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to reverse a linked list in groups  
// of given size  
import java.util.*; 
class GfG  
{ 

/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
} 
static Node head = null; 

/* Reverses the linked list in groups of size k  
and returns the pointer to the new head node. */
static Node Reverse(Node head, int k)  
{  
    // Create a stack of Node*  
    Stack<Node> mystack = new Stack<Node> ();  
    Node current = head;  
    Node prev = null;  

    while (current != null) 
    {  

        // Terminate the loop whichever comes first  
        // either current == NULL or count >= k  
        int count = 0;  
        while (current != null && count < k) 
        {  
            mystack.push(current);  
            current = current.next;  
            count++;  
        }  

        // Now pop the elements of stack one by one  
        while (mystack.size() > 0)  
        {  

            // If final list has not been started yet.  
            if (prev == null) 
            {  
                prev = mystack.peek();  
                head = prev;  
                mystack.pop();  
            }  
            else
            {  
                prev.next = mystack.peek();  
                prev = prev.next;  
                mystack.pop();  
            }  
        }  
    }  

    // Next of last element will point to NULL.  
    prev.next = null;  

    return head;  
}  

/* UTILITY FUNCTIONS */
/* Function to push a node */
static void push( int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list off the new node */
    new_node.next = head;  

    /* move the head to point to the new node */
    head = new_node;  
}  

/* Function to print linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data + " ");  
        node = node.next;  
    }  
}  

/* Driver code*/
public static void main(String[] args)  
{  
    /* Start with the empty list */
    //Node head = null;  

    /* Created Linked list is 1->2->3-> 
    4->5->6->7->8->9 */
    push( 9);  
    push( 8);  
    push( 7);  
    push( 6);  
    push( 5);  
    push(4);  
    push(3);  
    push(2);  
    push( 1);  

    System.out.println("Given linked list ");  
    printList(head);  
    head = Reverse(head, 3); 
    System.out.println(); 

    System.out.println("Reversed Linked list ");  
    printList(head);  
}  
}  

// This code is contributed by Prerna Saini 

```

## Python3

```py

# Python3 program to reverse a Linked List 
# in groups of given size 

# Node class 
class Node(object): 
    __slots__ = 'data', 'next'

    # Constructor to initialize the node object 
    def __init__(self, data = None, next = None): 
        self.data = data 
        self.next = next

    def __repr__(self): 
        return repr(self.data) 

class LinkedList(object): 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Utility function to print nodes  
    # of LinkedList 
    def __repr__(self): 
        nodes = [] 
        curr = self.head 
        while curr: 
            nodes.append(repr(curr)) 
            curr = curr.next
        return '[' + ', '.join(nodes) + ']'

    # Function to insert a new node at 
    # the beginning 
    def prepend(self, data): 
        self.head = Node(data = data, 
                         next = self.head) 

    # Reverses the linked list in groups of size k 
    # and returns the pointer to the new head node. 
    def reverse(self, k = 1): 
        if self.head is None: 
            return

        curr = self.head 
        prev = None
        new_stack = [] 
        while curr is not None: 
            val = 0

            # Terminate the loop whichever comes first 
            # either current == None or value >= k 
            while curr is not None and val < k: 
                new_stack.append(curr.data) 
                curr = curr.next
                val += 1

            # Now pop the elements of stack one by one 
            while new_stack: 

                # If final list has not been started yet. 
                if prev is None: 
                    prev = Node(new_stack.pop()) 
                    self.head = prev 
                else: 
                    prev.next = Node(new_stack.pop()) 
                    prev = prev.next

        # Next of last element will point to None. 
        prev.next = None
        return self.head 

# Driver Code 
llist = LinkedList()  
llist.prepend(9) 
llist.prepend(8) 
llist.prepend(7) 
llist.prepend(6) 
llist.prepend(5) 
llist.prepend(4) 
llist.prepend(3) 
llist.prepend(2) 
llist.prepend(1) 

print("Given linked list") 
print(llist) 
llist.head = llist.reverse(3) 

print("Reversed Linked list") 
print(llist) 

# This code is contributed by  
# Sagar Kumar Sinha(sagarsinha7777) 

```

## C#

```cs

// C# program to reverse a linked list   
// in groups of given size  
using System; 
using System.Collections; 

class GfG  
{  

/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
}  
static Node head = null;  

/* Reverses the linked list in groups of size k  
and returns the pointer to the new head node. */
static Node Reverse(Node head, int k)  
{  
    // Create a stack of Node*  
    Stack mystack = new Stack();  
    Node current = head;  
    Node prev = null;  

    while (current != null)  
    {  

        // Terminate the loop whichever comes first  
        // either current == NULL or count >= k  
        int count = 0;  
        while (current != null && count < k)  
        {  
            mystack.Push(current);  
            current = current.next;  
            count++;  
        }  

        // Now Pop the elements of stack one by one  
        while (mystack.Count > 0)  
        {  

            // If final list has not been started yet.  
            if (prev == null)  
            {  
                prev = (Node)mystack.Peek();  
                head = prev;  
                mystack.Pop();  
            }  
            else
            {  
                prev.next = (Node)mystack.Peek();  
                prev = prev.next;  
                mystack.Pop();  
            }  
        }  
    }  

    // Next of last element will point to NULL.  
    prev.next = null;  

    return head;  
}  

/* UTILITY FUNCTIONS */
/* Function to Push a node */
static void Push( int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list off the new node */
    new_node.next = head;  

    /* move the head to point to the new node */
    head = new_node;  
}  

/* Function to print linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(node.data + " ");  
        node = node.next;  
    }  
}  

/* Driver code*/
public static void Main(String []args)  
{  
    /* Start with the empty list */
    //Node head = null;  

    /* Created Linked list is 1->2->3->  
    4->5->6->7->8->9 */
    Push( 9);  
    Push( 8);  
    Push( 7);  
    Push( 6);  
    Push( 5);  
    Push(4);  
    Push(3);  
    Push(2);  
    Push( 1);  

    Console.WriteLine("Given linked list ");  
    printList(head);  
    head = Reverse(head, 3);  
    Console.WriteLine();  

    Console.WriteLine("Reversed Linked list ");  
    printList(head);  
}  
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Given Linked List
1 2 3 4 5 6 7 8 9 
Reversed list
3 2 1 6 5 4 9 8 7

```

本文由 **Jatin Goyal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

