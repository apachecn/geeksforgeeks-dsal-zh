# 从双向链表中删除所有大于给定值的节点

给定一个包含 N 个节点和一个数字 X 的双向链表，任务是从列表中删除所有大于给定值 X 的节点。

**示例：**

> **输入：** 10 8 4 11 9，X = 9
> **输出：** 8 4 9
> 
> **输入：** 4 4 2 1 3 5，X = 2
> **输出：** 2 1

**方法：**遍历双向链表的节点，并获得数据值大于 **x** 的节点的指针。 遵循此[中使用的方法删除这些节点。](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)

## C++

```cpp

// C++ implementation to delete all 
// the nodes from the doubly 
// linked list that are greater than 
// the specified value x 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the doubly linked list 
struct Node { 
    int data; 
    Node *prev, *next; 
}; 

// function to insert a node at the beginning 
// of the Doubly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node = (Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

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

// function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del  -->  pointer to node to be deleted 
void deleteNode(Node** head_ref, Node* del) 
{ 
    // base case 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 

    // Change next only if node to be  
    // deleted is NOT the last node 
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    // Change prev only if node to be  
    // deleted is NOT the first node 
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    // Finally, free the memory occupied by del 
    free(del); 

    return; 
} 

// function to delete all the nodes 
// from the doubly linked 
// list that are greater than the 
// specified value x 
void deleteGreaterNodes(Node** head_ref, int x) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 

    while (ptr != NULL) { 
        next = ptr->next; 
        // if true, delete node 'ptr' 
        if (ptr->data > x) 
            deleteNode(head_ref, ptr); 
        ptr = next; 
    } 
} 

// function to print nodes in a 
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
    // start with the empty list 
    Node* head = NULL; 

    // create the doubly linked list  
    // 10<->8<->4<->11<->9 
    push(&head, 9); 
    push(&head, 11); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 10); 

    int x = 9; 

    cout << "Original List: "; 
    printList(head); 

    deleteGreaterNodes(&head, x); 

    cout << "\nModified List: "; 
    printList(head); 
} 

```

## Java

```java

// Java implementation to delete all  
// the nodes from the doubly  
// linked list that are greater than  
// the specified value x  
class GFG 
{ 

// Node of the doubly linked list  
static class Node  
{  
    int data;  
    Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
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

// function to delete a node in a Doubly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    if (head_ref == null || del == null)  
        return null;  

    // If node to be deleted is head node  
    if (head_ref == del)  
        head_ref = del.next;  

    // Change next only if node to be  
    // deleted is NOT the last node  
    if (del.next != null)  
        del.next.prev = del.prev;  

    // Change prev only if node to be  
    // deleted is NOT the first node  
    if (del.prev != null)  
        del.prev.next = del.next;  

    return head_ref;  
}  

// function to delete all the nodes  
// from the doubly linked  
// list that are greater than the  
// specified value x  
static Node deleteGreaterNodes(Node head_ref, int x)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null)  
    {  
        next = ptr.next; 

        // if true, delete node 'ptr'  
        if (ptr.data > x)  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given doubly linked list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 10<.8<.4<.11<.9  
    head = push(head, 9);  
    head = push(head, 11);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 10);  

    int x = 9;  

    System.out.print( "Original List: ");  
    printList(head);  

    head=deleteGreaterNodes(head, x);  

    System.out.print( "\nModified List: ");  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python implementation to delete all 
# the nodes from the doubly 
# linked list that are greater than 
# the specified value x 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None
        self.prev = None

# function to insert a node at the beginning  
# of the Doubly Linked List  
def push( head_ref, new_data):  

    # allocate node  
    new_node = Node(0)  

    # put in the data  
    new_node.data = new_data  

    # since we are adding at the beginning,  
    # prev is always None  
    new_node.prev = None

    # link the old list off the new node  
    new_node.next = (head_ref)  

    # change prev of head node to new node  
    if ((head_ref) != None) : 
        (head_ref).prev = new_node  

    # move the head to point to the new node  
    (head_ref) = new_node  

    return head_ref; 

# function to delete a node in a Doubly Linked List.  
# head_ref -. pointer to head node pointer.  
# del -. pointer to node to be deleted  
def deleteNode(head_ref, del_) : 

    # base case  
    if (head_ref == None or del_ == None) : 
        return head_ref 

    # If node to be deleted is head node  
    if (head_ref == del_) : 
        head_ref = del_.next

    # Change next only if node to be  
    # deleted is NOT the last node  
    if (del_.next != None) : 
        del_.next.prev = del_.prev  

    # Change prev only if node to be  
    # deleted is NOT the first node  
    if (del_.prev != None) : 
        del_.prev.next = del_.next

    return head_ref 

# function to delete all the nodes  
# from the doubly linked  
# list that are greater than the  
# specified value x  
def deleteGreaterNodes(head_ref, x) : 

    ptr = head_ref  
    next = None

    while (ptr != None) : 
        next = ptr.next

        # if true, delete node 'ptr'  
        if (ptr.data > x) : 
            head_ref = deleteNode(head_ref, ptr)  
        ptr = next

    return head_ref; 

# function to print nodes in a  
# given doubly linked list  
def printList( head) : 

    while (head != None) : 
        print( head.data, end= " ")  
        head = head.next

# Driver program to test above  

# start with the empty list  
head = None

# create the doubly linked list  
# 10<.8<.4<.11<.9  
head = push(head, 9)  
head = push(head, 11)  
head = push(head, 4)  
head = push(head, 8)  
head = push(head, 10)  

x = 9

print("Original List: ")  
printList(head)  

head = deleteGreaterNodes(head, x)  

print("\nModified List: ")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to delete all  
// the nodes from the doubly  
// linked list that are greater than  
// the specified value x 
using System; 

class GFG 
{ 

// Node of the doubly linked list  
public class Node  
{  
    public int data;  
    public Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
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

// function to delete a node in a Doubly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    if (head_ref == null || del == null)  
        return null;  

    // If node to be deleted is head node  
    if (head_ref == del)  
        head_ref = del.next;  

    // Change next only if node to be  
    // deleted is NOT the last node  
    if (del.next != null)  
        del.next.prev = del.prev;  

    // Change prev only if node to be  
    // deleted is NOT the first node  
    if (del.prev != null)  
        del.prev.next = del.next;  

    return head_ref;  
}  

// function to delete all the nodes  
// from the doubly linked  
// list that are greater than the  
// specified value x  
static Node deleteGreaterNodes(Node head_ref, int x)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null)  
    {  
        next = ptr.next; 

        // if true, delete node 'ptr'  
        if (ptr.data > x)  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given doubly linked list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 10<.8<.4<.11<.9  
    head = push(head, 9);  
    head = push(head, 11);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 10);  

    int x = 9;  

    Console.Write( "Original List: ");  
    printList(head);  

    head=deleteGreaterNodes(head, x);  

    Console.Write( "\nModified List: ");  
    printList(head);  
}  
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
Original List: 10 8 4 11 9 
Modified List: 8 4 9

```

**时间复杂度：** O（N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。