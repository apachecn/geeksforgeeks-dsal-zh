# 在两个双链表中查找公共节点的数量

> 原文：[https://www.geeksforgeeks.org/find-count-of-common-nodes-in-two-doubly-linked-lists/](https://www.geeksforgeeks.org/find-count-of-common-nodes-in-two-doubly-linked-lists/)

给定两个双链表。 任务是在两个双链表中找到公共节点的总数。

**示例**：

```
Input : 
list 1 = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17 
list 2 = 15 <=> 16 <=> 45 <=> 9 <=> 6
Output : Number of common nodes: 4

Input :
list 1 = 18 <=> 30 <=> 92 <=> 46 <=> 72 <=> 1
list 2 = 12 <=> 32 <=> 45 <=> 9 <=> 6 <=> 30
Output : Number of common nodes: 1

```

**方法**：使用两个嵌套循环遍历两个列表，直到列表的末尾。 对于列表 1 中的每个节点，检查它是否与列表 2 中的任何节点匹配。如果是，则增加公共节点的数量。 最后，打印计数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count 
// common element in given two 
// doubly linked list 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the doubly linked list 
struct Node { 
    int data; 
    Node *prev, *next; 
}; 

// Function to insert a node at the beginning 
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

// Count common nodes in both list1 and list 2 
int countCommonNodes(Node** head_ref, Node** head) 
{ 
    // head for list 1 
    Node* ptr = *head_ref; 

    // head for list 2 
    Node* ptr1 = *head; 

    // initialize count = 0 
    int count = 0; 

    // traverse list 1 till the end 
    while (ptr != NULL) { 
        // traverse list 2 till the end 
        while (ptr1 != NULL) { 
            // if node value is equal then 
            // increment count 
            if (ptr->data == ptr1->data) { 
                count++; 
                break; 
            } 

            // increment pointer list 2 
            ptr1 = ptr1->next; 
        } 

        // again list 2 start with starting point 
        ptr1 = *head; 

        // increment pointer list 1 
        ptr = ptr->next; 
    } 

    // return count of common nodes 
    return count; 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 
    Node* head1 = NULL; 

    // create the doubly linked list 1 
    // 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 9); 
    push(&head, 10); 
    push(&head, 16); 
    push(&head, 15); 

    // create the doubly linked list 2 
    // 15 <-> 16 <-> 45 <-> 9 <-> 6 
    push(&head1, 6); 
    push(&head1, 9); 
    push(&head1, 45); 
    push(&head1, 16); 
    push(&head1, 15); 

    cout << "Number of common nodes:"
         << countCommonNodes(&head, &head1); 

    return 0; 
} 

```

## Java

```java

// Java implementation to count 
// common element in given two 
// doubly linked list 
class GFG  
{ 

// Node of the doubly linked list 
static class Node 
{ 
    int data; 
    Node prev, next; 
}; 

// Function to insert a node at the beginning 
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
    new_node.next = head_ref; 

    // change prev of head node to new node 
    if (head_ref != null) 
        head_ref.prev = new_node; 

    // move the head to point to the new node 
    head_ref = new_node; 
    return head_ref; 
} 

// Count common nodes in both list1 and list 2 
static int countCommonNodes(Node head_ref,  
                            Node head) 
{ 
    // head for list 1 
    Node ptr = head_ref; 

    // head for list 2 
    Node ptr1 = head; 

    // initialize count = 0 
    int count = 0; 

    // traverse list 1 till the end 
    while (ptr != null) 
    { 

        // traverse list 2 till the end 
        while (ptr1 != null)  
        { 

            // if node value is equal then 
            // increment count 
            if (ptr.data == ptr1.data) 
            { 
                count++; 
                break; 
            } 

            // increment pointer list 2 
            ptr1 = ptr1.next; 
        } 

        // again list 2 start with starting point 
        ptr1 = head; 

        // increment pointer list 1 
        ptr = ptr.next; 
    } 

    // return count of common nodes 
    return count; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    // start with the empty list 
    Node head = null; 
    Node head1 = null; 

    // create the doubly linked list 1 
    // 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17 
    head = push(head, 17); 
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 9); 
    head = push(head, 10); 
    head = push(head, 16); 
    head = push(head, 15); 

    // create the doubly linked list 2 
    // 15 <. 16 <. 45 <. 9 <. 6 
    head1 = push(head1, 6); 
    head1 = push(head1, 9); 
    head1 = push(head1, 45); 
    head1 = push(head1, 16); 
    head1 = push(head1, 15); 

    System.out.println("Number of common nodes: " +  
                        countCommonNodes(head, head1)); 
} 
}  

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation to count 
// common element in given two 
// doubly linked list 
using System; 

class GFG  
{ 

// Node of the doubly linked list 
public class Node 
{ 
    public int data; 
    public Node prev, next; 
}; 

// Function to insert a node at the beginning 
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
    new_node.next = head_ref; 

    // change prev of head node to new node 
    if (head_ref != null) 
        head_ref.prev = new_node; 

    // move the head to point to the new node 
    head_ref = new_node; 
    return head_ref; 
} 

// Count common nodes in both list1 and list 2 
static int countCommonNodes(Node head_ref,  
                            Node head) 
{ 
    // head for list 1 
    Node ptr = head_ref; 

    // head for list 2 
    Node ptr1 = head; 

    // initialize count = 0 
    int count = 0; 

    // traverse list 1 till the end 
    while (ptr != null) 
    { 

        // traverse list 2 till the end 
        while (ptr1 != null)  
        { 

            // if node value is equal then 
            // increment count 
            if (ptr.data == ptr1.data) 
            { 
                count++; 
                break; 
            } 

            // increment pointer list 2 
            ptr1 = ptr1.next; 
        } 

        // again list 2 start with starting point 
        ptr1 = head; 

        // increment pointer list 1 
        ptr = ptr.next; 
    } 

    // return count of common nodes 
    return count; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    // start with the empty list 
    Node head = null; 
    Node head1 = null; 

    // create the doubly linked list 1 
    // 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17 
    head = push(head, 17); 
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 9); 
    head = push(head, 10); 
    head = push(head, 16); 
    head = push(head, 15); 

    // create the doubly linked list 2 
    // 15 <. 16 <. 45 <. 9 <. 6 
    head1 = push(head1, 6); 
    head1 = push(head1, 9); 
    head1 = push(head1, 45); 
    head1 = push(head1, 16); 
    head1 = push(head1, 15); 

    Console.WriteLine("Number of common nodes: " +  
                   countCommonNodes(head, head1)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Number of common nodes:4

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。