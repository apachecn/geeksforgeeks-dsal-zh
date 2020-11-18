# 在第k个位置将整个链表插入另一个

给定两个链表和一个数字k。 将第二个链接列表插入第k个第一个链接列表

**示例：**

```
Input : a : 1->2->3->4->5->NULL
        b : 7->8->9->10->11->NULL
        k = 2
Output :1->2->7->8->9->10->11->3->4->5->NULL

Input : a: 10->15->20->NULL
        b: 11->17->16->18->NULL
        k = 3
Output : 10->15->20->11->17->16->18->NULL

```

**问题的图形表示**
![](img/578b7819115c78a8f7af52d597f6a97f.png)

1）遍历第一个链表直到第k个点
2）将第二个链表头节点连接到第一个链表的第k个点
3）遍历第二个链表直到
结束4） 将第一个链表的第（k + 1）点添加到第二个链表的末尾

## C++

```cpp

// A C++ program to insert a linked list in 
// to another linked list at position k 
#include <bits/stdc++.h> 
using namespace std; 

/* Structure for a linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert whole linked list in 
// to another linked list at position k 
void insert(struct Node* head1, struct Node* head2, 
            int k) 
{ 
    // traverse the first linked list until k-th 
    // point is reached 
    int count = 1; 
    struct Node* curr = head1; 
    while (count < k) { 
        curr = curr->next; 
        count++; 
    } 

    // backup next node of the k-th point 
    struct Node* temp = curr->next; 

    // join second linked list at the kth point 
    curr->next = head2; 

    // traverse the second linked list till end 
    while (head2->next != NULL) 
        head2 = head2->next; 

    // join the second part of the linked list 
    // to the end 
    head2->next = temp; 
} 

// Function to print linked list recursively 
void printList(Node* head) 
{ 
    if (head == NULL) 
        return; 

    // If head is not NULL, print current node 
    // and recur for remaining list 
    cout << head->data << " "; 
    printList(head->next); 
} 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, insert a new node on the front 
  of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Driven program to test above function */
int main() 
{ 
    /* The constructed linked lists are : 
     a: 1->2->3->4->5; 
     b: 7->8->9->10->11 */
    struct Node* a = NULL; 
    struct Node* b = NULL; 
    int k = 2; 

    // first linked list 
    push(&a, 5); 
    push(&a, 4); 
    push(&a, 3); 
    push(&a, 2); 
    push(&a, 1); 

    // second linked list 
    push(&b, 11); 
    push(&b, 10); 
    push(&b, 9); 
    push(&b, 8); 
    push(&b, 7); 

    printList(a); 
    cout << "\n"; 

    printList(b); 

    insert(a, b, k); 

    cout << "\nResulting linked list\t"; 
    printList(a); 

    return 0; 
} 

```

## Java

```java

// A Java program to insert a linked list in 
// to another linked list at position k 
class GFG { 

    // Structure for a linked list node / 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to insert whole linked list in 
    // to another linked list at position k 
    static Node insert(Node head1, Node head2, 
                       int k) 
    { 
        // traverse the first linked list until k-th 
        // point is reached 
        int count = 1; 
        Node curr = head1; 
        while (count < k) { 
            curr = curr.next; 
            count++; 
        } 

        // backup next node of the k-th point 
        Node temp = curr.next; 

        // join second linked list at the kth point 
        curr.next = head2; 

        // traverse the second linked list till end 
        while (head2.next != null) 
            head2 = head2.next; 

        // join the second part of the linked list 
        // to the end 
        head2.next = temp; 
        return head1; 
    } 

    // Function to print linked list recursively 
    static void printList(Node head) 
    { 
        if (head == null) 
            return; 

        // If head is not null, print current node 
        // and recur for remaining list 
        System.out.print(head.data + " "); 
        printList(head.next); 
    } 

    // Given a reference (pointer to pointer) to the head 
    // of a list and an int, insert a new node on the front 
    // of the list. 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driven code 
    public static void main(String args[]) 
    { 
        // The constructed linked lists are : 
        // a: 1.2.3.4.5; 
        // b: 7.8.9.10.11 
        Node a = null; 
        Node b = null; 
        int k = 2; 

        // first linked list 
        a = push(a, 5); 
        a = push(a, 4); 
        a = push(a, 3); 
        a = push(a, 2); 
        a = push(a, 1); 

        // second linked list 
        b = push(b, 11); 
        b = push(b, 10); 
        b = push(b, 9); 
        b = push(b, 8); 
        b = push(b, 7); 

        printList(a); 
        System.out.println(); 

        printList(b); 

        a = insert(a, b, k); 

        System.out.print("\nResulting linked list\t"); 
        printList(a); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# A Python3 program to insert a linked list in 
# to another linked list at position k 

# Node of the single linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert whole linked list in 
# to another linked list at position k 
def insert(head1, head2, k): 

    # traverse the first linked list until k-th 
    # point is reached 
    count = 1
    curr = head1 
    while (count < k):  
        curr = curr.next
        count += 1

    # backup next node of the k-th point 
    temp = curr.next

    # join second linked list at the kth point 
    curr.next = head2 

    # traverse the second linked list till end 
    while (head2.next != None): 
        head2 = head2.next

    # join the second part of the linked list 
    # to the end 
    head2.next = temp 
    return head1 

# Function to print linked list recursively 
def printList(head): 

    if (head == None): 
        return

    # If head is not None, print current node 
    # and recur for remaining list 
    print( head.data, end = " ") 
    printList(head.next) 

""" Given a reference (pointer to pointer) to the head 
of a list and an int, insert a new node on the front 
of the list. """
def push(head_ref, new_data): 

    new_node = Node(0) 
    new_node.data = new_data 
    new_node.next = (head_ref) 
    (head_ref) = new_node 
    return head_ref 

# Driver Code 
if __name__ == "__main__":  

    """ The constructed linked lists are : 
    a: 1.2.3.4.5 
    b: 7.8.9.10.11 """
    a = None
    b = None
    k = 2

    # first linked list 
    a = push(a, 5) 
    a = push(a, 4) 
    a = push(a, 3) 
    a = push(a, 2) 
    a = push(a, 1) 

    # second linked list 
    b = push(b, 11) 
    b = push(b, 10) 
    b = push(b, 9) 
    b = push(b, 8) 
    b = push(b, 7) 

    printList(a) 
    print() 

    printList(b) 

    a = insert(a, b, k) 

    print("\nResulting linked list\t", end = " "); 
    printList(a) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// A C# program to insert a linked list in 
// to another linked list at position k 
using System; 

class GFG { 

    // Structure for a linked list node / 
    public class Node { 
        public int data; 
        public Node next; 
    }; 

    // Function to insert whole linked list in 
    // to another linked list at position k 
    static Node insert(Node head1, Node head2, 
                       int k) 
    { 
        // traverse the first linked list until k-th 
        // point is reached 
        int count = 1; 
        Node curr = head1; 
        while (count < k) { 
            curr = curr.next; 
            count++; 
        } 

        // backup next node of the k-th point 
        Node temp = curr.next; 

        // join second linked list at the kth point 
        curr.next = head2; 

        // traverse the second linked list till end 
        while (head2.next != null) 
            head2 = head2.next; 

        // join the second part of the linked list 
        // to the end 
        head2.next = temp; 
        return head1; 
    } 

    // Function to print linked list recursively 
    static void printList(Node head) 
    { 
        if (head == null) 
            return; 

        // If head is not null, print current node 
        // and recur for remaining list 
        Console.Write(head.data + " "); 
        printList(head.next); 
    } 

    // Given a reference (pointer to pointer) to the head 
    // of a list and an int, insert a new node on the front 
    // of the list. 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driven code 
    public static void Main(String[] args) 
    { 
        // The constructed linked lists are : 
        // a: 1.2.3.4.5; 
        // b: 7.8.9.10.11 
        Node a = null; 
        Node b = null; 
        int k = 2; 

        // first linked list 
        a = push(a, 5); 
        a = push(a, 4); 
        a = push(a, 3); 
        a = push(a, 2); 
        a = push(a, 1); 

        // second linked list 
        b = push(b, 11); 
        b = push(b, 10); 
        b = push(b, 9); 
        b = push(b, 8); 
        b = push(b, 7); 

        printList(a); 
        Console.WriteLine(); 

        printList(b); 

        a = insert(a, b, k); 

        Console.Write("\nResulting linked list\t"); 
        printList(a); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
1 2 3 4 5 
7 8 9 10 11 
Resulting linked list    1 2 7 8 9 10 11 3 4 5 

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。