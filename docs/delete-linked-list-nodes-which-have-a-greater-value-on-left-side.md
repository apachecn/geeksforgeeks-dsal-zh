# 删除左侧具有较大值的链表节点

> 原文：[https://www.geeksforgeeks.org/delete-linked-list-nodes-which-have-a-greater-value-on-left-side/](https://www.geeksforgeeks.org/delete-linked-list-nodes-which-have-a-greater-value-on-left-side/)

给定一个单链表，任务是删除左侧所有具有较大值的所有节点。

**示例**：

```
Input: 12->15->10->11->5->6->2->3
Output: Modified Linked List = 12 15

Input: 25->15->6->48->12->5->16->14
Output: Modified Linked List = 14 16 48 

```

**方法**：

1.  用头节点初始化最大值。

2.  遍历列表。

3.  检查下一个节点是否大于`max_node`，然后更新`max_node`的值并移动到下一个节点。

4.  否则删除下一个节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to Delete nodes which have 
// greater value node(s) on right side 
void delNodes(struct Node* head) 
{ 
    struct Node* current = head; 

    // Initialize max 
    struct Node* maxnode = head; 
    struct Node* temp; 

    while (current != NULL && current->next != NULL) { 

        // If current is greater than max, 
        // then update max and move current 
        if (current->next->data >= maxnode->data) { 
            current = current->next; 
            maxnode = current; 
        } 

        // If current is smaller than max, then delete current 
        else { 
            temp = current->next; 
            current->next = temp->next; 
            free(temp); 
        } 
    } 
} 

/* Utility function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

/* Driver program to test above functions */
int main() 
{ 
    struct Node* head = NULL; 

    /* Create following linked list  
    12->15->10->11->5->6->2->3 */
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 11); 
    push(&head, 10); 
    push(&head, 15); 
    push(&head, 12); 

    printf("Given Linked List \n"); 
    printList(head); 

    delNodes(head); 

    printf("Modified Linked List \n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of above approach  
class GFG 
{ 

// Structure of a linked list node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to Delete nodes which have  
// greater value node(s) on right side  
static Node delNodes(Node head)  
{  
    Node current = head;  

    // Initialize max  
    Node maxnode = head;  
    Node temp;  

    while (current != null && current.next != null)  
    {  

        // If current is greater than max,  
        // then update max and move current  
        if (current.next.data >= maxnode.data)  
        {  
            current = current.next;  
            maxnode = current;  
        }  

        // If current is smaller than  
        // max, then delete current  
        else 
        {  
            temp = current.next;  
            current.next = temp.next;  
        }  
    }  
    return head; 
}  

// Utility function to insert  
// a node at the beginning  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    return head_ref; 
}  

// Utility function to print a linked list / 
static Node printList(Node head)  
{  
    while (head != null)  
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
    System.out.println(); 
    return head; 
}  

// Driver code 
public static void main(String args[])  
{  
    Node head = null;  

    /* Create following linked list  
    12->15->10->11->5->6->2->3 */
    head=push(head, 3);  
    head=push(head, 2);  
    head=push(head, 6);  
    head=push(head, 5);  
    head=push(head, 11);  
    head=push(head, 10);  
    head=push(head, 15);  
    head=push(head, 12);  

    System.out.printf("Given Linked List \n");  
    printList(head);  

    head=delNodes(head);  

    System.out.printf("Modified Linked List \n");  
    printList(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of above approach 
import math  

# Structure of a linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to Delete nodes which have 
# greater value node(s) on right side 
def delNodes( head): 
    current = head 

    # Initialize max 
    maxnode = head 

    while (current != None and 
           current.next != None) : 

        # If current is greater than max, 
        # then update max and move current 
        if (current.next.data >= maxnode.data) : 
            current = current.next
            maxnode = current 

        # If current is smaller than max,  
        # then delete current 
        else: 
            temp = current.next
            current.next = temp.next
            #free(temp) 

    return head 

# Utility function to insert a node 
# at the beginning  
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Utility function to print a linked list  
def printList( head): 
    while (head != None) : 
        print(head.data, end = " ") 
        head = head.next

    print() 
    return head 

# Driver Code 
if __name__=='__main__': 
    head = None

    # Create following linked list  
    #12.15.10.11.5.6.2.3  
    head = push(head, 3) 
    head = push(head, 2) 
    head = push(head, 6) 
    head = push(head, 5) 
    head = push(head, 11) 
    head = push(head, 10) 
    head = push(head, 15) 
    head = push(head, 12) 

    print("Given Linked List") 
    printList(head) 

    head = delNodes(head) 

    print("Modified Linked List") 
    printList(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the above approach:  
using System; 

class GFG 
{ 

// Structure of a linked list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to Delete nodes which have  
// greater value node(s) on right side  
static Node delNodes(Node head)  
{  
    Node current = head;  

    // Initialize max  
    Node maxnode = head;  
    Node temp;  

    while (current != null &&  
           current.next != null)  
    {  

        // If current is greater than max,  
        // then update max and move current  
        if (current.next.data >= maxnode.data)  
        {  
            current = current.next;  
            maxnode = current;  
        }  

        // If current is smaller than  
        // max, then delete current  
        else
        {  
            temp = current.next;  
            current.next = temp.next;  
        }  
    }  
    return head; 
}  

// Utility function to insert  
// a node at the beginning  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    return head_ref; 
}  

// Utility function to print a linked list  
static Node printList(Node head)  
{  
    while (head != null)  
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
    Console.WriteLine(); 
    return head; 
}  

// Driver code 
public static void Main(String []args)  
{  
    Node head = null;  

    /* Create following linked list  
    12->15->10->11->5->6->2->3 */
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 11);  
    head = push(head, 10);  
    head = push(head, 15);  
    head = push(head, 12);  

    Console.Write("Given Linked List \n");  
    printList(head);  

    head = delNodes(head);  

    Console.Write("Modified Linked List \n");  
    printList(head);  
} 
}  

// This code is contributed by PrinciRaj1992  

```

**输出**：

```
Given Linked List 
12 15 10 11 5 6 2 3 
Modified Linked List 
12 15

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。