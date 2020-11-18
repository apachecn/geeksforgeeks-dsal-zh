# 使用链接列表

的优先级队列

使用链接列表实现优先级队列。

**Operations on Priority Queue :**

*   push（）：此函数用于将新数据插入队列。

*   pop（）：此函数从队列中删除优先级最高的元素。

*   peek（）/ top（）：此函数用于获取队列中优先级最高的元素，而无需将其从队列中删除。

可以使用常见的数据结构（如数组，链接列表，堆和二叉树）来实现优先级队列。

**先决条件**：

[链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)

这样创建列表，以使优先级最高的元素始终位于列表的开头。 该列表根据元素的优先级以降序排列。 这使我们可以删除`O(1)`时间中的最高优先级元素。 要插入元素，我们必须遍历列表并找到合适的位置插入节点，以便维护优先级队列的整体顺序。 这使 push（）操作花费`O(n)`时间。 pop（）和 peek（）操作在固定时间内执行。

**算法**：

PUSH（HEAD，数据，优先级）

步骤 1：使用 DATA 和 PRIORITY 创建新节点

步骤 2：检查 HEAD 是否具有较低的优先级。 如果是，请执行步骤 3-4，然后结束。 否则，转到步骤 5。

步骤 3：NEW-> NEXT = HEAD

步骤 4：HEAD = NEW

步骤 5：将 TEMP 设置为列表的标题

步骤 6：While TEMP- >下一个！= NULL 和 TEMP->下一个->优先级>优先级

步骤 7：TEMP = TEMP->下一个

[循环结束]

步骤 8 ：新->下一个=温度->下一个

步骤 9：温度->下一个=新

步骤 10：结束

POP（HEAD）

步骤 2：将列表的开头设置为列表中的下一个节点。 HEAD = HEAD-> NEXT。

步骤 3：释放列表顶部的节点

步骤 4：结束

PEEK（HEAD）：

步骤 1：返回 HEAD-> DATA

步骤 2：结束

下面是该算法的实现：

## C++

```cpp

// C++ code to implement Priority Queue 
// using Linked List 
#include <bits/stdc++.h> 
using namespace std; 

// Node 
typedef struct node 
{ 
    int data; 

    // Lower values indicate  
    // higher priority 
    int priority; 

    struct node* next; 

} Node; 

// Function to create a new node 
Node* newNode(int d, int p) 
{ 
    Node* temp = (Node*)malloc(sizeof(Node)); 
    temp->data = d; 
    temp->priority = p; 
    temp->next = NULL; 

    return temp; 
} 

// Return the value at head 
int peek(Node** head) 
{ 
    return (*head)->data; 
} 

// Removes the element with the 
// highest priority form the list 
void pop(Node** head) 
{ 
    Node* temp = *head; 
    (*head) = (*head)->next; 
    free(temp); 
} 

// Function to push according to priority 
void push(Node** head, int d, int p) 
{ 
    Node* start = (*head); 

    // Create new Node 
    Node* temp = newNode(d, p); 

    // Special Case: The head of list has  
    // lesser priority than new node. So  
    // insert newnode before head node  
    // and change head node. 
    if ((*head)->priority > p) 
    { 

        // Insert New Node before head 
        temp->next = *head; 
        (*head) = temp; 
    } 
    else
    { 

        // Traverse the list and find a 
        // position to insert new node 
        while (start->next != NULL &&  
               start->next->priority < p)  
        { 
            start = start->next; 
        } 

        // Either at the ends of the list 
        // or at required position 
        temp->next = start->next; 
        start->next = temp; 
    } 
} 

// Function to check is list is empty 
int isEmpty(Node** head) 
{ 
    return (*head) == NULL; 
} 

// Driver code 
int main() 
{ 

    // Create a Priority Queue 
    // 7->4->5->6 
    Node* pq = newNode(4, 1); 
    push(&pq, 5, 2); 
    push(&pq, 6, 3); 
    push(&pq, 7, 0); 

    while (!isEmpty(&pq))  
    { 
        cout << " " << peek(&pq); 
        pop(&pq); 
    } 
    return 0; 
} 

// This code is contributed by shivanisinghss2110 

```

## C

```c

// C code to implement Priority Queue 
// using Linked List 
#include <stdio.h> 
#include <stdlib.h> 

// Node 
typedef struct node { 
    int data; 

    // Lower values indicate higher priority 
    int priority; 

    struct node* next; 

} Node; 

// Function to Create A New Node 
Node* newNode(int d, int p) 
{ 
    Node* temp = (Node*)malloc(sizeof(Node)); 
    temp->data = d; 
    temp->priority = p; 
    temp->next = NULL; 

    return temp; 
} 

// Return the value at head 
int peek(Node** head) 
{ 
    return (*head)->data; 
} 

// Removes the element with the 
// highest priority form the list 
void pop(Node** head) 
{ 
    Node* temp = *head; 
    (*head) = (*head)->next; 
    free(temp); 
} 

// Function to push according to priority 
void push(Node** head, int d, int p) 
{ 
    Node* start = (*head); 

    // Create new Node 
    Node* temp = newNode(d, p); 

    // Special Case: The head of list has lesser 
    // priority than new node. So insert new 
    // node before head node and change head node. 
    if ((*head)->priority > p) { 

        // Insert New Node before head 
        temp->next = *head; 
        (*head) = temp; 
    } 
    else { 

        // Traverse the list and find a 
        // position to insert new node 
        while (start->next != NULL && 
               start->next->priority < p) { 
            start = start->next; 
        } 

        // Either at the ends of the list 
        // or at required position 
        temp->next = start->next; 
        start->next = temp; 
    } 
} 

// Function to check is list is empty 
int isEmpty(Node** head) 
{ 
    return (*head) == NULL; 
} 

// Driver code 
int main() 
{ 
    // Create a Priority Queue 
    // 7->4->5->6 
    Node* pq = newNode(4, 1); 
    push(&pq, 5, 2); 
    push(&pq, 6, 3); 
    push(&pq, 7, 0); 

    while (!isEmpty(&pq)) { 
        printf("%d ", peek(&pq)); 
        pop(&pq); 
    } 

    return 0; 
} 

```

## Java

```java

// Java code to implement Priority Queue  
// using Linked List  
import java.util.* ; 

class Solution 
{ 

// Node  
 static class Node {  
    int data;  

    // Lower values indicate higher priority  
    int priority;  

     Node next;  

} 

static Node node = new Node(); 

// Function to Create A New Node  
static Node newNode(int d, int p)  
{  
    Node temp = new Node();  
    temp.data = d;  
    temp.priority = p;  
    temp.next = null;  

    return temp;  
}  

// Return the value at head  
static int peek(Node head)  
{  
    return (head).data;  
}  

// Removes the element with the  
// highest priority form the list  
static Node pop(Node head)  
{  
    Node temp = head;  
    (head)  = (head).next;  
    return head; 
}    

// Function to push according to priority  
static Node push(Node head, int d, int p)  
{  
    Node start = (head);  

    // Create new Node  
    Node temp = newNode(d, p);  

    // Special Case: The head of list has lesser  
    // priority than new node. So insert new  
    // node before head node and change head node.  
    if ((head).priority > p) {  

        // Insert New Node before head  
        temp.next = head;  
        (head) = temp;  
    }  
    else {  

        // Traverse the list and find a  
        // position to insert new node  
        while (start.next != null &&  
               start.next.priority < p) {  
            start = start.next;  
        }  

        // Either at the ends of the list  
        // or at required position  
        temp.next = start.next;  
        start.next = temp;  
    }  
    return head; 
}  

// Function to check is list is empty  
static int isEmpty(Node head)  
{  
    return ((head) == null)?1:0;  
}  

// Driver code  
public static void main(String args[]) 
{  
    // Create a Priority Queue  
    // 7.4.5.6  
    Node pq = newNode(4, 1);  
    pq =push(pq, 5, 2);  
    pq =push(pq, 6, 3);  
    pq =push(pq, 7, 0);  

    while (isEmpty(pq)==0) {  
        System.out.printf("%d ", peek(pq));  
        pq=pop(pq);  
    }  

}  
} 

// This code is contributed 
// by Arnab Kundu 

```

## C#

```cs

// C# code to implement Priority Queue  
// using Linked List  
using System; 

class GFG 
{ 
// Node  
public class Node 
{ 
    public int data; 

    // Lower values indicate  
    // higher priority  
    public int priority; 

    public Node next; 
} 

public static Node node = new Node(); 

// Function to Create A New Node  
public static Node newNode(int d, int p) 
{ 
    Node temp = new Node(); 
    temp.data = d; 
    temp.priority = p; 
    temp.next = null; 

    return temp; 
} 

// Return the value at head  
public static int peek(Node head) 
{ 
    return (head).data; 
} 

// Removes the element with the  
// highest priority form the list  
public static Node pop(Node head) 
{ 
    Node temp = head; 
    (head) = (head).next; 
    return head; 
} 

// Function to push according to priority  
public static Node push(Node head,  
                        int d, int p) 
{ 
    Node start = (head); 

    // Create new Node  
    Node temp = newNode(d, p); 

    // Special Case: The head of list 
    // has lesser priority than new node.  
    // So insert new node before head node  
    // and change head node.  
    if ((head).priority > p) 
    { 

        // Insert New Node before head  
        temp.next = head; 
        (head) = temp; 
    } 
    else
    { 

        // Traverse the list and find a  
        // position to insert new node  
        while (start.next != null &&  
               start.next.priority < p) 
        { 
            start = start.next; 
        } 

        // Either at the ends of the list  
        // or at required position  
        temp.next = start.next; 
        start.next = temp; 
    } 
    return head; 
} 

// Function to check is list is empty  
public static int isEmpty(Node head) 
{ 
    return ((head) == null) ? 1 : 0; 
} 

// Driver code  
public static void Main(string[] args) 
{ 
    // Create a Priority Queue  
    // 7.4.5.6  
    Node pq = newNode(4, 1); 
    pq = push(pq, 5, 2); 
    pq = push(pq, 6, 3); 
    pq = push(pq, 7, 0); 

    while (isEmpty(pq) == 0) 
    { 
        Console.Write("{0:D} ", peek(pq)); 
        pq = pop(pq); 
    } 
} 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
7 4 5 6 

```

**时间复杂度以及与[二元堆](https://www.geeksforgeeks.org/binary-heap/)**：的比较

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