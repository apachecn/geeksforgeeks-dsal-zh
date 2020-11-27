# 反向链表中的偶数元素

> 原文：[https://www.geeksforgeeks.org/reverse-even-elements-in-a-linked-list/](https://www.geeksforgeeks.org/reverse-even-elements-in-a-linked-list/)

给定一个链表，任务是反转连续的偶数元素并打印更新的链表。

> **输入**：`1 -> 2 -> 3 -> 3 -> 4 -> 6 -> 8 -> 5 -> NULL`
>
> **输出**：`1 2 3 3 8 6 4 5`
>
> 初始列表：`1 -> 2 -> 3 -> 3 -> 4 -> 6 -> 8 -> 5 -> NULL`
>
> 反转列表：`1 -> 2 -> 3  -> 3 -> 8 -> 6 -> 4 -> 5 -> NULL`
> 
> **输入**：`11 -> 32 -> 7 -> NULL`
>
> **输出**：`11 32 7`

**方法**：在以下情况下，反转偶数元素将不会发生：

1.  节点的值是奇数。

2.  节点的值为偶数，但相邻的值为奇数。

在其余情况下，偶数节点的连续块可以反转。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Structure of a node of the linked list 
struct node { 
    int data; 
    struct node* next; 
}; 

// Function to create a new node 
struct node* newNode(int d) 
{ 
    struct node* newnode = new node(); 
    newnode->data = d; 
    newnode->next = NULL; 
    return newnode; 
} 

// Recursive function to reverse the consecutive 
// even nodes of the linked list 
struct node* reverse(struct node* head, struct node* prev) 
{ 

    // Base case 
    if (head == NULL) 
        return NULL; 

    struct node* temp; 
    struct node* curr; 
    curr = head; 

    // Reversing nodes until curr node's value 
    // turn odd or Linked list is fully traversed 
    while (curr != NULL && curr->data % 2 == 0) { 
        temp = curr->next; 
        curr->next = prev; 
        prev = curr; 
        curr = temp; 
    } 

    // If elements were reversed then head 
    // pointer needs to be changed 
    if (curr != head) { 

        head->next = curr; 

        // Recur for the remaining linked list 
        curr = reverse(curr, NULL); 
        return prev; 
    } 

    // Simply iterate over the odd value nodes 
    else { 
        head->next = reverse(head->next, head); 
        return head; 
    } 
} 

// Utility function to print the 
// contents of the linked list 
void printLinkedList(struct node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 3, 3, 4, 6, 8, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    struct node* head = NULL; 
    struct node* p; 

    // Constructing linked list 
    for (int i = 0; i < n; i++) { 

        if (head == NULL) { 
            p = newNode(arr[i]); 
            head = p; 
            continue; 
        } 
        p->next = newNode(arr[i]); 
        p = p->next; 
    } 

    // Head of the updated linked list 
    head = reverse(head, NULL); 

    // Printing the reversed linked list 
    printLinkedList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.*; 

class GFG 
{ 

// Structure of a node of the linked list 
static class node 
{ 
    int data; 
    node next; 
}; 

// Function to create a new node 
static node newNode(int d) 
{ 
    node newnode = new node(); 
    newnode.data = d; 
    newnode.next = null; 
    return newnode; 
} 

// Recursive function to reverse the consecutive 
// even nodes of the linked list 
static node reverse(node head, node prev) 
{ 

    // Base case 
    if (head == null) 
        return null; 

    node temp; 
    node curr; 
    curr = head; 

    // Reversing nodes until curr node's value 
    // turn odd or Linked list is fully traversed 
    while (curr != null && curr.data % 2 == 0)  
    { 
        temp = curr.next; 
        curr.next = prev; 
        prev = curr; 
        curr = temp; 
    } 

    // If elements were reversed then head 
    // pointer needs to be changed 
    if (curr != head)  
    { 
        head.next = curr; 

        // Recur for the remaining linked list 
        curr = reverse(curr, null); 
        return prev; 
    } 

    // Simply iterate over the odd value nodes 
    else
    { 
        head.next = reverse(head.next, head); 
        return head; 
    } 
} 

// Utility function to print the 
// contents of the linked list 
static void printLinkedList(node head) 
{ 
    while (head != null) 
    { 
        System.out.print(head.data + " "); 
        head = head.next; 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 1, 2, 3, 3, 4, 6, 8, 5 }; 
    int n = arr.length; 

    node head = null; 
    node p = new node(); 

    // Constructing linked list 
    for (int i = 0; i < n; i++) 
    { 
        if (head == null)  
        { 
            p = newNode(arr[i]); 
            head = p; 
            continue; 
        } 
        p.next = newNode(arr[i]); 
        p = p.next; 
    } 

    // Head of the updated linked list 
    head = reverse(head, null); 

    // Printing the reversed linked list 
    printLinkedList(head); 
} 
}  

// This code is contributed by PrinciRaj1992 

```

## Python

```py

# Python implementation of the approach  

# Node of a linked list  
class Node:  
    def __init__(self, next = None, data = None):  
        self.next = next
        self.data = data  

# Function to create a new node 
def newNode( d): 

    newnode = Node() 
    newnode.data = d 
    newnode.next = None
    return newnode 

# Recursive function to reverse the consecutive 
# even nodes of the linked list 
def reverse(head, prev): 

    # Base case 
    if (head == None): 
        return None

    temp = None
    curr = None
    curr = head 

    # Reversing nodes until curr node's value 
    # turn odd or Linked list is fully traversed 
    while (curr != None and curr.data % 2 == 0) : 
        temp = curr.next
        curr.next = prev 
        prev = curr 
        curr = temp 

    # If elements were reversed then head 
    # pointer needs to be changed 
    if (curr != head) : 

        head.next = curr 

        # Recur for the remaining linked list 
        curr = reverse(curr, None) 
        return prev 

    # Simply iterate over the odd value nodes 
    else: 

        head.next = reverse(head.next, head) 
        return head 

# Utility function to print the 
# contents of the linked list 
def printLinkedList(head): 

    while (head != None): 

        print(head.data ,end= " ") 
        head = head.next

# Driver code 
arr = [ 1, 2, 3, 3, 4, 6, 8, 5 ] 
n = len(arr) 

head = None
p = Node() 

i = 0

# Constructing linked list 
while ( i < n ): 

    if (head == None): 

        p = newNode(arr[i]) 
        head = p 
    else: 
        p.next = newNode(arr[i]) 
        p = p.next
    i = i + 1; 

# Head of the updated linked list 
head = reverse(head, None) 

# Printing the reversed linked list 
printLinkedList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the above approach 
using System; 

class GFG 
{ 

// Structure of a node of the linked list 
public class node 
{ 
    public int data; 
    public node next; 
}; 

// Function to create a new node 
static node newNode(int d) 
{ 
    node newnode = new node(); 
    newnode.data = d; 
    newnode.next = null; 
    return newnode; 
} 

// Recursive function to reverse the consecutive 
// even nodes of the linked list 
static node reverse(node head, node prev) 
{ 

    // Base case 
    if (head == null) 
        return null; 

    node temp; 
    node curr; 
    curr = head; 

    // Reversing nodes until curr node's value 
    // turn odd or Linked list is fully traversed 
    while (curr != null && curr.data % 2 == 0)  
    { 
        temp = curr.next; 
        curr.next = prev; 
        prev = curr; 
        curr = temp; 
    } 

    // If elements were reversed then head 
    // pointer needs to be changed 
    if (curr != head)  
    { 
        head.next = curr; 

        // Recur for the remaining linked list 
        curr = reverse(curr, null); 
        return prev; 
    } 

    // Simply iterate over the odd value nodes 
    else
    { 
        head.next = reverse(head.next, head); 
        return head; 
    } 
} 

// Utility function to print the 
// contents of the linked list 
static void printLinkedList(node head) 
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
    int []arr = { 1, 2, 3, 3, 4, 6, 8, 5 }; 
    int n = arr.Length; 

    node head = null; 
    node p = new node(); 

    // Constructing linked list 
    for (int i = 0; i < n; i++) 
    { 
        if (head == null)  
        { 
            p = newNode(arr[i]); 
            head = p; 
            continue; 
        } 
        p.next = newNode(arr[i]); 
        p = p.next; 
    } 

    // Head of the updated linked list 
    head = reverse(head, null); 

    // Printing the reversed linked list 
    printLinkedList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
1 2 3 3 8 6 4 5

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。