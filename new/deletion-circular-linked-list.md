# 从循环链表

> 原文：[https://www.geeksforgeeks.org/deletion-circular-linked-list/](https://www.geeksforgeeks.org/deletion-circular-linked-list/)

中删除

我们已经在以下文章中讨论了循环链表和循环链表中的遍历：

[循环链表简介](http://quiz.geeksforgeeks.org/circular-linked-list/)

[遍历循环链表](http://quiz.geeksforgeeks.org/circular-linked-list-set-2-traversal/)

在本文中，我们将学习有关从特定链表中删除节点的信息。 考虑如下所示的链表：

![cll_inserted](img/8eddd191841c8f7a7360ea003dcbf87b.png)

我们将获得一个节点，我们的任务是从循环链表中删除该节点。

**示例**：

```
Input : 2->5->7->8->10->(head node)
        data = 5
Output : 2->7->8->10->(head node)

Input : 2->5->7->8->10->(head node)
         7
Output : 2->5->8->10->2(head node)

```

**算法**

**情况 1** ：列表为空。

*   如果列表为空，我们将简单地返回。

**情况 2** ：列表不为空

*   如果列表不为空，那么我们定义两个指针`curr`和`prev`，并使用**头**节点初始化指针`curr`。

*   使用`curr`遍历列表，找到要删除的节点，然后在将`curr`移至下一个节点之前，每次设置`prev = curr`。

*   如果找到该节点，请检查它是否是列表中的唯一节点。 如果是，则设置`head = NULL`和`free(curr)`。

*   如果列表具有多个节点，请检查它是否是列表的第一个节点。 检查条件`curr == head`。 如果是，则移动上一个，直到到达最后一个节点。 在`prev`到达最后一个节点后，设置`head = head->next`和`prev->next = head`。 删除`curr`。

*   如果`curr`不是第一个节点，则检查它是否是列表中的最后一个节点。 检查的条件是`curr->next == head`。

*   如果`curr`是最后一个节点。 设置`prev->next = head`并通过`free(curr)`删除节点`curr`。

*   如果要删除的节点既不是第一个节点，也不是最后一个节点，则设置`prev->next = temp->next`并删除`curr`。

**完整程序，以在循环链表中演示删除**：

## C++ 14

```

// C++ program to delete a given key from
// linked list.
#include <bits/stdc++.h>
using namespace std;

/* structure for a node */
class Node {
public:
    int data;
    Node* next;
};

/* Function to insert a node at the beginning of 
a Circular linked list */
void push(Node** head_ref, int data)
{
    // Create a new node and make head as next
    // of it.
    Node* ptr1 = new Node();
    ptr1->data = data;
    ptr1->next = *head_ref;

    /* If linked list is not NULL then set the 
    next of last node */
    if (*head_ref != NULL) 
    {
        // Find the node before head and update
        // next of it.
        Node* temp = *head_ref;
        while (temp->next != *head_ref)
            temp = temp->next;
        temp->next = ptr1;
    }
    else
        ptr1->next = ptr1; /*For the first node */

    *head_ref = ptr1;
}

/* Function to print nodes in a given 
circular linked list */
void printList(Node* head)
{
    Node* temp = head;
    if (head != NULL) {
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
    }

    cout << endl;
}

/* Function to delete a given node from the list */
void deleteNode(Node** head, int key) 
{

    // If linked list is empty
    if (*head == NULL)
        return;

    // If the list contains only a single node
    if((*head)->data==key && (*head)->next==*head)
    {
        free(*head);
        *head=NULL;
        return;
    }

    Node *last=*head,*d;

    // If head is to be deleted
    if((*head)->data==key) 
    {

        // Find the last node of the list
        while(last->next!=*head)
            last=last->next;

        // Point last node to the next of head i.e. 
        // the second node of the list
        last->next=(*head)->next;
        free(*head);
        *head=last->next;
    }

    // Either the node to be deleted is not found 
    // or the end of list is not reached
    while(last->next!=*head&&last->next->data!=key) 
    {
        last=last->next;
    }

    // If node to be deleted was found
    if(last->next->data==key) 
    {
        d=last->next;
        last->next=d->next;
        free(d);
    }
    else
        cout<<"no such keyfound";
    }

/* Driver code */
int main()
{
    /* Initialize lists as empty */
    Node* head = NULL;

    /* Created linked list will be 2->5->7->8->10 */
    push(&head, 2);
    push(&head, 5);
    push(&head, 7);
    push(&head, 8);
    push(&head, 10);

    cout << "List Before Deletion: ";
    printList(head);

    deleteNode(&head, 7);

    cout << "List After Deletion: ";
    printList(head);

    return 0;
}

// This is code is contributed by rathbhupendra

```

## C

```c

// C program to delete a given key from
// linked list.
#include <stdio.h>
#include <stdlib.h>

/* structure for a node */
struct Node {
    int data;
    struct Node* next;
};

/* Function to insert a node at the beginning of
   a Circular linked list */
void push(struct Node** head_ref, int data)
{
    // Create a new node and make head as next
    // of it.
    struct Node* ptr1 = (struct Node*)malloc(sizeof(struct Node));
    ptr1->data = data;
    ptr1->next = *head_ref;

    /* If linked list is not NULL then set the
       next of last node */
    if (*head_ref != NULL) {
        // Find the node before head and update
        // next of it.
        struct Node* temp = *head_ref;
        while (temp->next != *head_ref)
            temp = temp->next;
        temp->next = ptr1;
    }
    else
        ptr1->next = ptr1; /*For the first node */

    *head_ref = ptr1;
}

/* Function to print nodes in a given
  circular linked list */
void printList(struct Node* head)
{
    struct Node* temp = head;
    if (head != NULL) {
        do {
            printf("%d ", temp->data);
            temp = temp->next;
        } while (temp != head);
    }

    printf("\n");
}

/* Function to delete a given node from the list */
void deleteNode(struct Node* head, int key)
{
    if (head == NULL)
        return;

    // Find the required node
    struct Node *curr = head, *prev;
    while (curr->data != key) 
    {
        if (curr->next == head)
        {
            printf("\nGiven node is not found"
                   " in the list!!!");
            break;
        }

        prev = curr;
        curr = curr->next;
    }

    // Check if node is only node
    if (curr->next == head) 
    {
        head = NULL;
        free(curr);
        return;
    }

    // If more than one node, check if
    // it is first node
    if (curr == head) 
    {
        prev = head;
        while (prev->next != head)
            prev = prev->next;
        head = curr->next;
        prev->next = head;
        free(curr);
    }

    // check if node is last node
    else if (curr->next == head && curr == head) 
    {
        prev->next = head;
        free(curr);
    }
    else
    {
        prev->next = curr->next;
        free(curr);
    }
}

/* Driver code */
int main()
{
    /* Initialize lists as empty */
    struct Node* head = NULL;

    /* Created linked list will be 2->5->7->8->10 */
    push(&head, 2);
    push(&head, 5);
    push(&head, 7);
    push(&head, 8);
    push(&head, 10);

    printf("List Before Deletion: ");
    printList(head);

    deleteNode(head, 7);

    printf("List After Deletion: ");
    printList(head);

    return 0;
}

```

## Java

```java

// Java program to delete a given key from
// linked list.
class GFG {

    /* ure for a node */
    static class Node {
        int data;
        Node next;
    };

    /* Function to insert a node at the beginning of 
a Circular linked list */
    static Node push(Node head_ref, int data)
    {
        // Create a new node and make head as next
        // of it.
        Node ptr1 = new Node();
        ptr1.data = data;
        ptr1.next = head_ref;

        /* If linked list is not null then set the 
    next of last node */
        if (head_ref != null) {
            // Find the node before head and update
            // next of it.
            Node temp = head_ref;
            while (temp.next != head_ref)
                temp = temp.next;
            temp.next = ptr1;
        }
        else
            ptr1.next = ptr1; /*For the first node */

        head_ref = ptr1;
        return head_ref;
    }

    /* Function to print nodes in a given 
circular linked list */
    static void printList(Node head)
    {
        Node temp = head;
        if (head != null) {
            do {
                System.out.printf("%d ", temp.data);
                temp = temp.next;
            } while (temp != head);
        }

        System.out.printf("\n");
    }

    /* Function to delete a given node from the list */
    static Node deleteNode(Node head, int key)
    {
        if (head == null)
            return null;

        // Find the required node
        Node curr = head, prev = new Node();
        while (curr.data != key) {
            if (curr.next == head) {
                System.out.printf("\nGiven node is not found"
                                  + " in the list!!!");
                break;
            }

            prev = curr;
            curr = curr.next;
        }

        // Check if node is only node
        if (curr == head && curr.next == head) {
            head = null;
            return head;
        }

        // If more than one node, check if
        // it is first node
        if (curr == head) {
            prev = head;
            while (prev.next != head)
                prev = prev.next;
            head = curr.next;
            prev.next = head;
        }

        // check if node is last node
        else if (curr.next == head) {
            prev.next = head;
        }
        else {
            prev.next = curr.next;
        }
        return head;
    }

    /* Driver code */
    public static void main(String args[])
    {
        /* Initialize lists as empty */
        Node head = null;

        /* Created linked list will be 2.5.7.8.10 */
        head = push(head, 2);
        head = push(head, 5);
        head = push(head, 7);
        head = push(head, 8);
        head = push(head, 10);

        System.out.printf("List Before Deletion: ");
        printList(head);

        head = deleteNode(head, 7);

        System.out.printf("List After Deletion: ");
        printList(head);
    }
}

// This code is contributed by Arnab Kundu

```

## Python

```py

# Python program to delete a given key from
# linked list.

# Node of a doubly linked list 
class Node: 
    def __init__(self, next = None, data = None): 
        self.next = next
        self.data = data 

# Function to insert a node at the beginning of 
# a Circular linked list 
def push(head_ref, data):

    # Create a new node and make head as next
    # of it.
    ptr1 = Node()
    ptr1.data = data
    ptr1.next = head_ref

    # If linked list is not None then set the 
    # next of last node 
    if (head_ref != None) :

        # Find the node before head and update
        # next of it.
        temp = head_ref
        while (temp.next != head_ref):
            temp = temp.next
        temp.next = ptr1

    else:
        ptr1.next = ptr1 # For the first node 

    head_ref = ptr1
    return head_ref

# Function to print nodes in a given 
# circular linked list 
def printList( head):

    temp = head
    if (head != None) :
        while(True) :
            print( temp.data, end = " ")
            temp = temp.next
            if (temp == head):
                break
    print()

# Function to delete a given node from the list 
def deleteNode( head, key) :

    # If linked list is empty
    if (head == None):
        return

    # If the list contains only a single node
    if((head).data == key and (head).next == head):

        head = None

    last = head
    d = None

    # If head is to be deleted
    if((head).data == key) :

        # Find the last node of the list
        while(last.next != head):
            last = last.next

        # Point last node to the next of head i.e. 
        # the second node of the list
        last.next = (head).next
        head = last.next

    # Either the node to be deleted is not found 
    # or the end of list is not reached
    while(last.next != head and last.next.data != key) :
        last = last.next

    # If node to be deleted was found
    if(last.next.data == key) :
        d = last.next
        last.next = d.next

    else:
        print("no such keyfound")

    return head

# Driver code

# Initialize lists as empty 
head = None

# Created linked list will be 2.5.7.8.10 
head = push(head, 2)
head = push(head, 5)
head = push(head, 7)
head = push(head, 8)
head = push(head, 10)

print("List Before Deletion: ")
printList(head)

head = deleteNode(head, 7)

print( "List After Deletion: ")
printList(head)

# This code is contributed by Arnab Kundu

```

## C#

```cs

// C# program to delete a given key from
// linked list.
using System;

class GFG {

    /* structure for a node */
    public class Node {
        public int data;
        public Node next;
    };

    /* Function to insert a node at the beginning of 
a Circular linked list */
    static Node push(Node head_ref, int data)
    {
        // Create a new node and make head as next
        // of it.
        Node ptr1 = new Node();
        ptr1.data = data;
        ptr1.next = head_ref;

        /* If linked list is not null then set the 
         next of last node */
        if (head_ref != null) 
        {
            // Find the node before head and update
            // next of it.
            Node temp = head_ref;
            while (temp.next != head_ref)
                temp = temp.next;
            temp.next = ptr1;
        }
        else
            ptr1.next = ptr1; /*For the first node */

        head_ref = ptr1;
        return head_ref;
    }

    /* Function to print nodes in a given 
       circular linked list */
    static void printList(Node head)
    {
        Node temp = head;
        if (head != null) 
        {
            do
            {
                Console.Write("{0} ", temp.data);
                temp = temp.next;
            } while (temp != head);
        }

        Console.Write("\n");
    }

    /* Function to delete a given node from the list */
    static Node deleteNode(Node head, int key)
    {
        if (head == null)
            return null;

        // Find the required node
        Node curr = head, prev = new Node();
        while (curr.data != key)
        {
            if (curr.next == head) 
            {
                Console.Write("\nGiven node is not found"
                              + " in the list!!!");
                break;
            }

            prev = curr;
            curr = curr.next;
        }

        // Check if node is only node
        if (curr.next == head && curr == head) 
        {
            head = null;
            return head;
        }

        // If more than one node, check if
        // it is first node
        if (curr == head) 
        {
            prev = head;
            while (prev.next != head)
                prev = prev.next;
            head = curr.next;
            prev.next = head;
        }

        // check if node is last node
        else if (curr.next == head) 
        {
            prev.next = head;
        }
        else
        {
            prev.next = curr.next;
        }
        return head;
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        /* Initialize lists as empty */
        Node head = null;

        /* Created linked list will be 2.5.7.8.10 */
        head = push(head, 2);
        head = push(head, 5);
        head = push(head, 7);
        head = push(head, 8);
        head = push(head, 10);

        Console.Write("List Before Deletion: ");
        printList(head);

        head = deleteNode(head, 7);

        Console.Write("List After Deletion: ");
        printList(head);
    }
}

// This code has been contributed by 29AjayKumar

```

**输出**：

```
List Before Deletion: 10 8 7 5 2
List After Deletion: 10 8 5 2

```

本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

