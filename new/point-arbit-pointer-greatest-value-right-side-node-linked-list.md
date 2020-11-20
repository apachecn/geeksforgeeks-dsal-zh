# 将仲裁指针指向链表中的最大值右侧节点

> 原文：[https://www.geeksforgeeks.org/point-arbit-pointer-greatest-value-right-side-node-linked-list/](https://www.geeksforgeeks.org/point-arbit-pointer-greatest-value-right-side-node-linked-list/)

给定单链表，每个节点都有一个额外的“任意”指针，该指针当前指向 NULL。 我们需要在右侧链表中使“任意”指针指向最大值节点。

![listwithArbit1](img/e37b455dc722e9b607243f9f28641891.png)

**简单解决方案**是一个接一个地遍历所有节点。 对于每个节点，找到右侧最大的节点并更改下一个指针。 该解决方案的时间复杂度为`O(N ^ 2)`。

有效的**解决方案**可以在`O(n)`时间内工作。 以下是步骤。

1.  反转给定的链表。

2.  开始遍历链表并存储到目前为止遇到的最大值节点。 使每个节点的仲裁指向最大。 如果到目前为止，当前节点中的数据大于最大节点，请更新最大。

3.  反向修改链表和返回头。

以下是上述步骤的执行。

## C++

```cpp

// C++ program to point arbit pointers to highest 
// value on its right 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node 
{ 
    int data; 
    Node* next, *arbit; 
}; 

/* Function to reverse the linked list */
Node* reverse(Node *head) 
{ 
    Node *prev = NULL, *current = head, *next; 
    while (current != NULL) 
    { 
        next  = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 
    return prev; 
} 

// This function populates arbit pointer in every 
// node to the greatest value to its right. 
Node* populateArbit(Node *head) 
{ 
    // Reverse given linked list 
    head = reverse(head); 

    // Initialize pointer to maximum value node 
    Node *max = head; 

    // Traverse the reversed list 
    Node *temp = head->next; 
    while (temp != NULL) 
    { 
        // Connect max through arbit pointer 
        temp->arbit = max; 

        // Update max if required 
        if (max->data < temp->data) 
            max = temp; 

        // Move ahead in reversed list 
        temp = temp->next; 
    } 

    // Reverse modified linked list and return 
    // head. 
    return reverse(head); 
} 

// Utility function to print result linked list 
void printNextArbitPointers(Node *node) 
{ 
    printf("Node\tNext Pointer\tArbit Pointer\n"); 
    while (node!=NULL) 
    { 
        cout << node->data << "\t\t"; 

        if (node->next) 
            cout << node->next->data << "\t\t"; 
        else cout << "NULL" << "\t\t"; 

        if (node->arbit) 
            cout << node->arbit->data; 
        else cout << "NULL"; 

        cout << endl; 
        node = node->next; 
    } 
} 

/* Function to create a new node with given data */
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    Node *head = newNode(5); 
    head->next = newNode(10); 
    head->next->next = newNode(2); 
    head->next->next->next = newNode(3); 

    head = populateArbit(head); 

    printf("Resultant Linked List is: \n"); 
    printNextArbitPointers(head); 

    return 0; 
} 

```

## Java

```java

// Java program to point arbit pointers to highest  
// value on its right  
class GfG  
{  

/* Link list node */
static class Node  
{  
    int data;  
    Node next, arbit;  
} 

/* Function to reverse the linked list */
static Node reverse(Node head)  
{  
    Node prev = null, current = head, next = null;  
    while (current != null)  
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
    }  
    return prev;  
}  

// This function populates arbit pointer in every  
// node to the greatest value to its right.  
static Node populateArbit(Node head)  
{  
    // Reverse given linked list  
    head = reverse(head);  

    // Initialize pointer to maximum value node  
    Node max = head;  

    // Traverse the reversed list  
    Node temp = head.next;  
    while (temp != null)  
    {  
        // Connect max through arbit pointer  
        temp.arbit = max;  

        // Update max if required  
        if (max.data < temp.data)  
            max = temp;  

        // Move ahead in reversed list  
        temp = temp.next;  
    }  

    // Reverse modified linked list and return  
    // head.  
    return reverse(head);  
}  

// Utility function to print result linked list  
static void printNextArbitPointers(Node node)  
{  
    System.out.println("Node\tNext Pointer\tArbit Pointer");  
    while (node != null)  
    {  
        System.out.print(node.data + "\t\t");  

        if (node.next != null)  
            System.out.print(node.next.data + "\t\t");  
        else
            System.out.print("NULL" +"\t\t");  

        if (node.arbit != null)  
            System.out.print(node.arbit.data);  
        else
            System.out.print("NULL");  

        System.out.println();  
        node = node.next;  
    }  
}  

/* Function to create a new node with given data */
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

/* Driver code*/
public static void main(String[] args)  
{  
    Node head = newNode(5);  
    head.next = newNode(10);  
    head.next.next = newNode(2);  
    head.next.next.next = newNode(3);  

    head = populateArbit(head);  

    System.out.println("Resultant Linked List is: ");  
    printNextArbitPointers(head);  

} 
}  

// This code is contributed by Prerna Saini. 

```

## Python

```py

# Python Program to point arbit pointers to highest 
# value on its right 

# Node class  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None
        self.arbit = None

# Function to reverse the linked list  
def reverse(head): 

    prev = None
    current = head 
    next = None
    while (current != None): 

        next = current.next
        current.next = prev 
        prev = current 
        current = next

    return prev 

# This function populates arbit pointer in every 
# node to the greatest value to its right. 
def populateArbit(head): 

    # Reverse given linked list 
    head = reverse(head) 

    # Initialize pointer to maximum value node 
    max = head 

    # Traverse the reversed list 
    temp = head.next
    while (temp != None): 

        # Connect max through arbit pointer 
        temp.arbit = max

        # Update max if required 
        if (max.data < temp.data): 
            max = temp 

        # Move ahead in reversed list 
        temp = temp.next

    # Reverse modified linked list and return 
    # head. 
    return reverse(head) 

# Utility function to print result linked list 
def printNextArbitPointers(node): 

    print("Node\tNext Pointer\tArbit Pointer\n") 
    while (node != None): 

        print( node.data , "\t\t",end = "") 

        if (node.next != None): 
            print( node.next.data , "\t\t",end = "") 
        else : 
            print( "None" , "\t\t",end = "") 

        if (node.arbit != None): 
            print( node.arbit.data,end = "") 
        else : 
            print( "None",end = "") 

        print("\n") 
        node = node.next

# Function to create a new node with given data  
def newNode(data): 

    new_node = Node(0) 
    new_node.data = data 
    new_node.next = None
    return new_node 

# Driver code 

head = newNode(5) 
head.next = newNode(10) 
head.next.next = newNode(2) 
head.next.next.next = newNode(3) 

head = populateArbit(head) 

print("Resultant Linked List is: \n") 
printNextArbitPointers(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to point arbit pointers   
// to highest value on its right 
using System; 

class GfG  
{  

    /* Link list node */
    class Node  
    {  
        public int data;  
        public Node next, arbit;  
    } 

    /* Function to reverse the linked list */
    static Node reverse(Node head)  
    {  
        Node prev = null, current = head, next = null;  
        while (current != null)  
        {  
            next = current.next;  
            current.next = prev;  
            prev = current;  
            current = next;  
        }  
        return prev;  
    }  

    // This function populates arbit pointer in every  
    // node to the greatest value to its right.  
    static Node populateArbit(Node head)  
    {  
        // Reverse given linked list  
        head = reverse(head);  

        // Initialize pointer to maximum value node  
        Node max = head;  

        // Traverse the reversed list  
        Node temp = head.next;  
        while (temp != null)  
        {  
            // Connect max through arbit pointer  
            temp.arbit = max;  

            // Update max if required  
            if (max.data < temp.data)  
                max = temp;  

            // Move ahead in reversed list  
            temp = temp.next;  
        }  

        // Reverse modified linked list   
        // and return head.  
        return reverse(head);  
    }  

    // Utility function to print result linked list  
    static void printNextArbitPointers(Node node)  
    {  
        Console.WriteLine("Node\tNext Pointer\tArbit Pointer");  
        while (node != null)  
        {  
            Console.Write(node.data + "\t\t");  

            if (node.next != null)  
                Console.Write(node.next.data + "\t\t");  
            else
                Console.Write("NULL" +"\t\t");  

            if (node.arbit != null)  
                Console.Write(node.arbit.data);  
            else
                Console.Write("NULL");  

            Console.WriteLine();  
            node = node.next;  
        }  
    }  

    /* Function to create a new node with given data */
    static Node newNode(int data)  
    {  
        Node new_node = new Node();  
        new_node.data = data;  
        new_node.next = null;  
        return new_node;  
    }  

    /* Driver code*/
    public static void Main(String[] args)  
    {  
        Node head = newNode(5);  
        head.next = newNode(10);  
        head.next.next = newNode(2);  
        head.next.next.next = newNode(3);  

        head = populateArbit(head);  

        Console.WriteLine("Resultant Linked List is: ");  
        printNextArbitPointers(head);  
    } 
} 

/* This code is contributed by 29AjayKumar */

```

**Output:**

```
Resultant Linked List is: 
Node    Next Pointer    Arbit Pointer
5               10              10
10              2               3
2               3               3
3               NULL            NULL

```

**递归解决方案**：

我们可以递归到达最后一个节点并从末端遍历链表。 递归解决方案不需要反向链表。 我们还可以使用栈代替递归来临时保存节点。 感谢 Santosh Kumar Mishra 提供此解决方案。

## C++

```cpp

// C++ program to point arbit pointers to highest 
// value on its right 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node 
{ 
    int data; 
    Node* next, *arbit; 
}; 

// This function populates arbit pointer in every 
// node to the greatest value to its right. 
void populateArbit(Node *head) 
{ 
    // using static maxNode to keep track of maximum 
    // orbit node address on right side 
    static Node *maxNode; 

    // if head is null simply return the list 
    if (head == NULL) 
        return; 

    /* if head->next is null it means we reached at 
       the last node just update the max and maxNode */
    if (head->next == NULL) 
    { 
        maxNode = head; 
        return; 
    } 

    /* Calling the populateArbit to the next node */
    populateArbit(head->next); 

    /* updating the arbit node of the current 
     node with the maximum value on the right side */
    head->arbit = maxNode; 

    /* if current Node value id greater then 
     the previous right node then  update it */
    if (head->data > maxNode->data) 
        maxNode = head; 

   return; 
} 

// Utility function to print result linked list 
void printNextArbitPointers(Node *node) 
{ 
    printf("Node\tNext Pointer\tArbit Pointer\n"); 
    while (node!=NULL) 
    { 
        cout << node->data << "\t\t"; 

        if(node->next) 
            cout << node->next->data << "\t\t"; 
        else cout << "NULL" << "\t\t"; 

        if(node->arbit) 
            cout << node->arbit->data; 
        else cout << "NULL"; 

        cout << endl; 
        node = node->next; 
    } 
} 

/* Function to create a new node with given data */
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    Node *head = newNode(5); 
    head->next = newNode(10); 
    head->next->next = newNode(2); 
    head->next->next->next = newNode(3); 

    populateArbit(head); 

    printf("Resultant Linked List is: \n"); 
    printNextArbitPointers(head); 

    return 0; 
} 

```

## Java

```java

// Java program to point arbit pointers to highest 
// value on its right 
class GfG 
{ 

    /* Link list node */
    static class Node 
    { 
        int data; 
        Node next, arbit; 
    } 

    static Node maxNode; 

    // This function populates arbit pointer in every 
    // node to the greatest value to its right. 
    static void populateArbit(Node head) 
    { 

        // if head is null simply return the list 
        if (head == null) 
            return; 

        /* if head->next is null it means we reached at 
        the last node just update the max and maxNode */
        if (head.next == null) 
        { 
            maxNode = head; 
            return; 
        } 

        /* Calling the populateArbit to the next node */
        populateArbit(head.next); 

        /* updating the arbit node of the current 
        node with the maximum value on the right side */
        head.arbit = maxNode; 

        /* if current Node value id greater then 
        the previous right node then update it */
        if (head.data > maxNode.data) 
            maxNode = head; 

        return; 
    } 

    // Utility function to print result linked list 
    static void printNextArbitPointers(Node node) 
    { 
        System.out.println("Node\tNext Pointer\tArbit Pointer"); 
        while (node != null) 
        { 
            System.out.print(node.data + "\t\t\t"); 

            if (node.next != null) 
                System.out.print(node.next.data + "\t\t\t\t"); 
            else
                System.out.print("NULL" +"\t\t\t"); 

            if (node.arbit != null) 
                System.out.print(node.arbit.data); 
            else
                System.out.print("NULL"); 

            System.out.println(); 
            node = node.next; 
        } 
    } 

    /* Function to create a new node with given data */
    static Node newNode(int data) 
    { 
        Node new_node = new Node(); 
        new_node.data = data; 
        new_node.next = null; 
        return new_node; 
    } 

    /* Driver code*/
    public static void main(String[] args) 
    { 
        Node head = newNode(5); 
        head.next = newNode(10); 
        head.next.next = newNode(2); 
        head.next.next.next = newNode(3); 

        populateArbit(head); 

        System.out.println("Resultant Linked List is: "); 
        printNextArbitPointers(head); 

    } 
} 

// This code is contributed by shubham96301     

```

## Python3

```py

# Python3 program to poarbit pointers to highest  
# value on its right  

''' Link list node '''
# Node class  
class newNode:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None
        self.arbit = None

# This function populates arbit pointer in every  
# node to the greatest value to its right.  
maxNode = newNode(None) 
def populateArbit(head): 

    # using static maxNode to keep track of maximum  
    # orbit node address on right side  
    global maxNode 

    # if head is null simply return the list  
    if (head == None): 
        return

    ''' if head.next is null it means we reached at  
    the last node just update the max and maxNode '''
    if (head.next == None): 
        maxNode = head  
        return

    ''' Calling the populateArbit to the next node '''
    populateArbit(head.next)  

    ''' updating the arbit node of the current  
    node with the maximum value on the right side '''
    head.arbit = maxNode  

    ''' if current Node value id greater then  
    the previous right node then update it '''
    if (head.data > maxNode.data and maxNode.data != None ): 
        maxNode = head  
    return

# Utility function to prresult linked list  
def printNextArbitPointers(node): 
    print("Node\tNext Pointer\tArbit Pointer") 
    while (node != None): 
        print(node.data,"\t\t", end = "") 
        if(node.next): 
            print(node.next.data,"\t\t", end = "") 
        else: 
            print("NULL","\t\t", end = "") 
        if(node.arbit): 
            print(node.arbit.data, end = "") 
        else: 
            print("NULL", end = "") 
        print() 
        node = node.next

''' Driver code'''
head = newNode(5)  
head.next = newNode(10)  
head.next.next = newNode(2)  
head.next.next.next = newNode(3)  

populateArbit(head)  

print("Resultant Linked List is:")  
printNextArbitPointers(head)  

# This code is contributed by SHUBHAMSINGH10 

```

## C#

```cs

// C# program to point arbit pointers to highest 
// value on its right 
using System; 

class GfG 
{ 

    /* Link list node */
    public class Node 
    { 
        public int data; 
        public Node next, arbit; 
    } 

    static Node maxNode; 

    // This function populates arbit pointer in every 
    // node to the greatest value to its right. 
    static void populateArbit(Node head) 
    { 

        // if head is null simply return the list 
        if (head == null) 
            return; 

        /* if head->next is null it means we reached at 
        the last node just update the max and maxNode */
        if (head.next == null) 
        { 
            maxNode = head; 
            return; 
        } 

        /* Calling the populateArbit to the next node */
        populateArbit(head.next); 

        /* updating the arbit node of the current 
        node with the maximum value on the right side */
        head.arbit = maxNode; 

        /* if current Node value id greater then 
        the previous right node then update it */
        if (head.data > maxNode.data) 
            maxNode = head; 

        return; 
    } 

    // Utility function to print result linked list 
    static void printNextArbitPointers(Node node) 
    { 
        Console.WriteLine("Node\tNext Pointer\tArbit Pointer"); 
        while (node != null) 
        { 
            Console.Write(node.data + "\t\t\t"); 

            if (node.next != null) 
                Console.Write(node.next.data + "\t\t\t\t"); 
            else
                Console.Write("NULL" +"\t\t\t"); 

            if (node.arbit != null) 
                Console.Write(node.arbit.data); 
            else
                Console.Write("NULL"); 

            Console.WriteLine(); 
            node = node.next; 
        } 
    } 

    /* Function to create a new node with given data */
    static Node newNode(int data) 
    { 
        Node new_node = new Node(); 
        new_node.data = data; 
        new_node.next = null; 
        return new_node; 
    } 

    /* Driver code*/
    public static void Main(String[] args) 
    { 
        Node head = newNode(5); 
        head.next = newNode(10); 
        head.next.next = newNode(2); 
        head.next.next.next = newNode(3); 

        populateArbit(head); 

        Console.WriteLine("Resultant Linked List is: "); 
        printNextArbitPointers(head); 

    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
Resultant Linked List is: 
Node    Next Pointer    Arbit Pointer
5               10              10
10              2               3
2               3               3
3               NULL            NULL

```

本文由 **Aditya Goel** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

