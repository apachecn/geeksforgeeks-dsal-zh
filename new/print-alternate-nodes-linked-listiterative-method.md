# 打印链表的备用节点（迭代方法）

> 原文：[https://www.geeksforgeeks.org/print-alternate-nodes-linked-listiterative-method/](https://www.geeksforgeeks.org/print-alternate-nodes-linked-listiterative-method/)

给定一个链表，打印链表的备用节点。

例子：

```
Input : 1 -> 8 -> 3 -> 10 -> 17 -> 22 -> 29 -> 42
Output : 1 -> 3 -> 17 -> 29
Alternate nodes : 1 -> 3 -> 17 -> 29

Input : 10 -> 17 -> 33 -> 38 -> 73
Output : 10 -> 33 -> 73
Alternate nodes : 10 -> 33 -> 73

```

**方法**：

1.遍历整个链表。

2.设置计数为 0。

3.当计数为偶数时打印节点。

4.访问下一个节点。

## C++

```cpp

// CPP code to print Alternate Nodes  
#include <iostream> 
using namespace std; 

/* Link list node */
struct Node 
{  
    int data;  
    struct Node* next;  
};  

/* Function to get the alternate  
nodes of the linked list */
void printAlternateNode(struct Node* head)  
{  
    int count = 0;  

    while (head != NULL) 
    {  

        // when count is even print the nodes  
        if (count % 2 == 0)  
            cout  << head->data << " ";  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head->next;  
    }  
}  

// Function to push node at head  
void push(struct Node** head_ref, int new_data)  
{  
    struct Node* new_node =  
        (struct Node*)malloc(sizeof(struct Node));  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

// Driver code  
int main()  
{  
    /* Start with the empty list */
    struct Node* head = NULL;  

    /* Use push() function to construct  
    the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12);  
    push(&head, 29);  
    push(&head, 11);  
    push(&head, 23);  
    push(&head, 8);  

    printAlternateNode(head);  

    return 0;  
}  

// This code is contributed by shubhamsingh10 

```

## C

```c

// C code to print Alternate Nodes 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the alternate 
   nodes of the linked list */
void printAlternateNode(struct Node* head) 
{ 
    int count = 0; 

    while (head != NULL) { 

        // when count is even print the nodes 
        if (count % 2 == 0)  
            printf(" %d ", head->data); 

        // count the nodes 
        count++; 

        // move on the next node. 
        head = head->next; 
    } 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node =  
          (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() function to construct 
       the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    printAlternateNode(head); 

    return 0; 
} 

```

## Java

```java

// Java code to print Alternate Nodes  
class GFG 
{ 

/* Link list node */
static class Node 
{  
    int data;  
    Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static void printAlternateNode( Node head)  
{  
    int count = 0;  

    while (head != null) 
    {  

        // when count is even print the nodes  
        if (count % 2 == 0)  
            System.out.printf(" %d ", head.data);  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

// Driver code  
public static void main(String args[])  
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    printAlternateNode(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 code to print Alternate Nodes 

# Link list node 
class Node :  

    def __init__(self, data = None) : 
        self.data = data 
        self.next = None

    # Function to push node at head 
    def push(self, data) : 

        new = Node(data) 
        new.next = self
        return new 

    # Function to get the alternate 
    # nodes of the linked list      
    def printAlternateNode(self) : 
        head = self

        while head and head.next != None : 

            print(head.data, end = " ") 
            head = head.next.next

# Driver Code         
node = Node() 

# Use push() function to construct 
# the below list 8 -> 23 -> 11 -> 29 -> 12 
node = node.push(12) 
node = node.push(29) 
node = node.push(11) 
node = node.push(23) 
node = node.push(8) 

node.printAlternateNode() 

```

## C#

```cs

// C# code to print Alternate Nodes 
using System; 

class GFG  
{  

/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static void printAlternateNode( Node head)  
{  
    int count = 0;  

    while (head != null)  
    {  

        // when count is even print the nodes  
        if (count % 2 == 0)  
            Console.Write(" {0} ", head.data);  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Driver code  
public static void Main(String []args)  
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    printAlternateNode(head);  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
8  11  12

```

**时间复杂度：`O(n)`

辅助空间：`O(1)`**

**提问者：Govivace**



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。