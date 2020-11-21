# 从单链表中删除所有非主要节点

> 原文：[https://www.geeksforgeeks.org/delete-all-non-prime-nodes-from-a-singly-linked-list/](https://www.geeksforgeeks.org/delete-all-non-prime-nodes-from-a-singly-linked-list/)

给定一个包含`N`个节点的单链表，任务是从列表中删除不是素数的所有节点。

**示例**：

> **输入**：列表= 15-> 16-> 6-> 7-> 17
> **输出**：最终列表= 7-> 17
> 
> **输入**：列表= 15-> 3-> 4-> 2-> 9
> **输出**：最终列表= 3-> 2

**方法**：想法是一个遍历单链表的节点，并获得**不是素数**的节点的指针。 通过按照帖子中使用的方法删除这些节点：[从链表](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)中删除一个节点。

以下是上述想法的实现：

## C++

```cpp

// C++ implementation to delete all 
// non-prime nodes from the singly 
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
    Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
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

// function to delete all non-prime nodes 
// from the singly linked list 
void deleteNonPrimeNodes(Node** head_ref) 
{ 
    // Remove all composite nodes at the beginning 
    Node* ptr = *head_ref; 
    while (ptr != NULL && !isPrime(ptr->data)) 
    { 
       Node *temp = ptr; 
       ptr = ptr->next; 
       delete(temp); 
    } 
    *head_ref = ptr; 
    if (ptr == NULL) 
       return; 

    // Remove remaining nodes 
    Node *curr = ptr->next; 
    while (curr != NULL) { 

        if (!isPrime(curr->data)) 
        { 
            ptr->next = curr->next; 
            delete(curr); 
            curr = ptr->next; 
        } 
        else
        { 
            ptr = curr; 
            curr = curr->next; 
        } 
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

    deleteNonPrimeNodes(&head); 

    cout << "\nModified List: "; 
    printList(head); 
} 

```

## Java

```java

// Java implementation to delete all  
// non-prime nodes from the singly  
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
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
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

// function to delete all non-prime nodes  
// from the singly linked list  
static Node deleteNonPrimeNodes(Node head_ref)  
{  
    // Remove all composite nodes at the beginning  
    Node ptr = head_ref;  
    while (ptr != null && !isPrime(ptr.data))  
    {  
        Node temp = ptr;  
        ptr = ptr.next;  
    }  
    head_ref = ptr;  
    if (ptr == null)  
        return null;  

    // Remove remaining nodes  
    Node curr = ptr.next;  
    while (curr != null)  
    {  

        if (!isPrime(curr.data))  
        {  
            ptr.next = curr.next;  
            curr = ptr.next;  
        }  
        else
        {  
            ptr = curr;  
            curr = curr.next;  
        }  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given singly linked list  
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

    head = deleteNonPrimeNodes(head);  

    System.out.print("\nModified List: ");  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to delete all 
# non-prime nodes from the singly 
# linked list 
import math  

# Node of the singly linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to insert a node at the beginning 
# of the singly Linked List 
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
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
    if (n % 2 == 0 or n % 3 == 0): 
        return False
    for i in range(5, n + 1, 6): 
        if (i * i < n + 2 and 
           (n % i == 0 or n % (i + 2) == 0)): 
            return False

    return True

# function to delete all non-prime nodes 
# from the singly linked list 
def deleteNonPrimeNodes(head_ref): 

    # Remove all composite nodes at the beginning 
    ptr = head_ref 
    while (ptr != None and 
           isPrime(ptr.data)!= True): 
        temp = ptr 
        ptr = ptr.next
        # delete(temp) 

    head_ref = ptr 
    if (ptr == None): 
        return None

    # Remove remaining nodes 
    curr = ptr.next
    while (curr != None) : 

        if (isPrime(curr.data) != True): 
            ptr.next = curr.next
            #delete(curr) 
            curr = ptr.next

        else: 
            ptr = curr 
            curr = curr.next

        return head_ref      

# function to print nodes in a 
# given singly linked list 
def printList( head): 
    while (head != None) : 
        print(head.data, end = " ") 
        head = head.next

# Driver Code 
if __name__=='__main__':  

    # start with the empty list 
    head = None

    # create the linked list 
    # 15 -> 16 -> 7 -> 6 -> 17 
    head = push(head, 17) 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 16) 
    head = push(head, 15) 

    print("Original List: ") 
    printList(head) 

    head = deleteNonPrimeNodes(head) 

    print("\nModified List: ") 
    printList(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# implementation to delete all  
// non-prime nodes from the singly  
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
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Function to check if a number is prime  
    static bool isPrime(int n) 
    { 
        // Corner cases  
        if (n <= 1)  
        { 
            return false; 
        } 
        if (n <= 3)  
        { 
            return true; 
        } 

        // This is checked so that we can skip  
        // middle five numbers in below loop  
        if (n % 2 == 0 || n % 3 == 0)  
        { 
            return false; 
        } 

        for (int i = 5; i * i <= n; i = i + 6)  
        { 
            if (n % i == 0 || n % (i + 2) == 0) 
            { 
                return false; 
            } 
        } 
        return true; 
    } 

    // function to delete all non-prime nodes  
    // from the singly linked list  
    static Node deleteNonPrimeNodes(Node head_ref)  
    { 
        // Remove all composite nodes 
        // at the beginning  
        Node ptr = head_ref; 
        while (ptr != null && !isPrime(ptr.data)) 
        { 
            Node temp = ptr; 
            ptr = ptr.next; 
        } 
        head_ref = ptr; 
        if (ptr == null)  
        { 
            return null; 
        } 

        // Remove remaining nodes  
        Node curr = ptr.next; 
        while (curr != null)  
        { 
            if (!isPrime(curr.data)) 
            { 
                ptr.next = curr.next; 
                curr = ptr.next; 
            }  
            else 
            { 
                ptr = curr; 
                curr = curr.next; 
            } 
        } 
        return head_ref; 
    } 

    // function to print nodes in a  
    // given singly linked list  
    static void printList(Node head) 
    { 
        while (head != null)  
        { 
            Console.Write(head.data + " "); 
            head = head.next; 
        } 
    } 

    // Driver code  
    public static void Main(String[] args)  
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

        head = deleteNonPrimeNodes(head); 

        Console.Write("\nModified List: "); 
        printList(head); 
    } 
}  

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Original List: 15 16 6 7 17 
Modified List: 7 17

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。