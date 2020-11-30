# 链表中存在的所有完美数的总和

> 原文：[https://www.geeksforgeeks.org/sum-of-all-perfect-numbers-present-in-an-linked-list/](https://www.geeksforgeeks.org/sum-of-all-perfect-numbers-present-in-an-linked-list/)

给定[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)包含`N`个正整数，任务是从列表中查找所有[完美数](https://www.geeksforgeeks.org/perfect-number/)的和。

> 如果数字等于其适当除数的总和，即其正除数的总和（不包括数字本身），则该数字是完美的。

**示例**：，

> **输入**：`L1 = 3 -> 6 -> 9`
>
> **输出**：6
>
> 适当的除数之和为`3 = 1`
>
> 适当的除数之和为`6 = 1 + 2 + 3 = 6`
>
> 适当的除数总和为`9 = 1 + 3 = 4`
>
> `ans = 6`
>
>
> **输入**：`L1 = 17 -> 6 -> 10 -> 6 -> 4`
> **输出**：12

**方法**：初始化`sum = 0`，对于列表的每个节点，找到其适当除数的总和，即`sumFactors`。 如果`cur_node = sumFactors`，则将结果总和更新为`sum = sum + cur_node`。 最后打印`sum`。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 

#include <bits/stdc++.h> 
using namespace std; 

// Node of the singly linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node 
// at the beginning of 
// the singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node 
        = (Node*)malloc( 
            sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // move the head to point 
    // to the new node 
    (*head_ref) = new_node; 
} 
// Function to return the sum of 
// all the proper factors of n 
int sumOfFactors(int n) 
{ 
    int sum = 0; 
    for (int f = 1; f <= n / 2; f++) { 

        // f is the factor of n 
        if (n % f == 0) { 
            sum += f; 
        } 
    } 
    return sum; 
} 

// Function to return the required sum 
int getSum(Node* head_1) 
{ 

    // To store the sum 
    int sum = 0; 
    Node* ptr = head_1; 
    while (ptr != NULL) { 

        // If current element is non-zero 
        // and equal to the sum 
        // of proper factors of itself 
        if (ptr->data > 0 
            && ptr->data 
                   == sumOfFactors(ptr->data)) { 
            sum += ptr->data; 
        } 
        ptr = ptr->next; 
    } 
    return sum; 
} 

// Driver code 
int main() 
{ 
    // start with the empty list 
    Node* head1 = NULL; 

    // create the linked list 
    push(&head1, 17); 
    push(&head1, 6); 
    push(&head1, 10); 
    push(&head1, 6); 
    push(&head1, 4); 
    int k = getSum(head1); 
    cout << k; 
    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG{ 

// Node of the singly linked list 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to insert a node 
// at the beginning of 
// the singly Linked List 
static Node push(Node head_ref,  
                 int new_data) 
{ 

    // Allocate node 
    Node new_node= new Node(); 

    // Put in the data 
    new_node.data = new_data; 

    // Link the old list off the new node 
    new_node.next = head_ref; 

    // Move the head to point 
    // to the new node 
    head_ref = new_node; 

    return head_ref; 
} 

// Function to return the sum of 
// all the proper factors of n 
static int sumOfFactors(int n) 
{ 
    int sum = 0; 

    for(int f = 1; f <= n / 2; f++) 
    { 

       // f is the factor of n 
       if (n % f == 0) 
       { 
           sum += f; 
       } 
    } 
    return sum; 
} 

// Function to return the required sum 
static int getSum(Node head_1) 
{ 

    // To store the sum 
    int sum = 0; 

    Node ptr = head_1; 

    while (ptr != null)  
    { 

        // If current element is non-zero 
        // and equal to the sum of proper 
        //  factors of itself 
        if (ptr.data > 0 && ptr.data ==  
                sumOfFactors(ptr.data)) 
        { 
            sum += ptr.data; 
        } 
        ptr = ptr.next; 
    } 
    return sum; 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // Start with the empty list 
    Node head = new Node(); 

    // Create the linked list 
    head = push(head, 17); 
    head = push(head, 6); 
    head = push(head, 10); 
    head = push(head, 6); 
    head = push(head, 4); 

    int k = getSum(head); 

    System.out.print(k); 
} 
} 

// This code is contributed by amal kumar choubey 

```

## Python3

```py

# Python3 implementation of the approach 

# Node class  
class Node:  

    # Function to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None 

# Linked List Class 
class LinkedList: 

    # Function to initialize the 
    # LinkedList class. 
    def __init__(self):  

        self.head = None 

    # This function insert a new node at  
    # the beginning of the linked list  
    def push(self, new_data):  

        # Create a new Node  
        new_node = Node(new_data)  

        # Make next of new Node as head  
        new_node.next = self.head  

        # Move the head to point to new Node  
        self.head = new_node  

    # Function to return the required sum 
    def getSum(self): 

        # To store the sum 
        Sum = 0

        # Initialising the pointer 
        ptr = self.head 
        while(True): 

            # If current element is non Zero 
            # and is a perfect number then 
            # add to sum 
            if(ptr.data > 0 and ptr.data == 
                   sumOfFactors(ptr.data)): 
                Sum += ptr.data 

            # Breaking the loop if list terminates 
            if(ptr.next == None): 
                break

            # Moving to next node 
            ptr = ptr.next

        # Returning the sum 
        return Sum

# Function to return the sum of  
# all the proper factors of n  
def sumOfFactors(n): 

    Sum = 0

    # f is factor of n 
    for f in range(1, (n // 2) + 1): 
        if(n % f == 0): 
            Sum += f 

    return Sum

# Driver Code 
if __name__=='__main__': 

    # Start with empty list 
    head1 = LinkedList() 

    # Create the linked list 
    head1.push(17) 
    head1.push(6)  
    head1.push(10) 
    head1.push(6) 
    head1.push(4) 

    # Getting the required sum 
    k = head1.getSum() 
    print(k) 

# This code is contributed by Amit Mangal 

```

## C#

```cs

// C# implementation of the approach 
using System; 
class GFG{ 

// Node of the singly linked list 
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert a node 
// at the beginning of 
// the singly Linked List 
static Node push(Node head_ref,  
                 int new_data) 
{ 

    // Allocate node 
    Node new_node= new Node(); 

    // Put in the data 
    new_node.data = new_data; 

    // Link the old list off the new node 
    new_node.next = head_ref; 

    // Move the head to point 
    // to the new node 
    head_ref = new_node; 

    return head_ref; 
} 

// Function to return the sum of 
// all the proper factors of n 
static int sumOfFactors(int n) 
{ 
    int sum = 0; 

    for(int f = 1; f <= n / 2; f++) 
    { 

        // f is the factor of n 
        if (n % f == 0) 
        { 
            sum += f; 
        } 
    } 
    return sum; 
} 

// Function to return the required sum 
static int getSum(Node head_1) 
{ 

    // To store the sum 
    int sum = 0; 

    Node ptr = head_1; 

    while (ptr != null)  
    { 

        // If current element is non-zero 
        // and equal to the sum of proper 
        // factors of itself 
        if (ptr.data > 0 && ptr.data ==  
               sumOfFactors(ptr.data)) 
        { 
            sum += ptr.data; 
        } 
        ptr = ptr.next; 
    } 
    return sum; 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    // Start with the empty list 
    Node head = new Node(); 

    // Create the linked list 
    head = push(head, 17); 
    head = push(head, 6); 
    head = push(head, 10); 
    head = push(head, 6); 
    head = push(head, 4); 

    int k = getSum(head); 

    Console.Write(k); 
} 
} 

// This code is contributed by amal kumar choubey 

```

**输出**： 

```
12

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。