# 从链表中删除最后一次出现的项目

> 原文：[https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/](https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/)

遍历整个列表，并使用双指针跟踪包含最后出现节点地址的节点。

```

#include <stdio.h> 
#include <stdlib.h> 

// A linked list Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to delete the last occurrence 
void deleteLast(struct Node** head, int x) 
{ 
        struct Node** tmp1 = NULL; 
        while(*head) { 
                if((*head)->data == x) { 
                        tmp1 = head; 
                } 
                head = &(*head)->next; 
        } 
        if(tmp1) { 
                struct Node* tmp = *tmp1; 
                *tmp1 = tmp->next; 
                free(tmp); 
        } 
} 

/* Utility function to create a new node with 
given key */
struct Node* newNode(int x) 
{ 
    struct Node* node = malloc(sizeof(struct Node*)); 
    node->data = x; 
    node->next = NULL; 
    return node; 
} 

// This function prints contents of linked list 
// starting from the given Node 
void display(struct Node* head) 
{ 
    struct Node* temp = head; 
    if (head == NULL) { 
        printf("NULL\n"); 
        return; 
    } 
    while (temp != NULL) { 
        printf("%d --> ", temp->data); 
        temp = temp->next; 
    } 
    printf("NULL\n"); 
} 

/* Driver program to test above functions*/
int main() 
{ 
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 
    head->next->next->next->next->next = newNode(4); 
    head->next->next->next->next->next->next = newNode(4); 
    printf("Created Linked list: "); 
    display(head); 
    deleteLast(&head, 4);   // Pass the address of the head pointer 
    printf("List after deletion of 4: "); 
    display(head); 
    return 0; 
} 

```

给定喜欢的列表和要删除的键。 从链接中删除最后一次出现的键。 该列表可能有重复项。

例子：

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

这个想法是从头到尾遍历链表。 遍历时，请跟踪最后出现的关键字。 遍历完整列表后，通过复制下一个节点的数据并删除下一个节点来删除最后一个出现的节点。

## C++

```cpp

// A C++ program to demonstrate deletion of last 
// Node in singly linked list 
#include <bits/stdc++.h> 

// A linked list Node 
struct Node { 
    int key; 
    struct Node* next; 
}; 

void deleteLast(Node* head, int key) 
{ 
    // Initialize previous of Node to be deleted 
    Node* x = NULL; 

    // Start from head and find the Node to be 
    // deleted 
    Node* temp = head; 
    while (temp) { 
        // If we found the key, update xv 
        if (temp->key == key) 
            x = temp; 

        temp = temp->next; 
    } 

    // key occurs at-least once 
    if (x != NULL) { 

        // Copy key of next Node to x 
        x->key = x->next->key; 

        // Store and unlink next 
        temp = x->next; 
        x->next = x->next->next; 

        // Free memory for next 
        delete temp; 
    } 
} 

/* Utility function to create a new node with 
   given key */
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->key = key; 
    temp->next = NULL; 
    return temp; 
} 

// This function prints contents of linked list 
// starting from the given Node 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf(" %d ", node->key); 
        node = node->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(5); 
    head->next->next->next->next = newNode(2); 
    head->next->next->next->next->next = newNode(10); 

    puts("Created Linked List: "); 
    printList(head); 
    deleteLast(head, 2); 
    puts("\nLinked List after Deletion of 1: "); 
    printList(head); 
    return 0; 
} 

```

## Java

```java

// A Java program to demonstrate deletion of last  
// Node in singly linked list  
class GFG 
{ 

// A linked list Node  
static class Node  
{  
    int key;  
    Node next;  
};  

static Node deleteLast(Node head, int key)  
{  
    // Initialize previous of Node to be deleted  
    Node x = null;  

    // Start from head and find the Node to be  
    // deleted  
    Node temp = head;  
    while (temp != null)  
    {  
        // If we found the key, update xv  
        if (temp.key == key)  
            x = temp;  

        temp = temp.next;  
    }  

    // key occurs at-least once  
    if (x != null)  
    {  

        // Copy key of next Node to x  
        x.key = x.next.key;  

        // Store and unlink next  
        temp = x.next;  
        x.next = x.next.next;  

        // Free memory for next  
    }  
    return head; 
}  

/// Utility function to create a new node with  
//given key / 
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.key = key;  
    temp.next = null;  
    return temp;  
}  

// This function prints contents of linked list  
// starting from the given Node  
static void printList( Node node)  
{  
    while (node != null)  
    {  
        System.out.printf(" %d ", node.key);  
        node = node.next;  
    }  
}  

// Driver code/ 
public static void main(String args[]) 
{  
    // /Start with the empty list / 
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(5);  
    head.next.next.next.next = newNode(2);  
    head.next.next.next.next.next = newNode(10);  

    System.out.printf("Created Linked List: ");  
    printList(head);  
    deleteLast(head, 2);  
    System.out.printf("\nLinked List after Deletion of 1: ");  
    printList(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to demonstrate deletion of  
# last Node in singly linked list  

# A linked list Node  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

def deleteLast(head, key) : 

    # Initialize previous of Node to be deleted  
    x = None

    # Start from head and find the Node to be  
    # deleted  
    temp = head  
    while (temp != None) : 

        # If we found the key, update xv  
        if (temp.key == key) : 
            x = temp  

        temp = temp.next

    # key occurs at-least once  
    if (x != None) : 

        # Copy key of next Node to x  
        x.key = x.next.key  

        # Store and unlink next  
        temp = x.next
        x.next = x.next.next

        # Free memory for next  

    return head 

# Utility function to create  
# a new node with given key  
def newNode(key) : 

    temp = Node(0)  
    temp.key = key  
    temp.next = None
    return temp  

# This function prints contents of linked list  
# starting from the given Node  
def printList( node) : 

    while (node != None) : 

        print ( node.key, end = " ")  
        node = node.next

# Driver Code  
if __name__=='__main__':  

    # Start with the empty list  
    head = newNode(1)  
    head.next = newNode(2)  
    head.next.next = newNode(3)  
    head.next.next.next = newNode(5)  
    head.next.next.next.next = newNode(2)  
    head.next.next.next.next.next = newNode(10)  

    print("Created Linked List: ")  
    printList(head)  
    deleteLast(head, 2)  

    print("\nLinked List after Deletion of 1: ")  
    printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to demonstrate deletion of last  
// Node in singly linked list  
using System; 

class GFG  
{  

// A linked list Node  
public class Node  
{  
    public int key;  
    public Node next;  
};  

static Node deleteLast(Node head, int key)  
{  
    // Initialize previous of Node to be deleted  
    Node x = null;  

    // Start from head and find the Node to be  
    // deleted  
    Node temp = head;  
    while (temp != null)  
    {  
        // If we found the key, update xv  
        if (temp.key == key)  
            x = temp;  

        temp = temp.next;  
    }  

    // key occurs at-least once  
    if (x != null)  
    {  

        // Copy key of next Node to x  
        x.key = x.next.key;  

        // Store and unlink next  
        temp = x.next;  
        x.next = x.next.next;  

        // Free memory for next  
    }  
    return head;  
}  

/// Utility function to create a new node with  
//given key /  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.key = key;  
    temp.next = null;  
    return temp;  
}  

// This function prints contents of linked list  
// starting from the given Node  
static void printList( Node node)  
{  
    while (node != null)  
    {  
        Console.Write(" {0} ", node.key);  
        node = node.next;  
    }  
}  

// Driver code 
public static void Main(String []args)  
{  
    // Start with the empty list  
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(5);  
    head.next.next.next.next = newNode(2);  
    head.next.next.next.next.next = newNode(10);  

    Console.Write("Created Linked List: ");  
    printList(head);  
    deleteLast(head, 2);  
    Console.Write("\nLinked List after Deletion of 1: ");  
    printList(head);  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
Created Linked List: 
 1  2  3  5  2  10 
Linked List after Deletion of 1: 
 1  2  3  5  10
```

**当要删除的节点是最后一个节点时，以上解决方案不起作用。**

以下解决方案可处理所有情况。

## C/C++ 

```cpp

// A C program to demonstrate deletion of last 
// Node in singly linked list 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to delete the last occurrence 
void deleteLast(struct Node* head, int x) 
{ 
    struct Node *temp = head, *ptr = NULL; 
    while (temp) { 

        // If found key, update 
        if (temp->data == x)  
            ptr = temp;         
        temp = temp->next; 
    } 

    // If the last occurrence is the last node 
    if (ptr != NULL && ptr->next == NULL) { 
        temp = head; 
        while (temp->next != ptr)  
            temp = temp->next;        
        temp->next = NULL; 
    } 

    // If it is not the last node 
    if (ptr != NULL && ptr->next != NULL) { 
        ptr->data = ptr->next->data; 
        temp = ptr->next; 
        ptr->next = ptr->next->next; 
        free(temp); 
    } 
} 

/* Utility function to create a new node with 
given key */
struct Node* newNode(int x) 
{ 
    struct Node* node = malloc(sizeof(struct Node*)); 
    node->data = x; 
    node->next = NULL; 
    return node; 
} 

// This function prints contents of linked list 
// starting from the given Node 
void display(struct Node* head) 
{ 
    struct Node* temp = head; 
    if (head == NULL) { 
        printf("NULL\n"); 
        return; 
    } 
    while (temp != NULL) { 
        printf("%d --> ", temp->data); 
        temp = temp->next; 
    } 
    printf("NULL\n"); 
} 

/* Driver program to test above functions*/
int main() 
{ 
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 
    head->next->next->next->next->next = newNode(4); 
    head->next->next->next->next->next->next = newNode(4); 
    printf("Created Linked list: "); 
    display(head); 
    deleteLast(head, 4); 
    printf("List after deletion of 4: "); 
    display(head); 
    return 0; 
}

```

## Java

```java

// Java program to demonstrate deletion of last  
// Node in singly linked list  
class GFG  
{ 

// A linked list Node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to delete the last occurrence  
static void deleteLast(Node head, int x)  
{  
    Node temp = head, ptr = null;  
    while (temp!=null)  
    {  

        // If found key, update  
        if (temp.data == x)  
            ptr = temp;      
        temp = temp.next;  
    }  

    // If the last occurrence is the last node  
    if (ptr != null && ptr.next == null)  
    {  
        temp = head;  
        while (temp.next != ptr)  
            temp = temp.next;  
        temp.next = null;  
    }  

    // If it is not the last node  
    if (ptr != null && ptr.next != null) 
    {  
        ptr.data = ptr.next.data;  
        temp = ptr.next;  
        ptr.next = ptr.next.next;  
        System.gc(); 
    }  
}  

/* Utility function to create a new node with  
given key */
static Node newNode(int x)  
{  
    Node node = new Node();  
    node.data = x;  
    node.next = null;  
    return node;  
}  

// This function prints contents of linked list  
// starting from the given Node  
static void display(Node head)  
{  
    Node temp = head;  
    if (head == null)  
    {  
        System.out.print("null\n");  
        return;  
    }  
    while (temp != null)  
    {  
        System.out.printf("%d --> ", temp.data);  
        temp = temp.next;  
    }  
    System.out.print("null\n");  
}  

/* Driver code*/
public static void main(String[] args)  
{ 
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  
    head.next.next.next.next.next = newNode(4);  
    head.next.next.next.next.next.next = newNode(4);  
    System.out.print("Created Linked list: ");  
    display(head);  
    deleteLast(head, 4);  
    System.out.print("List after deletion of 4: ");  
    display(head);  
} 
} 

/* This code is contributed by PrinciRaj1992 */

```

## Python

```py

# A Python program to demonstrate deletion of last 
# Node in singly linked list 

# A linked list Node 
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None

# Function to delete the last occurrence 
def deleteLast(head, x): 

    temp = head 
    ptr = None
    while (temp!=None):  

        # If found key, update 
        if (temp.data == x) : 
            ptr = temp      
        temp = temp.next

    # If the last occurrence is the last node 
    if (ptr != None and ptr.next == None):  
        temp = head 
        while (temp.next != ptr) : 
            temp = temp.next    
        temp.next = None

    # If it is not the last node 
    if (ptr != None and ptr.next != None):  
        ptr.data = ptr.next.data 
        temp = ptr.next
        ptr.next = ptr.next.next

    return head 

# Utility function to create a new node with 
# given key  
def newNode(x): 

    node = Node(0) 
    node.data = x 
    node.next = None
    return node 

# This function prints contents of linked list 
# starting from the given Node 
def display( head): 

    temp = head 
    if (head == None):  
        print("None\n") 
        return

    while (temp != None):  
        print( temp.data," -> ",end="") 
        temp = temp.next

    print("None") 

# Driver code 

head = newNode(1) 
head.next = newNode(2) 
head.next.next = newNode(3) 
head.next.next.next = newNode(4) 
head.next.next.next.next = newNode(5) 
head.next.next.next.next.next = newNode(4) 
head.next.next.next.next.next.next = newNode(4) 
print("Created Linked list: ") 
display(head) 
head = deleteLast(head, 4) 
print("List after deletion of 4: ") 
display(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to demonstrate deletion of last  
// Node in singly linked list  
using System; 

class GFG  
{ 

// A linked list Node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to delete the last occurrence  
static void deleteLast(Node head, int x)  
{  
    Node temp = head, ptr = null;  
    while (temp != null)  
    {  

        // If found key, update  
        if (temp.data == x)  
            ptr = temp;      
        temp = temp.next;  
    }  

    // If the last occurrence is the last node  
    if (ptr != null && ptr.next == null)  
    {  
        temp = head;  
        while (temp.next != ptr)  
            temp = temp.next;  
        temp.next = null;  
    }  

    // If it is not the last node  
    if (ptr != null && ptr.next != null) 
    {  
        ptr.data = ptr.next.data;  
        temp = ptr.next;  
        ptr.next = ptr.next.next;  
    }  
}  

/* Utility function to create a new node with  
given key */
static Node newNode(int x)  
{  
    Node node = new Node();  
    node.data = x;  
    node.next = null;  
    return node;  
}  

// This function prints contents of linked list  
// starting from the given Node  
static void display(Node head)  
{  
    Node temp = head;  
    if (head == null)  
    {  
        Console.Write("null\n");  
        return;  
    }  
    while (temp != null)  
    {  
        Console.Write("{0} --> ", temp.data);  
        temp = temp.next;  
    }  
    Console.Write("null\n");  
}  

/* Driver code*/
public static void Main(String[] args)  
{ 
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  
    head.next.next.next.next.next = newNode(4);  
    head.next.next.next.next.next.next = newNode(4);  
    Console.Write("Created Linked list: ");  
    display(head);  
    deleteLast(head, 4);  
    Console.Write("List after deletion of 4: ");  
    display(head);  
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Created Linked List: 
 1  2  3  4  5  4  4 
Linked List after Deletion of 1: 
 1  2  3  4  5  4
```

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

