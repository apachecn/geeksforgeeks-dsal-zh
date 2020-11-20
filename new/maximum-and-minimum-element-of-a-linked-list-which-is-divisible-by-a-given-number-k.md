# 链表的最大和最小元素，该元素可被给定数 k 整除

> 原文：[https://www.geeksforgeeks.org/maximum-and-minimum-element-of-a-linked-list-which-is-divisible-by-a-given-number-k/](https://www.geeksforgeeks.org/maximum-and-minimum-element-of-a-linked-list-which-is-divisible-by-a-given-number-k/)

给定![N](img/19e409e13c1238e1f3ff3dbd06cdd45e.png "Rendered by QuickLaTeX.com")节点的单链表。 在链表中找到可被给定数字![K](img/36191961d5c0517749557e907a8f3817.png "Rendered by QuickLaTeX.com")整除的最小和最大元素。

**示例**：

> **输入**：列表= 15-> 14-> 13-> 22-> 50
> K = 5
> **输出**：
> 链表中可被 K 整除的最大元素：50
> 链表中可被 K 整除的最小元素：5
> 
> **输入**：列表= 10-> 14-> 13-> 22-> 100
> K = 10
> **输出**：
> 链表中可被 K 整除的最大元素：100
> 链表中可被 K 整除的最小元素：10

**方法**：

*   这个想法是将链表遍历到最后，并将 max 和 min 变量分别初始化为 INT_MIN 和 INT_MAX。

*   然后检查一下条件，如果最大值小于当前节点的值并且可以被 K 整除，那么当前节点的值将分配给 max。

*   同样，检查当前节点的值是否小于最小值，并被 k 整除，然后将当前节点的值分配给 min。 重复以上两个步骤，直到到达列表的末尾。

下面是上述方法的实现：

## C++

```cpp

// Program to find the smallest and largest 
// elements divisible by a given number k  
// in singly linked list 

#include <bits/stdc++.h> 

using namespace std; 

/* Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to print max and min elements of 
// linked list divisible by K 
void findMaxMin(struct Node* head, int k) 
{ 
    // Declare a min variable and initialize 
    // it with INT_MAX value. 
    // INT_MAX is integer type and its value 
    // is 32767 or greater. 
    int min = INT_MAX; 

    // Declare a max variable and initialize 
    // it with INT_MIN value. 
    // INT_MIN is integer type and its value 
    // is -32767 or less. 
    int max = INT_MIN; 

    // Check loop while head not equal to NULL 
    while (head != NULL) { 

        // If head->data is less than min and divisible 
        // by k then assign value of head->data to min 
        // otherwise node point to next node. 
        if ((head->data < min) && (head->data % k == 0)) 
            min = head->data; 

        // If head->data is greater than max and divisible 
        // by k then assign value of head->data to max 
        // otherwise node point to next node. 
        if ((head->data > max) && (head->data % k == 0)) 
            max = head->data; 

        head = head->next; 
    } 

    // Print max element 
    cout << "Max Element : " << max << endl; 

    // print min element 
    cout << "Min Element : " << min; 
} 

// Function that pushes the element in the linked list. 
void push(struct Node** head, int data) 
{ 
    // Allocate dynamic memory for newNode. 
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node)); 

    // Assign the data into newNode. 
    newNode->data = data; 

    // newNode->next assign the address of 
    // head node. 
    newNode->next = (*head); 

    // newNode become the headNode. 
    (*head) = newNode; 
} 

// Driver Code 
int main() 
{ 
    // Start with empty list 
    struct Node* head = NULL; 

    // Using push() function to construct 
    // singly linked list 
    // 50->5->13->14->15 
    push(&head, 15); 
    push(&head, 14); 
    push(&head, 13); 
    push(&head, 5); 
    push(&head, 50); 

    int k = 5; 

    findMaxMin(head, k); 

    return 0; 
} 

```

## Java

```java

// Java program to find the smallest and largest  
// elements divisible by a given number k  
// in singly linked list  
class GFG 
{ 

// Linked list node / 
static class Node 
{  
    int data;  
    Node next;  
};  

// Function to print max and min elements of  
// linked list divisible by K  
static void findMaxMin( Node head, int k)  
{  
    // Declare a min variable and initialize  
    // it with INT_MAX value.  
    // INT_MAX is integer type and its value  
    // is 32767 or greater.  
    int min = Integer.MAX_VALUE;  

    // Declare a max variable and initialize  
    // it with INT_MIN value.  
    // INT_MIN is integer type and its value  
    // is -32767 or less.  
    int max = Integer.MIN_VALUE;  

    // Check loop while head not equal to null  
    while (head != null)  
    {  

        // If head.data is less than min and divisible  
        // by k then assign value of head.data to min  
        // otherwise node point to next node.  
        if ((head.data < min) && (head.data % k == 0))  
            min = head.data;  

        // If head.data is greater than max and divisible  
        // by k then assign value of head.data to max  
        // otherwise node point to next node.  
        if ((head.data > max) && (head.data % k == 0))  
            max = head.data;  

        head = head.next;  
    }  

    // Print max element  
    System.out.println( "Max Element : " + max);  

    // print min element  
    System.out.println( "Min Element : " + min);  
}  

// Function that push the element in linked list.  
static Node push( Node head, int data)  
{  
    // Allocate dynamic memory for newNode.  
    Node newNode = new Node();  

    // Assign the data into newNode.  
    newNode.data = data;  

    // newNode.next assign the address of  
    // head node.  
    newNode.next = (head);  

    // newNode become the headNode.  
    (head) = newNode;  
    return head; 
}  

// Driver Code  
public static void main(String args[])  
{  
    // Start with empty list  
    Node head = null;  

    // Using push() function to con  
    // singly linked list  
    // 50.5.13.14.15  
    head = push(head, 15);  
    head = push(head, 14);  
    head = push(head, 13);  
    head = push(head, 5);  
    head = push(head, 50);  

    int k = 5;  

    findMaxMin(head, k);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find the smallest and largest  
# elements divisible by a given number k  
# in singly linked list  

# Linked list node / 
class Node: 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to print max and min elements of  
# linked list divisible by K  
def findMaxMin(head, k):  

    # Declare a min variable and initialize  
    # it with INT_MAX value.  
    # INT_MAX is integer type and its value  
    # is 32767 or greater.  
    min = 32767

    # Declare a max variable and initialize  
    # it with INT_MIN value.  
    # INT_MIN is integer type and its value  
    # is -32767 or less.  
    max = -32767

    # Check loop while head not equal to None  
    while (head != None) : 

        # If head.data is less than min and divisible  
        # by k then assign value of head.data to min  
        # otherwise node point to next node.  
        if ((head.data < min) and (head.data % k == 0)) : 
            min = head.data  

        # If head.data is greater than max and divisible  
        # by k then assign value of head.data to max  
        # otherwise node point to next node.  
        if ((head.data > max) and (head.data % k == 0)) : 
            max = head.data  

        head = head.next

    # Print max element  
    print( "Max Element : " , max)  

    # print min element  
    print( "Min Element : " , min)  

# Function that push the element in linked list.  
def push( head, data):  

    # Allocate dynamic memory for newNode.  
    newNode = Node()  

    # Assign the data into newNode.  
    newNode.data = data  

    # newNode.next assign the address of  
    # head node.  
    newNode.next = (head)  

    # newNode become the headNode.  
    (head) = newNode  
    return head 

# Driver Code  

# Start with empty list  
head = None

# Using push() function to con  
# singly linked list  
# 50.5.13.14.15  
head = push(head, 15)  
head = push(head, 14)  
head = push(head, 13)  
head = push(head, 5)  
head = push(head, 50)  

k = 5

findMaxMin(head, k)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find the smallest and largest  
// elements divisible by a given number k  
// in singly linked list  
using System; 

class GFG  
{  

// Linked list node /  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to print max and min elements of  
// linked list divisible by K  
static void findMaxMin( Node head, int k)  
{  
    // Declare a min variable and initialize  
    // it with INT_MAX value.  
    // INT_MAX is integer type and its value  
    // is 32767 or greater.  
    int min = int.MaxValue;  

    // Declare a max variable and initialize  
    // it with INT_MIN value.  
    // INT_MIN is integer type and its value  
    // is -32767 or less.  
    int max = int.MinValue;  

    // Check loop while head not equal to null  
    while (head != null)  
    {  

        // If head.data is less than min and divisible  
        // by k then assign value of head.data to min  
        // otherwise node point to next node.  
        if ((head.data < min) && (head.data % k == 0))  
            min = head.data;  

        // If head.data is greater than max and divisible  
        // by k then assign value of head.data to max  
        // otherwise node point to next node.  
        if ((head.data > max) && (head.data % k == 0))  
            max = head.data;  

        head = head.next;  
    }  

    // Print max element  
    Console.WriteLine( "Max Element : " + max);  

    // print min element  
    Console.WriteLine( "Min Element : " + min);  
}  

// Function that push the element in linked list.  
static Node push( Node head, int data)  
{  
    // Allocate dynamic memory for newNode.  
    Node newNode = new Node();  

    // Assign the data into newNode.  
    newNode.data = data;  

    // newNode.next assign the address of  
    // head node.  
    newNode.next = (head);  

    // newNode become the headNode.  
    (head) = newNode;  
    return head;  
}  

// Driver Code  
public static void Main(String []args)  
{  
    // Start with empty list  
    Node head = null;  

    // Using push() function to con  
    // singly linked list  
    // 50.5.13.14.15  
    head = push(head, 15);  
    head = push(head, 14);  
    head = push(head, 13);  
    head = push(head, 5);  
    head = push(head, 50);  

    int k = 5;  

    findMaxMin(head, k);  
}  
}  

// This code contributed by Rajput-Ji 

```

**Output:**

```
Max Element : 50
Min Element : 5

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。