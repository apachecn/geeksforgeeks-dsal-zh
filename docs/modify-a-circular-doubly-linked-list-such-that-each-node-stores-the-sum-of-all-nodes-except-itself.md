# 修改循环双向链表，使得每个节点存储除自身以外的所有节点的总和

> 原文:[https://www . geesforgeks . org/modify-a-circular-double-link-list-so-每个节点存储除自身之外的所有节点的总和/](https://www.geeksforgeeks.org/modify-a-circular-doubly-linked-list-such-that-each-node-stores-the-sum-of-all-nodes-except-itself/)

给定由 **N** 个节点组成的[循环双链表](https://www.geeksforgeeks.org/doubly-circular-linked-list-set-1-introduction-and-insertion/)，任务是修改给定[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的每个节点，使得每个节点包含除该节点之外的所有节点的总和。

**示例:**

> **输入:**4↔5↔6 ↔7↔8
> T3】输出:26↔25↔24↔23↔22
> T6】解释:t8】1<sup>ST</sup>节点:除自身以外的所有节点之和= (5 + 6 + 7 + 8) = 26。
> 2 <sup>nd</sup> 节点:除自身以外的所有节点之和= (4 + 6 + 7 + 8) = 25。
> 3 <sup>rd</sup> 节点:除自身外所有节点之和= (4 + 5 + 7 + 8) = 24。
> 4 <sup>第</sup>个节点:除自身以外的所有节点之和= (4 + 5 + 6 + 8) = 23。
> 5 <sup>第</sup>个节点:除自身外的所有节点之和= (4 + 5 + 6 + 7) = 25。
> 
> **输入:**1↔2
> T3】输出: 2 ↔ 1

**天真方法:**解决问题最简单的方法是[遍历给定的循环双链表](https://www.geeksforgeeks.org/doubly-circular-linked-list-set-1-introduction-and-insertion/)，对于每个节点，遍历所有节点，用除该节点外的所有节点的和更新该节点。更新完所有节点后，[打印更新列表](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过将所有节点的[数据之和存储在一个变量中进行优化，比如说 **S** ，然后更新给定的链表。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/sum-nodes-binary-tree/)

*   将给定链表的[和存储在一个变量中，比如 **S** 。](https://www.geeksforgeeks.org/sum-of-the-nodes-of-a-singly-linked-list/)
*   初始化一个指针，在链表的 [**头**处 **temp** 。](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)
*   [循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到**温度→下一个**不等于**头**并执行以下步骤:
    *   将**温度→数据**的值更新为**(S-温度→数据)**。
    *   将**温度**更新为**温度→下一个**。
*   完成上述步骤后，将最后一个节点的值更新为**(S–temp→data)**，[打印更新后的链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include<stdio.h>
#include<stdlib.h>
// Structure of a Node
struct Node {
    int data;
    struct Node* next;
    struct Node* prev;
};

// Function to insert a node at the
// end of the given Linked List
void insertEnd(struct Node** start,
            int value)
{
    // If the list is empty, then
    // create a single node
    // circular and doubly list
    if (*start == NULL) {

        // Create a new Node
        struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

        // Add values and links to
        // the next & the previous
        new_node->data = value;
        new_node->next = new_node;
        new_node->prev = new_node;

        // Update the start
        *start = new_node;
        return;
    }

    // If list is not empty, then
    // find last node
    struct Node* last = (*start)->prev;

    // Create Node dynamically
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = value;

    // Start is the next of new_node
    new_node->next = *start;

    // Make new node previous of start
    (*start)->prev = new_node;

    // Make last previous of new node
    new_node->prev = last;

    // Make new node next of old last
    last->next = new_node;
}

// Function to print the linked list
void display(struct Node* start)
{
    // Forward traversal
    struct Node* temp = start;

    printf( "Traversal in forward "
        "direction \n");
    while (temp->next != start) {
        printf("%d  ",temp->data);
        temp = temp->next;
    }
printf("%d  ",temp->data);
    // Backward traversal
    printf("\nTraversal in reverse"
        " direction \n");
    struct Node* last = start->prev;
    temp = last;

    // Traverse the Linked List
    while (temp->prev != last) {

        // Print the data
        printf("%d  ",temp->data);
        temp = temp->prev;
    }

    // Print the data
    printf("%d  ",temp->data);
}

// Function to find the sum of all
// nodes in the given Linked List
int findSum(struct Node* start)
{
    // Stores the sum of all the nodes
    int sum = 0;

    struct Node* temp = start;

    // Traverse the linked list and
    // update the sum
    while (temp->next != start) {

        // Update the sum
        sum += temp->data;

        // Update the temp
        temp = temp->next;
    }

    // Update the sum
    sum += temp->data;

    // Return the sum
    return sum;
}

// Function to update the data of
// every node with the sum of data
// of all nodes except itself
void updateNodeValue(struct Node* start)
{
    // Stores the total sum
    // of all the nodes
    int sum = findSum(start);

    struct Node* temp = start;

    // Traverse the linked list
    // and update each node's data
    while (temp->next != start) {

        // Update the temp->data
        temp->data = sum - temp->data;

        // Update the temp
        temp = temp->next;
    }

    // Update the temp->data
    temp->data = sum - temp->data;
}

// Function to construct a
// circular doubly linked list
struct Node* formLinkedList(struct Node* start)
{
    // Given linked list as:
    // 4 <-> 5 <-> 6 <-> 7 <-> 8
    insertEnd(&start, 4);
    insertEnd(&start, 5);
    insertEnd(&start, 6);
    insertEnd(&start, 7);
    insertEnd(&start, 8);

    // Return the head of the
    // constructed Linked List
    return start;
}

// Driver Code
int main()
{
    // Linked list formation
    struct Node* start = NULL;
    start = formLinkedList(start);

    // Display the linked list
    display(start);

    // Function Call
    updateNodeValue(start);

    // Display the linked list
    // after updating nodes
    printf("\nAfter updating the node values:\n");

    // Print the Linked List
    display(start);

    return 0;
}
```

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
struct Node {
    int data;
    struct Node* next;
    struct Node* prev;
};

// Function to insert a node at the
// end of the given Linked List
void insertEnd(struct Node** start,
               int value)
{
    // If the list is empty, then
    // create a single node
    // circular and doubly list
    if (*start == NULL) {

        // Create a new Node
        struct Node* new_node = new Node();

        // Add values and links to
        // the next & the previous
        new_node->data = value;
        new_node->next = new_node;
        new_node->prev = new_node;

        // Update the start
        *start = new_node;
        return;
    }

    // If list is not empty, then
    // find last node
    Node* last = (*start)->prev;

    // Create Node dynamically
    struct Node* new_node = new Node;
    new_node->data = value;

    // Start is the next of new_node
    new_node->next = *start;

    // Make new node previous of start
    (*start)->prev = new_node;

    // Make last previous of new node
    new_node->prev = last;

    // Make new node next of old last
    last->next = new_node;
}

// Function to print the linked list
void display(struct Node* start)
{
    // Forward traversal
    struct Node* temp = start;

    cout << "Traversal in forward "
           "direction \n";
    while (temp->next != start) {
        cout << temp->data << " ";
        temp = temp->next;
    }
   cout <<  temp->data << " " ;

    // Backward traversal
    cout <<  "\nTraversal in reverse"
           " direction \n";
    Node* last = start->prev;
    temp = last;

    // Traverse the Linked List
    while (temp->prev != last) {

        // Print the data
        cout << temp->data << " " ;
        temp = temp->prev;
    }

    // Print the data
    cout <<  temp->data << " ";
}

// Function to find the sum of all
// nodes in the given Linked List
int findSum(Node*& start)
{
    // Stores the sum of all the nodes
    int sum = 0;

    Node* temp = start;

    // Traverse the linked list and
    // update the sum
    while (temp->next != start) {

        // Update the sum
        sum += temp->data;

        // Update the temp
        temp = temp->next;
    }

    // Update the sum
    sum += temp->data;

    // Return the sum
    return sum;
}

// Function to update the data of
// every node with the sum of data
// of all nodes except itself
void updateNodeValue(Node*& start)
{
    // Stores the total sum
    // of all the nodes
    int sum = findSum(start);

    Node* temp = start;

    // Traverse the linked list
    // and update each node's data
    while (temp->next != start) {

        // Update the temp->data
        temp->data = sum - temp->data;

        // Update the temp
        temp = temp->next;
    }

    // Update the temp->data
    temp->data = sum - temp->data;
}

// Function to construct a
// circular doubly linked list
Node* formLinkedList(Node* start)
{
    // Given linked list as:
    // 4 <-> 5 <-> 6 <-> 7 <-> 8
    insertEnd(&start, 4);
    insertEnd(&start, 5);
    insertEnd(&start, 6);
    insertEnd(&start, 7);
    insertEnd(&start, 8);

    // Return the head of the
    // constructed Linked List
    return start;
}

// Driver Code
int main()
{
    // Linked list formation
    struct Node* start = NULL;
    start = formLinkedList(start);

    // Display the linked list
    display(start);

    // Function Call
    updateNodeValue(start);

    // Display the linked list
    // after updating nodes
    cout << "\nAfter updating "
         << "the node values:\n";

    // Print the Linked List
    display(start);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static Node start;
static class Node
{
    int data;
    Node next;
    Node prev;
}

// Function to insert a node at the
// end of the given Linked List
// Function to insert at the end
static void insertEnd(int value)
{

    // If the list is empty, create a single
    // node circular and doubly list
    if (start == null)
    {
        Node new_node = new Node();
        new_node.data = value;
        new_node.next = new_node.prev = new_node;
        start = new_node;
        return;
    }

    // If list is not empty

    // Find last node
    Node last = (start).prev;

    // Create Node dynamically
    Node new_node = new Node();
    new_node.data = value;

    // Start is going to be
    // next of new_node
    new_node.next = start;

    // Make new node previous of start
    (start).prev = new_node;

    // Make last previous of new node
    new_node.prev = last;

    // Make new node next of old last
    last.next = new_node;
}

// Function to print the linked list
static void display()
{
    Node temp = start;

    System.out.printf("\nTraversal in " +
                      "forward direction \n");
    while (temp.next != start)
    {
        System.out.printf("%d ", temp.data);
        temp = temp.next;
    }
    System.out.printf("%d ", temp.data);

    System.out.printf("\nTraversal in reverse " +
                     "direction \n");
    Node last = start.prev;
    temp = last;

    while (temp.prev != last)
    {
        System.out.printf("%d ", temp.data);
        temp = temp.prev;
    }
    System.out.printf("%d ", temp.data);
}

// Function to update the data of
// every node with the sum of data
// of all nodes except itself
static void updateNodeValue()
{

    // Stores the total sum
    // of all the nodes
    int sum = findSum(start);

    Node temp = start;

    // Traverse the linked list
    // and update each node's data
    while (temp.next != start)
    {

        // Update the temp->data
        temp.data = sum - temp.data;

        // Update the temp
        temp = temp.next;
    }

    // Update the temp->data
    temp.data = sum - temp.data;
}

static Node formLinkedList(Node start)
{

    // Given linked list as:
    // 4 <-> 5 <-> 6 <-> 7 <-> 8
    insertEnd(4);
    insertEnd(5);
    insertEnd(6);
    insertEnd(7);
    insertEnd(8);

    // Return the head of the
    // constructed Linked List
    return start;
}

// Function to find the sum of all
// nodes in the given Linked List
static int findSum(Node head)
{
    Node temp = head;

    // Stores the sum of all the nodes
    int sum = 0;

    if (head != null)
    {

        // Traverse the linked list and
        // update the sum
        do
        {
            temp = temp.next;
            sum += temp.data;
        } while (temp != head);
    }

    // Return the sum
    return sum;
}

// Driver code
public static void main(String args[])
{
    Node start = null;
    start = formLinkedList(start);

    // Display the linked list
    display();

    // Function call
    updateNodeValue();

    // Display the linked list
    // after updating nodes
    System.out.print("\nAfter updating " +
                     "the node value:\n");

    // Print the Linked List
    display();
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a Node
class Node:

    def __init__(self, d):

        self.data = d
        self.next = None
        self.prev = None

# Function to insert a node at the
# end of the given Linked List
def insertEnd(start, value):

    # If the list is empty, then
    # create a single node
    # circular and doubly list
    if (start == None):

        # Create a new Node
        new_node = Node(value)

        new_node.next = new_node
        new_node.prev = new_node

        # Update the start
        start = new_node
        return start

    # If list is not empty, then
    # find last node
    last = start.prev

    # Create Node dynamically
    new_node = Node(value)
    new_node.data = value

    # Start is the next of new_node
    new_node.next = start

    # Make new node previous of start
    start.prev = new_node

    # Make last previous of new node
    new_node.prev = last

    # Make new node next of old last
    last.next = new_node

    return start

# Function to print the linked list
def display(start):

    # Forward traversal
    temp = start

    print("Traversal in forward direction")
    while (temp and temp.next != start):
        print(temp.data, end = " ")
        temp = temp.next

    print(temp.data, end = " ")

    # Backward traversal
    print("\nTraversal in reverse direction")
    last = start.prev
    temp = last

    # Traverse the Linked List
    while (temp.prev != last):

        # Print the data
        print(temp.data, end = " ")
        temp = temp.prev

    # Print the data
    print(temp.data, end = " ")

# Function to find the sum of all
# nodes in the given Linked List
def findSum(start):

    # Stores the sum of all the nodes
    sum = 0

    temp = start

    # Traverse the linked list and
    # update the sum
    while (temp.next != start):

        # Update the sum
        sum += temp.data

        # Update the temp
        temp = temp.next

    # Update the sum
    sum += temp.data

    # Return the sum
    return sum

# Function to update the data of
# every node with the sum of data
# of all nodes except itself
def updateNodeValue(start):

    # Stores the total sum
    # of all the nodes
    sum = findSum(start)

    temp = start

    # Traverse the linked list
    # and update each node's data
    while (temp.next != start):

        # Update the temp.data
        temp.data = sum - temp.data

        # Update the temp
        temp = temp.next

    # Update the temp.data
    temp.data = sum - temp.data

# Function to construct a
# circular doubly linked list
def formLinkedList(start):

    # Given linked list as:
    # 4 <. 5 <. 6 <. 7 <. 8
    start = insertEnd(start, 4)
    start = insertEnd(start, 5)
    start = insertEnd(start, 6)
    start = insertEnd(start, 7)
    start = insertEnd(start, 8)

    # Return the head of the
    # constructed Linked List
    return start

# Driver Code
if __name__ == '__main__':

    # Linked list formation
    start = None
    start = formLinkedList(start)

    # Display the linked list
    display(start)

    # Function Call
    updateNodeValue(start)

    # Display the linked list
    # after updating nodes
    print("\nAfter updating the node values:")

    # Print the Linked List
    display(start)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static Node start;
public class Node
{
    public int data;
    public Node next;
    public Node prev;
}

// Function to insert a node at the
// end of the given Linked List
// Function to insert at the end
static void insertEnd(int value)
{
    Node new_node;

    // If the list is empty, create a single
    // node circular and doubly list
    if (start == null)
    {
        new_node = new Node();
        new_node.data = value;
        new_node.next = new_node.prev = new_node;
        start = new_node;
        return;
    }

    // If list is not empty

    // Find last node
    Node last = (start).prev;

    // Create Node dynamically
    new_node = new Node();
    new_node.data = value;

    // Start is going to be
    // next of new_node
    new_node.next = start;

    // Make new node previous of start
    (start).prev = new_node;

    // Make last previous of new node
    new_node.prev = last;

    // Make new node next of old last
    last.next = new_node;
}

// Function to print the linked list
static void display()
{
    Node temp = start;

    Console.Write("\nTraversal in " +
                  "forward direction \n");

    while (temp.next != start)
    {
        Console.Write("{0} ", temp.data);
        temp = temp.next;
    }
    Console.Write("{0} ", temp.data);

    Console.Write("\nTraversal in reverse " +
                     "direction \n");
    Node last = start.prev;
    temp = last;

    while (temp.prev != last)
    {
        Console.Write("{0} ", temp.data);
        temp = temp.prev;
    }
    Console.Write("{0} ", temp.data);
}

// Function to update the data of
// every node with the sum of data
// of all nodes except itself
static void updateNodeValue()
{

    // Stores the total sum
    // of all the nodes
    int sum = findSum(start);

    Node temp = start;

    // Traverse the linked list
    // and update each node's data
    while (temp.next != start)
    {

        // Update the temp->data
        temp.data = sum - temp.data;

        // Update the temp
        temp = temp.next;
    }

    // Update the temp->data
    temp.data = sum - temp.data;
}

static Node formList(Node start)
{

    // Given linked list as:
    // 4 <-> 5 <-> 6 <-> 7 <-> 8
    insertEnd(4);
    insertEnd(5);
    insertEnd(6);
    insertEnd(7);
    insertEnd(8);

    // Return the head of the
    // constructed Linked List
    return start;
}

// Function to find the sum of all
// nodes in the given Linked List
static int findSum(Node head)
{
    Node temp = head;

    // Stores the sum of all the nodes
    int sum = 0;

    if (head != null)
    {

        // Traverse the linked list and
        // update the sum
        do
        {
            temp = temp.next;
            sum += temp.data;
        } while (temp != head);
    }

    // Return the sum
    return sum;
}

// Driver code
public static void Main(String []args)
{
    Node start = null;
    start = formList(start);

    // Display the linked list
    display();

    // Function call
    updateNodeValue();

    // Display the linked list
    // after updating nodes
    Console.Write("\nAfter updating " +
                  "the node value:\n");

    // Print the Linked List
    display();
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of a Node
class Node {

    constructor()
    {
        this.data = 0;
        this.next = null;
        this.prev = null;
    }
};

// Function to insert a node at the
// end of the given Linked List
function insertEnd(start, value)
{
    // If the list is empty, then
    // create a single node
    // circular and doubly list
    if (start == null) {

        // Create a new Node
        var new_node = new Node();

        // Add values and links to
        // the next & the previous
        new_node.data = value;
        new_node.next = new_node;
        new_node.prev = new_node;

        // Update the start
        start = new_node;
        return start;
    }

    // If list is not empty, then
    // find last node
    var last = start.prev;

    // Create Node dynamically
    var new_node = new Node;
    new_node.data = value;

    // Start is the next of new_node
    new_node.next = start;

    // Make new node previous of start
    start.prev = new_node;

    // Make last previous of new node
    new_node.prev = last;

    // Make new node next of old last
    last.next = new_node;

    return start;
}

// Function to print the linked list
function display(start)
{
    // Forward traversal
    var temp = start;

    document.write("Traversal in forward "+
           "direction <br>");
    while (temp.next != start) {
        document.write(temp.data + " ");
        temp = temp.next;
    }
    document.write(temp.data  + " ");

    // Backward traversal
    document.write("<br>Traversal in reverse"+
           " direction <br>");
    var last = start.prev;
    temp = last;

    // Traverse the Linked List
    while (temp.prev != last) {

        // Print the data
        document.write( temp.data + " ");
        temp = temp.prev;
    }

    // Print the data
    document.write( temp.data + " ");
}

// Function to find the sum of all
// nodes in the given Linked List
function findSum(start)
{
    // Stores the sum of all the nodes
    var sum = 0;

    var temp = start;

    // Traverse the linked list and
    // update the sum
    while (temp.next != start) {

        // Update the sum
        sum += temp.data;

        // Update the temp
        temp = temp.next;
    }

    // Update the sum
    sum += temp.data;

    // Return the sum
    return sum;
}

// Function to update the data of
// every node with the sum of data
// of all nodes except itself
function updateNodeValue(start)
{
    // Stores the total sum
    // of all the nodes
    var sum = findSum(start);

    var temp = start;

    // Traverse the linked list
    // and update each node's data
    while (temp.next != start) {

        // Update the temp.data
        temp.data = sum - temp.data;

        // Update the temp
        temp = temp.next;
    }

    // Update the temp.data
    temp.data = sum - temp.data;
}

// Function to construct a
// circular doubly linked list
function formLinkedList(start)
{
    // Given linked list as:
    // 4 <. 5 <. 6 <. 7 <. 8
    start = insertEnd(start, 4);
    start = insertEnd(start, 5);
    start = insertEnd(start, 6);
    start = insertEnd(start, 7);
    start = insertEnd(start, 8);

    // Return the head of the
    // constructed Linked List
    return start;
}

// Driver Code
// Linked list formation
var start = null;
start = formLinkedList(start);

// Display the linked list
display(start);

// Function Call
updateNodeValue(start);

// Display the linked list
// after updating nodes
document.write( "<br>After updating "
     + "the node values:<br>");

// Print the Linked List
display(start);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Traversal in forward direction 
4 5 6 7 8 
Traversal in reverse direction 
8 7 6 5 4 
After updating the node values:
Traversal in forward direction 
26 25 24 23 22 
Traversal in reverse direction 
22 23 24 25 26
```

***时间复杂度:** O(N)，其中 N 为循环双链表中的节点总数。*
***辅助空间:** O(1)*