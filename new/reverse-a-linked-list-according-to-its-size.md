# 根据其大小反向链表

> 原文：[https://www.geeksforgeeks.org/reverse-a-linked-list-according-to-its-size/](https://www.geeksforgeeks.org/reverse-a-linked-list-according-to-its-size/)

给定具有`n`个节点的链表，请按以下方式将其反向：

1.  如果`n`为偶数，则将其反转为`n / 2`个节点。

2.  如果`n`为奇数，则保持中间节点不变，反转前`n / 2`个元素，反转后`n / 2`个元素。

例子：

> 输入：`1 2 3 4 5 6`（`n`为偶数）
>
> 输出：`3 2 1 6 5 4`
> 
> 输入：`1 2 3 4 5 6 7`（`n`为奇数）
>
> 输出：`3 2 1 4 7 6 5`

**方法**：这个想法类似于[反转大小为`k`的组中的链表](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)，其中`k`为`n / 2`。 只需要检查中间节点。

*   如果`n`为偶数，则将链表分为两部分，即前`n / 2`个元素和后`n / 2`个元素，并将这两个部分取反。

*   如果`n`为奇数，则将链表分为三部分，即前`n / 2`个元素，第`n / 2 + 1`个元素和后`n / 2`个元素，并反转除第`n / 2 + 1`个元素之外的两个部分。

## C++

```cpp

// C++ program to reverse given 
// linked list according to its size 
#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    Node* next; 
}; 

// Function to create a new Node 
Node* newNode(int data) 
{ 
    Node *temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Prints a list. 
void printList(Node* head) 
{ 
    Node *temp = head; 
    while (temp) { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
    cout << endl; 
} 

/* Function to push a Node */
void push(Node** head_ref, int new_data) 
{ 
    Node* new_Node = new Node; 
    new_Node->data = new_data; 
    new_Node->next = (*head_ref); 
    (*head_ref) = new_Node; 
} 

// Returns size of list. 
int getSize(Node* head) 
{ 
    Node* curr = head; 
    int count = 0; 
    while (curr) { 
        curr = curr->next; 
        count++; 
    } 
    return count; 
} 

// Function to reverse the linked 
// list according to its size 
Node* reverseSizeBy2Util(Node* head, int k,  
                            bool skipMiddle) 
{ 
    if (!head) 
        return NULL; 

    int count = 0; 
    Node* curr = head; 
    Node* prev = NULL; 
    Node* next; 

    // Reverse current block of list. 
    while (curr && count < k) { 
        next = curr->next; 
        curr->next = prev; 
        prev = curr; 
        curr = next; 
        count++; 
    } 

    // If size is even, reverse next block too. 
    if (!skipMiddle) 
        head->next = reverseSizeBy2Util(next, k, false); 

    else { 

        // if size is odd, skip next element 
        // and reverse the block after that. 
        head->next = next; 
        if (next) 
            next->next = reverseSizeBy2Util(next->next, 
                                              k, true); 
    } 
    return prev; 
} 

Node* reverseBySizeBy2(Node* head) 
{ 
    // Get the size of list. 
    int n = getSize(head); 

    // If the size is even, no need 
    // to skip middle Node. 
    if (n % 2 == 0) 
        return reverseSizeBy2Util(head, n/2, false); 

    // If size is odd, middle Node has 
    // to be skipped. 
    else
        return reverseSizeBy2Util(head, n/2, true); 
} 

// Drivers code 
int main() 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    /* Created Linked list is 1->2->3->4->5->6->7->8->9 */
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    cout << "Original List : "; 
    printList(head); 

    cout << "Reversed List : "; 
    Node* reversedHead = reverseBySizeBy2(head); 
    printList(reversedHead); 

    return 0; 
} 

```

## Java

```java

// Java program to reverse given  
// linked list according to its size  
class GFG 
{ 

static class Node 
{  
    int data;  
    Node next;  
};  

// Function to create a new Node  
static Node newNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  

// Prints a list.  
static void printList(Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        System.out.print( temp.data + " ");  
        temp = temp.next;  
    } System.out.println(); 
}  

// Function to push a Node  
static Node push(Node head_ref, int new_data)  
{  
    Node new_Node = new Node();  
    new_Node.data = new_data;  
    new_Node.next = (head_ref);  
    (head_ref) = new_Node;  
    return head_ref; 
}  

// Returns size of list.  
static int getSize(Node head)  
{  
    Node curr = head;  
    int count = 0;  
    while (curr != null) 
    {  
        curr = curr.next;  
        count++;  
    }  
    return count;  
}  

// Function to reverse the linked  
// list according to its size  
static Node reverseSizeBy2Util(Node head, int k,  
                            boolean skipMiddle)  
{  
    if (head == null)  
        return null;  

    int count = 0;  
    Node curr = head;  
    Node prev = null;  
    Node next=null;  

    // Reverse current block of list.  
    while (curr!=null && count < k) 
    {  
        next = curr.next;  
        curr.next = prev;  
        prev = curr;  
        curr = next;  
        count++;  
    }  

    // If size is even, reverse next block too.  
    if (!skipMiddle)  
        head.next = reverseSizeBy2Util(next, k, false);  

    else 
    {  

        // if size is odd, skip next element  
        // and reverse the block after that.  
        head.next = next;  
        if (next != null)  
            next.next = reverseSizeBy2Util(next.next,  
                                            k, true);  
    }  
    return prev;  
}  

static Node reverseBySizeBy2(Node head)  
{  
    // Get the size of list.  
    int n = getSize(head);  

    // If the size is even, no need  
    // to skip middle Node.  
    if (n % 2 == 0)  
        return reverseSizeBy2Util(head, n/2, false);  

    // If size is odd, middle Node has  
    // to be skipped.  
    else
        return reverseSizeBy2Util(head, n/2, true);  
}  

// Driver code  
public static void main(String args[])  
{  
    // Start with the empty list / 
    Node head = null;  

    // Created Linked list is 1.2.3.4.5.6.7.8.9 / 
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    System.out.print( "Original List : ");  
    printList(head);  

    System.out.print( "Reversed List : ");  
    Node reversedHead = reverseBySizeBy2(head);  
    printList(reversedHead);  
} 
} 

// This code is contributed by Arnab Kundu  

```

## Python3

```py

# Python3 program to reverse given  
# linked list according to its size  

class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# Prints a list.  
def printList(head):  

    temp = head  
    while temp:   
        print(temp.data, end = " ")  
        temp = temp.next 

    print() 

# Function to push a Node  
def push(head_ref, new_data):  

    new_Node = Node(new_data)  
    new_Node.next = head_ref  
    head_ref = new_Node 

    return head_ref 

# Returns size of list.  
def getSize(head): 

    curr = head  
    count = 0 
    while curr:   
        curr = curr.next 
        count += 1 

    return count  

# Function to reverse the linked  
# list according to its size  
def reverseSizeBy2Util(head, k, skipMiddle):  

    if not head: 
        return None 

    count = 0 
    curr, prev, next = head, None, None 

    # Reverse current block of list.  
    while curr and count < k: 
        next = curr.next 
        curr.next = prev  
        prev = curr  
        curr = next 
        count += 1 

    # If size is even, reverse next block too.  
    if not skipMiddle:  
        head.next = reverseSizeBy2Util(next, k, False)  

    else: 

        # if size is odd, skip next element  
        # and reverse the block after that.  
        head.next = next 
        if next:  
            next.next = reverseSizeBy2Util(next.next,  
                                            k, True)  

    return prev  

def reverseBySizeBy2(head):  

    # Get the size of list.  
    n = getSize(head)  

    # If the size is even, no  
    # need to skip middle Node.  
    if n % 2 == 0:  
        return reverseSizeBy2Util(head, n//2, False)  

    # If size is odd, middle  
    # Node has to be skipped.  
    else: 
        return reverseSizeBy2Util(head, n//2, True)  

# Drivers code  
if __name__ == "__main__":  

    # Start with the empty list  
    head = None 

    # Created Linked list is 1.2.3.4.5.6.7.8.9  
    head = push(head, 9)  
    head = push(head, 8)  
    head = push(head, 7)  
    head = push(head, 6)  
    head = push(head, 5)  
    head = push(head, 4)  
    head = push(head, 3)  
    head = push(head, 2)  
    head = push(head, 1)  

    print("Original List : ", end = "")  
    printList(head)  

    print("Reversed List : ", end = "") 
    reversedHead = reverseBySizeBy2(head)  
    printList(reversedHead)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to reverse given  
// linked list according to its size  
using System; 

class GFG 
{ 

public class Node 
{  
    public int data;  
    public Node next;  
};  

// Function to create a new Node  
static Node newNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  

// Prints a list.  
static void printList(Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        Console.Write( temp.data + " ");  
        temp = temp.next;  
    } Console.WriteLine(); 
}  

// Function to push a Node  
static Node push(Node head_ref, int new_data)  
{  
    Node new_Node = new Node();  
    new_Node.data = new_data;  
    new_Node.next = (head_ref);  
    (head_ref) = new_Node;  
    return head_ref; 
}  

// Returns size of list.  
static int getSize(Node head)  
{  
    Node curr = head;  
    int count = 0;  
    while (curr != null) 
    {  
        curr = curr.next;  
        count++;  
    }  
    return count;  
}  

// Function to reverse the linked  
// list according to its size  
static Node reverseSizeBy2Util(Node head, int k,  
                            Boolean skipMiddle)  
{  
    if (head == null)  
        return null;  

    int count = 0;  
    Node curr = head;  
    Node prev = null;  
    Node next=null;  

    // Reverse current block of list.  
    while (curr!=null && count < k) 
    {  
        next = curr.next;  
        curr.next = prev;  
        prev = curr;  
        curr = next;  
        count++;  
    }  

    // If size is even, reverse next block too.  
    if (!skipMiddle)  
        head.next = reverseSizeBy2Util(next, k, false);  

    else
    {  

        // if size is odd, skip next element  
        // and reverse the block after that.  
        head.next = next;  
        if (next != null)  
            next.next = reverseSizeBy2Util(next.next,  
                                            k, true);  
    }  
    return prev;  
}  

static Node reverseBySizeBy2(Node head)  
{  
    // Get the size of list.  
    int n = getSize(head);  

    // If the size is even, no need  
    // to skip middle Node.  
    if (n % 2 == 0)  
        return reverseSizeBy2Util(head, n/2, false);  

    // If size is odd, middle Node has  
    // to be skipped.  
    else
        return reverseSizeBy2Util(head, n/2, true);  
}  

// Driver code  
public static void Main(String []args)  
{  
    // Start with the empty list / 
    Node head = null;  

    // Created Linked list is 1.2.3.4.5.6.7.8.9 / 
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    Console.Write( "Original List : ");  
    printList(head);  

    Console.Write( "Reversed List : ");  
    Node reversedHead = reverseBySizeBy2(head);  
    printList(reversedHead);  
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Original List : 1 2 3 4 5 6 7 8 9 
Reversed List : 4 3 2 1 5 9 8 7 6

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。