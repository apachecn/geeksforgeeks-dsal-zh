# 合并两个排序的链接列表，以使合并列表的顺序相反

> 原文：[https://www.geeksforgeeks.org/merge-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/)

给定两个链表，以递增顺序排序。 合并它们，使结果列表按降序排列（反向排列）。

例子：

```
Input:  a: 5->10->15->40
        b: 2->3->20 
Output: res: 40->20->15->10->5->3->2

Input:  a: NULL
        b: 2->3->20 
Output: res: 20->3->2

```

**简单解决方案**要执行以下操作。

1）[反向列出第一个“ a”](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/) 。

2）[倒数第二个列表'b'](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。

3）[合并两个反向列表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)。

另一个简单的解决方案是首先合并两个列表，然后反转合并的列表。

以上两种解决方案都需要两次遍历链表。

**如何求解无反向`O(1)`辅助空间（就地）并且仅遍历两个列表？**

这个想法是遵循合并样式的过程。 将结果列表初始化为空。 从头到尾遍历两个列表。 比较两个列表的当前节点，并在结果列表的开头插入两个中较小的一个。

```
1) Initialize result list as empty: res = NULL.
2) Let 'a' and 'b' be heads first and second lists respectively.
3) While (a != NULL and b != NULL)
    a) Find the smaller of two (Current 'a' and 'b')
    b) Insert the smaller value node at the front of result.
    c) Move ahead in the list of smaller node. 
4) If 'b' becomes NULL before 'a', insert all nodes of 'a' 
   into result list at the beginning.
5) If 'a' becomes NULL before 'b', insert all nodes of 'a' 
   into result list at the beginning. 
```

下面是上述解决方案的实现。

## C / C++

```cpp

/* Given two sorted non-empty linked lists. Merge them in 
   such a way that the result list will be in reverse 
   order. Reversing of linked list is not allowed. Also, 
   extra space should be O(1) */
#include<iostream> 
using namespace std; 

/* Link list Node */
struct Node 
{ 
    int key; 
    struct Node* next; 
}; 

// Given two non-empty linked lists 'a' and 'b' 
Node* SortedMerge(Node *a, Node *b) 
{ 
    // If both lists are empty 
    if (a==NULL && b==NULL) return NULL; 

    // Initialize head of resultant list 
    Node *res = NULL; 

    // Traverse both lists while both of then 
    // have nodes. 
    while (a != NULL && b != NULL) 
    { 
        // If a's current value is smaller or equal to 
        // b's current value. 
        if (a->key <= b->key) 
        { 
            // Store next of current Node in first list 
            Node *temp = a->next; 

            // Add 'a' at the front of resultant list 
            a->next = res; 
            res = a; 

            // Move ahead in first list 
            a = temp; 
        } 

        // If a's value is greater. Below steps are similar 
        // to above (Only 'a' is replaced with 'b') 
        else
        { 
            Node *temp = b->next; 
            b->next = res; 
            res = b; 
            b = temp; 
        } 
    } 

    // If second list reached end, but first list has 
    // nodes. Add remaining nodes of first list at the 
    // front of result list 
    while (a != NULL) 
    { 
        Node *temp = a->next; 
        a->next = res; 
        res = a; 
        a = temp; 
    } 

    // If first list reached end, but second list has 
    // node. Add remaining nodes of first list at the 
    // front of result list 
    while (b != NULL) 
    { 
        Node *temp = b->next; 
        b->next = res; 
        res = b; 
        b = temp; 
    } 

    return res; 
} 

/* Function to print Nodes in a given linked list */
void printList(struct Node *Node) 
{ 
    while (Node!=NULL) 
    { 
        cout << Node->key << " "; 
        Node = Node->next; 
    } 
} 

/* Utility function to create a new node with 
   given key */
Node *newNode(int key) 
{ 
    Node *temp = new Node; 
    temp->key = key; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* res = NULL; 

    /* Let us create two sorted linked lists to test 
       the above functions. Created lists shall be 
         a: 5->10->15 
         b: 2->3->20  */
    Node *a = newNode(5); 
    a->next = newNode(10); 
    a->next->next = newNode(15); 

    Node *b = newNode(2); 
    b->next = newNode(3); 
    b->next->next = newNode(20); 

    cout << "List A before merge: \n"; 
    printList(a); 

    cout << "\nList B before merge: \n"; 
    printList(b); 

    /* merge 2 increasing order LLs in descresing order */
    res = SortedMerge(a, b); 

    cout << "\nMerged Linked List is: \n"; 
    printList(res); 

    return 0; 
}

```

## Java

```java

// Java program to merge two sorted linked list such that merged  
// list is in reverse order 

// Linked List Class 
class LinkedList { 

    Node head;  // head of list 
    static Node a, b; 

    /* Node Class */
    static class Node { 

        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    void printlist(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    Node sortedmerge(Node node1, Node node2) { 

        // if both the nodes are null 
        if (node1 == null && node2 == null) { 
            return null; 
        } 

        // resultant node 
        Node res = null; 

        // if both of them have nodes present traverse them 
        while (node1 != null && node2 != null) { 

            // Now compare both nodes current data 
            if (node1.data <= node2.data) { 
                Node temp = node1.next; 
                node1.next = res; 
                res = node1; 
                node1 = temp; 
            } else { 
                Node temp = node2.next; 
                node2.next = res; 
                res = node2; 
                node2 = temp; 
            } 
        } 

        // If second list reached end, but first list has 
        // nodes. Add remaining nodes of first list at the 
        // front of result list 
        while (node1 != null) { 
            Node temp = node1.next; 
            node1.next = res; 
            res = node1; 
            node1 = temp; 
        } 

        // If first list reached end, but second list has 
        // node. Add remaining nodes of first list at the 
        // front of result list 
        while (node2 != null) { 
            Node temp = node2.next; 
            node2.next = res; 
            res = node2; 
            node2 = temp; 
        } 

        return res; 

    } 

    public static void main(String[] args) { 

        LinkedList list = new LinkedList(); 
        Node result = null; 

        /*Let us create two sorted linked lists to test 
         the above functions. Created lists shall be 
         a: 5->10->15 
         b: 2->3->20*/
        list.a = new Node(5); 
        list.a.next = new Node(10); 
        list.a.next.next = new Node(15); 

        list.b = new Node(2); 
        list.b.next = new Node(3); 
        list.b.next.next = new Node(20); 

        System.out.println("List a before merge :"); 
        list.printlist(a); 
        System.out.println(""); 
        System.out.println("List b before merge :"); 
        list.printlist(b); 

        // merge two sorted linkedlist in decreasing order 
        result = list.sortedmerge(a, b); 
        System.out.println(""); 
        System.out.println("Merged linked list : "); 
        list.printlist(result); 

    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python

```py

# Given two sorted non-empty linked lists. Merge them in 
# such a way that the result list will be in reverse 
# order. Reversing of linked list is not allowed. Also, 
# extra space should be O(1)  

# Node of a linked list  
class Node:  
    def __init__(self, next = None, data = None):  
        self.next = next
        self.data = data  

# Given two non-empty linked lists 'a' and 'b' 
def SortedMerge(a,b): 

    # If both lists are empty 
    if (a == None and b == None): 
        return None

    # Initialize head of resultant list 
    res = None

    # Traverse both lists while both of then 
    # have nodes. 
    while (a != None and b != None): 

        # If a's current value is smaller or equal to 
        # b's current value. 
        if (a.key <= b.key): 

            # Store next of current Node in first list 
            temp = a.next

            # Add 'a' at the front of resultant list 
            a.next = res 
            res = a 

            # Move ahead in first list 
            a = temp 

        # If a's value is greater. Below steps are similar 
        # to above (Only 'a' is replaced with 'b') 
        else: 

            temp = b.next
            b.next = res 
            res = b 
            b = temp 

    # If second list reached end, but first list has 
    # nodes. Add remaining nodes of first list at the 
    # front of result list 
    while (a != None): 

        temp = a.next
        a.next = res 
        res = a 
        a = temp 

    # If first list reached end, but second list has 
    # node. Add remaining nodes of first list at the 
    # front of result list 
    while (b != None): 

        temp = b.next
        b.next = res 
        res = b 
        b = temp 

    return res 

# Function to print Nodes in a given linked list  
def printList(Node): 

    while (Node != None): 

        print( Node.key, end = " ") 
        Node = Node.next

# Utility function to create a new node with 
# given key  
def newNode( key): 

    temp = Node() 
    temp.key = key 
    temp.next = None
    return temp 

# Driver program to test above functions 

# Start with the empty list  
res = None

# Let us create two sorted linked lists to test 
# the above functions. Created lists shall be 
#     a: 5.10.15 
#     b: 2.3.20  
a = newNode(5) 
a.next = newNode(10) 
a.next.next = newNode(15) 

b = newNode(2) 
b.next = newNode(3) 
b.next.next = newNode(20) 

print( "List A before merge: ") 
printList(a) 

print( "\nList B before merge: ") 
printList(b) 

# merge 2 increasing order LLs in descresing order  
res = SortedMerge(a, b) 

print("\nMerged Linked List is: ") 
printList(res) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to merge two sorted  
// linked list such that merged  
// list is in reverse order 

// Linked List Class 
using System; 

class LinkedList 
{ 

    public Node head; // head of list 
    static Node a, b; 

    /* Node Class */
    public class Node 
    { 
        public int data; 
        public Node next; 

        // Constructor to create a new node 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void printlist(Node node)  
    { 
        while (node != null) 
        { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
    } 

    Node sortedmerge(Node node1, Node node2) 
    { 

        // if both the nodes are null 
        if (node1 == null && node2 == null) 
        { 
            return null; 
        } 

        // resultant node 
        Node res = null; 

        // if both of them have nodes  
        // present traverse them 
        while (node1 != null && node2 != null) 
        { 

            // Now compare both nodes current data 
            if (node1.data <= node2.data) 
            { 
                Node temp = node1.next; 
                node1.next = res; 
                res = node1; 
                node1 = temp; 
            }  
            else 
            { 
                Node temp = node2.next; 
                node2.next = res; 
                res = node2; 
                node2 = temp; 
            } 
        } 

        // If second list reached end, but first 
        // list has nodes. Add remaining nodes of  
        // first list at the front of result list 
        while (node1 != null)  
        { 
            Node temp = node1.next; 
            node1.next = res; 
            res = node1; 
            node1 = temp; 
        } 

        // If first list reached end, but second  
        // list has node. Add remaining nodes of  
        // first list at the front of result list 
        while (node2 != null) 
        { 
            Node temp = node2.next; 
            node2.next = res; 
            res = node2; 
            node2 = temp; 
        } 

        return res; 

    } 

    // Driver code 
    public static void Main(String[] args)  
    { 

        LinkedList list = new LinkedList(); 
        Node result = null; 

        /*Let us create two sorted linked lists to test 
        the above functions. Created lists shall be 
        a: 5->10->15 
        b: 2->3->20*/
        LinkedList.a = new Node(5); 
        LinkedList.a.next = new Node(10); 
        LinkedList.a.next.next = new Node(15); 

        LinkedList.b = new Node(2); 
        LinkedList.b.next = new Node(3); 
        LinkedList.b.next.next = new Node(20); 

        Console.WriteLine("List a before merge :"); 
        list.printlist(a); 
        Console.WriteLine(""); 
        Console.WriteLine("List b before merge :"); 
        list.printlist(b); 

        // merge two sorted linkedlist in decreasing order 
        result = list.sortedmerge(a, b); 
        Console.WriteLine(""); 
        Console.WriteLine("Merged linked list : "); 
        list.printlist(result); 

    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
List A before merge: 
5 10 15 
List B before merge: 
2 3 20 
Merged Linked List is: 
20 15 10 5 3 2 
```

此解决方案仅遍历两个列表，不需要反向，并且可以就地工作。

本文由 [**Mohammed Raqeeb**](https://www.linkedin.com/in/mohammed-raqeeb-soudagar-951b345a) 贡献。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

