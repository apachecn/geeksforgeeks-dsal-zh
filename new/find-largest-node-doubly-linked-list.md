# 在双向链接列表

中找到最大的节点

给定双向链表，请在双向链表中找到最大的节点。

**示例：**

```
Input: 10->8->4->23->67->88
        Largest node is: 88
Output: 88

Input : 34->2->78->18->120->39->7
        Largest node  is: 120
Output :120

```

**使用的方法：**

1.初始化指向头节点的临时和最大指针。
2.遍历整个列表。
3.如果 temp 的数据大于 max 的数据，则将 max = temp。
4.在下一个节点上移动。

## C++

```cpp

/* C++ Program to find the largest  
nodes in doubly linked list */
#include <iostream> 
using namespace std; 

// Create a node of the doubly linked list  
struct Node 
{  
    int data;  
    struct Node* next;  
    struct Node* prev;  
};  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the  
beginging of the Doubly Linked List */
void push(struct Node** head_ref, int new_data)  
{  
    /* allocate node */
    struct Node* new_node =  
    (struct Node*)malloc(sizeof(struct Node));  

    /* put in the data */
    new_node->data = new_data;  

    /* since we are adding at the  
    beginning, prev is always NULL */
    new_node->prev = NULL;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* change prev of head node to new node */
    if ((*head_ref) != NULL)  
        (*head_ref)->prev = new_node;  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Function to find the largest  
nodes in Doubly Linked List */
int LargestInDLL(struct Node** head_ref)  
{  
    struct Node *max, *temp;  

    /* initialize two pointer temp  
    and max on the head node */
    temp = max = *head_ref;  

    // traverse the whole doubly linked list  
    while (temp != NULL)  
    {  

        /* if temp's data is greater than  
        max's data, then put max = temp  
        and return max->data */
        if (temp->data > max->data)  
            max = temp;  

        temp = temp->next;  
    }  
    return max->data;  
}  

// Driver code 
int main()  
{  
    // Start with the empty list  
    struct Node* head = NULL;  

    // Let us create a linked list  
    push(&head, 20);  
    push(&head, 14);  
    push(&head, 181);  
    push(&head, 100);  

    cout << LargestInDLL(&head);  
    return 0;  
}  

// This code is contributed by shubhamsingh10 

```

## C

```c

/* Program to find the largest 
   nodes in doubly linked list */
#include <stdio.h> 
#include <stdlib.h> 

// Create a node of the doubly linked list 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the 
beginging of the Doubly Linked List */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* since we are adding at the  
    beginning, prev is always NULL */
    new_node->prev = NULL; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* change prev of head node to new node */
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to find the largest  
   nodes in Doubly Linked List */
int LargestInDLL(struct Node** head_ref) 
{ 
    struct Node *max, *temp; 

    /* initialize two pointer temp  
       and max on the head node */
    temp = max = *head_ref; 

    // traverse the whole doubly linked list 
    while (temp != NULL) { 

        /* if temp's data is greater than 
           max's data, then put max = temp 
           and return max->data */
        if (temp->data > max->data) 
            max = temp; 

        temp = temp->next; 
    } 
    return max->data; 
} 

int main() 
{ 
    // Start with the empty list 
    struct Node* head = NULL; 

    // Let us create a linked list 
    push(&head, 20); 
    push(&head, 14); 
    push(&head, 181); 
    push(&head, 100); 

    printf("%d", LargestInDLL(&head)); 
    return 0; 
} 

```

## Java

```java

// Java Program to find the largest 
// nodes in doubly linked list 
class GFG { 

    // Create node of the doubly linked list 
    static class Node { 
        int data; 
        Node next; 
        Node prev; 
    }; 

    // UTILITY FUNCTIONS 
    // Function to insert a node at the 
    // beginging of the Doubly Linked List 
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // since we are adding at the 
        // beginning, prev is always null 
        new_node.prev = null; 

        // link the old list off the new node 
        new_node.next = (head_ref); 

        // change prev of head node to new node 
        if ((head_ref) != null) 
            (head_ref).prev = new_node; 

        // move the head to point to the new node 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Function to find the largest 
    // nodes in Doubly Linked List 
    static int LargestInDLL(Node head_ref) 
    { 
        Node max, temp; 

        // initialize two pointer temp 
        // and max on the head node 
        temp = max = head_ref; 

        // traverse the whole doubly linked list 
        while (temp != null) { 

            // if temp's data is greater than 
            // max's data, then put max = temp 
            // and return max.data 
            if (temp.data > max.data) 
                max = temp; 

            temp = temp.next; 
        } 
        return max.data; 
    } 

    public static void main(String args[]) 
    { 
        // Start with the empty list 
        Node head = null; 

        // Let us create a linked list 
        head = push(head, 20); 
        head = push(head, 14); 
        head = push(head, 181); 
        head = push(head, 100); 

        System.out.printf("%d", LargestInDLL(head)); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find largest  
# node in doubly linked list 

# Node of the doubly linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.prev = None
        self.next = None

# Function to find pair whose product 
# equal to given value x 
def pairProduct(head, x): 

    # Set two pointers, 
    # first to the beginning of DLL 
    # and second to the end of DLL. 
    first = head 
    second = head 
    while (second.next != None): 
        second = second.next

    # To track if we find a pair or not 
    found = False

    # The loop terminates when either of two pointers 
    # become None, or they cross each other (second.next 
    # == first), or they become same (first == second) 
    while (first != None and
           second != None and first != second and 
           second.next != first) : 

        # pair found 
        if ((first.data * second.data) == x) : 
            found = True
            print("(" , first.data,  
                  ", ", second.data, ")") 

            # move first in forward direction 
            first = first.next

            # move second in backward direction 
            second = second.prev 

        else : 
            if ((first.data * second.data) < x): 
                first = first.next
            else: 
                second = second.prev 

    # if pair is not present 
    if (found == False): 
        print( "No pair found") 

# A utility function to insert a new node at the 
# beginning of doubly linked list 
def push( head, data): 

    temp = Node(0) 
    temp.data = data 
    temp.next = temp.prev = None
    if (head == None): 
        (head) = temp 
    else : 
        temp.next = head 
        (head).prev = temp 
        (head) = temp 
    return head 

""" Function to find the largest  
nodes in Doubly Linked List """
def LargestInDLL( head_ref): 

    max = None
    temp = None

    """ initialize two pointer temp  
    and max on the head node """
    temp = max = head_ref 

    # traverse the whole doubly linked list 
    while (temp != None):  

        """ if temp's data is greater than 
        max's data, then put max = temp 
        and return max.data """
        if (temp.data > max.data): 
            max = temp 

        temp = temp.next

    return max.data 

# Driver Code 
if __name__ == "__main__":  

    # Start with the empty list 
    head = None

    # Let us create a linked list 
    head = push(head, 20) 
    head = push(head, 14) 
    head = push(head, 181) 
    head = push(head, 100) 

    print( LargestInDLL(head)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# Program to find the largest 
// nodes in doubly linked list 
using System; 

class GFG { 

    // Create node of the doubly linked list 
    public class Node { 
        public int data; 
        public Node next; 
        public Node prev; 
    }; 

    // UTILITY FUNCTIONS 
    // Function to insert a node at the 
    // beginging of the Doubly Linked List 
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // since we are adding at the 
        // beginning, prev is always null 
        new_node.prev = null; 

        // link the old list off the new node 
        new_node.next = (head_ref); 

        // change prev of head node to new node 
        if ((head_ref) != null) 
            (head_ref).prev = new_node; 

        // move the head to point to the new node 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Function to find the largest 
    // nodes in Doubly Linked List 
    static int LargestInDLL(Node head_ref) 
    { 
        Node max, temp; 

        // initialize two pointer temp 
        // and max on the head node 
        temp = max = head_ref; 

        // traverse the whole doubly linked list 
        while (temp != null) { 

            // if temp's data is greater than 
            // max's data, then put max = temp 
            // and return max.data 
            if (temp.data > max.data) 
                max = temp; 

            temp = temp.next; 
        } 
        return max.data; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        // Start with the empty list 
        Node head = null; 

        // Let us create a linked list 
        head = push(head, 20); 
        head = push(head, 14); 
        head = push(head, 181); 
        head = push(head, 100); 

        Console.Write("{0}", LargestInDLL(head)); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出：**

```
 181

```

**时间复杂度：O（n）
辅助空间：O（1）** 



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。