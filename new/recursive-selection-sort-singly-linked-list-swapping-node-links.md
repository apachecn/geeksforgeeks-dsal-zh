# 单链列表的递归选择排序| 交换节点链接

给定一个包含 **n** 个节点的单链列表。 问题是使用递归选择排序技术对列表进行排序。 该方法应使其涉及交换节点链接而不是交换节点数据。
![sorting image](img/30e3fe49cc11f92ab4b7277b9fee727d.png)

**示例：**

```
Input : 10 -> 12 -> 8 -> 4 -> 6
Output : 4 -> 6 -> 8 -> 10 -> 12

```

在选择排序中，我们首先找到最小元素，将其与起始节点交换，然后递归以获取剩余列表。 下面是链表的这些步骤的递归实现。

```
recurSelectionSort(head)
     if head->next == NULL
         return head
     Initialize min = head
     Initialize beforeMin = NULL
     Initialize ptr = head

     while ptr->next != NULL 
         if min->data > ptr->next->data
         min = ptr->next
         beforeMin = ptr
     ptr = ptr->next    

     if min != head
         swapNodes(&head, head, min, beforeMin)

     head->next = recurSelectionSort(head->next)
     return head

swapNodes(head_ref, currX, currY, prevY)
     head_ref = currY
     prevY->next = currX

     Initialize temp = currY->next
     currY->next = currX->next
     currX->next  = temp    

```

**swapNodes（head_ref，currX，currY，prevY）**基于此处[讨论的方法](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)，但为实现此帖子而对其进行了相应的修改。

## C++

```cpp

// C++ implementation of recursive selection sort 
// for singly linked list | Swapping node links 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to swap nodes 'currX' and 'currY' in a 
// linked list without swapping data 
void swapNodes(struct Node** head_ref, struct Node* currX, 
               struct Node* currY, struct Node* prevY) 
{ 
    // make 'currY' as new head 
    *head_ref = currY; 

    // adjust links 
    prevY->next = currX; 

    // Swap next pointers 
    struct Node* temp = currY->next; 
    currY->next = currX->next; 
    currX->next = temp; 
} 

// function to sort the linked list using 
// recursive selection sort technique 
struct Node* recurSelectionSort(struct Node* head) 
{ 
    // if there is only a single node 
    if (head->next == NULL) 
        return head; 

    // 'min' - pointer to store the node having 
    // minimum data value 
    struct Node* min = head; 

    // 'beforeMin' - pointer to store node previous 
    // to 'min' node 
    struct Node* beforeMin = NULL; 
    struct Node* ptr; 

    // traverse the list till the last node 
    for (ptr = head; ptr->next != NULL; ptr = ptr->next) { 

        // if true, then update 'min' and 'beforeMin' 
        if (ptr->next->data < min->data) { 
            min = ptr->next; 
            beforeMin = ptr; 
        } 
    } 

    // if 'min' and 'head' are not same, 
    // swap the head node with the 'min' node 
    if (min != head) 
        swapNodes(&head, head, min, beforeMin); 

    // recursively sort the remaining list 
    head->next = recurSelectionSort(head->next); 

    return head; 
} 

// function to sort the given linked list 
void sort(struct Node** head_ref) 
{ 
    // if list is empty 
    if ((*head_ref) == NULL) 
        return; 

    // sort the list using recursive selection 
    // sort technique 
    *head_ref = recurSelectionSort(*head_ref); 
} 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node 
    struct Node* new_node =  
         (struct Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list to the new node 
    new_node->next = (*head_ref); 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// function to print the linked list 
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->12->8->4->6 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 12); 
    push(&head, 10); 

    cout << "Linked list before sorting:n"; 
    printList(head); 

    // sort the linked list 
    sort(&head); 

    cout << "\nLinked list after sorting:n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of recursive selection sort  
// for singly linked list | Swapping node links  
class GFG 
{ 

// A Linked list node  
static class Node 
{  
    int data;  
    Node next;  
};  

// function to swap nodes 'currX' and 'currY' in a  
// linked list without swapping data  
static Node swapNodes( Node head_ref, Node currX,  
                        Node currY, Node prevY)  
{  
    // make 'currY' as new head  
    head_ref = currY;  

    // adjust links  
    prevY.next = currX;  

    // Swap next pointers  
    Node temp = currY.next;  
    currY.next = currX.next;  
    currX.next = temp;  
    return head_ref; 
}  

// function to sort the linked list using  
// recursive selection sort technique  
static Node recurSelectionSort( Node head)  
{  
    // if there is only a single node  
    if (head.next == null)  
        return head;  

    // 'min' - pointer to store the node having  
    // minimum data value  
    Node min = head;  

    // 'beforeMin' - pointer to store node previous  
    // to 'min' node  
    Node beforeMin = null;  
    Node ptr;  

    // traverse the list till the last node  
    for (ptr = head; ptr.next != null; ptr = ptr.next)  
    {  

        // if true, then update 'min' and 'beforeMin'  
        if (ptr.next.data < min.data)  
        {  
            min = ptr.next;  
            beforeMin = ptr;  
        }  
    }  

    // if 'min' and 'head' are not same,  
    // swap the head node with the 'min' node  
    if (min != head)  
        head = swapNodes(head, head, min, beforeMin);  

    // recursively sort the remaining list  
    head.next = recurSelectionSort(head.next);  

    return head;  
}  

// function to sort the given linked list  
static Node sort( Node head_ref)  
{  
    // if list is empty  
    if ((head_ref) == null)  
        return null;  

    // sort the list using recursive selection  
    // sort technique  
    head_ref = recurSelectionSort(head_ref);  
    return head_ref; 
}  

// function to insert a node at the  
// beginning of the linked list  
static Node push( Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list to the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// function to print the linked list  
static void printList( Node head)  
{  
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

    // create linked list 10.12.8.4.6  
    head = push(head, 6);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 12);  
    head = push(head, 10);  

    System.out.println( "Linked list before sorting:");  
    printList(head);  

    // sort the linked list  
    head = sort(head);  

    System.out.print( "\nLinked list after sorting:");  
    printList(head);  
}  
}  

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python implementation of recursive selection sort  
# for singly linked list | Swapping node links  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to swap nodes 'currX' and 'currY' in a  
# linked list without swapping data  
def swapNodes(head_ref, currX, currY, prevY) : 

    # make 'currY' as new head  
    head_ref = currY  

    # adjust links  
    prevY.next = currX  

    # Swap next pointers  
    temp = currY.next
    currY.next = currX.next
    currX.next = temp  
    return head_ref 

# function to sort the linked list using  
# recursive selection sort technique  
def recurSelectionSort( head) : 

    # if there is only a single node  
    if (head.next == None) : 
        return head  

    # 'min' - pointer to store the node having  
    # minimum data value  
    min = head  

    # 'beforeMin' - pointer to store node previous  
    # to 'min' node  
    beforeMin = None
    ptr = head 

    # traverse the list till the last node  
    while ( ptr.next != None ) : 

        # if true, then update 'min' and 'beforeMin'  
        if (ptr.next.data < min.data) : 

            min = ptr.next
            beforeMin = ptr  

        ptr = ptr.next

    # if 'min' and 'head' are not same,  
    # swap the head node with the 'min' node  
    if (min != head) : 
        head = swapNodes(head, head, min, beforeMin)  

    # recursively sort the remaining list  
    head.next = recurSelectionSort(head.next)  

    return head  

# function to sort the given linked list  
def sort( head_ref) : 

    # if list is empty  
    if ((head_ref) == None) : 
        return None

    # sort the list using recursive selection  
    # sort technique  
    head_ref = recurSelectionSort(head_ref)  
    return head_ref 

# function to insert a node at the  
# beginning of the linked list  
def push( head_ref, new_data) : 

    # allocate node  
    new_node = Node(0)  

    # put in the data  
    new_node.data = new_data  

    # link the old list to the new node  
    new_node.next = (head_ref)  

    # move the head to point to the new node  
    (head_ref) = new_node  
    return head_ref 

# function to print the linked list  
def printList( head) : 

    while (head != None) : 

        print( head.data ,end = " ")  
        head = head.next

# Driver code  
head = None

# create linked list 10.12.8.4.6  
head = push(head, 6)  
head = push(head, 4)  
head = push(head, 8)  
head = push(head, 12)  
head = push(head, 10)  

print( "Linked list before sorting:")  
printList(head)  

# sort the linked list  
head = sort(head)  

print( "\nLinked list after sorting:")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of recursive selection sort  
// for singly linked list | Swapping node links  
using System; 
public class GFG 
{ 

// A Linked list node  
public class Node 
{  
    public int data;  
    public Node next;  
};  

// function to swap nodes 'currX' and 'currY' in a  
// linked list without swapping data  
static Node swapNodes(Node head_ref, Node currX,  
                      Node currY, Node prevY)  
{  
    // make 'currY' as new head  
    head_ref = currY;  

    // adjust links  
    prevY.next = currX;  

    // Swap next pointers  
    Node temp = currY.next;  
    currY.next = currX.next;  
    currX.next = temp;  
    return head_ref; 
}  

// function to sort the linked list using  
// recursive selection sort technique  
static Node recurSelectionSort(Node head)  
{  
    // if there is only a single node  
    if (head.next == null)  
        return head;  

    // 'min' - pointer to store the node having  
    // minimum data value  
    Node min = head;  

    // 'beforeMin' - pointer to store node  
    // previous to 'min' node  
    Node beforeMin = null;  
    Node ptr;  

    // traverse the list till the last node  
    for (ptr = head; ptr.next != null;  
                     ptr = ptr.next)  
    {  

        // if true, then update 'min' and 'beforeMin'  
        if (ptr.next.data < min.data)  
        {  
            min = ptr.next;  
            beforeMin = ptr;  
        }  
    }  

    // if 'min' and 'head' are not same,  
    // swap the head node with the 'min' node  
    if (min != head)  
        head = swapNodes(head, head, min, beforeMin);  

    // recursively sort the remaining list  
    head.next = recurSelectionSort(head.next);  

    return head;  
}  

// function to sort the given linked list  
static Node sort( Node head_ref)  
{  
    // if list is empty  
    if ((head_ref) == null)  
        return null;  

    // sort the list using recursive selection  
    // sort technique  
    head_ref = recurSelectionSort(head_ref);  
    return head_ref; 
}  

// function to insert a node at the  
// beginning of the linked list  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list to the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// function to print the linked list  
static void printList( Node head)  
{  
    while (head != null)  
    {  
        Console.Write(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = null;  

    // create linked list 10->12->8->4->6 
    head = push(head, 6);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 12);  
    head = push(head, 10);  

    Console.WriteLine("Linked list before sorting:");  
    printList(head);  

    // sort the linked list  
    head = sort(head);  

    Console.Write("\nLinked list after sorting:");  
    printList(head);  
}  
}  

// This code is contributed by Princi Singh 

```

**Output:**

```
Linked list before sorting:
10 12 8 4 6
Linked list after sorting:
4 6 8 10 12

```

**时间复杂度：** O（n <sup>2</sup> ）

本文由 **Ayush Jauhari** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

