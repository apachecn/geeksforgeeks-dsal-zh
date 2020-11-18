# 纠正双链表

中的随机指针

给定一个双向链接列表，其中正好有一个节点指向列表中的随机节点，任务是纠正双向链接列表中的该随机指针，以使其指向预期节点。
**示例：** [

> **输入：**
> 
> ![](img/479ffdc9cd6066ff77acdac2f9aafe97.png)
> 
> **输出：**
> 
> ![](img/81c5c424cb60ada545f52d817c726b76.png)
> 
> **说明：** 2 的下一个指针已更正为指向 3。之前，它指向 1，这是不正确的。

**方法：**这可以通过简单地迭代列表并检查各个指针来实现。
以下是上述方法的实现：

## C++

```cpp

// C++ program to Correct
// the Random Pointer in Doubly Linked List
#include<iostream>
using namespace std; 

// Node of a doubly linked list
class Node
{
    public:
    int data;
    // Pointer to next node in DLL
    Node *next;

      // Pointer to previous node in DLL
    Node *prev;

    Node():prev(NULL),next(NULL){}
    Node(int data):data(data),prev(NULL),next(NULL){}

};
class doublell
{
    public:
    Node *head;
    // Function to append node in the DLL
    void appendNode(Node *n)
    {
        Node *temp=head;
        if(temp==NULL)
        {
            head=n;

        }
        else
        {
            while(temp->next!=NULL)
            {
                temp=temp->next;
            }
            temp->next=n;
            n->prev=temp;
        }
    }
      // Function to print the DLL
    void print()
    {
        Node *temp=head;
        while(temp!=NULL)
        {
            cout<<temp->data<<"->";
            temp=temp->next;
        }
        cout<<endl;
    }
      // Function to print reverse of the DLL
    void printReverse()
    {
        Node *temp=head;
        while(temp->next!=NULL)
        {
            temp=temp->next;
        }
        while(temp!=NULL)
        {
            cout<<temp->data<<" ->";
            temp=temp->prev;
        }
        cout<<endl;
    }
    // Function to correct the random pointer
    void correctPointer()
    {
        if(!head)
        {
            return;
        }
        Node *temp=head;
        while(temp->next!=NULL)
        {
            if(temp->next->prev!=temp)
            {
                temp->next->prev=temp;
            }
            temp=temp->next;
        }
    }
};

// Driver Code
int main() 
{ 

    // Creating a DLL 
    doublell ll;
    ll.head = new Node(1); 
    ll.head->next = new Node(2); 
    ll.head->next->prev = ll.head; 
    ll.head->next->next = new Node(3); 
    ll.head->next->next->prev =ll.head; 
    ll.head->next->next->next = new Node(4); 
    ll.head->next->next->next->prev = ll.head->next->next; 

    cout << "\nIncorrect Linked List: "; 
    ll.print(); 
    ll.printReverse();

    ll.correctPointer(); 

    cout << "\nCorrected Linked List: "; 
    ll.print(); 
    ll.printReverse();

    return 0; 
}

```

## Java

```java

// Java program to Correct
// the Random Pointer in Doubly Linked List
class GFG 
{

// Node of a doubly linked list
static class node 
{
    int data;

    // Pointer to next node in DLL
    node next;

    // Pointer to previous node in DLL
    node prev;
};

// Function to allocate node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.next = temp.prev = null;
    return temp;
}

// Function to correct the random pointer
static void correctPointer(node head)
{
    if (head == null)
        return;

    node temp = head;

    // if head->next's previous is not
    // pointing to head itself,
    // change it.
    if (head.next != null && 
        head.next.prev != head) 
    {
        head.next.prev = head;
        return;
    }

    // If head's previous pointer is incorrect,
    // change it.
    if (head.prev != null) 
    {
        head.prev = null;
        return;
    }

    // Else check for remaining nodes.
    temp = temp.next;
    while (temp != null) 
    {

        // If node.next's previous pointer is
        // incorrect, change it.
        if (temp.next != null && 
            temp.next.prev != temp) 
        {
            temp.next.prev = temp;
            return;
        }

        // Else If node.prev's next pointer is 
        // incorrect, change it.
        else if (temp.prev != null &&
                 temp.prev.next != temp) 
        {
            temp.prev.next = temp;
            return;
        }
        System.out.print("");

        // Else iterate on remaining.
        temp = temp.next;
    }
}

// Function to print the DLL
static void printList(node head)
{
    node temp = head;

    while (temp != null) 
    {

        System.out.print(temp.data + " (");

        // If prev pointer is null, print -1.
        System.out.print((temp.prev != null ?
                          temp.prev.data: -1) + ") ");

        temp = temp.next;
    }
    System.out.print("\n");
}

// Driver Code
public static void main(String[] args)
{
    // Creating a DLL
    node head = newNode(1);
    head.next = newNode(2);
    head.next.prev = head;
    head.next.next = newNode(3);
    head.next.next.prev = head;
    head.next.next.next = newNode(4);
    head.next.next.next.prev = head.next.next;

    System.out.print("\nIncorrect Linked List: ");
    printList(head);

    correctPointer(head);

    System.out.print("\nCorrected Linked List: ");
    printList(head);
}
}

// This code is contributed by Princi Singh

```

## Python3

```py

# Python3 program to Correct the
# Random Pointer in Doubly Linked List

class Node:

    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

# Function to correct the random pointer
def correctPointer(head):

    if head == None:
        return

    temp = head

    # if head.next's previous is not
    # pointing to head itself, change it.
    if (head.next != None and
        head.next.prev != head): 

        head.next.prev = head
        return

    # If head's previous pointer is 
    # incorrect, change it.
    if head.prev != None: 

        head.prev = None
        return

    # Else check for remaining nodes.
    temp = temp.next
    while temp != None: 

        # If node.next's previous pointer 
        # is incorrect, change it.
        if (temp.next != None and
            temp.next.prev != temp): 

            temp.next.prev = temp
            return

        # Else If node.prev's next pointer 
        # is incorrect, change it.
        elif (temp.prev != None and
              temp.prev.next != temp): 

            temp.prev.next = temp
            return

        # Else iterate on remaining.
        temp = temp.next

# Function to print the DLL
def printList(head):

    temp = head

    while temp != None:

        print(temp.data, "(", end = "")

        # If prev pointer is null, print -1.
        if temp.prev == None:
            print(-1, end = ") ")
        else:
            print(temp.prev.data, end = ") ")

        temp = temp.next

    print()

# Driver Code
if __name__ == "__main__":

    # Creating a DLL
    head = Node(1)
    head.next = Node(2)
    head.next.prev = head
    head.next.next = Node(3)
    head.next.next.prev = head
    head.next.next.next = Node(4)
    head.next.next.next.prev = head.next.next

    print("Incorrect Linked List:", 
                         end = " ")
    printList(head)

    correctPointer(head)

    print("\nCorrected Linked List:",
                           end = " ")
    printList(head)

# This code is contributed 
# by Rituraj Jain

```

## C#

```cs

// C# program to Correct the 
// Random Pointer in Doubly Linked List
using System;
class GFG 
{

// Node of a doubly linked list
class node 
{
    public int data;

    // Pointer to next node in DLL
    public node next;

    // Pointer to next node in DLL
    public node prev;
};

// Function to allocate node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.next = temp.prev = null;
    return temp;
}

// Function to correct the random pointer
static void correctPointer(node head)
{
    if (head == null)
        return;

    node temp = head;

    // if head->next's previous is not
    // pointing to head itself,
    // change it.
    if (head.next != null && 
        head.next.prev != head) 
    {
        head.next.prev = head;
        return;
    }

    // If head's previous pointer is incorrect,
    // change it.
    if (head.prev != null) 
    {
        head.prev = null;
        return;
    }

    // Else check for remaining nodes.
    temp = temp.next;
    while (temp != null) 
    {

        // If node.next's previous pointer is
        // incorrect, change it.
        if (temp.next != null && 
            temp.next.prev != temp) 
        {
            temp.next.prev = temp;
            return;
        }

        // Else If node.prev's next pointer 
        // is incorrect, change it.
        else if (temp.prev != null &&
                 temp.prev.next != temp) 
        {
            temp.prev.next = temp;
            return;
        }
        Console.Write("");

        // Else iterate on remaining.
        temp = temp.next;
    }
}

// Function to print the DLL
static void printList(node head)
{
    node temp = head;

    while (temp != null) 
    {
        Console.Write(temp.data + " (");

        // If prev pointer is null, print -1.
        Console.Write((temp.prev != null ?
                       temp.prev.data: -1) + ") ");

        temp = temp.next;
    }
    Console.Write("\n");
}

// Driver Code
public static void Main(String[] args)
{
    // Creating a DLL
    node head = newNode(1);
    head.next = newNode(2);
    head.next.prev = head;
    head.next.next = newNode(3);
    head.next.next.prev = head;
    head.next.next.next = newNode(4);
    head.next.next.next.prev = head.next.next;

    Console.Write("\nIncorrect Linked List: ");
    printList(head);

    correctPointer(head);

    Console.Write("\nCorrected Linked List: ");
    printList(head);
}
}

// This code is contributed by PrinciRaj1992

```

**Output:** 

```
Incorrect Linked List: 1 (-1) 2 (1) 3 (1) 4 (3) 

Corrected Linked List: 1 (-1) 2 (1) 3 (2) 4 (3)

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。