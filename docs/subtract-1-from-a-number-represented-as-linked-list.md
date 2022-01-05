# 从表示为链表的数字中减去 1

> 原文:[https://www . geeksforgeeks . org/从表示为链表的数字中减去 1/](https://www.geeksforgeeks.org/subtract-1-from-a-number-represented-as-linked-list/)

给定代表正整数的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的**头**，任务是在减去 1 后打印更新的链表。

**示例:**

> **输入:**LL = 1->2->3->4
> **输出:** 1 - > 2 - > 3 - > 3
> 
> **输入:**LL = 1->2
> T3】输出: 1 - > 1

**方法:**给定的问题可以用[递归](https://www.geeksforgeeks.org/recursion/)求解。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，比如**减法器**以链表头为参数，执行以下步骤:
    *   **基本情况:**如果链表头节点为**空**，则从该递归调用返回 **-1** 。
    *   [**递归调用**](https://www.geeksforgeeks.org/recursion/) **:** 递归调用链表的下一个节点，让这个递归调用返回的值是**借用**。
    *   如果**借用**的值是 **-1** ，头节点的值是 **0** ，那么将头节点的值更新为 **9** ，并从当前递归调用中返回 **-1** 。
    *   否则，将头节点的值递减 **1** ，并从当前递归调用中返回 **0** 。
*   调用上述函数作为**减法器(头)**，从链表中减去 **1** 。
*   如果更新链表有前导 **0s** ，则移动头部指针。
*   完成上述步骤后，[打印更新后的链表](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)作为结果链表。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Linked list Node
class Node {
public:
    int data;
    Node* next;
};

// Function to create a new node with
// the given data
Node* newNode(int data)
{
    // Create a new node
    Node* new_node = new Node;
    new_node->data = data;
    new_node->next = NULL;

    // Return the created node
    return new_node;
}

// Recursive function to subtract 1
// from the linked list and update
// the node value accordingly
int subtractOneUtil(Node* head)
{

    // Base Case
    if (head == NULL)
        return -1;

    // Recursively call for the next
    // node of the head
    int borrow = subtractOneUtil(
        head->next);

    // If there is a borrow
    if (borrow == -1) {

        // If the head data is 0, then
        // update it with 9 and return -1
        if (head->data == 0) {
            head->data = 9;
            return -1;
        }

        // Otherwise, decrement head's
        // data by 1 and return 0
        else {
            head->data = head->data - 1;
            return 0;
        }
    }

    // Otherwise, return 0
    else {
        return 0;
    }
}

// Function to subtract 1 from the given
// Linked List representation of number
Node* subtractOne(Node* head)
{

    // Recursively subtract 1 from
    // the Linked List
    subtractOneUtil(head);

    // Increment the head pointer
    // if there are any leading zeros
    while (head and head->next
           and head->data == 0) {
        head = head->next;
    }

    return head;
}

// Function to print a linked list
void printList(Node* node)
{
    // Iterate until node is NULL
    while (node != NULL) {
        cout << node->data;
        node = node->next;
    }
    cout << endl;
}

// Driver Code
int main()
{
    Node* head = newNode(1);
    head->next = newNode(0);
    head->next->next = newNode(0);
    head->next->next->next = newNode(0);

    cout << "List is ";
    printList(head);

    head = subtractOne(head);

    cout << "Resultant list is ";
    printList(head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Linked list Node
static class Node
{
    int data;
    Node next;
};

// Function to create a new node with
// the given data
static Node newNode(int data)
{

    // Create a new node
    Node new_node = new Node();
    new_node.data = data;
    new_node.next = null;

    // Return the created node
    return new_node;
}

// Recursive function to subtract 1
// from the linked list and update
// the node value accordingly
static  int subtractOneUtil(Node head)
{

    // Base Case
    if (head == null)
        return -1;

    // Recursively call for the next
    // node of the head
    int borrow = subtractOneUtil(
        head.next);

    // If there is a borrow
    if (borrow == -1)
    {

        // If the head data is 0, then
        // update it with 9 and return -1
        if (head.data == 0)
        {
            head.data = 9;
            return -1;
        }

        // Otherwise, decrement head's
        // data by 1 and return 0
        else
        {
            head.data = head.data - 1;
            return 0;
        }
    }

    // Otherwise, return 0
    else
    {
        return 0;
    }
}

// Function to subtract 1 from the given
// Linked List representation of number
static Node subtractOne(Node head)
{

    // Recursively subtract 1 from
    // the Linked List
    subtractOneUtil(head);

    // Increment the head pointer
    // if there are any leading zeros
    while (head != null && head.next != null &&
           head.data == 0)
    {
        head = head.next;
    }
    return head;
}

// Function to print a linked list
static void printList(Node node)
{

    // Iterate until node is null
    while (node != null)
    {
        System.out.print(node.data);
        node = node.next;
    }
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    Node head = newNode(1);
    head.next = newNode(0);
    head.next.next = newNode(0);
    head.next.next.next = newNode(0);

    System.out.print("List is ");
    printList(head);

    head = subtractOne(head);

    System.out.print("Resultant list is ");
    printList(head);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Linked list Node
class Node:

    def __init__(self, d):

        self.data = d
        self.next = None

# Recursive function to subtract 1
# from the linked list and update
# the node value accordingly
def subtractOneUtil(head):

    # Base Case
    if (head == None):
        return -1

    # Recursively call for the next
    # node of the head
    borrow = subtractOneUtil(head.next)

    # If there is a borrow
    if (borrow == -1):

        # If the head data is 0, then
        # update it with 9 and return -1
        if (head.data == 0):
            head.data = 9
            return -1

        # Otherwise, decrement head's
        # data by 1 and return 0
        else:
            head.data = head.data - 1
            return 0

    # Otherwise, return 0
    else:
        return 0

# Function to subtract 1 from the given
# Linked List representation of number
def subtractOne(head):

    # Recursively subtract 1 from
    # the Linked List
    subtractOneUtil(head)

    # Increment the head pointer
    # if there are any leading zeros
    while (head and head.next and
           head.data == 0):
        head = head.next

    return head

# Function to pra linked list
def printList(node):

    # Iterate until node is None
    while (node != None):
        print(node.data, end = "")
        node = node.next

    print()

# Driver Code
if __name__ == '__main__':

    head = Node(1)
    head.next = Node(0)
    head.next.next = Node(0)
    head.next.next.next = Node(0)

    print("List is ", end = "")
    printList(head)

    head = subtractOne(head)

    print("Resultant list is ", end = "")
    printList(head)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Linked list Node
class Node
{
    public int data;
    public Node next;
};

// Function to create a new node with
// the given data
static Node newNode(int data)
{

    // Create a new node
    Node new_node = new Node();
    new_node.data = data;
    new_node.next = null;

    // Return the created node
    return new_node;
}

// Recursive function to subtract 1
// from the linked list and update
// the node value accordingly
static  int subtractOneUtil(Node head)
{

    // Base Case
    if (head == null)
        return -1;

    // Recursively call for the next
    // node of the head
    int borrow = subtractOneUtil(
        head.next);

    // If there is a borrow
    if (borrow == -1)
    {

        // If the head data is 0, then
        // update it with 9 and return -1
        if (head.data == 0)
        {
            head.data = 9;
            return -1;
        }

        // Otherwise, decrement head's
        // data by 1 and return 0
        else
        {
            head.data = head.data - 1;
            return 0;
        }
    }

    // Otherwise, return 0
    else
    {
        return 0;
    }
}

// Function to subtract 1 from the given
// Linked List representation of number
static Node subtractOne(Node head)
{

    // Recursively subtract 1 from
    // the Linked List
    subtractOneUtil(head);

    // Increment the head pointer
    // if there are any leading zeros
    while (head != null && head.next != null &&
           head.data == 0)
    {
        head = head.next;
    }
    return head;
}

// Function to print a linked list
static void printList(Node node)
{

    // Iterate until node is null
    while (node != null)
    {
        Console.Write(node.data);
        node = node.next;
    }
    Console.WriteLine();
}

// Driver Code
public static void Main()
{
    Node head = newNode(1);
    head.next = newNode(0);
    head.next.next = newNode(0);
    head.next.next.next = newNode(0);

    Console.Write("List is ");
    printList(head);

    head = subtractOne(head);

    Console.Write("Resultant list is ");
    printList(head);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Linked list Node
class Node
{
    constructor()
    {
        this.next = null;
    }
}

// Function to create a new node with
// the given data
function newNode(data)
{

    // Create a new node
    let new_node = new Node();
    new_node.data = data;
    new_node.next = null;

    // Return the created node
    return new_node;
}

// Recursive function to subtract 1
// from the linked list and update
// the node value accordingly
function subtractOneUtil(head)
{

    // Base Case
    if (head == null)
        return -1;

    // Recursively call for the next
    // node of the head
    let borrow = subtractOneUtil(head.next);

    // If there is a borrow
    if (borrow == -1)
    {

        // If the head data is 0, then
        // update it with 9 and return -1
        if (head.data == 0)
        {
            head.data = 9;
            return -1;
        }

        // Otherwise, decrement head's
        // data by 1 and return 0
        else
        {
            head.data = head.data - 1;
            return 0;
        }
    }

    // Otherwise, return 0
    else
    {
        return 0;
    }
}

// Function to subtract 1 from the given
// Linked List representation of number
function subtractOne(head)
{

    // Recursively subtract 1 from
    // the Linked List
    subtractOneUtil(head);

    // Increment the head pointer
    // if there are any leading zeros
    while (head != null && head.next != null &&
           head.data == 0)
    {
        head = head.next;
    }
    return head;
}

// Function to print a linked list
function printList(node)
{

    // Iterate until node is null
    while (node != null)
    {
        document.write(node.data);
        node = node.next;
    }
    document.write("<br>");
}

// Driver Code
let head = newNode(1);
head.next = newNode(0);
head.next.next = newNode(0);
head.next.next.next = newNode(0);

document.write("List is ");
printList(head);

head = subtractOne(head);

document.write("Resultant list is ");
printList(head);

// This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
List is 1000
Resultant list is 999
```

***时间复杂度:** O(N)，N 是*[T5】给定链表](https://www.geeksforgeeks.org/find-length-of-a-linked-list-iterative-and-recursive/) *的长度。*
***辅助空间:** O(1)*