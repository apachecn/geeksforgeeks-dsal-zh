# 删除链表

> 原文：[https://www.geeksforgeeks.org/remove-first-node-of-the-linked-list/](https://www.geeksforgeeks.org/remove-first-node-of-the-linked-list/)

的第一个节点

给定一个链表，任务是删除链表的第一个节点并更新链表的头指针。

例子：

```
Input : 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Output : 2 -> 3 -> 4 -> 5 -> NULL

Input : 2 -> 4 -> 6 -> 8 -> 33 -> 67 -> NULL
Output : 4 -> 6 -> 8 -> 33 -> 67 -> NULL

```

要删除第一个节点，我们需要将第二个节点设为头，并删除分配给第一个节点的内存。

## C++

```cpp

// CPP program to remove first node of 
// linked list. 
#include <iostream> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to remove the first node  
   of the linked list */
Node* removeFirstNode(struct Node* head) 
{ 
    if (head == NULL) 
        return NULL; 

    // Move the head pointer to the next node 
    Node* temp = head; 
    head = head->next; 

    delete temp; 

    return head; 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    /* Use push() function to construct   
       the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    head = removeFirstNode(head); 
    for (Node* temp = head; temp != NULL; temp = temp->next) 
        cout << temp->data << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to remove first node of 
// linked list. 
class GFG { 

    // Link list node / 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to remove the first node 
    // of the linked list / 
    static Node removeFirstNode(Node head) 
    { 
        if (head == null) 
            return null; 

        // Move the head pointer to the next node 
        Node temp = head; 
        head = head.next; 

        return head; 
    } 

    // Function to push node at head 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Start with the empty list / 
        Node head = null; 

        // Use push() function to con 
        // the below list 8 . 23 . 11 . 29 . 12 / 
        head = push(head, 12); 
        head = push(head, 29); 
        head = push(head, 11); 
        head = push(head, 23); 
        head = push(head, 8); 

        head = removeFirstNode(head); 
        for (Node temp = head; temp != null; temp = temp.next) 
            System.out.print(temp.data + " "); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to remove first node of   
# linked list. 
import sys 

# Link list node  
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to remove the first node   
# of the linked list  
def removeFirstNode(head): 
    if not head: 
        return None
    temp = head 

    # Move the head pointer to the next node 
    head = head.next
    temp = None
    return head 

# Function to push node at head  
def push(head, data): 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# Driver code 
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # Use push() function to construct    
    # the below list 8 -> 23 -> 11 -> 29 -> 12  
    head = push(head, 12) 
    head = push(head, 29) 
    head = push(head, 11) 
    head = push(head, 23) 
    head = push(head, 8) 

    head = removeFirstNode(head) 

    while(head): 
        print("{} ".format(head.data), end ="") 
        head = head.next

# This code is Contributed by Vikash Kumar 37 

```

## C#

```cs

// C# program to remove first node of 
// linked list. 
using System;  

class GFG  
{ 

    // Link list node / 
    public class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    // Function to remove the first node 
    // of the linked list / 
    static Node removeFirstNode(Node head) 
    { 
        if (head == null) 
            return null; 

        // Move the head pointer to the next node 
        Node temp = head; 
        head = head.next; 

        return head; 
    } 

    // Function to push node at head 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        // Start with the empty list / 
        Node head = null; 

        // Use push() function to con 
        // the below list 8 . 23 . 11 . 29 . 12 / 
        head = push(head, 12); 
        head = push(head, 29); 
        head = push(head, 11); 
        head = push(head, 23); 
        head = push(head, 8); 

        head = removeFirstNode(head); 
        for (Node temp = head; temp != null; temp = temp.next) 
            Console.Write(temp.data + " "); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
23 11 29 12

```

**时间复杂度**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。