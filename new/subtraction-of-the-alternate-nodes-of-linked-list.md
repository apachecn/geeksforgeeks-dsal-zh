# 减去链表

> 原文：[https://www.geeksforgeeks.org/subtraction-of-the-alternate-nodes-of-linked-list/](https://www.geeksforgeeks.org/subtraction-of-the-alternate-nodes-of-linked-list/)

的备用节点

给定一个链表。 任务是打印第一个奇数位置的节点与所有其他奇数位置的节点之和之间的差。

**示例**：

> **输入**：1-> 8-> 3-> 10-> 17-> 22-> 29-> 42
> **输出**：-48
> **备用节点**：1-> 3-> 17-> 29
> 1 –（3 + 17 + 29）= -48
> 
> **输入**：10-> 17-> 33-> 38-> 73
> **输出**：-96
> **备用节点 **：10-> 33-> 73
> 10 –（33 + 73）= -96

我们已经讨论了链表的替代节点的[总和](https://www.geeksforgeeks.org/sum-of-the-alternate-nodes-of-linked-list/)

**迭代方法**：

1.  遍历整个链表。

2.  设置差异= 0，计数= 0。

3.  当计数为偶数时，从差中减去节点的数据。

4.  访问下一个节点。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print the difference  
// of Alternate Nodes  
#include <bits/stdc++.h> 
using namespace std; 

// Link list node  
struct Node {  
    int data;  
    struct Node* next;  
};  

// Function to get the alternate  
// nodes of the linked list  
int subtractAlternateNode(struct Node* head)  
{  
    int count = 0;  
    int difference = 0;  

    while (head != NULL) {  

        // When count is even subtract the nodes  
        if (count % 2 == 0) 
            if (difference == 0){ 
                difference = head->data; 
            } 
            else{ 
                difference -= head->data;  
            }  
        // Count the nodes  
        count++;  

        // Move on the next node.  
        head = head->next;  
    }  
    return difference;  
}  

// Function to push node at head  
void push(struct Node** head_ref, int new_data)  
{  
    struct Node* new_node = new Node;  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

// Driver code  
int main()  
{  
    // Start with the empty list  
    struct Node* head = NULL;  

    // Use push() function to construct  
    // the below list 8 -> 23 -> 11 -> 29 -> 12  
    push(&head, 12);  
    push(&head, 29);  
    push(&head, 11);  
    push(&head, 23);  
    push(&head, 8);  

    cout << subtractAlternateNode(head);  
    return 0;  
} 

// This code is contributed by shubhamsingh10 

```

## C

```c

// C program to print the difference  
// of Alternate Nodes  
#include <stdio.h>  
#include <stdlib.h>  

// Link list node  
struct Node {  
    int data;  
    struct Node* next;  
};  

// Function to get the alternate   
// nodes of the linked list  
int subtractAlternateNode(struct Node* head)  
{  
    int count = 0;  
    int difference = 0;  

    while (head != NULL) {  

        // When count is even subtract the nodes  
        if (count % 2 == 0) 
            if (difference == 0){ 
                difference = head->data; 
            } 
            else{ 
                difference -= head->data;  
            }   
        // Count the nodes  
        count++;  

        // Move on the next node.  
        head = head->next;  
    }  
    return difference;  
}  

// Function to push node at head  
void push(struct Node** head_ref, int new_data)  
{  
    struct Node* new_node = (struct Node* 
              )malloc(sizeof(struct Node));  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

// Driver code  
int main()  
{  
    // Start with the empty list  
    struct Node* head = NULL;  

    // Use push() function to construct   
    // the below list 8 -> 23 -> 11 -> 29 -> 12  
    push(&head, 12);  
    push(&head, 29);  
    push(&head, 11);  
    push(&head, 23);  
    push(&head, 8);  

    printf(" %d ", subtractAlternateNode(head));  
    return 0;  
} 

```

## Java

```java

// Java program to print the difference  
// of Alternate Nodes  
import java.util.*; 

class GFG  
{ 

static Node head; 
// Link list node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to get the alternate  
// nodes of the linked list  
static int subtractAlternateNode(Node head)  
{  
    int count = 0;  
    int difference = 0;  

    while (head != null)  
    {  

        // When count is even subtract the nodes  
        if (count % 2 == 0) 
            if (difference == 0) 
            { 
                difference = head.data; 
            } 
            else
            { 
                difference -= head.data;  
            }  

        // Count the nodes  
        count++;  

        // Move on the next node.  
        head = head.next;  
    }  
    return difference;  
}  

// Function to push node at head  
static void push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    head = head_ref; 
}  

// Driver code  
public static void main(String[] args)  
{ 
    // Start with the empty list  
    head = null;  

    // Use push() function to con  
    // the below list 8 . 23 . 11 . 29 . 12  
    push(head, 12);  
    push(head, 29);  
    push(head, 11);  
    push(head, 23);  
    push(head, 8);  

    System.out.printf(" %d ", subtractAlternateNode(head)); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to print the difference  
# of Alternate Nodes  
import math  

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to get the alternate  
# nodes of the linked list  
def subtractAlternateNode(head):  
    count = 0
    difference = 0

    while (head != None) :  

        # When count is even subtract the nodes  
        if (count % 2 == 0): 
            if (difference == 0): 
                difference = head.data 

            else: 
                difference = difference - head.data  

        # Count the nodes  
        count = count + 1

        # Move on the next node.  
        head = head.next

    return difference  

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

    # Use head=push() function to construct  
    # the below list 8 . 23 . 11 . 29 . 12  
    head = push(head, 12)  
    head = push(head, 29)  
    head = push(head, 11)  
    head = push(head, 23)  
    head = push(head, 8)  

    print(subtractAlternateNode(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to print the difference  
// of Alternate Nodes  
using System; 

class GFG  
{ 

static Node head; 

// Link list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to get the alternate  
// nodes of the linked list  
static int subtractAlternateNode(Node head)  
{  
    int count = 0;  
    int difference = 0;  

    while (head != null)  
    {  

        // When count is even subtract the nodes  
        if (count % 2 == 0) 
            if (difference == 0) 
            { 
                difference = head.data; 
            } 
            else
            { 
                difference -= head.data;  
            }  

        // Count the nodes  
        count++;  

        // Move on the next node.  
        head = head.next;  
    }  
    return difference;  
}  

// Function to push node at head  
static void push(Node head_ref, 
                 int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    head = head_ref; 
}  

// Driver code  
public static void Main(String[] args)  
{ 
    // Start with the empty list  
    head = null;  

    // Use push() function to con  
    // the below list 8 . 23 . 11 . 29 . 12  
    push(head, 12);  
    push(head, 29);  
    push(head, 11);  
    push(head, 23);  
    push(head, 8);  

    Console.WriteLine(" {0} ",  
            subtractAlternateNode(head)); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

**输出**：

```
-15
```

**递归方法**：

1.  初始化静态变量（例如 flag）。

2.  如果标志为奇数，则从差中减去节点。

3.  将 head 和 flag 增加 1，然后递归到下一个节点。

下面是上述方法的实现：

## C++

```cpp

// CPP code to print difference of alternate nodes 
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
    struct Node* new_node = (struct Node*) 
                malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to find difference of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
void subtractAlternateNodes(struct Node* node, 
                 int& difference, bool isOdd = true) 
{ 
    if (node == NULL) 
        return; 

    if (isOdd == true) { 
        if (difference == 0) { 
            difference = node->data; 
        } 
        else { 
            difference = difference - (node->data); 
        } 
    } 
    subtractAlternateNodes(node->next, difference,  
                                            !isOdd); 
} 

// Driver code 
int main() 
{ 
    // Start with the empty list 
    struct Node* head = NULL; 

    // Construct below list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    int difference = 0; 

    subtractAlternateNodes(head, difference); 

    cout << difference; 

    return 0; 
} 

```

## Java

```java

// Java code to print difference of  
// alternate nodes of a linked list  
// using recursion 
class GFG  
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 
static Node head;  
static int difference; 

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
    return head; 
} 

// Function to find difference of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void subtractAlternateNodes(Node node,  
                                   boolean isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true)  
    { 
        if (difference == 0)  
        { 
            difference = node.data; 
        } 
        else
        { 
            difference = difference - (node.data); 
        } 
    } 
    subtractAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void main(String[] args)  
{ 
    // Start with the empty list 

    // Conbelow list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(head, 12); 
    push(head, 29); 
    push(head, 11); 
    push(head, 23); 
    push(head, 8); 

    difference = 0; 

    subtractAlternateNodes(head, true); 
    System.out.println(difference); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

## Python

```py

# Python code to print difference of alternate nodes 
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

difference = 0; 

# Function to find difference of alternate 
# nodes of linked list. 
# The boolean flag isOdd is used to find 
# if the current node is even or odd. 
def subtractAlternateNodes(node, isOdd ): 

    global difference 

    if (node == None): 
        return; 

    if (isOdd == True):  
        if (difference == 0) : 
            difference = node.data; 

        else : 
            difference = difference - (node.data); 

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

difference = 0; 

subtractAlternateNodes(head, True); 

print( difference); 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# code to print difference of  
// alternate nodes of a linked list  
// using recursion 
using System; 

class GFG  
{ 

// A linked list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 
static Node head;  
static int difference; 

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
    return head; 
} 

// Function to find difference of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void subtractAlternateNodes(Node node,  
                                   Boolean isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true)  
    { 
        if (difference == 0)  
        { 
            difference = node.data; 
        } 
        else
        { 
            difference = difference - (node.data); 
        } 
    } 
    subtractAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    // Start with the empty list 

    // Conbelow list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(head, 12); 
    push(head, 29); 
    push(head, 11); 
    push(head, 23); 
    push(head, 8); 

    difference = 0; 

    subtractAlternateNodes(head, true); 
    Console.WriteLine(difference); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
-15
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。