# 隔离链表

中的偶数和奇数节点

给定整数链接列表，编写一个函数来修改链接列表，以使所有偶数出现在修改后的链接列表中的所有奇数之前。 另外，请保持偶数和奇数的顺序相同。

例子：

```
Input: 17->15->8->12->10->5->4->1->7->6->NULL
Output: 8->12->10->4->6->17->15->5->1->7->NULL

Input: 8->12->10->5->4->1->6->NULL
Output: 8->12->10->4->6->5->1->NULL

// If all numbers are even then do not change the list
Input: 8->12->10->NULL
Output: 8->12->10->NULL

// If all numbers are odd then do not change the list
Input: 1->3->5->7->NULL
Output: 1->3->5->7->NULL

```

**方法 1**

这个想法是获得指向列表最后一个节点的指针。 然后从头节点开始遍历列表，并将奇数值节点从其当前位置移动到列表末尾。

感谢 blunderboy 建议这种方法。

算法：

…1）获取指向最后一个节点的指针。

…2）将所有奇数节点移到末尾。

……..a）考虑第一个偶数节点之前的所有奇数节点，并将它们移到末尾。

……..b）更改头指针，使其指向第一个偶数节点。

……..b）考虑第一个偶数节点之后的所有奇数节点，并将它们移到末尾。

## C++

```cpp

// C++ program to segregate even and 
//  odd nodes in a Linked List  
#include <bits/stdc++.h> 
using namespace std; 

/* a node of the singly linked list */
class Node  
{  
    public: 
    int data;  
    Node *next;  
};  

void segregateEvenOdd(Node **head_ref)  
{  
    Node *end = *head_ref;  
    Node *prev = NULL;  
    Node *curr = *head_ref;  

    /* Get pointer to the last node */
    while (end->next != NULL)  
        end = end->next;  

    Node *new_end = end;  

    /* Consider all odd nodes before the first  
     even node and move then after end */
    while (curr->data % 2 != 0 && curr != end)  
    {  
        new_end->next = curr;  
        curr = curr->next;  
        new_end->next->next = NULL;  
        new_end = new_end->next;  
    }  

    // 10->8->17->17->15  
    /* Do following steps only if  
    there is any even node */
    if (curr->data%2 == 0)  
    {  
        /* Change the head pointer to  
        point to first even node */
        *head_ref = curr;  

        /* now current points to 
        the first even node */
        while (curr != end)  
        {  
            if ( (curr->data) % 2 == 0 )  
            {  
                prev = curr;  
                curr = curr->next;  
            }  
            else
            {  
                /* break the link between 
                prev and current */
                prev->next = curr->next;  

                /* Make next of curr as NULL */
                curr->next = NULL;  

                /* Move curr to end */
                new_end->next = curr;  

                /* make curr as new end of list */
                new_end = curr;  

                /* Update current pointer to 
                next of the moved node */
                curr = prev->next;  
            }  
        }  
    }  

    /* We must have prev set before executing  
    lines following this statement */
    else prev = curr;  

    /* If there are more than 1 odd nodes  
    and end of original list is odd then  
    move this node to end to maintain  
    same order of odd numbers in modified list */
    if (new_end != end && (end->data) % 2 != 0)  
    {  
        prev->next = end->next;  
        end->next = NULL;  
        new_end->next = end;  
    }  
    return;  
}  

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginning */
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

/* Function to print nodes in a given linked list */
void printList(Node *node)  
{  
    while (node != NULL)  
    {  
        cout << node->data <<" ";  
        node = node->next;  
    }  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Let us create a sample linked list as following  
    0->2->4->6->8->10->11 */

    push(&head, 11);  
    push(&head, 10);  
    push(&head, 8);  
    push(&head, 6);  
    push(&head, 4);  
    push(&head, 2);  
    push(&head, 0);  

    cout << "Original Linked list ";  
    printList(head);  

    segregateEvenOdd(&head);  

    cout << "\nModified Linked list ";  
    printList(head);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to segregate even and odd nodes in a 
// Linked List 
#include <stdio.h> 
#include <stdlib.h> 

/* a node of the singly linked list */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

void segregateEvenOdd(struct Node **head_ref) 
{ 
    struct Node *end = *head_ref; 
    struct Node *prev = NULL; 
    struct Node *curr = *head_ref; 

    /* Get pointer to the last node */
    while (end->next != NULL) 
        end = end->next; 

    struct Node *new_end = end; 

    /* Consider all odd nodes before the first even node 
       and move then after end */
    while (curr->data %2 != 0 && curr != end) 
    { 
        new_end->next = curr; 
        curr = curr->next; 
        new_end->next->next = NULL; 
        new_end = new_end->next; 
    } 

    // 10->8->17->17->15 
    /* Do following steps only if there is any even node */
    if (curr->data%2 == 0) 
    { 
        /* Change the head pointer to point to first even node */
        *head_ref = curr; 

        /* now current points to the first even node */
        while (curr != end) 
        { 
            if ( (curr->data)%2 == 0 ) 
            { 
                prev = curr; 
                curr = curr->next; 
            } 
            else
            { 
                /* break the link between prev and current */
                prev->next = curr->next; 

                /* Make next of curr as NULL  */
                curr->next = NULL; 

                /* Move curr to end */
                new_end->next = curr; 

                /* make curr as new end of list */
                new_end = curr; 

                /* Update current pointer to next of the moved node */
                curr = prev->next; 
            } 
        } 
    } 

    /* We must have prev set before executing lines following this 
       statement */
    else prev = curr; 

    /* If there are more than 1 odd nodes and end of original list is 
      odd then move this node to end to maintain same order of odd 
      numbers in modified list */
    if (new_end!=end && (end->data)%2 != 0) 
    { 
        prev->next = end->next; 
        end->next = NULL; 
        new_end->next = end; 
    } 
    return; 
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginning  */
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

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while (node!=NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create a sample linked list as following 
      0->2->4->6->8->10->11 */

    push(&head, 11); 
    push(&head, 10); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 2); 
    push(&head, 0); 

    printf("\nOriginal Linked list \n"); 
    printList(head); 

    segregateEvenOdd(&head); 

    printf("\nModified Linked list \n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to segregate even and odd nodes in a 
// Linked List 
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

    void segregateEvenOdd() 
    { 
        Node end = head; 
        Node prev = null; 
        Node curr = head; 

        /* Get pointer to last Node */
        while (end.next != null) 
            end = end.next; 

        Node new_end = end; 

        // Consider all odd nodes before getting first eve node 
        while (curr.data %2 !=0 && curr != end) 
        { 
            new_end.next = curr; 
            curr = curr.next; 
            new_end.next.next = null; 
            new_end = new_end.next; 
        } 

        // do following steps only if there is an even node 
        if (curr.data %2 ==0) 
        { 
            head = curr; 

            // now curr points to first even node 
            while (curr != end) 
            { 
                if (curr.data % 2 == 0) 
                { 
                    prev = curr; 
                    curr = curr.next; 
                } 
                else
                { 
                    /* Break the link between prev and curr*/
                    prev.next = curr.next; 

                    /* Make next of curr as null */
                    curr.next = null; 

                    /*Move curr to end */
                    new_end.next = curr; 

                    /*Make curr as new end of list */
                    new_end = curr; 

                    /*Update curr pointer */
                    curr = prev.next; 
                } 
            } 
        } 

        /* We have to set prev before executing rest of this code */
        else prev = curr; 

        if (new_end != end && end.data %2 != 0) 
        { 
            prev.next = end.next; 
            end.next = null; 
            new_end.next = end; 
        } 
    } 

    /*  Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Utility function to print a linked list 
    void printList() 
    { 
        Node temp = head; 
        while(temp != null) 
        { 
            System.out.print(temp.data+" "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 
        llist.push(11); 
        llist.push(10); 
        llist.push(8); 
        llist.push(6); 
        llist.push(4); 
        llist.push(2); 
        llist.push(0); 
        System.out.println("Origional Linked List"); 
        llist.printList(); 

        llist.segregateEvenOdd(); 

        System.out.println("Modified Linked List"); 
        llist.printList(); 
    } 
} /* This code is contributed by Rajat Mishra */

```

## Python

```py

# Python program to segregate even and odd nodes in a 
# Linked List 
head = None # head of list 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data # Assign data  
        self.next =None

def segregateEvenOdd(): 

    global head 
    end = head 
    prev = None
    curr = head 

    # Get pointer to last Node  
    while (end.next != None): 
        end = end.next

    new_end = end 

    # Consider all odd nodes before getting first eve node 
    while (curr.data % 2 !=0 and curr != end): 

        new_end.next = curr 
        curr = curr.next
        new_end.next.next = None
        new_end = new_end.next

    # do following steps only if there is an even node 
    if (curr.data % 2 == 0): 

        head = curr 

        # now curr points to first even node 
        while (curr != end): 

            if (curr.data % 2 == 0): 

                prev = curr 
                curr = curr.next

            else: 

                # Break the link between prev and curr 
                prev.next = curr.next

                # Make next of curr as None  
                curr.next = None

                # Move curr to end  
                new_end.next = curr 

                # Make curr as new end of list  
                new_end = curr 

                # Update curr pointer  
                curr = prev.next

    # We have to set prev before executing rest of this code  
    else: 
        prev = curr 

    if (new_end != end and end.data % 2 != 0): 

        prev.next = end.next
        end.next = None
        new_end.next = end 

# Given a reference (pointer to pointer) to the head 
# of a list and an int, push a new node on the front 
# of the list.  
def push(new_data): 
    global head 

    # 1 & 2: Allocate the Node & 
    #         Put in the data 
    new_node = Node(new_data) 

    # 3\. Make next of new Node as head  
    new_node.next = head 

    # 4\. Move the head to point to new Node  
    head = new_node 

# Utility function to print a linked list 
def printList(): 
    global head 
    temp = head 
    while(temp != None): 

        print(temp.data, end = " ") 
        temp = temp.next

    print(" ") 

# Driver program to test above functions  

push(11) 
push(10) 
push(8) 
push(6) 
push(4) 
push(2) 
push(0) 
print("Origional Linked List") 
printList() 

segregateEvenOdd() 

print("Modified Linked List") 
printList() 

# This code is contributed by Arnab Kundu  

```

## C#

```cs

// C# program to segregate even and odd nodes in a 
// Linked List 
using System; 

public class LinkedList 
{ 
    Node head; // head of list 

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

    void segregateEvenOdd() 
    { 
        Node end = head; 
        Node prev = null; 
        Node curr = head; 

        /* Get pointer to last Node */
        while (end.next != null) 
            end = end.next; 

        Node new_end = end; 

        // Consider all odd nodes before  
        // getting first eve node 
        while (curr.data % 2 != 0 && curr != end) 
        { 
            new_end.next = curr; 
            curr = curr.next; 
            new_end.next.next = null; 
            new_end = new_end.next; 
        } 

        // do following steps only  
        // if there is an even node 
        if (curr.data % 2 == 0) 
        { 
            head = curr; 

            // now curr points to first even node 
            while (curr != end) 
            { 
                if (curr.data % 2 == 0) 
                { 
                    prev = curr; 
                    curr = curr.next; 
                } 
                else
                { 
                    /* Break the link between prev and curr*/
                    prev.next = curr.next; 

                    /* Make next of curr as null */
                    curr.next = null; 

                    /*Move curr to end */
                    new_end.next = curr; 

                    /*Make curr as new end of list */
                    new_end = curr; 

                    /*Update curr pointer */
                    curr = prev.next; 
                } 
            } 
        } 

        /* We have to set prev before  
        executing rest of this code */
        else prev = curr; 

        if (new_end != end && end.data % 2 != 0) 
        { 
            prev.next = end.next; 
            end.next = null; 
            new_end.next = end; 
        } 
    } 

    /* Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Utility function to print a linked list 
    void printList() 
    { 
        Node temp = head; 
        while(temp != null) 
        { 
            Console.Write(temp.data + " "); 
            temp = temp.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main(String []args) 
    { 
        LinkedList llist = new LinkedList(); 
        llist.push(11); 
        llist.push(10); 
        llist.push(8); 
        llist.push(6); 
        llist.push(4); 
        llist.push(2); 
        llist.push(0); 
        Console.WriteLine("Origional Linked List"); 
        llist.printList(); 

        llist.segregateEvenOdd(); 

        Console.WriteLine("Modified Linked List"); 
        llist.printList(); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
 Original Linked list 0 2 4 6 8 10 11
 Modified Linked list 0 2 4 6 8 10 11

```

**时间复杂度**：`O(n)`

**方法 2**

的想法是将链表分为两部分：一个包含所有偶数节点，另一个包含所有奇数节点。 最后在偶数节点链接列表之后附加奇数节点链接列表。

要拆分链表，请遍历原始链表，然后将所有奇数节点移动到所有奇数节点的单独链表中。 在循环结束时，原始列表将具有所有偶数节点，奇数节点列表将具有所有奇数节点。 为了保持所有节点的顺序相同，我们必须在奇数节点列表的末尾插入所有奇数节点。 为了做到这一点，我们必须始终跟踪奇数节点列表中的最后一个指针。

## C++

```cpp

// CPP program to segregate even and odd nodes in a 
// Linked List 
#include <stdio.h> 
#include <stdlib.h> 

/* a node of the singly linked list */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

// Function to segregate even and odd nodes. 
void segregateEvenOdd(struct Node **head_ref) 
{ 
    // Starting node of list having  
    // even values. 
    Node *evenStart = NULL; 

    // Ending node of even values list. 
    Node *evenEnd = NULL; 

    // Starting node of odd values list. 
    Node *oddStart = NULL; 

    // Ending node of odd values list. 
    Node *oddEnd = NULL; 

    // Node to traverse the list. 
    Node *currNode = *head_ref; 

    while(currNode != NULL){ 
        int val = currNode -> data; 

        // If current value is even, add 
        // it to even values list. 
        if(val % 2 == 0) { 
            if(evenStart == NULL){ 
                evenStart = currNode; 
                evenEnd = evenStart; 
            } 

            else{ 
                evenEnd -> next = currNode; 
                evenEnd = evenEnd -> next; 
            } 
        }  

        // If current value is odd, add  
        // it to odd values list. 
        else{ 
            if(oddStart == NULL){ 
                oddStart = currNode; 
                oddEnd = oddStart; 
            } 
            else{ 
                oddEnd -> next = currNode; 
                oddEnd = oddEnd -> next; 
            } 
        } 

        // Move head pointer one step in  
        // forward direction 
        currNode = currNode -> next;     
    } 

    // If either odd list or even list is empty, 
    // no change is required as all elements  
    // are either even or odd. 
    if(oddStart == NULL || evenStart == NULL){ 
        return; 
    } 

    // Add odd list after even list.      
    evenEnd -> next = oddStart; 
    oddEnd -> next = NULL; 

    // Modify head pointer to  
    // starting of even list. 
    *head_ref = evenStart; 
} 

/* UTILITY FUNCTIONS */
/* Function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while (node!=NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create a sample linked list as following 
    0->1->4->6->9->10->11 */

    push(&head, 11); 
    push(&head, 10); 
    push(&head, 9); 
    push(&head, 6); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 0); 

    printf("\nOriginal Linked list \n"); 
    printList(head); 

    segregateEvenOdd(&head); 

    printf("\nModified Linked list \n"); 
    printList(head); 

    return 0; 
} 

// This code is contributed by NIKHIL JINDAL. 

```

## Java

```java

// Java program to segregate even and odd nodes in a 
// Linked List 
import java.io.*; 

class LinkedList { 

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

    public void segregateEvenOdd() { 

        Node evenStart = null; 
        Node evenEnd = null; 
        Node oddStart = null; 
        Node oddEnd = null; 
        Node currentNode = head; 

        while(currentNode != null) { 
            int element = currentNode.data; 

            if(element % 2 == 0) { 

                if(evenStart == null) { 
                    evenStart = currentNode; 
                    evenEnd = evenStart; 
                } else { 
                    evenEnd.next = currentNode; 
                    evenEnd = evenEnd.next; 
                } 

            } else { 

                if(oddStart == null) { 
                    oddStart = currentNode; 
                    oddEnd = oddStart; 
                } else { 
                    oddEnd.next = currentNode; 
                    oddEnd = oddEnd.next; 
                } 
            } 
                        // Move head pointer one step in forward direction 
            currentNode = currentNode.next;     
        } 

        if(oddStart == null || evenStart == null) { 
            return; 
        } 

        evenEnd.next = oddStart; 
        oddEnd.next = null; 
        head=evenStart; 
    } 

    /*  Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Utility function to print a linked list 
    void printList() 
    { 
        Node temp = head; 
        while(temp != null) 
        { 
            System.out.print(temp.data+" "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 
        llist.push(11); 
        llist.push(10); 
        llist.push(9); 
        llist.push(6); 
        llist.push(4); 
        llist.push(1); 
        llist.push(0); 
        System.out.println("Origional Linked List"); 
        llist.printList(); 

        llist.segregateEvenOdd(); 

        System.out.println("Modified Linked List"); 
        llist.printList(); 
    } 
} 

```

## C#

```cs

// C# program to segregate even and odd nodes in a 
// Linked List 
using System; 

public class LinkedList 
{ 

    Node head; // head of list 

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

    public void segregateEvenOdd()  
    { 

        Node evenStart = null; 
        Node evenEnd = null; 
        Node oddStart = null; 
        Node oddEnd = null; 
        Node currentNode = head; 

        while(currentNode != null)  
        { 
            int element = currentNode.data; 

            if(element % 2 == 0)  
            { 

                if(evenStart == null)  
                { 
                    evenStart = currentNode; 
                    evenEnd = evenStart; 
                } 
                else
                { 
                    evenEnd.next = currentNode; 
                    evenEnd = evenEnd.next; 
                } 

            }  
            else
            { 

                if(oddStart == null) 
                { 
                    oddStart = currentNode; 
                    oddEnd = oddStart; 
                } 
                else
                { 
                    oddEnd.next = currentNode; 
                    oddEnd = oddEnd.next; 
                } 
            } 

        // Move head pointer one step in forward direction 
            currentNode = currentNode.next;  
        } 

        if(oddStart == null || evenStart == null) 
        { 
            return; 
        } 

        evenEnd.next = oddStart; 
        oddEnd.next = null; 
        head=evenStart; 
    } 

    /* Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    // Utility function to print a linked list 
    void printList() 
    { 
        Node temp = head; 
        while(temp != null) 
        { 
            Console.Write(temp.data+" "); 
            temp = temp.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main() 
    { 
        LinkedList llist = new LinkedList(); 
        llist.push(11); 
        llist.push(10); 
        llist.push(9); 
        llist.push(6); 
        llist.push(4); 
        llist.push(1); 
        llist.push(0); 
        Console.WriteLine("Origional Linked List"); 
        llist.printList(); 

        llist.segregateEvenOdd(); 

        Console.WriteLine("Modified Linked List"); 
        llist.printList(); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python3

```py

# Python3 program to segregate even and odd nodes in a 
# Linked List 
head = None # head of list  

# Node class   
class Node:   

    # Function to initialise the node object   
    def __init__(self, data):   
        self.data = data # Assign data   
        self.next =None

# Function to segregate even and odd nodes. 
def segregateEvenOdd(): 
    global head  

    # Starting node of list having  
    # even values. 
    evenStart = None

    # Ending node of even values list. 
    evenEnd = None

    # Starting node of odd values list. 
    oddStart = None

    # Ending node of odd values list. 
    oddEnd = None

    # Node to traverse the list. 
    currNode = head 

    while(currNode != None): 
        val = currNode.data 

        # If current value is even, add 
        # it to even values list. 
        if(val % 2 == 0): 
            if(evenStart == None): 
                evenStart = currNode 
                evenEnd = evenStart 
            else: 
                evenEnd . next = currNode 
                evenEnd = evenEnd . next

        # If current value is odd, add  
        # it to odd values list. 
        else: 
            if(oddStart == None): 
                oddStart = currNode 
                oddEnd = oddStart 
            else: 
                oddEnd . next = currNode 
                oddEnd = oddEnd . next

        # Move head pointer one step in  
        # forward direction 
        currNode = currNode . next 

    # If either odd list or even list is empty, 
    # no change is required as all elements  
    # are either even or odd. 
    if(oddStart == None or evenStart == None): 
        return

    # Add odd list after even list.      
    evenEnd . next = oddStart 
    oddEnd . next = None

    # Modify head pointer to  
    # starting of even list. 
    head = evenStart 

''' UTILITY FUNCTIONS '''
''' Function to insert a node at the beginning '''
def push(new_data): 

    global head  
    # 1 & 2: Allocate the Node &  
    #         Put in the data  
    new_node = Node(new_data)  

    # 3\. Make next of new Node as head   
    new_node.next = head  

    # 4\. Move the head to point to new Node   
    head = new_node  

''' Function to prnodes in a given linked list '''
def printList(): 
    global head 
    node = head 
    while (node != None): 
        print(node.data, end = " ") 
        node = node.next
    print() 

''' Driver program to test above functions'''

''' Let us create a sample linked list as following 
0.1.4.6.9.10.11 '''

push(11) 
push(10) 
push(9) 
push(6) 
push(4) 
push(1) 
push(0) 

print("Original Linked list") 
printList() 

segregateEvenOdd() 

print("Modified Linked list") 
printList() 

# This code is contributed by shubhamsingh10\. 

```

 **Output:**

```
Origional Linked List
0 1 4 6 9 10 11 
Modified Linked List
0 4 6 10 1 9 11 

```

**时间复杂度**：`O(n)`

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

