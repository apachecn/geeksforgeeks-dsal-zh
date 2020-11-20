# 比较链接列表

> 原文：[https://www.geeksforgeeks.org/compare-numbers-represented-by-linked-lists/](https://www.geeksforgeeks.org/compare-numbers-represented-by-linked-lists/)

表示的数字

给定指向两个链接列表的头节点的指针。 任务是比较链接列表表示的数字。 列表表示的数字可能包含前导零。

1.  如果数字相等，则打印`0`。

2.  如果第一个链接列表表示的数字更大，则打印`1`。

3.  如果第二个链接列表表示的数字更大，则打印`-1`。

**示例**：

> **输入**：
> List1 = 2-> 3-> 1-> 2-> 4-> NULL
> List2 = 2-> 3 -> 2-> 4-> 2->空
> **输出**：-1
> 
> **输入**：
> List1 = 0-> 0-> 1-> 2-> 4-> NULL
> List2 = 0-> 0 -> 0-> 4-> 2->空
> **输出**：1

**方法**：由于数字可能包含前导零，因此请首先从链接列表的开头删除所有前导零。 在比较它们的长度之后，如果长度不相等，则意味着其中一个数字肯定更大，并根据长度更大而返回 1 或-1。 否则，同时遍历两个列表，并且遍历时，我们比较每个节点上的数字。 如果在任何时候数字不相等，则根据数字值返回 1 或-1。 如果到达链表的末尾，则链表是相同的，因此返回 0。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Structure for a linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* A helper function to remove zeros from  
the start of the linked list */
Node* removeLeadingZeros(struct Node* a) 
{ 
    if (a != NULL && a->data == 0) 
        return removeLeadingZeros(a->next); 
    else
        return a; 
} 

/* A hepler function to find the length of  
linked list*/
int getSize(struct Node* a) 
{ 
    int sz = 0; 
    while (a != NULL) { 
        a = a->next; 
        sz++; 
    } 
    return sz; 
} 

/* Given a reference (pointer to pointer) to the  
head of a list and an int, push a new node on the  
front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* Allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* Set the data */
    new_node->data = new_data; 

    /* Link the old list after the new node */
    new_node->next = (*head_ref); 

    /* Set the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to compar ethe numbers 
// represented as linked lists 
int compare(struct Node* a, 
            struct Node* b) 
{ 

    // Remover leading zeroes from 
    // the linked lists 
    a = removeLeadingZeros(a); 
    b = removeLeadingZeros(b); 

    int lenA = getSize(a); 
    int lenB = getSize(b); 

    if (lenA > lenB) { 

        /* Since the number represented by a  
        has a greater length, it will be greater*/
        return 1; 
    } 
    else if (lenB > lenA) { 
        return -1; 
    } 

    /* If the lenghts of two numbers are equal 
        we have to check their magnitudes*/
    while (a != NULL && b != NULL) { 
        if (a->data > b->data) 
            return 1; 
        else if (a->data < b->data) 
            return -1; 

        /* If we reach here, then a and b are  
        not NULL and their data is same, so  
        move to next nodes in both lists */
        a = a->next; 
        b = b->next; 
    } 

    // If linked lists are identical, then 
    // we need to return zero 
    return 0; 
} 

// Driver code 
int main() 
{ 
    /* The constructed linked lists are :  
    a: 5->6->7  
    b: 2->3->3 */
    struct Node* a = NULL; 
    push(&a, 7); 
    push(&a, 6); 
    push(&a, 5); 

    struct Node* b = NULL; 
    push(&b, 3); 
    push(&b, 3); 
    push(&b, 2); 

    cout << compare(a, b); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG  
{ 

/* Structure for a linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 

/* A helper function to remove zeros from  
the start of the linked list */
static Node removeLeadingZeros(Node a) 
{ 
    if (a != null && a.data == 0) 
        return removeLeadingZeros(a.next); 
    else
        return a; 
} 

/* A hepler function to find the length of  
linked list*/
static int getSize(Node a) 
{ 
    int sz = 0; 
    while (a != null) 
    { 
        a = a.next; 
        sz++; 
    } 
    return sz; 
} 

/* Given a reference (pointer to pointer) to the  
head of a list and an int, push a new node on the  
front of the list. */
static Node push(Node head_ref, int new_data) 
{ 
    /* Allocate node */
    Node new_node = new Node(); 

    /* Set the data */
    new_node.data = new_data; 

    /* Link the old list after the new node */
    new_node.next = head_ref; 

    /* Set the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Function to compar ethe numbers 
// represented as linked lists 
static int compare(Node a, 
                   Node b) 
{ 

    // Remover leading zeroes from 
    // the linked lists 
    a = removeLeadingZeros(a); 
    b = removeLeadingZeros(b); 

    int lenA = getSize(a); 
    int lenB = getSize(b); 

    if (lenA > lenB)  
    { 

        /* Since the number represented by a  
        has a greater length, it will be greater*/
        return 1; 
    } 

    else if (lenB > lenA)  
    { 
        return -1; 
    } 

    /* If the lenghts of two numbers are equal 
        we have to check their magnitudes*/
    while (a != null && b != null)  
    { 
        if (a.data > b.data) 
            return 1; 
        else if (a.data < b.data) 
            return -1; 

        /* If we reach here, then a and b are  
        not null and their data is same, so  
        move to next nodes in both lists */
        a = a.next; 
        b = b.next; 
    } 

    // If linked lists are identical, then 
    // we need to return zero 
    return 0; 
} 

// Driver code 
public static void main(String[] args)  
{ 

    /* The constructed linked lists are :  
    a: 5->6->7  
    b: 2->3->3 */
    Node a = null; 
    a = push(a, 7); 
    a = push(a, 6); 
    a = push(a, 5); 

    Node b = null; 
    b = push(b, 3); 
    b = push(b, 3); 
    b = push(b, 2); 

    System.out.println(compare(a, b)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation of the approach  
using System; 
using System.Collections.Generic;              

class GFG  
{ 

/* Structure for a linked list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

/* A helper function to remove zeros from  
the start of the linked list */
static Node removeLeadingZeros(Node a) 
{ 
    if (a != null && a.data == 0) 
        return removeLeadingZeros(a.next); 
    else
        return a; 
} 

/* A hepler function to find the length of  
linked list*/
static int getSize(Node a) 
{ 
    int sz = 0; 
    while (a != null) 
    { 
        a = a.next; 
        sz++; 
    } 
    return sz; 
} 

/* Given a reference (pointer to pointer) to the  
head of a list and an int, push a new node on the  
front of the list. */
static Node push(Node head_ref, int new_data) 
{ 
    /* Allocate node */
    Node new_node = new Node(); 

    /* Set the data */
    new_node.data = new_data; 

    /* Link the old list after the new node */
    new_node.next = head_ref; 

    /* Set the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Function to compar ethe numbers 
// represented as linked lists 
static int compare(Node a, Node b) 
{ 

    // Remover leading zeroes from 
    // the linked lists 
    a = removeLeadingZeros(a); 
    b = removeLeadingZeros(b); 

    int lenA = getSize(a); 
    int lenB = getSize(b); 

    if (lenA > lenB)  
    { 

        /* Since the number represented by a  
        has a greater length, it will be greater*/
        return 1; 
    } 

    else if (lenB > lenA)  
    { 
        return -1; 
    } 

    /* If the lenghts of two numbers are equal 
        we have to check their magnitudes*/
    while (a != null && b != null)  
    { 
        if (a.data > b.data) 
            return 1; 
        else if (a.data < b.data) 
            return -1; 

        /* If we reach here, then a and b are  
        not null and their data is same, so  
        move to next nodes in both lists */
        a = a.next; 
        b = b.next; 
    } 

    // If linked lists are identical, then 
    // we need to return zero 
    return 0; 
} 

// Driver code 
public static void Main(String[] args)  
{ 

    /* The constructed linked lists are :  
    a: 5->6->7  
    b: 2->3->3 */
    Node a = null; 
    a = push(a, 7); 
    a = push(a, 6); 
    a = push(a, 5); 

    Node b = null; 
    b = push(b, 3); 
    b = push(b, 3); 
    b = push(b, 2); 

    Console.WriteLine(compare(a, b)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
1

```

**时间复杂度**：O（max（N，M）），其中 N 和 M 是链表的长度。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。