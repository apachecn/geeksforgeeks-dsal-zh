# 链表的迭代式选择排序

> 原文：[https://www.geeksforgeeks.org/iterative-selection-sort-for-linked-list/](https://www.geeksforgeeks.org/iterative-selection-sort-for-linked-list/)

给定一个链表，任务是使用选择排序以升序对链表排序。

**示例**：

```
Input : 1->4->2->2->3
Output : 1->2->2->3->4

Input : 5->4->3->2
Output : 2->3->4->5

```

**选择排序算法**：迭代给定列表`N`次，其中`N`是列表中元素的数量。 在选择排序的每次迭代中，都会从未排序的子数组中选取最小元素（考虑升序）并将其移至已排序的子数组。

**示例**：

```
list = 64 25 12 22 11

// Find the minimum element in list(0...4)
// and place it at beginning
11 25 12 22 64

// Find the minimum element in list(1...4)
// and place it at beginning of list(1...4)
11 12 25 22 64

// Find the minimum element in list(2...4)
// and place it at beginning of list(2...4)
11 12 22 25 64

// Find the minimum element in list(3...4)
// and place it at beginning of list(3...4)
11 12 22 25 64 

```

可以通过两种方式完成所需的交换：

1.  通过交换节点的数据部分。

2.  通过交换完整的节点。

当列表的元素是某种记录时，通常使用第二种实现方式，因为在这种情况下，由于存在大量数据元素，数据交换变得乏味且昂贵。

**实现方法 1** ：以下是通过仅交换节点的数据部分来对链表排序的选择排序函数的实现。

## C++

```cpp

void selectionSort(node* head) 
{ 
    node* temp = head; 

    // Traverse the List 
    while (temp) { 
        node* min = temp; 
        node* r = temp->next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min->data > r->data) 
                min = r; 

            r = r->next; 
        } 

        // Swap Data 
        int x = temp->data; 
        temp->data = min->data; 
        min->data = x; 
        temp = temp->next; 
    } 
} 

```

## Java

```java

void selectionSort(node head) 
{ 
    node temp = head; 

    // Traverse the List 
    while (temp) { 
        node min = temp; 
        node r = temp.next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min.data > r.data) 
                min = r; 

            r = r.next; 
        } 

        // Swap Data 
        int x = temp.data; 
        temp.data = min.data; 
        min.data = x; 
        temp = temp.next; 
    } 
} 

// This code is contributed by shivanisinghss2110 

```

## C#

```cs

static void selectionSort(node head) 
{ 
    node temp = head; 

    // Traverse the List 
    while (temp) { 
        node min = temp; 
        node r = temp.next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min.data > r.data) 
                min = r; 

            r = r.next; 
        } 

        // Swap Data 
        int x = temp.data; 
        temp.data = min.data; 
        min.data = x; 
        temp = temp.next; 
    } 
} 
// This code contributed by shivanisinghss2110 

```

## Python3

```py

def selectionSort(head): 

    temp = head 

    # Traverse the List 
    while (temp): 

        minn = temp 
        r = temp.next

        # Traverse the unsorted sublist 
        while (r): 
            if (minn.data > r.data): 
                minn = r 

            r = r.next

        # Swap Data 
        x = temp.data 
        temp.data = minn.data 
        minn.data = x 
        temp = temp.next

# This code is contributed by shubhamsingh10 

```

**方法 2** ：数据交换无疑易于实现和理解，但在某些情况下（如上所述），这是不希望的。 在交换两个节点的下一部分时，需要考虑四种情况：

1.  节点是相邻的，第一个节点是起始节点。

2.  节点相邻，第一个节点不是起始节点。

3.  节点不相邻，第一个节点是起始节点。

4.  节点不相邻，第一个节点也不是起始节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Utility function to create a 
// new Linked List Node 
Node* newNode(int val) 
{ 
    Node* temp = new Node; 

    temp->data = val; 

    temp->next = NULL; 

    return temp; 
} 

// Function to sort a linked list using selection 
// sort algorithm by swapping the next pointers 
Node* selectionSort(Node* head) 
{ 
    Node *a, *b, *c, *d, *r; 

    a = b = head; 

    // While b is not the last node 
    while (b->next) { 

        c = d = b->next; 

        // While d is pointing to a valid node 
        while (d) { 

            if (b->data > d->data) { 

                // If d appears immediately after b 
                if (b->next == d) { 

                    // Case 1: b is the head of the linked list 
                    if (b == head) { 

                        // Move d before b 
                        b->next = d->next; 
                        d->next = b; 

                        // Swap b and d pointers 
                        r = b; 
                        b = d; 
                        d = r; 

                        c = d; 

                        // Update the head 
                        head = b; 

                        // Skip to the next element 
                        // as it is already in order 
                        d = d->next; 
                    } 

                    // Case 2: b is not the head of the linked list 
                    else { 

                        // Move d before b 
                        b->next = d->next; 
                        d->next = b; 
                        a->next = d; 

                        // Swap b and d pointers 
                        r = b; 
                        b = d; 
                        d = r; 

                        c = d; 

                        // Skip to the next element 
                        // as it is already in order 
                        d = d->next; 
                    } 
                } 

                // If b and d have some non-zero 
                // number of nodes in between them 
                else { 

                    // Case 3: b is the head of the linked list 
                    if (b == head) { 

                        // Swap b->next and d->next 
                        r = b->next; 
                        b->next = d->next; 
                        d->next = r; 
                        c->next = b; 

                        // Swap b and d pointers 
                        r = b; 
                        b = d; 
                        d = r; 

                        c = d; 

                        // Skip to the next element 
                        // as it is already in order 
                        d = d->next; 

                        // Update the head 
                        head = b; 
                    } 

                    // Case 4: b is not the head of the linked list 
                    else { 

                        // Swap b->next and d->next 
                        r = b->next; 
                        b->next = d->next; 
                        d->next = r; 
                        c->next = b; 
                        a->next = d; 

                        // Swap b and d pointers 
                        r = b; 
                        b = d; 
                        d = r; 

                        c = d; 

                        // Skip to the next element 
                        // as it is already in order 
                        d = d->next; 
                    } 
                } 
            } 
            else { 

                // Update c and skip to the next element 
                // as it is already in order 
                c = d; 
                d = d->next; 
            } 
        } 

        a = b; 
        b = b->next; 
    } 

    return head; 
} 

// Function to print the list 
void printList(Node* head) 
{ 
    while (head) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver Code 
int main() 
{ 
    Node* head = newNode(5); 
    head->next = newNode(4); 
    head->next->next = newNode(3); 

    head = selectionSort(head); 

    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG { 

    // Linked List Node 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Utility function to create a 
    // new Linked List Node 
    static Node newNode(int val) 
    { 
        Node temp = new Node(); 

        temp.data = val; 

        temp.next = null; 

        return temp; 
    } 

    // Function to sort a linked list using selection 
    // sort algorithm by swapping the next pointers 
    static Node selectionSort(Node head) 
    { 
        Node a, b, c, d, r; 

        a = b = head; 

        // While b is not the last node 
        while (b.next != null) { 

            c = d = b.next; 

            // While d is pointing to a valid node 
            while (d != null) { 

                if (b.data > d.data) { 

                    // If d appears immediately after b 
                    if (b.next == d) { 

                        // Case 1: b is the head of the linked list 
                        if (b == head) { 

                            // Move d before b 
                            b.next = d.next; 
                            d.next = b; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Update the head 
                            head = b; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 

                        // Case 2: b is not the head of the linked list 
                        else { 

                            // Move d before b 
                            b.next = d.next; 
                            d.next = b; 
                            a.next = d; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 
                    } 

                    // If b and d have some non-zero 
                    // number of nodes in between them 
                    else { 

                        // Case 3: b is the head of the linked list 
                        if (b == head) { 

                            // Swap b.next and d.next 
                            r = b.next; 
                            b.next = d.next; 
                            d.next = r; 
                            c.next = b; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 

                            // Update the head 
                            head = b; 
                        } 

                        // Case 4: b is not the head of the linked list 
                        else { 

                            // Swap b.next and d.next 
                            r = b.next; 
                            b.next = d.next; 
                            d.next = r; 
                            c.next = b; 
                            a.next = d; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 
                    } 
                } 
                else { 

                    // Update c and skip to the next element 
                    // as it is already in order 
                    c = d; 
                    d = d.next; 
                } 
            } 

            a = b; 
            b = b.next; 
        } 

        return head; 
    } 

    // Function to print the list 
    static void printList(Node head) 
    { 
        while (head != null) { 
            System.out.print(head.data + " "); 
            head = head.next; 
        } 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        Node head = newNode(5); 
        head.next = newNode(4); 
        head.next.next = newNode(3); 

        head = selectionSort(head); 

        printList(head); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach  

# Linked List Node  
class Node: 

    def __init__(self, val): 
        self.data = val 
        self.next = None

# Function to sort a linked list  
# using selection sort algorithm 
# by swapping the next pointers  
def selectionSort(head):  

    a = b = head  

    # While b is not the last node  
    while b.next:  

        c = d = b.next

        # While d is pointing to a valid node  
        while d:  

            if b.data > d.data:  

                # If d appears immediately after b  
                if b.next == d:  

                    # Case 1: b is the head  
                    # of the linked list  
                    if b == head:  

                        # Move d before b  
                        b.next = d.next
                        d.next = b  

                        # Swap b and d pointers  
                        b, d = d, b  
                        c = d  

                        # Update the head  
                        head = b  

                        # Skip to the next element  
                        # as it is already in order  
                        d = d.next

                    # Case 2: b is not the head  
                    # of the linked list  
                    else:  

                        # Move d before b  
                        b.next = d.next
                        d.next = b  
                        a.next = d  

                        # Swap b and d pointers  
                        b, d = d, b  
                        c = d  

                        # Skip to the next element  
                        # as it is already in order  
                        d = d.next

                # If b and d have some non-zero  
                # number of nodes in between them  
                else: 

                    # Case 3: b is the head  
                    # of the linked list  
                    if b == head:  

                        # Swap b.next and d.next  
                        r = b.next
                        b.next = d.next
                        d.next = r  
                        c.next = b  

                        # Swap b and d pointers  
                        b, d = d, b  
                        c = d  

                        # Skip to the next element  
                        # as it is already in order  
                        d = d.next

                        # Update the head  
                        head = b  

                    # Case 4: b is not the head 
                    # of the linked list  
                    else:  

                        # Swap b.next and d.next  
                        r = b.next
                        b.next = d.next
                        d.next = r  
                        c.next = b  
                        a.next = d  

                        # Swap b and d pointers  
                        b, d = d, b  
                        c = d  

                        # Skip to the next element  
                        # as it is already in order  
                        d = d.next

            else: 

                # Update c and skip to the next element  
                # as it is already in order  
                c = d  
                d = d.next

        a = b  
        b = b.next

    return head  

# Function to print the list  
def printList(head):  

    while head:  
        print(head.data, end = " ")  
        head = head.next

# Driver Code  
if __name__ == "__main__": 

    head = Node(5)  
    head.next = Node(4)  
    head.next.next = Node(3)  

    head = selectionSort(head)  

    printList(head)  

# This code is contributed  
# by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG { 

    // Linked List Node 
    public class Node { 
        public int data; 
        public Node next; 
    }; 

    // Utility function to create a 
    // new Linked List Node 
    static Node newNode(int val) 
    { 
        Node temp = new Node(); 

        temp.data = val; 

        temp.next = null; 

        return temp; 
    } 

    // Function to sort a linked list using selection 
    // sort algorithm by swapping the next pointers 
    static Node selectionSort(Node head) 
    { 
        Node a, b, c, d, r; 

        a = b = head; 

        // While b is not the last node 
        while (b.next != null) { 

            c = d = b.next; 

            // While d is pointing to a valid node 
            while (d != null) { 

                if (b.data > d.data) { 

                    // If d appears immediately after b 
                    if (b.next == d) { 

                        // Case 1: b is the head of the linked list 
                        if (b == head) { 

                            // Move d before b 
                            b.next = d.next; 
                            d.next = b; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Update the head 
                            head = b; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 

                        // Case 2: b is not the head of the linked list 
                        else { 

                            // Move d before b 
                            b.next = d.next; 
                            d.next = b; 
                            a.next = d; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 
                    } 

                    // If b and d have some non-zero 
                    // number of nodes in between them 
                    else { 

                        // Case 3: b is the head of the linked list 
                        if (b == head) { 

                            // Swap b.next and d.next 
                            r = b.next; 
                            b.next = d.next; 
                            d.next = r; 
                            c.next = b; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 

                            // Update the head 
                            head = b; 
                        } 

                        // Case 4: b is not the head of the linked list 
                        else { 

                            // Swap b.next and d.next 
                            r = b.next; 
                            b.next = d.next; 
                            d.next = r; 
                            c.next = b; 
                            a.next = d; 

                            // Swap b and d pointers 
                            r = b; 
                            b = d; 
                            d = r; 

                            c = d; 

                            // Skip to the next element 
                            // as it is already in order 
                            d = d.next; 
                        } 
                    } 
                } 
                else { 

                    // Update c and skip to the next element 
                    // as it is already in order 
                    c = d; 
                    d = d.next; 
                } 
            } 

            a = b; 
            b = b.next; 
        } 

        return head; 
    } 

    // Function to print the list 
    static void printList(Node head) 
    { 
        while (head != null) { 
            Console.Write(head.data + " "); 
            head = head.next; 
        } 
    } 

    // Driver Code 
    public static void Main(String[] arg) 
    { 
        Node head = newNode(5); 
        head.next = newNode(4); 
        head.next.next = newNode(3); 

        head = selectionSort(head); 

        printList(head); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
3 4 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。