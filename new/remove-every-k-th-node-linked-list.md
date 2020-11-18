# 删除链接列表

> 原文：[https://www.geeksforgeeks.org/remove-every-k-th-node-linked-list/](https://www.geeksforgeeks.org/remove-every-k-th-node-linked-list/)

的每个第 k 个节点

给定一个单链表，您的任务是删除链表的第 K 个节点。 假定 K 始终小于或等于链接列表的长度。

**示例**：

```
Input : 1->2->3->4->5->6->7->8  
        k = 3
Output : 1->2->4->5->7->8
As 3 is the k-th node after its deletion list 
would be 1->2->4->5->6->7->8
And now 4 is the starting node then from it, 6 
would be the k-th node. So no other kth node 
could be there.So, final list is:
1->2->4->5->7->8.

Input: 1->2->3->4->5->6  
       k = 1
Output: Empty list 
All nodes need to be deleted

```

这个想法是从头开始遍历列表，并跟踪上次删除后访问的节点。 每当计数变为 k 时，删除当前节点并将计数重置为 0。

```
(1) Traverse list and do following
   (a) Count node before deletion.
   (b) If (count == k) that means current 
        node is to be deleted.
      (i)  Delete current node i.e. do

          //  assign address of next node of 
          // current node to the previous node
          // of the current node.
          prev->next = ptr->next i.e.

       (ii) Reset count as 0, i.e., do count = 0.
   (c) Update prev node if count != 0 and if
       count is 0 that means that node is a
       starting point.
   (d) Update ptr and continue until all 
       k-th node gets deleted.

```

下面是实现。

## C++

```cpp

// C++ program to delete every k-th Node of 
// a singly linked list. 
#include<bits/stdc++.h> 
using namespace std; 

/* Linked list Node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// To remove complete list (Needed for 
// case when k is 1) 
void freeList(Node *node) 
{ 
    while (node != NULL) 
    { 
        Node *next = node->next; 
        delete (node); 
        node  = next; 
    } 
} 

// Deletes every k-th node and returns head 
// of modified list. 
Node *deleteKthNode(struct Node *head, int k) 
{ 
    // If linked list is empty 
    if (head == NULL) 
        return NULL; 

    if (k == 1) 
    { 
       freeList(head); 
       return NULL; 
    } 

    // Initialize ptr and prev before starting 
    // traversal. 
    struct Node *ptr = head, *prev = NULL; 

    // Traverse list and delete every k-th node 
    int count = 0; 
    while (ptr != NULL) 
    { 
        // increment Node count 
        count++; 

        // check if count is equal to k 
        // if yes, then delete current Node 
        if (k == count) 
        { 
            // put the next of current Node in 
            // the next of previous Node 
            delete(prev->next); 
            prev->next = ptr->next; 

            // set count = 0 to reach further 
            // k-th Node 
            count = 0; 
        } 

        // update prev if count is not 0 
        if (count != 0) 
            prev = ptr; 

        ptr = prev->next; 
    } 

    return head; 
} 

/* Function to print linked list */
void displayList(struct Node *head) 
{ 
    struct Node *temp = head; 
    while (temp != NULL) 
    { 
        cout<<temp->data<<" "; 
        temp = temp->next; 
    } 
} 

// Utility function to create a new node. 
struct Node *newNode(int x) 
{ 
    Node *temp = new Node; 
    temp->data = x; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 
    head->next->next->next->next->next = newNode(6); 
    head->next->next->next->next->next->next = 
                                        newNode(7); 
    head->next->next->next->next->next->next->next = 
                                        newNode(8); 

    int k = 3; 
    head = deleteKthNode(head, k); 

    displayList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to delete every k-th Node  
// of a singly linked list. 
class GFG 
{ 

/* Linked list Node */
static class Node 
{ 
    int data; 
    Node next; 
} 

// To remove complete list (Needed for 
// case when k is 1) 
static Node freeList(Node node) 
{ 
    while (node != null) 
    { 
        Node next = node.next; 
        node = next; 
    } 
    return node; 
} 

// Deletes every k-th node and  
// returns head of modified list. 
static Node deleteKthNode(Node head, int k) 
{ 
    // If linked list is empty 
    if (head == null) 
        return null; 

    if (k == 1) 
    { 
        head = freeList(head); 
        return null; 
    } 

    // Initialize ptr and prev before  
    // starting traversal. 
    Node ptr = head, prev = null; 

    // Traverse list and delete  
    // every k-th node 
    int count = 0; 
    while (ptr != null) 
    { 
        // increment Node count 
        count++; 

        // check if count is equal to k 
        // if yes, then delete current Node 
        if (k == count) 
        { 
            // put the next of current Node in 
            // the next of previous Node 
            prev.next = ptr.next; 

            // set count = 0 to reach further 
            // k-th Node 
            count = 0; 
        } 

        // update prev if count is not 0 
        if (count != 0) 
            prev = ptr; 

        ptr = prev.next; 
    } 
    return head; 
} 

/* Function to print linked list */
static void displayList(Node head) 
{ 
    Node temp = head; 
    while (temp != null) 
    { 
        System.out.print(temp.data + " "); 
        temp = temp.next; 
    } 
} 

// Utility function to create a new node. 
static Node newNode(int x) 
{ 
    Node temp = new Node(); 
    temp.data = x; 
    temp.next = null; 
    return temp; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    /* Start with the empty list */
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = newNode(4); 
    head.next.next.next.next = newNode(5); 
    head.next.next.next.next.next = newNode(6); 
    head.next.next.next.next.next.next = 
                                        newNode(7); 
    head.next.next.next.next.next.next.next = 
                                        newNode(8); 

    int k = 3; 
    head = deleteKthNode(head, k); 

    displayList(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to delete every k-th Node  
# of a singly linked list. 
import math 

# Linked list Node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# To remove complete list (Needed for 
# case when k is 1) 
def freeList(node): 
    while (node != None): 
        next = node.next
        node = next
    return node 

# Deletes every k-th node and  
# returns head of modified list. 
def deleteKthNode(head, k): 

    # If linked list is empty 
    if (head == None): 
        return None

    if (k == 1): 
        freeList(head) 
        return None

    # Initialize ptr and prev before  
    # starting traversal. 
    ptr = head 
    prev = None

    # Traverse list and delete every k-th node 
    count = 0
    while (ptr != None): 

        # increment Node count 
        count = count + 1

        # check if count is equal to k 
        # if yes, then delete current Node 
        if (k == count): 

            # put the next of current Node in 
            # the next of previous Node 
            # delete(prev.next) 
            prev.next = ptr.next

            # set count = 0 to reach further 
            # k-th Node 
            count = 0

        # update prev if count is not 0 
        if (count != 0): 
            prev = ptr 

        ptr = prev.next

    return head 

# Function to print linked list  
def displayList(head): 
    temp = head 
    while (temp != None): 
        print(temp.data, end = ' ') 
        temp = temp.next

# Utility function to create a new node. 
def newNode( x): 
    temp = Node(x) 
    temp.data = x 
    temp.next = None
    return temp 

# Driver Code 
if __name__=='__main__':  

    # Start with the empty list  
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(3) 
    head.next.next.next = newNode(4) 
    head.next.next.next.next = newNode(5) 
    head.next.next.next.next.next = newNode(6) 
    head.next.next.next.next.next.next = newNode(7) 
    head.next.next.next.next.next.next.next = newNode(8) 

    k = 3
    head = deleteKthNode(head, k) 

    displayList(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to delete every k-th Node  
// of a singly linked list. 
using System; 

class GFG 
{ 

/* Linked list Node */
public class Node 
{ 
    public int data; 
    public Node next; 
} 

// To remove complete list (Needed for 
// case when k is 1) 
static Node freeList(Node node) 
{ 
    while (node != null) 
    { 
        Node next = node.next; 
        node = next; 
    } 
    return node; 
} 

// Deletes every k-th node and  
// returns head of modified list. 
static Node deleteKthNode(Node head, int k) 
{ 
    // If linked list is empty 
    if (head == null) 
        return null; 

    if (k == 1) 
    { 
        head = freeList(head); 
        return null; 
    } 

    // Initialize ptr and prev before  
    // starting traversal. 
    Node ptr = head, prev = null; 

    // Traverse list and delete  
    // every k-th node 
    int count = 0; 
    while (ptr != null) 
    { 
        // increment Node count 
        count++; 

        // check if count is equal to k 
        // if yes, then delete current Node 
        if (k == count) 
        { 
            // put the next of current Node in 
            // the next of previous Node 
            prev.next = ptr.next; 

            // set count = 0 to reach further 
            // k-th Node 
            count = 0; 
        } 

        // update prev if count is not 0 
        if (count != 0) 
            prev = ptr; 

        ptr = prev.next; 
    } 
    return head; 
} 

/* Function to print linked list */
static void displayList(Node head) 
{ 
    Node temp = head; 
    while (temp != null) 
    { 
        Console.Write(temp.data + " "); 
        temp = temp.next; 
    } 
} 

// Utility function to create a new node. 
static Node newNode(int x) 
{ 
    Node temp = new Node(); 
    temp.data = x; 
    temp.next = null; 
    return temp; 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    /* Start with the empty list */
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = newNode(4); 
    head.next.next.next.next = newNode(5); 
    head.next.next.next.next.next = newNode(6); 
    head.next.next.next.next.next.next = newNode(7); 
    head.next.next.next.next.next.next.next = newNode(8); 

    int k = 3; 
    head = deleteKthNode(head, k); 

    displayList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
1 2 4 5 7 8

```

时间复杂度：`O(n)`

本文由 [**Sahil Chhabra**](https://www.facebook.com/sahil.chhabra.965) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

