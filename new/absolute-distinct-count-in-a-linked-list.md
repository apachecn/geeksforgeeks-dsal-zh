# 链表中的唯一绝对值计数

> 原文：[https://www.geeksforgeeks.org/absolute-distinct-count-in-a-linked-list/](https://www.geeksforgeeks.org/absolute-distinct-count-in-a-linked-list/)

给定由整数组成的[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)，任务是打印链表中存在的不同绝对值的数量。

**示例**：

> **输入**：`-1 -> -2 -> 0 -> 4 -> 5 -> 8`
> 
> **输出**：6
> 
> **解释**：
> 
> 不同的绝对节点值为`{0, 1, 2, 4, 4, 5, 8}`
> 
> **输入**：`- 1-> -1 -> -1 -> 0 -> 1`
> 
> **输出**：2
> 
> **说明**：
> 
> 不同的绝对节点值为`{0, 1}`。

**方法**：为了解决此问题，我们需要[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)或[`HashSet`](https://www.geeksforgeeks.org/hashset-in-java/)来存储链表中存在的不同绝对值。 [遍历整个链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)并在**集合**中插入每个节点的绝对值后，**集合**大小给出了[链表中存在的不同的绝对值](https://www.geeksforgeeks.org/setsize-c-stl/)。

下面是该方法的实现：

## C++

```cpp

// C++ Program to print the count 
// of distinct absolute values 
// in a linked list 

#include <bits/stdc++.h> 
using namespace std; 
// Node of a singly 
// linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a 
// node at the beginning 
// of a singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // Allocate node 
    Node* new_node = (Node*)malloc( 
        sizeof(struct Node)); 

    // Insert the data 
    new_node->data = new_data; 

    // Point to the current head 
    new_node->next = (*head_ref); 

    // Make the current Node 
    // the new head 
    (*head_ref) = new_node; 
} 

// Function to return number of 
// distinct absolute values 
// present in the linked list 
int distinctCount(Node* head_1) 
{ 
    Node* ptr = head_1; 
    unordered_set<int> s; 

    while (ptr != NULL) { 
        s.insert(abs(ptr->data)); 
        ptr = ptr->next; 
    } 

    return s.size(); 
} 
int main() 
{ 
    // Create the head 
    Node* head1 = NULL; 
    // Insert Nodes 
    push(&head1, -1); 
    push(&head1, -2); 
    push(&head1, 0); 
    push(&head1, 4); 
    push(&head1, 5); 
    push(&head1, 8); 

    int k = distinctCount(head1); 
    cout << k; 
    return 0; 
} 

```

## Java

```java

// Java program to calculate 
// the count of distinct 
// absolute values in a 
// linked list 

import java.util.*; 

class GFG { 

    // Node of the singly 
    // linked list 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to insert a node 
    // at the beginning of the 
    // singly Linked List 
    static Node push(Node head_ref, 
                     int new_data) 
    { 
        // Allocate node 
        Node new_node = new Node(); 

        // Insert the data 
        new_node.data = new_data; 

        // Point the current Node 
        // to the current head 
        new_node.next = (head_ref); 

        // Make the current node 
        // as the new head 
        (head_ref) = new_node; 

        return head_ref; 
    } 

    // Function to return the count of 
    // distinct absolute values 
    // present in the Linked list 
    static int distinctCount(Node head_ref1) 
    { 
        Set<Integer> s = new HashSet<Integer>(); 
        Node ptr1 = head_ref1; 

        while (ptr1 != null) { 
            s.add(Math.abs(ptr1.data)); 
            ptr1 = ptr1.next; 
        } 
        return s.size(); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        // Create the head 
        Node head1 = null; 
        // Insert nodes to the 
        // Linked List 
        head1 = push(head1, -1); 
        head1 = push(head1, -2); 
        head1 = push(head1, 0); 
        head1 = push(head1, 4); 
        head1 = push(head1, 5); 
        head1 = push(head1, 8); 

        int ans = distinctCount(head1); 
        System.out.println(ans); 
    } 
} 

```

## Python3

```py

# Python3 program to calculate 
# the count of distinct  
# absolute values in a  
# linked list 

class Node:   

    def __init__(self, data):   
        self.data = data   
        self.next = next

# Function to insert a  
# node at the beginning   
# of the singly Linked List   
def push( head_ref, new_data) :  

    # Alocate node   
    new_node = Node(0)   

    # Insert data   
    new_node.data = new_data   

    # Pont to the head  
    new_node.next = (head_ref)   

    # Make the new Node 
    # the new head 
    (head_ref) = new_node  

    return head_ref 

# Function to return the  
# count of distinct absolute 
# values in the linked list 
def distinctCount(head_ref1):  
    s = set()  
    ptr1 = head_ref1 
    # set keeps all unique elements  
    while (ptr1 != None):  
        s.add(abs(ptr1.data))  
        ptr1 = ptr1.next
    return len(s)     

# Driver code   
# Create the Head 
head1 = None
# Insert nodes   
head1 = push(head1, -1)   
head1 = push(head1, -2)   
head1 = push(head1, 0)   
head1 = push(head1, 4)   
head1 = push(head1, 5) 
head1 = push(head1, 8) 

ans = distinctCount(head1) 
print(ans) 

```

## C#

```cs

// C# program to calculate the count 
// of distinct absolute values in a 
// linked list 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Node of the singly 
// linked list 
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert a node 
// at the beginning of the 
// singly Linked List 
static Node push(Node head_ref, 
                 int new_data) 
{ 

    // Allocate node 
    Node new_node = new Node(); 

    // Insert the data 
    new_node.data = new_data; 

    // Point the current Node 
    // to the current head 
    new_node.next = (head_ref); 

    // Make the current node 
    // as the new head 
    (head_ref) = new_node; 

    return head_ref; 
} 

// Function to return the count of 
// distinct absolute values 
// present in the Linked list 
static int distinctCount(Node head_ref1) 
{ 
    HashSet<int> s = new HashSet<int>(); 
    Node ptr1 = head_ref1; 

    while (ptr1 != null) 
    { 
        s.Add(Math.Abs(ptr1.data)); 
        ptr1 = ptr1.next; 
    } 
    return s.Count; 
} 

// Driver Code 
public static void Main(String []args) 
{ 

    // Create the head 
    Node head1 = null; 

    // Insert nodes to the 
    // Linked List 
    head1 = push(head1, -1); 
    head1 = push(head1, -2); 
    head1 = push(head1, 0); 
    head1 = push(head1, 4); 
    head1 = push(head1, 5); 
    head1 = push(head1, 8); 

    int ans = distinctCount(head1); 
    Console.WriteLine(ans); 
} 
} 

// This code is contributed by Princi Singh

```

**输出**： 

```
6

```

**时间复杂度**：`O(N)`

**辅助空间**：`O(N)`



* * *

* * *



