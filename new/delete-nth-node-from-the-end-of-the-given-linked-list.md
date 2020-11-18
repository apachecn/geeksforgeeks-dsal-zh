# 从给定链接列表

的末尾删除第N个节点

给定一个链表和一个整数 **N** ，任务是从给定链表的末尾删除 **N <sup>N个</sup>** 节点。

**示例：**

> **输入：** 2-> 3-> 1-> 7->空，N = 1
> **输出：**
> 已创建链接列表 是：
> 2 3 1 7
> 删除后的链接列表是：
> 2 3 1
> 
> **输入：** 1-> 2-> 3-> 4->空，N = 4
> **输出：**
> 已创建链接列表 是：
> 1 2 3 4
> 删除后的链接列表是：
> 2 3 4

**方法：**

*   带两个指针，**第一个**指向链接列表的**头**，第二个指向 **N <sup>th</sup> [** 节点从头开始。
*   现在，使两个指针同时增加一个，直到第二个指针指向链接列表的最后一个节点。
*   从上一步开始进行操作之后，从现在开始，第一个指针应该指向第 **N <sup>个</sup>** 节点。 因此，删除节点第一个指针指向的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include<bits/stdc++.h> 
using namespace std; 

class LinkedList 
{ 
    public: 

    // Linked list Node 
    class Node 
    { 
        public: 
        int data; 
        Node* next; 
        Node(int d) 
        { 
            data = d; 
            next = NULL; 
        } 
    }; 

    // Head of list 
    Node* head; 

    // Function to delete the nth node from 
    // the end of the given linked list 
    Node* deleteNode(int key) 
    { 

        // First pointer will point to 
        // the head of the linked list 
        Node *first = head; 

        // Second pointer will point to the 
        // Nth node from the beginning 
        Node *second = head; 
        for (int i = 0; i < key; i++) 
        { 

            // If count of nodes in the given 
            // linked list is <= N 
            if (second->next == NULL)  
            { 

                // If count = N i.e. 
                // delete the head node 
                if (i == key - 1) 
                    head = head->next; 
                return head; 
            } 
            second = second->next; 
        } 

        // Increment both the pointers by one until 
        // second pointer reaches the end 
        while (second->next != NULL) 
        { 
            first = first->next; 
            second = second->next; 
        } 

        // First must be pointing to the 
        // Nth node from the end by now 
        // So, delete the node first is pointing to 
        first->next = first->next->next; 
        return head; 
    } 

    // Function to insert a new Node  
    // at front of the list 
    Node* push(int new_data) 
    { 
        Node* new_node = new Node(new_data); 
        new_node->next = head; 
        head = new_node; 
        return head; 
    } 

    // Function to print the linked list 
    void printList() 
    { 
        Node* tnode = head; 
        while (tnode != NULL)  
        { 
            cout << (tnode->data) << ( " "); 
            tnode = tnode->next; 
        } 
    } 
}; 

// Driver code 
int main() 
{ 
    LinkedList* llist = new LinkedList(); 

    llist->head = llist->push(7); 
    llist->head = llist->push(1); 
    llist->head = llist->push(3); 
    llist->head = llist->push(2); 

    cout << ("Created Linked list is:\n"); 
    llist->printList(); 

    int N = 1; 
    llist->head = llist->deleteNode(N); 

    cout << ("\nLinked List after Deletion is:\n"); 
    llist->printList(); 
} 

// This code is contributed by Arnab Kundu  

```

## Java

```java

// Java implementation of the approach 
class LinkedList { 

    // Head of list 
    Node head; 

    // Linked list Node 
    class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    // Function to delete the nth node from 
    // the end of the given linked list 
    void deleteNode(int key) 
    { 

        // First pointer will point to 
        // the head of the linked list 
        Node first = head; 

        // Second pointer will point to the 
        // Nth node from the beginning 
        Node second = head; 
        for (int i = 0; i < key; i++) { 

            // If count of nodes in the given 
            // linked list is <= N 
            if (second.next == null) { 

                // If count = N i.e. delete the head node 
                if (i == key - 1) 
                    head = head.next; 
                return; 
            } 
            second = second.next; 
        } 

        // Increment both the pointers by one until 
        // second pointer reaches the end 
        while (second.next != null) { 
            first = first.next; 
            second = second.next; 
        } 

        // First must be pointing to the 
        // Nth node from the end by now 
        // So, delete the node first is pointing to 
        first.next = first.next.next; 
    } 

    // Function to insert a new Node at front of the list 
    public void push(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
    } 

    // Function to print the linked list 
    public void printList() 
    { 
        Node tnode = head; 
        while (tnode != null) { 
            System.out.print(tnode.data + " "); 
            tnode = tnode.next; 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 

        llist.push(7); 
        llist.push(1); 
        llist.push(3); 
        llist.push(2); 

        System.out.println("\nCreated Linked list is:"); 
        llist.printList(); 

        int N = 1; 
        llist.deleteNode(N); 

        System.out.println("\nLinked List after Deletion is:"); 
        llist.printList(); 
    } 
} 

```

## Python3

```py

# Python3 implementation of the approach 
class Node:  
    def __init__(self, new_data):  
        self.data = new_data  
        self.next = None
class LinkedList: 
    def __init__(self): 
        self.head = None

    # createNode and and make linked list  
    def push(self, new_data):  
        new_node = Node(new_data)  
        new_node.next = self.head  
        self.head = new_node  

    def deleteNode(self, n): 
        first = self.head 
        second = self.head 
        for i in range(n): 

            # If count of nodes in the  
            # given list is less than 'n' 
            if(second.next == None): 

                # If index = n then  
                # delete the head node 
                if(i == n - 1): 
                    self.head = self.head.next
                return self.head 
            second = second.next

        while(second.next != None): 
            second = second.next
            first = first.next

        first.next = first.next.next

    def printList(self): 
        tmp_head = self.head 
        while(tmp_head != None): 
            print(tmp_head.data, end = ' ') 
            tmp_head = tmp_head.next

# Driver Code 
llist = LinkedList()  
llist.push(7)  
llist.push(1)  
llist.push(3)  
llist.push(2)  
print("Created Linked list is:") 
llist.printList() 
llist.deleteNode(1)  
print("\nLinked List after Deletion is:") 
llist.printList() 

# This code is contributed by RaviParkash 

```

## C#

```cs

// C# implementation of the approach 
using System; 

public class LinkedList 
{ 

    // Head of list 
    public Node head; 

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

    // Function to delete the nth node from 
    // the end of the given linked list 
    void deleteNode(int key) 
    { 

        // First pointer will point to 
        // the head of the linked list 
        Node first = head; 

        // Second pointer will point to the 
        // Nth node from the beginning 
        Node second = head; 
        for (int i = 0; i < key; i++)  
        { 

            // If count of nodes in the given 
            // linked list is <= N 
            if (second.next == null)  
            { 

                // If count = N i.e. delete the head node 
                if (i == key - 1) 
                    head = head.next; 
                return; 
            } 
            second = second.next; 
        } 

        // Increment both the pointers by one until 
        // second pointer reaches the end 
        while (second.next != null)  
        { 
            first = first.next; 
            second = second.next; 
        } 

        // First must be pointing to the 
        // Nth node from the end by now 
        // So, delete the node first is pointing to 
        first.next = first.next.next; 
    } 

    // Function to insert a new Node at front of the list 
    public void push(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
    } 

    // Function to print the linked list 
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
        LinkedList llist = new LinkedList(); 

        llist.push(7); 
        llist.push(1); 
        llist.push(3); 
        llist.push(2); 

        Console.WriteLine("\nCreated Linked list is:"); 
        llist.printList(); 

        int N = 1; 
        llist.deleteNode(N); 

        Console.WriteLine("\nLinked List after Deletion is:"); 
        llist.printList(); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Created Linked list is:
2 3 1 7 
Linked List after Deletion is:
2 3 1

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。