# 在给定约束下删除链表中的给定节点

> 原文：[https://www.geeksforgeeks.org/delete-a-given-node-in-linked-list-under-given-constraints/](https://www.geeksforgeeks.org/delete-a-given-node-in-linked-list-under-given-constraints/)

给定一个单链列表，编写一个删除给定节点的函数。 您的函数必须遵循以下约束：

1.  它必须接受指向起始节点的指针作为第一个参数，并接受要删除的节点作为第二个参数，即，指向头节点的指针不是全局的。

2.  它不应返回指向头节点的指针。

3.  它不应接受指向头节点的指针。

您可以假定“链表”永远不会为空。

让函数名称为 deleteNode（）。 在一个简单的实现中，当要删除的节点是第一个节点时，该函数需要修改头指针。 如[上一篇文章](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)所讨论的，当函数修改头指针时，该函数必须使用给定方法的[中的一种，此处我们无法使用任何一种方法。](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)

**解决方案**

我们明确处理要删除的节点是第一个节点的情况，我们将下一个节点的数据复制到头部，然后删除下一个节点。 可以通过找到上一个节点并更改下一个下一个节点来正常处理被删除节点不是头节点的情况。 以下是实现。

## C++

```cpp

// C++ program to delete a given node 
// in linked list under given constraints 
#include <bits/stdc++.h> 
using namespace std; 

/* structure of a linked list node */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

void deleteNode(Node *head, Node *n)  
{  
    // When node to be deleted is head node  
    if(head == n)  
    {  
        if(head->next == NULL)  
        {  
            cout << "There is only one node." << 
                    " The list can't be made empty ";  
            return;  
        }  

        /* Copy the data of next node to head */
        head->data = head->next->data;  

        // store address of next node  
        n = head->next;  

        // Remove the link of next node  
        head->next = head->next->next;  

        // free memory  
        free(n);  

        return;  
    }  

    // When not first node, follow  
    // the normal deletion process  

    // find the previous node  
    Node *prev = head;  
    while(prev->next != NULL && prev->next != n)  
        prev = prev->next;  

    // Check if node really exists in Linked List  
    if(prev->next == NULL)  
    {  
        cout << "\nGiven node is not present in Linked List";  
        return;  
    }  

    // Remove node from Linked List  
    prev->next = prev->next->next;  

    // Free memory  
    free(n);  

    return;  
}  

/* Utility function to insert a node at the beginning */
void push(Node **head_ref, int new_data)  
{  
    Node *new_node = new Node(); 
    new_node->data = new_data;  
    new_node->next = *head_ref;  
    *head_ref = new_node;  
}  

/* Utility function to print a linked list */
void printList(Node *head)  
{  
    while(head!=NULL)  
    {  
        cout<<head->data<<" ";  
        head=head->next;  
    }  
    cout<<endl; 
}  

/* Driver code */
int main()  
{  
    Node *head = NULL;  

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

    cout<<"Given Linked List: ";  
    printList(head);  

    /* Let us delete the node with value 10 */
    cout<<"\nDeleting node "<< head->next->next->data<<" ";  
    deleteNode(head, head->next->next);  

    cout<<"\nModified Linked List: ";  
    printList(head);  

    /* Let us delete the first node */
    cout<<"\nDeleting first node ";  
    deleteNode(head, head);  

    cout<<"\nModified Linked List: ";  
    printList(head);  
    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

#include <stdio.h> 
#include <stdlib.h> 

/* structure of a linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

void deleteNode(struct Node *head, struct Node *n) 
{ 
    // When node to be deleted is head node 
    if(head == n) 
    { 
        if(head->next == NULL) 
        { 
            printf("There is only one node. The list can't be made empty "); 
            return; 
        } 

        /* Copy the data of next node to head */
        head->data = head->next->data; 

        // store address of next node 
        n = head->next; 

        // Remove the link of next node 
        head->next = head->next->next; 

        // free memory 
        free(n); 

        return; 
    } 

    // When not first node, follow the normal deletion process 

    // find the previous node 
    struct Node *prev = head; 
    while(prev->next != NULL && prev->next != n) 
        prev = prev->next; 

    // Check if node really exists in Linked List 
    if(prev->next == NULL) 
    { 
        printf("\n Given node is not present in Linked List"); 
        return; 
    } 

    // Remove node from Linked List 
    prev->next = prev->next->next; 

    // Free memory 
    free(n); 

    return;  
} 

/* Utility function to insert a node at the beginning */
void push(struct Node **head_ref, int new_data) 
{ 
    struct Node *new_node = 
        (struct Node *)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node *head) 
{ 
    while(head!=NULL) 
    { 
        printf("%d ",head->data); 
        head=head->next; 
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

    printf("Given Linked List: "); 
    printList(head); 

    /* Let us delete the node with value 10 */
    printf("\nDeleting node %d: ", head->next->next->data); 
    deleteNode(head, head->next->next); 

    printf("\nModified Linked List: "); 
    printList(head); 

    /* Let us delete the first node */
    printf("\nDeleting first node "); 
    deleteNode(head, head); 

    printf("\nModified Linked List: "); 
    printList(head); 

    getchar(); 
    return 0; 
} 

```

## Python 3

```

# Node class 
class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# LinkedList class 
class LinkedList: 

    def __init__(self): 
        self.head = None

    def deleteNode(self, data): 
        temp = self.head 
        prev = self.head 
        if temp.data == data: 
            if temp.next is None: 
                print("Can't delete the node as it has only one node") 
            else: 
                temp.data = temp.next.data 
                temp.next = temp.next.next
            return
        while temp.next is not None and temp.data != data: 
            prev = temp 
            temp = temp.next
        if temp.next is None and temp.data !=data: 
            print("Can't delete the node as it doesn't exist") 
         # If node is last node of the linked list 
        elif temp.next is None and temp.data == data: 
            prev.next = None
        else: 
            prev.next = temp.next

    # To push a new element in the Linked List      
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # To print all the elements of the Linked List 
    def PrintList(self): 

        temp = self.head 
        while(temp): 
            print(temp.data, end = " ") 
            temp = temp.next

# Driver Code 
llist = LinkedList() 
llist.push(3) 
llist.push(2) 
llist.push(6) 
llist.push(5) 
llist.push(11) 
llist.push(10) 
llist.push(15) 
llist.push(12) 

print("Given Linked List: ", end = ' ') 
llist.PrintList() 
print("\n\nDeleting node 10:") 
llist.deleteNode(10) 
print("Modified Linked List: ", end = ' ') 
llist.PrintList() 
print("\n\nDeleting first node") 
llist.deleteNode(12) 
print("Modified Linked List: ", end = ' ') 
llist.PrintList() 

# This code is contributed by Akarsh Somani 

```

## Java

```java

// Java program to delete a given node  
// in linked list under given constraints 

class LinkedList { 

    static Node head; 

    static class Node { 

        int data; 
        Node next; 

        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    void deleteNode(Node node, Node n) { 

        // When node to be deleted is head node 
        if (node == n) { 
            if (node.next == null) { 
                System.out.println("There is only one node. The list "
                                 + "can't be made empty "); 
                return; 
            } 

            /* Copy the data of next node to head */
            node.data = node.next.data; 

            // store address of next node 
            n = node.next; 

            // Remove the link of next node 
            node.next = node.next.next; 

            // free memory 
            System.gc(); 

            return; 
        } 

        // When not first node, follow the normal deletion process 
        // find the previous node 
        Node prev = node; 
        while (prev.next != null && prev.next != n) { 
            prev = prev.next; 
        } 

        // Check if node really exists in Linked List 
        if (prev.next == null) { 
            System.out.println("Given node is not present in Linked List"); 
            return; 
        } 

        // Remove node from Linked List 
        prev.next = prev.next.next; 

        // Free memory 
        System.gc(); 

        return; 
    } 

    /* Utility function to print a linked list */
    void printList(Node head) { 
        while (head != null) { 
            System.out.print(head.data + " "); 
            head = head.next; 
        } 
        System.out.println(""); 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(12); 
        list.head.next = new Node(15); 
        list.head.next.next = new Node(10); 
        list.head.next.next.next = new Node(11); 
        list.head.next.next.next.next = new Node(5); 
        list.head.next.next.next.next.next = new Node(6); 
        list.head.next.next.next.next.next.next = new Node(2); 
        list.head.next.next.next.next.next.next.next = new Node(3); 

        System.out.println("Given Linked List :"); 
        list.printList(head); 
        System.out.println(""); 

        // Let us delete the node with value 10 
        System.out.println("Deleting node :" + head.next.next.data); 
        list.deleteNode(head, head.next.next); 

        System.out.println("Modified Linked list :"); 
        list.printList(head); 
        System.out.println(""); 

        // Lets delete the first node 
        System.out.println("Deleting first Node"); 
        list.deleteNode(head, head); 
        System.out.println("Modified Linked List"); 
        list.printList(head); 

    } 
} 

// this code has been contributed by Mayank Jaiswal 

```

## C#

```cs

// C# program to delete a given  
// node in linked list under  
// given constraints 
using System; 

public class LinkedList  
{ 

    Node head; 

    class Node  
    { 

        public int data; 
        public Node next; 

        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void deleteNode(Node node, Node n) 
    { 

        // When node to be deleted is head node 
        if (node == n) 
        { 
            if (node.next == null)  
            { 
                Console.WriteLine("There is only one node. The list "
                                + "can't be made empty "); 
                return; 
            } 

            /* Copy the data of next node to head */
            node.data = node.next.data; 

            // store address of next node 
            n = node.next; 

            // Remove the link of next node 
            node.next = node.next.next; 

            // free memory 
            GC.Collect(); 

            return; 
        } 

        // When not first node, follow 
        // the normal deletion process 
        // find the previous node 
        Node prev = node; 
        while (prev.next != null && prev.next != n)  
        { 
            prev = prev.next; 
        } 

        // Check if node really exists in Linked List 
        if (prev.next == null)  
        { 
            Console.WriteLine("Given node is not" + 
                               "present in Linked List"); 
            return; 
        } 

        // Remove node from Linked List 
        prev.next = prev.next.next; 

        // Free memory 
        GC.Collect(); 

        return; 
    } 

    /* Utility function to print a linked list */
    void printList(Node head)  
    { 
        while (head != null) 
        { 
            Console.Write(head.data + " "); 
            head = head.next; 
        } 
        Console.WriteLine(""); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(12); 
        list.head.next = new Node(15); 
        list.head.next.next = new Node(10); 
        list.head.next.next.next = new Node(11); 
        list.head.next.next.next.next = new Node(5); 
        list.head.next.next.next.next.next = new Node(6); 
        list.head.next.next.next.next.next.next = new Node(2); 
        list.head.next.next.next.next.next.next.next = new Node(3); 

        Console.WriteLine("Given Linked List :"); 
        list.printList(list.head); 
        Console.WriteLine(""); 

        // Let us delete the node with value 10 
        Console.WriteLine("Deleting node :" + 
                            list.head.next.next.data); 
        list.deleteNode(list.head, list.head.next.next); 

        Console.WriteLine("Modified Linked list :"); 
        list.printList(list.head); 
        Console.WriteLine(""); 

        // Lets delete the first node 
        Console.WriteLine("Deleting first Node"); 
        list.deleteNode(list.head, list.head); 
        Console.WriteLine("Modified Linked List"); 
        list.printList(list.head); 
    } 
}  

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Given Linked List: 12 15 10 11 5 6 2 3

Deleting node 10:
Modified Linked List: 12 15 11 5 6 2 3

Deleting first node
Modified Linked List: 15 11 5 6 2 3

```

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

