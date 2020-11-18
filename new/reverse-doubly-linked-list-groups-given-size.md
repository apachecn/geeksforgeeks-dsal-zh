# 将给定大小的组中的双向链接列表反向

给定一个包含 **n** 个节点的双向链表。 问题是要反转列表中的每组 **k** 个节点。

范例：

![](img/f94b7d97202151446280399d423a7126.png)

**先决条件：** [反向双向链表| 设置 2。](https://www.geeksforgeeks.org/reverse-doubly-linked-list-set-2/)

**方法：**创建一个递归函数，例如 **reverse（head，k）**。 该功能接收每组 **k** 节点的头或第一个节点。 通过应用[中讨论的方法，可以反转 **k** 个节点组。 设置 2。](https://www.geeksforgeeks.org/reverse-doubly-linked-list-set-2/) 反转 **k 个**节点组后，该功能检查列表中是否存在下一组节点。 如果组存在，则使用下一个组的第一个节点对其自身进行递归调用，并使用该组的下一个和上一个链接进行必要的调整。 最后，它返回反转组的新头节点。

## C++

```cpp

// C++ implementation to reverse a doubly linked list 
// in groups of given size 
#include <bits/stdc++.h> 

using namespace std; 

// a node of the doubly linked list 
struct Node { 
    int data; 
    Node *next, *prev; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* new_node = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    new_node->data = data; 
    new_node->next = new_node->prev = NULL; 
    return new_node; 
} 

// function to insert a node at the beginging 
// of the Doubly Linked List 
void push(Node** head_ref, Node* new_node) 
{ 
    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// function to reverse a doubly linked list 
// in groups of given size 
Node* revListInGroupOfGivenSize(Node* head, int k) 
{ 
    Node *current = head; 
    Node* next = NULL; 
    Node* newHead = NULL; 
    int count = 0; 

    // reversing the current group of k  
    // or less than k nodes by adding 
    // them at the beginning of list 
    // 'newHead' 
    while (current != NULL && count < k) 
    { 
        next = current->next; 
        push(&newHead, current); 
        current = next; 
        count++; 
    } 

    // if next group exists then making the desired 
    // adjustments in the link 
    if (next != NULL) 
    { 
        head->next = revListInGroupOfGivenSize(next, k); 
        head->next->prev = head; 
    } 

    // pointer to the new head of the  
    // reversed group 
    return newHead; 
} 

// Function to print nodes in a 
// given doubly linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Start with the empty list 
    Node* head = NULL; 

    // Create doubly linked: 10<->8<->4<->2  
    push(&head, getNode(2)); 
    push(&head, getNode(4)); 
    push(&head, getNode(8)); 
    push(&head, getNode(10)); 

    int k = 2; 

    cout << "Original list: "; 
    printList(head); 

    // Reverse doubly linked list in groups of  
    // size 'k' 
    head = revListInGroupOfGivenSize(head, k); 

    cout << "\nModified list: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to reverse a doubly linked list  
// in groups of given size  
import java.io.*; 
import java.util.*; 

// Represents a node of doubly linked list 
class Node 
{ 
    int data; 
    Node next, prev; 
} 

class GFG  
{ 

    // function to get a new node 
    static Node getNode(int data) 
    { 
        // allocating node 
        Node new_node = new Node(); 
        new_node.data = data; 
        new_node.next = new_node.prev = null; 

        return new_node; 
    } 

    // function to insert a node at the beginning  
    // of the Doubly Linked List  
    static Node push(Node head, Node new_node)  
    { 
        // since we are adding at the beginning,  
        // prev is always NULL  
        new_node.prev = null; 

        // link the old list off the new node 
        new_node.next = head; 

        // change prev of head node to new node  
        if (head != null) 
            head.prev = new_node; 

        // move the head to point to the new node  
        head = new_node; 
        return head; 
    } 

    // function to reverse a doubly linked list  
    // in groups of given size  
    static Node revListInGroupOfGivenSize(Node head, int k) 
    { 
        Node current = head; 
        Node next = null; 
        Node newHead = null; 
        int count = 0; 

        // reversing the current group of k  
        // or less than k nodes by adding  
        // them at the beginning of list  
        // 'newHead' 
        while (current != null && count < k) 
        { 
            next = current.next; 
            newHead = push(newHead, current); 
            current = next; 
            count++; 
        } 

        // if next group exists then making the desired  
        // adjustments in the link  
        if (next != null) 
        { 
            head.next = revListInGroupOfGivenSize(next, k);  
            head.next.prev = head; 
        } 

        // pointer to the new head of the  
        // reversed group 
        return newHead;  
    } 

    // Function to print nodes in a  
    // given doubly linked list  
    static void printList(Node head) 
    { 
        while (head != null) 
        { 
            System.out.print(head.data + " "); 
            head = head.next; 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Start with the empty list 
        Node head = null;  

        // Create doubly linked: 10<->8<->4<->2 
        head = push(head, getNode(2)); 
        head = push(head, getNode(4)); 
        head = push(head, getNode(8)); 
        head = push(head, getNode(10)); 

        int k = 2; 

        System.out.print("Original list: "); 
        printList(head); 

        // Reverse doubly linked list in groups of  
        // size 'k' 
        head = revListInGroupOfGivenSize(head, k);  

        System.out.print("\nModified list: "); 
        printList(head); 
    } 
} 

// This code is contributed by rachana soma 

```

## 蟒蛇

```

# Python implementation to reverse a doubly linked list 
# in groups of given size 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# function to get a new node 
def getNode(data): 

    # allocate space 
    new_node = Node(0) 

    # put in the data 
    new_node.data = data 
    new_node.next = new_node.prev = None
    return new_node 

# function to insert a node at the beginging 
# of the Doubly Linked List 
def push(head_ref, new_node): 

    # since we are adding at the beginning, 
    # prev is always None 
    new_node.prev = None

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # change prev of head node to new node 
    if ((head_ref) != None): 
        (head_ref).prev = new_node 

    # move the head to point to the new node 
    (head_ref) = new_node 
    return head_ref 

# function to reverse a doubly linked list 
# in groups of given size 
def revListInGroupOfGivenSize( head, k): 

    current = head 
    next = None
    newHead = None
    count = 0

    # reversing the current group of k  
    # or less than k nodes by adding 
    # them at the beginning of list 
    # 'newHead' 
    while (current != None and count < k): 

        next = current.next
        newHead = push(newHead, current) 
        current = next
        count = count + 1

    # if next group exists then making the desired 
    # adjustments in the link 
    if (next != None): 

        head.next = revListInGroupOfGivenSize(next, k) 
        head.next.prev = head 

    # pointer to the new head of the  
    # reversed group 
    return newHead 

# Function to print nodes in a 
# given doubly linked list 
def printList(head): 

    while (head != None):  
        print( head.data , end=" ") 
        head = head.next

# Driver program to test above 

# Start with the empty list 
head = None

# Create doubly linked: 10<.8<.4<.2  
head = push(head, getNode(2)) 
head = push(head, getNode(4)) 
head = push(head, getNode(8)) 
head = push(head, getNode(10)) 

k = 2

print("Original list: ") 
printList(head) 

# Reverse doubly linked list in groups of  
# size 'k' 
head = revListInGroupOfGivenSize(head, k) 

print("\nModified list: ") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to reverse a doubly linked list  
// in groups of given size  
using System; 

// Represents a node of doubly linked list  
public class Node  
{  
    public int data;  
    public Node next, prev;  
}  

class GFG  
{  

    // function to get a new node  
    static Node getNode(int data)  
    {  
        // allocating node  
        Node new_node = new Node();  
        new_node.data = data;  
        new_node.next = new_node.prev = null;  

        return new_node;  
    }  

    // function to insert a node at the beginning  
    // of the Doubly Linked List  
    static Node push(Node head, Node new_node)  
    {  
        // since we are adding at the beginning,  
        // prev is always NULL  
        new_node.prev = null;  

        // link the old list off the new node  
        new_node.next = head;  

        // change prev of head node to new node  
        if (head != null)  
            head.prev = new_node;  

        // move the head to point to the new node  
        head = new_node;  
        return head;  
    }  

    // function to reverse a doubly linked list  
    // in groups of given size  
    static Node revListInGroupOfGivenSize(Node head, int k)  
    {  
        Node current = head;  
        Node next = null;  
        Node newHead = null;  
        int count = 0;  

        // reversing the current group of k  
        // or less than k nodes by adding  
        // them at the beginning of list  
        // 'newHead'  
        while (current != null && count < k)  
        {  
            next = current.next;  
            newHead = push(newHead, current);  
            current = next;  
            count++;  
        }  

        // if next group exists then making the desired  
        // adjustments in the link  
        if (next != null)  
        {  
            head.next = revListInGroupOfGivenSize(next, k);  
            head.next.prev = head;  
        }  

        // pointer to the new head of the  
        // reversed group  
        return newHead;  
    }  

    // Function to print nodes in a  
    // given doubly linked list  
    static void printList(Node head)  
    {  
        while (head != null)  
        {  
            Console.Write(head.data + " ");  
            head = head.next;  
        }  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        // Start with the empty list  
        Node head = null;  

        // Create doubly linked: 10<->8<->4<->2  
        head = push(head, getNode(2));  
        head = push(head, getNode(4));  
        head = push(head, getNode(8));  
        head = push(head, getNode(10));  

        int k = 2;  

        Console.Write("Original list: ");  
        printList(head);  

        // Reverse doubly linked list in groups of  
        // size 'k'  
        head = revListInGroupOfGivenSize(head, k);  

        Console.Write("\nModified list: ");  
        printList(head);  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Original list: 10 8 4 2
Modified list: 8 10 2 4

```

**时间复杂度：** O（n）。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。