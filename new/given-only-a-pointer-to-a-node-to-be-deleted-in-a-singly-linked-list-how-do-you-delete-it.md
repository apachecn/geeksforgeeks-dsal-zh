# 在单链列表中仅给定要删除节点的指针/引用，如何删除它？

> 原文：[https://www.geeksforgeeks.org/given-only-a-pointer-to-a-node-to-be-deleted-in-a-singly-linked-list-how-do-you-delete-it/](https://www.geeksforgeeks.org/given-only-a-pointer-to-a-node-to-be-deleted-in-a-singly-linked-list-how-do-you-delete-it/)

给定要删除的节点的指针，请删除该节点。 请注意，我们没有指向头节点的指针。

**简单解决方案**是遍历链接列表，直到找到要删除的节点。 但是，此解决方案需要指向与问题陈述相矛盾的头节点的指针。

**快速解决方案**是将数据从下一个节点复制到要删除的节点，然后删除下一个节点。 像下面这样。

```
    // Find next node using next pointer
    struct Node *temp  = node_ptr->next;

    // Copy data of next node to this node
    node_ptr->data  = temp->data;

    // Unlink next node
    node_ptr->next  = temp->next;

    // Delete next node
    free(temp);

```

**程序**：

## C++

```cpp

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

void deleteNode(Node* node) 
{ 
    Node* prev; 
    if (node == NULL) 
        return; 
    else { 
        while (node->next != NULL) { 
            node->data = node->next->data; 
            prev = node; 
            node = node->next; 
        } 
        prev->next = NULL; 
    } 
} 

/* Driver code*/
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

// This is code is contributed by rathbhupendra 

```

## C

```c

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
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

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

void deleteNode(struct Node* node) 
{ 
    struct Node* prev; 
    if (node == NULL) 
        return; 
    else { 
        while (node->next != NULL) { 
            node->data = node->next->data; 
            prev = node; 
            node = node->next; 
        } 
        prev->next = NULL; 
    } 
} 

/* Driver program to test above function*/
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

    printf("Before deleting \n"); 
    printList(head); 

    /* I m deleting the head itself. 
        You can check for more cases */
    deleteNode(head); 

    printf("\nAfter deleting \n"); 
    printList(head); 
    getchar(); 
    return 0; 
} 

```

## Java

```java

class LinkedList { 
    Node head; // head of the list 

    class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    /* Given a reference to the head of a list and an int, 
        inserts a new Node on the front of the list. */
    public void push(int new_data) 
    { 
        /* 1\. alloc the Node and put the data */
        Node new_Node = new Node(new_data); 

        /* 2\. Make next of new Node as head */
        new_Node.next = head; 

        /* 3\. Move the head to point to new Node */
        head = new_Node; 
    } 

    /* This function prints contents of linked list  
        starting from the given Node */
    public void printList() 
    { 
        Node tNode = head; 
        while (tNode != null) { 
            System.out.print(tNode.data + " "); 
            tNode = tNode.next; 
        } 
    } 

    public void deleteNode(Node Node_ptr) 
    { 
        Node temp = Node_ptr.next; 
        Node_ptr.data = temp.data; 
        Node_ptr.next = temp.next; 
        temp = null; 
    } 

    public static void main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Use push() to construct below list 
        1->12->1->4->1  */
        llist.push(1); 
        llist.push(4); 
        llist.push(1); 
        llist.push(12); 
        llist.push(1); 

        System.out.println("Before deleting"); 
        llist.printList(); 

        /* I m deleting the head itself. 
        You can check for more cases */
        llist.deleteNode(llist.head); 

        System.out.println("\nAfter Deleting"); 
        llist.printList(); 
    } 
} 
// This code is contributed by Rajat Mishra 

```

## Python

```py

# a class to define a node with  
# data and next pointer 
class Node(): 

    # constructor to initialize a new node 
    def __init__(self, val = None): 
        self.data = val 
        self.next = None

# push a node to the front of the list 
def push(head, val): 

    # allocate new node 
    newnode = Node(val) 

    # link the first node of the old list to the new node 
    newnode.next = head.next

    # make the new node as head of the linked list  
    head.next = newnode 

# function to print the list 
def print_list(head): 

    temp = head.next
    while(temp != None): 
        print(temp.data, end = ' ') 
        temp = temp.next
    print() 

# function to delete the node 
# the main logic is in this 
def delete_node(node): 

    prev = Node() 

    if(node == None): 
        return
    else: 
        while(node.next != None): 
            node.data = node.next.data 
            prev = node 
            node = node.next

        prev.next = None

if __name__ == '__main__': 

    # allocate an empty header node 
    # this is a node that simply points to the 
    # first node in the list 
    head = Node() 

    # construct the below linked list 
    # 1->12->1->4->1 
    push(head, 1) 
    push(head, 4) 
    push(head, 1) 
    push(head, 12) 
    push(head, 1) 

    print('list before deleting:') 
    print_list(head) 

    # deleting the first node in the list 
    delete_node(head.next) 

    print('list after deleting: ') 
    print_list(head) 

# This code is contributed by Adith Bharadwaj 

```

## C#

```cs

using System; 

public class LinkedList  
{ 
    Node head; // head of the list 

    public class Node 
    { 
        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    /* Given a reference to the head of a list and an int, 
        inserts a new Node on the front of the list. */
    public void push(int new_data) 
    { 
        /* 1\. alloc the Node and put the data */
        Node new_Node = new Node(new_data); 

        /* 2\. Make next of new Node as head */
        new_Node.next = head; 

        /* 3\. Move the head to point to new Node */
        head = new_Node; 
    } 

    /* This function prints contents of linked list  
        starting from the given Node */
    public void printList() 
    { 
        Node tNode = head; 
        while (tNode != null)  
        { 
            Console.Write(tNode.data + " "); 
            tNode = tNode.next; 
        } 
    } 

    public void deleteNode(Node Node_ptr) 
    { 
        Node temp = Node_ptr.next; 
        Node_ptr.data = temp.data; 
        Node_ptr.next = temp.next; 
        temp = null; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        /* Use push() to construct below list 
        1->12->1->4->1 */
        llist.push(1); 
        llist.push(4); 
        llist.push(1); 
        llist.push(12); 
        llist.push(1); 

        Console.WriteLine("Before deleting"); 
        llist.printList(); 

        /* I m deleting the head itself. 
        You can check for more cases */
        llist.deleteNode(llist.head); 

        Console.WriteLine("\nAfter Deleting"); 
        llist.printList(); 
    } 
} 

// This code is contributed by 29AjayKumar  

```

**输出**：

```
Before deleting 
1 12 1 4 1 
After deleting 
12 1 4 1 
```

**如果要删除的节点是列表的最后一个节点，则此解决方案不起作用。** 为使此解决方案有效，我们可以将末端节点标记为虚拟节点。 但是使用此功能的程序/功能也应进行修改。

练习：对双链表尝试此问题。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

