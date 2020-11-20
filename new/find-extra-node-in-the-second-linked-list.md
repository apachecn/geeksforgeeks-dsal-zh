# 在第二个链表

> 原文：[https://www.geeksforgeeks.org/find-extra-node-in-the-second-linked-list/](https://www.geeksforgeeks.org/find-extra-node-in-the-second-linked-list/)

中查找其他节点

给定两个链表 L1 和 L2。 第二个列表 L2 包含 L1 的所有节点以及 1 个额外的节点。 任务是找到那个额外的节点。

**范例**：

> **输入**：L1 = 17-> 7-> 6-> 16
> L2 = 17-> 7-> 6-> 16-> 15
> **输出**：15
> **说明**：
> 元素 15 不存在于 L1 列表中
> 
> **输入**：L1 = 10-> 15-> 5
> L2 = 10-> 100-> 15-> 5
> **输出**：100

**天真的方法**：

*   运行嵌套循环并找到 L1 中不存在的 L2 中的节点。

*   此方法的时间复杂度将为`O(N ^ 2)`，其中 N 是链​​表的长度。

**有效方法**：

*   如果将 L1 和 L2 的所有节点都进行异或运算，则 A []的每个节点在 L2 中的出现都将为 0，并且额外元素说 X 与 0 进行异或时将得到（X XOR 0）= X，这就是结果 。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the  
// extra node 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the singly linked  
// list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at  
// the beginning of the singly 
// Linked List 
void push(Node** head_ref, 
          int new_data) 
{ 
    // allocate node 
    Node* new_node =  
    (Node*)malloc(sizeof
                  (struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // link the old list off the 
    // new node 
    new_node->next = (*head_ref); 

    // move the head to point to  
    // the new node 
    (*head_ref) = new_node; 
} 

int print(Node* head_ref, 
          Node* head_ref1) 
{ 
    int ans = 0; 

    Node* ptr1 = head_ref; 
    Node* ptr2 = head_ref1; 
    // Traverse the linked list 
    while (ptr1 != NULL) { 
        ans ^= ptr1->data; 
        ptr1 = ptr1->next; 
    } 
    while (ptr2 != NULL) { 
        ans ^= ptr2->data; 
        ptr2 = ptr2->next; 
    } 
    return ans; 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head1 = NULL; 
    Node* head2 = NULL; 
    // create the linked list 
    // 15 -> 16 -> 7 -> 6 -> 17 
    push(&head1, 17); 
    push(&head1, 7); 
    push(&head1, 6); 
    push(&head1, 16); 

    // second  LL 
    push(&head2, 17); 
    push(&head2, 7); 
    push(&head2, 6); 
    push(&head2, 16); 
    push(&head1, 15); 
    int k = print(head1, head2); 
    cout << k; 
    return 0; 
} 

```

## Java

```java

// Java program to find the  
// extra node 
class GFG { 
    // Node of the singly 
    // linked list 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to insert a node at  
    // the beginning of the singly 
    // Linked List 
    static Node push(Node head_ref, 
                     int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list off 
        // the new node 
        new_node.next = (head_ref); 

        // move the head to point 
        // to the new node 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    static void extra(Node head_ref1,  
                      Node head_ref2) 
    { 
        int ans = 0; 

        Node ptr1 = head_ref1; 
        Node ptr2 = head_ref2; 

        // Traverse the linked list 
        while (ptr1 != null) { 
            ans ^= ptr1.data; 
            ptr1 = ptr1.next; 
        } 
        while (ptr2 != null) { 
            ans ^= ptr2.data; 
            ptr2 = ptr2.next; 
        } 

        System.out.println(ans); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // start with the empty list 
        Node head1 = null; 
        Node head2 = null; 
        // create the linked list 
        // 15 . 16 . 7 . 6 . 17 
        head1 = push(head1, 17); 
        head1 = push(head1, 7); 
        head1 = push(head1, 6); 
        head1 = push(head1, 16); 
        head1 = push(head1, 15); 

        // second LL 
        head2 = push(head2, 17); 
        head2 = push(head2, 7); 
        head2 = push(head2, 6); 
        head2 = push(head2, 16); 

        extra(head1, head2); 
    } 
} 

```

## Python3

```py

# Python3 program to find the  
# extra node 
class Node:   

    def __init__(self, data):   
        self.data = data   
        self.next = next

# Function to insert a node at    
# the beginning of the singly  
# Linked List   
def push( head_ref, new_data) :  

    # allocate node   
    new_node = Node(0)   

    # put in the data   
    new_node.data = new_data   

    # link the old list off  
    # the new node   
    new_node.next = (head_ref)   

    # move the head to point 
    # to the new node   
    (head_ref) = new_node  
    return head_ref  

def extra(head_ref1, head_ref2) :  

    ans = 0

    ptr1 = head_ref1   
    ptr2 = head_ref2 
    # Traverse the linked list   
    while (ptr1 != None): 
        # if current node is prime,   
        # Find sum and product   
        ans ^= ptr1.data 
        ptr1 = ptr1.next
    while(ptr2 != None): 
        ans^= ptr2.data 
        ptr2 = ptr2.next
    print(ans)   
   ## print( "Product = ", prod)   

# Driver code   

# start with the empty list   
head1 = None
head2 = None 
# create the linked list   
# 15 . 16 . 7 . 6 . 17   
head1 = push(head1, 17)   
head1 = push(head1, 7)   
head1 = push(head1, 6)   
head1 = push(head1, 16)   
head1 = push(head1, 15)   

# create the linked list  
head2 = push(head2, 17)   
head2 = push(head2, 7)   
head2 = push(head2, 6)   
head2 = push(head2, 16)   

extra(head1, head2) 

```

## C#

```cs

// C# program to find the extra node 
using System; 

class GFG{ 

// Node of the singly 
// linked list 
class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert a node at  
// the beginning of the singly 
// Linked List 
static Node push(Node head_ref, 
                 int new_data) 
{ 

    // Allocate node 
    Node new_node = new Node(); 

    // Put in the data 
    new_node.data = new_data; 

    // Link the old list off 
    // the new node 
    new_node.next = (head_ref); 

    // Move the head to point 
    // to the new node 
    (head_ref) = new_node; 

    return head_ref; 
} 

static void extra(Node head_ref1,  
                  Node head_ref2) 
{ 
    int ans = 0; 

    Node ptr1 = head_ref1; 
    Node ptr2 = head_ref2; 

    // Traverse the linked list 
    while (ptr1 != null) 
    { 
        ans ^= ptr1.data; 
        ptr1 = ptr1.next; 
    } 
    while (ptr2 != null)  
    { 
        ans ^= ptr2.data; 
        ptr2 = ptr2.next; 
    } 
    Console.WriteLine(ans); 
} 

// Driver code 
public static void Main(String []args) 
{ 

    // Start with the empty list 
    Node head1 = null; 
    Node head2 = null; 

    // Create the linked list 
    // 15 . 16 . 7 . 6 . 17 
    head1 = push(head1, 17); 
    head1 = push(head1, 7); 
    head1 = push(head1, 6); 
    head1 = push(head1, 16); 
    head1 = push(head1, 15); 

    // Second LL 
    head2 = push(head2, 17); 
    head2 = push(head2, 7); 
    head2 = push(head2, 6); 
    head2 = push(head2, 16); 

    extra(head1, head2); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
15

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。