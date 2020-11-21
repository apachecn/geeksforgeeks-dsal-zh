# 递归查找单链表的中间

> 原文：[https://www.geeksforgeeks.org/find-middle-singly-linked-list-recursively/](https://www.geeksforgeeks.org/find-middle-singly-linked-list-recursively/)

给定一个单链表，任务是找到链表的中间位置。

**示例**：

```
Input  : 1->2->3->4->5  
Output : 3

Input  : 1->2->3->4->5->6
Output : 4

```

我们已经讨论了[迭代解决方案](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)。 本文讨论了迭代解决方案。 假定该值为 n，则以递归方式计算列表中节点的总数，并进行一半的计算。 然后，对于每个调用，将递归 n 递减 1。 返回 n 为零的节点。

## C++

```cpp

// C++ program for Recursive approach to find 
// middle of singly linked list 
#include <iostream> 
using namespace std; 

// Tree Node Structure 
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// Create new Node 
Node* newLNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Function for finding midpoint recursively 
void midpoint_util(Node* head, int* n, Node** mid) 
{ 

    // If we reached end of linked list 
    if (head == NULL) 
    { 
        *n = (*n) / 2; 
        return; 
    } 

    *n = *n + 1; 

    midpoint_util(head->next, n, mid); 

    // Rolling back, decrement n by one 
    *n = *n - 1; 
    if (*n == 0) 
    { 

        // Final answer 
        *mid = head; 
    } 
} 

Node* midpoint(Node* head) 
{ 
    Node* mid = NULL; 
    int n = 1; 
    midpoint_util(head, &n, &mid); 
    return mid; 
} 

int main() 
{ 
    Node* head = newLNode(1); 
    head->next = newLNode(2); 
    head->next->next = newLNode(3); 
    head->next->next->next = newLNode(4); 
    head->next->next->next->next = newLNode(5); 
    Node* result = midpoint(head); 
    cout << result->data << endl; 
    return 0; 
} 

```

## Java

```java

// Java program for Recursive approach to find  
// middle of singly linked list  
class GFG 
{ 

// Tree Node Structure  
static class Node  
{  
    int data;  
    Node next;  
};  

// Create new Node  
static Node newLNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  

static int n; 
static Node mid; 

// Function for finding midpoint recursively  
static void midpoint_util(Node head )  
{  

    // If we reached end of linked list  
    if (head == null)  
    {  
        n = (n) / 2;  
        return;  
    }  

    n = n + 1;  

    midpoint_util(head.next);  

    // Rolling back, decrement n by one  
    n = n - 1;  
    if (n == 0)  
    {  

        // Final answer  
        mid = head;  
    }  
}  

static Node midpoint(Node head)  
{  
    mid = null;  
    n = 1;  
    midpoint_util(head);  
    return mid;  
}  

// Driver code 
public static void main(String args[]) 
{  
    Node head = newLNode(1);  
    head.next = newLNode(2);  
    head.next.next = newLNode(3);  
    head.next.next.next = newLNode(4);  
    head.next.next.next.next = newLNode(5);  
    Node result = midpoint(head);  
    System.out.print( result.data );  
} 
}  

// This code is contributed by Arnab Kundu  

```

## Python3

```py

# Python3 program for Recursive approach 
# to find middle of singly linked list 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Create new Node 
def newLNode(data): 

    temp = Node(data) 
    temp.data = data 
    temp.next = None
    return temp 

mid = None
n = 0

# Function for finding midpoint recursively 
def midpoint_util(head ): 

    global n 
    global mid 

    # If we reached end of linked list 
    if (head == None): 

        n = int((n) / 2) 
        return

    n = n + 1

    midpoint_util(head.next) 

    # Rolling back, decrement n by one 
    n = n - 1
    if (n == 0): 

        # Final answer 
        mid = head 

def midpoint(head): 

    global n 
    global mid 

    mid = None
    n = 1
    midpoint_util(head) 
    return mid 

# Driver Code  
if __name__=='__main__':  

    head = newLNode(1) 
    head.next = newLNode(2) 
    head.next.next = newLNode(3) 
    head.next.next.next = newLNode(4) 
    head.next.next.next.next = newLNode(5) 
    result = midpoint(head) 
    print( result.data ) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program for Recursive approach to find  
// middle of singly linked list  
using System;  
class GFG 
{ 

// Tree Node Structure  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Create new Node  
static Node newLNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  

static int n; 
static Node mid; 

// Function for finding midpoint recursively  
static void midpoint_util(Node head )  
{  

    // If we reached end of linked list  
    if (head == null)  
    {  
        n = (n) / 2;  
        return;  
    }  

    n = n + 1;  

    midpoint_util(head.next);  

    // Rolling back, decrement n by one  
    n = n - 1;  
    if (n == 0)  
    {  

        // Final answer  
        mid = head;  
    }  
}  

static Node midpoint(Node head)  
{  
    mid = null;  
    n = 1;  
    midpoint_util(head);  
    return mid;  
}  

// Driver code 
public static void Main() 
{  
    Node head = newLNode(1);  
    head.next = newLNode(2);  
    head.next.next = newLNode(3);  
    head.next.next.next = newLNode(4);  
    head.next.next.next.next = newLNode(5);  
    Node result = midpoint(head);  
    Console.WriteLine( result.data );  
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
3
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。