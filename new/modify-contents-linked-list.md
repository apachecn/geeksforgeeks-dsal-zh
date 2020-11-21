# 修改链表

> 原文：[https://www.geeksforgeeks.org/modify-contents-linked-list/](https://www.geeksforgeeks.org/modify-contents-linked-list/)

的内容

给定一个包含 **n** 个节点的单链列表。 修改前半个节点的值，以使第一个节点的新值等于最后一个节点的值减去第一个节点的当前值，第二个节点的新值等于后一个节点的值减去第二个节点的当前值，对于前半个节点也是如此。 如果 **n** 为奇数，则中间节点的值保持不变。

（无需使用额外的内存）。

**示例**：

```
Input : 10 -> 4 -> 5 -> 3 -> 6
Output : 4 -> 1 -> 5 -> 3 -> 6

Input : 2 -> 9 -> 8 -> 12 -> 7 -> 10
Output : -8 -> 2 -> -4 -> 12 -> 7 -> 10

```

在亚马逊采访中问

**方法**：以下步骤是：

1.  从中间拆分列表。 进行 [**前后拆分**](https://www.geeksforgeeks.org/merge-sort-for-linked-list/) 。 如果元素的数量为奇数，则多余的元素应放在第一（前）列表中。

2.  [**反转第二（后）列表**](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/) 。

3.  同时遍历两个列表时，请执行所需的减法操作。

4.  再次反转第二个列表。

5.  将第二个列表连接回第一个列表的末尾。

## C++

```cpp

// C++ implementation to modify the contents of  
// the linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Linked list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* function prototype for printing the list */
void printList(struct Node*); 

/* Function to insert a node at the beginning of  
   the linked list */
void push(struct Node **head_ref, int new_data) 
{ 
  /* allocate node */
  struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 

  /* put in the data  */
  new_node->data = new_data; 

  /* link the old list at the end of the new node */
  new_node->next = *head_ref;     

  /* move the head to point to the new node */
  *head_ref = new_node; 
}  

/* Split the nodes of the given list  
   into front and back halves, 
   and return the two lists  
   using the reference parameters. 
   Uses the fast/slow pointer strategy. */
void frontAndBackSplit(struct Node *head,  
               struct Node **front_ref, struct Node **back_ref) 
{ 
    Node *slow, *fast; 

    slow = head; 
    fast = head->next; 

    /* Advance 'fast' two nodes, and  
       advance 'slow' one node */
    while (fast != NULL) 
    { 
        fast = fast->next; 
        if (fast != NULL) 
        { 
            slow = slow->next; 
            fast = fast->next; 
        } 
    } 

     /* 'slow' is before the midpoint in the list,  
        so split it in two at that point. */
    *front_ref = head; 
    *back_ref = slow->next; 
    slow->next = NULL; 
} 

/* Function to reverse the linked list */
void reverseList(struct Node **head_ref) 
{ 
    struct Node *current, *prev, *next; 
    current = *head_ref; 
    prev = NULL; 
    while (current != NULL) 
    { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    }     
    *head_ref = prev; 
} 

// perfrom the required subtraction operation on 
// the 1st half of the linked list 
void modifyTheContentsOf1stHalf(struct Node *front, 
                                struct Node *back) 
{ 
    // traversing both the lists simultaneously 
    while (back != NULL) 
    { 
        // subtraction operation and node data 
        // modification 
        front->data = front->data - back->data; 

        front = front->next; 
        back = back->next; 
    } 
} 

// function to concatenate the 2nd(back) list at the end of 
// the 1st(front) list and returns the head of the new list 
struct Node* concatFrontAndBackList(struct Node *front, 
                                    struct Node *back) 
{ 
    struct Node *head = front; 

    while (front->next != NULL) 
        front = front->next;     

    front->next    = back; 

    return head; 
} 

// function to modify the contents of the linked list 
struct Node* modifyTheList(struct Node *head) 
{ 
    // if list is empty or contains only single node 
    if (!head || head->next == NULL) 
        return head; 

    struct Node *front, *back; 

    // split the list into two halves 
    // front and back lists 
    frontAndBackSplit(head, &front, &back);     

    // reverse the 2nd(back) list 
    reverseList(&back); 

    // modify the contents of 1st half     
    modifyTheContentsOf1stHalf(front, back); 

    // agains reverse the 2nd(back) list 
    reverseList(&back); 

    // concatenating the 2nd list back to the  
    // end of the 1st list 
    head = concatFrontAndBackList(front, back); 

    // pointer to the modified list 
    return head; 
} 

// function to print the linked list 
void printList(struct Node *head) 
{ 
    if (!head) 
        return; 

    while (head->next != NULL) 
    { 
        cout << head->data << " -> "; 
        head = head->next; 
    } 
    cout << head->data << endl; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node *head = NULL; 

    // creating the linked list 
    push(&head, 10); 
    push(&head, 7); 
    push(&head, 12); 
    push(&head, 8); 
    push(&head, 9); 
    push(&head, 2); 

    // modify the linked list 
    head = modifyTheList(head); 

    // print the modified linked list 
    cout << "Modified List:" << endl; 
    printList(head); 
    return 0; 
}  

```

## Java

```java

// Java implementation to modify the contents  
// of the linked list 
class GFG 
{ 

/* Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 

/* Function to insert a node at the beginning  
of the linked list */
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node =new Node(); 
    /* put in the data */
    new_node.data = new_data; 

    /* link the old list at the end  
    of the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node; 

    return head_ref; 
}  

static Node front,back; 

/* Split the nodes of the given list  
into front and back halves, 
and return the two lists  
using the reference parameters. 
Uses the fast/slow pointer strategy. */
static void frontAndBackSplit( Node head) 
{ 
    Node slow, fast; 

    slow = head; 
    fast = head.next; 

    /* Advance 'fast' two nodes, and  
    advance 'slow' one node */
    while (fast != null) 
    { 
        fast = fast.next; 
        if (fast != null) 
        { 
            slow = slow.next; 
            fast = fast.next; 
        } 
    } 

    /* 'slow' is before the midpoint in the list,  
        so split it in two at that point. */
    front = head; 
    back = slow.next; 
    slow.next = null; 
} 

/* Function to reverse the linked list */
static Node reverseList( Node head_ref) 
{ 
    Node current, prev, next; 
    current = head_ref; 
    prev = null; 
    while (current != null) 
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    }  
    head_ref = prev; 
    return head_ref; 
} 

// perfrom the required subtraction operation  
// on the 1st half of the linked list 
static void modifyTheContentsOf1stHalf() 
{ 
    Node front1 = front, back1 = back; 
    // traversing both the lists simultaneously 
    while (back1 != null) 
    { 
        // subtraction operation and node data 
        // modification 
        front1.data = front1.data - back1.data; 

        front1 = front1.next; 
        back1 = back1.next; 
    } 
} 

// function to concatenate the 2nd(back) list  
// at the end of the 1st(front) list and  
// returns the head of the new list 
static Node concatFrontAndBackList(Node front, 
                                   Node back) 
{ 
    Node head = front; 

    if(front == null)return back; 

    while (front.next != null) 
        front = front.next;  

    front.next = back; 

    return head; 
} 

// function to modify the contents of the linked list 
static Node modifyTheList( Node head) 
{ 
    // if list is empty or contains only single node 
    if (head == null || head.next == null) 
        return head; 
    front = null; back = null; 

    // split the list into two halves 
    // front and back lists 
    frontAndBackSplit(head); 

    // reverse the 2nd(back) list 
    back = reverseList(back); 

    // modify the contents of 1st half  
    modifyTheContentsOf1stHalf(); 

    // agains reverse the 2nd(back) list 
    back = reverseList(back); 

    // concatenating the 2nd list back to the  
    // end of the 1st list 
    head = concatFrontAndBackList(front, back); 

    // pointer to the modified list 
    return head; 
} 

// function to print the linked list 
static void printList( Node head) 
{ 
    if (head == null) 
        return; 

    while (head.next != null) 
    { 
        System.out.print(head.data + " -> "); 
        head = head.next; 
    } 
    System.out.println(head.data ); 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    Node head = null; 

    // creating the linked list 
    head = push(head, 10); 
    head = push(head, 7); 
    head = push(head, 12); 
    head = push(head, 8); 
    head = push(head, 9); 
    head = push(head, 2); 

    // modify the linked list 
    head = modifyTheList(head); 

    // print the modified linked list 
    System.out.println( "Modified List:" ); 
    printList(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python implementation to modify the contents  
# of the linked list 

# Linked list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the beginning  
# of the linked list  
def push(head_ref, new_data): 

    # allocate node  
    new_node =Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list at the end  
    #of the new node  
    new_node.next = head_ref  

    # move the head to point to the new node  
    head_ref = new_node 

    return head_ref 

front = None
back = None

# Split the nodes of the given list  
# into front and back halves, 
# and return the two lists  
# using the reference parameters. 
# Uses the fast/slow pointer strategy.  
def frontAndBackSplit( head): 

    global front 
    global back 
    slow = None
    fast = None

    slow = head 
    fast = head.next

    # Advance 'fast' two nodes, and  
    # advance 'slow' one node  
    while (fast != None): 

        fast = fast.next
        if (fast != None): 
            slow = slow.next
            fast = fast.next

    # 'slow' is before the midpoint in the list,  
    # so split it in two at that point.  
    front = head 
    back = slow.next
    slow.next = None
    return head 

# Function to reverse the linked list  
def reverseList( head_ref): 

    current = None
    prev = None
    next = None
    current = head_ref 
    prev = None
    while (current != None): 

        next = current.next
        current.next = prev 
        prev = current 
        current = next

    head_ref = prev 
    return head_ref 

# perfrom the required subtraction operation  
# on the 1st half of the linked list 
def modifyTheContentsOf1stHalf(): 

    global front 
    global back 
    front1 = front 
    back1 = back 

    # traversing both the lists simultaneously 
    while (back1 != None): 

        # subtraction operation and node data 
        # modification 
        front1.data = front1.data - back1.data 

        front1 = front1.next
        back1 = back1.next

# function to concatenate the 2nd(back) list  
# at the end of the 1st(front) list and  
# returns the head of the new list 
def concatFrontAndBackList( front, back): 

    head = front 

    if(front == None): 
        return back 

    while (front.next != None): 
        front = front.next

    front.next = back 
    return head 

# function to modify the contents of the linked list 
def modifyTheList( head): 

    global front 
    global back 

    # if list is empty or contains only single node 
    if (head == None or head.next == None): 
        return head 
    front = None
    back = None

    # split the list into two halves 
    # front and back lists 
    frontAndBackSplit(head) 

    # reverse the 2nd(back) list 
    back = reverseList(back) 

    # modify the contents of 1st half  
    modifyTheContentsOf1stHalf() 

    # agains reverse the 2nd(back) list 
    back = reverseList(back) 

    # concatenating the 2nd list back to the  
    # end of the 1st list 
    head = concatFrontAndBackList(front, back) 

    # pointer to the modified list 
    return head 

# function to print the linked list 
def printList( head): 

    if (head == None): 
        return

    while (head.next != None): 

        print(head.data , " -> ",end="") 
        head = head.next

    print(head.data ) 

# Driver Code 

head = None

# creating the linked list 
head = push(head, 10) 
head = push(head, 7) 
head = push(head, 12) 
head = push(head, 8) 
head = push(head, 9) 
head = push(head, 2) 

# modify the linked list 
head = modifyTheList(head) 

# print the modified linked list 
print( "Modified List:" ) 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to modify the  
// contents of the linked list 
using System; 

class GFG 
{ 

/* Linked list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

/* Function to insert a node at  
the beginning of the linked list */
static Node push(Node head_ref,  
                  int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list at the end  
    of the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node; 

    return head_ref; 
}  

static Node front, back; 

/* Split the nodes of the given list  
into front and back halves, 
and return the two lists  
using the reference parameters. 
Uses the fast/slow pointer strategy. */
static void frontAndBackSplit( Node head) 
{ 
    Node slow, fast; 

    slow = head; 
    fast = head.next; 

    /* Advance 'fast' two nodes, and  
    advance 'slow' one node */
    while (fast != null) 
    { 
        fast = fast.next; 
        if (fast != null) 
        { 
            slow = slow.next; 
            fast = fast.next; 
        } 
    } 

    /* 'slow' is before the midpoint in the list,  
        so split it in two at that point. */
    front = head; 
    back = slow.next; 
    slow.next = null; 
} 

/* Function to reverse the linked list */
static Node reverseList(Node head_ref) 
{ 
    Node current, prev, next; 
    current = head_ref; 
    prev = null; 
    while (current != null) 
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    }  
    head_ref = prev; 
    return head_ref; 
} 

// perfrom the required subtraction operation  
// on the 1st half of the linked list 
static void modifyTheContentsOf1stHalf() 
{ 
    Node front1 = front, back1 = back; 

    // traversing both the lists simultaneously 
    while (back1 != null) 
    { 
        // subtraction operation and node data 
        // modification 
        front1.data = front1.data - back1.data; 

        front1 = front1.next; 
        back1 = back1.next; 
    } 
} 

// function to concatenate the 2nd(back) list  
// at the end of the 1st(front) list and  
// returns the head of the new list 
static Node concatFrontAndBackList(Node front, 
                                   Node back) 
{ 
    Node head = front; 

    if(front == null) 
        return back; 

    while (front.next != null) 
        front = front.next;  

    front.next = back; 

    return head; 
} 

// function to modify the contents of 
// the linked list 
static Node modifyTheList(Node head) 
{ 
    // if list is empty or contains  
    // only single node 
    if (head == null || head.next == null) 
        return head; 
    front = null; back = null; 

    // split the list into two halves 
    // front and back lists 
    frontAndBackSplit(head); 

    // reverse the 2nd(back) list 
    back = reverseList(back); 

    // modify the contents of 1st half  
    modifyTheContentsOf1stHalf(); 

    // agains reverse the 2nd(back) list 
    back = reverseList(back); 

    // concatenating the 2nd list back to the  
    // end of the 1st list 
    head = concatFrontAndBackList(front, back); 

    // pointer to the modified list 
    return head; 
} 

// function to print the linked list 
static void printList( Node head) 
{ 
    if (head == null) 
        return; 

    while (head.next != null) 
    { 
        Console.Write(head.data + " -> "); 
        head = head.next; 
    } 
    Console.WriteLine(head.data ); 
} 

// Driver Code 
public static void Main() 
{ 
    Node head = null; 

    // creating the linked list 
    head = push(head, 10); 
    head = push(head, 7); 
    head = push(head, 12); 
    head = push(head, 8); 
    head = push(head, 9); 
    head = push(head, 2); 

    // modify the linked list 
    head = modifyTheList(head); 

    // print the modified linked list 
    Console.WriteLine( "Modified List:" ); 
    printList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Modified List:
-8 -> 2 -> -4 -> 12 -> 7 -> 10

```

**时间复杂度**：`O(n)`，其中 **n** 的节点数。

**另一种方法（使用栈）**：

1.找到下半个链表的起点。

2.将后半列表的所有元素推入栈 s 中。

3.使用温度从头开始遍历列表，直到栈不为空

，并通过减去每个节点的栈顶部元素来修改 temp- >数据。

下面是使用栈的实现。

## C++

```cpp

// C++ implementation to modify the 
// contents of the linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Linked list node 
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// function prototype for printing the list 
void printList(struct Node*); 

// Function to insert a node at the 
// beginning of the linked list 
void push(struct Node **head_ref, int new_data) 
{ 

// allocate node 
struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 

// put in the data 
new_node->data = new_data; 

// link the old list at the end of the new node 
new_node->next = *head_ref;  

// move the head to point to the new node 
*head_ref = new_node; 
}  

// function to print the linked list 
void printList(struct Node *head) 
{ 
    if (!head) 
        return; 

    while (head->next != NULL) 
    { 
        cout << head->data << " -> "; 
        head = head->next; 
    } 
    cout << head->data << endl; 
} 

// Function to middle node of list. 
Node* find_mid(Node *head) 
{ 
    Node *temp = head, *slow = head, *fast = head ; 

    while(fast && fast->next) 
    { 

    // Advance 'fast' two nodes, and  
    // advance 'slow' one node 
    slow = slow->next ; 
    fast = fast->next->next ; 
    } 

    // If number of nodes are odd then update slow 
    // by slow->next; 
    if(fast) 
    slow = slow->next ; 

return slow ; 
} 

// function to modify the contents of the linked list. 
void modifyTheList(struct Node *head, struct Node *slow) 
{ 
// Create Stack.  
stack <int> s; 
Node *temp = head ; 

while(slow) 
{ 
    s.push( slow->data ) ; 
    slow = slow->next ; 
} 

// Traverse the list by using temp until stack is empty. 
while( !s.empty() ) 
{ 
    temp->data = temp->data - s.top() ; 
    temp = temp->next ; 
    s.pop() ; 
} 

} 

// Driver program to test above 
int main() 
{ 
    struct Node *head = NULL, *mid ; 

    // creating the linked list 
    push(&head, 10); 
    push(&head, 7); 
    push(&head, 12); 
    push(&head, 8); 
    push(&head, 9); 
    push(&head, 2); 

    // Call Function to Find the starting point of second half of list.  
    mid = find_mid(head) ; 

    // Call function to modify the contents of the linked list. 
    modifyTheList( head, mid); 

    // print the modified linked list 
    cout << "Modified List:" << endl; 
    printList(head); 
    return 0; 
}  

// This is contributed by Mr. Gera 

```

## Java

```java

// Java implementation to modify the 
// contents of the linked list 
import java.util.*; 

class GFG  
{ 

    // Linked list node 
    static class Node  
    { 

        int data; 
        Node next; 
    }; 

    // Function to insert a node at the 
    // beginning of the linked list 
    static Node push(Node head_ref, int new_data)  
    { 

        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list at the end of the new node 
        new_node.next = head_ref; 

        // move the head to point to the new node 
        head_ref = new_node; 
        return head_ref; 
    } 

    // function to print the linked list 
    static void printList(Node head)  
    { 
        if (head == null)  
        { 
            return; 
        } 

        while (head.next != null)  
        { 
            System.out.print(head.data + "->"); 
            head = head.next; 
        } 
        System.out.print(head.data + "\n"); 
    } 

    // Function to middle node of list. 
    static Node find_mid(Node head)  
    { 
        Node temp = head, slow = head, fast = head; 

        while (fast != null && fast.next != null) 
        { 

            // Advance 'fast' two nodes, and  
            // advance 'slow' one node 
            slow = slow.next; 
            fast = fast.next.next; 
        } 

        // If number of nodes are odd then update slow 
        // by slow.next; 
        if (fast != null)  
        { 
            slow = slow.next; 
        } 

        return slow; 
    } 

    // function to modify the contents of the linked list. 
    static void modifyTheList(Node head, Node slow)  
    { 
        // Create Stack.  
        Stack<Integer> s = new Stack<Integer>(); 
        Node temp = head; 

        while (slow != null)  
        { 
            s.add(slow.data); 
            slow = slow.next; 
        } 

    // Traverse the list by using temp until stack is empty. 
        while (!s.empty()) 
        { 
            temp.data = temp.data - s.peek(); 
            temp = temp.next; 
            s.pop(); 
        } 

    } 

    // Driver program to test above 
    public static void main(String[] args) 
    { 
        Node head = null, mid; 

        // creating the linked list 
        head = push(head, 10); 
        head = push(head, 7); 
        head = push(head, 12); 
        head = push(head, 8); 
        head = push(head, 9); 
        head = push(head, 2); 

        // Call Function to Find the starting 
        // point of second half of list.  
        mid = find_mid(head); 

        // Call function to modify  
        // the contents of the linked list. 
        modifyTheList(head, mid); 

        // print the modified linked list 
        System.out.print("Modified List:" + "\n"); 
        printList(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation to modify the 
// contents of the linked list 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Linked list node 
    public class Node  
    { 

        public int data; 
        public Node next; 
    }; 

    // Function to insert a node at the 
    // beginning of the linked list 
    static Node push(Node head_ref, int new_data)  
    { 

        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list at the end of the new node 
        new_node.next = head_ref; 

        // move the head to point to the new node 
        head_ref = new_node; 
        return head_ref; 
    } 

    // function to print the linked list 
    static void printList(Node head)  
    { 
        if (head == null)  
        { 
            return; 
        } 

        while (head.next != null)  
        { 
            Console.Write(head.data + "->"); 
            head = head.next; 
        } 
        Console.Write(head.data + "\n"); 
    } 

    // Function to middle node of list. 
    static Node find_mid(Node head)  
    { 
        Node temp = head, slow = head, fast = head; 

        while (fast != null && fast.next != null) 
        { 

            // Advance 'fast' two nodes, and  
            // advance 'slow' one node 
            slow = slow.next; 
            fast = fast.next.next; 
        } 

        // If number of nodes are odd then update slow 
        // by slow.next; 
        if (fast != null)  
        { 
            slow = slow.next; 
        } 

        return slow; 
    } 

    // function to modify the contents of the linked list. 
    static void modifyTheList(Node head, Node slow)  
    { 
        // Create Stack.  
        Stack<int> s = new Stack<int>(); 
        Node temp = head; 

        while (slow != null)  
        { 
            s.Push(slow.data); 
            slow = slow.next; 
        } 

        // Traverse the list by using temp until stack is empty. 
        while (s.Count != 0) 
        { 
            temp.data = temp.data - s.Peek(); 
            temp = temp.next; 
            s.Pop(); 
        } 

    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head = null, mid; 

        // creating the linked list 
        head = push(head, 10); 
        head = push(head, 7); 
        head = push(head, 12); 
        head = push(head, 8); 
        head = push(head, 9); 
        head = push(head, 2); 

        // Call Function to Find the starting 
        // point of second half of list.  
        mid = find_mid(head); 

        // Call function to modify  
        // the contents of the linked list. 
        modifyTheList(head, mid); 

        // print the modified linked list 
        Console.Write("Modified List:" + "\n"); 
        printList(head); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Modified List:
-8 -> 2 -> -4 -> 12 -> 7 -> 10

```

**时间复杂度**：`O(n)`

**空间复杂度**：O（n / 2）

**参考**：[https://www.careercup.com/question?id=5657550909341696](https://www.careercup.com/question?id=5657550909341696)

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

