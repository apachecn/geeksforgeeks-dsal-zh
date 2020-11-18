# 使用递归

从排序的链表中删除重复项

编写一个 removeDuplicates（）函数，该函数采用以非降序排序的列表，并从列表中删除所有重复的节点。 该列表仅应遍历一次。

例如，如果链接列表是 11-> 11-> 11-> 21-> 43-> 43-> 60，则 removeDuplicates（）应该将列表转换为 11-> 21-> 43-> 60。

**算法：**

从头（或头）递归遍历列表，在完成递归调用后，比较下一个节点（返回的节点）和当前节点（头）。 如果两个节点的数据相等，则返回下一个**（头为>），否则返回当前**节点（头）**。**

**实现：**

除了 removeDuplicates（）以外的功能仅用于创建链接链表并测试 removeDuplicates（）。

## C++

```cpp

/* C Program to remove duplicates 
 from a sorted linked list */
#include <bits/stdc++.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* The function removes duplicates from a sorted list */
struct Node* removeDuplicates(struct Node* head) 
{ 
    /* if head is null then return*/
    if (head == NULL) 
        return NULL; 

    /* Remove duplicates from list after head */
    head->next = removeDuplicates(head->next); 

    // Check if head itself is duplicate 
    if (head->next != NULL &&  
        head->next->data == head->data) { 

        Node* res = head->next; 
        delete head; 
        return res; 
    } 

    return head; 
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at  
   the beginning of the linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create a sorted linked list to test the functions 
    Created linked list will be 11->11->11->13->13->20 */
    push(&head, 20); 
    push(&head, 13); 
    push(&head, 13); 
    push(&head, 11); 
    push(&head, 11); 
    push(&head, 11); 

    printf("\n Linked list before duplicate removal "); 
    printList(head); 

    /* Remove duplicates from linked list */
    struct Node* h = removeDuplicates(head); 

    printf("\n Linked list after duplicate removal "); 
    printList(h); 

    return 0; 
} 

```

## Java

```java

/* Java Program to remove duplicates  
from a sorted linked list */
class GFG  
{ 

/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
};  

/* The function removes duplicates from a sorted list */
static Node removeDuplicates( Node head)  
{  
    /* if head is null then return*/
    if (head == null)  
        return null;  

    /* Remove duplicates from list after head */
    head.next = removeDuplicates(head.next);  

    // Check if head itself is duplicate  
    if (head.next != null &&  
        head.next.data == head.data) 
    {  

        Node res = head.next;  

        return res;  
    }  

    return head;  
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at  
the beginning of the linked list */
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

/* Function to print nodes in a given linked list */
static void printList( Node node)  
{  
    while (node != null)  
    {  
        System.out.printf("%d ", node.data);  
        node = node.next;  
    }  
}  

/* Driver program to test above functions*/
public static void main(String args[])  
{  
    /* Start with the empty list */
    Node head = null;  

    /* Let us create a sorted linked list to test the functions  
    Created linked list will be 11.11.11.13.13.20 */
    head = push(head, 20);  
    head = push(head, 13);  
    head = push(head, 13);  
    head = push(head, 11);  
    head = push(head, 11);  
    head = push(head, 11);  

    System.out.printf("\n Linked list before duplicate removal ");  
    printList(head);  

    /* Remove duplicates from linked list */
    Node h = removeDuplicates(head);  

    System.out.printf("\n Linked list after duplicate removal ");  
    printList(h);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python Program to remove duplicates  
# from a sorted linked list  

# A linked list node 
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None

# The function removes duplicates from a sorted list  
def removeDuplicates( head) : 

    # if head is None then return 
    if (head == None) : 
        return None

    # Remove duplicates from list after head  
    head.next = removeDuplicates(head.next)  

    # Check if head itself is duplicate  
    if (head.next != None and
        head.next.data == head.data): 
        res = head.next

        return res  

    return head  

# UTILITY FUNCTIONS  
# Function to insert a node at  
#the beginning of the linked list  
def push( head_ref, new_data) : 
    new_node = Node(0)  
    new_node.data = new_data  
    new_node.next = (head_ref)  
    (head_ref) = new_node 
    return head_ref 

# Function to print nodes in a given linked list  
def printList(node) : 

    while (node != None) : 

        print(node.data,end=" ")  
        node = node.next

# Driver program to test above functions 

# Start with the empty list  
head = None

# Let us create a sorted linked list to test the functions  
# Created linked list will be 11.11.11.13.13.20  
head = push(head, 20)  
head = push(head, 13)  
head = push(head, 13)  
head = push(head, 11)  
head = push(head, 11)  
head = push(head, 11)  

print("\n Linked list before duplicate removal ")  
printList(head)  

# Remove duplicates from linked list  
h = removeDuplicates(head)  

print("\n Linked list after duplicate removal ")  
printList(h)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

/* C# Program to remove duplicates  
from a sorted linked list */
using System; 

class GFG  
{ 

    /* Link list node */
    public class Node  
    {  
        public int data;  
        public Node next;  
    };  

    /* The function removes duplicates from a sorted list */
    static Node removeDuplicates( Node head)  
    {  
        /* if head is null then return*/
        if (head == null)  
            return null;  

        /* Remove duplicates from list after head */
        head.next = removeDuplicates(head.next);  

        // Check if head itself is duplicate  
        if (head.next != null &&  
            head.next.data == head.data) 
        {  

            Node res = head.next;  

            return res;  
        }  

        return head;  
    }  

    /* UTILITY FUNCTIONS */
    /* Function to insert a node at  
    the beginning of the linked list */
    static Node push( Node head_ref, int new_data)  
    {  
        Node new_node = new Node();  
        new_node.data = new_data;  
        new_node.next = (head_ref);  
        (head_ref) = new_node; 
        return head_ref; 
    }  

    /* Function to print nodes in a given linked list */
    static void printList( Node node)  
    {  
        while (node != null)  
        {  
            Console.Write("{0} ", node.data);  
            node = node.next;  
        }  
    }  

    /* Driver program to test above functions*/
    public static void Main(String []args)  
    {  
        /* Start with the empty list */
        Node head = null;  

        /* Let us create a sorted linked list to test the functions  
        Created linked list will be 11.11.11.13.13.20 */
        head = push(head, 20);  
        head = push(head, 13);  
        head = push(head, 13);  
        head = push(head, 11);  
        head = push(head, 11);  
        head = push(head, 11);  

        Console.Write("\n Linked list before duplicate removal ");  
        printList(head);  

        /* Remove duplicates from linked list */
        Node h = removeDuplicates(head);  

        Console.Write("\n Linked list after duplicate removal ");  
        printList(h);  
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Linked list before duplicate removal 11 11 11 13 13 20 
 Linked list after duplicate removal 11 13 20

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。