# 编写删除链接列表的功能

**用于C / C ++的算法：**遍历链接列表，并一一删除所有节点。 这里的要点是，如果删除了当前指针，则不要访问当前指针的下一个指针。

在 **Java** 中，会发生自动垃圾收集，因此删除链接列表很容易。 我们只需要将head更改为null。

**实施：**

## C ++

```

// C++ program to delete a linked list  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Function to delete the entire linked list */
void deleteList(Node** head_ref)  
{  

/* deref head_ref to get the real head */
Node* current = *head_ref;  
Node* next;  

while (current != NULL)  
{  
    next = current->next;  
    free(current);  
    current = next;  
}  

/* deref head_ref to affect the real head back  
    in the caller. */
*head_ref = NULL;  
}  

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

    cout << "Deleting linked list";  
    deleteList(&head);  

    cout << "\nLinked list deleted";  
}  

// This is code is contributed by rathbhupendra 

```

## C

```

// C program to delete a linked list 
#include<stdio.h> 
#include<stdlib.h> 
#include<assert.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Function to delete the entire linked list */
void deleteList(struct Node** head_ref) 
{ 
   /* deref head_ref to get the real head */
   struct Node* current = *head_ref; 
   struct Node* next; 

   while (current != NULL)  
   { 
       next = current->next; 
       free(current); 
       current = next; 
   } 

   /* deref head_ref to affect the real head back 
      in the caller. */
   *head_ref = NULL; 
} 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Driver program to test count function*/
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

    printf("\n Deleting linked list"); 
    deleteList(&head);   

    printf("\n Linked list deleted"); 
} 

```

## 爪哇

```

// Java program to delete a linked list 
class LinkedList 
{ 
    Node head; // head of the list 

    /* Linked List node */
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) { data = d; next = null; } 
    } 

    /* Function deletes the entire linked list */
    void deleteList() 
    { 
        head = null; 
    } 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    public static void main(String [] args) 
    { 
        LinkedList llist = new LinkedList(); 
        /* Use push() to construct below list 
           1->12->1->4->1  */

        llist.push(1); 
        llist.push(4); 
        llist.push(1); 
        llist.push(12); 
        llist.push(1); 

        System.out.println("Deleting the list"); 
        llist.deleteList(); 

        System.out.println("Linked list deleted"); 
    } 
} 
// This code is contributed by Rajat Mishra 

```

## Python3

```

# Python3 program to delete all  
# the nodes of singly linked list 

# Node class 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None # Initialize next as null 

# Constructor to initialize the node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    def deleteList(self): 

        # initialize the current node 
        current = self.head 
        while current: 
            prev = current.next # move next node 

            # delete the current node 
            del current.data 

            # set current equals prev node 
            current = prev  

    # push function to add node in front of llist 
    def push(self, new_data): 

        # Allocate the Node & 
        # Put in the data 
        new_node = Node(new_data) 

        # Make next of new Node as head 
        new_node.next = self.head 

        # Move the head to point to new Node 
        self.head = new_node 

# Use push() to construct below  
# list 1-> 12-> 1-> 4-> 1   
if __name__ == '__main__': 

    llist = LinkedList() 
    llist.push(1) 
    llist.push(4) 
    llist.push(1) 
    llist.push(12) 
    llist.push(1) 

    print("Deleting linked list") 
    llist.deleteList() 

    print("Linked list deleted") 

# This article is provided by Shrikant13 

```

## C＃

```

// C# program to delete a linked list 
using System; 

public class LinkedList 
{ 
    Node head; // head of the list 

    /* Linked List node */
    class Node 
    { 
        public int data; 
        public Node next; 
        public Node(int d)  
        {  
            data = d; next = null; 
        } 
    } 

    /* Function deletes the entire linked list */
    void deleteList() 
    { 
        head = null; 
    } 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Driver code 
    public static void Main(String [] args) 
    { 
        LinkedList llist = new LinkedList(); 
        /* Use push() to construct below list 
        1->12->1->4->1 */

        llist.push(1); 
        llist.push(4); 
        llist.push(1); 
        llist.push(12); 
        llist.push(1); 

        Console.WriteLine("Deleting the list"); 
        llist.deleteList(); 

        Console.WriteLine("Linked list deleted"); 
    } 
} 

// This code has been contributed by Rajput-Ji  

```

**Output:**

```
 Deleting linked list
 Linked list deleted
```

**时间复杂度：** O（n）
**辅助空间：** O（1）

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。