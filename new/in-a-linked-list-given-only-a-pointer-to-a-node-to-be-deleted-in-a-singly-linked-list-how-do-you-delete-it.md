# 仅给出一个指向要在单链列表中删除的节点的指针，如何删除它？

**简单解决方案**是遍历链接列表，直到找到要删除的节点。 但是此解决方案需要指向头节点的指针，该指针与问题陈述相矛盾。

**快速解决方案**是将数据从下一个节点复制到要删除的节点，然后删除下一个节点。 像这样：

```
struct Node *temp  = node_ptr->next;
node_ptr->data  = temp->data;
node_ptr->next  = temp->next;
free(temp);

```

下面是上述代码的实现：

## C++

```cpp

// C++ program to del the node 
// in which only a single pointer 
// is known pointing to that node 
#include <assert.h> 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
of a list and an int, push a new node on the front 
of the list. */
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

void printList(Node* head) 
{ 
    Node* temp = head; 
    while (temp != NULL) { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
} 

void deleteNode(Node* node_ptr) 
{ 
    // If the node to be deleted is the  
    // last node of linked list 
    if (node_ptr->next == NULL) 
    { 
        free(node_ptr); 
        // this will simply make the node_ptr NULL. 
        return; 
    } 

    // if node to be deleted is the first or  
    // any node in between the linked list. 
    Node* temp = node_ptr->next; 
    node_ptr->data = temp->data; 
    node_ptr->next = temp->next; 
    free(temp); 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    /* Use push() to construct below list 
    1->12->1->4->1 */
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 

    cout << "Before deleting \n"; 
    printList(head); 

    /* I m deleting the head itself. 
        You can check for more cases */
    deleteNode(head); 

    cout << "\nAfter deleting \n"; 
    printList(head); 
    return 0; 
} 

// This code is contributed by rathbhupendra

```

## C

```c

// C++ program to del the node 
// in which only a single pointer 
// is known pointing to that node 
#include <assert.h> 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
of a list and an int, push a new node on the front 
of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node 
        = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

void deleteNode(struct Node* node_ptr) 
{ 
    // If the node to be deleted is the last  
    // node of linked list 
    if (node_ptr->next == NULL) 
    { 
        free(node_ptr); 

        // this will simply make the node_ptr NULL. 
        return; 
    } 
    struct Node* temp = node_ptr->next; 
    node_ptr->data = temp->data; 
    node_ptr->next = temp->next; 
    free(temp); 
} 

// Driver code  
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
    1->12->1->4->1  */
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 

    printf("\n Before deleting \n"); 
    printList(head); 

    /* I m deleting the head itself. 
        You can check for more cases */
    deleteNode(head); 

    printf("\n After deleting \n"); 
    printList(head); 
    getchar(); 
}

```

## Java

```java

// Java program to del the node in  
// which only a single pointer is  
// known pointing to that node 
class LinkedList { 

    static Node head; 
    static class Node { 

        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void printList(Node node) 
    { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    void deleteNode(Node node) 
    { 
        Node temp = node.next; 
        node.data = temp.data; 
        node.next = temp.next; 
        System.gc(); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(1); 
        list.head.next = new Node(12); 
        list.head.next.next = new Node(1); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(1); 

        System.out.println("Before Deleting "); 
        list.printList(head); 

        /* I m deleting the head itself. 
         You can check for more cases */
        list.deleteNode(head); 
        System.out.println(""); 
        System.out.println("After deleting "); 
        list.printList(head); 
    } 
} 

// This code has been contributed by Mayank Jaiswal

```

## Python3

```py

# A python3 program to delete 
# the node in which only a single pointer 
# is known pointing to that node 

# Linked list node 

class Node(): 
    def __init__(self): 
        self.data = None
        self.next = None

# Given a reference (pointer to pointer) 
# to the head of a list and an int, 
# push a new node on the front of the list 

def push(head_ref, new_data): 

    # allocate node 
    new_node = Node() 

    # put in the data 
    new_node.data = new_data 

    # link the old list off the new node 
    new_node.next = head_ref 

    # move the head to point to the new node 
    head_ref = new_node 

    return head_ref 

def printList(head): 
    temp = head 
    while(temp != None): 
        print(temp.data, end=' ') 
        temp = temp.next

def deleteNode(node_ptr): 
    temp = node_ptr.next
    node_ptr.data = temp.data 
    node_ptr.next = temp.next

# Driver code 
if __name__ == '__main__': 

    # Start with the empty list 
    head = None

    # Use push() to construct below list 
    # 1->12->1->4->1 
    head = push(head, 1) 
    head = push(head, 4) 
    head = push(head, 1) 
    head = push(head, 12) 
    head = push(head, 1) 

    print("Before deleting ") 
    printList(head) 

    # I'm deleting the head itself. 
    # You can check for more cases 
    deleteNode(head) 

    print("\nAfter deleting") 
    printList(head) 

# This code is contributed by Yashyasvi Agarwal 

```

## C#

```cs

// C# program to del the node in 
// which only a single pointer is 
// known pointing to that node 
using System; 

public class LinkedList { 

    Node head; 
    public class Node { 

        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    void printList(Node node) 
    { 
        while (node != null) { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
    } 

    void deleteNode(Node node) 
    { 
        Node temp = node.next; 
        node.data = temp.data; 
        node.next = temp.next; 
    } 

    // Driver code 
    public static void Main() 
    { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(1); 
        list.head.next = new Node(12); 
        list.head.next.next = new Node(1); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(1); 

        Console.WriteLine("Before Deleting "); 
        list.printList(list.head); 

        /* I m deleting the head itself. 
        You can check for more cases */
        list.deleteNode(list.head); 
        Console.WriteLine(""); 
        Console.WriteLine("After deleting "); 
        list.printList(list.head); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output**

```
Before deleting 
1 12 1 4 1 
After deleting 
12 1 4 1 
```

为了使该解决方案有效，我们可以将末端节点标记为虚拟节点。 但是使用此功能的程序/功能也应进行修改。

对于双向链接列表，请尝试解决此问题。

