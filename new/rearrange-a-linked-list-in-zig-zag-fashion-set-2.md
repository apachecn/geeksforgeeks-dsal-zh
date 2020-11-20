# 以 Zig-Zag 格式重新排列链表| 第 2 组

> 原文：[https://www.geeksforgeeks.org/rearrange-a-linked-list-in-zig-zag-fashion-set-2/](https://www.geeksforgeeks.org/rearrange-a-linked-list-in-zig-zag-fashion-set-2/)

给定一个链表，重新排列它，使转换后的链表的形式应为< b > c < d > e

**示例**：

```
Input:  1->2->3->4
Output: 1->3->2->4 

Input:  11->15->20->5->10
Output: 11->20->5->15->10

```

**方法**：

在先前的[文章](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)中讨论了将给定列表转换为锯齿形的解决方案。 讨论的解决方案通过交换节点数据来执行转换。 当数据包含许多字段时，在许多情况下交换节点的数据可能会很昂贵。 在这篇文章中，讨论了通过交换链接执行转换的解决方案。

想法是遍历给定的链表，并检查当前节点是否保持锯齿形顺序。 为了检查给定节点是否保持锯齿形顺序，使用了变量 *ind* 。 如果 **ind = 0** ，则当前节点的数据应小于其相邻节点的数据；如果 **ind = 1，则**则当前节点的数据应大于其相邻节点的数据。 如果当前节点违反了锯齿形顺序，则交换两个节点的位置。 为此，请维护两个指针 **prev 和 next** 。 *上一个*存储当前节点的上一个节点，*下一个*存储当前节点的新下一个节点。 要交换两个节点，请执行以下步骤：

*   将当前节点的下一个节点设为上一个节点的下一个节点。

*   使当前节点成为其相邻节点的下一个节点。

*   将当前节点设为下一个=下一个节点。

下面是上述方法的实现：

## C++

```cpp

// CPP program to arrange linked list in 
// zigzag fashion 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// This function converts the Linked list in 
// zigzag fashion 
Node* zigZagList(Node* head) 
{ 
    if (head == NULL || head->next == NULL) { 
        return head; 
    } 

    // to store new head 
    Node* res = NULL; 

    // to traverse linked list 
    Node* curr = head; 

    // to store previous node of current node 
    Node* prev = NULL; 

    // to store new next node of current node 
    Node* next; 

    // to check if current element should 
    // be less than or greater than. 
    // ind = 0 --> less than 
    // ind = 1 --> greater than 
    int ind = 0; 

    while (curr->next) { 

        // If elements are not in zigzag fashion 
        // swap them. 
        if ((ind == 0 && curr->data > curr->next->data) 
            || (ind == 1 && curr->data < curr->next->data)) { 

            if (res == NULL) 
                res = curr->next; 

            // Store new next element of current 
            // node 
            next = curr->next->next; 

            // Previous node of current node will 
            // now point to next node of current node 
            if (prev) 
                prev->next = curr->next; 

            // Change next pointers of both 
            // adjacent nodes 
            curr->next->next = curr; 
            curr->next = next; 

            // Change previous pointer. 
            if (prev) 
                prev = prev->next; 
            else
                prev = res; 
        } 

        // If already in zig zag form, then move 
        // to next element. 
        else { 
            if (res == NULL) { 
                res = curr; 
            } 

            prev = curr; 
            curr = curr->next; 
        } 

        // Update info whether next element should 
        // be less than or greater than. 
        ind = 1 - ind; 
    } 

    return res; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a Node */
void push(Node** head_ref, int new_data) 
{ 
    /* allocate Node */
    struct Node* new_Node = new Node; 

    /* put in the data */
    new_Node->data = new_data; 

    /* link the old list off the new Node */
    new_Node->next = (*head_ref); 

    /* move the head to point to the new Node */
    (*head_ref) = new_Node; 
} 

/* Function to print linked list */
void printList(struct Node* Node) 
{ 
    while (Node != NULL) { 
        printf("%d->", Node->data); 
        Node = Node->next; 
    } 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
    // answer should be -> 3 7 4 8 2 6 1 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 3); 
    push(&head, 4); 

    printf("Given linked list \n"); 
    printList(head); 

    head = zigZagList(head); 

    printf("\nZig Zag Linked list \n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to arrange linked list in 
// zigzag fashion 
class GFG 
{  

/* Link list Node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

static Node head; 

// This function converts the Linked list in 
// zigzag fashion 
static Node zigZagList(Node head) 
{ 
    if (head == null || head.next == null) 
    { 
        return head; 
    } 

    // to store new head 
    Node res = null; 

    // to traverse linked list 
    Node curr = head; 

    // to store previous node of current node 
    Node prev = null; 

    // to store new next node of current node 
    Node next; 

    // to check if current element should 
    // be less than or greater than. 
    // ind = 0 -. less than 
    // ind = 1 -. greater than 
    int ind = 0; 

    while (curr.next != null)  
    { 

        // If elements are not in zigzag fashion 
        // swap them. 
        if ((ind == 0 && curr.data > curr.next.data) ||  
            (ind == 1 && curr.data < curr.next.data))  
        { 
            if (res == null) 
                res = curr.next; 

            // Store new next element of current 
            // node 
            next = curr.next.next; 

            // Previous node of current node will 
            // now point to next node of current node 
            if (prev != null) 
                prev.next = curr.next; 

            // Change next pointers of both 
            // adjacent nodes 
            curr.next.next = curr; 
            curr.next = next; 

            // Change previous pointer. 
            if (prev != null) 
                prev = prev.next; 
            else
                prev = res; 
        } 

        // If already in zig zag form, then move 
        // to next element. 
        else 
        { 
            if (res == null)  
            { 
                res = curr; 
            } 

            prev = curr; 
            curr = curr.next; 
        } 

        // Update info whether next element should 
        // be less than or greater than. 
        ind = 1 - ind; 
    } 
    return res; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a Node */
static void push(Node head_ref, int new_data) 
{ 
    /* allocate Node */
    Node new_Node = new Node(); 

    /* put in the data */
    new_Node.data = new_data; 

    /* link the old list off the new Node */
    new_Node.next = head_ref; 

    /* move the head to point to the new Node */
    head_ref = new_Node; 
    head = head_ref; 
} 

/* Function to print linked list */
static void printList(Node Node) 
{ 
    while (Node != null) 
    { 
        System.out.printf("%d->", Node.data); 
        Node = Node.next; 
    } 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    /* Start with the empty list */
    head = null; 

    // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
    // answer should be -> 3 7 4 8 2 6 1 
    push(head, 1); 
    push(head, 2); 
    push(head, 6); 
    push(head, 8); 
    push(head, 7); 
    push(head, 3); 
    push(head, 4); 

    System.out.printf("Given linked list \n"); 
    printList(head); 

    head = zigZagList(head); 

    System.out.printf("\nZig Zag Linked list \n"); 
    printList(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to arrange  
# linked list in zigzag fashion  

class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# This function converts the  
# Linked list in zigzag fashion  
def zigZagList(head):  

    if head == None or head.next == None:   
        return head  

    # To store new head  
    res = None 

    # To traverse linked list  
    curr = head  

    # To store previous node of current node  
    prev = None 

    # to check if current element should  
    # be less than or greater than.  
    # ind = 0 -. less than  
    # ind = 1 -. greater than  
    ind = 0 

    while curr.next:   

        # If elements are not in  
        # zigzag fashion swap them.  
        if ((ind == 0 and curr.data > curr.next.data)  
            or (ind == 1 and curr.data < curr.next.data)):   

            if res == None: 
                res = curr.next 

            # Store new next element of current  
            # node  
            next = curr.next.next 

            # Previous node of current node will  
            # now point to next node of current node  
            if prev:  
                prev.next = curr.next 

            # Change next pointers of  
            # both adjacent nodes  
            curr.next.next = curr  
            curr.next = next 

            # Change previous pointer.  
            if prev:  
                prev = prev.next 
            else: 
                prev = res  

        # If already in zig zag form,  
        # then move to next element.  
        else:  
            if res == None:   
                res = curr  

            prev = curr  
            curr = curr.next 

        # Update info whether next element  
        # should be less than or greater than.  
        ind = 1 - ind  

    return res  

# UTILITY FUNCTIONS 
# Function to push a Node  
def push(head_ref, new_data): 

    # put in the data 
    new_Node = Node(new_data)  

    # link the old list off the new Node 
    new_Node.next = head_ref  

    # move the head to point to the new Node 
    head_ref = new_Node 
    return head_ref 

# Function to print linked list 
def printList(Node):  

    while Node != None:  
        print(Node.data, end = "->")  
        Node = Node.next

# Driver program to test above function 
if __name__ == "__main__":  

    # Start with the empty list  
    head = None 

    # create a list 4 . 3 . 7 . 8 . 6 . 2 . 1  
    # answer should be . 3 7 4 8 2 6 1  
    head = push(head, 1)  
    head = push(head, 2)  
    head = push(head, 6)  
    head = push(head, 8)  
    head = push(head, 7)  
    head = push(head, 3)  
    head = push(head, 4)  

    print("Given linked list")  
    printList(head)  

    head = zigZagList(head)  

    print("\nZig Zag Linked list")  
    printList(head) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to arrange linked list in 
// zigzag fashion 
using System; 

class GFG 
{  

/* Link list Node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

static Node head; 

// This function converts the Linked list in 
// zigzag fashion 
static Node zigZagList(Node head) 
{ 
    if (head == null || head.next == null) 
    { 
        return head; 
    } 

    // to store new head 
    Node res = null; 

    // to traverse linked list 
    Node curr = head; 

    // to store previous node of current node 
    Node prev = null; 

    // to store new next node of current node 
    Node next; 

    // to check if current element should 
    // be less than or greater than. 
    // ind = 0 -. less than 
    // ind = 1 -. greater than 
    int ind = 0; 

    while (curr.next != null)  
    { 

        // If elements are not in zigzag fashion 
        // swap them. 
        if ((ind == 0 && curr.data > curr.next.data) ||  
            (ind == 1 && curr.data < curr.next.data))  
        { 
            if (res == null) 
                res = curr.next; 

            // Store new next element of current 
            // node 
            next = curr.next.next; 

            // Previous node of current node will 
            // now point to next node of current node 
            if (prev != null) 
                prev.next = curr.next; 

            // Change next pointers of both 
            // adjacent nodes 
            curr.next.next = curr; 
            curr.next = next; 

            // Change previous pointer. 
            if (prev != null) 
                prev = prev.next; 
            else
                prev = res; 
        } 

        // If already in zig zag form, then move 
        // to next element. 
        else
        { 
            if (res == null)  
            { 
                res = curr; 
            } 

            prev = curr; 
            curr = curr.next; 
        } 

        // Update info whether next element should 
        // be less than or greater than. 
        ind = 1 - ind; 
    } 
    return res; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a Node */
static void push(Node head_ref, int new_data) 
{ 
    /* allocate Node */
    Node new_Node = new Node(); 

    /* put in the data */
    new_Node.data = new_data; 

    /* link the old list off the new Node */
    new_Node.next = head_ref; 

    /* move the head to point to the new Node */
    head_ref = new_Node; 
    head = head_ref; 
} 

/* Function to print linked list */
static void printList(Node Node) 
{ 
    while (Node != null) 
    { 
        Console.Write("{0}->", Node.data); 
        Node = Node.next; 
    } 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    /* Start with the empty list */
    head = null; 

    // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
    // answer should be -> 3 7 4 8 2 6 1 
    push(head, 1); 
    push(head, 2); 
    push(head, 6); 
    push(head, 8); 
    push(head, 7); 
    push(head, 3); 
    push(head, 4); 

    Console.Write("Given linked list \n"); 
    printList(head); 

    head = zigZagList(head); 

    Console.Write("\nZig Zag Linked list \n"); 
    printList(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Given linked list 
4->3->7->8->6->2->1->
Zig Zag Linked list 
3->7->4->8->2->6->1->

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。