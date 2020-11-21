# 链表的节点总数为 0 之间

> 原文：[https://www.geeksforgeeks.org/linked-list-sum-nodes-0s/](https://www.geeksforgeeks.org/linked-list-sum-nodes-0s/)

给定一个链表，其中包含一系列用“ 0”分隔的数字。 添加它们并将它们存储在链表中。

**注意**：输入中不会存在连续的零。

例子：

```
Input  : 1->2->3->0->5->4->0->3->2->0
Output : 6->9->5

Input  : 1->2->3->4
Output : 1->2->3->4

```

1.开始遍历链表的节点。

2.在 temp.data！= 0 时进行迭代，并将这些数据添加到变量“ sum”中。

3.当遇到 0 作为该节点的数据时，请更改先前节点的指针。

## C++

```cpp

// C++ program to in-place add linked list  
// nodes between 0s. 
#include <bits/stdc++.h> 
using namespace std; 
#define NODE struct node 

// Structure of a node 
NODE 
{ 
    int data; 
    struct node *next; 
}; 

// Function to create a node 
NODE *getNode(int val) 
{ 
    NODE *temp; 
    temp = (NODE*)malloc(sizeof(NODE)); 
    temp->data = val; 
    temp->next = NULL; 
    return temp; 
} 

// Function to traverse and print Linked List  
void printList(NODE *head) 
{ 
    while(head->next) 
    { 
        cout << head->data << "-> "; 
        head = head->next; 
    } 
    cout << "->" << head->data ; 
} 

void inPlaceStore(NODE *head) 
{ 

    // Function to store numbers till 0  
    if(head->data == 0) 
    { 
        head = head->next; 
    } 

    // To store modified list  
    NODE *res = head; 

    // Traverse linked list and keep  
    // adding nodes between 0s.  
    NODE *temp = head; 
    int sum = 0; 

    while(temp) 
    { 

        // loop to sum the data of nodes till  
        // it encounters 0  
        if(temp->data != 0) 
        { 
            sum += temp->data; 
            temp = temp->next; 
        } 

        // If we encounters 0, we need  
        // to update next pointers  
        else
        { 
            res->data = sum; 
            res->next = temp->next; 
            temp = temp->next; 
            res = temp; 
            sum = 0; 
        } 
    } 
    printList(head); 
} 

// Driver Code 
int main()  
{ 

    NODE *head; 
    head = getNode(3); 
    head->next = getNode(2); 
    head->next->next = getNode(0); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(0); 
    head->next->next->next->next->next->next = getNode(6); 
    head->next->next->next->next->next->next->next = getNode(7); 
    inPlaceStore(head); 
    return 0; 
} 

// This code is contributed by shivanisinghss2110 

```

## C

```c

// C program to in-place add linked list  
// nodes between 0s. 
#include <stdio.h> 
#include<stdlib.h> 
#define NODE struct node 

// Structure of a node 
NODE 
{ 
    int data; 
    struct node *next; 
}; 

// Function to create a node 
NODE *getNode(int val) 
{ 
    NODE *temp; 
    temp = (NODE*)malloc(sizeof(NODE)); 
    temp->data = val; 
    temp->next = NULL; 
    return temp; 
} 

// Function to traverse and print Linked List  
void printList(NODE *head) 
{ 
    while(head->next) 
    { 
        printf("%d->",head->data); 
        head = head->next; 
    } 
    printf("%d\n",head->data); 
} 

void inPlaceStore(NODE *head) 
{ 

    // Function to store numbers till 0  
    if(head->data == 0) 
    { 
        head = head->next; 
    } 

    // To store modified list  
    NODE *res = head; 

    // Traverse linked list and keep  
    // adding nodes between 0s.  
    NODE *temp = head; 
    int sum = 0; 

    while(temp) 
    { 

        // loop to sum the data of nodes till  
        // it encounters 0  
        if(temp->data != 0) 
        { 
            sum+=temp->data; 
            temp = temp->next; 
        } 

        // If we encounters 0, we need  
        // to update next pointers  
        else
        { 

            res->data = sum; 
            res->next = temp->next; 
            temp = temp->next; 
            res = temp; 
            sum = 0; 
        } 
    } 
    printList(head); 
} 

// Driver Code 
int main()  
{ 

    NODE *head; 
    head = getNode(3); 
    head->next = getNode(2); 
    head->next->next = getNode(0); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(0); 
    head->next->next->next->next->next->next = getNode(6); 
    head->next->next->next->next->next->next->next = getNode(7); 
    inPlaceStore(head); 
    return 0; 
} 

// This code is contributed by  
// Kaustav kumar Chanda 

```

## Java

```java

// Java program to in-place add linked list  
// nodes between 0s. 
class Node { 
    int data; 
    Node next; 

    public Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

public class inPlaceStoreLL { 

    // Function to store numbers till 0 
    static void inPlaceStore(Node head) 
    {      
        if(head.data == 0){  
           head = head.next; 
        } 

        // To store modified list  
        Node res = head; 

        // Traverse linked list and keep 
        // adding nodes between 0s. 
        Node temp = head;  
        int sum = 0; 
        while (temp != null) { 

            // loop to sum the data of nodes till  
            // it encounters 0 
            if (temp.data != 0) { 
                sum += temp.data; 
                temp = temp.next; 
            } 

            // If we encounters 0, we need  
            // to update next pointers 
            else { 
                res.data = sum; 
                res.next = temp.next; 
                temp = res.next; 
                res = res.next; 
                sum = 0; 
            } 
        } 
        printList(head); 
    } 

    // Function to traverse and print Linked List 
    static void printList(Node head) 
    { 
        while (head.next != null) { 
            System.out.print(head.data + "-> "); 
            head = head.next; 
        } 
        System.out.println(head.data); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        Node head = new Node(3); 
                head.next = new Node(2); 
                head.next.next = new Node(0); 
                head.next.next.next = new Node(4); 
                head.next.next.next.next = new Node(5); 
                head.next.next.next.next.next = new Node(0); 
                head.next.next.next.next.next.next = new Node(6); 
                head.next.next.next.next.next.next.next = new Node(7); 
        inPlaceStore(head); 

    } 
} 

```

## C#

```cs

// C# program to in-place add linked list  
// nodes between 0s.  
using System; 

public class Node  
{  
    public int data;  
    public Node next;  

    public Node(int data)  
    {  
        this.data = data;  
        this.next = null;  
    }  
}  

public class inPlaceStoreLL  
{  

    // Function to store numbers till 0  
    static void inPlaceStore(Node head)  
    {  
        if(head.data == 0) 
        {  
            head = head.next;  
        }  

        // To store modified list  
        Node res = head;  

        // Traverse linked list and keep  
        // adding nodes between 0s.  
        Node temp = head;  
        int sum = 0;  
        while (temp != null)  
        {  

            // loop to sum the data of nodes till  
            // it encounters 0  
            if (temp.data != 0) 
            {  
                sum += temp.data;  
                temp = temp.next;  
            }  

            // If we encounters 0, we need  
            // to update next pointers  
            else
            {  
                res.data = sum;  
                res.next = temp.next;  
                temp = res.next;  
                res = res.next;  
                sum = 0;  
            }  
        }  
        printList(head);  
    }  

    // Function to traverse and print Linked List  
    static void printList(Node head)  
    {  
        while (head.next != null) 
        {  
            Console.Write(head.data + "-> ");  
            head = head.next;  
        }  
        Console.WriteLine(head.data);  
    }  

    // Driver Code  
    public static void Main()  
    {  
        Node head = new Node(3);  
        head.next = new Node(2);  
        head.next.next = new Node(0);  
        head.next.next.next = new Node(4);  
        head.next.next.next.next = new Node(5);  
        head.next.next.next.next.next = new Node(0);  
        head.next.next.next.next.next.next = new Node(6);  
        head.next.next.next.next.next.next.next = new Node(7);  
        inPlaceStore(head);  
    }  
}  

/* This code is contributed PrinciRaj1992 */

```

**输出**：

```
5-> 9-> 6-> 7

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。