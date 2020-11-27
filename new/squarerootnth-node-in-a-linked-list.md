# 链表中的第`sqrt(n)`个节点

> 原文：[https://www.geeksforgeeks.org/squarerootnth-node-in-a-linked-list/](https://www.geeksforgeeks.org/squarerootnth-node-in-a-linked-list/)

给定一个链表，编写一个函数，该函数接受链表的头节点作为参数，并返回链表中第`floor(sqrt(n))`个位置上存在的节点的值，其中`n`是长度。 链表或列表中的节点总数。

**示例**：

```
Input: 1->2->3->4->5->NULL
Output: 2

Input : 10->20->30->40->NULL
Output : 20

Input : 10->20->30->40->50->60->70->80->90->NULL
Output : 30

```

**简单方法**：简单方法是首先找到链表中存在的节点总数，然后找到`floor(squareroot(n))`的值，其中`n`是节点总数。 然后从列表中的第一个节点遍历到该位置，并返回此位置的节点。

此方法遍历链表 2 次。

**优化方法**：在这种方法中，我们只需遍历链表一次即可获得所需的节点。 以下是此方法的分步算法。

1.  将两个计数器`i`和`j`都初始化为 1，并将指针`sqrtn`初始化为`NULL`，以遍历直到所需的位置。

2.  使用头节点开始遍历列表，直到到达最后一个节点。

3.  遍历时检查`j`的值是否等于`sqrt(i)`。 如果值相等，则将`i`和`j`和`sqrtn`都增加到指向`sqrtn->next`，否则仅增加`i`。

4.  现在，当我们到达列表的最后一个节点时，`i`将包含`n`值，`j`将包含`sqrt(i)`值，而`sqrtn`将指向第`j`个位置的节点。

## C++

```cpp

// C++ program to find sqrt(n)'th node  
// of a linked list  

#include <bits/stdc++.h> 
using namespace std; 

// Linked list node  
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

// Function to get the sqrt(n)th  
// node of a linked list  
int printsqrtn(Node* head)  
{  
    Node* sqrtn = NULL;  
    int i = 1, j = 1;  

    // Traverse the list  
    while (head!=NULL)  
    {  
        // check if j = sqrt(i)  
        if (i == j*j)  
        {  
            // for first node  
            if (sqrtn == NULL)  
                sqrtn = head;  
            else
                sqrtn = sqrtn->next;  

            // increment j if j = sqrt(i)  
            j++;  
        }  
        i++;  

        head=head->next;  
    }  

    // return node's data  
    return sqrtn->data;  
}  

void print(Node* head)  
{  
    while (head != NULL)  
    {  
        cout << head->data << " ";  
        head = head->next;  
    }  
    cout<<endl;  
}  

// function to add a new node at the  
// beginning of the list  
void push(Node** head_ref, int new_data)  
{  
    // allocate node  
    Node* new_node = new Node(); 

    // put in the data  
    new_node->data = new_data;  

    // link the old list off the new node  
    new_node->next = (*head_ref);  

    // move the head to point to the new node  
    (*head_ref) = new_node;  
}  

/* Driver program to test above function*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  
    push(&head, 40);  
    push(&head, 30);  
    push(&head, 20);  
    push(&head, 10);  
    cout << "Given linked list is:";  
    print(head);  
    cout << "sqrt(n)th node is " << printsqrtn(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to find sqrt(n)'th node  
// of a linked list 

#include<stdio.h> 
#include<stdlib.h> 

// Linked list node  
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// Function to get the sqrt(n)th  
// node of a linked list 
int printsqrtn(struct Node* head) 
{ 
    struct Node* sqrtn = NULL; 
    int i = 1, j = 1; 

    // Traverse the list 
    while (head!=NULL) 
    {    
        // check if j = sqrt(i) 
        if (i == j*j) 
        {    
            // for first node 
            if (sqrtn == NULL) 
                sqrtn = head; 
            else
                sqrtn = sqrtn->next;  

            // increment j if j = sqrt(i)     
            j++; 
        } 
        i++; 

        head=head->next; 
    } 

    // return node's data 
    return sqrtn->data; 
} 

void print(struct Node* head) 
{ 
    while (head != NULL) 
    { 
        printf("%d ", head->data); 
        head = head->next; 
    } 
    printf("\n"); 
} 

// function to add a new node at the  
// beginning of the list 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node  
    struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 

    // put in the data  
    new_node->data = new_data; 

    // link the old list off the new node  
    new_node->next = (*head_ref);  

    // move the head to point to the new node  
    (*head_ref) = new_node; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 
    push(&head, 40); 
    push(&head, 30); 
    push(&head, 20); 
    push(&head, 10); 
    printf("Given linked list is:"); 
    print(head); 
    printf("sqrt(n)th node is %d ",printsqrtn(head)); 

    return 0; 
} 

```

## Java

```java

// Java program to find sqrt(n)'th node  
// of a linked list  

class GfG  
{ 

// Linked list node  
static class Node  
{  
    int data;  
    Node next;  
} 
static Node head = null; 

// Function to get the sqrt(n)th  
// node of a linked list  
static int printsqrtn(Node head)  
{  
    Node sqrtn = null;  
    int i = 1, j = 1;  

    // Traverse the list  
    while (head != null)  
    {  
        // check if j = sqrt(i)  
        if (i == j * j)  
        {  
            // for first node  
            if (sqrtn == null)  
                sqrtn = head;  
            else
                sqrtn = sqrtn.next;  

            // increment j if j = sqrt(i)  
            j++;  
        }  
        i++;  

        head=head.next;  
    }  

    // return node's data  
    return sqrtn.data;  
}  

static void print(Node head)  
{  
    while (head != null)  
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
    System.out.println();  
}  

// function to add a new node at the  
// beginning of the list  
static void push( int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list off the new node  
    new_node.next = head;  

    // move the head to point to the new node  
    head = new_node;  
}  

/* Driver code*/
public static void main(String[] args)  
{  
    /* Start with the empty list */
    push( 40);  
    push( 30);  
    push( 20);  
    push( 10);  
    System.out.print("Given linked list is:");  
    print(head);  
    System.out.print("sqrt(n)th node is " + 
                        printsqrtn(head));  
}  
}  

// This code is contributed by prerna saini 

```

## Python3

```py

# Python3 program to find sqrt(n)'th node  
# of a linked list  

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to get the sqrt(n)th  
# node of a linked list  
def printsqrtn(head) : 

    sqrtn = None
    i = 1
    j = 1

    # Traverse the list  
    while (head != None) : 

        # check if j = sqrt(i)  
        if (i == j * j) : 

            # for first node  
            if (sqrtn == None) : 
                sqrtn = head  
            else: 
                sqrtn = sqrtn.next

            # increment j if j = sqrt(i)  
            j = j + 1

        i = i + 1

        head = head.next

    # return node's data  
    return sqrtn.data  

def print_1(head) : 

    while (head != None) : 
        print( head.data, end = " ")  
        head = head.next
    print(" ") 

# function to add a new node at the  
# beginning of the list  
def push(head_ref, new_data) : 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = (head_ref)  

    # move the head to point to the new node  
    (head_ref) = new_node  
    return head_ref 

# Driver Code  
if __name__=='__main__':  

    # Start with the empty list  
    head = None
    head = push(head, 40)  
    head = push(head, 30)  
    head = push(head, 20)  
    head = push(head, 10)  
    print("Given linked list is:")  
    print_1(head)  
    print("sqrt(n)th node is ",  
              printsqrtn(head)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find sqrt(n)'th node  
// of a linked list  
using System; 
public class GfG  
{  

// Linked list node  
class Node  
{  
    public int data;  
    public Node next;  
}  
static Node head = null;  

// Function to get the sqrt(n)th  
// node of a linked list  
static int printsqrtn(Node head)  
{  
    Node sqrtn = null;  
    int i = 1, j = 1;  

    // Traverse the list  
    while (head != null)  
    {  
        // check if j = sqrt(i)  
        if (i == j * j)  
        {  
            // for first node  
            if (sqrtn == null)  
                sqrtn = head;  
            else
                sqrtn = sqrtn.next;  

            // increment j if j = sqrt(i)  
            j++;  
        }  
        i++;  

        head=head.next;  
    }  

    // return node's data  
    return sqrtn.data;  
}  

static void print(Node head)  
{  
    while (head != null)  
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
    Console.WriteLine();  
}  

// function to add a new node at the  
// beginning of the list  
static void push( int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list off the new node  
    new_node.next = head;  

    // move the head to point to the new node  
    head = new_node;  
}  

/* Driver code*/
public static void Main(String[] args)  
{  
    /* Start with the empty list */
    push( 40);  
    push( 30);  
    push( 20);  
    push( 10);  
    Console.Write("Given linked list is:");  
    print(head);  
    Console.Write("sqrt(n)th node is " +  
                        printsqrtn(head));  
}  
}  

/* This code is contributed by 29AjayKumar */

```

**输出**：

```
Given linked list is:10 20 30 40
sqrt(n)th node is 20

```

本文由 **Akshit Agarwal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

