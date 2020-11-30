# 双链表中所有可被给定数`K`整除的节点的总和

> 原文：[https://www.geeksforgeeks.org/sum-of-all-nodes-in-a-doubly-linked-list-divisible-by-a-given-number-k/](https://www.geeksforgeeks.org/sum-of-all-nodes-in-a-doubly-linked-list-divisible-by-a-given-number-k/)

给定一个包含`N`个节点的双链表，并给定数字`K`。任务是找到所有可被`K`整除的节点之和。

**示例**：

```
Input: List = 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
       K = 3
Output: Sum = 30

Input: List = 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
       K = 2
Output: Sum = 20

```

**方法**：想法是遍历双链表并逐个检查节点。 如果节点的值可被`K`整除，则将该节点值添加到`sum`，否则在未到达列表末尾的情况下继续此过程。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to add 
// all nodes value which is 
// divided by any given number K 
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

// function to sum all the nodes 
// from the doubly linked 
// list that are divided by K 
int sumOfNode(Node** head_ref, int K) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 
    // variable sum=0 for add nodes value 
    int sum = 0; 
    // traves list till last node 
    while (ptr != NULL) { 
        next = ptr->next; 
        // check is node value divided by K 
        // if true then add in sum 
        if (ptr->data % K == 0) 
            sum += ptr->data; 
        ptr = next; 
    } 
    // return sum of nodes which is divided by K 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the doubly linked list 
    // 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 9); 
    push(&head, 10); 
    push(&head, 16); 
    push(&head, 15); 

    int sum = sumOfNode(&head, 3); 
    cout << "Sum = " << sum; 
} 

```

## Java

```java

// Java implementation to add 
// all nodes value which is 
// divided by any given number K 

// Node of the doubly linked list 
class Node { 
    int data; 
    Node next, prev; 

    Node(int d) { 
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

        // allocate node 
        Node newNode = new Node(data); 
        newNode.next = head; 

        // since we are adding at the beginning, 
        // prev is always NULL 
        newNode.prev = null; 

        // change prev of head node to new node 
        if (head != null) 
            head.prev = newNode; 

        // move the head to point to the new node 
        head = newNode; 

        return head; 
    } 

    // function to sum all the nodes 
    // from the doubly linked 
    // list that are divided by K 
    static int sumOfNode(Node node, int K) { 
        // variable sum=0 for add nodes value 
        int sum = 0; 
        // travese list till last node 
        while (node != null) { 
            // check is node value divided by K 
            // if true then add in sum 
            if (node.data % K == 0) 
                sum += node.data; 
            node = node.next; 
        } 
        // return sum of nodes which is divided by K 
        return sum; 
    } 

    // Driver program 
    public static void main(String[] args)  
    { 
        // start with the empty list 
        Node head = null; 

        // create the doubly linked list 
        // 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17 
        head = push(head, 17); 
        head = push(head, 7); 
        head = push(head, 6); 
        head = push(head, 9); 
        head = push(head, 10); 
        head = push(head, 16); 
        head = push(head, 15); 
        int sum = sumOfNode(head, 3); 
        System.out.println("Sum = " + sum); 
    } 
} 

// This code is contributed by Vivekkumar Singh 

```

## Python3

```py

# Python3 implementation to add 
# all nodes value which is 
# divided by any given number K 

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
    new_node =Node(0) 

    # put in the data 
    new_node.data = new_data 

    # since we are adding at the beginning, 
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

# function to sum all the nodes 
# from the doubly linked 
# list that are divided by K 
def sumOfNode(head_ref, K): 

    ptr = head_ref 
    next = None

    # variable sum=0 for add nodes value 
    sum = 0

    # traverse list till last node 
    while (ptr != None) : 
        next = ptr.next

        # check is node value divided by K 
        # if true then add in sum 
        if (ptr.data % K == 0): 
            sum += ptr.data 
        ptr = next

    # return sum of nodes which is divided by K 
    return sum

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

    sum = sumOfNode(head, 3) 
    print("Sum =", sum) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to add  
// all nodes value which is  
// divided by any given number K  
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

        // allocate node  
        Node newNode = new Node(data);  
        newNode.next = head;  

        // since we are adding at the beginning,  
        // prev is always NULL  
        newNode.prev = null;  

        // change prev of head node to new node  
        if (head != null)  
            head.prev = newNode;  

        // move the head to point to the new node  
        head = newNode;  

        return head;  
    }  

    // function to sum all the nodes  
    // from the doubly linked  
    // list that are divided by K  
    static int sumOfNode(Node node, int K) 
    {  
        // variable sum=0 for add nodes value  
        int sum = 0;  
        // travese list till last node  
        while (node != null) 
        {  
            // check is node value divided by K  
            // if true then add in sum  
            if (node.data % K == 0)  
                sum += node.data;  
            node = node.next;  
        }  
        // return sum of nodes which is divided by K  
        return sum;  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        // start with the empty list  
        Node head = null;  

        // create the doubly linked list  
        // 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17  
        head = push(head, 17);  
        head = push(head, 7);  
        head = push(head, 6);  
        head = push(head, 9);  
        head = push(head, 10);  
        head = push(head, 16);  
        head = push(head, 15);  
        int sum = sumOfNode(head, 3);  
        Console.WriteLine("Sum = " + sum);  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**输出**：

```
Sum = 30

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。