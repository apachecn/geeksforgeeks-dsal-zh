# 使用递归交替打印链表节点

> 原文：[https://www.geeksforgeeks.org/print-alternate-nodes-linked-list-using-recursion/](https://www.geeksforgeeks.org/print-alternate-nodes-linked-list-using-recursion/)

给定一个链表，请交替打印此链表节点。

**示例**：

```
Input : 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10
Output : 1 -> 3 -> 5 -> 7 -> 9 

Input : 10 -> 9
Output : 10

```

**递归方法**：

1.  初始化静态变量（例如标记）

2.  如果标记为奇数，则打印节点

3.  将头和标记加 1，然后递归返回下一个 节点。

## C++

```cpp

// CPP code to print alternate nodes 
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
    struct Node* new_node =  
       (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to print alternate nodes of linked list. 
// The boolean flag isOdd is used to find if the current 
// node is even or odd. 
void printAlternate(struct Node* node, bool isOdd=true) 
{ 
    if (node == NULL) 
       return; 
    if (isOdd == true) 
        cout << node->data << " ";  
    printAlternate(node->next, !isOdd); 
} 

// Driver code 
int main() 
{ 
    // Start with the empty list 
    struct Node* head = NULL; 

    // construct below list 
    // 1->2->3->4->5->6->7->8->9->10 

    push(&head, 10); 
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    printAlternate(head); 

    return 0; 
} 

```

## Java

```java

// Java code to print alternate nodes  
// of a linked list using recursion  
class GFG  
{ 

// A linked list node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Inserting node at the beginning  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print alternate nodes of linked list.  
// The boolean flag isOdd is used to find if the current  
// node is even or odd.  
static void printAlternate( Node node, boolean isOdd)  
{  
    if (node == null)  
    return;  
    if (isOdd == true)  
        System.out.print( node.data + " ");  
    printAlternate(node.next, !isOdd);  
}  

// Driver code  
public static void main(String args[]) 
{  
    // Start with the empty list  
    Node head = null;  

    // con below list  
    // 1.2.3.4.5.6.7.8.9.10  

    head = push(head, 10);  
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    printAlternate(head,true);  

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 code to print alternate nodes  
# of a linked list using recursion  

# A linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Inserting node at the beginning  
def push( head_ref, new_data): 

    new_node = Node(new_data); 
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    return head_ref;  

# Function to print alternate nodes of  
# linked list. The boolean flag isOdd  
# is used to find if the current node 
# is even or odd.  
def printAlternate( node, isOdd): 
    if (node == None): 
        return;  
    if (isOdd == True): 
        print( node.data, end = " ");  
    if (isOdd == True): 
        isOdd = False; 
    else: 
        isOdd = True; 
    printAlternate(node.next, isOdd);  

# Driver code  

# Start with the empty list  
head = None;  

# con below list  
# 1->2->3->4->5->6->7->8->9->10  
head = push(head, 10);  
head = push(head, 9);  
head = push(head, 8);  
head = push(head, 7);  
head = push(head, 6);  
head = push(head, 5);  
head = push(head, 4);  
head = push(head, 3);  
head = push(head, 2);  
head = push(head, 1);  

printAlternate(head, True);  

# This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# code to print alternate nodes  
// of a linked list using recursion  
using System; 

class GFG  
{ 

// A linked list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Inserting node at the beginning  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to print alternate nodes of linked list.  
// The boolean flag isOdd is used to find if the current  
// node is even or odd.  
static void printAlternate( Node node, bool isOdd)  
{  
    if (node == null)  
    return;  
    if (isOdd == true)  
        Console.Write( node.data + " ");  
    printAlternate(node.next, !isOdd);  
}  

// Driver code  
public static void Main(String []args) 
{  
    // Start with the empty list  
    Node head = null;  

    // con below list  
    // 1.2.3.4.5.6.7.8.9.10  

    head = push(head, 10);  
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    printAlternate(head,true);  

} 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
1 3 5 7 9

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。