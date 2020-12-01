# 链表节点的交替总和

> 原文：[https://www.geeksforgeeks.org/sum-of-the-alternate-nodes-of-linked-list/](https://www.geeksforgeeks.org/sum-of-the-alternate-nodes-of-linked-list/)

给定一个链表，任务是打印链表节点的交替总和。

**示例**：

```
Input : 1 -> 8 -> 3 -> 10 -> 17 -> 22 -> 29 -> 42
Output : 50
Alternate nodes : 1 -> 3 -> 17 -> 29

Input : 10 -> 17 -> 33 -> 38 -> 73
Output : 116
Alternate nodes : 10 -> 33 -> 73

```

**迭代方法**：

1.  遍历整个链表。

2.  设置总和为 0 且计数为 0。

3.  计数为偶数时，将节点的数据相加。

4.  访问下一个节点。

以下是此方法的实现：

## C++

```cpp

// C++ code to print the sum of Alternate Nodes  
#include <iostream> 
using namespace std; 

/* Link list node */
struct Node 
{  
    int data;  
    struct Node* next;  
};  

/* Function to get the alternate  
nodes of the linked list */
int sumAlternateNode(struct Node* head)  
{  
    int count = 0;  
    int sum = 0;  

    while (head != NULL)  
    {  

        // when count is even sum the nodes  
        if (count % 2 == 0)  
            sum += head->data;  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head->next;  
    }  
    return sum;  
}  

// Function to push node at head  
void push(struct Node** head_ref, int new_data)  
{  
    struct Node* new_node =  
            (struct Node*)malloc(sizeof(struct Node));  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

// Driver code  
int main()  
{  
    /* Start with the empty list */
    struct Node* head = NULL;  

    /* Use push() function to construct  
    the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12);  
    push(&head, 29);  
    push(&head, 11);  
    push(&head, 23);  
    push(&head, 8);  

    cout << sumAlternateNode(head);  
    return 0;  
}  

// This code is contributed by SHUBHAMSINGH10 

```

## C

```c

// C code to print the sum of Alternate Nodes 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the alternate  
   nodes of the linked list */
int sumAlternateNode(struct Node* head) 
{ 
    int count = 0; 
    int sum = 0; 

    while (head != NULL) { 

        // when count is even sum the nodes 
        if (count % 2 == 0) 
            sum += head->data; 

        // count the nodes 
        count++; 

        // move on the next node. 
        head = head->next; 
    } 
    return sum; 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() function to construct  
       the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    printf(" %d ", sumAlternateNode(head)); 
    return 0; 
} 

```

## Java

```java

// Java code to print the sum of Alternate Nodes  
class GFG 
{ 

/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static int sumAlternateNode( Node head)  
{  
    int count = 0;  
    int sum = 0;  

    while (head != null)  
    {  

        // when count is even sum the nodes  
        if (count % 2 == 0)  
            sum += head.data;  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
    return sum;  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node =new Node(); 
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Driver code  
public static void main(String args[]) 
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    System.out.printf(" %d ", sumAlternateNode(head));  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 code to print the 
# sum of Alternate Nodes 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to get the alternate  
# nodes of the linked list  
def sumAlternateNode(head): 
    count = 0
    sum = 0

    while (head != None): 

        # when count is even sum the nodes 
        if (count % 2 == 0): 
            sum = sum + head.data 

        # count the nodes 
        count = count + 1

        # move on the next node. 
        head = head.next

    return sum

# Function to push node at head 
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Driver code 
if __name__=='__main__':  

    # Start with the empty list  
    head = None

    # Use push() function to construct  
    # the below list 8 . 23 . 11 . 29 . 12  
    head = push(head, 12)  
    head = push(head, 29)  
    head = push(head, 11)  
    head = push(head, 23)  
    head = push(head, 8)  

    print(sumAlternateNode(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# code to print the sum of Alternate Nodes  
using System; 

class GFG  
{  

/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static int sumAlternateNode( Node head)  
{  
    int count = 0;  
    int sum = 0;  

    while (head != null)  
    {  

        // when count is even sum the nodes  
        if (count % 2 == 0)  
            sum += head.data;  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
    return sum;  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node =new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Driver code  
public static void Main(String []args)  
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    Console.Write(" {0} ", sumAlternateNode(head));  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
31

```

**递归方法**：

1.  初始化静态变量（例如`flag`）。

2.  如果`flag`为奇数，则将节点与`sum`相加。

3.  将`head`和`flag`增加 1，然后递归到下一个节点。

以下是此方法的实现：

## C++

```cpp

// CPP code to print sum of alternate nodes 
// of a linked list using recursion 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Inserting node at the beginning 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to find sum of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
void productAlternateNodes(struct Node* node, 
                           int& sum, bool isOdd = true) 
{ 
    if (node == NULL) 
        return; 

    if (isOdd == true) 
        sum = sum + (node->data); 

    productAlternateNodes(node->next, sum, !isOdd); 
} 

// Driver code 
int main() 
{ 
    // Start with the empty list 
    struct Node* head = NULL; 

    // construct below list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    int sum = 0; 

    productAlternateNodes(head, sum); 

    cout << sum; 

    return 0; 
} 

```

## Java

```java

// Java code to print sum of alternate nodes 
// of a linked list using recursion 

class GFG  
{ 

// Start with the empty list  
static Node head=null;  

static int sum; 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head=head_ref; 
} 

// Function to find sum of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void productAlternateNodes(Node node, boolean isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true) 
        sum = sum + (node.data); 

    productAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void main(String[] args)  
{ 
    // conbelow list 
    // 8 . 23 . 11 . 29 . 12 

    push(head, 12); 
    push(head, 29); 
    push(head, 11); 
    push(head, 23); 
    push(head, 8); 

    sum = 0; 

    productAlternateNodes(head,true); 

    System.out.println(sum); 
} 
} 

/* This code is contributed by PrinciRaj1992 */

```

## Python

```py

# Python code to print sum of alternate nodes 
# of a linked list using recursion 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 

    return head_ref 

sum = 0; 

# Function to find sum of alternate 
# nodes of linked list. 
# The boolean flag isOdd is used to find 
# if the current node is even or odd. 
def subtractAlternateNodes(node, isOdd ): 

    global sum

    if (node == None): 
        return; 

    if (isOdd == True):  
        if (sum == 0) : 
            sum = node.data; 

        else : 
            sum = sum + (node.data); 

    subtractAlternateNodes(node.next, not isOdd); 

# Driver code 

# Start with the empty list 
head = None; 

# Construct below list 
# 8 -> 23 -> 11 -> 29 -> 12 

head = push(head, 12); 
head = push(head, 29); 
head = push(head, 11); 
head = push(head, 23); 
head = push(head, 8); 

sum = 0; 

subtractAlternateNodes(head, True); 

print( sum); 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# code to print sum of alternate nodes 
// of a linked list using recursion 
using System;  

class GFG  
{ 

// Start with the empty list  
static Node head = null;  

static int sum; 

// A linked list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head=head_ref; 
} 

// Function to find sum of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void productAlternateNodes(Node node, bool isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true) 
        sum = sum + (node.data); 

    productAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    // conbelow list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(head, 12); 
    push(head, 29); 
    push(head, 11); 
    push(head, 23); 
    push(head, 8); 

    sum = 0; 

    productAlternateNodes(head,true); 

    Console.WriteLine(sum); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
31

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。