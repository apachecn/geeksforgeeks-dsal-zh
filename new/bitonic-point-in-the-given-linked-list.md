# 给定链表

> 原文：[https://www.geeksforgeeks.org/bitonic-point-in-the-given-linked-list/](https://www.geeksforgeeks.org/bitonic-point-in-the-given-linked-list/)

中的双音点

给定具有不同元素的链表，任务是在给定链表中找到[双音点](https://www.geeksforgeeks.org/find-bitonic-point-given-bitonic-sequence/)。 如果没有该点，则打印`-1`。

**示例**：

> **输入**：` 1-> 2 -> 3 -> 4 -> 3 -> 2 -> 1 -> NULL`
>
> **输出**：4
>
> `1 -> 2 -> 3 -> 4`严格增加。
>
> `4 -> 3 -> 2 -> 1 -> NULL`严格减少。
> 
>
> **输入**：`97 -> 98 -> 99 -> 91 -> NULL`
>
> **输出**：99

**方法**：双音点是双音序列中的一个点，在该点之前元素严格增加，而在元素之后严格减少。 如果数组仅在减少或仅在增加，则不存在双音点。 因此，找到第一个节点，使其旁边的节点的值严格较小。 从该节点开始遍历链表，如果每个其他节点都严格小于其先前的节点，则找到的节点处于重音序列之外，否则给定的链表不包含有效的重音序列。 **注意**空列表或具有单个节点的列表并不代表有效的音调序列。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Node for linked list 
class Node { 
public: 
    int data; 
    Node* next; 
}; 

// Function to insert a node at 
// the head of the linked list 
Node* push(Node** head_ref, int data) 
{ 
    Node* new_node = new Node; 
    new_node->data = data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to return the bitonic 
// of the given linked list 
int bitonic_point(Node* node) 
{ 
    // If list is empty 
    if (node == NULL) 
        return -1; 

    // If list contains only 
    // a single node 
    if (node->next == NULL) 
        return -1; 

    // Invalid bitonic sequence 
    if (node->data > node->next->data) 
        return -1; 

    while (node->next != NULL) { 

        // If current node is the bitonic point 
        if (node->data > node->next->data) 
            break; 

        // Get to the next node in the list 
        node = node->next; 
    } 

    int bitonicPoint = node->data; 
    // Nodes must be in descending 
    // starting from here 
    while (node->next != NULL) { 

        // Out of order node 
        if (node->data < node->next->data) 
            return -1; 

        // Get to the next node in the list 
        node = node->next; 
    } 

    return bitonicPoint; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 

    push(&head, 100); 
    push(&head, 201); 
    push(&head, 399); 
    push(&head, 490); 
    push(&head, 377); 
    push(&head, 291); 
    push(&head, 100); 

    cout << bitonic_point(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GFG 
{ 

// Node for linked list  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node at  
// the head of the linked list  
static Node push(Node head_ref, int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

// Function to return the bitonic  
// of the given linked list  
static int bitonic_point(Node node)  
{  
    // If list is empty  
    if (node == null)  
        return -1;  

    // If list contains only  
    // a single node  
    if (node.next == null)  
        return -1;  

    // Invalid bitonic sequence  
    if (node.data > node.next.data)  
        return -1;  

    while (node.next != null)  
    {  

        // If current node is the bitonic point  
        if (node.data > node.next.data)  
            break;  

        // Get to the next node in the list  
        node = node.next;  
    }  

    int bitonicPoint = node.data;  

    // Nodes must be in descending  
    // starting from here  
    while (node.next != null)  
    {  

        // Out of order node  
        if (node.data < node.next.data)  
            return -1;  

        // Get to the next node in the list  
        node = node.next;  
    }  

    return bitonicPoint;  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = null;  

    head=push(head, 100);  
    head=push(head, 201);  
    head=push(head, 399);  
    head=push(head, 490);  
    head=push(head, 377);  
    head=push(head, 291);  
    head=push(head, 100);  

    System.out.println(bitonic_point(head));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach  
using System; 

class GFG 
{ 

// Node for linked list  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at  
// the head of the linked list  
static Node push(Node head_ref, int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

// Function to return the bitonic  
// of the given linked list  
static int bitonic_point(Node node)  
{  
    // If list is empty  
    if (node == null)  
        return -1;  

    // If list contains only  
    // a single node  
    if (node.next == null)  
        return -1;  

    // Invalid bitonic sequence  
    if (node.data > node.next.data)  
        return -1;  

    while (node.next != null)  
    {  

        // If current node is the bitonic point  
        if (node.data > node.next.data)  
            break;  

        // Get to the next node in the list  
        node = node.next;  
    }  

    int bitonicPoint = node.data;  

    // Nodes must be in descending  
    // starting from here  
    while (node.next != null)  
    {  

        // Out of order node  
        if (node.data < node.next.data)  
            return -1;  

        // Get to the next node in the list  
        node = node.next;  
    }  

    return bitonicPoint;  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = null;  

    head=push(head, 100);  
    head=push(head, 201);  
    head=push(head, 399);  
    head=push(head, 490);  
    head=push(head, 377);  
    head=push(head, 291);  
    head=push(head, 100);  

    Console.WriteLine(bitonic_point(head));  
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
490

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。