# 不查找长度的情况下查找两个链表的交点

> 原文：[https://www.geeksforgeeks.org/find-intersection-point-of-two-linked-lists-without-finding-the-length/](https://www.geeksforgeeks.org/find-intersection-point-of-two-linked-lists-without-finding-the-length/)

系统中有两个单链表。 由于编程错误，链表之一的末端节点链接到第二个列表，从而形成了一个倒 Y 形列表。 编写一个程序，使两个链表合并。

**示例**：

```
Input: 1 -> 2 -> 3 -> 4 -> 5 -> 6
                      ^
                      |
            7 -> 8 -> 9
Output: 4

Input:         13 -> 14 -> 5 -> 6
                      ^
                      |
      10 -> 2 -> 3 -> 4 
Output: 14

```

**先决条件**：[编写函数来获取两个链表的交点](https://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)

**方法**：将两个指针指向两个链表的头部。 如果其中一个提前到达末尾，则通过将其移至另一列表的开头来使用它。 一旦它们都经过重新分配，它们将与碰撞点等距。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

// Function to return the intersection point 
// of the two linked lists head1 and head2 
int getIntesectionNode(Node* head1, Node* head2) 
{ 
    Node* current1 = head1; 
    Node* current2 = head2; 

    // If one of the head is NULL 
    if (!current1 or !current2) 
        return -1; 

    // Continue until we find intersection node 
    while (current1 and current2 
           and current1 != current2) { 
        current1 = current1->next; 
        current2 = current2->next; 

        // If we get intersection node 
        if (current1 == current2) 
            return current1->data; 

        // If one of them reaches end 
        if (!current1) 
            current1 = head2; 
        if (!current2) 
            current2 = head1; 
    } 

    return current1->data; 
} 

// Driver code 
int main() 
{ 
    /*  
        Create two linked lists  

        1st 3->6->9->15->30  
        2nd 10->15->30  

        15 is the intersection point  
    */

    Node* newNode; 

    // Addition of new nodes 
    Node* head1 = new Node(); 
    head1->data = 10; 

    Node* head2 = new Node(); 
    head2->data = 3; 

    newNode = new Node(); 
    newNode->data = 6; 
    head2->next = newNode; 

    newNode = new Node(); 
    newNode->data = 9; 
    head2->next->next = newNode; 

    newNode = new Node(); 
    newNode->data = 15; 
    head1->next = newNode; 
    head2->next->next->next = newNode; 

    newNode = new Node(); 
    newNode->data = 30; 
    head1->next->next = newNode; 

    head1->next->next->next = NULL; 

    cout << getIntesectionNode(head1, head2); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

/* Link list node */
static class Node 
{ 

    int data; 
    Node next; 
}; 

// Function to return the intersection point 
// of the two linked lists head1 and head2 
static int getIntesectionNode(Node head1, Node head2) 
{ 
    Node current1 = head1; 
    Node current2 = head2; 

    // If one of the head is null 
    if (current1 == null || current2 == null ) 
        return -1; 

    // Continue until we find intersection node 
    while (current1 != null && current2 != null
        && current1 != current2) 
    { 
        current1 = current1.next; 
        current2 = current2.next; 

        // If we get intersection node 
        if (current1 == current2) 
            return current1.data; 

        // If one of them reaches end 
        if (current1 == null ) 
            current1 = head2; 
        if (current2 == null ) 
            current2 = head1; 
    } 

    return current1.data; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    /*  
        Create two linked lists  

        1st 3.6.9.15.30  
        2nd 10.15.30  

        15 is the intersection point  
    */

    Node newNode; 

    // Addition of new nodes 
    Node head1 = new Node(); 
    head1.data = 10; 

    Node head2 = new Node(); 
    head2.data = 3; 

    newNode = new Node(); 
    newNode.data = 6; 
    head2.next = newNode; 

    newNode = new Node(); 
    newNode.data = 9; 
    head2.next.next = newNode; 

    newNode = new Node(); 
    newNode.data = 15; 
    head1.next = newNode; 
    head2.next.next.next = newNode; 

    newNode = new Node(); 
    newNode.data = 30; 
    head1.next.next = newNode; 

    head1.next.next.next = null; 

    System.out.print(getIntesectionNode(head1, head2)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation of the approach 

''' Link list node '''
class new_Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to return the intersection point 
# of the two linked lists head1 and head2 
def getIntesectionNode(head1, head2): 

    current1 = head1 
    current2 = head2 

    # If one of the head is None 
    if (not current1 or not current2 ): 
        return -1

    # Continue until we find intersection node 
    while (current1 and current2 and current1 != current2): 
        current1 = current1.next
        current2 = current2.next

        # If we get intersection node 
        if (current1 == current2): 
            return current1.data 

        # If one of them reaches end 
        if (not current1): 
            current1 = head2 

        if (not current2): 
            current2 = head1 

    return current1.data 

# Driver code 
'''  
    Create two linked lists  

    1st 3.6.9.15.30  
    2nd 10.15.30  

    15 is the intersection po 
'''

# Addition of newNodes 
head1 = new_Node(10) 

head2 = new_Node(3) 

newNode = new_Node(6) 
head2.next = newNode 

newNode = new_Node(9) 
head2.next.next = newNode 

newNode = new_Node(15) 
head1.next = newNode 
head2.next.next.next = newNode 

newNode = new_Node(30) 
head1.next.next = newNode 

head1.next.next.next = None

print(getIntesectionNode(head1, head2)) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

/* Link list node */
class Node 
{ 

    public int data; 
    public Node next; 
}; 

// Function to return the intersection point 
// of the two linked lists head1 and head2 
static int getIntesectionNode(Node head1, Node head2) 
{ 
    Node current1 = head1; 
    Node current2 = head2; 

    // If one of the head is null 
    if (current1 == null || current2 == null ) 
        return -1; 

    // Continue until we find intersection node 
    while (current1 != null && current2 != null
        && current1 != current2) 
    { 
        current1 = current1.next; 
        current2 = current2.next; 

        // If we get intersection node 
        if (current1 == current2) 
            return current1.data; 

        // If one of them reaches end 
        if (current1 == null ) 
            current1 = head2; 
        if (current2 == null ) 
            current2 = head1; 
    } 

    return current1.data; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    /*  
        Create two linked lists  

        1st 3.6.9.15.30  
        2nd 10.15.30  

        15 is the intersection point  
    */

    Node newNode; 

    // Addition of new nodes 
    Node head1 = new Node(); 
    head1.data = 10; 

    Node head2 = new Node(); 
    head2.data = 3; 

    newNode = new Node(); 
    newNode.data = 6; 
    head2.next = newNode; 

    newNode = new Node(); 
    newNode.data = 9; 
    head2.next.next = newNode; 

    newNode = new Node(); 
    newNode.data = 15; 
    head1.next = newNode; 
    head2.next.next.next = newNode; 

    newNode = new Node(); 
    newNode.data = 30; 
    head1.next.next = newNode; 

    head1.next.next.next = null; 

    Console.Write(getIntesectionNode(head1, head2)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
15

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。