# 反向链接列表

> 原文：[https://www.geeksforgeeks.org/reverse-a-linked-list/](https://www.geeksforgeeks.org/reverse-a-linked-list/)

给定指向链表头节点的指针，任务是反转链表。 我们需要通过更改节点之间的链接来反转列表。

**范例**：

> **输入**：以下链接列表的开头。
> 1- > 2- > 3- > 4- >空
> **输出**：链接列表 应该更改为
> 4- > 3- > 2- > 1- > NULL
> 
> **输入**：以下链接列表的标题。
> 1- > 2- > 3- > 4- > 5- >空
> **输出**：链接列表应更改为
> 5- > 4- > 3- > 2- > 1- > NULL
> 
> **输入**：NULL
> **输出**：NULL
> 
> **输入**：1- >空
> **输出**：1- >空

**迭代方法**

> 1.  初始化三个指针，前一个为 NULL，curr 为头，下一个为 NULL。
> 2.  迭代链接列表。 循环执行以下操作。
>     //在更改当前下一个之前，
>     //存储下一个节点
>     next = curr- > next
>     //现在在当前下一个更改
>     //这是实际可逆的地方 发生
>     curr- > next =上一个
>     //将上一个和 curr 向前移动一个步骤。
>     prev = curr
>     curr =下一个

![](img/db76ab0690faf25cc2f3c83e5c67e6de.png)

下面是上述方法的实现：

## C++

```cpp

// Iterative C++ program to reverse
// a linked list
#include <iostream>
using namespace std;

/* Link list node */
struct Node {
    int data;
    struct Node* next;
    Node(int data)
    {
        this->data = data;
        next = NULL;
    }
};

struct LinkedList {
    Node* head;
    LinkedList() { head = NULL; }

    /* Function to reverse the linked list */
    void reverse()
    {
        // Initialize current, previous and
        // next pointers
        Node* current = head;
        Node *prev = NULL, *next = NULL;

        while (current != NULL) {
            // Store next
            next = current->next;

            // Reverse current node's pointer
            current->next = prev;

            // Move pointers one position ahead.
            prev = current;
            current = next;
        }
        head = prev;
    }

    /* Function to print linked list */
    void print()
    {
        struct Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
    }

    void push(int data)
    {
        Node* temp = new Node(data);
        temp->next = head;
        head = temp;
    }
};

/* Driver code*/
int main()
{
    /* Start with the empty list */
    LinkedList ll;
    ll.push(20);
    ll.push(4);
    ll.push(15);
    ll.push(85);

    cout << "Given linked list\n";
    ll.print();

    ll.reverse();

    cout << "\nReversed Linked list \n";
    ll.print();
    return 0;
}

```

## C

```c

// Iterative C program to reverse a linked list
#include <stdio.h>
#include <stdlib.h>

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

/* Function to reverse the linked list */
static void reverse(struct Node** head_ref)
{
    struct Node* prev = NULL;
    struct Node* current = *head_ref;
    struct Node* next = NULL;
    while (current != NULL) {
        // Store next
        next = current->next;

        // Reverse current node's pointer
        current->next = prev;

        // Move pointers one position ahead.
        prev = current;
        current = next;
    }
    *head_ref = prev;
}

/* Function to push a node */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

/* Function to print linked list */
void printList(struct Node* head)
{
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d  ", temp->data);
        temp = temp->next;
    }
}

/* Driver code*/
int main()
{
    /* Start with the empty list */
    struct Node* head = NULL;

    push(&head, 20);
    push(&head, 4);
    push(&head, 15);
    push(&head, 85);

    printf("Given linked list\n");
    printList(head);
    reverse(&head);
    printf("\nReversed Linked list \n");
    printList(head);
    getchar();
}

```

## Java

```java

// Java program for reversing the linked list

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

    /* Function to reverse the linked list */
    Node reverse(Node node)
    {
        Node prev = null;
        Node current = node;
        Node next = null;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        node = prev;
        return node;
    }

    // prints content of double linked list
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();
        list.head = new Node(85);
        list.head.next = new Node(15);
        list.head.next.next = new Node(4);
        list.head.next.next.next = new Node(20);

        System.out.println("Given Linked list");
        list.printList(head);
        head = list.reverse(head);
        System.out.println("");
        System.out.println("Reversed linked list ");
        list.printList(head);
    }
}

// This code has been contributed by Mayank Jaiswal

```

## Python

```py

# Python program to reverse a linked list
# Time Complexity : O(n)
# Space Complexity : O(1)

# Node class

class Node:

    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Function to reverse the linked list
    def reverse(self):
        prev = None
        current = self.head
        while(current is not None):
            next = current.next
            current.next = prev
            prev = current
            current = next
        self.head = prev

    # Function to insert a new node at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Utility function to print the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

# Driver code
llist = LinkedList()
llist.push(20)
llist.push(4)
llist.push(15)
llist.push(85)

print "Given Linked List"
llist.printList()
llist.reverse()
print "\nReversed Linked List"
llist.printList()

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)

```

## C#

```cs

// C# program for reversing the linked list
using System;

class GFG {

    // Driver Code
    static void Main(string[] args)
    {
        LinkedList list = new LinkedList();
        list.AddNode(new LinkedList.Node(85));
        list.AddNode(new LinkedList.Node(15));
        list.AddNode(new LinkedList.Node(4));
        list.AddNode(new LinkedList.Node(20));

        // List before reversal
        Console.WriteLine("Given linked list:");
        list.PrintList();

        // Reverse the list
        list.ReverseList();

        // List after reversal
        Console.WriteLine("Reversed linked list:");
        list.PrintList();
    }
}

class LinkedList {
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

    // function to add a new node at
    // the end of the list
    public void AddNode(Node node)
    {
        if (head == null)
            head = node;
        else {
            Node temp = head;
            while (temp.next != null) {
                temp = temp.next;
            }
            temp.next = node;
        }
    }

    // function to reverse the list
    public void ReverseList()
    {
        Node prev = null, current = head, next = null;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }

    // function to print the list data
    public void PrintList()
    {
        Node current = head;
        while (current != null) {
            Console.Write(current.data + " ");
            current = current.next;
        }
        Console.WriteLine();
    }
}

// This code is contributed by Mayank Sharma

```

**输出**：

```
Given linked list
85 15 4 20 
Reversed Linked list 
20 4 15 85 

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`

**递归方法**：

```
   1) Divide the list in two parts - first node and 
      rest of the linked list.
   2) Call reverse for the rest of the linked list.
   3) Link rest to first.
   4) Fix head pointer 

```

![Linked List Rverse](img/c42997b58f1bb0fb445bc20c05d0a4d5.png)

## C++

```cpp

// Recursive C++ program to reverse
// a linked list
#include <iostream>
using namespace std;

/* Link list node */
struct Node {
    int data;
    struct Node* next;
    Node(int data)
    {
        this->data = data;
        next = NULL;
    }
};

struct LinkedList {
    Node* head;
    LinkedList()
    {
        head = NULL;
    }

    Node* reverse(Node* head)
    {
        if (head == NULL || head->next == NULL)
            return head;

        /* reverse the rest list and put 
          the first element at the end */
        Node* rest = reverse(head->next);
        head->next->next = head;

        /* tricky step -- see the diagram */
        head->next = NULL;

        /* fix the head pointer */
        return rest;
    }

    /* Function to print linked list */
    void print()
    {
        struct Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
    }

    void push(int data)
    {
        Node* temp = new Node(data);
        temp->next = head;
        head = temp;
    }
};

/* Driver program to test above function*/
int main()
{
    /* Start with the empty list */
    LinkedList ll;
    ll.push(20);
    ll.push(4);
    ll.push(15);
    ll.push(85);

    cout << "Given linked list\n";
    ll.print();

    ll.head = ll.reverse(ll.head);

    cout << "\nReversed Linked list \n";
    ll.print();
    return 0;
}

```

## Java

```java

// Recursive Java program to reverse
// a linked list
class recursion { 
    static Node head; // head of list 

    static class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    static Node reverse(Node head) 
    { 
        if (head == null || head.next == null) 
            return head; 

        /* reverse the rest list and put 
        the first element at the end */
        Node rest = reverse(head.next); 
        head.next.next = head; 

        /* tricky step -- see the diagram */
        head.next = null; 

        /* fix the head pointer */
        return rest; 
    } 

    /* Function to print linked list */
    static void print() 
    { 
        Node temp = head; 
        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println();
    } 

    static void push(int data) 
    { 
        Node temp = new Node(data); 
        temp.next = head; 
        head = temp; 
    } 

/* Driver program to test above function*/
public static void main(String args[]) 
{ 
    /* Start with the empty list */

    push(20); 
    push(4); 
    push(15); 
    push(85); 

    System.out.println("Given linked list"); 
    print(); 

    head = reverse(head); 

    System.out.println("Reversed Linked list"); 
    print(); 
}
}

// This code is contributed by Prakhar Agarwal

```

## Python3

```py

"""Python3 program to reverse linked list
using recursive method"""

# Linked List Node
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Create and Handle list operations
class LinkedList:
    def __init__(self):
        self.head = None # Head of list

    # Method to reverse the list
    def reverse(self, head):

        # If head is empty or has reached the list end
        if head is None or head.next is None:
            return head

        # Reverse the rest list
        rest = self.reverse(head.next)

        # Put first element at the end
        head.next.next = head
        head.next = None

        # Fix the header pointer
        return rest

    # Returns the linked list in display format
    def __str__(self):
        linkedListStr = ""
        temp = self.head
        while temp:
            linkedListStr = (linkedListStr +
                            str(temp.data) + " ")
            temp = temp.next
        return linkedListStr

    # Pushes new data to the head of the list
    def push(self, data):
        temp = Node(data)
        temp.next = self.head
        self.head = temp

# Driver code
linkedList = LinkedList()
linkedList.push(20)
linkedList.push(4)
linkedList.push(15)
linkedList.push(85)

print("Given linked list")
print(linkedList)

linkedList.head = linkedList.reverse(linkedList.head)

print("Reversed linked list")
print(linkedList)

# This code is contributed by Debidutta Rath

```

## C#

```cs

// Recursive C# program to 
// reverse a linked list
using System;
class recursion{ 

// Head of list 
static Node head; 

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

static Node reverse(Node head) 
{ 
  if (head == null || 
      head.next == null) 
    return head; 

  // Reverse the rest list and put  
  // the first element at the end
  Node rest = reverse(head.next); 
  head.next.next = head; 

  // Tricky step -- 
  // see the diagram
  head.next = null; 

  // Fix the head pointer
  return rest; 
} 

// Function to print 
// linked list 
static void print() 
{ 
  Node temp = head; 
  while (temp != null) 
  { 
    Console.Write(temp.data + " "); 
    temp = temp.next; 
  } 
  Console.WriteLine();
} 

static void push(int data) 
{ 
  Node temp = new Node(data); 
  temp.next = head; 
  head = temp; 
} 

// Driver code
public static void Main(String []args) 
{ 
  // Start with the 
  // empty list
  push(20); 
  push(4); 
  push(15); 
  push(85); 

  Console.WriteLine("Given linked list"); 
  print(); 
  head = reverse(head); 
  Console.WriteLine("Reversed Linked list"); 
  print(); 
}
}

// This code is contributed by gauravrajput1

```

**输出**：

```
Given linked list
85 15 4 20 
Reversed Linked list
20 4 15 85 

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`

**一种更简单且尾部递归的方法**

下面是此方法的实现。

## C++

```cpp

// A simple and tail recursive C++ program to reverse
// a linked list
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* next;
};

void reverseUtil(Node* curr, Node* prev, Node** head);

// This function mainly calls reverseUtil()
// with prev as NULL
void reverse(Node** head)
{
    if (!head)
        return;
    reverseUtil(*head, NULL, head);
}

// A simple and tail-recursive function to reverse
// a linked list.  prev is passed as NULL initially.
void reverseUtil(Node* curr, Node* prev, Node** head)
{
    /* If last node mark it head*/
    if (!curr->next) {
        *head = curr;

        /* Update next to prev node */
        curr->next = prev;
        return;
    }

    /* Save curr->next node for recursive call */
    Node* next = curr->next;

    /* and update next ..*/
    curr->next = prev;

    reverseUtil(next, curr, head);
}

// A utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->data = key;
    temp->next = NULL;
    return temp;
}

// A utility function to print a linked list
void printlist(Node* head)
{
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Driver code
int main()
{
    Node* head1 = newNode(1);
    head1->next = newNode(2);
    head1->next->next = newNode(3);
    head1->next->next->next = newNode(4);
    head1->next->next->next->next = newNode(5);
    head1->next->next->next->next->next = newNode(6);
    head1->next->next->next->next->next->next = newNode(7);
    head1->next->next->next->next->next->next->next
        = newNode(8);
    cout << "Given linked list\n";
    printlist(head1);
    reverse(&head1);
    cout << "\nReversed linked list\n";
    printlist(head1);
    return 0;
}

```

## Java

```java

// Java program for reversing the Linked list

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

    // A simple and tail recursive function to reverse
    // a linked list.  prev is passed as NULL initially.
    Node reverseUtil(Node curr, Node prev)
    {
        /*If head is initially null OR list is empty*/
        if (head == null)
            return head;
        /* If last node mark it head*/
        if (curr.next == null) {
            head = curr;

            /* Update next to prev node */
            curr.next = prev;

            return head;
        }

        /* Save curr->next node for recursive call */
        Node next1 = curr.next;

        /* and update next ..*/
        curr.next = prev;

        reverseUtil(next1, curr);
        return head;
    }

    // prints content of double linked list
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next
            = new Node(7);
        list.head.next.next.next.next.next.next.next
            = new Node(8);

        System.out.println("Original Linked list ");
        list.printList(head);
        Node res = list.reverseUtil(head, null);
        System.out.println("");
        System.out.println("");
        System.out.println("Reversed linked list ");
        list.printList(res);
    }
}

// This code has been contributed by Mayank Jaiswal

```

## Python

```py

# Simple and tail recursive Python program to
# reverse a linked list

# Node class

class Node:

    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    def reverseUtil(self, curr, prev):

        # If last node mark it head
        if curr.next is None:
            self.head = curr

            # Update next to prev node
            curr.next = prev
            return

        # Save curr.next node for recursive call
        next = curr.next

        # And update next
        curr.next = prev

        self.reverseUtil(next, curr)

    # This function mainly calls reverseUtil()
    # with previous as None

    def reverse(self):
        if self.head is None:
            return
        self.reverseUtil(self.head, None)

    # Function to insert a new node at the beginning

    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Utility function to print the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

# Driver code
llist = LinkedList()
llist.push(8)
llist.push(7)
llist.push(6)
llist.push(5)
llist.push(4)
llist.push(3)
llist.push(2)
llist.push(1)

print "Given linked list"
llist.printList()

llist.reverse()

print "\nReverse linked list"
llist.printList()

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)

```

## C#

```cs

// C# program for reversing the Linked list
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

    // A simple and tail-recursive function to reverse
    // a linked list. prev is passed as NULL initially.
    Node reverseUtil(Node curr, Node prev)
    {

        /* If last node mark it head*/
        if (curr.next == null) {
            head = curr;

            /* Update next to prev node */
            curr.next = prev;

            return head;
        }

        /* Save curr->next node for recursive call */
        Node next1 = curr.next;

        /* and update next ..*/
        curr.next = prev;

        reverseUtil(next1, curr);
        return head;
    }

    // prints content of double linked list
    void printList(Node node)
    {
        while (node != null) {
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = new Node(4);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next
            = new Node(7);
        list.head.next.next.next.next.next.next.next
            = new Node(8);

        Console.WriteLine("Original Linked list ");
        list.printList(list.head);
        Node res = list.reverseUtil(list.head, null);
        Console.WriteLine("");
        Console.WriteLine("");
        Console.WriteLine("Reversed linked list ");
        list.printList(res);
    }
}

// This code contributed by Rajput-Ji

```

**Output**

```
Given linked list
1 2 3 4 5 6 7 8 

Reversed linked list
8 7 6 5 4 3 2 1 

```

**使用堆栈**：

*   将节点（值和地址）存储在堆栈中，直到输入所有值。

*   完成所有输入后，将 Head 指针更新到最后一个位置（即最后一个值）。

*   开始弹出节点（值和地址）并以相同顺序存储它们，直到堆栈为空。

*   用 NULL 更新堆栈中最后一个节点的下一个指针。

下面是上述方法的实现：

## C++

```cpp

// C++ program for above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Create a class Node to enter 
// values and address in the list
class Node 
{
public:
    int data;
    Node* next;
};

// Function to reverse the 
// linked list
void reverseLL(Node** head)
{   

    // Create a stack "s" 
    // of Node type
    stack<Node*> s; 
    Node* temp = *head;
    while (temp->next != NULL) 
    {

        // Push all the nodes 
        // in to stack
        s.push(temp); 
        temp = temp->next;
    }
    *head = temp;

    while (!s.empty()) 
    {

        // Store the top value of
        // stack in list
        temp->next = s.top(); 

        // Pop the value from stack
        s.pop(); 

        // update the next pointer in the
        // in the list
        temp = temp->next; 
    }
    temp->next = NULL;
}

// Function to Display 
// the elements in List
void printlist(Node* temp) 
{
    while (temp != NULL) 
    {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Program to insert back of the 
// linked list
void insert_back(Node** head, int value)
{ 

    // we have used insertion at back method
    // to enter values in the list.(eg:
    // head->1->2->3->4->Null)
    Node* temp = new Node();
    temp->data = value;
    temp->next = NULL;

    // If *head equals to NULL
    if (*head == NULL) 
    {
      *head = temp;
      return;
    }
    else
    {
      Node* last_node = *head;
      while (last_node->next != NULL) 
      {
        last_node = last_node->next;
      }
      last_node->next = temp;
      return;
    }
}

// Driver Code
int main()
{
    Node* head = NULL;

    insert_back(&head, 1);
    insert_back(&head, 2);
    insert_back(&head, 3);
    insert_back(&head, 4);
    cout << "Given linked list\n";
    printlist(head);
    reverseLL(&head);
    cout << "\nReversed linked list\n";
    printlist(head);
    return 0;
}

```

**Output**

```
Given linked list
1 2 3 4 
Reversed linked list
4 3 2 1 
```

感谢 Gaurav Ahirwar 提出了此解决方案。

[递归地反向链接列表（一个简单的实现）](https://www.geeksforgeeks.org/recursively-reversing-a-linked-list-a-simple-implementation/)

[仅使用 2 个指针迭代反向链接的列表（一种有趣的方法）](https://www.geeksforgeeks.org/iteratively-reverse-a-linked-list-using-only-2-pointers/)

**参考**：

[http://cslibrary.stanford.edu/105/LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)

