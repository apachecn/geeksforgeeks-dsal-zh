# 从链表的末尾查找第`n`个节点的递归方法

> 原文：[https://www.geeksforgeeks.org/recursive-approach-to-find-nth-node-from-the-end-in-the-linked-list/](https://www.geeksforgeeks.org/recursive-approach-to-find-nth-node-from-the-end-in-the-linked-list/)

使用递归方法从给定链表的末尾找到第`n`个节点。

**示例**：

```
Input : list: 4->2->1->5->3
         n = 2
Output : 5

```

**算法**：

```
findNthFromLast(head, n, count, nth_last)
    if head == NULL then
        return

    findNthFromLast(head->next, n, count, nth_last)
    count = count + 1
    if count == n then
        nth_last = head

findNthFromLastUtil(head, n)
    Initialize nth_last = NULL
    Initialize count = 0

    findNthFromLast(head, n, &count, &nth_last)

    if nth_last != NULL then
        print nth_last->data
    else
        print "Node does not exists"

```

**注意**：参数`count`和`nth_last`将是`findNthFromLast()`中的指针变量。

## C++

```cpp

// C++ implementation to recursively find the nth node from 
// the last of the linked list 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node of a linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = new Node; 

    // put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// funnction to recursively find the nth node from 
// the last of the linked list 
void findNthFromLast(Node* head, int n, int* count, 
                     Node** nth_last) 
{ 
    // if list is empty 
    if (!head) 
        return; 

    // recursive call 
    findNthFromLast(head->next, n, count, nth_last); 

    // increment count 
    *count = *count + 1; 

    // if true, then head is the nth node from the last 
    if (*count == n) 
        *nth_last = head; 
} 

// utility function to find the nth node from 
// the last of the linked list 
void findNthFromLastUtil(Node* head, int n) 
{ 
    // Initialize 
    Node* nth_last = NULL; 
    int count = 0; 

    // find nth node from the last 
    findNthFromLast(head, n, &count, &nth_last); 

    // if node exists, then print it 
    if (nth_last != NULL) 
        cout << "Nth node from last is: "
             << nth_last->data; 
    else
        cout << "Node does not exists"; 
} 

// Driver program to test above 
int main() 
{ 
    // linked list: 4->2->1->5->3 
    Node* head = getNode(4); 
    head->next = getNode(2); 
    head->next->next = getNode(1); 
    head->next->next->next = getNode(5); 
    head->next->next->next->next = getNode(3); 

    int n = 2; 

    findNthFromLastUtil(head, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation to recursively  
// find the nth node from the last 
// of the linked list  
import java.util.*; 
class GFG 
{ 
static int count = 0, data = 0; 

// a node of a linked list  
static class Node  
{  
    int data;  
    Node next;  
} 

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// funnction to recursively  
// find the nth node from  
// the last of the linked list  
static void findNthFromLast(Node head, int n,  
                            Node nth_last)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // recursive call  
    findNthFromLast(head.next, n, nth_last);  

    // increment count  
    count = count + 1;  

    // if true, then head is the 
    // nth node from the last  
    if (count == n)  
    { 
        data = head.data;  
    } 
}  

// utility function to find  
// the nth node from the last 
// of the linked list  
static void findNthFromLastUtil(Node head, int n)  
{  
    // Initialize  
    Node nth_last = new Node();  
    count = 0;  

    // find nth node from the last  
    findNthFromLast(head, n, nth_last);  

    // if node exists, then print it  
    if (nth_last != null)  
        System.out.println("Nth node from last is: " + 
                                                data);  
    else
        System.out.println("Node does not exists");  
}  

// Driver Code 
public static void main(String args[]) 
{  
    // linked list: 4.2.1.5.3  
    Node head = getNode(4);  
    head.next = getNode(2);  
    head.next.next = getNode(1);  
    head.next.next.next = getNode(5);  
    head.next.next.next.next = getNode(3);  

    int n = 2;  

    findNthFromLastUtil(head, n);  
}  
} 

// This code is contributed  
// by Arnab Kundu 

```

## Python

```py

# Python implementation to recursively  
# find the nth node from the last  
# of the linked list  
count = 0
data = 0

# a node of a linked list  
class Node(object):  
    def __init__(self, d):  
        self.data = d  
        self.next = None

# function to get a new node  
def getNode(data):  

    # allocate space  
    newNode = Node(0)  

    # put in data  
    newNode.data = data  
    newNode.next = None
    return newNode  

# funnction to recursively  
# find the nth node from  
# the last of the linked list  
def findNthFromLast(head, n, nth_last) : 

    global count 
    global data 

    # if list is empty  
    if (head == None):  
        return

    # recursive call  
    findNthFromLast(head.next, n, nth_last)  

    # increment count  
    count = count + 1

    # if true, then head is the  
    # nth node from the last  
    if (count == n) : 

        data = head.data  

# utility function to find  
# the nth node from the last  
# of the linked list  
def findNthFromLastUtil(head, n) : 

    global count 
    global data 

    # Initialize  
    nth_last = Node(0)  
    count = 0

    # find nth node from the last  
    findNthFromLast(head, n, nth_last)  

    # if node exists, then print it  
    if (nth_last != None) : 
        print("Nth node from last is: " , data)  
    else: 
        print("Node does not exists")  

# Driver Code  

# linked list: 4.2.1.5.3  
head = getNode(4)  
head.next = getNode(2)  
head.next.next = getNode(1)  
head.next.next.next = getNode(5)  
head.next.next.next.next = getNode(3)  

n = 2

findNthFromLastUtil(head, n)  

# This code is contributed  
# by Arnab Kundu  

```

## C#

```cs

// C# implementation to recursively  
// find the nth node from the last 
// of the linked list  
using System; 

public class GFG 
{ 
    static int count = 0, data = 0; 

    // a node of a linked list  
    class Node  
    {  
        public int data;  
        public Node next;  
    } 

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// funnction to recursively  
// find the nth node from  
// the last of the linked list  
static void findNthFromLast(Node head, int n,  
                            Node nth_last)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // recursive call  
    findNthFromLast(head.next, n, nth_last);  

    // increment count  
    count = count + 1;  

    // if true, then head is the 
    // nth node from the last  
    if (count == n)  
    { 
        data = head.data;  
    } 
}  

// utility function to find  
// the nth node from the last 
// of the linked list  
static void findNthFromLastUtil(Node head, int n)  
{  
    // Initialize  
    Node nth_last = new Node();  
    count = 0;  

    // find nth node from the last  
    findNthFromLast(head, n, nth_last);  

    // if node exists, then print it  
    if (nth_last != null)  
        Console.WriteLine("Nth node from last is: " + 
                                                data);  
    else
        Console.WriteLine("Node does not exists");  
}  

// Driver Code 
public static void Main(String []args) 
{  
    // linked list: 4.2.1.5.3  
    Node head = getNode(4);  
    head.next = getNode(2);  
    head.next.next = getNode(1);  
    head.next.next.next = getNode(5);  
    head.next.next.next.next = getNode(3);  

    int n = 2;  

    findNthFromLastUtil(head, n);  
}  
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Nth node from last is: 5

```

**时间复杂度**：`O(n)`，其中`n`是链表中的节点数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。