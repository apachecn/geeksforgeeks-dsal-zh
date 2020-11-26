# 原地重新排列给定的链表。

> 原文：[https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/)

给定一个单链表`L0, L1, ..., Ln`。 重新排列列表中的节点，以使新形成的列表为`L0, Ln, L1, L(n-1), L2, ...`

您需要原地执行此操作，而无需更改节点的值。

**示例**：

```
Input:  1 -> 2 -> 3 -> 4
Output: 1 -> 4 -> 2 -> 3

Input:  1 -> 2 -> 3 -> 4 -> 5
Output: 1 -> 5 -> 2 -> 4 -> 3 
```

**简单解决方案**

```
1) Initialize current node as head.
2) While next of current node is not null, do following
    a) Find the last node, remove it from the end and insert it as next
       of the current node.
    b) Move current to next to next of current
```

上述简单解决方案的时间复杂度为`O(N ^ 2)`，其中`n`是链表中节点的数量。

**更好的解决方案**

1.  将给定链表的内容复制到向量中。

2.  通过交换两端的节点来重新排列给定向量。

3.  将修改后的向量复制回链表。

此方法的实现： [https://ide.geeksforgeeks.org/1eGSEy](https://ide.geeksforgeeks.org/1eGSEy)

感谢 Arushi Dhamija 提出了此方法。

**高效解决方案**：

```
1) Find the middle point using tortoise and hare method.
2) Split the linked list into two halves using found middle point in step 1.
3) Reverse the second half.
4) Do alternate merge of first and second halves. 
```

该解决方案的时间复杂度为`O(n)`。

下面是此方法的实现。

## C++

```cpp

// C++ program to rearrange a linked list in-place 
#include <bits/stdc++.h> 
using namespace std; 

// Linkedlist Node structure 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to create newNode in a linkedlist 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Function to reverse the linked list 
void reverselist(Node** head) 
{ 
    // Initialize prev and current pointers 
    Node *prev = NULL, *curr = *head, *next; 

    while (curr) { 
        next = curr->next; 
        curr->next = prev; 
        prev = curr; 
        curr = next; 
    } 

    *head = prev; 
} 

// Function to print the linked list 
void printlist(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        if (head->next) 
            cout << "-> "; 
        head = head->next; 
    } 
    cout << endl; 
} 

// Function to rearrange a linked list 
void rearrange(Node** head) 
{ 
    // 1) Find the middle point using tortoise and hare method 
    Node *slow = *head, *fast = slow->next; 
    while (fast && fast->next) { 
        slow = slow->next; 
        fast = fast->next->next; 
    } 

    // 2) Split the linked list in two halves 
    // head1, head of first half    1 -> 2 
    // head2, head of second half   3 -> 4 
    Node* head1 = *head; 
    Node* head2 = slow->next; 
    slow->next = NULL; 

    // 3) Reverse the second half, i.e.,  4 -> 3 
    reverselist(&head2); 

    // 4) Merge alternate nodes 
    *head = newNode(0); // Assign dummy Node 

    // curr is the pointer to this dummy Node, which will 
    // be used to form the new list 
    Node* curr = *head; 
    while (head1 || head2) { 
        // First add the element from list 
        if (head1) { 
            curr->next = head1; 
            curr = curr->next; 
            head1 = head1->next; 
        } 

        // Then add the element from the second list 
        if (head2) { 
            curr->next = head2; 
            curr = curr->next; 
            head2 = head2->next; 
        } 
    } 

    // Assign the head of the new list to head pointer 
    *head = (*head)->next; 
} 

// Driver program 
int main() 
{ 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 

    printlist(head); // Print original list 
    rearrange(&head); // Modify the list 
    printlist(head); // Print modified list 
    return 0; 
} 

```

## Java

```java

// Java program to rearrange link list in place 

// Linked List Class 
class LinkedList { 

    static Node head; // head of the list 

    /* Node Class */
    static class Node { 

        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void printlist(Node node) 
    { 
        if (node == null) { 
            return; 
        } 
        while (node != null) { 
            System.out.print(node.data + " -> "); 
            node = node.next; 
        } 
    } 

    Node reverselist(Node node) 
    { 
        Node prev = null, curr = node, next; 
        while (curr != null) { 
            next = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = next; 
        } 
        node = prev; 
        return node; 
    } 

    void rearrange(Node node) 
    { 

        // 1) Find the middle point using tortoise and hare method 
        Node slow = node, fast = slow.next; 
        while (fast != null && fast.next != null) { 
            slow = slow.next; 
            fast = fast.next.next; 
        } 

        // 2) Split the linked list in two halves 
        // node1, head of first half    1 -> 2 -> 3 
        // node2, head of second half   4 -> 5 
        Node node1 = node; 
        Node node2 = slow.next; 
        slow.next = null; 

        // 3) Reverse the second half, i.e., 5 -> 4 
        node2 = reverselist(node2); 

        // 4) Merge alternate nodes 
        node = new Node(0); // Assign dummy Node 

        // curr is the pointer to this dummy Node, which will 
        // be used to form the new list 
        Node curr = node; 
        while (node1 != null || node2 != null) { 

            // First add the element from first list 
            if (node1 != null) { 
                curr.next = node1; 
                curr = curr.next; 
                node1 = node1.next; 
            } 

            // Then add the element from second list 
            if (node2 != null) { 
                curr.next = node2; 
                curr = curr.next; 
                node2 = node2.next; 
            } 
        } 

        // Assign the head of the new list to head pointer 
        node = node.next; 
    } 

    public static void main(String[] args) 
    { 

        LinkedList list = new LinkedList(); 
        list.head = new Node(1); 
        list.head.next = new Node(2); 
        list.head.next.next = new Node(3); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(5); 

        list.printlist(head); // print original list 
        list.rearrange(head); // rearrange list as per ques 
        System.out.println(""); 
        list.printlist(head); // print modified list 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## C#

```cs

// C# program to rearrange link list in place 
using System; 

// Linked List Class 
public class LinkedList { 

    Node head; // head of the list 

    /* Node Class */
    class Node { 

        public int data; 
        public Node next; 

        // Constructor to create a new node 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void printlist(Node node) 
    { 
        if (node == null) { 
            return; 
        } 
        while (node != null) { 
            Console.Write(node.data + " -> "); 
            node = node.next; 
        } 
    } 

    Node reverselist(Node node) 
    { 
        Node prev = null, curr = node, next; 
        while (curr != null) { 
            next = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = next; 
        } 
        node = prev; 
        return node; 
    } 

    void rearrange(Node node) 
    { 

        // 1) Find the middle point using 
        // tortoise and hare method 
        Node slow = node, fast = slow.next; 
        while (fast != null && fast.next != null) { 
            slow = slow.next; 
            fast = fast.next.next; 
        } 

        // 2) Split the linked list in two halves 
        // node1, head of first half 1 -> 2 -> 3 
        // node2, head of second half 4 -> 5 
        Node node1 = node; 
        Node node2 = slow.next; 
        slow.next = null; 

        // 3) Reverse the second half, i.e., 5 -> 4 
        node2 = reverselist(node2); 

        // 4) Merge alternate nodes 
        node = new Node(0); // Assign dummy Node 

        // curr is the pointer to this dummy Node, which will 
        // be used to form the new list 
        Node curr = node; 
        while (node1 != null || node2 != null) { 

            // First add the element from first list 
            if (node1 != null) { 
                curr.next = node1; 
                curr = curr.next; 
                node1 = node1.next; 
            } 

            // Then add the element from second list 
            if (node2 != null) { 
                curr.next = node2; 
                curr = curr.next; 
                node2 = node2.next; 
            } 
        } 

        // Assign the head of the new list to head pointer 
        node = node.next; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        LinkedList list = new LinkedList(); 
        list.head = new Node(1); 
        list.head.next = new Node(2); 
        list.head.next.next = new Node(3); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(5); 

        list.printlist(list.head); // print original list 
        list.rearrange(list.head); // rearrange list as per ques 
        Console.WriteLine(""); 
        list.printlist(list.head); // print modified list 
    } 
} 

/* This code is contributed PrinciRaj1992 */

```

**输出**：

```
1 -> 2 -> 3 -> 4 -> 5 
1 -> 5 -> 2 -> 4 -> 3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`

感谢 Gaurav Ahirwar 提出了上述方法。

**另一种方法**：

1.  取两个指针`prev`和`curr`，它们分别保留`head`和`head->next`的地址。

2.  比较他们的数据并交换。

之后，形成一个新的链表。

下面是实现：

## C++

```cpp

// CPP code to rearrange linked list in place 
#include <bits/stdc++.h> 

using namespace std; 

struct node { 
    int data; 
    struct node* next; 
}; 
typedef struct node Node; 

// function for rearranging a linked list with high and low value. 
void rearrange(Node* head) 
{ 
    if (head == NULL) // Base case. 
        return; 

    // two pointer variable. 
    Node *prev = head, *curr = head->next; 

    while (curr) { 
        // swap function for swapping data. 
        if (prev->data > curr->data) 
            swap(prev->data, curr->data); 

        // swap function for swapping data. 
        if (curr->next && curr->next->data > curr->data) 
            swap(curr->next->data, curr->data); 

        prev = curr->next; 

        if (!curr->next) 
            break; 
        curr = curr->next->next; 
    } 
} 

// function to insert a node in the linked list at the beginning. 
void push(Node** head, int k) 
{ 
    Node* tem = (Node*)malloc(sizeof(Node)); 
    tem->data = k; 
    tem->next = *head; 
    *head = tem; 
} 

// function to display node of linked list. 
void display(Node* head) 
{ 
    Node* curr = head; 
    while (curr != NULL) { 
        printf("%d ", curr->data); 
        curr = curr->next; 
    } 
} 

// driver code 
int main() 
{ 

    Node* head = NULL; 

    // let create a linked list. 
    // 9 -> 6 -> 8 -> 3 -> 7 
    push(&head, 7); 
    push(&head, 3); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 9); 

    rearrange(head); 

    display(head); 

    return 0; 
} 

```

## Java

```java

// Java code to rearrange linked list in place 
class Geeks 
{ 

static class Node  
{ 
    int data; 
    Node next; 
} 

// function for rearranging a linked list 
// with high and low value. 
static Node rearrange(Node head) 
{ 
    if (head == null) // Base case. 
        return null; 

    // two pointer variable. 
    Node prev = head, curr = head.next; 

    while (curr != null)  
    { 
        // swap function for swapping data. 
        if (prev.data > curr.data) 
        { 
            int t = prev.data; 
            prev.data = curr.data; 
            curr.data = t; 
        } 

        // swap function for swapping data. 
        if (curr.next != null && curr.next.data > curr.data) 
        { 
            int t = curr.next.data; 
            curr.next.data = curr.data; 
            curr.data = t; 
        } 

        prev = curr.next; 

        if (curr.next == null) 
            break; 
        curr = curr.next.next; 
    } 
    return head; 
} 

// function to insert a Node in  
// the linked list at the beginning. 
static Node push(Node head, int k) 
{ 
    Node tem = new Node(); 
    tem.data = k; 
    tem.next = head; 
    head = tem; 
    return head; 
} 

// function to display Node of linked list. 
static void display(Node head) 
{ 
    Node curr = head; 
    while (curr != null) 
    { 
        System.out.printf("%d ", curr.data); 
        curr = curr.next; 
    } 
} 

// Driver code 
public static void main(String args[]) 
{ 

    Node head = null; 

    // let create a linked list. 
    // 9 . 6 . 8 . 3 . 7 
    head = push(head, 7); 
    head = push(head, 3); 
    head = push(head, 8); 
    head = push(head, 6); 
    head = push(head, 9); 

    head = rearrange(head); 

    display(head); 

} 
} 

// This code is contributed by Arnab Kundu 

```

**输出**：

```
6 9 3 8 7

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`

感谢 [Aditya](https://auth.geeksforgeeks.org/user/aditya1011/articles) 提出了这种方法。

**另一种方法**：（使用递归）

1.  保持指向头节点的指针，并使用递归操作直到最后一个节点

2.  到达最后一个节点后，开始将最后一个节点交换到根节点的下一个节点

3.  将头指针移动到下一个节点

4.  重复此过程，直到头节点和最后一个节点相遇或彼此相邻

```

// C/C++ implementation 
#include <stdio.h> 
#include <stdlib.h> 

// Creating the structure for node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to create newNode in a linkedlist 
struct Node* newNode(int key) 
{ 
    struct Node* temp = malloc(sizeof(struct Node)); 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Function to print the list 
void printlist(struct Node* head) 
{ 
    while (head) { 
        printf("%d ", head->data); 
        if (head->next) 
            printf("->"); 
        head = head->next; 
    } 
    printf("\n"); 
} 

// Function to rearrange 
void rearrange(struct Node** head, struct Node* last) 
{ 

    if (!last) 
        return; 

    // Recursive call 
    rearrange(head, last->next); 

    // (*head)->next will be set to NULL 
    // after rearrangement. 
    // Need not do any operation further 
    // Just return here to come out of recursion 
    if (!(*head)->next) 
        return; 

    // Rearrange the list until both head 
    // and last meet or next to each other. 
    if ((*head) != last && (*head)->next != last) { 
        struct Node* tmp = (*head)->next; 
        (*head)->next = last; 
        last->next = tmp; 
        *head = tmp; 
    } 
    else { 
        if ((*head) != last) 
            *head = (*head)->next; 
        (*head)->next = NULL; 
    } 
} 

// Drivers Code 
int main() 
{ 
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 

    // Print original list 
    printlist(head); 

    struct Node* tmp = head; 

    // Modify the list 
    rearrange(&tmp, head); 

    // Print modified list 
    printlist(head); 
    return 0; 
} 

```

**输出**：

```
1 ->2 ->3 ->4 ->5 
1 ->5 ->2 ->4 ->3

```

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

