# 检查给定链表的长度是偶数还是奇数

给定一个链表，任务是创建一个函数来检查链表的长度是偶数还是奇数。

示例：

```
Input : 1->2->3->4->NULL
Output : Even

Input : 1->2->3->4->5->NULL
Output : Odd

```

**方法 1：线性计算代码**

遍历整个链表，并继续计算节点数。 循环结束后，我们可以检查计数是偶数还是奇数。 您可以自己尝试。

**方法 2：一次步进 2 个节点**

**方法：**

```
1\. Take a pointer and move that pointer two nodes at a time
2\. At the end, if the pointer is NULL then length is Even, else Odd.

```

## C++

```cpp

// C++ program to check length  
// of a given linklist  
#include <bits/stdc++.h> 
using namespace std;  

// Defining structure  
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

// Function to check the length of linklist  
int LinkedListLength(Node* head)  
{  
    while (head && head->next)  
    {  
        head = head->next->next;  
    }  
    if (!head)  
        return 0;  
    return 1;  
}  

// Push function  
void push(Node** head, int info)  
{  
    // Allocating node  
    Node* node = new Node(); 

    // Info into node  
    node->data = info;  

    // Next of new node to head  
    node->next = (*head);  

    // head points to new node  
    (*head) = node;  
}  

// Driver code  
int main(void)  
{  
    Node* head = NULL;  

    // Adding elements to Linked List  
    push(&head, 4);  
    push(&head, 5);  
    push(&head, 7);  
    push(&head, 2);  
    push(&head, 9);  
    push(&head, 6);  
    push(&head, 1);  
    push(&head, 2);  
    push(&head, 0);  
    push(&head, 5);  
    push(&head, 5);  
    int check = LinkedListLength(head);  

    // Checking for length of  
    // linklist  
    if(check == 0)  
    {  
        cout << "Even\n";  
    }  
    else
    {  
        cout << "Odd\n";  
    }  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to check length  
// of a given linklist 
#include<stdio.h> 
#include<stdlib.h> 

// Defining structure 
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// Function to check the length of linklist 
int LinkedListLength(struct Node* head) 
{ 
    while (head && head->next) 
    { 
        head = head->next->next; 
    } 
    if (!head) 
        return 0; 
    return 1; 
} 

// Push function 
void push(struct Node** head, int info) 
{ 
    // Allocating node 
    struct Node* node = (struct Node*) malloc(sizeof(struct Node)); 

    // Info into node 
    node->data = info; 

    // Next of new node to head 
    node->next = (*head); 

    // head points to new node 
    (*head) = node; 
} 

// Driver function 
int main(void) 
{ 
    struct Node* head = NULL; 

    // Adding elements to Linked List 
    push(&head, 4); 
    push(&head, 5); 
    push(&head, 7); 
    push(&head, 2); 
    push(&head, 9); 
    push(&head, 6); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 0); 
    push(&head, 5); 
    push(&head, 5); 
    int check = LinkedListLength(head); 

    // Checking for length of 
    // linklist 
    if(check == 0) 
    { 
        printf("Even\n"); 
    } 
    else
    { 
        printf("Odd\n"); 
    } 
    return 0; 
} 

```

## Java

```java

/*package whatever //do not write package name here */

import java.io.*; 

// Java program to check length  
// of a given linklist  
class GfG  
{  

// Defining structure  
static class Node  
{  
    int data;  
    Node next;  
} 

// Function to check the length of linklist  
static int LinkedListLength(Node head)  
{  
    while (head != null && head.next != null)  
    {  
        head = head.next.next;  
    }  
    if (head == null)  
        return 0;  
    return 1;  
}  

// Push function  
static void push(Node head, int info)  
{  
    // Allocating node  
    Node node = new Node();  

    // Info into node  
    node.data = info;  

    // Next of new node to head  
    node.next = (head);  

    // head points to new node  
    (head) = node;  
}  

// Driver code  
public static void main(String[] args)  
{  
    Node head = null;  

    // Adding elements to Linked List  
    push(head, 4);  
    push(head, 5);  
    push(head, 7);  
    push(head, 2);  
    push(head, 9);  
    push(head, 6);  
    push(head, 1);  
    push(head, 2);  
    push(head, 0);  
    push(head, 5);  
    push(head, 5);  
    int check = LinkedListLength(head);  

    // Checking for length of  
    // linklist  
    if(check == 0)  
    {  
        System.out.println("Odd");  
    }  
    else
    {  
        System.out.println("Even");  
    }  
} 
}  

// This code is contributed by Prerna saini 

```

## Python3

```py

# Python program to check length  
# of a given linklist  

# Defining structure  
class Node:  
    def __init__(self, d): 
        self.data = d 
        self.next = None
        self.head = None

    # Function to check the length of linklist  
    def LinkedListLength(self): 
        while (self.head != None and self.head.next != None):  
            self.head = self.head.next.next

        if(self.head == None): 
            return 0
        return 1

    # Push function  
    def push(self, info): 

    # Allocating node  
        node = Node(info)  

    # Next of new node to head  
        node.next = (self.head)  

    # head points to new node  
        (self.head) = node  

# Driver code  

head = Node(0)  

# Adding elements to Linked List  
head.push( 4)  
head.push( 5)  
head.push( 7)  
head.push( 2)  
head.push( 9)  
head.push( 6)  
head.push( 1)  
head.push( 2)  
head.push( 0)  
head.push( 5)  
head.push( 5)  
check = head.LinkedListLength() 

# Checking for length of  
# linklist  
if(check == 0) : 
    print("Even") 
else: 
    print("Odd") 

# This code is contributed by Prerna saini 

```

## C#

```cs

// C# program to check length  
// of a given linklist  
using System; 

class GfG  
{  

// Defining structure  
class Node  
{  
    public int data;  
    public Node next;  
}  

// Function to check the length of linklist  
static int LinkedListLength(Node head)  
{  
    while (head != null && head.next != null)  
    {  
        head = head.next.next;  
    }  
    if (head == null)  
        return 0;  
    return 1;  
}  

// Push function  
static void push(Node head, int info)  
{  
    // Allocating node  
    Node node = new Node();  

    // Info into node  
    node.data = info;  

    // Next of new node to head  
    node.next = (head);  

    // head points to new node  
    (head) = node;  
}  

// Driver code  
public static void Main()  
{  
    Node head = null;  

    // Adding elements to Linked List  
    push(head, 4);  
    push(head, 5);  
    push(head, 7);  
    push(head, 2);  
    push(head, 9);  
    push(head, 6);  
    push(head, 1);  
    push(head, 2);  
    push(head, 0);  
    push(head, 5);  
    push(head, 5);  
    int check = LinkedListLength(head);  

    // Checking for length of  
    // linklist  
    if(check == 0)  
    {  
        Console.WriteLine("Odd");  
    }  
    else
    {  
        Console.WriteLine("Even");  
    }  
}  
}  

// This code has been contributed  
// by PrinciRaj1992  

```

**输出：**

```
Odd

```

**时间复杂度：** O（n）

**空间复杂度：** O（1）

本文由 **[Sahil Rajput](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

