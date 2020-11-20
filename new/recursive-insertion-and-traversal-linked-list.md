# 递归插入和遍历链表

> 原文：[https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)

我们讨论了[链表插入](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的不同方法。 如何递归地创建一个链表？

**递归插入到最后**：

要使用递归创建链表，请按照以下步骤操作。 下面的步骤在链表的末尾递归插入一个新节点。

```

// Function to insert a new node at the 
// end of linked list using recursion. 
Node* insertEnd(Node* head, int data) 
{ 
    // If linked list is empty, create a  
    // new node (Assuming newNode() allocates 
    // a new node with given data) 
    if (head == NULL)  
         return newNode(data); 

    // If we have not reached end, keep traversing 
    // recursively. 
    else 
        head->next = insertEnd(head->next, data); 
    return head; 
} 

```

**递归遍历列表**：

这个想法很简单，我们打印当前节点，然后递归其余列表。

```

void traverse(Node* head) 
{ 
    if (head == NULL) 
       return; 

    // If head is not NULL, print current node 
    // and recur for remaining list    
    cout << head->data << " "; 

    traverse(head->next); 
} 

```

**完整程序**：

下面是完整的程序，用于演示插入和遍历链表的工作。

## C++

```cpp

// Recursive CPP program to recursively insert 
// a node and recursively print the list. 
#include <bits/stdc++.h> 
using namespace std; 
struct Node { 
    int data; 
    Node* next; 
}; 

// Allocates a new node with given data 
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Function to insert a new node at the 
// end of linked list using recursion. 
Node* insertEnd(Node* head, int data) 
{ 
    // If linked list is empty, create a  
    // new node (Assuming newNode() allocates 
    // a new node with given data) 
    if (head == NULL)  
         return newNode(data); 

    // If we have not reached end, keep traversing 
    // recursively. 
    else 
        head->next = insertEnd(head->next, data); 
    return head; 
} 

void traverse(Node* head) 
{ 
    if (head == NULL) 
       return; 

    // If head is not NULL, print current node 
    // and recur for remaining list    
    cout << head->data << " "; 

    traverse(head->next); 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    head = insertEnd(head, 6); 
    head = insertEnd(head, 8); 
    head = insertEnd(head, 10); 
    head = insertEnd(head, 12); 
    head = insertEnd(head, 14); 
    traverse(head); 
} 

```

## Java

```java

// Recursive Java program to recursively insert  
// a node and recursively print the list.  
class GFG 
{ 

static class Node  
{  
    int data;  
    Node next;  
};  

// Allocates a new node with given data  
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to insert a new node at the  
// end of linked list using recursion.  
static Node insertEnd(Node head, int data)  
{  
    // If linked list is empty, create a  
    // new node (Assuming newNode() allocates  
    // a new node with given data)  
    if (head == null)  
        return newNode(data);  

    // If we have not reached end, keep traversing  
    // recursively.  
    else
        head.next = insertEnd(head.next, data);  
    return head;  
}  

static void traverse(Node head)  
{  
    if (head == null)  
    return;  

    // If head is not null, print current node  
    // and recur for remaining list  
    System.out.print( head.data + " ");  

    traverse(head.next);  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = null;  
    head = insertEnd(head, 6);  
    head = insertEnd(head, 8);  
    head = insertEnd(head, 10);  
    head = insertEnd(head, 12);  
    head = insertEnd(head, 14);  
    traverse(head);  
}  
} 

// This code is contributed by andrew1234 

```

## Python3

```py

# Recursive Python3 program to  
# recursively insert a node and 
# recursively print the list. 
import math 

class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Allocates a new node with given data 
def newNode(data): 
    new_node = Node(data) 
    new_node.data = data 
    new_node.next = None
    return new_node 

# Function to insert a new node at the 
# end of linked list using recursion. 
def insertEnd(head, data): 

    # If linked list is empty, create a  
    # new node (Assuming newNode() allocates 
    # a new node with given data) 
    if (head == None): 
        return newNode(data) 

    # If we have not reached end,  
    # keep traversing recursively. 
    else: 
        head.next = insertEnd(head.next, data) 
    return head 

def traverse(head): 
    if (head == None): 
        return

    # If head is not None, print current node 
    # and recur for remaining list  
    print(head.data, end = " "); 
    traverse(head.next) 

# Driver code 
if __name__=='__main__':  
    head = None
    head = insertEnd(head, 6) 
    head = insertEnd(head, 8) 
    head = insertEnd(head, 10) 
    head = insertEnd(head, 12) 
    head = insertEnd(head, 14) 
    traverse(head) 

# This code is contributed by sapna singh 

```

## C#

```cs

// Recursive C# program to recursively insert  
// a node and recursively print the list.  
using System;  

class GFG  
{  

public class Node  
{  
    public int data;  
    public Node next;  
};  

// Allocates a new node with given data  
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to insert a new node at the  
// end of linked list using recursion.  
static Node insertEnd(Node head, int data)  
{  
    // If linked list is empty, create a  
    // new node (Assuming newNode() allocates  
    // a new node with given data)  
    if (head == null)  
        return newNode(data);  

    // If we have not reached end, keep traversing  
    // recursively.  
    else
        head.next = insertEnd(head.next, data);  
    return head;  
}  

static void traverse(Node head)  
{  
    if (head == null)  
    return;  

    // If head is not null, print current node  
    // and recur for remaining list  
    Console.Write(head.data + " ");  

    traverse(head.next);  
}  

// Driver code  
public static void Main(String []args)  
{  
    Node head = null;  
    head = insertEnd(head, 6);  
    head = insertEnd(head, 8);  
    head = insertEnd(head, 10);  
    head = insertEnd(head, 12);  
    head = insertEnd(head, 14);  
    traverse(head);  
}  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
6 8 10 12 14
```

本文由 [**AMIT KUMAR**](https://auth.geeksforgeeks.org/profile.php?user=Amit kumar) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

