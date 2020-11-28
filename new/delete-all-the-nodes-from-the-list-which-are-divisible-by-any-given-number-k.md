# 从列表中删除可被给定数字`K`整除的所有节点

> 原文：[https://www.geeksforgeeks.org/delete-all-the-nodes-from-the-list-which-are-divisible-by-any-given-number-k/](https://www.geeksforgeeks.org/delete-all-the-nodes-from-the-list-which-are-divisible-by-any-given-number-k/)

给定一个链表和一个密钥`K`。任务是编写一个程序，删除列表中所有可被`K`整除的节点。

**示例**：

```
Input : 12->15->9->11->5->6->7
        K = 3
Output :  11 -> 5 -> 7

Input :13->4->16->9->22->45->5->16->6
        K = 4
Output : 13 -> 9 -> 22 -> 45 -> 5 -> 6

```

解决该问题的方法类似于[从列表中删除所有小于给定键的节点](https://www.geeksforgeeks.org/delete-all-the-nodes-from-the-list-which-are-less-than-k/)。

**有两种可能的情况**：

1.  头节点的值可被`K`整除：首先检查头节点上所有可被`K`整除的事件，删除它们并适当地更改头节点。

2.  一些中间节点持有可被`K`整除的值：从头开始遍历并检查当前节点的值是否可被`K`整除。如果是，则删除该节点并在列表中向前移动。

下面是上述方法的实现：

## C++

```cpp

// C++ program to delete all the nodes from the list 
// that are divisible by  the specified value K 
#include <bits/stdc++.h> 

using namespace std; 

// Tree Node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to create a new node 
Node* getNode(int data) 
{ 
    Node* newNode = new Node; 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to delete all the nodes from the list 
// that divisible by the specified value K 
void deleteDivisibleNodes(Node** head_ref, int K) 
{ 
    Node *temp = *head_ref, *prev; 

    // If head node itself holds the value divisible by K 
    while (temp != NULL && temp->data % K == 0) { 
        *head_ref = temp->next; // Changed head 
        free(temp); // free old head 
        temp = *head_ref; // Change temp 
    } 

    // Delete occurrences other than head 
    while (temp != NULL) { 

        // Search for the node to be deleted, 
        // keep track of the previous node as we 
        // need to change 'prev->next' 
        while (temp != NULL && temp->data % K != 0) { 
            prev = temp; 
            temp = temp->next; 
        } 

        // If required value node was not present 
        // in linked list 
        if (temp == NULL) 
            return; 

        // Unlink the node from linked list 
        prev->next = temp->next; 

        delete temp; // Free memory 

        // Update Temp for next iteration of 
        // outer loop 
        temp = prev->next; 
    } 
} 

// function to a print a linked list 
void printList(Node* head) 
{ 
    while (head) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver code 
int main() 
{ 
    // Create list: 12->15->9->11->5->6->7 
    Node* head = getNode(12); 
    head->next = getNode(15); 
    head->next->next = getNode(9); 
    head->next->next->next = getNode(11); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(6); 
    head->next->next->next->next->next->next = getNode(7); 
    int K = 3; 

    cout << "Initial List: "; 
    printList(head); 

    deleteDivisibleNodes(&head, K); 

    cout << "\nFinal List: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to delete all the nodes from the list 
// that are divisible by the specified value K 
import java.util.*; 

class GFG 
{ 

// Tree Node 
static class Node 
{ 
    int data; 
    Node next; 
}; 

// Function to create a new node 
static Node getNode(int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to delete all the nodes from the list 
// that divisible by the specified value K 
static Node deleteDivisibleNodes(Node head_ref, int K) 
{ 
    Node temp = head_ref, prev = null; 

    // If head node itself holds the value divisible by K 
    while (temp != null && temp.data % K == 0)  
    { 
        head_ref = temp.next; // Changed head 
        //free(temp); // free old head 
        temp = head_ref; // Change temp 
    } 

    // Delete occurrences other than head 
    while (temp != null)  
    { 

        // Search for the node to be deleted, 
        // keep track of the previous node as we 
        // need to change 'prev.next' 
        while (temp != null && temp.data % K != 0)  
        { 
            prev = temp; 
            temp = temp.next; 
        } 

        // If required value node was not present 
        // in linked list 
        if (temp == null) 
            return head_ref; 

        // Unlink the node from linked list 
        prev.next = temp.next; 

        //delete temp; // Free memory 

        // Update Temp for next iteration of 
        // outer loop 
        temp = prev.next; 
    } 
    return null; 
} 

// function to a print a linked list 
static void printList(Node head) 
{ 
    while (head != null) 
    { 
        System.out.print(head.data + " "); 
        head = head.next; 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Create list: 12->15->9->11->5->6->7 
    Node head = getNode(12); 
    head.next = getNode(15); 
    head.next.next = getNode(9); 
    head.next.next.next = getNode(11); 
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(6); 
    head.next.next.next.next.next.next = getNode(7); 
    int K = 3; 

    System.out.print("Initial List: "); 
    printList(head); 

    head = deleteDivisibleNodes(head, K); 

    System.out.print("\nFinal List: "); 
    printList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 program to delete all the 
# nodes from the list that are  
# divisible by the specified value K 

# Node class  
class Node:  

    # Function to initialize the node object  
    def __init__(self, data):  

        self.data = data  
        self.next = None 

# Linked List Class 
class LinkedList: 

    # Function to initialize the 
    # LinkedList class. 
    def __init__(self): 

        # Initialize head as None 
        self.head = None

    # This Method insert a new node  
    # at the End of the list 
    def push(self, new_data): 

        # Taking a pointer to iterate 
        ptr = self.head 

        # Making a new node with 
        # given data as it's element 
        new_node = Node(new_data) 

        # assigning the first node to 
        # head if list is empty or DNE 
        if(ptr == None): 
            self.head = new_node 

        # If list exits then.. 
        else: 

            # Iteraring to the last 
            # node of the list 
            while(ptr.next != None): 
                ptr = ptr.next

            # Attatching new node at 
            # the end of list 
            ptr.next = new_node 

    # Method to delete Nodes divisible 
    # by given integer. 
    def deleteDivisibleNodes(self, K): 

        # Declaring a temporary object 
        # cotaining address of head 
        temp = self.head 

        # Deleting the first node if it's 
        # data is divisible by given integer 
        # repeat till first node gets 
        # indivisible. 
        while(temp != None and
             (temp.data % K) == 0): 
            self.head = temp.next
            del(temp) 
            temp = self.head 

        # Now iterating through each node 
        # of the list. 
        while(temp != None): 

            # Checking if data in current node is 
            # divisible by given element and move 
            # to next node till it gets not divisible. 
            while(temp != None and 
                 (temp.data % K) != 0): 
                prev = temp 
                temp = temp.next

            # Returning if list ends 
            if(temp == None): 
                return

            # Else storing address of next node 
            # in next of previous node 
            prev.next = temp.next

            # And deleting the current Node 
            del(temp) 

            # Then move to next node and repeat 
            # the loop till list ends. 
            temp = prev.next

    # Method to print the linked list 
    def printList(self): 

        ptr = self.head 

        while(ptr != None): 
            x = ptr.data 
            print(x, ' ', end = '') 
            ptr = ptr.next

        print() 

# Driver Code 
if __name__=='__main__': 

    # Start with empty list 
    head = LinkedList() 

    # Create the linked list Adding 
    # a new node at End of the list 
    head.push(12) 
    head.push(15)  
    head.push(9) 
    head.push(11) 
    head.push(5) 
    head.push(6) 
    head.push(7) 

    print("Initila List: ", end = '') 
    head.printList() 

    K = 3
    head.deleteDivisibleNodes(K) 

    print("Final List: ", end = '') 
    head.printList() 

# This code is contributed by Amit Mangal 

```

## C#

```cs

// C# program to delete all the nodes  
// from the list that are divisible  
// by the specified value K 
using System; 

class GFG 
{ 

// Tree Node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to create a new node 
static Node getNode(int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to delete all the nodes 
// from the list that divisible by 
// the specified value K 
static Node deleteDivisibleNodes(Node head_ref,  
                                         int K) 
{ 
    Node temp = head_ref, prev = null; 

    // If head node itself holds 
    // the value divisible by K 
    while (temp != null &&  
           temp.data % K == 0)  
    { 
        head_ref = temp.next; // Changed head 
        //free(temp); // free old head 
        temp = head_ref; // Change temp 
    } 

    // Delete occurrences other than head 
    while (temp != null)  
    { 

        // Search for the node to be deleted, 
        // keep track of the previous node as we 
        // need to change 'prev.next' 
        while (temp != null && 
               temp.data % K != 0)  
        { 
            prev = temp; 
            temp = temp.next; 
        } 

        // If required value node  
        // was not present in linked list 
        if (temp == null) 
            return head_ref; 

        // Unlink the node from linked list 
        prev.next = temp.next; 

        //delete temp; // Free memory 

        // Update Temp for next iteration of 
        // outer loop 
        temp = prev.next; 
    } 
    return null; 
} 

// function to a print a linked list 
static void printList(Node head) 
{ 
    while (head != null) 
    { 
        Console.Write(head.data + " "); 
        head = head.next; 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Create list: 12->15->9->11->5->6->7 
    Node head = getNode(12); 
    head.next = getNode(15); 
    head.next.next = getNode(9); 
    head.next.next.next = getNode(11); 
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(6); 
    head.next.next.next.next.next.next = getNode(7); 
    int K = 3; 

    Console.Write("Initial List: "); 
    printList(head); 

    head = deleteDivisibleNodes(head, K); 

    Console.Write("\nFinal List: "); 
    printList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**： 

```
Initial List: 12 15 9 11 5 6 7 
Final List: 11 5 7

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。