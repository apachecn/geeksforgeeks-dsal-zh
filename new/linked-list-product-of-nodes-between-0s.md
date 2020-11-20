# 节点之间的链表乘积为 0

> 原文：[https://www.geeksforgeeks.org/linked-list-product-of-nodes-between-0s/](https://www.geeksforgeeks.org/linked-list-product-of-nodes-between-0s/)

给定一个链表，其中包含一系列用“ 0”分隔的数字。 生产它们并就地存储在链表中。

**注意**：输入中不会存在连续的零。

**范例**：

```
Input  : 1->2->3->0->5->4->0->3->2->0
Output : 6->20->6

Input  : 1->2->3->4
Output : 1->2->3->4

```

**方法**：

1.  开始遍历链表的节点。

2.  在 temp.data！= 0 时进行迭代，并将这些数据乘积为变量“ prod”。

3.  当您遇到 0 作为节点数据时，请更改先前节点的指针。

下面是上述方法的实现：

## C++

```cpp

// C++ program to in-place product linked list 
// nodes between 0s 
#include<bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node  
{ 
    int data; 
    Node* next; 
    Node(int d) 
    { 
        data = d; 
        next = NULL; 
    } 
}; 

// Function to traverse and print Linked List 
    void printList(Node* head) 
    { 
        while (head->next != NULL)  
        { 
            cout<<head->data <<"-> "; 
                head = head->next; 
        } 
        cout << head->data << "\n"; 
    } 

// Function to in-place product linked list 
// nodes between 0s 

    // Function to store numbers till 0 
    void inPlaceStore(Node* head) 
    { 
        if (head->data == 0)  
        { 
            head = head->next; 
        } 

        // To store modified list 
        Node* res = head; 

        // Traverse linked list and keep 
        // adding nodes between 0s. 
        Node* temp = head; 
        int prod = 1; 
        while (temp != NULL) 
        { 

            // loop to product the data of nodes till 
            // it encounters 0 
            if (temp->data != 0) 
            { 
                prod *= temp->data; 
                temp = temp->next; 
            } 

            // If we encounters 0, we need 
            // to update next pointers 
            else
            { 

                res->data = prod; 
                res->next = temp->next; 
                temp = temp->next; 
                res = res->next; 
                prod = 1; 
            } 
        } 

        // For the last segment 
        res->data = prod; 
        res->next = temp; 

        printList(head); 
    } 

    // Driver Code 
    int main() 
    { 
        Node *head = new Node(3); 
        head->next = new Node(2); 
        head->next->next = new Node(0); 
        head->next->next->next = new Node(4); 
        head->next->next->next->next = new Node(5); 
        head->next->next->next->next->next = new Node(0); 
        head->next->next->next->next->next->next = new Node(6); 
        head->next->next->next->next->next->next->next = new Node(7); 
        inPlaceStore(head); 
        return 0; 
    } 

// This code is contributed by Arnab Kundu 

```

## Java

```java

// Java program to in-place product linked list 
// nodes between 0s 

// Linked List Node 
class Node { 
    int data; 
    Node next; 

    public Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

// Function to in-place product linked list 
// nodes between 0s 
public class inPlaceStoreLL { 

    // Function to store numbers till 0 
    static void inPlaceStore(Node head) 
    { 
        if (head.data == 0) { 
            head = head.next; 
        } 

        // To store modified list 
        Node res = head; 

        // Traverse linked list and keep 
        // adding nodes between 0s. 
        Node temp = head; 
        int prod = 1; 
        while (temp != null) { 

            // loop to product the data of nodes till 
            // it encounters 0 
            if (temp.data != 0) { 
                prod *= temp.data; 
                temp = temp.next; 
            } 

            // If we encounters 0, we need 
            // to update next pointers 
            else { 

                res.data = prod; 
                res.next = temp.next; 
                temp = temp.next; 
                res = res.next; 
                prod = 1; 
            } 
        } 

        // For the last segment 
        res.data = prod; 
        res.next = temp; 

        printList(head); 
    } 

    // Function to traverse and print Linked List 
    static void printList(Node head) 
    { 
        while (head.next != null) { 
            System.out.print(head.data + "-> "); 
            head = head.next; 
        } 
        System.out.println(head.data); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        Node head = new Node(3); 
        head.next = new Node(2); 
        head.next.next = new Node(0); 
        head.next.next.next = new Node(4); 
        head.next.next.next.next = new Node(5); 
        head.next.next.next.next.next = new Node(0); 
        head.next.next.next.next.next.next = new Node(6); 
        head.next.next.next.next.next.next.next = new Node(7); 
        inPlaceStore(head); 
    } 
} 

```

## Python3

```py

# Python3 program to in-place  
# product linked list nodes between 0s 
import math 

# Linked List Node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to traverse and pr Linked List 
def prList(head): 
        while (head.next != None): 
            print(head.data, end = "->") 
            head = head.next

        print(head.data) 
        print() 

# Function to in-place product linked list 
# nodes between 0s 

# Function to store numbers till 0 
def inPlaceStore(head): 
        if (head.data == 0): 
            head = head.next

        # To store modified list 
        res = head 

        # Traverse linked list and keep 
        # adding nodes between 0s. 
        temp = head 
        prod = 1
        while (temp != None): 

            # loop to product the data of nodes till 
            # it encounters 0 
            if (temp.data != 0): 
                prod = prod * temp.data 
                temp = temp.next

            # If we encounters 0, we need 
            # to update next poers 
            else: 

                res.data = prod 
                res.next = temp.next
                temp = temp.next
                res = res.next
                prod = 1

        # For the last segment 
        res.data = prod 
        res.next = temp 

        prList(head) 

# Driver Code 
if __name__=='__main__': 
    head = Node(3) 
    head.next = Node(2) 
    head.next.next = Node(0) 
    head.next.next.next = Node(4) 
    head.next.next.next.next = Node(5) 
    head.next.next.next.next.next = Node(0) 
    head.next.next.next.next.next.next = Node(6) 
    head.next.next.next.next.next.next.next = Node(7) 
    inPlaceStore(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to in-place product linked list  
// nodes between 0s  
using System; 

// Linked List Node  
public class Node  
{  
    public int data;  
    public Node next;  

    public Node(int data)  
    {  
        this.data = data;  
        this.next = null;  
    }  
}  

// Function to in-place product linked list  
// nodes between 0s  
public class inPlaceStoreLL  
{  

    // Function to store numbers till 0  
    static void inPlaceStore(Node head)  
    {  
        if (head.data == 0)  
        {  
            head = head.next;  
        }  

        // To store modified list  
        Node res = head;  

        // Traverse linked list and keep  
        // adding nodes between 0s.  
        Node temp = head;  
        int prod = 1;  
        while (temp != null) 
        {  

            // loop to product the data of nodes till  
            // it encounters 0  
            if (temp.data != 0)  
            {  
                prod *= temp.data;  
                temp = temp.next;  
            }  

            // If we encounters 0, we need  
            // to update next pointers  
            else 
            {  

                res.data = prod;  
                res.next = temp.next;  
                temp = temp.next;  
                res = res.next;  
                prod = 1;  
            }  
        }  

        // For the last segment  
        res.data = prod;  
        res.next = temp;  

        printList(head);  
    }  

    // Function to traverse and print Linked List  
    static void printList(Node head)  
    {  
        while (head.next != null)  
        {  
            Console.Write(head.data + "-> ");  
            head = head.next;  
        }  
        Console.WriteLine(head.data);  
    }  

    // Driver Code  
    public static void Main(String[] args)  
    {  
        Node head = new Node(3);  
        head.next = new Node(2);  
        head.next.next = new Node(0);  
        head.next.next.next = new Node(4);  
        head.next.next.next.next = new Node(5);  
        head.next.next.next.next.next = new Node(0);  
        head.next.next.next.next.next.next = new Node(6);  
        head.next.next.next.next.next.next.next = new Node(7);  
        inPlaceStore(head);  
    }  
}  

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
6-> 20-> 42

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。