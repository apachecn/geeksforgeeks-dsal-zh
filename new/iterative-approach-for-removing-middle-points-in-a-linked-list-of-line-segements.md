# 迭代方法，用于删除线段链接列表中的中点

这篇文章解释了[这个](http://www.geeksforgeeks.org/given-linked-list-line-segments-remove-middle-points/)问题的迭代方法。
我们维护两个指针：prev和temp。 如果这两个x或y相同，我们继续前进直到等式成立，并继续删除它们之间的节点。 从其开始相等的节点，我们调整该节点的下一个指针。

## C++

```cpp

// C++ program to remove intermediate  
// points in a linked list that represents 
// horizontal and vertical line segments 
#include <iostream> 
using namespace std; 

// Node has 3 fields including x, y 
// coordinates and a pointer to next node 
struct Node { 
    int x, y; 
    struct Node *next; 
}; 

/* Function to insert a node at the beginning */
void push(struct Node **head_ref, int x, int y) 
{ 
    struct Node *new_node = new Node;    
    new_node->x = x; 
    new_node->y = y; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Utility function to print a singly linked list */
void printList(struct Node *head) 
{ 
    struct Node *temp = head;     
    while (temp != NULL) { 
        printf("(%d, %d)-> ", temp->x, temp->y);         
        temp = temp->next; 
    }     
    printf("\n"); 
} 

// This function deletes middle nodes in a  
// sequence of horizontal and vertical line  
// segments represented by linked list. 
void delete_Middle_Nodes(Node *head)  
{     
    Node *temp = head->next, *prev = head;   

    while (temp) { 

        // checking equlity of point x 
        if (temp->x == prev->x)  
        { 
            Node *curr = prev; 
            prev = temp; 
            temp = temp->next;         

            // removing vertical points of line  
            // segment from linked list 
            while (temp && temp->x == prev->x)  
            { 
                curr->next = temp; 
                free(prev); 
                prev = temp; 
                temp = temp->next; 
            } 
        } 

        // checking equlity of point y 
        else if (temp->y == prev->y)  
        { 
            Node *curr = prev; 
            prev = temp; 
            temp = temp->next; 

            // removing horizontal points of line  
            // segment from linked list 
            while (temp && temp->y == prev->y) 
            { 
                curr->next = temp; 
                free(prev); 
                prev = temp; 
                temp = temp->next; 
            } 
        } else { 
            prev = temp; 
            temp = temp->next; 
        } 
    } 
} 

// Driver program to test above functions 
int main() { 
    struct Node *head = NULL; 

    push(&head, 40,5); 
    push(&head, 20,5); 
    push(&head, 10,5); 
    push(&head, 10,8); 
    push(&head, 10,10); 
    push(&head, 3,10); 
    push(&head, 1,10); 
    push(&head, 0,10); 

    printf("Given Linked List: \n"); 
    printList(head); 

    delete_Middle_Nodes(head); 

    printf("Modified Linked List: \n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

class LinkedList 
{ 
    Node head; // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int x,y; 
        Node next; 
        Node(int x, int y) 
        { 
            this.x = x; 
            this.y = y; 
            next = null; 
        } 
    } 

    // This function deletes middle nodes in a sequence of 
    // horizontal and vertical line segments represented 
    // by linked list. 
    private void delete_Middle_Nodes(Node head) 
    { 
        Node prev = head; 
        Node temp = head.next; 

        while (temp != null) 
        { 

            // checking equlity of point x 
            if (temp.x == prev.x) 
            { 
                Node curr = prev; 
                prev = temp; 
                temp = temp.next; 

                // removing vertical points of line  
                // segment from linked list 
                while (temp != null && temp.x == prev.x) 
                { 
                    curr.next = temp; 
                    prev.next = null; 
                    prev = temp; 
                    temp = temp.next; 
                } 
            } 

            // checking equlity of point y  
            else if (temp.y == prev.y) 
            { 
                Node curr = prev; 
                prev = temp; 
                temp = temp.next; 

                // removing horizontal points of line  
                // segment from linked list 
                while (temp != null && temp.y == prev.y) 
                { 
                    curr.next = temp; 
                    prev.next = null; 
                    prev = temp; 
                    temp = temp.next; 
                } 
            }  
            else
            { 
                prev =temp; 
                temp = temp.next; 
            } 
        } 
    } 

    /* Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int x, int y) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(x,y); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    void printList() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
            System.out.print("(" + temp.x + "," + temp.y + ")->"); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /* Driver code */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 

        llist.push(40,5); 
        llist.push(20,5); 
        llist.push(10,5); 
        llist.push(10,8); 
        llist.push(10,10); 
        llist.push(3,10); 
        llist.push(1,10); 
        llist.push(0,10); 

        System.out.println("Given list"); 
        llist.printList(); 

        llist.delete_Middle_Nodes(llist.head); 

        System.out.println("Modified Linked List is"); 
        llist.printList(); 
    } 
} 

// This code is contributed by shubham96301\. 

```

## Python3

```py

# Python3 program to remove intermediate  
# points in a linked list that represents 
# horizontal and vertical line segments 
import math 

# Node has 3 fields including x, y 
# coordinates and a pointer to next node 
class Node:  
    def __init__(self, x, y):  
        self.x = x 
        self.y = y 
        self.next = None

# Function to insert a node at the beginning  
def push(head_ref, x, y): 
    new_node = Node(x, y)  
    new_node.x = x 
    new_node.y = y 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Utility function to print  
# a singly linked list  
def printList(head): 
    temp = head  
    while (temp != None): 
        print("(", temp.x, ",", 
                   temp.y, ")", end = "->",)      
        temp = temp.next

    print() 

# This function deletes middle nodes in a  
# sequence of horizontal and vertical line  
# segments represented by linked list. 
def delete_Middle_Nodes(head):  
    temp = head.next
    prev = head  

    while (temp): 

        # checking equlity of point x 
        if (temp.x == prev.x): 
            curr = prev 
            prev = temp 
            temp = temp.next    

            # removing vertical points of line  
            # segment from linked list 
            while (temp != None and temp.x == prev.x): 
                curr.next = temp 

                #free(prev) 
                prev = temp 
                temp = temp.next

        # checking equlity of point y 
        elif (temp.y == prev.y): 
            curr = prev 
            prev = temp 
            temp = temp.next

            # removing horizontal points of line  
            # segment from linked list 
            while (temp != None and temp.y == prev.y): 
                curr.next = temp 
                #free(prev) 
                prev = temp 
                temp = temp.next

        else: 
            prev = temp 
            temp = temp.next

# Driver Code 
if __name__=='__main__':  
    head = None

    head = push(head, 40, 5) 
    head = push(head, 20, 5) 
    head = push(head, 10, 5) 
    head = push(head, 10, 8) 
    head = push(head, 10, 10) 
    head = push(head, 3, 10) 
    head = push(head, 1, 10) 
    head = push(head, 0, 10) 

    print("Given Linked List: \n", end = "") 
    printList(head) 

    delete_Middle_Nodes(head) 

    print("Modified Linked List: \n", end = "") 
    printList(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# program to remove intermediate  
// points in a linked list that represents 
// horizontal and vertical line segments 
using System; 

public class LinkedList 
{ 
    public Node head; // head of list 

    /* Linked list Node*/
    public class Node 
    { 
        public int x,y; 
        public Node next; 
        public Node(int x, int y) 
        { 
            this.x = x; 
            this.y = y; 
            next = null; 
        } 
    } 

    // This function deletes middle nodes in a sequence of 
    // horizontal and vertical line segments represented 
    // by linked list. 
    private void delete_Middle_Nodes(Node head) 
    { 
        Node prev = head; 
        Node temp = head.next; 

        while (temp != null) 
        { 

            // checking equlity of point x 
            if (temp.x == prev.x) 
            { 
                Node curr = prev; 
                prev = temp; 
                temp = temp.next; 

                // removing vertical points of line  
                // segment from linked list 
                while (temp != null && temp.x == prev.x) 
                { 
                    curr.next = temp; 
                    prev.next = null; 
                    prev = temp; 
                    temp = temp.next; 
                } 
            } 

            // checking equlity of point y  
            else if (temp.y == prev.y) 
            { 
                Node curr = prev; 
                prev = temp; 
                temp = temp.next; 

                // removing horizontal points of line  
                // segment from linked list 
                while (temp != null && temp.y == prev.y) 
                { 
                    curr.next = temp; 
                    prev.next = null; 
                    prev = temp; 
                    temp = temp.next; 
                } 
            }  
            else
            { 
                prev =temp; 
                temp = temp.next; 
            } 
        } 
    } 

    /* Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
    void push(int x, int y) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(x,y); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    void printList() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
            Console.Write("(" + temp.x + "," + temp.y + ")->"); 
            temp = temp.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main(String []args) 
    { 
        LinkedList llist = new LinkedList(); 

        llist.push(40,5); 
        llist.push(20,5); 
        llist.push(10,5); 
        llist.push(10,8); 
        llist.push(10,10); 
        llist.push(3,10); 
        llist.push(1,10); 
        llist.push(0,10); 

        Console.WriteLine("Given list"); 
        llist.printList(); 

        llist.delete_Middle_Nodes(llist.head); 

        Console.WriteLine("Modified Linked List is"); 
        llist.printList(); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出：**

```

Given Linked List: 
(0, 10)-> (1, 10)-> (3, 10)-> (10, 10)-> (10, 8)-> (10, 5)-> (20, 5)-> (40, 5)-> 
Modified Linked List: 
(0, 10)-> (10, 10)-> (10, 5)-> (40, 5)-> 

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。