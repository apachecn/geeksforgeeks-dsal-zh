# 以递归方式反向链接列表（简单实现）

给定指向链接列表头节点的指针，任务是递归地反向链接列表。 我们需要通过更改节点之间的链接来反转列表。

**示例：**

```
Input : Head of following linked list  
       1->2->3->4->NULL
Output : Linked list should be changed to,
       4->3->2->1->NULL

Input : Head of following linked list  
       1->2->3->4->5->NULL
Output : Linked list should be changed to,
       5->4->3->2->1->NULL

Input : NULL
Output : NULL

Input  : 1->NULL
Output : 1->NULL

```

在上一篇关于反向链接列表的文章[中，我们讨论了一种迭代和两种递归方法。](https://www.geeksforgeeks.org/reverse-a-linked-list/)

在通过传递单个指针来反转链表的方法中，我们试图做的是将当前节点的上一个节点作为其下一个节点来反转链表。

1.  我们将下一个节点的指针返回到他的上一个（当前）节点，然后使上一个节点成为返回节点的下一个节点，然后返回当前节点。
2.  我们首先遍历最后一个节点，并使最后一个节点成为反向链表的头节点，然后以递归的方式应用上述过程。

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

    /* Function to reverse the linked list */
    Node* reverse(Node* node) 
    { 
        if (node == NULL) 
            return NULL; 
        if (node->next == NULL) { 
            head = node; 
            return node; 
        } 
        Node* node1 = reverse(node->next); 
        node1->next = node; 
        node->next = NULL; 
        return node; 
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

    ll.reverse(ll.head); 

    cout << "\nReversed Linked list \n"; 
    ll.print(); 
    return 0; 
} 

```

## Java

```java

// Recursive Java program to reverse 
// a linked list 
import java.io.BufferedWriter; 
import java.io.IOException; 
import java.io.OutputStreamWriter; 
import java.util.Scanner; 

public class ReverseLinkedListRecursive { 

    /* Link list node */
    static class Node { 
        public int data; 
        public Node next; 

        public Node(int nodeData) { 
            this.data = nodeData; 
            this.next = null; 
        } 
    } 

    static class LinkedList { 
        public Node head; 

        public LinkedList() { 
            this.head = null; 
        } 

        public void insertNode(int nodeData) { 
            Node node = new Node(nodeData); 

            if (this.head != null) { 
                node.next = head; 
            }  
            this.head = node; 
        } 
    } 

    /* Function to print linked list */
    public static void printSinglyLinkedList(Node node, 
                        String sep) throws IOException { 
        while (node != null) { 
            System.out.print(String.valueOf(node.data) + sep); 
            node = node.next; 
        } 
    } 

    // Complete the reverse function below. 
    static Node reverse(Node head) { 
        if(head == null) { 
            return head; 
        } 

        // last node or only one node 
        if(head.next == null) { 
            return head; 
        } 

        Node newHeadNode = reverse(head.next); 

        // change references for middle chain 
        head.next.next = head; 
        head.next = null; 

        // send back new head node in every recursion 
        return newHeadNode; 
    } 

    private static final Scanner scanner = new Scanner(System.in); 

    public static void main(String[] args) throws IOException { 
            LinkedList llist = new LinkedList(); 

            llist.insertNode(20); 
            llist.insertNode(4); 
            llist.insertNode(15); 
            llist.insertNode(85); 

            System.out.println("Given linked list:"); 
            printSinglyLinkedList(llist.head, " "); 

            System.out.println(); 
            System.out.println("Reversed Linked list:"); 
            Node llist1 = reverse(llist.head); 
            printSinglyLinkedList(llist1, " "); 

        scanner.close(); 
    } 
} 

```

## Python3

```py

# Recursive Python3 program to reverse 
# a linked list 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

def LinkedList(): 
    head = None

# Function to reverse the linked list  
def reverse(node): 
    if (node == None): 
        return node 

    if (node.next == None): 
        return node 

    node1 = reverse(node.next) 
    node.next.next = node 
    node.next = None
    return node1 

# Function to print linked list  
def printList(): 
    temp = head 
    while (temp != None) : 
        print(temp.data, end = " ") 
        temp = temp.next

def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Driver Code 
if __name__=='__main__':  

    # Start with the empty list  
    head = LinkedList() 
    head = push(head, 20) 
    head = push(head, 4) 
    head = push(head, 15) 
    head = push(head, 85) 

    print("Given linked list") 
    printList() 

    head = reverse(head) 

    print("\nReversed Linked list") 
    printList() 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// Recursive C# program to reverse 
// a linked list 
using System; 

public class ReverseLinkedListRecursive  
{ 

    /* Link list node */
    public class Node  
    { 
        public int data; 
        public Node next; 

        public Node(int nodeData)  
        { 
            this.data = nodeData; 
            this.next = null; 
        } 
    } 

    class LinkedList  
    { 
        public Node head; 

        public LinkedList() 
        { 
            this.head = null; 
        } 

        public void insertNode(int nodeData)  
        { 
            Node node = new Node(nodeData); 

            if (this.head != null) 
            { 
                node.next = head; 
            }  
            this.head = node; 
        } 
    } 

    /* Function to print linked list */
    public static void printSinglyLinkedList(Node node, 
                        String sep) 
    { 
        while (node != null)  
        { 
            Console.Write(node.data + sep); 
            node = node.next; 
        } 
    } 

    // Complete the reverse function below. 
    static Node reverse(Node head)  
    { 
        if(head == null)  
        { 
            return head; 
        } 

        // last node or only one node 
        if(head.next == null)  
        { 
            return head; 
        } 

        Node newHeadNode = reverse(head.next); 

        // change references for middle chain 
        head.next.next = head; 
        head.next = null; 

        // send back new head  
        // node in every recursion 
        return newHeadNode; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
            LinkedList llist = new LinkedList(); 

            llist.insertNode(20); 
            llist.insertNode(4); 
            llist.insertNode(15); 
            llist.insertNode(85); 

            Console.WriteLine("Given linked list:"); 
            printSinglyLinkedList(llist.head, " "); 

            Console.WriteLine(); 
            Console.WriteLine("Reversed Linked list:"); 
            Node llist1 = reverse(llist.head); 
            printSinglyLinkedList(llist1, " "); 
    } 
} 

// This code has been contributed by Rajput-Ji  

```

**Output:**

```
Given linked list
85 15 4 20 
Reversed Linked list 
20 4 15 85

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。