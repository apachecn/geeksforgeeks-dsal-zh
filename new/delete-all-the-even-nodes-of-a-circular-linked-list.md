# 删除循环链接列表

的所有偶数节点

给定一个包含 N 个节点的循环单链接列表，任务是从列表中删除所有偶数节点。

![](img/a5952645a5099f3049e9216a4d8dbaad.png)

**示例：**

```
Input : 57->11->2->56->12->61 
Output : List after deletion : 57 -> 11 -> 61 

Input : 9->11->32->6->13->20
Output : List after deletion : 9 -> 11 -> 13 

```

这个想法是一个遍历循环单链表的节点，并获得具有偶数数据的节点的指针。 遵循中的[中使用的方法删除那些节点。](https://www.geeksforgeeks.org/deletion-circular-linked-list/)

以下是上述想法的实现：

## C++

```cpp

// CPP program to delete all even 
// node from a Circular singly linked list 

#include <bits/stdc++.h> 
using namespace std; 

// Structure for a node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert a node at the beginning 
// of a Circular linked list 
void push(struct Node** head_ref, int data) 
{ 
    struct Node* ptr1 = (struct Node*)malloc(sizeof(struct Node)); 
    struct Node* temp = *head_ref; 
    ptr1->data = data; 
    ptr1->next = *head_ref; 

    // If linked list is not NULL then 
    // set the next of last node 
    if (*head_ref != NULL) { 
        while (temp->next != *head_ref) 
            temp = temp->next; 
        temp->next = ptr1; 
    } 
    else
        ptr1->next = ptr1; // For the first node 

    *head_ref = ptr1; 
} 

// Delete the node if it is even 
void deleteNode(Node* head_ref, Node* del) 
{ 
    struct Node* temp = head_ref; 
    // If node to be deleted is head node 

    if (head_ref == del) 
        head_ref = del->next; 

    // traverse list till not found 
    // delete node 
    while (temp->next != del) { 
        temp = temp->next; 
    } 

    // copy address of node 
    temp->next = del->next; 

    // Finally, free the memory occupied by del 
    free(del); 
    return; 
} 

// Function to delete all even nodes 
// from the singly circular  linked list 
void deleteEvenNodes(Node* head) 
{ 
    struct Node* ptr = head; 

    struct Node* next; 

    // traverse list till the end 
    // if the node is even then delete it 
    do { 
        // if node is even 
        if (ptr->data % 2 == 0) 
            deleteNode(head, ptr); 

        // point to next node 
        next = ptr->next; 
        ptr = next; 
    } while (ptr != head); 
} 

// Function to print nodes 
void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    if (head != NULL) { 
        do { 
            printf("%d ", temp->data); 
            temp = temp->next; 
        } while (temp != head); 
    } 
} 

// Driver code 
int main() 
{ 
    // Initialize lists as empty 
    struct Node* head = NULL; 

    // Created linked list will be 57->11->2->56->12->61 
    push(&head, 61); 
    push(&head, 12); 
    push(&head, 56); 
    push(&head, 2); 
    push(&head, 11); 
    push(&head, 57); 

    cout << "\nList after deletion : "; 
    deleteEvenNodes(head); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to delete all prime  
// node from a Circular singly linked list  
class GFG 
{ 

// Structure for a node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the beginning  
// of a Circular linked list  
static Node push(Node head_ref, int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    // If linked list is not null then  
    // set the next of last node  
    if (head_ref != null)  
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
        return head_ref; 
    }  
    else
        ptr1.next = ptr1; // For the first node  

    head_ref = ptr1;  
return head_ref; 
}  

// Delete the node if it is even  
static Node deleteNode(Node head_ref, Node del)  
{  
    Node temp = head_ref;  
    // If node to be deleted is head node  

    if (head_ref == del)  
        head_ref = del.next;  

    // traverse list till not found  
    // delete node  
    while (temp.next != del) 
    {  
        temp = temp.next;  
    }  

    // copy address of node  
    temp.next = del.next;  

    return head_ref;  
}  

// Function to delete all even nodes  
// from the singly circular linked list  
static Node deleteEvenNodes(Node head)  
{  
    Node ptr = head;  

    Node next;  

    // traverse list till the end  
    // if the node is even then delete it  
    do 
    {  
        // if node is even  
        if (ptr.data % 2 == 0)  
            deleteNode(head, ptr);  

        // point to next node  
        next = ptr.next;  
        ptr = next;  
    }  
    while (ptr != head);  
    return head; 
}  

// Function to print nodes  
static void printList(Node head)  
{  
    Node temp = head;  
    if (head != null) 
    {  
        do 
        {  
            System.out.printf("%d ", temp.data);  
            temp = temp.next;  
        }  
        while (temp != head);  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    // Initialize lists as empty  
    Node head = null;  

    // Created linked list will be 57.11.2.56.12.61  
    head=push(head, 61);  
    head=push(head, 12);  
    head=push(head, 56);  
    head=push(head, 2);  
    head=push(head, 11);  
    head=push(head, 57);  

    System.out.println( "\nList after deletion : ");  
    head=deleteEvenNodes(head);  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to delete all even 
# node from a Circular singly linked list 
import math 

# Structure for a node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the beginning 
# of a Circular linked list 
def push(head_ref, data): 
    ptr1 = Node(data) 
    temp = head_ref 
    ptr1.data = data 
    ptr1.next = head_ref 

    # If linked list is not None then 
    # set the next of last node 
    if (head_ref != None): 
        while (temp.next != head_ref): 
            temp = temp.next
        temp.next = ptr1 

    else: 
        ptr1.next = ptr1 # For the first node 

    head_ref = ptr1 
    return head_ref 

# Delete the node if it is even 
def deleteNode(head_ref, delete): 
    temp = head_ref 

    # If node to be deleted is head node 
    if (head_ref == delete): 
        head_ref = delete.next

    # traverse list till not found 
    # delete node 
    while (temp.next != delete): 
        temp = temp.next

    # copy address of node 
    temp.next = delete.next

    # Finally, free the memory occupied by delete 

# Function to delete all even nodes 
# from the singly circular linked list 
def deleteEvenNodes(head): 
    ptr = head 
    next = None

    # traverse list till the end 
    # if the node is even then delete it 
    # if node is even 
    next = ptr.next
    ptr = next
    while (ptr != head): 
        if (ptr.data % 2 == 0): 
            deleteNode(head, ptr) 

        # po to next node 
        next = ptr.next
        ptr = next
    return head 

# Function to pr nodes 
def prList(head): 
    temp = head 
    if (head != None): 
        print(temp.data, end = " ") 
        temp = temp.next
        while (temp != head): 
            print(temp.data, end = " ") 
            temp = temp.next

# Driver code 
if __name__=='__main__':  

    # Initialize lists as empty 
    head = None

    # Created linked list will be 57.11.2.56.12.61 
    head = push(head, 61)  
    head = push(head, 12) 
    head = push(head, 56)  
    head = push(head, 2)  
    head = push(head, 11)  
    head = push(head, 57) 

    print("List after deletion : ", end = "") 
    head = deleteEvenNodes(head) 
    prList(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to delete all prime  
// node from a Circular singly linked list  
using System; 

class GFG  
{  

// Structure for a node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the beginning  
// of a Circular linked list  
static Node push(Node head_ref, int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    // If linked list is not null then  
    // set the next of last node  
    if (head_ref != null)  
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
        return head_ref;  
    }  
    else
        ptr1.next = ptr1; // For the first node  

    head_ref = ptr1;  
return head_ref;  
}  

// Delete the node if it is even  
static Node deleteNode(Node head_ref, Node del)  
{  
    Node temp = head_ref;  

    // If node to be deleted is head node  
    if (head_ref == del)  
        head_ref = del.next;  

    // traverse list till not found  
    // delete node  
    while (temp.next != del)  
    {  
        temp = temp.next;  
    }  

    // copy address of node  
    temp.next = del.next;  

    return head_ref;  
}  

// Function to delete all even nodes  
// from the singly circular linked list  
static Node deleteEvenNodes(Node head)  
{  
    Node ptr = head;  

    Node next;  

    // traverse list till the end  
    // if the node is even then delete it  
    do
    {  
        // if node is even  
        if (ptr.data % 2 == 0)  
            deleteNode(head, ptr);  

        // point to next node  
        next = ptr.next;  
        ptr = next;  
    }  
    while (ptr != head);  
    return head;  
}  

// Function to print nodes  
static void printList(Node head)  
{  
    Node temp = head;  
    if (head != null)  
    {  
        do
        {  
            Console.Write("{0} ", temp.data);  
            temp = temp.next;  
        }  
        while (temp != head);  
    }  
}  

// Driver code  
public static void Main(String []args)  
{  
    // Initialize lists as empty  
    Node head = null;  

    // Created linked list will be 57.11.2.56.12.61  
    head=push(head, 61);  
    head=push(head, 12);  
    head=push(head, 56);  
    head=push(head, 2);  
    head=push(head, 11);  
    head=push(head, 57);  

    Console.WriteLine( "\nList after deletion : ");  
    head=deleteEvenNodes(head);  
    printList(head);  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
List after deletion : 57 11 61

```

**时间复杂度：`O(n)`**，其中 N 是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。