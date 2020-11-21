# 程序，用于查找双链表

> 原文：[https://www.geeksforgeeks.org/program-find-size-doubly-linked-list/](https://www.geeksforgeeks.org/program-find-size-doubly-linked-list/)

的大小

给定[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，任务是找到该双链表的大小。 例如，下面的链表的大小为 4。

![dll](img/1fac4717827a04f080fae80f8fd57fe7.png)

双链表是一种由一组顺序链接的记录（称为节点）组成的链接数据结构。 每个节点包含两个称为链接的字段，这些字段引用节点序列中的上一个节点和下一个节点。

双向链表的遍历可以是任一方向。 实际上，如果需要，遍历的方向可以更改很多次。

例如对于上面的双向链表函数应该返回 3。

## 算法：

1.  初始化大小为 0。

2.  初始化节点指针，temp = head。

3.  在 temp 不为 NULL 时执行以下操作

……a）temp = temp->接下来的

……b）size ++;

4.  返回大小。

## C++

```cpp

// A complete working C++ program to 
// find size of doubly linked list. 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
    struct Node *prev; 
}; 

/* Function to add a node to front of doubly 
   linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data  = new_data; 
    new_node->next = (*head_ref); 
    new_node->prev = NULL; 
    if ((*head_ref) !=  NULL) 
      (*head_ref)->prev = new_node ; 
    (*head_ref)    = new_node; 
} 

// This function returns size of linked list 
int findSize(struct Node *node) 
{ 
   int res = 0; 
   while (node != NULL) 
   { 
       res++; 
       node = node->next; 
   } 
   return res; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    struct Node* head = NULL; 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 
    cout << findSize(head); 
    return 0; 
} 

```

## Java

```java

// A complete working Java program to  
// find size of doubly linked list.  
import java.io.*; 
import java.util.*; 

// Represents a doubly linked list node 
class Node  
{ 
    int data; 
    Node next, prev; 
    Node(int val) 
    { 
        data = val; 
        next = null; 
        prev = null; 
    } 
} 

class GFG  
{ 

    /* Function to add a node to front of doubly  
    linked list */
    static Node push(Node head, int data) 
    { 
        Node new_node = new Node(data); 
        new_node.next = head; 
        new_node.prev = null; 
        if (head != null) 
            head.prev = new_node; 
        head = new_node; 

        return head; 
    } 

    // This function returns size of doubly linked list 
    static int findSize(Node node) 
    { 
        int res = 0; 
        while (node != null)  
        { 
                res++; 
                node = node.next; 
        } 

        return res; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        Node head = null;  
        head = push(head, 4); 
        head = push(head, 3); 
        head = push(head, 2); 
        head = push(head, 1); 
        System.out.println(findSize(head)); 
    } 
} 

// This code is contributed by rachana soma 

```

## Python3

```py

# A complete working Python3 program to 
# find size of doubly linked list. 

# A linked list node 
class Node: 
    def __init__(self): 
        self.data = None
        self.next = None
        self.prev = None

# Function to add a node to front of doubly 
# linked list  
def push( head_ref, new_data): 

    new_node = Node() 
    new_node.data = new_data 
    new_node.next = (head_ref) 
    new_node.prev = None
    if ((head_ref) != None): 
        (head_ref).prev = new_node  
    (head_ref) = new_node 
    return head_ref 

# This function returns size of linked list 
def findSize(node): 

    res = 0
    while (node != None): 
        res = res + 1
        node = node.next

    return res 

# Driver code 
head = None
head = push(head, 4) 
head = push(head, 3) 
head = push(head, 2) 
head = push(head, 1) 
print(findSize(head)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// A complete working C# program to  
// find size of doubly linked list.  
 using System;  

// Represents a doubly linked list node  
public class Node  
{  
    public int data;  
    public Node next, prev;  
    public Node(int val)  
    {  
        data = val;  
        next = null;  
        prev = null;  
    }  
}  

class GFG  
{  

    /* Function to add a node to front of doubly  
    linked list */
    static Node push(Node head, int data)  
    {  
        Node new_node = new Node(data);  
        new_node.next = head;  
        new_node.prev = null;  
        if (head != null)  
            head.prev = new_node;  
        head = new_node;  

        return head;  
    }  

    // This function returns size of doubly linked list  
    static int findSize(Node node)  
    {  
        int res = 0;  
        while (node != null)  
        {  
                res++;  
                node = node.next;  
        }  

        return res;  
    }  

    // Driver Code  
    public static void Main(String []args)  
    {  
        Node head = null;  
        head = push(head, 4);  
        head = push(head, 3);  
        head = push(head, 2);  
        head = push(head, 1);  
        Console.WriteLine(findSize(head));  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**输出**：

```
4

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。