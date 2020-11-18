# 将链接列表划分为给定值，如果我们不在乎使列表的元素“稳定”，则

给定一个链表和一个值 x，将一个链表划分为一个值 x，这样所有小于 x 的节点都在所有大于或等于 x 的节点之前。 如果 x 包含在列表中，则 x 的值仅需要在小于 x 的元素之后（请参见下文）。 分区元素 x 可以出现在“右分区”中的任何位置； 它不需要出现在左右分区之间。

相似的问题：[将给定值周围的链表分区，并保持原始顺序](https://www.geeksforgeeks.org/partitioning-a-linked-list-around-a-given-value-and-keeping-the-original-order/)

**示例：**

```
Input :  3 -> 5 -> 10 -> 2 -> 8 -> 2 -> 1 
         x = 5
Output : 1-> 2-> 2-> 3-> 5-> 10-> 8

```

如果我们不在乎使列表的元素“稳定”，那么我们可以通过增加列表的头和尾来重新排列元素。

在这种方法中，我们使用现有节点开始一个“新”列表。 大于枢轴元素的元素放在尾部，而小于元素的元素放在头部。 每次插入元素时，都会更新头或尾。

以下是上述想法的实现。

## C++

```cpp

// C++ program to partition a linked list around a 
// given value. 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// A utility function to create a new node 
Node *newNode(int data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data  = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Function to make a new list(using the existing 
// nodes) and return head of new list. 
struct Node *partition(struct Node *head, int x) 
{ 
    /* Let us initialize start and tail nodes of 
    new list */
    struct Node *tail = head; 

    // Now iterate original list and connect nodes 
    Node *curr = head; 
    while (curr != NULL) 
    { 
        struct Node *next = curr->next; 
        if (curr->data < x) 
        { 
            /* Insert node at head. */
            curr->next = head; 
            head = curr; 
        } 

        else // Append to the list of greater values 
        { 
            /* Insert node at tail. */
            tail->next = curr; 
            tail = curr; 
        } 
        curr = next; 
    } 
    tail->next = NULL; 

    // The head has changed, so we need 
    // to return it to the user. 
    return head; 
} 

/* Function to print linked list */
void printList(struct Node *head) 
{ 
    struct Node *temp = head; 
    while (temp != NULL) 
    { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

// Driver program to run the case 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(3); 
    head->next = newNode(5); 
    head->next->next = newNode(8); 
    head->next->next->next = newNode(2); 
    head->next->next->next->next = newNode(10); 
    head->next->next->next->next->next = newNode(2); 
    head->next->next->next->next->next->next = newNode(1); 

    int x = 5; 
    head = partition(head, x); 
    printList(head); 
    return 0; 
} 

```

## Java

```java

// Java program to partition a linked list  
// around a given value.  
class GfG {  

/* Link list Node */
static class Node  
{  
    int data;  
    Node next;  
} 

// A utility function to create a new node  
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to make a new list  
// (using the existing nodes) and  
// return head of new list.  
static Node partition(Node head, int x)  
{  
    /* Let us initialize start and tail nodes of  
    new list */
    Node tail = head;  

    // Now iterate original list and connect nodes  
    Node curr = head;  
    while (curr != null)  
    {  
        Node next = curr.next;  
        if (curr.data < x)  
        {  
            /* Insert node at head. */
            curr.next = head;  
            head = curr;  
        }  

        else // Append to the list of greater values  
        {  
            /* Insert node at tail. */
            tail.next = curr;  
            tail = curr;  
        }  
        curr = next;  
    }  
    tail.next = null;  

    // The head has changed, so we need  
    // to return it to the user.  
    return head;  
}  

/* Function to print linked list */
static void printList(Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        System.out.print(temp.data + " ");  
        temp = temp.next;  
    }  
}  

// Driver code  
public static void main(String[] args)  
{  
    /* Start with the empty list */
    Node head = newNode(3);  
    head.next = newNode(5);  
    head.next.next = newNode(8);  
    head.next.next.next = newNode(2);  
    head.next.next.next.next = newNode(10);  
    head.next.next.next.next.next = newNode(2);  
    head.next.next.next.next.next.next = newNode(1);  

    int x = 5;  
    head = partition(head, x);  
    printList(head);  
} 
}  

// This code is contributed by prerna saini 

```

## Python3

```py

# Python3 program to partition a  
# linked list around a given value. 
import math 

# Link list Node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# A utility function to create a new node 
def newNode(data): 
    new_node = Node(data) 
    new_node.data = data 
    new_node.next = None
    return new_node 

# Function to make a new list 
# (using the existing nodes)  
# and return head of new list. 
def partition(head, x): 

    # Let us initialize start and 
    # tail nodes of new list  
    tail = head 

    # Now iterate original list  
    # and connect nodes 
    curr = head 
    while (curr != None): 
        next = curr.next
        if (curr.data < x): 

            # Insert node at head.  
            curr.next = head 
            head = curr 

        else: 

            # Append to the list of greater values 
            # Insert node at tail.  
            tail.next = curr 
            tail = curr 

        curr = next

    tail.next = None

    # The head has changed, so we need 
    # to return it to the user. 
    return head 

# Function to print linked list  
def printList(head): 
    temp = head 
    while (temp != None): 
        print(temp.data, end = " ") 
        temp = temp.next

# Driver Code 
if __name__=='__main__':  

    # Start with the empty list  
    head = newNode(3) 
    head.next = newNode(5) 
    head.next.next = newNode(8) 
    head.next.next.next = newNode(2) 
    head.next.next.next.next = newNode(10) 
    head.next.next.next.next.next = newNode(2) 
    head.next.next.next.next.next.next = newNode(1) 

    x = 5
    head = partition(head, x) 
    printList(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# program to partition a linked list  
// around a given value. 
using System; 

class GfG  
{  

/* Link list Node */
class Node  
{  
    public int data;  
    public Node next;  
} 

// A utility function to create a new node  
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to make a new list  
// (using the existing nodes) and  
// return head of new list.  
static Node partition(Node head, int x)  
{  
    /* Let us initialize start and   
    tail nodes of new list */
    Node tail = head;  

    // Now iterate original list 
    // and connect nodes  
    Node curr = head;  
    while (curr != null)  
    {  
        Node next = curr.next;  
        if (curr.data < x)  
        {  
            /* Insert node at head. */
            curr.next = head;  
            head = curr;  
        }  

        else // Append to the list of greater values  
        {  
            /* Insert node at tail. */
            tail.next = curr;  
            tail = curr;  
        }  
        curr = next;  
    }  
    tail.next = null;  

    // The head has changed, so we need  
    // to return it to the user.  
    return head;  
}  

/* Function to print linked list */
static void printList(Node head)  
{  
    Node temp = head;  
    while (temp != null)  
    {  
        Console.Write(temp.data + " ");  
        temp = temp.next;  
    }  
}  

// Driver code  
public static void Main(String[] args)  
{  
    /* Start with the empty list */
    Node head = newNode(3);  
    head.next = newNode(5);  
    head.next.next = newNode(8);  
    head.next.next.next = newNode(2);  
    head.next.next.next.next = newNode(10);  
    head.next.next.next.next.next = newNode(2);  
    head.next.next.next.next.next.next = newNode(1);  

    int x = 5;  
    head = partition(head, x);  
    printList(head);  
} 
} 

// This code has been contributed by Rajput-Ji  

```

**Output:**

```
1  2  2  3  5  8  10  

```

本文由 **Somesh Awasthi 先生**提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

