# 从单个链接列表中删除所有主要节点

> 原文：[https://www.geeksforgeeks.org/delete-all-prime-nodes-from-a-singly-linked-list/](https://www.geeksforgeeks.org/delete-all-prime-nodes-from-a-singly-linked-list/)

给定一个包含 N 个节点的单链接列表，任务是从列表中删除所有素数的节点。

**示例**：

> **输入**：列表= 15-> 16-> 6-> 7-> 17
> **输出**：最终列表= 15-> 16-> 6
> 
> **输入**：列表= 15-> 3-> 4-> 2-> 9
> **输出**：最终列表= 15-> 4-> 9

**方法**：想法是逐个遍历单链接列表的节点并获得素数节点的指针。 通过遵循帖子中使用的方法删除那些节点：[从链接列表](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)中删除一个节点。

以下是上述想法的实现：

## C++

```cpp

// C++ implementation to delete all 
// prime nodes from the singly 
// linked list 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the singly linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to insert a node at the beginning 
// of the singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node = (Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to check if a number is prime 
bool isPrime(int n) 
{ 
    // Corner cases 
    if (n <= 1) 
        return false; 
    if (n <= 3) 
        return true; 

    // This is checked so that we can skip 
    // middle five numbers in below loop 
    if (n % 2 == 0 || n % 3 == 0) 
        return false; 

    for (int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return false; 

    return true; 
} 

// function to delete a node in a singly Linked List. 
// head_ref --> pointer to head node pointer. 
// del --> pointer to node to be deleted 
void deleteNode(Node** head_ref, Node* del) 
{ 
    // base case 
    struct Node* temp = *head_ref; 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 
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

// function to delete all prime nodes 
// from the singly linked list 
void deletePrimeNodes(Node** head_ref) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 

    while (ptr != NULL) { 
        next = ptr->next; 
        // if true, delete node 'ptr' 
        if (isPrime(ptr->data)) 
            deleteNode(head_ref, ptr); 
        ptr = next; 
    } 
} 

// function to print nodes in a 
// given singly linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the linked list 
    // 15 -> 16 -> 7 -> 6 -> 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 16); 
    push(&head, 15); 

    cout << "Original List: "; 
    printList(head); 

    deletePrimeNodes(&head); 

    cout << "\nModified List: "; 
    printList(head); 
} 

```

## Java

```java

// Java implementation to delete all  
// prime nodes from the singly  
// linked list  
class GFG 
{ 

// Node of the singly linked list  
static class Node  
{  
    int data;  
    Node next;  
};  

// function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to check if a number is prime  
static boolean isPrime(int n)  
{  
    // Corner cases  
    if (n <= 1)  
        return false;  
    if (n <= 3)  
        return true;  

    // This is checked so that we can skip  
    // middle five numbers in below loop  
    if (n % 2 == 0 || n % 3 == 0)  
        return false;  

    for (int i = 5; i * i <= n; i = i + 6)  
        if (n % i == 0 || n % (i + 2) == 0)  
            return false;  

    return true;  
}  

// function to delete a node in a singly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    Node temp = head_ref;  
    if (head_ref == null || del == null)  
        return null;  

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

// function to delete all prime nodes  
// from the singly linked list  
static Node deletePrimeNodes(Node head_ref)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null) 
    {  
        next = ptr.next;  

        // if true, delete node 'ptr'  
        if (isPrime(ptr.data))  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given singly linked list  
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

    // create the linked list  
    // 15 . 16 . 7 . 6 . 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 16);  
    head = push(head, 15);  

    System.out.print("Original List: ");  
    printList(head);  

    head = deletePrimeNodes(head);  

    System.out.print("\nModified List: ");  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to delete all 
# prime nodes from the singly 
# linked list 

# Node class  
class Node:  

    # Constructor to initialize  
    # the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to insert a node at the beginning 
# of the singly Linked List 
def push(head_ref, new_data): 

    # allocate node 
    new_node = Node(0) 

    # put in the data 
    new_node.data = new_data 

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # move the head to point to the new node 
    (head_ref) = new_node 

    return head_ref 

# Function to check if a number is prime 
def isPrime(n): 

    # Corner cases 
    if (n <= 1): 
        return False
    if (n <= 3): 
        return True

    # This is checked so that we can skip 
    # middle five numbers in below loop 
    if (n % 2 == 0) or (n % 3 == 0) : 
        return False

    i = 6
    while( i * i <= n ): 
        if (n % i == 0 or n % (i + 2) == 0): 
            return False
        i = i + 6

    return True

# function to delete a node in a singly Linked List. 
# head_ref -. pointer to head node pointer. 
# del -. pointer to node to be deleted 
def deleteNode(head_ref, del1): 

    # base case 
    temp = head_ref 
    if (head_ref == None or del1 == None): 
        return

    # If node to be deleted is head node 
    if (head_ref == del1): 
        head_ref = del1.next

    # traverse list till not found 
    # delete node 
    while (temp.next != del1) : 
        temp = temp.next

    # copy address of node 
    temp.next = del1.next

    return head_ref; 

# function to delete all prime nodes 
# from the singly linked list 
def deletePrimeNodes(head_ref): 

    ptr = head_ref 
    next = None

    while (ptr != None) : 
        next = ptr.next

        # if True, delete node 'ptr' 
        if (isPrime(ptr.data)): 
            head_ref = deleteNode(head_ref, ptr) 
        ptr = next
    return head_ref 

# function to print nodes in a 
# given singly linked list 
def printList(head): 

    while (head != None) : 
        print(head.data, " ", end = " ") 
        head = head.next

# Driver Code 
if __name__=='__main__':  

    # start with the empty list 
    head = None

    # create the linked list 
    # 15 . 16 . 7 . 6 . 17 
    head = push(head, 17) 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 16) 
    head = push(head, 15) 

    print( "Original List: ") 
    printList(head) 

    head = deletePrimeNodes(head) 

    print("\nModified List: ") 
    printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to delete all  
// prime nodes from the singly  
// linked list  
using System; 

class GFG  
{  

// Node of the singly linked list  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Function to check if a number is prime  
static bool isPrime(int n)  
{  
    // Corner cases  
    if (n <= 1)  
        return false;  
    if (n <= 3)  
        return true;  

    // This is checked so that we can skip  
    // middle five numbers in below loop  
    if (n % 2 == 0 || n % 3 == 0)  
        return false;  

    for (int i = 5; i * i <= n; i = i + 6)  
        if (n % i == 0 || n % (i + 2) == 0)  
            return false;  

    return true;  
}  

// function to delete a node in a singly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    Node temp = head_ref;  
    if (head_ref == null || del == null)  
        return null;  

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

// function to delete all prime nodes  
// from the singly linked list  
static Node deletePrimeNodes(Node head_ref)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null)  
    {  
        next = ptr.next;  

        // if true, delete node 'ptr'  
        if (isPrime(ptr.data))  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref;  
}  

// function to print nodes in a  
// given singly linked list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main()  
{  
    // start with the empty list  
    Node head = null;  

    // create the linked list  
    // 15 . 16 . 7 . 6 . 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 16);  
    head = push(head, 15);  

    Console.Write("Original List: ");  
    printList(head);  

    head = deletePrimeNodes(head);  

    Console.Write("\nModified List: ");  
    printList(head);  
}  
}  

// This code is contributed by Princi Singh 

```

**Output:**

```
Original List: 15 16 6 7 17 
Modified List: 15 16 6

```

**时间复杂度：`O(n)`**，其中 N 是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。