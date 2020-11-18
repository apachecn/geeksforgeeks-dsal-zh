# 在给定位置

删除链接列表节点

给定一个链表和一个位置，请删除给定位置的链表节点。

**示例：**

```
Input: position = 1, Linked List = 8->2->3->1->7
Output: Linked List =  8->3->1->7

Input: position = 0, Linked List = 8->2->3->1->7
Output: Linked List = 2->3->1->7

```

如果要删除的节点是根节点，则只需将其删除。 要删除中间节点，我们必须有一个指向要删除节点之前的节点的指针。 因此，如果位置不为零，我们将循环位置1次，并获得指向前一个节点的指针。

以下是上述想法的实现。

## C

```

// A complete working C program to delete a node in a linked list 
// at a given position 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Given a reference (pointer to pointer) to the head of a list 
   and an int inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node)); 
    new_node->data  = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref)    = new_node; 
} 

/* Given a reference (pointer to pointer) to the head of a list 
   and a position, deletes the node at the given position */
void deleteNode(struct Node **head_ref, int position) 
{ 
   // If linked list is empty 
   if (*head_ref == NULL) 
      return; 

   // Store head node 
   struct Node* temp = *head_ref; 

    // If head needs to be removed 
    if (position == 0) 
    { 
        *head_ref = temp->next;   // Change head 
        free(temp);               // free old head 
        return; 
    } 

    // Find previous node of the node to be deleted 
    for (int i=0; temp!=NULL && i<position-1; i++) 
         temp = temp->next; 

    // If position is more than number of nodes 
    if (temp == NULL || temp->next == NULL) 
         return; 

    // Node temp->next is the node to be deleted 
    // Store pointer to the next of node to be deleted 
    struct Node *next = temp->next->next; 

    // Unlink the node from linked list 
    free(temp->next);  // Free memory 

    temp->next = next;  // Unlink the deleted node from list 
} 

// This function prints contents of linked list starting from 
// the given node 
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf(" %d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    push(&head, 7); 
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 8); 

    puts("Created Linked List: "); 
    printList(head); 
    deleteNode(&head, 4); 
    puts("\nLinked List after Deletion at position 4: "); 
    printList(head); 
    return 0; 
}

```

## 爪哇

```

// A complete working Java program to delete a node in a linked list 
// at a given position 
class LinkedList 
{ 
    Node head;  // head of list 

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

    /* Given a reference (pointer to pointer) to the head of a list 
       and a position, deletes the node at the given position */
    void deleteNode(int position) 
    { 
        // If linked list is empty 
        if (head == null) 
            return; 

        // Store head node 
        Node temp = head; 

        // If head needs to be removed 
        if (position == 0) 
        { 
            head = temp.next;   // Change head 
            return; 
        } 

        // Find previous node of the node to be deleted 
        for (int i=0; temp!=null && i<position-1; i++) 
            temp = temp.next; 

        // If position is more than number of nodes 
        if (temp == null || temp.next == null) 
            return; 

        // Node temp->next is the node to be deleted 
        // Store pointer to the next of node to be deleted 
        Node next = temp.next.next; 

        temp.next = next;  // Unlink the deleted node from list 
    } 

    /* This function prints contents of linked list starting from 
        the given node */
    public void printList() 
    { 
        Node tnode = head; 
        while (tnode != null) 
        { 
            System.out.print(tnode.data+" "); 
            tnode = tnode.next; 
        } 
    } 

    /* Driver program to test above functions. Ideally this function 
       should be in a separate user class.  It is kept here to keep 
       code compact */
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        LinkedList llist = new LinkedList(); 

        llist.push(7); 
        llist.push(1); 
        llist.push(3); 
        llist.push(2); 
        llist.push(8); 

        System.out.println("\nCreated Linked list is: "); 
        llist.printList(); 

        llist.deleteNode(4);  // Delete node at position 4 

        System.out.println("\nLinked List after Deletion at position 4: "); 
        llist.printList(); 
    } 
} 

```

## 蟒蛇

```

# Python program to delete a node in a linked list 
# at a given position 

# Node class  
class Node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Constructor to initialize head 
    def __init__(self): 
        self.head = None

    # Function to insert a new node at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Given a reference to the head of a list  
    # and a position, delete the node at a given position 
    def deleteNode(self, position): 

        # If linked list is empty 
        if self.head == None: 
            return 

        # Store head node 
        temp = self.head 

        # If head needs to be removed 
        if position == 0: 
            self.head = temp.next
            temp = None
            return 

        # Find previous node of the node to be deleted 
        for i in range(position -1 ): 
            temp = temp.next
            if temp is None: 
                break

        # If position is more than number of nodes 
        if temp is None: 
            return 
        if temp.next is None: 
            return 

        # Node temp.next is the node to be deleted 
        # store pointer to the next of node to be deleted 
        next = temp.next.next

        # Unlink the node from linked list 
        temp.next = None

        temp.next = next 

    # Utility function to print the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print " %d " %(temp.data), 
            temp = temp.next

# Driver program to test above function 
llist = LinkedList() 
llist.push(7) 
llist.push(1) 
llist.push(3) 
llist.push(2) 
llist.push(8) 

print "Created Linked List: "
llist.printList() 
llist.deleteNode(4) 
print "\nLinked List after Deletion at position 4: "
llist.printList() 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C＃

```

// A complete working C# program to delete  
// a node in a linked list at a given position 
using System; 

class GFG{ 

// Head of list 
Node head;   

// Linked list Node 
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

// Inserts a new Node at front of the list.  
public void Push(int new_data) 
{ 

    /* 1 & 2: Allocate the Node & 
              Put in the data*/
    Node new_node = new Node(new_data); 

    /* 3\. Make next of new Node as head */
    new_node.next = head; 

    /* 4\. Move the head to point to new Node */
    head = new_node; 
} 

// Given a reference (pointer to pointer) 
// to the head of a list and a position,  
// deletes the node at the given position  
void deleteNode(int position) 
{ 

    // If linked list is empty 
    if (head == null) 
        return; 

    // Store head node 
    Node temp = head; 

    // If head needs to be removed 
    if (position == 0) 
    { 

        // Change head 
        head = temp.next;    
        return; 
    } 

    // Find previous node of the node to be deleted 
    for(int i = 0;  
            temp != null && i < position - 1; 
            i++) 
        temp = temp.next; 

    // If position is more than number of nodes 
    if (temp == null || temp.next == null) 
        return; 

    // Node temp->next is the node to be deleted 
    // Store pointer to the next of node to be deleted 
    Node next = temp.next.next; 

    // Unlink the deleted node from list 
    temp.next = next;   
} 

// This function prints contents of 
// linked list starting from the 
// given node  
public void printList() 
{ 
    Node tnode = head; 
    while (tnode != null) 
    { 
        Console.Write(tnode.data + " "); 
        tnode = tnode.next; 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    // Start with the empty list  
    GFG llist = new GFG(); 

    llist.Push(7); 
    llist.Push(1); 
    llist.Push(3); 
    llist.Push(2); 
    llist.Push(8); 

    Console.WriteLine("\nCreated Linked list is: "); 
    llist.printList(); 

    // Delete node at position 4 
    llist.deleteNode(4);   

    Console.WriteLine("\nLinked List after " +  
                      "Deletion at position 4: "); 
    llist.printList(); 
} 
} 

// This code is contributed by Rajput-Ji

```

**输出：**

```
Created Linked List: 
 8  2  3  1  7 
Linked List after Deletion at position 4: 
 8  2  3  1 

```

感谢 **Hemanth Kumar** 提出了初步的解决方案。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。