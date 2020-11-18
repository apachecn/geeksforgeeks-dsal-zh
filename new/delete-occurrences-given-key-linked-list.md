# 删除链接列表

中所有出现的给定键

给定一个单链表，请删除其中所有出现的给定键。 例如，考虑以下列表。

**示例：**

```
Input: 2 -> 2 -> 1 -> 8 -> 2 ->  3 -> 2 -> 7
       Key to delete = 2
Output:  1 -> 8 -> 3 -> 7 

```

这主要是此帖子的[的扩展，该帖子删除了](http://quiz.geeksforgeeks.org/linked-list-set-3-deleting-node/)给定密钥的首次出现的[。
我们需要首先检查头节点上的所有事件，并适当地更改头节点。 然后，我们需要检查循环中所有出现的事件，并将它们一一删除。](http://quiz.geeksforgeeks.org/linked-list-set-3-deleting-node/)

以下是上述想法的实现：

## C ++

```

// C++ program to delete all occurrences 
// of a given key in linked list
#include <bits/stdc++.h>
using namespace std;

// A linked list node
class Node 
{
    public:
        int data;
        Node* next;
};

// Given a reference (pointer) to the head 
// of a list and an int, inserts a new node
// on the front of the list
Node* push(Node* head, int new_data)
{
    Node* new_node = new Node();
    new_node->data = new_data;
    new_node->next = head;
    head = new_node;
    return head;
}

// Given a reference (pointer)to the head
// of a list and a key, deletes all 
// occurrence of the given key in 
// linked list 
Node* deleteKey(Node *head,int x)
{

    // Store head node
    Node *tmp = head;

    while (head->data == x)
    {
        head = head->next;
    }
    while (tmp->next != NULL)
    {
        if (tmp->next->data == x)
        {
            tmp->next = tmp->next->next;
        }
        else
        {
            tmp = tmp->next;
        }
    }
    return head;
}

// This function prints contents of 
// linked list starting from the
// given node
void printList(Node* node)
{
    while (node->next != NULL) 
    {
        cout << node->data << " ";
        node = node->next;
    }
    cout << node->data;
}

// Driver code
int main()
{

    // Start with the empty list
    Node* head = NULL;
    head = push(head, 7);
    head = push(head, 2);
    head = push(head, 3);
    head = push(head, 2);
    head = push(head, 8);
    head = push(head, 1);
    head = push(head, 2);
    head = push(head, 2);

    // Key to delete
    int key = 2 ; 

    cout << "Created Linked List:\n ";
    printList(head);

    // Function call
    head = deleteKey(head, key);
    cout << "\nLinked List after Deletion is:\n";

    printList(head);

    return 0;
}

// This code is contributed by shivamsharma2020

```

## C

```

// C Program to delete all occurrences of a given key in
// linked list
#include <stdio.h>
#include <stdlib.h>

// A linked list node
struct Node 
{
    int data;
    struct Node* next;
};

/* Given a reference (pointer to pointer) to the head of a
   list and an int, inserts a new node on the front of the
   list. */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

/* Given a reference (pointer to pointer) to the head of a
   list and a key, deletes all occurrence of the given key
   in linked list */
void deleteKey(struct Node** head_ref, int key)
{
    // Store head node
    struct Node *temp = *head_ref, *prev;

    // If head node itself holds the key or multiple
    // occurrences of key
    while (temp != NULL && temp->data == key) 
    {
        *head_ref = temp->next; // Changed head
        free(temp); // free old head
        temp = *head_ref; // Change Temp
    }

    // Delete occurrences other than head
    while (temp != NULL) 
    {
        // Search for the key to be deleted, keep track of
        // the previous node as we need to change
        // 'prev->next'
        while (temp != NULL && temp->data != key) 
        {
            prev = temp;
            temp = temp->next;
        }

        // If key was not present in linked list
        if (temp == NULL)
            return;

        // Unlink the node from linked list
        prev->next = temp->next;

        free(temp); // Free memory

        // Update Temp for next iteration of outer loop
        temp = prev->next;
    }
}

// This function prints contents of linked list starting
// from the given node
void printList(struct Node* node)
{
    while (node != NULL) 
    {
        printf(" %d ", node->data);
        node = node->next;
    }
}

// Driver code
int main()
{
    // Start with the empty list
    struct Node* head = NULL;

    push(&head, 7);
    push(&head, 2);
    push(&head, 3);
    push(&head, 2);
    push(&head, 8);
    push(&head, 1);
    push(&head, 2);
    push(&head, 2);

    int key = 2; // key to delete

    puts("Created Linked List: ");
    printList(head);

    // Function call
    deleteKey(&head, key);
    puts("\nLinked List after Deletion is:");

    printList(head);
    return 0;
}

```

## 爪哇

```

// Java Program to delete all occurrences
// of a given key in linked list
class LinkedList 
{
    static Node head; // head of list

    /* Linked list Node*/
    class Node 
    {
        int data;
        Node next;
        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Given a key, deletes all occurrence
    of the given key in linked list */
    void deleteKey(int key)
    {
        // Store head node
        Node temp = head, prev = null;

        // If head node itself holds the key
        // or multiple occurrences of key
        while (temp != null && temp.data == key) 
        {
            head = temp.next; // Changed head
            temp = head; // Change Temp
        }

        // Delete occurrences other than head
        while (temp != null) 
        {
            // Search for the key to be deleted,
            // keep track of the previous node
            // as we need to change 'prev->next'
            while (temp != null && temp.data != key) 
            {
                prev = temp;
                temp = temp.next;
            }

            // If key was not present in linked list
            if (temp == null)
                return;

            // Unlink the node from linked list
            prev.next = temp.next;

            // Update Temp for next iteration of outer loop
            temp = prev.next;
        }
    }

    /* Inserts a new Node at front of the list. */
    public void push(int new_data)
    {
        Node new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    /* This function prints contents of linked list
    starting from the given node */
    public void printList()
    {
        Node tnode = head;
        while (tnode != null) 
        {
            System.out.print(tnode.data + " ");
            tnode = tnode.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList llist = new LinkedList();

        llist.push(7);
        llist.push(2);
        llist.push(3);
        llist.push(2);
        llist.push(8);
        llist.push(1);
        llist.push(2);
        llist.push(2);

        int key = 2; // key to delete

        System.out.println("Created Linked list is:");
        llist.printList();

        // Function call
        llist.deleteKey(key);

        System.out.println(
            "\nLinked List after Deletion is:");
        llist.printList();
    }
}

// This code is contributed by Shubham

```

## Python3

```

# Python3 program to delete all occurrences
# of a given key in linked list

# Link list node

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Given a reference (pointer to pointer)
# to the head of a list and an int,
# inserts a new node on the front of the list.

def push(head_ref, new_data):
    new_node = Node(0)
    new_node.data = new_data
    new_node.next = (head_ref)
    (head_ref) = new_node
    return head_ref

# Given a reference (pointer to pointer)
# to the head of a list and a key,
# deletes all occurrence of the given key
# in linked list

def deleteKey(head_ref, key):

    # Store head node
    temp = head_ref
    prev = None

    # If head node itself holds the key
    # or multiple occurrences of key
    while (temp != None and temp.data == key):
        head_ref = temp.next  # Changed head
        temp = head_ref         # Change Temp

    # Delete occurrences other than head
    while (temp != None):

        # Search for the key to be deleted,
        # keep track of the previous node
        # as we need to change 'prev.next'
        while (temp != None and temp.data != key):
            prev = temp
            temp = temp.next

        # If key was not present in linked list
        if (temp == None):
            return head_ref

        # Unlink the node from linked list
        prev.next = temp.next

        # Update Temp for next iteration of outer loop
        temp = prev.next
    return head_ref

# This function prints contents of linked list
# starting from the given node

def printList(node):
    while (node != None):
        print(node.data, end=" ")
        node = node.next

# Driver Code
if __name__ == '__main__':

    # Start with the empty list
    head = None

    head = push(head, 7)
    head = push(head, 2)
    head = push(head, 3)
    head = push(head, 2)
    head = push(head, 8)
    head = push(head, 1)
    head = push(head, 2)
    head = push(head, 2)

    key = 2  # key to delete

    print("Created Linked List: ")
    printList(head)

    # Function call
    head = deleteKey(head, key)
    print("\nLinked List after Deletion is: ")

    printList(head)

# This code is contributed by Arnab Kundu

```

## C＃

```

// C# Program to delete all occurrences
// of a given key in linked list
using System;

class GFG 
{
    static Node head; // head of list

    /* Linked list Node*/
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

    /* Given a key, deletes all occurrence
    of the given key in linked list */
    void deleteKey(int key)
    {
        // Store head node
        Node temp = head, prev = null;

        // If head node itself holds the key
        // or multiple occurrences of key
        while (temp != null && temp.data == key)
        {
            head = temp.next; // Changed head
            temp = head; // Change Temp
        }

        // Delete occurrences other than head
        while (temp != null) 
        {
            // Search for the key to be deleted,
            // keep track of the previous node
            // as we need to change 'prev->next'
            while (temp != null && temp.data != key) 
            {
                prev = temp;
                temp = temp.next;
            }

            // If key was not present in linked list
            if (temp == null)
                return;

            // Unlink the node from linked list
            prev.next = temp.next;

            // Update Temp for next iteration of outer loop
            temp = prev.next;
        }
    }

    /* Inserts a new Node at front of the list. */
    public void Push(int new_data)
    {
        Node new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    /* This function prints contents of linked list
    starting from the given node */
    public void printList()
    {
        Node tnode = head;
        while (tnode != null) 
        {
            Console.Write(tnode.data + " ");
            tnode = tnode.next;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        GFG llist = new GFG();

        llist.Push(7);
        llist.Push(2);
        llist.Push(3);
        llist.Push(2);
        llist.Push(8);
        llist.Push(1);
        llist.Push(2);
        llist.Push(2);

        int key = 2; // key to delete

        Console.WriteLine("Created Linked list is:");
        llist.printList();

        // Function call
        llist.deleteKey(key);

        Console.WriteLine(
            "\nLinked List after Deletion is:");
        llist.printList();
    }
}

// This code is contributed by 29AjayKumar

```

**Output**

```
Created Linked List: 
 2  2  1  8  2  3  2  7 
Linked List after Deletion is:
 1  8  3  7 

```

本文由 **Saransh** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。