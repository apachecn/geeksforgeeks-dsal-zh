# 排序生物群落双链表 | 系列 2

> 原文：[https://www.geeksforgeeks.org/sort-the-biotonic-doubly-linked-list-set-2/](https://www.geeksforgeeks.org/sort-the-biotonic-doubly-linked-list-set-2/)

对给定的生物张力双链表进行排序。 双调双向链表是一个双向链表，它先增加然后减小。 严格增加或严格减少的列表也是生物群落双链表。

**示例**：

```
Input : 2 5 7 12 10 6 4 1
Output : 1 2 4 5 6 7 10 12

Input : 20 17 14 8 3
Output : 3 8 14 17 20

```

 [### 推荐：请首先在 IDE 上尝试您的方法，然后查看解决方案。](https://ide.geeksforgeeks.org) 

在[先前的帖子](https://www.geeksforgeeks.org/sort-biotonic-doubly-linked-list/)中，我们拆分了双音双链表，将后半部分反转，然后将两半合并。 在这篇文章中，讨论了另一种替代方法。 想法是维护两个指针，一个指针最初指向双向链表的 head 元素，另一个指向双向链表的最后一个元素。 比较这两个元素并添加较小的元素以得到一个列表。 该元素指向下一个相邻元素的前进指针。 重复此过程，直到输入双链表的所有元素都添加到列表中。

下面是上述算法的实现：

## C++

```cpp

// C++ implementation to sort the biotonic 
// doubly linked list 

#include <bits/stdc++.h> 
using namespace std; 

// structure of node of the doubly linked list 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

// function to sort a biotonic doubly linked list 
struct Node* sort(struct Node* head) 
{ 
    // If number of elements are less than or 
    // equal to 1 then return. 
    if (head == NULL || head->next == NULL) { 
        return head; 
    } 

    // Pointer to first element of doubly 
    // linked list. 
    Node* front = head; 

    // Pointer to last element of doubly 
    // linked list. 
    Node* last = head; 

    // Dummy node to which resultant 
    // sorted list is added. 
    Node* res = new Node; 

    // Node after which next element 
    // of sorted list is added. 
    Node* resEnd = res; 

    // Node to store next element to 
    // which pointer is moved after 
    // element pointed by that pointer 
    // is added to result list. 
    Node* next; 

    // Find last element of input list. 
    while (last->next != NULL) { 
        last = last->next; 
    } 

    // Compare first and last element 
    // until both pointers are not equal. 
    while (front != last) { 

        // If last element data is less than 
        // or equal to front element data, 
        // then add last element to 
        // result list and change the 
        // last pointer to its previous 
        // element. 
        if (last->data <= front->data) { 
            resEnd->next = last; 
            next = last->prev; 
            last->prev->next = NULL; 
            last->prev = resEnd; 
            last = next; 
            resEnd = resEnd->next; 
        } 

        // If front element is smaller, then 
        // add it to result list and change 
        // front pointer to its next element. 
        else { 
            resEnd->next = front; 
            next = front->next; 
            front->next = NULL; 
            front->prev = resEnd; 
            front = next; 
            resEnd = resEnd->next; 
        } 
    } 

    // Add the single element left to the 
    // result list. 
    resEnd->next = front; 
    front->prev = resEnd; 

    // The head of required sorted list is 
    // next to dummy node res. 
    return res->next; 
} 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to print nodes in a given doubly 
// linked list 
void printList(struct Node* head) 
{ 
    // if list is empty 
    if (head == NULL) 
        cout << "Doubly Linked list empty"; 

    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // Create the doubly linked list: 
    // 2<->5<->7<->12<->10<->6<->4<->1 
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 6); 
    push(&head, 10); 
    push(&head, 12); 
    push(&head, 7); 
    push(&head, 5); 
    push(&head, 2); 

    cout << "Original Doubly linked list:\n"; 
    printList(head); 

    // sort the biotonic DLL 
    head = sort(head); 

    cout << "\nDoubly linked list after sorting:\n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to sort the biotonic  
// doubly linked list  
class GFG 
{ 

// structure of node of the doubly linked list  
static class Node 
{  
    int data;  
    Node next;  
    Node prev;  
};  

// function to sort a biotonic doubly linked list  
static Node sort(Node head)  
{  
    // If number of elements are less than or  
    // equal to 1 then return.  
    if (head == null || head.next == null)  
    {  
        return head;  
    }  

    // Pointer to first element of doubly  
    // linked list.  
    Node front = head;  

    // Pointer to last element of doubly  
    // linked list.  
    Node last = head;  

    // Dummy node to which resultant  
    // sorted list is added.  
    Node res = new Node();  

    // Node after which next element  
    // of sorted list is added.  
    Node resEnd = res;  

    // Node to store next element to  
    // which pointer is moved after  
    // element pointed by that pointer  
    // is added to result list.  
    Node next;  

    // Find last element of input list.  
    while (last.next != null) 
    {  
        last = last.next;  
    }  

    // Compare first and last element  
    // until both pointers are not equal.  
    while (front != last) 
    {  

        // If last element data is less than  
        // or equal to front element data,  
        // then add last element to  
        // result list and change the  
        // last pointer to its previous  
        // element.  
        if (last.data <= front.data) 
        {  
            resEnd.next = last;  
            next = last.prev;  
            last.prev.next = null;  
            last.prev = resEnd;  
            last = next;  
            resEnd = resEnd.next;  
        }  

        // If front element is smaller, then  
        // add it to result list and change  
        // front pointer to its next element.  
        else
        {  
            resEnd.next = front;  
            next = front.next;  
            front.next = null;  
            front.prev = resEnd;  
            front = next;  
            resEnd = resEnd.next;  
        }  
    }  

    // Add the single element left to the  
    // result list.  
    resEnd.next = front;  
    front.prev = resEnd;  

    // The head of required sorted list is  
    // next to dummy node res.  
    return res.next;  
}  

// Function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print nodes in a given doubly  
// linked list  
static void printList(Node head)  
{  
    // if list is empty  
    if (head == null)  
        System.out.print( "Doubly Linked list empty");  

    while (head != null) 
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = null;  

    // Create the doubly linked list:  
    // 2<.5<.7<.12<.10<.6<.4<.1  
    head = push(head, 1);  
    head = push(head, 4);  
    head = push(head, 6);  
    head = push(head, 10);  
    head = push(head, 12);  
    head = push(head, 7);  
    head = push(head, 5);  
    head = push(head, 2);  

    System.out.print("Original Doubly linked list:\n");  
    printList(head);  

    // sort the biotonic DLL  
    head = sort(head);  

    System.out.print("\nDoubly linked list after sorting:\n");  
    printList(head);  
}  
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to sort  
# the biotonic doubly linked list  

# structure of node of the doubly linked list  
class Node:   

    def __init__(self, data): 
        self.data = data 
        self.prev = None
        self.next = None

# function to sort a biotonic doubly linked list  
def sort(head):  

    # If number of elements are less  
    # than or equal to 1 then return.  
    if head == None or head.next == None:   
        return head  

    # Pointer to first element  
    # of doubly linked list.  
    front = head  

    # Pointer to last element  
    # of doubly linked list.  
    last = head  

    # Dummy node to which resultant  
    # sorted list is added.  
    res = Node(None)  

    # Node after which next element  
    # of sorted list is added.  
    resEnd = res  

    # Find last element of input list.  
    while last.next != None:  
        last = last.next 

    # Compare first and last element  
    # until both pointers are not equal.  
    while front != last:   

        # If last element data is less than  
        # or equal to front element data,  
        # then add last element to  
        # result list and change the last  
        # pointer to its previous element.  
        if last.data <= front.data: 
            resEnd.next = last  
            next = last.prev  
            last.prev.next = None 
            last.prev = resEnd  
            last = next 
            resEnd = resEnd.next 

        # If front element is smaller, then  
        # add it to result list and change  
        # front pointer to its next element.  
        else:   
            resEnd.next = front  
            next = front.next 
            front.next = None 
            front.prev = resEnd  
            front = next 
            resEnd = resEnd.next 

    # Add the single element left to the  
    # result list.  
    resEnd.next = front  
    front.prev = resEnd  

    # The head of required sorted list is  
    # next to dummy node res.  
    return res.next 

# Function to insert a node at the  
# beginning of the Doubly Linked List  
def push(head_ref, new_data):  

    # put in the data  
    new_node = Node(new_data)  

    # since we are adding at the  
    # beginning, prev is always None  
    new_node.prev = None 

    # link the old list off the new node  
    new_node.next = head_ref 

    # change prev of head node to new node  
    if head_ref != None:  
        head_ref.prev = new_node  

    # move the head to point to the new node  
    head_ref = new_node 
    return head_ref 

# Function to print nodes in  
# a given doubly linked list  
def printList(head):  

    # If list is empty  
    if head == None:  
        print("Doubly Linked list empty")  

    while head != None:   
        print(head.data, end = " ")  
        head = head.next 

# Driver program to test above  
if __name__ == '__main__': 

    head = None 

    # Create the doubly linked list:  
    # 2<.5<.7<.12<.10<.6<.4<.1  
    head = push(head, 1)  
    head = push(head, 4)  
    head = push(head, 6)  
    head = push(head, 10)  
    head = push(head, 12)  
    head = push(head, 7)  
    head = push(head, 5)  
    head = push(head, 2)  

    print("Original Doubly linked list:")  
    printList(head)  

    # sort the biotonic DLL  
    head = sort(head) 

    print("\nDoubly linked list after sorting:")  
    printList(head) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation to sort the biotonic  
// doubly linked list  
using System; 

class GFG 
{ 

// structure of node of the doubly linked list  
public class Node 
{  
    public int data;  
    public Node next;  
    public Node prev;  
};  

// function to sort a biotonic doubly linked list  
static Node sort(Node head)  
{  
    // If number of elements are less than or  
    // equal to 1 then return.  
    if (head == null || head.next == null)  
    {  
        return head;  
    }  

    // Pointer to first element of doubly  
    // linked list.  
    Node front = head;  

    // Pointer to last element of doubly  
    // linked list.  
    Node last = head;  

    // Dummy node to which resultant  
    // sorted list is added.  
    Node res = new Node();  

    // Node after which next element  
    // of sorted list is added.  
    Node resEnd = res;  

    // Node to store next element to  
    // which pointer is moved after  
    // element pointed by that pointer  
    // is added to result list.  
    Node next;  

    // Find last element of input list.  
    while (last.next != null) 
    {  
        last = last.next;  
    }  

    // Compare first and last element  
    // until both pointers are not equal.  
    while (front != last) 
    {  

        // If last element data is less than  
        // or equal to front element data,  
        // then add last element to  
        // result list and change the  
        // last pointer to its previous  
        // element.  
        if (last.data <= front.data) 
        {  
            resEnd.next = last;  
            next = last.prev;  
            last.prev.next = null;  
            last.prev = resEnd;  
            last = next;  
            resEnd = resEnd.next;  
        }  

        // If front element is smaller, then  
        // add it to result list and change  
        // front pointer to its next element.  
        else
        {  
            resEnd.next = front;  
            next = front.next;  
            front.next = null;  
            front.prev = resEnd;  
            front = next;  
            resEnd = resEnd.next;  
        }  
    }  

    // Add the single element left to the  
    // result list.  
    resEnd.next = front;  
    front.prev = resEnd;  

    // The head of required sorted list is  
    // next to dummy node res.  
    return res.next;  
}  

// Function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print nodes in a given doubly  
// linked list  
static void printList(Node head)  
{  
    // if list is empty  
    if (head == null)  
        Console.Write( "Doubly Linked list empty");  

    while (head != null) 
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = null;  

    // Create the doubly linked list:  
    // 2<.5<.7<.12<.10<.6<.4<.1  
    head = push(head, 1);  
    head = push(head, 4);  
    head = push(head, 6);  
    head = push(head, 10);  
    head = push(head, 12);  
    head = push(head, 7);  
    head = push(head, 5);  
    head = push(head, 2);  

    Console.Write("Original Doubly linked list:\n");  
    printList(head);  

    // sort the biotonic DLL  
    head = sort(head);  

    Console.Write("\nDoubly linked list after sorting:\n");  
    printList(head);  
}  
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Original Doubly linked list:
2 5 7 12 10 6 4 1
Doubly linked list after sorting:
1 2 4 5 6 7 10 12 

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。