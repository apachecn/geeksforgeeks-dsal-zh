# 查找给定链接列表

的后 n 个节点的总和

给定一个链表和一个数字 **n** 。 找到链表的最后 **n** 个节点的总和。

**约束：** 0 < = **n** < =链表中的节点数。

**示例：**

```
Input : 10->6->8->4->12, n = 2
Output : 16
Sum of last two nodes:
12 + 4 = 16

Input : 15->7->9->5->16->14, n = 4
Output : 44

```

**方法 1 ：（使用系统调用堆栈的递归方法）**
递归遍历链表直到最后。 现在，在从函数调用返回的过程中，将最后 **n 个**节点加起来。 总和可以累积在通过引用传递给该函数的某个变量或某个全局变量中。

## C++

```cpp

// C++ implementation to find the sum of 
// last 'n' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// function to recursively find the sum of last 
// 'n' nodes of the given linked list 
void sumOfLastN_Nodes(struct Node* head, int* n, 
                                      int* sum) 
{ 
    // if head = NULL 
    if (!head) 
        return; 

    // recursively traverse the remaining nodes 
    sumOfLastN_Nodes(head->next, n, sum); 

    // if node count 'n' is greater than 0 
    if (*n > 0) { 

        // accumulate sum 
        *sum = *sum + head->data; 

        // reduce node count 'n' by 1 
        --*n; 
    } 
} 

// utility function to find the sum of last 'n' nodes 
int sumOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int sum = 0; 

    // find the sum of last 'n' nodes 
    sumOfLastN_Nodes(head, &n, &sum); 

    // required sum 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int n = 2; 
    cout << "Sum of last " << n << " nodes = "
         << sumOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of 
// last 'n' nodes of the Linked List 
import java.util.*; 

class GFG 
{ 

/* A Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head;  
static int n, sum; 

// function to insert a node at the 
// beginning of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

// function to recursively find the sum of last 
// 'n' nodes of the given linked list 
static void sumOfLastN_Nodes(Node head) 
{ 
    // if head = NULL 
    if (head == null) 
        return; 

    // recursively traverse the remaining nodes 
    sumOfLastN_Nodes(head.next); 

    // if node count 'n' is greater than 0 
    if (n > 0)  
    { 

        // accumulate sum 
        sum = sum + head.data; 

        // reduce node count 'n' by 1 
        --n; 
    } 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    sum = 0; 

    // find the sum of last 'n' nodes 
    sumOfLastN_Nodes(head); 

    // required sum 
    return sum; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    head = null; 

    // create linked list 10.6.8.4.12 
    push(head, 12); 
    push(head, 4); 
    push(head, 8); 
    push(head, 6); 
    push(head, 10); 

    n = 2; 
    System.out.print("Sum of last " + n +  
                     " nodes = " +  
                     sumOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation to find the sum of 
# last 'n' nodes of the Linked List 

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

head = None
n = 0
sum = 0

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 
    global head 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = head_ref 

    # move the head to point to the new node  
    head_ref = new_node 
    head = head_ref 

# function to recursively find the sum of last 
# 'n' nodes of the given linked list 
def sumOfLastN_Nodes(head): 

    global sum
    global n 

    # if head = None 
    if (head == None): 
        return

    # recursively traverse the remaining nodes 
    sumOfLastN_Nodes(head.next) 

    # if node count 'n' is greater than 0 
    if (n > 0) : 

        # accumulate sum 
        sum = sum + head.data 

        # reduce node count 'n' by 1 
        n = n - 1

# utility function to find the sum of last 'n' nodes 
def sumOfLastN_NodesUtil(head, n): 

    global sum

    # if n == 0 
    if (n <= 0): 
        return 0

    sum = 0

    # find the sum of last 'n' nodes 
    sumOfLastN_Nodes(head) 

    # required sum 
    return sum

# Driver Code 
head = None

# create linked list 10.6.8.4.12 
push(head, 12) 
push(head, 4) 
push(head, 8) 
push(head, 6) 
push(head, 10) 

n = 2
print("Sum of last " , n ,  
    " nodes = ", sumOfLastN_NodesUtil(head, n)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to find the sum of 
// last 'n' nodes of the Linked List 
using System; 

class GFG 
{ 

/* A Linked list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head;  
static int n, sum; 

// function to insert a node at the 
// beginning of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

// function to recursively find the sum of last 
// 'n' nodes of the given linked list 
static void sumOfLastN_Nodes(Node head) 
{ 
    // if head = NULL 
    if (head == null) 
        return; 

    // recursively traverse the remaining nodes 
    sumOfLastN_Nodes(head.next); 

    // if node count 'n' is greater than 0 
    if (n > 0)  
    { 

        // accumulate sum 
        sum = sum + head.data; 

        // reduce node count 'n' by 1 
        --n; 
    } 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    sum = 0; 

    // find the sum of last 'n' nodes 
    sumOfLastN_Nodes(head); 

    // required sum 
    return sum; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    head = null; 

    // create linked list 10.6.8.4.12 
    push(head, 12); 
    push(head, 4); 
    push(head, 8); 
    push(head, 6); 
    push(head, 10); 

    n = 2; 
    Console.Write("Sum of last " + n +  
                  " nodes = " +  
                  sumOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
Sum of last 2 nodes = 16

```

**时间复杂度：** O（n），其中 n 是链表中节点的数量。
**辅助空间：** O（n）（如果正在考虑系统调用堆栈）。

**方法 2（使用用户定义堆栈的迭代方法）**
这是对**此**中**方法 1** 解释的递归方法的迭代过程。 从左到右遍历节点。 遍历时将节点推送到用户定义的堆栈。 然后从堆栈中弹出顶部的 **n** 个值并将其添加。

## C++

```cpp

// C++ implementation to find the sum of last 
// 'n' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// utility function to find the sum of last 'n' nodes 
int sumOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    stack<int> st; 
    int sum = 0; 

    // traverses the list from left to right 
    while (head != NULL) { 

        // push the node's data onto the stack 'st' 
        st.push(head->data); 

        // move to next node 
        head = head->next; 
    } 

    // pop 'n' nodes from 'st' and 
    // add them 
    while (n--) { 
        sum += st.top(); 
        st.pop(); 
    } 

    // required sum 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int n = 2; 
    cout << "Sum of last " << n << " nodes = "
         << sumOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of last 
// 'n' nodes of the Linked List 
import java.util.*; 

class GFG 
{ 

/* A Linked list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    Stack<Integer> st = new Stack<Integer>(); 
    int sum = 0; 

    // traverses the list from left to right 
    while (head != null)  
    { 

        // push the node's data onto the stack 'st' 
        st.push(head.data); 

        // move to next node 
        head = head.next; 
    } 

    // pop 'n' nodes from 'st' and 
    // add them 
    while (n-- >0) 
    { 
        sum += st.peek(); 
        st.pop(); 
    } 

    // required sum 
    return sum; 
} 

// Driver program to test above 
public static void main(String[] args) 
{ 
    Node head = null; 

    // create linked list 10.6.8.4.12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    int n = 2; 
    System.out.print("Sum of last " + n+ " nodes = "
        + sumOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation to find the sum of  
# last 'n' nodes of the Linked List  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

head = None
n = 0
sum = 0

# function to insert a node at the  
# beginning of the linked list  
def push(head_ref, new_data):  
    global head  

    # allocate node  
    new_node = Node(0)  

    # put in the data  
    new_node.data = new_data  

    # link the old list to the new node  
    new_node.next = head_ref  

    # move the head to point to the new node  
    head_ref = new_node  
    head = head_ref  

# utility function to find the sum of last 'n' nodes  
def sumOfLastN_NodesUtil(head, n): 

    global sum

    # if n == 0  
    if (n <= 0): 
        return 0

    st = [] 
    sum = 0

    # traverses the list from left to right  
    while (head != None): 

        # push the node's data onto the stack 'st'  
        st.append(head.data)  

        # move to next node  
        head = head.next

    # pop 'n' nodes from 'st' and  
    # add them  
    while (n): 
        n -= 1
        sum += st[0] 
        st.pop(0)  

    # required sum  
    return sum

# Driver Code  
head = None

# create linked list 10.6.8.4.12  
push(head, 12)  
push(head, 4)  
push(head, 8)  
push(head, 6)  
push(head, 10)  

n = 2
print("Sum of last" , n ,  
    "nodes =", sumOfLastN_NodesUtil(head, n))  

# This code is contributed by shubhamsingh10  

```

## C#

```cs

// C# implementation to find the sum of last 
// 'n' nodes of the Linked List 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

/* A Linked list node */
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    Stack<int> st = new Stack<int>(); 
    int sum = 0; 

    // traverses the list from left to right 
    while (head != null)  
    { 

        // push the node's data onto the stack 'st' 
        st.Push(head.data); 

        // move to next node 
        head = head.next; 
    } 

    // pop 'n' nodes from 'st' and 
    //.Add them 
    while (n-- >0) 
    { 
        sum += st.Peek(); 
        st.Pop(); 
    } 

    // required sum 
    return sum; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node head = null; 

    // create linked list 10.6.8.4.12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    int n = 2; 
    Console.Write("Sum of last " + n+ " nodes = "
        + sumOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出：**

```
Sum of last 2 nodes = 16

```

**时间复杂度：** O（n），其中 n 是链表中节点的数量。
**辅助空间：** O（n），堆栈大小

**方法 3（反向链接列表）**
以下是步骤：

1.  反转给定的链表。
2.  遍历反向链表的前 **n 个**节点。
3.  遍历时添加它们。
4.  将链接列表恢复为原始顺序。
5.  返回相加的总和。

## C++

```cpp

// C++ implementation to find the sum of last 
// 'n' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

void reverseList(struct Node** head_ref) 
{ 
    struct Node* current, *prev, *next; 
    current = *head_ref; 
    prev = NULL; 

    while (current != NULL) { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 

    *head_ref = prev; 
} 

// utility function to find the sum of last 'n' nodes 
int sumOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    reverseList(&head); 

    int sum = 0; 
    struct Node* current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and add them 
    while (current != NULL && n--) {                    

        // accumulate node's data to 'sum' 
        sum += current->data; 

        // move to next node 
        current = current->next; 
    } 

    // reverse back the linked list 
    reverseList(&head); 

    // required sum 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int n = 2; 
    cout << "Sum of last " << n << " nodes = "
         << sumOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of last 
// 'n' nodes of the Linked List 
import java.util.*; 

class GFG  
{ 

/* A Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head;  

// function to insert a node at the 
// beginning of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head=head_ref; 
} 

static void reverseList(Node head_ref) 
{ 
    Node current, prev, next; 
    current = head_ref; 
    prev = null; 

    while (current != null)  
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    } 

    head_ref = prev; 
    head = head_ref; 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    reverseList(head); 

    int sum = 0; 
    Node current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and add them 
    while (current != null && n-- >0)  
    {                  

        // accumulate node's data to 'sum' 
        sum += current.data; 

        // move to next node 
        current = current.next; 
    } 

    // reverse back the linked list 
    reverseList(head); 

    // required sum 
    return sum; 
} 

// Driver code 
public static void main(String[] args)  
{ 

    // create linked list 10.6.8.4.12 
    push(head, 12); 
    push(head, 4); 
    push(head, 8); 
    push(head, 6); 
    push(head, 10); 

    int n = 2; 
    System.out.println("Sum of last " + n + " nodes = "
        + sumOfLastN_NodesUtil(n)); 
} 
} 

/* This code is contributed by PrinciRaj1992 */

```

## C#

```cs

// C# implementation to find the sum of last 
// 'n' nodes of the Linked List 
using System;  

class GFG  
{ 

/* A Linked list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head;  

// function to insert a node at the 
// beginning of the linked list 
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head=head_ref; 
} 

static void reverseList(Node head_ref) 
{ 
    Node current, prev, next; 
    current = head_ref; 
    prev = null; 

    while (current != null)  
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    } 

    head_ref = prev; 
    head = head_ref; 
} 

// utility function to find the sum of last 'n' nodes 
static int sumOfLastN_NodesUtil(int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    reverseList(head); 

    int sum = 0; 
    Node current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and add them 
    while (current != null && n-- >0)  
    {                  

        // accumulate node's data to 'sum' 
        sum += current.data; 

        // move to next node 
        current = current.next; 
    } 

    // reverse back the linked list 
    reverseList(head); 

    // required sum 
    return sum; 
} 

// Driver code 
public static void Main(String[] args)  
{ 

    // create linked list 10->6->8->4->12 
    push(head, 12); 
    push(head, 4); 
    push(head, 8); 
    push(head, 6); 
    push(head, 10); 

    int n = 2; 
    Console.WriteLine("Sum of last " + n + " nodes = "
        + sumOfLastN_NodesUtil(n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
Sum of last 2 nodes = 16

```

**时间复杂度：** O（n），其中 n 是链表中节点的数量。
**辅助空间：** O（1）

**方法 4（使用链表的长度）**
以下是步骤：

1.  计算给定链接列表的长度。 设为 **len** 。
2.  首先从头开始遍历**（len – n）**节点。
3.  然后遍历其余的 **n 个**节点，并在遍历时将它们添加。
4.  返回相加的总和。

## C++

```cpp

// C++ implementation to find the sum of last 
// 'n' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// utility function to find the sum of last 'n' nodes 
int sumOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int sum = 0, len = 0; 
    struct Node* temp = head; 

    // calculate the length of the linked list 
    while (temp != NULL) { 
        len++; 
        temp = temp->next; 
    } 

    // count of first (len - n) nodes 
    int c = len - n; 
    temp = head; 

    // just traverse the 1st 'c' nodes 
    while (temp != NULL && c--)                     
        // move to next node 
        temp = temp->next; 

    // now traverse the last 'n' nodes and add them 
    while (temp != NULL) { 

        // accumulate node's data to sum 
        sum += temp->data; 

        // move to next node 
        temp = temp->next; 
    } 

    // required sum 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int n = 2; 
    cout << "Sum of last " << n << " nodes = "
         << sumOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of last  
// 'n' nodes of the Linked List  

class GFG  
{ 

/* A Linked list node */
static class Node 
{  
    int data;  
    Node next;  
};  
static Node head; 

// function to insert a node at the  
// beginning of the linked list  
static void push(Node head_ref, int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list to the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node;  
        head = head_ref; 
}  

// utility function to find the sum of last 'n' nodes  
static int sumOfLastN_NodesUtil(Node head, int n)  
{  
    // if n == 0  
    if (n <= 0)  
        return 0;  

    int sum = 0, len = 0;  
    Node temp = head;  

    // calculate the length of the linked list  
    while (temp != null) 
    {  
        len++;  
        temp = temp.next;  
    }  

    // count of first (len - n) nodes  
    int c = len - n;  
    temp = head;  

    // just traverse the 1st 'c' nodes  
    while (temp != null&&c-- >0) 
    {                      
        // move to next node  
        temp = temp.next;  
    } 

    // now traverse the last 'n' nodes and add them  
    while (temp != null)  
    {  

        // accumulate node's data to sum  
        sum += temp.data;  

        // move to next node  
        temp = temp.next;  
    }  

    // required sum  
    return sum;  
}  

// Driver code  
public static void main(String[] args) 
{ 

    // create linked list 10.6.8.4.12  
    push(head, 12);  
    push(head, 4);  
    push(head, 8);  
    push(head, 6);  
    push(head, 10);  

    int n = 2;  
    System.out.println("Sum of last " + n + " nodes = "
        + sumOfLastN_NodesUtil(head, n));  
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation to find the sum of last  
// 'n' nodes of the Linked List  
using System; 

class GFG  
{ 

/* A Linked list node */
public class Node 
{  
    public int data;  
    public Node next;  
};  
static Node head; 

// function to insert a node at the  
// beginning of the linked list  
static void push(Node head_ref, int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list to the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node;  
        head = head_ref; 
}  

// utility function to find the sum of last 'n' nodes  
static int sumOfLastN_NodesUtil(Node head, int n)  
{  
    // if n == 0  
    if (n <= 0)  
        return 0;  

    int sum = 0, len = 0;  
    Node temp = head;  

    // calculate the length of the linked list  
    while (temp != null) 
    {  
        len++;  
        temp = temp.next;  
    }  

    // count of first (len - n) nodes  
    int c = len - n;  
    temp = head;  

    // just traverse the 1st 'c' nodes  
    while (temp != null&&c-- >0) 
    {                      
        // move to next node  
        temp = temp.next;  
    } 

    // now traverse the last 'n' nodes and add them  
    while (temp != null)  
    {  

        // accumulate node's data to sum  
        sum += temp.data;  

        // move to next node  
        temp = temp.next;  
    }  

    // required sum  
    return sum;  
}  

// Driver code  
public static void Main(String[] args) 
{ 

    // create linked list 10.6.8.4.12  
    push(head, 12);  
    push(head, 4);  
    push(head, 8);  
    push(head, 6);  
    push(head, 10);  

    int n = 2;  
    Console.WriteLine("Sum of last " + n + " nodes = "
        + sumOfLastN_NodesUtil(head, n));  
} 
} 

// This code is contributed by Princi Singh 

```

**输出：**

```
Sum of last 2 nodes = 16

```

**时间复杂度：** O（n），其中 n 是链表中节点的数量。
**辅助空间：** O（1）

**方法 5（使用两个指针需要单遍历）**
维护两个指针–参考指针和主指针。 初始化引用和主指向 head 的指针。 首先将参考指针从头移到**个**节点，然后将累积的节点数据遍历到某个变量，例如 **sum** 。 现在，同时移动两个指针，直到参考指针到达列表的末尾，并在遍历时将所有节点的数据累加到**和由参考指针指向的**并将所有节点的数据累加到某个变量，例如 **temp [** ，由主指针指向。 现在，**（总和-温度）**是最后 **n 个**节点的必需总和。

## C++

```cpp

// C++ implementation to find the sum of last 
// 'n' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// utility function to find the sum of last 'n' nodes 
int sumOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int sum = 0, temp = 0; 
    struct Node* ref_ptr, *main_ptr; 
    ref_ptr = main_ptr = head; 

    // traverse 1st 'n' nodes through 'ref_ptr' and 
    // accumulate all node's data to 'sum' 
    while (ref_ptr != NULL &&  n--) {                    
        sum += ref_ptr->data; 

        // move to next node 
        ref_ptr = ref_ptr->next; 
    } 

    // traverse to the end of the linked list 
    while (ref_ptr != NULL) { 

        // accumulate all node's data to 'temp' pointed 
        // by the 'main_ptr' 
        temp += main_ptr->data; 

        // accumulate all node's data to 'sum' pointed by 
        // the 'ref_ptr' 
        sum += ref_ptr->data; 

        // move both the pointers to their respective 
        // next nodes 
        main_ptr = main_ptr->next; 
        ref_ptr = ref_ptr->next; 
    } 

    // required sum 
    return (sum - temp); 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 10->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int n = 2; 
    cout << "Sum of last " << n << " nodes = "
         << sumOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of last 
// 'n' nodes of the Linked List 
class GfG 
{ 

    // Defining structure 
    static class Node 
    { 
        int data; 
        Node next; 
    } 

    static Node head; 

    static void printList(Node start) 
    { 
        Node temp = start; 
        while (temp != null) 
        { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    // Push function 
    static void push(Node start, int info) 
    { 
        // Allocating node 
        Node node = new Node(); 

        // Info into node 
        node.data = info; 

        // Next of new node to head 
        node.next = start; 

        // head points to new node 
        head = node; 
    } 

    private static int sumOfLastN_NodesUtil(Node head, int n) 
    { 
        // if n == 0 
        if (n <= 0) 
            return 0; 

        int sum = 0, temp = 0; 
        Node ref_ptr, main_ptr; 
        ref_ptr = main_ptr = head; 

        // traverse 1st 'n' nodes through 'ref_ptr' and 
        // accumulate all node's data to 'sum' 
        while (ref_ptr != null && (n--) > 0) 
        { 
            sum += ref_ptr.data; 

            // move to next node 
            ref_ptr = ref_ptr.next; 
        } 

        // traverse to the end of the linked list 
        while (ref_ptr != null) 
        { 

            // accumulate all node's data to 'temp' pointed 
            // by the 'main_ptr' 
            temp += main_ptr.data; 

            // accumulate all node's data to 'sum' pointed by 
            // the 'ref_ptr' 
            sum += ref_ptr.data; 

            // move both the pointers to their respective 
            // next nodes 
            main_ptr = main_ptr.next; 
            ref_ptr = ref_ptr.next; 
        } 

        // required sum 
        return (sum - temp); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        head = null; 

        // Adding elements to Linked List 
        push(head, 12); 
        push(head, 4); 
        push(head, 8); 
        push(head, 6); 
        push(head, 10); 

        printList(head); 

        int n = 2; 

        System.out.println("Sum of last " + n +  
                    " nodes = " + sumOfLastN_NodesUtil(head, n)); 
    } 
} 

// This code is contributed by shubham96301 

```

## C#

```cs

// C# implementation to find the sum of last  
// 'n' nodes of the Linked List  
using System; 

class GfG  
{  

    // Defining structure  
    public class Node  
    {  
        public int data;  
        public Node next;  
    }  

    static Node head;  

    static void printList(Node start)  
    {  
        Node temp = start;  
        while (temp != null)  
        {  
            Console.Write(temp.data + " ");  
            temp = temp.next;  
        }  
        Console.WriteLine();  
    }  

    // Push function  
    static void push(Node start, int info)  
    {  
        // Allocating node  
        Node node = new Node();  

        // Info into node  
        node.data = info;  

        // Next of new node to head  
        node.next = start;  

        // head points to new node  
        head = node;  
    }  

    private static int sumOfLastN_NodesUtil(Node head, int n)  
    {  
        // if n == 0  
        if (n <= 0)  
            return 0;  

        int sum = 0, temp = 0;  
        Node ref_ptr, main_ptr;  
        ref_ptr = main_ptr = head;  

        // traverse 1st 'n' nodes through 'ref_ptr' and  
        // accumulate all node's data to 'sum'  
        while (ref_ptr != null && (n--) > 0)  
        {  
            sum += ref_ptr.data;  

            // move to next node  
            ref_ptr = ref_ptr.next;  
        }  

        // traverse to the end of the linked list  
        while (ref_ptr != null)  
        {  

            // accumulate all node's data to 'temp' pointed  
            // by the 'main_ptr'  
            temp += main_ptr.data;  

            // accumulate all node's data to 'sum' pointed by  
            // the 'ref_ptr'  
            sum += ref_ptr.data;  

            // move both the pointers to their respective  
            // next nodes  
            main_ptr = main_ptr.next;  
            ref_ptr = ref_ptr.next;  
        }  

        // required sum  
        return (sum - temp);  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  
        head = null;  

        // Adding elements to Linked List  
        push(head, 12);  
        push(head, 4);  
        push(head, 8);  
        push(head, 6);  
        push(head, 10);  

        printList(head);  

        int n = 2;  

        Console.WriteLine("Sum of last " + n +  
                    " nodes = " + sumOfLastN_NodesUtil(head, n));  
    }  
}  

// This code contributed by Rajput-Ji 

```

**输出：**

```
Sum of last 2 nodes = 16

```

**时间复杂度：** O（n），其中 n 是链表中节点的数量。
**辅助空间：** O（1）

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

