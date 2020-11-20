# 可被 K 整除的循环单链表的节点的总和和

> 原文：[https://www.geeksforgeeks.org/sum-and-product-of-the-nodes-of-a-circular-singly-linked-list-which-are-divisible-by-k/](https://www.geeksforgeeks.org/sum-and-product-of-the-nodes-of-a-circular-singly-linked-list-which-are-divisible-by-k/)

给定一个单循环链表。 任务是找到可被给定链表的 K 整除的节点的总和和乘积。

**示例**：

```
Input : List = 5->6->7->8->9->10->11->11
             K = 11
Output : Sum = 22, Product = 121

Input : List = 15->7->3->9->11->5
             K = 5
Output : Product = 75, Sum = 20

```

![Sum And Product of Singly Circular Linked List Node](img/8795cc5795962963898fe645c6ba5260.png)

单循环链表节点的总和与乘积

**方法**：

1.  用循环链表的开头初始化指针电流，并将和变量**和**设为 0，并将乘积变量**积**设为 1。

2.  使用 do while 循环开始遍历链表，直到遍历所有节点。

3.  如果当前节点数据可被给定键整除。

    *   将当前节点的值添加到总和，即 **sum =总和+当前->数据**。

    *   将当前节点的值乘以乘积，即**乘积=乘积*当前->数据**。

    *   递增指向链表的下一个节点的指针，即 **temp = temp-> next** 。

4.  打印总和和乘积。

下面是上述方法的实现：

## C++

```cpp

// C++ program to calculate sum and product from 
// singly circular linked list nodes 
// which are divisible by given key 

#include <bits/stdc++.h> 
using namespace std; 

// Circular list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to calculate sum and product 
void sumProduct(struct Node* head, int key) 
{ 
    struct Node* current = head; 

    int sum = 0, product = 1; 

    // if list is empty simply show message 
    if (head == NULL) { 
        printf("\nDisplay List is empty\n"); 
        return; 
    } 
    // traverse first to last node 
    else { 
        do { 
            // check if current node's data is 
            // divisible by key 
            if ((current->data) % key == 0) { 

                // Calculate sum 
                sum += current->data; 

                // Calculate product 
                product *= current->data; 
            } 

            current = current->next; 
        } while (current != head); 
    } 

    cout << "Sum = " << sum << ", Product = " << product; 
} 

// Function print the list 
void displayList(struct Node* head) 
{ 
    struct Node* current = head; 

    // if list is empty simply show message 
    if (head == NULL) { 
        printf("\nDisplay List is empty\n"); 
        return; 
    } 
    // traverse first to last node 
    else { 
        do { 
            printf("%d ", current->data); 
            current = current->next; 
        } while (current != head); 
    } 
} 

// Function to insert a node at the end of 
// a Circular linked list 
void InsertNode(struct Node** head, int data) 
{ 
    struct Node* current = *head; 
    // Create a new node 
    struct Node* newNode = new Node; 

    // check node is created or not 
    if (!newNode) { 
        printf("\nMemory Error\n"); 
        return; 
    } 

    // insert data into newly created node 
    newNode->data = data; 

    // check list is empty 
    // if not have any node then 
    // make first node it 
    if (*head == NULL) { 
        newNode->next = newNode; 
        *head = newNode; 
        return; 
    } 
    // if list have already some node 
    else { 

        // move firt node to last node 
        while (current->next != *head) { 
            current = current->next; 
        } 

        // put first or head node address in new node link 
        newNode->next = *head; 

        // put new node address into last node link(next) 
        current->next = newNode; 
    } 
} 

// Driver Code 
int main() 
{ 
    struct Node* head = NULL; 
    InsertNode(&head, 5); 
    InsertNode(&head, 6); 
    InsertNode(&head, 7); 
    InsertNode(&head, 8); 
    InsertNode(&head, 9); 
    InsertNode(&head, 10); 
    InsertNode(&head, 11); 
    InsertNode(&head, 11); 

    cout << "Initial List: "; 
    displayList(head); 

    cout << endl; 
    sumProduct(head, 11); 

    return 0; 
} 

```

## Java

```java

// Java program to calculate sum and product from  
// singly circular linked list nodes  
// which are divisible by given key  
import java.util.*; 
class Solution 
{ 

// Circular list node  
static class Node {  
    int data;  
    Node next;  
}  

// Function to calculate sum and product  
static void sumProduct( Node head, int key)  
{  
         Node current = head;  

    int sum = 0, product = 1;  

    // if list is empty simply show message  
    if (head == null) {  
        System.out.print("\nDisplay List is empty\n");  
        return;  
    }  
    // traverse first to last node  
    else {  
        do {  
            // check if current node's data is  
            // divisible by key  
            if ((current.data) % key == 0) {  

                // Calculate sum  
                sum += current.data;  

                // Calculate product  
                product *= current.data;  
            }  

            current = current.next;  
        } while (current != head);  
    }  

    System.out.print( "Sum = " + sum + ", Product = " + product);  
}  

// Function print the list  
static void displayList( Node head)  
{  
     Node current = head;  

    // if list is empty simply show message  
    if (head == null) {  
        System.out.print("\nDisplay List is empty\n");  
        return;  
    }  
    // traverse first to last node  
    else {  
        do {  
            System.out.print( current.data+" ");  
            current = current.next;  
        } while (current != head);  
    }  
}  

// Function to insert a node at the end of  
// a Circular linked list  
static Node InsertNode( Node head, int data)  
{  
     Node current = head;  
    // Create a new node  
     Node newNode = new Node();  

    // check node is created or not  
    if (newNode==null) {  
       System.out.print("\nMemory Error\n");  
        return head;  
    }  

    // insert data into newly created node  
    newNode.data = data;  

    // check list is empty  
    // if not have any node then  
    // make first node it  
    if (head == null) {  
        newNode.next = newNode;  
        head = newNode;  
        return head;  
    }  
    // if list have already some node  
    else {  

        // move firt node to last node  
        while (current.next != head) {  
            current = current.next;  
        }  

        // put first or head node address in new node link  
        newNode.next = head;  

        // put new node address into last node link(next)  
        current.next = newNode;  
    }  
    return head; 
}  

// Driver Code  
public static void main(String args[]) 
{  
     Node head=null ;  
    head =InsertNode(head, 5);  
    head =InsertNode(head, 6);  
    head =InsertNode(head, 7);  
    head =InsertNode(head, 8);  
    head =InsertNode(head, 9);  
    head =InsertNode(head, 10);  
    head =InsertNode(head, 11);  
    head =InsertNode(head, 11);  

    System.out.print( "Initial List: ");  
    displayList(head);  

    System.out.println();  
    sumProduct(head, 11);  

} 
} 
//contributed by Arnab Kundu 

```

## Python3

```py

    # Python3 program to calculate sum and  
# product from singly circular linked list  
# nodes which are divisible by given key 
import math  

# Circular list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to calculate sum and product 
def sumProduct(head, key): 
    current = head 

    sum = 0
    product = 1

    # if list is empty simply show message 
    if (head == None): 
        print("\nDisplay List is empty\n") 
        return

    # traverse first to last node 
    else : 

        # check if current node's data is 
        # divisible by key 
        if ((current.data) % key == 0) : 

            # Calculate sum 
            sum = sum + current.data 

            # Calculate product 
            product = product * current.data 

        current = current.next
        while (current != head): 
            if ((current.data) % key == 0) : 

                # Calculate sum 
                sum = sum + current.data 

                # Calculate product 
                product = product * current.data 

            current = current.next

    print("\nSum =", sum, end = ", ") 
    print("Product =", product) 

# Function print the list 
def displayList(head): 
    current = head 

    # if list is empty simply show message 
    if (head == None): 
        print("\nDisplay List is empty\n") 
        return

    # traverse first to last node 
    else : 

        print(current.data, end = " ") 
        current = current.next
        while (current != head): 
            print(current.data, end = " ") 
            current = current.next

# Function to insert a node at the end of 
# a Circular linked list 
def InsertNode(head, data): 
    current = head 

    # Create a new node 
    newNode = Node(data) 

    # check node is created or not 
    if (newNode == None): 
        print("\nMemory Error\n") 
        return head 

    # insert data o newly created node 
    newNode.data = data 

    # check list is empty 
    # if not have any node then 
    # make first node it 
    if (head == None): 
        newNode.next = newNode 
        head = newNode 
        return head 

    # if list have already some node 
    else : 

        # move firt node to last node 
        while (current.next != head): 
            current = current.next

        # put first or head node address 
        # in new node link 
        newNode.next = head 

        # put new node address o last node link(next) 
        current.next = newNode 

    return head 

# Driver Code 
if __name__=='__main__':  
    head = None
    head = InsertNode(head, 5)  
    head = InsertNode(head, 6)  
    head = InsertNode(head, 7)  
    head = InsertNode(head, 8)  
    head = InsertNode(head, 9)  
    head = InsertNode(head, 10)  
    head = InsertNode(head, 11)  
    head = InsertNode(head, 11)  

    print("Initial List: ", end = "") 
    displayList(head) 

    sumProduct(head, 11) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to calculate sum and product from  
// singly circular linked list nodes  
// which are divisible by given key  
using System; 

class GFG 
{ 

    // Circular list node  
    class Node  
    {  
        public int data;  
        public Node next;  
    }  

    // Function to calculate sum and product  
    static void sumProduct( Node head, int key)  
    {  
            Node current = head;  

        int sum = 0, product = 1;  

        // if list is empty simply show message  
        if (head == null)  
        {  
            Console.Write("\nDisplay List is empty\n");  
            return;  
        }  

        // traverse first to last node  
        else
        {  
            do
            {  
                // check if current node's data is  
                // divisible by key  
                if ((current.data) % key == 0)  
                {  

                    // Calculate sum  
                    sum += current.data;  

                    // Calculate product  
                    product = current.data;  
                }  

                current = current.next;  
            } while (current != head);  
        }  

        Console.Write( "Sum = " + sum + ", Product = " + product);  
    }  

    // Function print the list  
    static void displayList( Node head)  
    {  
        Node current = head;  

        // if list is empty simply show message  
        if (head == null)  
        {  
            Console.Write("\nDisplay List is empty\n");  
            return;  
        }  
        // traverse first to last node  
        else 
        {  
            do 
            {  
                Console.Write( current.data+" ");  
                current = current.next;  
            } while (current != head);  
        }  
    }  

    // Function to insert a node at the end of  
    // a Circular linked list  
    static Node InsertNode( Node head, int data)  
    {  
        Node current = head;  
        // Create a new node  
        Node newNode = new Node();  

        // check node is created or not  
        if (newNode==null)  
        {  
            Console.Write("\nMemory Error\n");  
            return head;  
        }  

        // insert data into newly created node  
        newNode.data = data;  

        // check list is empty  
        // if not have any node then  
        // make first node it  
        if (head == null) 
        {  
            newNode.next = newNode;  
            head = newNode;  
            return head;  
        }  
        // if list have already some node  
        else
        {  

            // move firt node to last node  
            while (current.next != head)  
            {  
                current = current.next;  
            }  

            // put first or head node address in new node link  
            newNode.next = head;  

            // put new node address into last node link(next)  
            current.next = newNode;  
        }  
        return head; 
    }  

    // Driver Code  
    public static void Main() 
    {  
        Node head=null ;  
        head =InsertNode(head, 5);  
        head =InsertNode(head, 6);  
        head =InsertNode(head, 7);  
        head =InsertNode(head, 8);  
        head =InsertNode(head, 9);  
        head =InsertNode(head, 10);  
        head =InsertNode(head, 11);  
        head =InsertNode(head, 11);  

        Console.Write( "Initial List: ");  
        displayList(head);  

        Console.WriteLine();  
        sumProduct(head, 11);  
    } 
} 

// This code has been contributed  
// by PrinciRaj1992  

```

**Output:**

```
Initial List: 5 6 7 8 9 10 11 11 
Sum = 22, Product = 121

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。