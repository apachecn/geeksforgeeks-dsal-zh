# 在单个循环链表

> 原文：[https://www.geeksforgeeks.org/find-minimum-and-maximum-elements-in-singly-circular-linked-list/](https://www.geeksforgeeks.org/find-minimum-and-maximum-elements-in-singly-circular-linked-list/)

中查找最小和最大元素

给定`N`个节点的循环单链表。 任务是在循环链表中找到最小和最大的元素。

**示例**：

```
Input : List = 99->11->22->33->44->55->66
Output : Minimum = 11, Maximum = 99

Input : List = 12->11->9->33->125->6->99
Output : Minimum = 6, Maximum = 125

```

这个想法是在没有到达最后一个节点的情况下遍历循环链表，并将`max`和`min`变量分别初始化为`INT_MIN`和`INT_MAX`。 之后检查一个条件，如果头部值大于`max`，则将头部值分配给`max`，如果头部值小于`min`，将头部值分配给`min`，然后头部指向下一个节点。 继续此过程，直到最后一个节点。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find minimum and maximum 
// value from singly circular linked list 
#include <bits/stdc++.h> 
using namespace std; 

// structure for a node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to print minimum and maximum 
// nodes of the circular linked list 
void printMinMax(struct Node** head) 
{ 
    // check list is empty 
    if (*head == NULL) { 
        return; 
    } 

    // pointer for traversing 
    struct Node* current; 

    // initialize head to current pointer 
    current = *head; 

    // initialize max int value to min 
    // initialize min int value to max 
    int min = INT_MAX, max = INT_MIN; 

    // While last node is not reached 
    do { 

        // If current node data is lesser for min 
        // then replace it 
        if (current->data < min) { 
            min = current->data; 
        } 

        // If current node data is greater for max 
        // then replace it 
        if (current->data > max) { 
            max = current->data; 
        } 

        current = current->next; 
    }while(current != head); 

    cout << "\nMinimum = " << min << ", Maximum = " << max; 
} 

// Function to insert a node at the end of 
// a Circular linked list 
void insertNode(struct Node** head, int data) 
{ 
    struct Node* current = *head; 
    // Create a new node 
    struct Node* newNode = new Node; 

    // check node is created or not 
    if (!newNode) { 
        printf("\nMemory Error\n"); 
        return; 
    } 

    // insert data into newly created node 
    newNode->data = data; 

    // check list is empty 
    // if not have any node then 
    // make first node it 
    if (*head == NULL) { 
        newNode->next = newNode; 
        *head = newNode; 
        return; 
    } 

    // if list have already some node 
    else { 

        // move firt node to last node 
        while (current->next != *head) { 
            current = current->next; 
        } 

        // put first or head node address 
        // in new node link 
        newNode->next = *head; 

        // put new node address into 
        // last node link(next) 
        current->next = newNode; 
    } 
} 

// Function to print the Circular linked list 
void displayList(struct Node* head) 
{ 

    struct Node* current = head; 

    // if list is empty simply show message 
    if (head == NULL) { 
        printf("\nDisplay List is empty\n"); 
        return; 
    } 

    // traverse first to last node 
    else { 
        do { 
            printf("%d ", current->data); 
            current = current->next; 
        } while (current != head); 
    } 
} 

// Driver Code 
int main() 
{ 
    struct Node* Head = NULL; 

    insertNode(&Head, 99); 
    insertNode(&Head, 11); 
    insertNode(&Head, 22); 
    insertNode(&Head, 33); 
    insertNode(&Head, 44); 
    insertNode(&Head, 55); 
    insertNode(&Head, 66); 

    cout << "Initial List: "; 

    displayList(Head); 

    printMinMax(&Head); 

    return 0; 
} 

```

## Java

```java

// Java program to find minimum and maximum  
// value from singly circular linked list  
class GFG 
{ 

// structure for a node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to print minimum and maximum  
// nodes of the circular linked list  
static void printMinMax(Node head)  
{  
    // check list is empty  
    if (head == null) 
    {  
        return;  
    }  

    // pointer for traversing  
    Node current;  

    // initialize head to current pointer  
    current = head;  

    // initialize max int value to min  
    // initialize min int value to max  
    int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;  

    // While last node is not reached  
    while (current.next != head) 
    {  

        // If current node data is lesser for min  
        // then replace it  
        if (current.data < min)  
        {  
            min = current.data;  
        }  

        // If current node data is greater for max  
        // then replace it  
        if (current.data > max) 
        {  
            max = current.data;  
        }  

        current = current.next;  
    }  

    System.out.println( "\nMinimum = " + min + ", Maximum = " + max);  
}  

// Function to insert a node at the end of  
// a Circular linked list  
static Node insertNode(Node head, int data)  
{  
    Node current = head;  

    // Create a new node  
    Node newNode = new Node();  

    // check node is created or not  
    if (newNode == null)  
    {  
        System.out.printf("\nMemory Error\n");  
        return null;  
    }  

    // insert data into newly created node  
    newNode.data = data;  

    // check list is empty  
    // if not have any node then  
    // make first node it  
    if (head == null)  
    {  
        newNode.next = newNode;  
        head = newNode;  
        return head;  
    }  

    // if list have already some node  
    else 
    {  

        // move firt node to last node  
        while (current.next != head) 
        {  
            current = current.next;  
        }  

        // put first or head node address  
        // in new node link  
        newNode.next = head;  

        // put new node address into  
        // last node link(next)  
        current.next = newNode;  
    }  
    return head; 
}  

// Function to print the Circular linked list  
static void displayList(Node head)  
{  

    Node current = head;  

    // if list is empty simply show message  
    if (head == null) 
    {  
        System.out.printf("\nDisplay List is empty\n");  
        return;  
    }  

    // traverse first to last node  
    else
    {  
        do 
        {  
            System.out.printf("%d ", current.data);  
            current = current.next;  
        } while (current != head);  
    }  
}  

// Driver Code  
public static void main(String args[]) 
{  
    Node Head = null;  

    Head=insertNode(Head, 99);  
    Head=insertNode(Head, 11);  
    Head=insertNode(Head, 22);  
    Head=insertNode(Head, 33);  
    Head=insertNode(Head, 44);  
    Head=insertNode(Head, 55);  
    Head=insertNode(Head, 66);  

    System.out.println("Initial List: ");  

    displayList(Head);  

    printMinMax(Head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find minimum and maximum  
// value from singly circular linked list  
using System; 

class GFG 
{ 

// structure for a node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to print minimum and maximum  
// nodes of the circular linked list  
static void printMinMax(Node head)  
{  
    // check list is empty  
    if (head == null) 
    {  
        return;  
    }  

    // pointer for traversing  
    Node current;  

    // initialize head to current pointer  
    current = head;  

    // initialize max int value to min  
    // initialize min int value to max  
    int min = int.MaxValue, max = int.MinValue;  

    // While last node is not reached  
    while (current.next != head) 
    {  

        // If current node data is lesser for min  
        // then replace it  
        if (current.data < min)  
        {  
            min = current.data;  
        }  

        // If current node data is greater for max  
        // then replace it  
        if (current.data > max) 
        {  
            max = current.data;  
        }  

        current = current.next;  
    }  

    Console.WriteLine( "\nMinimum = " + min + ", Maximum = " + max);  
}  

// Function to insert a node at the end of  
// a Circular linked list  
static Node insertNode(Node head, int data)  
{  
    Node current = head;  

    // Create a new node  
    Node newNode = new Node();  

    // check node is created or not  
    if (newNode == null)  
    {  
        Console.Write("\nMemory Error\n");  
        return null;  
    }  

    // insert data into newly created node  
    newNode.data = data;  

    // check list is empty  
    // if not have any node then  
    // make first node it  
    if (head == null)  
    {  
        newNode.next = newNode;  
        head = newNode;  
        return head;  
    }  

    // if list have already some node  
    else
    {  

        // move firt node to last node  
        while (current.next != head) 
        {  
            current = current.next;  
        }  

        // put first or head node address  
        // in new node link  
        newNode.next = head;  

        // put new node address into  
        // last node link(next)  
        current.next = newNode;  
    }  
    return head; 
}  

// Function to print the Circular linked list  
static void displayList(Node head)  
{  

    Node current = head;  

    // if list is empty simply show message  
    if (head == null) 
    {  
        Console.Write("\nDisplay List is empty\n");  
        return;  
    }  

    // traverse first to last node  
    else
    {  
        do
        {  
            Console.Write("{0} ", current.data);  
            current = current.next;  
        } while (current != head);  
    }  
}  

// Driver Code  
public static void Main() 
{  
    Node Head = null;  

    Head=insertNode(Head, 99);  
    Head=insertNode(Head, 11);  
    Head=insertNode(Head, 22);  
    Head=insertNode(Head, 33);  
    Head=insertNode(Head, 44);  
    Head=insertNode(Head, 55);  
    Head=insertNode(Head, 66);  

    Console.WriteLine("Initial List: ");  

    displayList(Head);  

    printMinMax(Head);  
}  
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
Initial List: 99 11 22 33 44 55 66 
Minimum = 11, Maximum = 99

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。