# 循环链表

> 原文：[https://www.geeksforgeeks.org/count-nodes-circular-linked-list/](https://www.geeksforgeeks.org/count-nodes-circular-linked-list/)

中的节点计数

给定一个循环链表，计算其中的节点数。 例如，以下列表的输出为 5。

![](img/703b24f6bea34bab0d870162e6b29efb.png "cll")

我们使用[循环链表|中的概念。 集合 2（Traversal）](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)。 在遍历时，我们会跟踪节点数。

## C / C++

```cpp

// C program to count number of nodes in 
// a circular linked list. 
#include <stdio.h> 
#include <stdlib.h> 

/* structure for a node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to insert a node at the beginning 
   of a Circular linked list */
void push(struct Node** head_ref, int data) 
{ 
    struct Node* ptr1 = (struct Node*)malloc(sizeof(struct Node)); 
    struct Node* temp = *head_ref; 
    ptr1->data = data; 
    ptr1->next = *head_ref; 

    /* If the linked list is not NULL then set 
       the next of last node */
    if (*head_ref != NULL) { 
        while (temp->next != *head_ref) 
            temp = temp->next; 
        temp->next = ptr1; 
    } else
        ptr1->next = ptr1; /*For the first node */

    *head_ref = ptr1; 
} 

/* Function to print nodes in a given Circular 
   linked list */
int countNodes(struct Node* head) 
{ 
    struct Node* temp = head; 
    int result = 0; 
    if (head != NULL) { 
        do { 
            temp = temp->next; 
            result++; 
        } while (temp != head); 
    } 

    return result; 
} 

/* Driver program to test above functions */
int main() 
{ 
    /* Initialize lists as empty */
    struct Node* head = NULL; 
    push(&head, 12); 
    push(&head, 56); 
    push(&head, 2); 
    push(&head, 11); 

    printf("%d", countNodes(head)); 

    return 0; 
} 

```

## Java

```java

// Java program to count number of nodes in  
// a circular linked list.  
class GFG 
{ 

/* ure for a node */
static class Node 
{  
    int data;  
    Node next;  
};  

/* Function to insert a node at the beginning  
of a Circular linked list */
static Node push( Node head_ref, int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    /* If linked list is not null then set  
    the next of last node */
    if (head_ref != null) 
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
    } else
        ptr1.next = ptr1; /*For the first node */

    head_ref = ptr1; 
    return head_ref; 
}  

/* Function to print nodes in a given Circular  
linked list */
static int countNodes( Node head)  
{  
    Node temp = head;  
    int result = 0;  
    if (head != null) 
    {  
        do 
        {  
            temp = temp.next;  
            result++;  
        } while (temp != head);  
    }  

    return result;  
}  

/* Driver program to test above functions */
public static void main(String args[]) 
{  
    /* Initialize lists as empty */
    Node head = null;  
    head = push(head, 12);  
    head = push(head, 56);  
    head = push(head, 2);  
    head = push(head, 11);  

    System.out.printf("%d", countNodes(head));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to count number of nodes in 
# a circular linked list. 

# structure for a node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the beginning 
# of a Circular linked list */ 
def push(head_ref,data): 

    ptr1 = Node(0) 
    temp = head_ref 
    ptr1.data = data 
    ptr1.next = head_ref 

    # If the linked list is not None then set 
    # the next of last node  
    if (head_ref != None) : 
        while (temp.next != head_ref): 
            temp = temp.next
        temp.next = ptr1 
    else: 
        ptr1.next = ptr1 #For the first node */ 

    head_ref = ptr1 
    return head_ref 

# Function to print nodes  
# in a given Circular linked list  
def countNodes(head): 

    temp = head 
    result = 0
    if (head != None) : 
        while True : 
            temp = temp.next
            result = result + 1
            if (temp == head): 
                break

    return result 

# Driver Code  
if __name__=='__main__':  

    # Initialize lists as empty */ 
    head = None
    head = push(head, 12) 
    head = push(head, 56) 
    head = push(head, 2) 
    head = push(head, 11) 

    print( countNodes(head)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to count number of nodes in  
// a circular linked list.  
using System; 

class GFG  
{  

/* structure for a node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to insert a node at the beginning  
of a Circular linked list */
static Node push( Node head_ref, int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    /* If linked list is not null then set  
    the next of last node */
    if (head_ref != null)  
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
    } else
        ptr1.next = ptr1; /*For the first node */

    head_ref = ptr1;  
    return head_ref;  
}  

/* Function to print nodes in a given Circular  
linked list */
static int countNodes( Node head)  
{  
    Node temp = head;  
    int result = 0;  
    if (head != null)  
    {  
        do
        {  
            temp = temp.next;  
            result++;  
        } while (temp != head);  
    }  

    return result;  
}  

/* Driver code */
public static void Main(String []args)  
{  
    /* Initialize lists as empty */
    Node head = null;  
    head = push(head, 12);  
    head = push(head, 56);  
    head = push(head, 2);  
    head = push(head, 11);  

    Console.Write( countNodes(head));  
}  
}  

// This code is contributed by Arnab Kundu  

```

```
4

```

本文由 **Rishabh jain** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

