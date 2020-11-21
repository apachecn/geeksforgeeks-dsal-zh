# 查找给定链表

> 原文：[https://www.geeksforgeeks.org/find-the-product-of-last-n-nodes-of-the-given-linked-list/](https://www.geeksforgeeks.org/find-the-product-of-last-n-nodes-of-the-given-linked-list/)

的最后 N 个节点的乘积

给定一个链表和一个数字 N。找到链表的最后 n 个节点的乘积。

**约束**：0 < = N < =链表中的节点数。

**示例**：

```
Input : List = 10->6->8->4->12, N = 2
Output : 48
Explanation : Product of last two nodes:
              12 * 4 = 48

Input : List = 15->7->9->5->16->14, N = 4
Output : 10080
Explanation : Product of last four nodes:
              9 * 5 * 16 * 14 = 10080

```

**方法 1 ：（使用用户定义的栈的迭代方法）**从左到右遍历节点。 遍历时将节点推送到用户定义的栈。 然后从栈中弹出前 n 个值，并找到其乘积。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the product of last 
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

// utility function to find the product of last 'n' nodes 
int productOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    stack<int> st; 
    int prod = 1; 

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
        prod *= st.top(); 
        st.pop(); 
    } 

    // required product 
    return prod; 
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
    cout << productOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the product  
// of last 'n' nodes of the Linked List 
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
static void push(Node head_ref,  
                int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = (head_ref); 

    /* move the head to point to the new node */
    (head_ref) = new_node; 
    head = head_ref; 
} 

// utility function to find the product  
// of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head, 
                                        int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    Stack<Integer> st = new Stack<Integer>(); 
    int prod = 1; 

    // traverses the list from left to right 
    while (head != null)  
    { 

        // push the node's data 
        // onto the stack 'st' 
        st.push(head.data); 

        // move to next node 
        head = head.next; 
    } 

    // pop 'n' nodes from 'st' and 
    // add them 
    while (n-- >0)  
    { 
        prod *= st.peek(); 
        st.pop(); 
    } 

    // required product 
    return prod; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    head = null; 

    // create linked list 10->6->8->4->12 
    push(head, 12); 
    push(head, 4); 
    push(head, 8); 
    push(head, 6); 
    push(head, 10); 

    int n = 2; 
    System.out.println(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

## Python

```py

# Python implementation to find the product  
# of last 'n' nodes of the Linked List 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

head = None

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    global head  

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 
    head = head_ref 

# utility function to find the product  
# of last 'n' nodes 
def productOfLastN_NodesUtil(head, n): 

    # if n == 0 
    if (n <= 0): 
        return 0

    st = [] 
    prod = 1

    # traverses the list from left to right 
    while (head != None) : 

        # push the node's data 
        # onto the stack 'st' 
        st.append(head.data) 

        # move to next node 
        head = head.next

    # pop 'n' nodes from 'st' and 
    # add them 
    while (n > 0) : 
        n = n - 1
        prod *= st[-1] 
        st.pop() 

    # required product 
    return prod 

# Driver Code 

head = None

# create linked list 10->6->8->4->12 
push(head, 12) 
push(head, 4) 
push(head, 8) 
push(head, 6) 
push(head, 10) 

n = 2
print(productOfLastN_NodesUtil(head, n)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to find the product  
// of last 'n' nodes of the Linked List 
using System; 

class GFG 
{ 

/* A Linked list node */
public class Node 
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

// utility function to find the product  
// of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head,  
                                    int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int prod = 1, len = 0; 
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
    while (temp != null && c-- >0) 

        // move to next node 
        temp = temp.next; 

    // now traverse the last 'n' nodes  
    // and add them 
    while (temp != null)  
    { 
        // accumulate node's data to sum 
        prod *= temp.data; 

        // move to next node 
        temp = temp.next; 
    } 

    // required product 
    return prod; 
} 

// Driver Code 
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
    Console.Write(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
48

```

**时间复杂度**：`O(n)`

**方法 2 ：（使用系统调用栈的递归方法）**递归地遍历链表直到最后。 现在，在从函数调用返回的过程中，将最后 n 个节点相乘。 乘积可以累积在通过引用传递给函数或某个全局变量的某个变量中。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the product of 
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

// Function to recursively find the product of last 
// 'n' nodes of the given linked list 
void productOfLastN_Nodes(struct Node* head, int* n, 
                          int* prod) 
{ 
    // if head = NULL 
    if (!head) 
        return; 

    // recursively traverse the remaining nodes 
    productOfLastN_Nodes(head->next, n, prod); 

    // if node count 'n' is greater than 0 
    if (*n > 0) { 

        // accumulate sum 
        *prod = *prod * head->data; 

        // reduce node count 'n' by 1 
        --*n; 
    } 
} 

// utility function to find the product of last 'n' nodes 
int productOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int prod = 1; 

    // find the sum of last 'n' nodes 
    productOfLastN_Nodes(head, &n, &prod); 

    // required product 
    return prod; 
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
    cout << productOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the product of 
// last 'n' nodes of the Linked List 

class GFG{ 

static int n, prod; 
/* A Linked list node */
static class Node { 
    int data; 
    Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data  */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Function to recursively find the product of last 
// 'n' nodes of the given linked list 
static void productOfLastN_Nodes(Node head) 
{ 
    // if head = null 
    if (head==null) 
        return; 

    // recursively traverse the remaining nodes 
    productOfLastN_Nodes(head.next); 

    // if node count 'n' is greater than 0 
    if (n > 0) { 

        // accumulate sum 
        prod = prod * head.data; 

        // reduce node count 'n' by 1 
        --n; 
    } 
} 

// utility function to find the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head) 
{ 
    // if n == 0 
    if (n <= 0) 
     return 0; 

    prod = 1; 

    // find the sum of last 'n' nodes 
    productOfLastN_Nodes(head); 

    // required product 
    return prod; 
} 

// Driver program to test above 
public static void main(String[] args) 
{ 
    Node head = null; 

 // create linked list 10->6->8->4->12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    n = 2; 
    System.out.print(productOfLastN_NodesUtil(head)); 
} 
} 

//This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python implementation to find the product of 
# last 'n' Nodes of the Linked List 

n, prod = 0, 0; 

''' A Linked list Node '''

class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = next

# function to insert a Node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    ''' allocate Node '''
    new_Node = Node(0); 

    ''' put in the data '''
    new_Node.data = new_data; 

    ''' link the old list to the new Node '''
    new_Node.next = head_ref; 

    ''' move the head to poto the new Node '''
    head_ref = new_Node; 
    return head_ref; 

# Function to recursively find the product of last 
# 'n' Nodes of the given linked list 
def productOfLastN_Nodes(head): 
    global n, prod; 

    # if head = None 
    if (head == None): 
        return; 

    # recursively traverse the remaining Nodes 
    productOfLastN_Nodes(head.next); 

    # if Node count 'n' is greater than 0 
    if (n > 0): 

        # accumulate sum 
        prod = prod * head.data; 

        # reduce Node count 'n' by 1 
        n -= 1; 

# utility function to find the product of last 'n' Nodes 
def productOfLastN_NodesUtil(head): 
    global n,prod; 

    # if n == 0 
    if (n <= 0): 
        return 0; 

    prod = 1; 

    # find the sum of last 'n' Nodes 
    productOfLastN_Nodes(head); 

    # required product 
    return prod; 

# Driver program to test above 
if __name__ == '__main__': 
    head = None; 
    n = 2; 

    # create linked list 10->6->8->4->12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    print(productOfLastN_NodesUtil(head)); 

# This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation to find the product of 
// last 'n' nodes of the Linked List 

using System; 

public class GFG{ 

static int n, prod; 
/* A Linked list node */
public class Node { 
    public int data; 
    public Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data  */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Function to recursively find the product of last 
// 'n' nodes of the given linked list 
static void productOfLastN_Nodes(Node head) 
{ 
    // if head = null 
    if (head==null) 
        return; 

    // recursively traverse the remaining nodes 
    productOfLastN_Nodes(head.next); 

    // if node count 'n' is greater than 0 
    if (n > 0) { 

        // accumulate sum 
        prod = prod * head.data; 

        // reduce node count 'n' by 1 
        --n; 
    } 
} 

// utility function to find the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head) 
{ 
    // if n == 0 
    if (n <= 0) 
     return 0; 

    prod = 1; 

    // find the sum of last 'n' nodes 
    productOfLastN_Nodes(head); 

    // required product 
    return prod; 
} 

// Driver program to test above 
public static void Main(String[] args) 
{ 
    Node head = null; 

 // create linked list 10->6->8->4->12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    n = 2; 
    Console.Write(productOfLastN_NodesUtil(head)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
48

```

**时间复杂度**：`O(n)`

**方法 3（反向链表）**：

1.  步骤如下：

2.  反转给定的链表。

3.  遍历反向链表的前 n 个节点。

4.  遍历时将它们相乘。

5.  将链表恢复为原始顺序。

6.  退货。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the product of last 
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
    struct Node *current, *prev, *next; 
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

// utility function to find the product of last 'n' nodes 
int productOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    reverseList(&head); 

    int prod = 1; 
    struct Node* current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and product them 
    while (current != NULL && n--) { 

        // accumulate node's data to 'sum' 
        prod *= current->data; 

        // move to next node 
        current = current->next; 
    } 

    // reverse back the linked list 
    reverseList(&head); 

    // required product 
    return prod; 
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
    cout << productOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the product of last 
// 'n' nodes of the Linked List 

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

static Node reverseList(Node head_ref) 
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
    return head_ref; 
} 

// utility function to find the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    head = reverseList(head); 

    int prod = 1; 
    Node current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and product them 
    while (current != null && n-- >0)  
    { 

        // accumulate node's data to 'sum' 
        prod *= current.data; 

        // move to next node 
        current = current.next; 
    } 

    // reverse back the linked list 
    head = reverseList(head); 

    // required product 
    return prod; 
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
    System.out.print(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation to find  
// the product of last 'n' nodes  
// of the Linked List 
using System; 

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
static Node push(Node head_ref,  
                 int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point  
    to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

static Node reverseList(Node head_ref) 
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
    return head_ref; 
} 

// utility function to find  
// the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    // reverse the linked list 
    head = reverseList(head); 

    int prod = 1; 
    Node current = head; 

    // traverse the 1st 'n' nodes of the reversed 
    // linked list and product them 
    while (current != null && n-- >0)  
    { 

        // accumulate node's data to 'sum' 
        prod *= current.data; 

        // move to next node 
        current = current.next; 
    } 

    // reverse back the linked list 
    head = reverseList(head); 

    // required product 
    return prod; 
} 

// Driver Code 
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
    Console.Write(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
48

```

**时间复杂度**：`O(n)`

**方法 4（使用链表的长度）**：

1.  步骤如下：

2.  计算给定链表的长度。 让它成为 len。

3.  首先从头开始遍历（len – n）节点。

4.  然后遍历其余的 n 个节点，并遍历它们的乘积。

5.  退货。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the product of last 
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

// utility function to find the product of last 'n' nodes 
int productOfLastN_NodesUtil(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int prod = 1, len = 0; 
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
        prod *= temp->data; 

        // move to next node 
        temp = temp->next; 
    } 

    // required product 
    return prod; 
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
    cout << productOfLastN_NodesUtil(head, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the product of last 
// 'n' nodes of the Linked List 
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

// utility function to find the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int prod = 1, len = 0; 
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
    while (temp != null && c-- >0) 

        // move to next node 
        temp = temp.next; 

    // now traverse the last 'n' nodes and add them 
    while (temp != null)  
    { 
        // accumulate node's data to sum 
        prod *= temp.data; 

        // move to next node 
        temp = temp.next; 
    } 

    // required product 
    return prod; 
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
    System.out.print(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# implementation to find the product of last 
// 'n' nodes of the Linked List 
using System; 

public class GFG 
{ 

/* A Linked list node */
public class Node 
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

// utility function to find the product of last 'n' nodes 
static int productOfLastN_NodesUtil(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return 0; 

    int prod = 1, len = 0; 
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
    while (temp != null && c-- >0) 

        // move to next node 
        temp = temp.next; 

    // now traverse the last 'n' nodes and add them 
    while (temp != null)  
    { 
        // accumulate node's data to sum 
        prod *= temp.data; 

        // move to next node 
        temp = temp.next; 
    } 

    // required product 
    return prod; 
} 

// Driver program to test above 
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
    Console.Write(productOfLastN_NodesUtil(head, n)); 
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
48

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。