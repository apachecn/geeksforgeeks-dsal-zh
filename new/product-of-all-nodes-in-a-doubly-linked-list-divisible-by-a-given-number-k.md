# 双链表中所有节点的乘积，该整数可被给定数 K 整除

> 原文：[https://www.geeksforgeeks.org/product-of-all-nodes-in-a-doubly-linked-list-divisible-by-a-given-number-k/](https://www.geeksforgeeks.org/product-of-all-nodes-in-a-doubly-linked-list-divisible-by-a-given-number-k/)

给定一个包含 N 个节点的双链表，并给定数字 K。任务是找到所有可被 K 整除的节点的乘积。

**示例**：

```
Input : List = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
        K = 3
Output : Product = 810

Input : List = 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
        K = 2
Output : Product = 384

```

这个想法是遍历双向链表并一一检查节点。 如果某个节点的值可被 K 整除，则将该节点的值乘以到目前为止的乘积，并在未到达列表末尾的情况下继续此过程。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find product of nodes in a 
// doubly linked list divisible by K 

#include <iostream> 
using namespace std; 

// Doubly linked list node 
struct Node { 
    int data; 
    Node *prev, *next; 
}; 

// function to insert a node at the beginning 
// of the Doubly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node = (Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to find the product of all the nodes from 
// the doubly linked list that is divisible by K 
int productOfNode(Node** head_ref, int K) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 

    int product = 1; 

    // Travese list till last node 
    while (ptr != NULL) { 
        next = ptr->next; 
        // check is node value divided by K 
        // if true then add in sum 
        if (ptr->data % K == 0) 
            product *= ptr->data; 
        ptr = next; 
    } 

    // Return product of nodes which 
    // are divisible by K 
    return product; 
} 

// Driver Code 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the doubly linked list 
    // 15 16 10 9 6 7 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 9); 
    push(&head, 10); 
    push(&head, 16); 
    push(&head, 15); 

    int K = 3; 

    int prod = productOfNode(&head, K); 

    cout << "Product = " << prod; 

    return 0; 
} 

```

## Java

```java

// Java program to find product of nodes in a  
// doubly linked list divisible by K  
class GFG 
{ 

// Doubly linked list node  
static class Node 
{  
    int data;  
    Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to find product of all the nodes from  
// the doubly linked list that are divisible by K  
static int productOfNode(Node head_ref, int K)  
{  
    Node ptr = head_ref;  
    Node next;  

    int product = 1;  

    // Travese list till last node  
    while (ptr != null) 
    {  
        next = ptr.next;  

        // check is node value divided by K  
        // if true then add in sum  
        if (ptr.data % K == 0)  
            product *= ptr.data;  
        ptr = next;  
    }  

    // Return product of nodes which  
    // are divisible by K  
    return product;  
}  

// Driver Code  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 15 16 10 9 6 7 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 9);  
    head = push(head, 10);  
    head = push(head, 16);  
    head = push(head, 15);  

    int K = 3;  

    int prod = productOfNode(head, K);  

    System.out.println( "Product = " + prod);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find product of nodes in a 
# doubly linked list divisible by K 

# Node of the doubly linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.prev = None
        self.next = None

# function to insert a node at the beginning 
# of the Doubly Linked List 
def push(head_ref, new_data): 

    # allocate node 
    new_node = Node(0) 

    # put in the data 
    new_node.data = new_data 

    # since we are multiplying at the beginning, 
    # prev is always None 
    new_node.prev = None

    # link the old list off the new node 
    new_node.next = (head_ref) 

    # change prev of head node to new node 
    if ((head_ref) != None): 
        (head_ref).prev = new_node 

    # move the head to point to the new node 
    (head_ref) = new_node 
    return head_ref 

# function to product all the nodes 
# from the doubly linked 
# list that are divided by K 
def productOfNode(head_ref, K): 

    ptr = head_ref 
    next = None

    # variable product=1  
    product = 1

    # traves list till last node 
    while (ptr != None) : 
        next = ptr.next

        # check is node value divided by K 
        # if true then multiply in product 
        if (ptr.data % K == 0): 
            product *= ptr.data 
        ptr = next

    # return product of nodes which is divided by K 
    return product 

# Driver Code 
if __name__ == "__main__":  

    # start with the empty list 
    head = None

    # create the doubly linked list 
    # 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17 
    head = push(head, 17) 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 9) 
    head = push(head, 10) 
    head = push(head, 16) 
    head = push(head, 15) 

    K = 3

    product = productOfNode(head, K) 
    print("product =", product) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find product of nodes in a  
// doubly linked list divisible by K  
using System; 

class GFG 
{ 

// Doubly linked list node  
public class Node 
{  
    public int data;  
    public Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to find product of all the nodes from  
// the doubly linked list that are divisible by K  
static int productOfNode(Node head_ref, int K)  
{  
    Node ptr = head_ref;  
    Node next;  

    int product = 1;  

    // Travese list till last node  
    while (ptr != null) 
    {  
        next = ptr.next;  

        // check is node value divided by K  
        // if true then add in sum  
        if (ptr.data % K == 0)  
            product *= ptr.data;  
        ptr = next;  
    }  

    // Return product of nodes which  
    // are divisible by K  
    return product;  
}  

// Driver Code  
public static void Main(String []args) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 15 16 10 9 6 7 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 9);  
    head = push(head, 10);  
    head = push(head, 16);  
    head = push(head, 15);  

    int K = 3;  

    int prod = productOfNode(head, K);  

    Console.WriteLine( "Product = " + prod);  
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Product = 810

```

**时间复杂度**：`O(n)`，其中 N 是节点数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。