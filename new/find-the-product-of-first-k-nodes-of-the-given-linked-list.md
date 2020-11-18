# 查找给定链接列表

的前 k 个节点的乘积

给定一个指向单链表头的指针和一个整数 **k** 。 任务是找到链表中第一个 **k** 个节点的乘积。

**示例：**

> **输入：** 10-> 6-> 8-> 4-> 12，k = 2
> **输出：** 60
> 10 * 6 = 60
> 
> **输入：** 15-> 7-> 9-> 5-> 16-> 14，k = 4
> **输出：** 4725
> 15 * 7 * 9 * 5 = 4725

**方法：**设置 **prod = 1** （必需产品），并且 **count = 0** （遍历的节点数）。 现在，开始从左到右遍历链表的节点，并在每个[[ **计数< k** 。 最后打印 **prod** 的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the product of first 
// 'k' nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 
#define ll long long int 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to return the product of 
// first k nodes of the given linked list 
ll product(struct Node* head, int k) 
{ 
    if (k <= 0) 
        return 0; 

    ll prod = 1; 
    int i = 0; 
    Node* node = head; 

    // Traverse the list from left to right 
    while (i < k) { 

        // Update product 
        prod = prod * node->data; 

        // Move to the next node 
        node = node->next; 
        i++; 
    } 

    // Return the required product 
    return prod; 
} 

// Driver code 
int main() 
{ 
    struct Node* head = NULL; 

    // Linked list 10 -> 6 -> 8 -> 4 -> 12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 10); 

    int k = 2; 
    cout << product(head, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find the product of first 
// 'k' nodes of the Linked List 
class Solution 
{ 

/* A Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
} 

// Function to insert a node at the 
// beginning of the linked list 
static Node push( Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = (head_ref); 

    /* move the head to point to the new node */
    (head_ref) = new_node; 

    return head_ref; 
} 

// Function to return the product of 
// first k nodes of the given linked list 
static long product( Node head, int k) 
{ 
    if (k <= 0) 
        return 0; 

    long prod = 1; 
    int i = 0; 
    Node node = head; 

    // Traverse the list from left to right 
    while (i < k) 
    { 

        // Update product 
        prod = prod * node.data; 

        // Move to the next node 
        node = node.next; 
        i++; 
    } 

    // Return the required product 
    return prod; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node head = new Node(); 

    // Linked list 10 . 6 . 8 . 4 . 12 
    head=push(head, 12); 
    head=push(head, 4); 
    head=push(head, 8); 
    head=push(head, 6); 
    head=push(head, 10); 

    int k = 2; 
    System.out.println( product(head, k)); 

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find the product  
# of first 'k' nodes of the Linked List 
import math 

#define ll long long  

# A Linked list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = head_ref 

    # move the head to po to the new node  
    head_ref = new_node 
    return head_ref 

# Function to return the product of 
# first k nodes of the given linked list 
def product(head, k): 
    if (k <= 0): 
        return 0

    prod = 1
    i = 0
    node = head 

    # Traverse the list from left to right 
    while (i < k): 

        # Update product 
        prod = prod * node.data 

        # Move to the next node 
        node = node.next
        i = i + 1

    # Return the required product 
    return prod 

# Driver code 
if __name__=='__main__': 
    head = None

    # Linked list 10 . 6 . 8 . 4 . 12 
    head = push(head, 12); 
    head = push(head, 4); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 10); 

    k = 2
    print(product(head, k)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to find the product of first 
// 'k' nodes of the Linked List 
using System; 

class GFG 
{ 

/* A Linked list node */
class Node 
{ 
    public int data; 
    public Node next; 
} 

// Function to insert a node at the 
// beginning of the linked list 
static Node push( Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = (head_ref); 

    /* move the head to point to the new node */
    (head_ref) = new_node; 

    return head_ref; 
} 

// Function to return the product of 
// first k nodes of the given linked list 
static long product( Node head, int k) 
{ 
    if (k <= 0) 
        return 0; 

    long prod = 1; 
    int i = 0; 
    Node node = head; 

    // Traverse the list from left to right 
    while (i < k) 
    { 

        // Update product 
        prod = prod * node.data; 

        // Move to the next node 
        node = node.next; 
        i++; 
    } 

    // Return the required product 
    return prod; 
} 

// Driver code 
public static void Main() 
{ 
    Node head = new Node(); 

    // Linked list 10 . 6 . 8 . 4 . 12 
    head=push(head, 12); 
    head=push(head, 4); 
    head=push(head, 8); 
    head=push(head, 6); 
    head=push(head, 10); 

    int k = 2; 
    Console.WriteLine( product(head, k)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
60

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。