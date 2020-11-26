# 用于从链表中删除第`k`个节点的递归函数

> 原文：[https://www.geeksforgeeks.org/recursive-function-delete-k-th-node-linked-list/](https://www.geeksforgeeks.org/recursive-function-delete-k-th-node-linked-list/)

给定一个单链列表，删除第`k`个位置的节点而不使用循环。

**示例**：

```
Input : list = 9->8->3->5->2->1 
          k = 4
Output : 9->8->3->2->1 

Input  : list = 0->0->1->6->2->3 
            k = 3
Output : 0->0->6->2->3 

```

我们递归地减少`k`的值。 当`k`达到 1 时，我们删除当前节点，然后将当前节点的下一个作为新节点返回。 当函数返回时，我们将返回的节点链接为上一个节点的下一个节点。

## C++

```cpp

// Recursive CPP program to delete k-th node  
// of a linked list 
#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// Deletes k-th node and returns new header. 
Node* deleteNode(Node* start, int k) 
{ 
    // If invalid k 
    if (k < 1) 
       return start; 

    // If linked list is empty  
    if (start == NULL) 
       return NULL; 

    // Base case (start needs to be deleted) 
    if (k == 1) 
    { 
        Node *res = start->next; 
        delete(start); 
        return res;   
    } 

    start->next = deleteNode(start->next, k-1); 
    return start; 
} 

/* Utility function to insert a node at the beginning */
void push(struct Node **head_ref, int new_data) 
{ 
    struct Node *new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node *head) 
{ 
    while (head!=NULL) 
    { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    printf("\n"); 
} 

/* Driver program to test above functions */
int main() 
{ 
    struct Node *head = NULL; 

    /* Create following linked list 
      12->15->10->11->5->6->2->3 */
    push(&head,3); 
    push(&head,2); 
    push(&head,6); 
    push(&head,5); 
    push(&head,11); 
    push(&head,10); 
    push(&head,15); 
    push(&head,12); 

    int k = 3; 
    head = deleteNode(head, k); 

    printf("\nModified Linked List: "); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Recursive Java program to delete k-th node  
// of a linked list  
class GFG 
{ 

static class Node  
{  
    int data;  
    Node next;  
};  

// Deletes k-th node and returns new header.  
static Node deleteNode(Node start, int k)  
{  
    // If invalid k  
    if (k < 1)  
    return start;  

    // If linked list is empty  
    if (start == null)  
    return null;  

    // Base case (start needs to be deleted)  
    if (k == 1)  
    {  
        Node res = start.next;  
        return res;  
    }  

    start.next = deleteNode(start.next, k-1);  
    return start;  
}  

// Utility function to insert a node at the beginning / 
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    return head_ref; 
}  

// Utility function to print a linked list / 
static void printList( Node head)  
{  
    while (head!=null)  
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
    System.out.printf("\n");  
}  

// Driver program to test above functions / 
public static void main(String args[]) 
{  
    Node head = null;  

    // Create following linked list  
    //12.15.10.11.5.6.2.3 / 
    head=push(head,3);  
    head=push(head,2);  
    head=push(head,6);  
    head=push(head,5);  
    head=push(head,11);  
    head=push(head,10);  
    head=push(head,15);  
    head=push(head,12);  

    int k = 3;  
    head = deleteNode(head, k);  

    System.out.printf("\nModified Linked List: ");  
    printList(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Recursive Java program to delete k-th node  
# of a linked list  
class Node(object):  
    def __init__(self, d):  
        self.data = d  
        self.next = None

# Deletes k-th node and returns new header.  
def deleteNode(start, k) : 

    # If invalid k  
    if (k < 1) : 
        return start  

    # If linked list is empty  
    if (start == None):  
        return None

    # Base case (start needs to be deleted)  
    if (k == 1) : 

        res = start.next
        return res  

    start.next = deleteNode(start.next, k - 1)  
    return start  

# Utility function to insert a node  
# at the beginning  
def push(head_ref, new_data) : 

    new_node = Node(0)  
    new_node.data = new_data  
    new_node.next = head_ref  
    head_ref = new_node  
    return head_ref 

# Utility function to print a linked list  
def printList( head) : 

    while (head != None):  

        print(head.data, end = " ")  
        head = head.next

    print("\n")  

# Driver Code 
head = None

# Create following linked list  
# 12.15.10.11.5.6.2.3 / 
head = push(head, 3)  
head = push(head, 2)  
head = push(head, 6)  
head = push(head, 5)  
head = push(head, 11)  
head = push(head, 10)  
head = push(head, 15)  
head = push(head, 12)  

k = 3
head = deleteNode(head, k)  

print("Modified Linked List: ", end = "")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// Recursive C# program to delete k-th node  
// of a linked list  
using System; 

class GFG 
{ 

    public class Node  
    {  
        public int data;  
        public Node next;  
    };  

    // Deletes k-th node and returns new header.  
    static Node deleteNode(Node start, int k)  
    {  
        // If invalid k  
        if (k < 1)  
        return start;  

        // If linked list is empty  
        if (start == null)  
        return null;  

        // Base case (start needs to be deleted)  
        if (k == 1)  
        {  
            Node res = start.next;  
            return res;  
        }  

        start.next = deleteNode(start.next, k-1);  
        return start;  
    }  

    // Utility function to insert a node at the beginning / 
    static Node push( Node head_ref, int new_data)  
    {  
        Node new_node = new Node();  
        new_node.data = new_data;  
        new_node.next = head_ref;  
        head_ref = new_node;  
        return head_ref; 
    }  

    // Utility function to print a linked list / 
    static void printList( Node head)  
    {  
        while (head != null)  
        {  
            Console.Write(head.data + " ");  
            head = head.next;  
        }  
        Console.Write("\n");  
    }  

    // Driver program to test above functions / 
    public static void Main(String []args) 
    {  
        Node head = null;  

        // Create following linked list  
        //12.15.10.11.5.6.2.3 / 
        head=push(head,3);  
        head=push(head,2);  
        head=push(head,6);  
        head=push(head,5);  
        head=push(head,11);  
        head=push(head,10);  
        head=push(head,15);  
        head=push(head,12);  

        int k = 3;  
        head = deleteNode(head, k);  

        Console.Write("\nModified Linked List: ");  
        printList(head);  
    } 
}  

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
Modified Linked List: 12 15 11 5 6 2 3 

```

本文由 [**Mohd Saleem**](https://auth.geeksforgeeks.org/profile.php?user=Mohd%20%20Saleem) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，也可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄到 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

