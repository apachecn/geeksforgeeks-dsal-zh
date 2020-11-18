# 两个链表的最长公共后缀

> 原文：[https://www.geeksforgeeks.org/longest-common-suffix-two-linked-lists/](https://www.geeksforgeeks.org/longest-common-suffix-two-linked-lists/)

给定两个单链表，找到两个链表的最长公共后缀。 如果没有后缀的公共字符，则返回两个链接列表的最小长度。

**示例**：

```
Input : list1 = w -> a -> l -> k -> i -> n -> g
        list2 = l -> i -> s -> t -> e -> n -> i -> n -> g
Output :i -> n -> g

Input : list1 = p -> a -> r -> t -> y
        list2 = p -> a -> r -> t -> y -> i -> n -> g
Output :p -> a -> r -> t -> y

```

一个简单的解决方案是使用辅助数组存储链接列表。 然后打印两个数组的最长公共后缀。

上述解决方案需要额外的空间。 我们可以通过首先对两个链表进行反向操作来节省空间。 反转后，我们可以轻松找到最长公共前缀的长度。 再次反转以恢复原始列表。

这里重要的一点是元素的顺序。 我们需要从第 n 个节点打印到最后一个节点。 我们使用上述找到的计数并使用两个指针方法按要求的顺序打印节点。

## C++

```cpp

// C++ program to find the Longest Common 
// suffix in linked lists 
#include <bits/stdc++.h> 
using namespace std; 

/* Linked list node */
struct Node 
{ 
    char data; 
    struct Node* next; 
}; 

/* Function to insert a node at the beginning of 
   the linked list */
void push(struct Node **head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Function to reverse the linked list */
struct Node *reverseList(struct Node *head_ref) 
{ 
    struct Node *current, *prev, *next; 
    current = head_ref; 
    prev = NULL; 

    while (current != NULL) 
    { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 
    return prev; 
} 

// Utility function to print last n nodes 
void printLastNNode(struct Node* head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return; 

    // Move reference pointer n positions ahead 
    struct Node* ref_ptr = head; 
    while (ref_ptr != NULL && n--) 
        ref_ptr = ref_ptr->next; 

    // Now move main and reference pointers at 
    // same speed. By the end of this loop, 
    // reference pointer would point to end and 
    // main pointer would point to n-th node 
    // from end. 
    Node *main_ptr = head; 
    while (ref_ptr != NULL) { 
        main_ptr = main_ptr->next; 
        ref_ptr = ref_ptr->next; 
    } 

    // Print last n nodes. 
    while (main_ptr != NULL) 
    { 
       cout << main_ptr->data; 
       main_ptr = main_ptr->next; 
    } 
} 

// Prints the Longest Common suffix in  
// linked lists 
void longestCommSuffix(Node *h1, Node *h2) 
{ 
    // Reverse Both Linked list 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    // Now we print common nodes from head 
    Node *temp1 = h1, *temp2 = h2; 
    int count = 0; 
    while (temp1!=NULL&&temp2!=NULL) 
    { 
        // If a node is not common, break 
        if (temp1 -> data != temp2 -> data) 
            break; 

        // Keep printing while there are 
        // common nodes. 
        count++; 
        temp1 = temp1 -> next; 
        temp2 = temp2 -> next; 
    } 

    // Reversing linked lists to retain 
    // original lists. 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    printLastNNode(h1, count); 
} 

// Driver program to test above 
int main() 
{ 
    struct Node *h1 = NULL, *h2 = NULL; 

    // creating the 1 linked list 
    push(&h1,'g'); 
    push(&h1,'n'); 
    push(&h1,'i'); 
    push(&h1,'k'); 
    push(&h1,'l'); 
    push(&h1,'a'); 
    push(&h1,'w'); 

    // creating the 2 linked list 
    push(&h2,'g'); 
    push(&h2,'n'); 
    push(&h2,'i'); 
    push(&h2,'n'); 
    push(&h2,'e'); 
    push(&h2,'t'); 
    push(&h2,'s'); 
    push(&h2,'i'); 
    push(&h2,'l'); 

    longestCommSuffix(h1, h2); 

    return 0; 
} 

```

## Java

```java

// Java program to find the Longest Common 
// suffix in linked lists 
import java.util.*; 
class GFG 
{ 

/* Linked list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 
static Node h1,h2; 

/* Function to insert a node at the beginning 
of the linked list */
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* Function to reverse the linked list */
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
    return prev; 
} 

// Utility function to print last n nodes 
static void printLastNNode(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return; 

    // Move reference pointer n positions ahead 
    Node ref_ptr = head; 
    while (ref_ptr != null && n-- > 0) 
        ref_ptr = ref_ptr.next; 

    // Now move main and reference pointers at 
    // same speed. By the end of this loop, 
    // reference pointer would point to end and 
    // main pointer would point to n-th node 
    // from end. 
    Node main_ptr = head; 
    while (ref_ptr != null)  
    { 
        main_ptr = main_ptr.next; 
        ref_ptr = ref_ptr.next; 
    } 

    // Print last n nodes. 
    while (main_ptr != null) 
    { 
        System.out.print((char)(main_ptr.data)); 
        main_ptr = main_ptr.next; 
    } 
} 

// Prints the Longest Common suffix in  
// linked lists 
static void longestCommSuffix() 
{ 
    // Reverse Both Linked list 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    // Now we print common nodes from head 
    Node temp1 = h1, temp2 = h2; 
    int count = 0; 
    while (temp1 != null && temp2 != null) 
    { 
        // If a node is not common, break 
        if (temp1 . data != temp2 . data) 
            break; 

        // Keep printing while there are 
        // common nodes. 
        count++; 
        temp1 = temp1 . next; 
        temp2 = temp2 . next; 
    } 

    // Reversing linked lists to retain 
    // original lists. 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    printLastNNode(h1, count); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    h1 = null; h2 = null; 

    // creating the 1 linked list 
    h1 = push(h1, 'g'); 
    h1 = push(h1, 'n'); 
    h1 = push(h1, 'i'); 
    h1 = push(h1, 'k'); 
    h1 = push(h1, 'l'); 
    h1 = push(h1, 'a'); 
    h1 = push(h1, 'w'); 

    // creating the 2 linked list 
    h2 = push(h2, 'g'); 
    h2 = push(h2, 'n'); 
    h2 = push(h2, 'i'); 
    h2 = push(h2, 'n'); 
    h2 = push(h2, 'e'); 
    h2 = push(h2, 't'); 
    h2 = push(h2, 's'); 
    h2 = push(h2, 'i'); 
    h2 = push(h2, 'l'); 

    longestCommSuffix(); 
} 
}  

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# program to find the Longest Common 
// suffix in linked lists 
using System; 

class GFG 
{ 

/* Linked list node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 
static Node h1, h2; 

/* Function to insert a node  
at the beginning of the linked list */
static Node push(Node head_ref,  
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* Function to reverse the linked list */
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
    return prev; 
} 

// Utility function to print last n nodes 
static void printLastNNode(Node head, int n) 
{ 
    // if n == 0 
    if (n <= 0) 
        return; 

    // Move reference pointer n positions ahead 
    Node ref_ptr = head; 
    while (ref_ptr != null && n-- > 0) 
        ref_ptr = ref_ptr.next; 

    // Now move main and reference pointers at 
    // same speed. By the end of this loop, 
    // reference pointer would point to end and 
    // main pointer would point to n-th node 
    // from end. 
    Node main_ptr = head; 
    while (ref_ptr != null)  
    { 
        main_ptr = main_ptr.next; 
        ref_ptr = ref_ptr.next; 
    } 

    // Print last n nodes. 
    while (main_ptr != null) 
    { 
        Console.Write((char)(main_ptr.data)); 
        main_ptr = main_ptr.next; 
    } 
} 

// Prints the Longest Common suffix in  
// linked lists 
static void longestCommSuffix() 
{ 
    // Reverse Both Linked list 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    // Now we print common nodes from head 
    Node temp1 = h1, temp2 = h2; 
    int count = 0; 
    while (temp1 != null && temp2 != null) 
    { 
        // If a node is not common, break 
        if (temp1 . data != temp2 . data) 
            break; 

        // Keep printing while there are 
        // common nodes. 
        count++; 
        temp1 = temp1 . next; 
        temp2 = temp2 . next; 
    } 

    // Reversing linked lists to retain 
    // original lists. 
    h1 = reverseList(h1); 
    h2 = reverseList(h2); 

    printLastNNode(h1, count); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    h1 = null; h2 = null; 

    // creating the 1 linked list 
    h1 = push(h1, 'g'); 
    h1 = push(h1, 'n'); 
    h1 = push(h1, 'i'); 
    h1 = push(h1, 'k'); 
    h1 = push(h1, 'l'); 
    h1 = push(h1, 'a'); 
    h1 = push(h1, 'w'); 

    // creating the 2 linked list 
    h2 = push(h2, 'g'); 
    h2 = push(h2, 'n'); 
    h2 = push(h2, 'i'); 
    h2 = push(h2, 'n'); 
    h2 = push(h2, 'e'); 
    h2 = push(h2, 't'); 
    h2 = push(h2, 's'); 
    h2 = push(h2, 'i'); 
    h2 = push(h2, 'l'); 

    longestCommSuffix(); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
ing

```

时间复杂度：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。