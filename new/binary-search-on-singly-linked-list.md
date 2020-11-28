# 对单链表

> 原文：[https://www.geeksforgeeks.org/binary-search-on-singly-linked-list/](https://www.geeksforgeeks.org/binary-search-on-singly-linked-list/)

进行二分搜索

给定一个单链表和一个密钥，请使用[二分搜索](https://www.geeksforgeeks.org/binary-search/)方法查找密钥。

为了执行基于分治算法的二分搜索，确定中间元素非常重要。 对于数组，二分搜索通常是快速而有效的，因为访问两个给定索引之间的中间索引既简单又快速（时间复杂度`O(1)`）。 但是，单链表的内存分配是动态且不连续的，这使得查找中间元素变得困难。 一种方法可能是使用[跳表](https://www.geeksforgeeks.org/skip-list/)，一种可能是使用一个指针遍历链表。

**前提**：[在链表的中间找到。](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)

**注意：以下提供的方法和实现旨在说明如何在链表上实现二分搜索。 该实现需要`O(n)`时间。**

**方法**：

*   在这里，给出了起始节点（设置为列表头）和最后一个节点（最初设置为`NULL`）。

*   中间是使用两个指针方法计算的。

*   如果中间数据与搜索所需的值匹配，则将其返回。

*   否则，如果中间的数据

*   否则转到下半部分（最后设置为中间）。

*   出现的条件是，找到元素或遍历整个列表。 当遍历整个列表时，`last`指向开始，即`last-> next == start`。

在主函数中，函数`InsertAtHead`在链表的开头插入值。 插入这样的值（为简单起见），以便对创建的列表进行排序。

例子 ：

```
Input : Enter value to search : 7
Output : Found

Input : Enter value to search : 12
Output : Not Found

```

## C++

```cpp

// CPP code to implement binary search 
// on Singly Linked List 
#include<stdio.h> 
#include<stdlib.h> 

struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

Node *newNode(int x) 
{ 
    struct Node* temp = new Node; 
    temp->data = x; 
    temp->next = NULL; 
    return temp; 
} 

// function to find out middle element 
struct Node* middle(Node* start, Node* last) 
{ 
    if (start == NULL) 
        return NULL; 

    struct Node* slow = start; 
    struct Node* fast = start -> next; 

    while (fast != last) 
    { 
        fast = fast -> next; 
        if (fast != last) 
        { 
            slow = slow -> next; 
            fast = fast -> next; 
        } 
    } 

    return slow; 
} 

// Function for implementing the Binary 
// Search on linked list 
struct Node* binarySearch(Node *head, int value) 
{ 
    struct Node* start = head; 
    struct Node* last = NULL; 

    do
    { 
        // Find middle 
        Node* mid = middle(start, last); 

        // If middle is empty 
        if (mid == NULL) 
            return NULL; 

        // If value is present at middle 
        if (mid -> data == value) 
            return mid; 

        // If value is more than mid 
        else if (mid -> data < value) 
            start = mid -> next; 

        // If the value is less than mid. 
        else
            last = mid; 

    } while (last == NULL || 
             last != start); 

    // value not present 
    return NULL; 
} 

// Driver Code 
int main() 
{ 
    Node *head = newNode(1); 
    head->next = newNode(4); 
    head->next->next = newNode(7); 
    head->next->next->next = newNode(8); 
    head->next->next->next->next = newNode(9); 
    head->next->next->next->next->next = newNode(10); 
    int value = 7; 
    if (binarySearch(head, value) == NULL) 
        printf("Value not present\n"); 
    else
        printf("Present"); 
    return 0; 
} 

```

## Java

```java

// Java code to implement binary search  
// on Singly Linked List  

// Node Class 
class Node 
{ 
    int data; 
    Node next; 

    // Constructor to create a new node 
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

class BinarySearch 
{ 
    // function to insert a node at the beginning 
    // of the Singaly Linked List 
    static Node push(Node head, int data) 
    { 
        Node newNode = new Node(data); 
        newNode.next = head; 
        head = newNode; 
        return head; 
    } 

    // Function to find middle element 
    // using Fast and Slow pointers 
    static Node middleNode(Node start, Node last)  
    { 
        if (start == null) 
            return null; 

        Node slow = start; 
        Node fast = start.next; 

        while (fast != last) 
        { 
            fast = fast.next; 
            if (fast != last)  
            { 
                slow = slow.next; 
                fast = fast.next; 
            } 
        } 
        return slow; 
    } 

    // function to insert a node at the beginning 
    // of the Singly Linked List 
    static Node binarySearch(Node head, int value)  
    { 
        Node start = head; 
        Node last = null; 

        do
        { 
            // Find Middle 
            Node mid = middleNode(start, last); 

            // If middle is empty 
            if (mid == null) 
                return null; 

            // If value is present at middle 
            if (mid.data == value) 
                return mid; 

            // If value is less than mid 
            else if (mid.data > value)  
            { 
                start = mid.next; 
            } 

            // If the value is more than mid. 
            else
                last = mid; 
        } while (last == null || last != start); 

        // value not present 
        return null; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        Node head = null; 

        // Using push() function to 
        // convert singly linked list 
        // 10 -> 9 -> 8 -> 7 -> 4 -> 1 
        head = push(head, 1); 
        head = push(head, 4); 
        head = push(head, 7); 
        head = push(head, 8); 
        head = push(head, 9); 
        head = push(head, 10); 
        int value = 7; 

        if (binarySearch(head, value) == null) 
        { 
            System.out.println("Value not present"); 
        }  
        else
        { 
            System.out.println("Present"); 
        } 
    } 
} 

// This code is contributed by Vivekkumar Singh 

```

## Python

```py

# Python code to implement binary search  
# on Singly Linked List  

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None
        self.prev = None

def newNode(x): 

    temp = Node(0) 
    temp.data = x 
    temp.next = None
    return temp 

# function to find out middle element 
def middle(start, last): 

    if (start == None): 
        return None

    slow = start 
    fast = start . next

    while (fast != last): 

        fast = fast . next
        if (fast != last): 

            slow = slow . next
            fast = fast . next

    return slow 

# Function for implementing the Binary 
# Search on linked list 
def binarySearch(head,value): 

    start = head 
    last = None

    while True : 

        # Find middle 
        mid = middle(start, last) 

        # If middle is empty 
        if (mid == None): 
            return None

        # If value is present at middle 
        if (mid . data == value): 
            return mid 

        # If value is more than mid 
        elif (mid . data < value): 
            start = mid . next

        # If the value is less than mid. 
        else: 
            last = mid 

        if not (last == None or last != start): 
            break

    # value not present 
    return None

# Driver Code 

head = newNode(1) 
head.next = newNode(4) 
head.next.next = newNode(7) 
head.next.next.next = newNode(8) 
head.next.next.next.next = newNode(9) 
head.next.next.next.next.next = newNode(10) 
value = 7
if (binarySearch(head, value) == None): 
    print("Value not present\n") 
else: 
    print("Present") 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# code to implement binary search  
// on Singly Linked List  

using System; 

// Node Class 
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

class BinarySearch 
{ 
    // function to insert a node at the beginning 
    // of the Singaly Linked List 
    static Node push(Node head, int data) 
    { 
        Node newNode = new Node(data); 
        newNode.next = head; 
        head = newNode; 
        return head; 
    } 

    // Function to find middle element 
    // using Fast and Slow pointers 
    static Node middleNode(Node start, Node last)  
    { 
        if (start == null) 
            return null; 

        Node slow = start; 
        Node fast = start.next; 

        while (fast != last) 
        { 
            fast = fast.next; 
            if (fast != last)  
            { 
                slow = slow.next; 
                fast = fast.next; 
            } 
        } 
        return slow; 
    } 

    // function to insert a node at the beginning 
    // of the Singly Linked List 
    static Node binarySearch(Node head, int value)  
    { 
        Node start = head; 
        Node last = null; 

        do
        { 
            // Find Middle 
            Node mid = middleNode(start, last); 

            // If middle is empty 
            if (mid == null) 
                return null; 

            // If value is present at middle 
            if (mid.data == value) 
                return mid; 

            // If value is less than mid 
            else if (mid.data > value)  
            { 
                start = mid.next; 
            } 

            // If the value is more than mid. 
            else
                last = mid; 
        } while (last == null || last != start); 

        // value not present 
        return null; 
    } 

    // Driver Code 
    public static void Main(String []args)  
    { 
        Node head = null; 

        // Using push() function to 
        // convert singly linked list 
        // 10 -> 9 -> 8 -> 7 -> 4 -> 1 
        head = push(head, 1); 
        head = push(head, 4); 
        head = push(head, 7); 
        head = push(head, 8); 
        head = push(head, 9); 
        head = push(head, 10); 
        int value = 7; 

        if (binarySearch(head, value) == null) 
        { 
            Console.WriteLine("Value not present"); 
        }  
        else
        { 
            Console.WriteLine("Present"); 
        } 
    } 
} 

// This code is contributed by Arnab Kundu 

```

**输出**：

```
Present

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。