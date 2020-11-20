# 以相反的顺序打印链表的最后 k 个节点| 迭代方法

> 原文：[https://www.geeksforgeeks.org/print-the-last-k-nodes-of-the-linked-list-in-reverse-order-iterative-approaches/](https://www.geeksforgeeks.org/print-the-last-k-nodes-of-the-linked-list-in-reverse-order-iterative-approaches/)

给定一个包含 N 个节点和正整数 K 的链表，其中 K 应当小于或等于 N。任务是按相反的顺序打印列表的最后 K 个节点。

**示例**：

```
Input : list: 1->2->3->4->5, K = 2
Output : 5 4

Input : list: 3->10->6->9->12->2->8, K = 4
Output : 8 2 12 9

```

[先前的文章](https://www.geeksforgeeks.org/print-the-last-k-nodes-of-the-linked-list-in-reverse-order/)中讨论的解决方案使用递归方法。 下面的文章讨论了解决上述问题的三种迭代方法。

**方法 1**：的想法是使用堆栈数据结构。 推送所有链接的列表节点数据值以堆叠并弹出前 K 个元素并打印它们。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to print the last k nodes 
// of linked list in reverse order 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = new Node; 

    // put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
void printLastKRev(Node* head, int k) 
{ 
    // if list is empty 
    if (!head) 
        return; 

    // Stack to store data value of nodes. 
    stack<int> st; 

    // Push data value of nodes to stack 
    while (head) { 
        st.push(head->data); 
        head = head->next; 
    } 

    int cnt = 0; 

    // Pop first k elements of stack and 
    // print them. 
    while (cnt < k) { 
        cout << st.top() << " "; 
        st.pop(); 
        cnt++; 
    } 
} 

// Driver code 
int main() 
{ 
    // Create list: 1->2->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(3); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation to print the last k nodes 
// of linked list in reverse order 
import java.util.*; 
class GFG  
{ 

// Structure of a node 
static class Node 
{ 
    int data; 
    Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Stack to store data value of nodes. 
    Stack<Integer> st = new Stack<Integer>(); 

    // Push data value of nodes to stack 
    while (head != null)  
    { 
        st.push(head.data); 
        head = head.next; 
    } 

    int cnt = 0; 

    // Pop first k elements of stack and 
    // print them. 
    while (cnt < k)  
    { 
        System.out.print(st.peek() + " "); 
        st.pop(); 
        cnt++; 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 implementation to print the last k nodes  
# of linked list in reverse order 
import sys 
import math 

# Structure of a node  
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Function to get a new node 
def getNode(data): 

    # allocate space and return new node 
    return Node(data) 

# Function to print the last k nodes  
# of linked list in reverse order  
def printLastKRev(head,k): 

    # if list is empty 
    if not head: 
        return

    # Stack to store data value of nodes. 
    stack = [] 

    # Push data value of nodes to stack  
    while(head): 
        stack.append(head.data) 
        head = head.next
    cnt = 0

    # Pop first k elements of stack and  
    # print them. 
    while(cnt < k): 
        print("{} ".format(stack[-1]),end="") 
        stack.pop() 
        cnt += 1

# Driver code  
if __name__=='__main__': 

    # Create list: 1->2->3->4->5  
    head = getNode(1) 
    head.next = getNode(2) 
    head.next.next = getNode(3) 
    head.next.next.next = getNode(4) 
    head.next.next.next.next = getNode(5) 

    k = 4

    # print the last k nodes  
    printLastKRev(head,k) 

# This Code is Contributed by Vikash Kumar 37 

```

## C#

```cs

// C# implementation to print the last k nodes 
// of linked list in reverse order 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// Structure of a node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Stack to store data value of nodes. 
    Stack<int> st = new Stack<int>(); 

    // Push data value of nodes to stack 
    while (head != null)  
    { 
        st.Push(head.data); 
        head = head.next; 
    } 

    int cnt = 0; 

    // Pop first k elements of stack and 
    // print them. 
    while (cnt < k)  
    { 
        Console.Write(st.Peek() + " "); 
        st.Pop(); 
        cnt++; 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
5 4 3 2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

**上述方法的辅助空间可以减小为 O（k）**。 这个想法是使用两个指针。 将第一个指针移到列表的开头，然后将第二个指针移到第 k 个节点。 然后使用本文讨论的方法从头开始查找第 k 个节点：[从链表](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)的末尾查找第 k 个节点。 从末端找到第 k 个节点后，推入堆栈中的所有其余节点。 从堆栈中逐一弹出所有元素并进行打印。

以下是上述有效方法的实现：

## C++

```cpp

// C++ implementation to print the last k nodes 
// of linked list in reverse order 

#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = new Node; 

    // put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
void printLastKRev(Node* head, int k) 
{ 
    // if list is empty 
    if (!head) 
        return; 

    // Stack to store data value of nodes. 
    stack<int> st; 

    // Declare two pointers. 
    Node *first = head, *sec = head; 

    int cnt = 0; 

    // Move second pointer to kth node. 
    while (cnt < k) { 
        sec = sec->next; 
        cnt++; 
    } 

    // Move first pointer to kth node from end 
    while (sec) { 
        first = first->next; 
        sec = sec->next; 
    } 

    // Push last k nodes in stack 
    while (first) { 
        st.push(first->data); 
        first = first->next; 
    } 

    // Last k nodes are reversed when pushed 
    // in stack. Pop all k elements of stack 
    // and print them. 
    while (!st.empty()) { 
        cout << st.top() << " "; 
        st.pop(); 
    } 
} 

// Driver code 
int main() 
{ 
    // Create list: 1->2->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(3); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation to print  
// the last k nodes of linked list 
// in reverse order 
import java.util.*; 
class GFG 
{ 

// Structure of a node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Stack to store data value of nodes. 
    Stack<Integer> st = new Stack<Integer>(); 

    // Declare two pointers. 
    Node first = head, sec = head; 

    int cnt = 0; 

    // Move second pointer to kth node. 
    while (cnt < k)  
    { 
        sec = sec.next; 
        cnt++; 
    } 

    // Move first pointer to kth node from end 
    while (sec != null) 
    { 
        first = first.next; 
        sec = sec.next; 
    } 

    // Push last k nodes in stack 
    while (first != null) 
    { 
        st.push(first.data); 
        first = first.next; 
    } 

    // Last k nodes are reversed when pushed 
    // in stack. Pop all k elements of stack 
    // and print them. 
    while (!st.empty()) 
    { 
        System.out.print(st.peek() + " "); 
        st.pop(); 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python

```py

# Python implementation to print the last k nodes 
# of linked list in reverse order 

# Node class  
class Node: 

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data # Assign data  
        self.next = None

# Function to get a new node 
def getNode(data): 

    # allocate space 
    newNode = Node(0) 

    # put in data 
    newNode.data = data 
    newNode.next = None
    return newNode 

# Function to print the last k nodes 
# of linked list in reverse order 
def printLastKRev( head, k): 

    # if list is empty 
    if (head == None): 
        return

    # Stack to store data value of nodes. 
    st = [] 

    # Declare two pointers. 
    first = head 
    sec = head 

    cnt = 0

    # Move second pointer to kth node. 
    while (cnt < k) : 
        sec = sec.next
        cnt = cnt + 1

    # Move first pointer to kth node from end 
    while (sec != None):  
        first = first.next
        sec = sec.next

    # Push last k nodes in stack 
    while (first != None):  
        st.append(first.data) 
        first = first.next

    # Last k nodes are reversed when pushed 
    # in stack. Pop all k elements of stack 
    # and print them. 
    while (len(st)):  
        print( st[-1], end= " ") 
        st.pop() 

# Driver code 

# Create list: 1.2.3.4.5 
head = getNode(1) 
head.next = getNode(2) 
head.next.next = getNode(3) 
head.next.next.next = getNode(4) 
head.next.next.next.next = getNode(5) 

k = 4

# print the last k nodes 
printLastKRev(head, k) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to print  
// the last k nodes of linked list 
// in reverse order 
using System; 
using System.Collections.Generic;  

class GFG 
{ 

// Structure of a node 
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Stack to store data value of nodes. 
    Stack<int> st = new Stack<int>(); 

    // Declare two pointers. 
    Node first = head, sec = head; 

    int cnt = 0; 

    // Move second pointer to kth node. 
    while (cnt < k)  
    { 
        sec = sec.next; 
        cnt++; 
    } 

    // Move first pointer to kth node from end 
    while (sec != null) 
    { 
        first = first.next; 
        sec = sec.next; 
    } 

    // Push last k nodes in stack 
    while (first != null) 
    { 
        st.Push(first.data); 
        first = first.next; 
    } 

    // Last k nodes are reversed when pushed 
    // in stack. Pop all k elements of stack 
    // and print them. 
    while (st.Count != 0) 
    { 
        Console.Write(st.Peek() + " "); 
        st.Pop(); 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
5 4 3 2

```

**时间复杂度**：`O(n)`

**辅助空间**：O（k）

**方法 2**：

*   计算链表中的节点数。

*   声明一个数组，并以节点数作为其大小。

*   从数组末尾开始存储链表的节点值，即反向存储。

*   从数组开始打印 k 个值。

## C++

```cpp

#include <iostream>  
using namespace std;  

// Structure of a node  
struct Node {  
    int data;  
    Node* next;  
};  

// Function to get a new node  
Node* getNode(int data){  
    // allocate space  
    Node* newNode = new Node;  

    // put in data  
    newNode->data = data;  
    newNode->next = NULL;  
    return newNode;  
}  

// Function to print the last k nodes  
// of linked list in reverse order  
void printLastKRev(Node* head,  
                     int& count, int k) { 
    struct Node* cur = head; 

    while(cur != NULL){ 
        count++; 
        cur = cur->next; 
    } 

    int arr[count], temp = count; 
    cur = head; 

    while(cur != NULL){ 
        arr[--temp] = cur->data; 
        cur = cur->next; 
    } 

    for(int i = 0; i < k; i++) 
        cout << arr[i] << " "; 
}  
  // 
// Driver code  
int main()  
{  
    // Create list: 1->2->3->4->5  
    Node* head = getNode(1);  
    head->next = getNode(2);  
    head->next->next = getNode(3);  
    head->next->next->next = getNode(4);  
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(10); 

    int k = 4, count = 0;  

    // print the last k nodes  
    printLastKRev(head, count, k);  

    return 0;  
}  

```

## Java

```java

// Java code implementation for above approach 
class GFG  
{  

// Structure of a node  
static class Node 
{  
    int data;  
    Node next;  
};  

// Function to get a new node  
static Node getNode(int data) 
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// Function to print the last k nodes  
// of linked list in reverse order  
static void printLastKRev(Node head,  
                          int count, int k)  
{ 
    Node cur = head; 

    while(cur != null) 
    { 
        count++; 
        cur = cur.next; 
    } 

    int []arr = new int[count]; 
    int temp = count; 
    cur = head; 

    while(cur != null) 
    { 
        arr[--temp] = cur.data; 
        cur = cur.next; 
    } 

    for(int i = 0; i < k; i++) 
        System.out.print(arr[i] + " "); 
}  

// Driver code  
public static void main(String[] args)  
{ 
    // Create list: 1.2.3.4.5  
    Node head = getNode(1);  
    head.next = getNode(2);  
    head.next.next = getNode(3);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(10); 

    int k = 4, count = 0;  

    // print the last k nodes  
    printLastKRev(head, count, k);  
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# code implementation for above approach 
using System; 
class GFG  
{  

// Structure of a node  
class Node 
{  
    public int data;  
    public Node next;  
};  

// Function to get a new node  
static Node getNode(int data) 
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// Function to print the last k nodes  
// of linked list in reverse order  
static void printLastKRev(Node head,  
                          int count, int k)  
{ 
    Node cur = head; 

    while(cur != null) 
    { 
        count++; 
        cur = cur.next; 
    } 

    int []arr = new int[count]; 
    int temp = count; 
    cur = head; 

    while(cur != null) 
    { 
        arr[--temp] = cur.data; 
        cur = cur.next; 
    } 

    for(int i = 0; i < k; i++) 
        Console.Write(arr[i] + " "); 
}  

// Driver code  
public static void Main(String[] args)  
{ 
    // Create list: 1.2.3.4.5  
    Node head = getNode(1);  
    head.next = getNode(2);  
    head.next.next = getNode(3);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(10); 

    int k = 4, count = 0;  

    // print the last k nodes  
    printLastKRev(head, count, k);  
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
10 5 4 3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

**方法 3**：的想法是首先迭代地反向链表，如以下文章所述：[反向链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)。 反转后，打印反转列表的前 k 个节点。 打印后，通过再次反转列表来恢复列表。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to print the last k nodes 
// of linked list in reverse order 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = new Node; 

    // put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to reverse the linked list. 
Node* reverseLL(Node* head) 
{ 
    if (!head || !head->next) 
        return head; 

    Node *prev = NULL, *next = NULL, *curr = head; 

    while (curr) { 
        next = curr->next; 
        curr->next = prev; 
        prev = curr; 
        curr = next; 
    } 

    return prev; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
void printLastKRev(Node* head, int k) 
{ 
    // if list is empty 
    if (!head) 
        return; 

    // Reverse linked list. 
    head = reverseLL(head); 

    Node* curr = head; 

    int cnt = 0; 

    // Print first k nodes of linked list. 
    while (cnt < k) { 
        cout << curr->data << " "; 
        cnt++; 
        curr = curr->next; 
    } 

    // Restore the list. 
    head = reverseLL(head); 
} 

// Driver code 
int main() 
{ 
    // Create list: 1->2->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(3); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation to print the last k nodes 
// of linked list in reverse order 
import java.util.*; 
class GFG 
{ 

// Structure of a node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to reverse the linked list. 
static Node reverseLL(Node head) 
{ 
    if (head == null || head.next == null) 
        return head; 

    Node prev = null, next = null, curr = head; 

    while (curr != null) 
    { 
        next = curr.next; 
        curr.next = prev; 
        prev = curr; 
        curr = next; 
    } 
    return prev; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Reverse linked list. 
    head = reverseLL(head); 

    Node curr = head; 

    int cnt = 0; 

    // Print first k nodes of linked list. 
    while (cnt < k)  
    { 
        System.out.print(curr.data + " "); 
        cnt++; 
        curr = curr.next; 
    } 

    // Restore the list. 
    head = reverseLL(head); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation to print the last k nodes 
// of linked list in reverse order 
using System; 

class GFG 
{ 

// Structure of a node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to get a new node 
static Node getNode(int data) 
{ 
    // allocate space 
    Node newNode = new Node(); 

    // put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to reverse the linked list. 
static Node reverseLL(Node head) 
{ 
    if (head == null || head.next == null) 
        return head; 

    Node prev = null, next = null, curr = head; 

    while (curr != null) 
    { 
        next = curr.next; 
        curr.next = prev; 
        prev = curr; 
        curr = next; 
    } 
    return prev; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
static void printLastKRev(Node head, int k) 
{ 
    // if list is empty 
    if (head == null) 
        return; 

    // Reverse linked list. 
    head = reverseLL(head); 

    Node curr = head; 

    int cnt = 0; 

    // Print first k nodes of linked list. 
    while (cnt < k)  
    { 
        Console.Write(curr.data + " "); 
        cnt++; 
        curr = curr.next; 
    } 

    // Restore the list. 
    head = reverseLL(head); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Create list: 1->2->3->4->5 
    Node head = getNode(1); 
    head.next = getNode(2); 
    head.next.next = getNode(3); 
    head.next.next.next = getNode(4); 
    head.next.next.next.next = getNode(5); 

    int k = 4; 

    // print the last k nodes 
    printLastKRev(head, k); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
5 4 3 2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。