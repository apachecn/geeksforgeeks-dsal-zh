# 单链表

> 原文：[https://www.geeksforgeeks.org/sum-and-product-of-all-prime-nodes-of-a-singly-linked-list/](https://www.geeksforgeeks.org/sum-and-product-of-all-prime-nodes-of-a-singly-linked-list/)

的所有主要节点的总和与乘积

给定一个包含 N 个节点的单链表，任务是从列表中查找素数所有节点的总和与乘积。

**示例**：

```
Input : List = 15 -> 16 -> 6 -> 7 -> 17
Output : Product = 119, Sum = 24
Prime nodes are 7, 17.

Input : List = 15 -> 3 -> 4 -> 2 -> 9
Output : Product = 6, Sum = 5

```

**方法**：的想法是逐个遍历单链表的节点，并检查当前节点是否为质数。 找到素数节点的数据之和和积。

以下是上述想法的实现：

## C++

```cpp

// C++ implementation to find sum and 
// product of all of prime nodes of 
// the singly linked list 

#include <bits/stdc++.h> 

using namespace std; 

// Node of the singly linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the beginning 
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

// Function to find sum and product of all 
// prime nodes of the singly linked list 
void sumAndProduct(Node* head_ref) 
{ 
    int prod = 1; 
    int sum = 0; 

    Node* ptr = head_ref; 

    // Traverse the linked list 
    while (ptr != NULL) { 
        // if current node is prime, 
        // Find sum and product 
        if (isPrime(ptr->data)) { 
            prod *= ptr->data; 
            sum += ptr->data; 
        } 

        ptr = ptr->next; 
    } 

    cout << "Sum = " << sum << endl; 
    cout << "Product = " << prod; 
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

    sumAndProduct(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find sum and  
// product of all of prime nodes of  
// the singly linked list  
class GFG  
{ 

// Node of the singly linked list  
static class Node 
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node =new Node();  

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

// Function to find sum and product of all  
// prime nodes of the singly linked list  
static void sumAndProduct(Node head_ref)  
{  
    int prod = 1;  
    int sum = 0;  

    Node ptr = head_ref;  

    // Traverse the linked list  
    while (ptr != null) 
    {  
        // if current node is prime,  
        // Find sum and product  
        if (isPrime(ptr.data)) 
        {  
            prod *= ptr.data;  
            sum += ptr.data;  
        }  

        ptr = ptr.next;  
    }  

    System.out.println("Sum = " + sum );  
    System.out.println( "Product = " + prod);  
}  

// Driver code  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node head = null;  

    // create the linked list  
    // 15 . 16 . 7 . 6 . 17  
    head=push(head, 17);  
    head=push(head, 7);  
    head=push(head, 6);  
    head=push(head, 16);  
    head=push(head, 15);  

    sumAndProduct(head);  

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python implementation to find sum and  
# product of all of prime nodes of  
# the singly linked list  

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# Function to insert a node at the beginning  
# of the singly Linked List  
def push( head_ref, new_data) : 

    # allocate node  
    new_node =Node(0)  

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = (head_ref)  

    # move the head to point to the new node  
    (head_ref) = new_node 
    return head_ref 

# Function to check if a number is prime  
def isPrime(n) : 

    # Corner cases  
    if (n <= 1) : 
        return False
    if (n <= 3) : 
        return True

    # This is checked so that we can skip  
    # middle five numbers in below loop  
    if (n % 2 == 0 or n % 3 == 0) : 
        return False

    i = 5
    while ( i * i <= n) : 
        if (n % i == 0 or n % (i + 2) == 0) : 
            return False
        i = i + 6
    return True

# Function to find sum and product of all  
# prime nodes of the singly linked list  
def sumAndProduct(head_ref) : 

    prod = 1
    sum = 0

    ptr = head_ref  

    # Traverse the linked list  
    while (ptr != None): 

        # if current node is prime,  
        # Find sum and product  
        if (isPrime(ptr.data)): 

            prod *= ptr.data  
            sum += ptr.data  

        ptr = ptr.next

    print("Sum = " , sum )  
    print( "Product = " , prod)  

# Driver code  

# start with the empty list  
head = None

# create the linked list  
# 15 . 16 . 7 . 6 . 17  
head = push(head, 17)  
head = push(head, 7)  
head = push(head, 6)  
head = push(head, 16)  
head = push(head, 15)  

sumAndProduct(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to find sum and  
// product of all of prime nodes of  
// the singly linked list  
using System; 

class GFG  
{  

// Node of the singly linked list  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node =new Node();  

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

// Function to find sum and product of all  
// prime nodes of the singly linked list  
static void sumAndProduct(Node head_ref)  
{  
    int prod = 1;  
    int sum = 0;  

    Node ptr = head_ref;  

    // Traverse the linked list  
    while (ptr != null)  
    {  
        // if current node is prime,  
        // Find sum and product  
        if (isPrime(ptr.data))  
        {  
            prod *= ptr.data;  
            sum += ptr.data;  
        }  

        ptr = ptr.next;  
    }  

    Console.WriteLine("Sum = " + sum);  
    Console.WriteLine( "Product = " + prod);  
}  

// Driver code  
public static void Main(String []args)  
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

    sumAndProduct(head);  
}  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Sum = 24
Product = 119

```

**时间复杂度**：`O(n)`，其中 N 是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。