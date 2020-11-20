# 链表

> 原文：[https://www.geeksforgeeks.org/sum-of-factorials-of-prime-numbers-in-a-linked-list/](https://www.geeksforgeeks.org/sum-of-factorials-of-prime-numbers-in-a-linked-list/)

中素数阶乘的和

给定 **N** 个整数的[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)，任务是找到列表中每个素数元素的阶乘和。

**示例**：

> **输入**：L1 = 4-> 6-> 2-> 12-> 3
> **输出**：8
> **说明 **：
> 质数是 2 和 3，因此是 2！ + 3！ = 2 + 6 = 8。
> 
> **输入**：L1 = 7-> 4-> 5
> **输出**：5160
> **说明**：
> 质数是 7 和 5，因此是 7！ + 5！ = 5160。

**方法**：要解决上述问题，请执行以下步骤：

*   实现 [N 的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)的函数 **factorial（n）**。

*   初始化变量 **sum = 0** 。 现在，遍历给定列表，并为每个节点检查节点是否为[素数](https://www.geeksforgeeks.org/prime-numbers/)。

*   如果节点是素数，则更新 **sum = sum + sumial（node）**，否则将节点移至下一个。

*   最后打印计算出的**和**。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to fine Sum of 
// prime factorials in a Linked list 

#include <bits/stdc++.h> 
using namespace std; 

// Node of the singly linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node 
// at the beginning 
// of the singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node 
        = (Node*)malloc( 
            sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list 
    // off the new node 
    new_node->next = (*head_ref); 

    // move the head to point 
    // to the new node 
    (*head_ref) = new_node; 
} 

// Function to return the factorial of N 
int factorial(int n) 
{ 
    int f = 1; 
    for (int i = 1; i <= n; i++) { 
        f *= i; 
    } 
    return f; 
} 

// Function to check if number is prime 
bool isPrime(int n) 
{ 
    if (n <= 1) 
        return false; 
    if (n <= 3) 
        return true; 

    if (n % 2 == 0 || n % 3 == 0) 
        return false; 

    for (int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 
            || n % (i + 2) == 0) 
            return false; 

    return true; 
} 

// Function to return the sum of 
// factorials of the LL elements 
int sumFactorial(Node* head_1) 
{ 

    // To store the required sum 
    Node* ptr = head_1; 
    int s = 0; 
    while (ptr != NULL) { 

        // Add factorial of all the elements 
        if (isPrime(ptr->data)) { 
            s += factorial(ptr->data); 
            ptr = ptr->next; 
        } 
        else
            ptr = ptr->next; 
    } 
    return s; 
} 

// Driver code 
int main() 
{ 
    Node* head1 = NULL; 

    push(&head1, 4); 
    push(&head1, 6); 
    push(&head1, 2); 
    push(&head1, 12); 
    push(&head1, 3); 

    cout << sumFactorial(head1); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find Sum of 
// prime factorials in a Linked list 

import java.util.*; 

class GFG { 

    // Node of the singly linked list 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to insert a 
    // node at the beginning 
    // of the singly Linked List 
    static Node push( 
        Node head_ref, 
        int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list 
        // off the new node 
        new_node.next = (head_ref); 

        // move the head to point 
        // to the new node 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Function to return 
    // the factorial of n 
    static int factorial(int n) 
    { 
        int f = 1; 
        for (int i = 1; i <= n; i++) { 
            f *= i; 
        } 
        return f; 
    } 

    // Function to check if number is prime 
    static boolean isPrime(int n) 
    { 
        // Corner cases 
        if (n <= 1) 
            return false; 
        if (n <= 3) 
            return true; 

        if (n % 2 == 0 || n % 3 == 0) 
            return false; 

        for (int i = 5; i * i <= n; i = i + 6) 
            if (n % i == 0
                || n % (i + 2) == 0) 
                return false; 

        return true; 
    } 

    // Function to return the sum of 
    // factorials of the LL elements 
    static int sumFactorial(Node head_1) 
    { 
        Node ptr = head_1; 
        // To store the required sum 
        int s = 0; 
        while (ptr != null) { 

            // Add factorial of 
            // all the elements 
            if (isPrime(ptr.data)) { 
                s += factorial(ptr.data); 
                ptr = ptr.next; 
            } 
            else { 
                ptr = ptr.next; 
            } 
        } 
        return s; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 

        Node head1 = null; 

        head1 = push(head1, 4); 
        head1 = push(head1, 6); 
        head1 = push(head1, 2); 
        head1 = push(head1, 12); 
        head1 = push(head1, 3); 
        int ans = sumFactorial(head1); 

        System.out.println(ans); 
    } 
} 

```

## Python3

```py

# Python implementation of the approach  
class Node:   

    def __init__(self, data):   
        self.data = data   
        self.next = next

# Function to insert a 
# node at the beginning   
# of the singly Linked List   
def push( head_ref, new_data) :  

    # allocate node   
    new_node = Node(0)   

    # put in the data   
    new_node.data = new_data   

    # link the old list 
    # off the new node   
    new_node.next = (head_ref)   

    # move the head to 
    # point to the new node   
    (head_ref) = new_node  
    return head_ref 

def factorial(n):  
    f = 1;  
    for i in range(1, n + 1):  
        f *= i;  
    return f;  
  # prime for def   
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
    i = 5
    while ( i * i <= n ):  
        if (n % i == 0 
            or n % (i + 2) == 0):  
            return False
        i += 6;  

    return True

# Function to return the sum of  
# factorials of the LL elements  
def sumFactorial(head_ref1):  

    # To store the required sum  
    s = 0;  
    ptr1 = head_ref1 
    while (ptr1 != None) :  

        # Add factorial of all the elements 
        if(isPrime(ptr1.data)): 
            s += factorial(ptr1.data); 
            ptr1 = ptr1.next
        else: 
            ptr1 = ptr1.next
    return s;  
# Driver code   
# start with the empty list   
head1 = None
# create the linked list   
head1 = push(head1, 4)   
head1 = push(head1, 6)   
head1 = push(head1, 2)   
head1 = push(head1, 12)   
head1 = push(head1, 3) 
ans = sumFactorial(head1) 
print(ans) 

```

## C#

```cs

// C# implementation to find Sum of 
// prime factorials in a Linked list 
using System; 

class GFG{ 

// Node of the singly linked list 
class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert a node  
// at the beginning of the  
// singly Linked List 
static Node push(Node head_ref, 
                 int new_data) 
{ 

    // Allocate node 
    Node new_node = new Node(); 

    // Put in the data 
    new_node.data = new_data; 

    // Link the old list 
    // off the new node 
    new_node.next = (head_ref); 

    // Move the head to point 
    // to the new node 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to return 
// the factorial of n 
static int factorial(int n) 
{ 
    int f = 1; 
    for(int i = 1; i <= n; i++) 
    { 
       f *= i; 
    } 
    return f; 
} 

// Function to check if number 
// is prime 
static bool isPrime(int n) 
{ 

    // Corner cases 
    if (n <= 1) 
        return false; 
    if (n <= 3) 
        return true; 

    if (n % 2 == 0 || n % 3 == 0) 
        return false; 

    for(int i = 5; i * i <= n; 
            i = i + 6) 
       if (n % i == 0 ||  
           n % (i + 2) == 0) 
           return false; 

    return true; 
} 

// Function to return the sum of 
// factorials of the LL elements 
static int sumFactorial(Node head_1) 
{ 
    Node ptr = head_1; 

    // To store the required sum 
    int s = 0; 
    while (ptr != null)  
    { 

        // Add factorial of 
        // all the elements 
        if (isPrime(ptr.data)) 
        { 
            s += factorial(ptr.data); 
            ptr = ptr.next; 
        } 
        else
        { 
            ptr = ptr.next; 
        } 
    } 
    return s; 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    Node head1 = null; 

    head1 = push(head1, 4); 
    head1 = push(head1, 6); 
    head1 = push(head1, 2); 
    head1 = push(head1, 12); 
    head1 = push(head1, 3); 

    int ans = sumFactorial(head1); 

    Console.WriteLine(ans); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**Output:**

```
8

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。