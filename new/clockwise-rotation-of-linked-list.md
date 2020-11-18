# 链表

的顺时针旋转

给定一个单链接列表和一个整数 **K** ，任务是将链接列表向右顺时针旋转 **K** 位置。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> NULL，K = 2
> **输出：** 4 -> 5-> 1-> 2-> 3->空
> 
> **输入：** 7-> 9-> 11-> 13-> 3-> 5-> NULL，K = 12
> **输出 ：** 7-> 9-> 11-> 13-> 3-> 5-> NULL

**方法：**要旋转链表，请首先检查给定的 k 是否大于链表中节点的数量。 遍历列表并找到链表的长度，然后将其与 k 进行比较，如果小于 k，则继续进行，否则通过对链表的长度取模，得出链表的大小。

之后，从列表的长度中减去 k 的值。 现在，问题已更改为链表的左旋转，因此请执行以下步骤：

*   将第 k 个节点的下一个更改为 NULL。

*   将最后一个节点的下一个更改为上一个头节点。

*   将头更改为第（k + 1）个节点。

为此，需要指向第 k 个节点，第（k + 1）个节点和最后一个节点的指针。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

/* A utility function to push a node */
void push(Node** head_ref, int new_data) 
{ 
    /* allocate node */
    Node* new_node = new Node(); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* A utility function to print linked list */
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " -> "; 
        node = node->next; 
    } 
    cout << "NULL"; 
} 

// Function that rotates the given linked list 
// clockwise by k and returns the updated 
// head pointer 
Node* rightRotate(Node* head, int k) 
{ 

    // If the linked list is empty 
    if (!head) 
        return head; 

    // len is used to store length of the linked list 
    // tmp will point to the last node after this loop 
    Node* tmp = head; 
    int len = 1; 
    while (tmp->next != NULL) { 
        tmp = tmp->next; 
        len++; 
    } 

    // If k is greater than the size 
    // of the linked list 
    if (k > len) 
        k = k % len; 

    // Subtract from length to convert 
    // it into left rotation 
    k = len - k; 

    // If no rotation needed then 
    // return the head node 
    if (k == 0 || k == len) 
        return head; 

    // current will either point to 
    // kth or NULL after this loop 
    Node* current = head; 
    int cnt = 1; 
    while (cnt < k && current != NULL) { 
        current = current->next; 
        cnt++; 
    } 

    // If current is NULL then k is equal to the 
    // count of nodes in the list 
    // Don't change the list in this case 
    if (current == NULL) 
        return head; 

    // current points to the kth node 
    Node* kthnode = current; 

    // Change next of last node to previous head 
    tmp->next = head; 

    // Change head to (k+1)th node 
    head = kthnode->next; 

    // Change next of kth node to NULL 
    kthnode->next = NULL; 

    // Return the updated head pointer 
    return head; 
} 

// Driver code 
int main() 
{ 

    /* The constructed linked list is:  
    1->2->3->4->5 */
    Node* head = NULL; 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    int k = 2; 

    // Rotate the linked list 
    Node* updated_head = rightRotate(head, k); 

    // Print the rotated linked list 
    printList(updated_head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

/* Link list node */
static class Node 
{ 
    int data; 
    Node next; 
} 

/* A utility function to push a node */
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = (head_ref); 

    /* move the head to point to the new node */
    (head_ref) = new_node; 
    return head_ref; 
} 

/* A utility function to print linked list */
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        System.out.print(node.data + " -> "); 
        node = node.next; 
    } 
    System.out.print( "null"); 
} 

// Function that rotates the given linked list 
// clockwise by k and returns the updated 
// head pointer 
static Node rightRotate(Node head, int k) 
{ 

    // If the linked list is empty 
    if (head == null) 
        return head; 

    // len is used to store length of the linked list 
    // tmp will point to the last node after this loop 
    Node tmp = head; 
    int len = 1; 
    while (tmp.next != null) 
    { 
        tmp = tmp.next; 
        len++; 
    } 

    // If k is greater than the size 
    // of the linked list 
    if (k > len) 
        k = k % len; 

    // Subtract from length to convert 
    // it into left rotation 
    k = len - k; 

    // If no rotation needed then 
    // return the head node     
    if (k == 0 || k == len) 
        return head; 

    // current will either point to 
    // kth or null after this loop 
    Node current = head; 
    int cnt = 1; 
    while (cnt < k && current != null) 
    { 
        current = current.next; 
        cnt++; 
    } 

    // If current is null then k is equal to the 
    // count of nodes in the list 
    // Don't change the list in this case 
    if (current == null) 
        return head; 

    // current points to the kth node 
    Node kthnode = current; 

    // Change next of last node to previous head 
    tmp.next = head; 

    // Change head to (k+1)th node 
    head = kthnode.next; 

    // Change next of kth node to null 
    kthnode.next = null; 

    // Return the updated head pointer 
    return head; 
} 

// Driver code 
public static void main(String args[]) 
{ 

    /* The constructed linked list is:  
    1.2.3.4.5 */
    Node head = null; 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    int k = 2; 

    // Rotate the linked list 
    Node updated_head = rightRotate(head, k); 

    // Print the rotated linked list 
    printList(updated_head); 
} 
} 

// This code is contributed by Arnub Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

/* Link list node */
public class Node 
{ 
    public int data; 
    public Node next; 
} 

/* A utility function to push a node */
static Node push(Node head_ref,  
                 int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = (head_ref); 

    /* move the head to point  
    to the new node */
    (head_ref) = new_node; 
    return head_ref; 
} 

/* A utility function to print linked list */
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        Console.Write(node.data + " -> "); 
        node = node.next; 
    } 
    Console.Write("null"); 
} 

// Function that rotates the given linked list 
// clockwise by k and returns the updated 
// head pointer 
static Node rightRotate(Node head, int k) 
{ 

    // If the linked list is empty 
    if (head == null) 
        return head; 

    // len is used to store length of  
    // the linked list, tmp will point 
    // to the last node after this loop 
    Node tmp = head; 
    int len = 1; 
    while (tmp.next != null) 
    { 
        tmp = tmp.next; 
        len++; 
    } 

    // If k is greater than the size 
    // of the linked list 
    if (k > len) 
        k = k % len; 

    // Subtract from length to convert 
    // it into left rotation 
    k = len - k; 

    // If no rotation needed then 
    // return the head node     
    if (k == 0 || k == len) 
        return head; 

    // current will either point to 
    // kth or null after this loop 
    Node current = head; 
    int cnt = 1; 
    while (cnt < k && current != null) 
    { 
        current = current.next; 
        cnt++; 
    } 

    // If current is null then k is equal  
    // to the count of nodes in the list 
    // Don't change the list in this case 
    if (current == null) 
        return head; 

    // current points to the kth node 
    Node kthnode = current; 

    // Change next of last node  
    // to previous head 
    tmp.next = head; 

    // Change head to (k+1)th node 
    head = kthnode.next; 

    // Change next of kth node to null 
    kthnode.next = null; 

    // Return the updated head pointer 
    return head; 
} 

// Driver code 
public static void Main(String []args) 
{ 

    /* The constructed linked list is:  
    1.2.3.4.5 */
    Node head = null; 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    int k = 2; 

    // Rotate the linked list 
    Node updated_head = rightRotate(head, k); 

    // Print the rotated linked list 
    printList(updated_head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
4 -> 5 -> 1 -> 2 -> 3 -> NULL

```

**时间复杂度：** O（n），其中 n 是链接列表中的节点数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。