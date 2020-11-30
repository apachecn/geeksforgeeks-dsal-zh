# 使用双链表的优先级队列

> 原文：[https://www.geeksforgeeks.org/priority-queue-using-doubly-linked-list/](https://www.geeksforgeeks.org/priority-queue-using-doubly-linked-list/)

给定具有优先级的节点，请使用双链表实现优先级队列。

**前提条件**：[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)

**优先级队列上的操作**：

*   `push()`：此函数用于将新数据插入队列。

*   `pop()`：此函数从队列中删除优先级最低的元素。

*   `peek()`/`top()`：此函数用于获取队列中优先级最低的元素，而不将其从队列中删除。

**方法**：

1.  创建一个双链表，其中包含字段`info`（保存节点的信息），优先级（保存节点的优先级），`prev`（指向上一个节点），`next`（指向下一个节点）。

2.  在节点中插入元素和优先级。

3.  按优先级的升序排列节点。

以下是上述步骤的实现：

## C++

```cpp

// CPP code to implement priority 
// queue using doubly linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node { 
    int info; 
    int priority; 
    struct Node *prev, *next; 
}; 

// Function to insert a new Node 
void push(Node** fr, Node** rr, int n, int p) 
{ 
    Node* news = (Node*)malloc(sizeof(Node)); 
    news->info = n; 
    news->priority = p; 

    // If linked list is empty 
    if (*fr == NULL) { 
        *fr = news; 
        *rr = news; 
        news->next = NULL; 
    } 
    else { 
        // If p is less than or equal front 
        // node's priority, then insert at 
        // the front. 
        if (p <= (*fr)->priority) { 
            news->next = *fr; 
            (*fr)->prev = news->next; 
            *fr = news; 
        } 

        // If p is more rear node's priority,  
        // then insert after the rear. 
        else if (p > (*rr)->priority) { 
            news->next = NULL; 
            (*rr)->next = news; 
            news->prev = (*rr)->next; 
            *rr = news; 
        } 

        // Handle other cases 
        else { 

            // Find position where we need to 
            // insert. 
            Node* start = (*fr)->next; 
            while (start->priority > p)  
                start = start->next;             
            (start->prev)->next = news; 
            news->next = start->prev; 
            news->prev = (start->prev)->next; 
            start->prev = news->next; 
        } 
    } 
} 

// Return the value at rear 
int peek(Node *fr) 
{ 
    return fr->info; 
} 

bool isEmpty(Node *fr) 
{ 
    return (fr == NULL); 
} 

// Removes the element with the 
// least priority value form the list 
int pop(Node** fr, Node** rr) 
{ 
    Node* temp = *fr; 
    int res = temp->info; 
    (*fr) = (*fr)->next; 
    free(temp); 
    if (*fr == NULL)  
       *rr = NULL; 
    return res; 
} 

// Driver code 
int main() 
{ 
    Node *front = NULL, *rear = NULL; 
    push(&front, &rear, 2, 3); 
    push(&front, &rear, 3, 4); 
    push(&front, &rear, 4, 5); 
    push(&front, &rear, 5, 6); 
    push(&front, &rear, 6, 7); 
    push(&front, &rear, 1, 2); 

    cout << pop(&front, &rear) << endl; 
    cout << peek(front); 

    return 0; 
} 

```

## Java

```java

// Java code to implement priority  
// queue using doubly linked list  

import java.util.* ; 

class Solution 
{ 

static Node front , rear; 

// Linked List Node  
static class Node {  
    int info;  
    int priority;  
     Node prev, next;  
} 

// Function to insert a new Node  
static void push(Node fr, Node rr, int n, int p)  
{  
    Node news = new Node();  
    news.info = n;  
    news.priority = p;  

    // If linked list is empty  
    if (fr == null) {  
        fr = news;  
        rr = news;  
        news.next = null;  
    }  
    else {  
        // If p is less than or equal front  
        // node's priority, then insert at  
        // the front.  
        if (p <= (fr).priority) {  
            news.next = fr;  
            (fr).prev = news.next;  
            fr = news;  
        }  

        // If p is more rear node's priority,   
        // then insert after the rear.  
        else if (p > (rr).priority) {  
            news.next = null;  
            (rr).next = news;  
            news.prev = (rr).next;  
            rr = news;  
        }  

        // Handle other cases  
        else {  

            // Find position where we need to  
            // insert.  
            Node start = (fr).next;  
            while (start.priority > p)   
                start = start.next;              
            (start.prev).next = news;  
            news.next = start.prev;  
            news.prev = (start.prev).next;  
            start.prev = news.next;  
        }  
    }  
    front =fr; 
    rear=rr; 
}  

// Return the value at rear  
static int peek(Node fr)  
{  
    return fr.info;  
}  

static boolean isEmpty(Node fr)  
{  
    return (fr == null);  
}  

// Removes the element with the  
// least priority value form the list  
static int pop(Node fr, Node rr)  
{  
    Node temp = fr;  
    int res = temp.info;  
    (fr) = (fr).next;  
    if (fr == null)   
       rr = null;  

    front =fr; 
    rear=rr; 
       return res;  

}  

// Driver code  
public static void main(String args[])  
{  

    push(front, rear, 2, 3);  
    push(front, rear, 3, 4);  
    push(front, rear, 4, 5);  
    push(front, rear, 5, 6);  
    push(front, rear, 6, 7);  
    push(front, rear, 1, 2);  

    System.out.println( pop(front, rear));  
    System.out.println( peek(front));  

}  
} 

// This code is contributed 
// by Arnab Kundu 

```

## C#

```cs

// C# code to implement priority  
// queue using doubly linked list  
using System; 

class GFG 
{ 
public static Node front, rear; 

// Linked List Node  
public class Node 
{ 
    public int info; 
    public int priority; 
    public Node prev, next; 
} 

// Function to insert a new Node  
public static void push(Node fr, Node rr,  
                        int n, int p) 
{ 
    Node news = new Node(); 
    news.info = n; 
    news.priority = p; 

    // If linked list is empty  
    if (fr == null) 
    { 
        fr = news; 
        rr = news; 
        news.next = null; 
    } 
    else
    { 
        // If p is less than or equal front  
        // node's priority, then insert at  
        // the front.  
        if (p <= (fr).priority) 
        { 
            news.next = fr; 
            (fr).prev = news.next; 
            fr = news; 
        } 

        // If p is more rear node's priority,  
        // then insert after the rear.  
        else if (p > (rr).priority) 
        { 
            news.next = null; 
            (rr).next = news; 
            news.prev = (rr).next; 
            rr = news; 
        } 

        // Handle other cases  
        else
        { 

            // Find position where we  
            // need to insert.  
            Node start = (fr).next; 
            while (start.priority > p) 
            { 
                start = start.next; 
            } 
            (start.prev).next = news; 
            news.next = start.prev; 
            news.prev = (start.prev).next; 
            start.prev = news.next; 
        } 
    } 
    front = fr; 
    rear = rr; 
} 

// Return the value at rear  
public static int peek(Node fr) 
{ 
    return fr.info; 
} 

public static bool isEmpty(Node fr) 
{ 
    return (fr == null); 
} 

// Removes the element with the  
// least priority value form the list  
public static int pop(Node fr, Node rr) 
{ 
    Node temp = fr; 
    int res = temp.info; 
    (fr) = (fr).next; 
    if (fr == null) 
    { 
        rr = null; 
    } 

    front = fr; 
    rear = rr; 
    return res; 
} 

// Driver code  
public static void Main(string[] args) 
{ 
    push(front, rear, 2, 3); 
    push(front, rear, 3, 4); 
    push(front, rear, 4, 5); 
    push(front, rear, 5, 6); 
    push(front, rear, 6, 7); 
    push(front, rear, 1, 2); 

    Console.WriteLine(pop(front, rear)); 
    Console.WriteLine(peek(front)); 
} 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
1
2

```

**相关文章**：

[使用单链表的优先级队列](https://www.geeksforgeeks.org/priority-queue-using-linked-list/)

**时间复杂度以及与[二叉堆](https://www.geeksforgeeks.org/binary-heap/)的比较**：

```
               peek()    push()    pop()
-----------------------------------------
Linked List |   O(1)      O(n)      O(1)
            |
Binary Heap |   O(1)    O(Log n)   O(Log n)
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。