# 双链表

中所有主要节点的乘积

给定一个包含N个节点的双链表。 任务是找到所有主要节点的乘积。

**示例：**

> **输入：**列表= 15 < = > 16 < = > 6 < = > 7 < = > 17
> **输出 ：**主节点乘积：119
> 
> **输入：**列表= 5 < = > 3 < = > 4 < = > 2 < = > 9
> **输出 ：**主节点乘积：30

**方法：**

*   用链接列表的开头初始化一个指针temp，并用1初始化一个product变量。
*   使用循环开始遍历链表，直到遍历所有节点。
*   如果节点值是质数，则将当前节点的值乘以乘积，即乘积* = current_node->数据。
*   递增指向链接列表的下一个节点的指针，即temp = temp-> next。
*   退货。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to product all 
// prime nodes from the doubly 
// linked list 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the doubly linked list 
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

// Function to check if a number is prime 
bool isPrime(int n) 
{ 
    // Corner cases 
    if (n <= 1) 
        return false; 
    if (n <= 3) 
        return true; 

    // This is checked so that we can skip 
    // middle five numbers in below loop 
    if (n % 2 == 0 || n % 3 == 0) 
        return false; 

    for (int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return false; 

    return true; 
} 

// function to product all prime nodes 
// from the doubly linked list 
int prodOfPrime(Node** head_ref) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 
    // variable prod = 1 for multiplying nodes value 
    int prod = 1; 
    // travese list till last node 
    while (ptr != NULL) { 
        next = ptr->next; 
        // if number is prime then 
        // multiply to product 
        if (isPrime(ptr->data)) 
            prod = prod * ptr->data; 
        ptr = next; 
    } 

    // return product 
    return prod; 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the doubly linked list 
    // 15 <-> 16 <-> 7 <-> 6 <-> 17 
    push(&head, 17); 
    push(&head, 6); 
    push(&head, 7); 
    push(&head, 16); 
    push(&head, 15); 
    int prod = prodOfPrime(&head); 

    cout << "Product of Prime Nodes : " << prod; 

    return 0; 
} 

```

## Java

```java

// Java implementation to product all 
// prime nodes from the doubly 
// linked list 

// Node of the doubly linked list 
class Node 
{ 
    int data; 
    Node next, prev; 

    Node(int d) 
    { 
        data = d; 
        next = null; 
        prev = null; 
    } 
} 

class DLL  
{ 
    // function to insert a node at the beginning 
    // of the Doubly Linked List 
    static Node push(Node head, int data) 
    { 
        Node newNode = new Node(data); 
        newNode.next = head; 
        newNode.prev = null; 
        if (head != null) 
            head.prev = newNode; 
        head = newNode; 

        return head; 
    } 

    // Function to check if a number is prime 
    static boolean isPrime(int n) 
    { 
        // Corner cases 
        if (n <= 1) 
            return false; 
        if (n <= 3) 
            return true; 

        // This is checked so that we can skip 
        // middle five numbers in below loop 
        if (n % 2 == 0 || n % 3 == 0) 
            return false; 

        for (int i = 5; i * i <= n; i = i + 6) 
            if (n % i == 0 || n % (i + 2) == 0) 
                return false; 

        return true; 
    } 

    // function to product all prime nodes 
    // from the doubly linked list 
    static int prodOfPrime(Node node) 
    { 
        // variable prod = 1 for multiplying nodes value 
        int prod = 1; 

        // travese list till last node 
        while (node != null) 
        { 
            // check is node value is Prime 
            // if true then multiply to prod 
            if (isPrime(node.data)) 
                prod *= node.data; 
            node = node.next; 
        } 
        // return product 
        return prod; 
    } 

    // Driver Program 
    public static void main(String[] args) 
    { 
        // Start with empty list 
        Node head = null; 

        // create the doubly linked list 
        // 15 <-> 16 <-> 7 <-> 6 <-> 17 
        head = push(head, 17); 
        head = push(head, 7); 
        head = push(head, 6); 
        head = push(head, 9); 
        head = push(head, 10); 
        head = push(head, 16); 
        head = push(head, 15); 

        int prod = prodOfPrime(head); 
        System.out.println("Product of Prime Nodes: " + prod); 
    } 
} 

// This code is contributed by Vivekkumar Singh 

```

## Python3

```py

# Python3 implementation to product all 
# prime nodes from the doubly 
# linked list 

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

# Function to check if a number is prime 
def isPrime(n): 

    # Corner cases 
    if (n <= 1): 
        return False
    if (n <= 3): 
        return True

    # This is checked so that we can skip 
    # middle five numbers in below loop 
    if (n % 2 == 0 or n % 3 == 0): 
        return False
    i = 5
    while ( i * i <= n ): 
        if (n % i == 0 or n % (i + 2) == 0): 
            return False
        i += 6; 

    return True

# function to product all prime nodes 
# from the doubly linked list 
def prodOfPrime(head_ref): 

    ptr = head_ref 
    next = None

    # variable prod = 1 for multiplying nodes value 
    prod = 1

    # travese list till last node 
    while (ptr != None):  
        next = ptr.next

        # if number is prime then 
        # multiply to product 
        if (isPrime(ptr.data)): 
            prod = prod * ptr.data 
        ptr = next

    # return product 
    return prod 

# Driver Code 
if __name__ == "__main__":  

    # start with the empty list 
    head = None

    # create the doubly linked list 
    # 15 <. 16 <. 7 <. 6 <. 17 
    head = push(head, 17) 
    head = push(head, 6) 
    head = push(head, 7) 
    head = push(head, 16) 
    head = push(head, 15) 
    prod = prodOfPrime(head) 

    print("Product of Prime Nodes : ", prod) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to product all  
// prime nodes from the doubly  
// linked list  
using System; 

// Node of the doubly linked list  
public class Node  
{  
    public int data;  
    public Node next, prev;  

    public Node(int d)  
    {  
        data = d;  
        next = null;  
        prev = null;  
    }  
}  

class DLL  
{  
    // function to insert a node at the beginning  
    // of the Doubly Linked List  
    static Node push(Node head, int data)  
    {  
        Node newNode = new Node(data);  
        newNode.next = head;  
        newNode.prev = null;  
        if (head != null)  
            head.prev = newNode;  
        head = newNode;  

        return head;  
    }  

    // Function to check if a number is prime  
    static Boolean isPrime(int n)  
    {  
        // Corner cases  
        if (n <= 1)  
            return false;  
        if (n <= 3)  
            return true;  

        // This is checked so that we can skip  
        // middle five numbers in below loop  
        if (n % 2 == 0 || n % 3 == 0)  
            return false;  

        for (int i = 5; i * i <= n; i = i + 6)  
            if (n % i == 0 || n % (i + 2) == 0)  
                return false;  

        return true;  
    }  

    // function to product all prime nodes  
    // from the doubly linked list  
    static int prodOfPrime(Node node)  
    {  
        // variable prod = 1 for multiplying nodes value  
        int prod = 1;  

        // travese list till last node  
        while (node != null)  
        {  
            // check is node value is Prime  
            // if true then multiply to prod  
            if (isPrime(node.data))  
                prod *= node.data;  
            node = node.next;  
        }  
        // return product  
        return prod;  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        // Start with empty list  
        Node head = null;  

        // create the doubly linked list  
        // 15 <-> 16 <-> 7 <-> 6 <-> 17  
        head = push(head, 17);  
        head = push(head, 7);  
        head = push(head, 6);  
        head = push(head, 9);  
        head = push(head, 10);  
        head = push(head, 16);  
        head = push(head, 15);  

        int prod = prodOfPrime(head);  
        Console.WriteLine("Product of Prime Nodes: " + prod);  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Product of Prime Nodes : 119

```

**时间复杂度**：O（N），其中N是节点数。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。