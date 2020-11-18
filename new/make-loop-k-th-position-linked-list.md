# 在链接列表中的第 k 个位置循环

> 原文：[https://www.geeksforgeeks.org/make-loop-k-th-position-linked-list/](https://www.geeksforgeeks.org/make-loop-k-th-position-linked-list/)

给定一个链表和位置 k。 在第 k 个位置循环

**示例**：

```
Input : Given linked list

Output : Modified linked list

```

**算法**

1）遍历第一个链表直到第 k 个点

2）备份第 k 个节点

3）遍历链表直到最后

4）将最后一个节点附加到第 k 个节点

## C++

```cpp

// CPP program for making loop at k-th index 
// of given linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to make loop at k-th elements of 
linked list */
void makeloop(struct Node** head_ref, int k) 
{ 
    // traverse the linked list until loop 
    // point not found 
    struct Node* temp = *head_ref; 
    int count = 1; 
    while (count < k) { 
        temp = temp->next; 
        count++; 
    } 

    // backup the joint point  
    struct Node* joint_point = temp;  

    // traverse remaining nodes 
    while (temp->next != NULL)  
        temp = temp->next; 

    // joint the last node to k-th element 
    temp->next = joint_point; 
} 

/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = 
        (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* head, int total_nodes) 
{ 
    struct Node* curr = head; 
    int count = 0; 
    while (count < total_nodes) { 
        count++; 
        cout << curr->data << " "; 
        curr = curr->next; 
    } 
} 

int countNodes(Node *ptr) 
{ 
    int count = 0; 
    while (ptr != NULL) 
    { 
        ptr = ptr->next; 
        count++; 
    } 
    return count; 
} 

/* Driver program to test above function*/
int main() 
{ 
    // Create a linked list 1->2->3->4->5->6->7 
    struct Node* head = NULL; 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    // k should be less than the 
    // numbers of nodes 
    int k = 4; 
    int total_nodes = countNodes(head); 

    cout << "\nGiven list\n"; 
    printList(head, total_nodes); 

    makeloop(&head, k); 

    cout << "\nModified list\n"; 
    printList(head, total_nodes); 
    return 0; 
} 

```

## Java

```java

// Java program for making loop at k-th index  
// of given linked list  
class GFG 
{ 

// Link list node / 
static class Node 
{  
    int data;  
    Node next;  
}  

// Function to make loop at k-th elements of  
//linked list / 
static Node makeloop( Node head_ref, int k)  
{  
    // traverse the linked list until loop  
    // point not found  
    Node temp = head_ref;  
    int count = 1;  
    while (count < k) 
    {  
        temp = temp.next;  
        count++;  
    }  

    // backup the joint point  
    Node joint_point = temp;  

    // traverse remaining nodes  
    while (temp.next != null)  
        temp = temp.next;  

    // joint the last node to k-th element  
    temp.next = joint_point;  
    return head_ref; 
}  

// Function to push a node / 
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print linked list / 
static void printList( Node head, int total_nodes)  
{  
    Node curr = head;  
    int count = 0;  
    while (count < total_nodes) 
    {  
        count++;  
        System.out.print(curr.data + " ");  
        curr = curr.next;  
    }  
}  

static int countNodes(Node ptr)  
{  
    int count = 0;  
    while (ptr != null)  
    {  
        ptr = ptr.next;  
        count++;  
    }  
    return count;  
}  

// Driver code 
public static void main(String args[]) 
{  
    // Create a linked list 1.2.3.4.5.6.7  
    Node head = null;  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    // k should be less than the  
    // numbers of nodes  
    int k = 4;  
    int total_nodes = countNodes(head);  

    System.out.print("\nGiven list\n");  
    printList(head, total_nodes);  

    head = makeloop(head, k);  

    System.out.print( "\nModified list\n");  
    printList(head, total_nodes);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program for making loop at k-th index 
# of given linked list 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to make loop at k-th elements of 
#linked list  
def makeloop(head_ref, k): 

    # traverse the linked list until loop 
    # point not found 
    temp = head_ref 
    count = 1
    while (count < k): 
        temp = temp.next
        count = count + 1

    # backup the joint point  
    joint_point = temp  

    # traverse remaining nodes 
    while (temp.next != None):  
        temp = temp.next

    # joint the last node to k-th element 
    temp.next = joint_point 
    return head_ref 

# Function to push a node  
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Function to print linked list  
def printList( head,total_nodes): 
    curr = head 
    count = 0
    while (count < total_nodes): 
        count = count + 1
        print(curr.data, end = " ") 
        curr = curr.next

def countNodes(ptr): 
    count = 0
    while (ptr != None): 
        ptr = ptr.next
        count = count + 1

    return count 

# Driver Code 
if __name__=='__main__': 

    # Create a linked list 1.2.3.4.5.6.7 
    head = None
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 5) 
    head = push(head, 4) 
    head = push(head, 3) 
    head = push(head, 2) 
    head = push(head, 1) 

    # k should be less than the 
    # numbers of nodes 
    k = 4
    total_nodes = countNodes(head) 

    print("Given list") 
    printList(head, total_nodes) 

    makeloop(head, k) 

    print("\nModified list") 
    printList(head, total_nodes) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program for making loop at k-th index  
// of given linked list  
using System; 

class GFG 
{ 

// Link list node / 
public class Node 
{  
    public int data;  
    public Node next;  
}  

// Function to make loop at k-th elements of  
//linked list / 
static Node makeloop( Node head_ref, int k)  
{  
    // traverse the linked list until loop  
    // point not found  
    Node temp = head_ref;  
    int count = 1;  
    while (count < k) 
    {  
        temp = temp.next;  
        count++;  
    }  

    // backup the joint point  
    Node joint_point = temp;  

    // traverse remaining nodes  
    while (temp.next != null)  
        temp = temp.next;  

    // joint the last node to k-th element  
    temp.next = joint_point;  
    return head_ref; 
}  

// Function to push a node / 
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print linked list / 
static void printList( Node head, int total_nodes)  
{  
    Node curr = head;  
    int count = 0;  
    while (count < total_nodes) 
    {  
        count++;  
        Console.Write(curr.data + " ");  
        curr = curr.next;  
    }  
}  

static int countNodes(Node ptr)  
{  
    int count = 0;  
    while (ptr != null)  
    {  
        ptr = ptr.next;  
        count++;  
    }  
    return count;  
}  

// Driver code 
public static void Main(String []args) 
{  
    // Create a linked list 1.2.3.4.5.6.7  
    Node head = null;  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    // k should be less than the  
    // numbers of nodes  
    int k = 4;  
    int total_nodes = countNodes(head);  

    Console.Write("\nGiven list\n");  
    printList(head, total_nodes);  

    head = makeloop(head, k);  

    Console.Write( "\nModified list\n");  
    printList(head, total_nodes);  
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
Given list
1 2 3 4 5 6 7 
Modified list
1 2 3 4 5 6 7 

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。