# 链表节点的和，链表的值正好包含三个因子

> 原文:[https://www . geeksforgeeks . org/其值包含三个精确因子的链表节点总和/](https://www.geeksforgeeks.org/sum-of-nodes-of-linked-list-whose-contains-values-with-exactly-three-factors/)

给定一个包含 **N** 个节点的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是找出该列表中所有可能节点的和，该列表包含恰好具有三个不同因素的[值。](https://www.geeksforgeeks.org/check-whether-number-exactly-three-distinct-factors-not/)

**示例:**

> **输入:**1->2->4->5
> **输出:** 4
> **解释:**
> 2 的因子为{1，2 }
> 3 的因子为{1，3 }
> 4 的因子为{1，2，4 }
> 5 的因子为{1，5}
> 因为只有 4 包含三个不同的因子。因此，所需的输出为 4。
> 
> **输入:** 1 - > 6 - > 8 - > 10
> **输出:** 0

**方法:**这个想法是基于这样一个事实:如果一个[数是一个质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)，那么这个数的平方正好包含三个不同的[因子](https://www.geeksforgeeks.org/perfect-square-factors-of-a-number/)。按照以下步骤解决问题:

*   初始化一个变量，比如**节点总和**，来存储节点的总和，这些节点包含正好三个不同因子的值。
*   [遍历链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，对于每个节点，检查当前节点的[平方根](https://www.geeksforgeeks.org/square-root-of-an-integer/)是否为[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。如果发现为真，则用当前节点的值增加**节点总和**。
*   最后，打印**节点总和**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a
// singly Linked List
struct Node {

    // Stores data value
    // of a Node
    int data;

    // Stores pointer
    // to next Node
    struct Node* next;
};

// Function to insert a node at the
// beginning of the singly Linked List
void push(Node** head_ref,
          int new_data)
{
    // Create a new Node
    Node* new_node = new Node;

    // Insert the data into
    // the Node
    new_node->data = new_data;

    // Insert pointer to
    // the next Node
    new_node->next = (*head_ref);

    // Update head_ref
    (*head_ref) = new_node;
}

// Function to check if a number
// is a prime number or not
bool CheckPrimeNumber(int n)
{
    // Base Case
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If n is multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over the range
    // [5, sqrt(N)]
    for (int i = 5; i * i <= n;
         i = i + 6) {

        // If n is multiple of
        // i or (i + 2)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }

    return true;
}

// Function to check if number is
// a perfect square number or not
bool checkperfect_square(int n)
{
    // Stores square root of n
    long double sr = sqrt(n);

    // If n is a
    // perfect square number
    if (sr - floor(sr) == 0) {
        return true;
    }

    return false;
}

// Function to check if n is square
// of a prime number or not
bool is_square(int n)
{
    // If n is a perfect square
    if (checkperfect_square(n)) {

        // Stores sqrt of n
        int root = sqrt(n);

        // If root is a prime number
        if (CheckPrimeNumber(root)) {
            return true;
        }
    }
    return false;
}

// Function to find sum of node values
// which contains three distinct factors
int calculate_sum(struct Node* head)
{

    // Stores head of
    // the linked list
    Node* curr = head;

    // Stores sum of nodes whose data value
    // contains three distinct factors
    int nodeSum = 0;

    // Traverse the linked list
    while (curr) {

        // If data value of curr is
        // square of a prime number
        if (is_square(curr->data)) {

            // Update nodeSum
            nodeSum += curr->data;
        }

        // Update curr
        curr = curr->next;
    }

    // Return sum
    return nodeSum;
}

// Driver Code
int main()
{
    // Stores head node of
    // the linked list
    Node* head = NULL;

    // Insert all data values
    // in the linked list
    push(&head, 5);
    push(&head, 4);
    push(&head, 2);
    push(&head, 1);

    cout << calculate_sum(head);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of a
// singly Linked List
static class Node
{

    // Stores data value
    // of a Node
    int data;

    // Stores pointer
    // to next Node
    Node next;
};

static  Node head = null;

// Function to insert a node at the
// beginning of the singly Linked List
static Node push(int new_data)
{

    // Create a new Node
    Node new_node = new Node();

    // Insert the data into
    // the Node
    new_node.data = new_data;

    // Insert pointer to
    // the next Node
    new_node.next = head;

    // Update head_ref
    return head = new_node;
}

// Function to check if a number
// is a prime number or not
static boolean CheckPrimeNumber(int n)
{

    // Base Case
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If n is multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over the range
    // [5, Math.sqrt(N)]
    for(int i = 5; i * i <= n; i = i + 6)
    {

        // If n is multiple of
        // i or (i + 2)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }
    return true;
}

// Function to check if number is
// a perfect square number or not
static boolean checkperfect_square(int n)
{

    // Stores square root of n
    long sr = (long)Math.sqrt(n);

    // If n is a
    // perfect square number
    if (sr - Math.floor(sr) == 0)
    {
        return true;
    }
    return false;
}

// Function to check if n is square
// of a prime number or not
static boolean is_square(int n)
{

    // If n is a perfect square
    if (checkperfect_square(n))
    {

        // Stores sqrt of n
        int root = (int)Math.sqrt(n);

        // If root is a prime number
        if (CheckPrimeNumber(root))
        {
            return true;
        }
    }
    return false;
}

// Function to find sum of node values
// which contains three distinct factors
static int calculate_sum(Node head)
{

    // Stores head of
    // the linked list
    Node curr = head;

    // Stores sum of nodes whose data value
    // contains three distinct factors
    int nodeSum = 0;

    // Traverse the linked list
    while (curr.next != null)
    {

        // If data value of curr is
        // square of a prime number
        if (is_square(curr.data))
        {

            // Update nodeSum
            nodeSum += curr.data;
        }

        // Update curr
        curr = curr.next;
    }

    // Return sum
    return nodeSum;
}

// Driver Code
public static void main(String[] args)
{

    // Stores head node of
    // the linked list

    // Insert all data values
    // in the linked list
    head = push(5);
    head = push(4);
    head = push(2);
    head = push(1);

    System.out.print(calculate_sum(head));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Structure of a
# singly linked list
class Node:

    def __init__(self, data):

        self.data = data
        self.next = None

class LinkedList:

    def __init__(self):

        self.head = None

    # Function to insert a nodeat the
    # beginning of the singly linked list
    def Push(self, new_data):

        # Create new node
        # and insert the data
        # into the node
        new_node = Node(new_data)

        # Insert pointer to the
        # next node
        new_node.next = self.head

        # Update head
        self.head = new_node

    # Function to find sum of node values
    # which contains three distinct factors
    def calculate_sum(self):

        # Stores the head of linked list
        curr = self.head

        # Stores sum of nodes whose data
        # value contains three distinct factors
        nodeSum = 0

        # Traverse the linked list
        while(curr):

            # If data value of curr is
            # square of a prime number
            if (is_square(curr.data)):

                # Update nodeSum
                nodeSum += curr.data

            # Update curr    
            curr = curr.next

        # Return Sum
        return nodeSum

# Function to check if a number
# is a prime number or not
def CheckPrimeNumber(n):

    # Base Class
    if n <= 1:
        return False
    if n <= 3:
        return True

    # If n is multiple of 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Iterate over the range
    # [5,sqrt(N)]
    i = 5
    while ((i * i) <= n):

        # If n is multiple of
        # i or (i+2)
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i += 6

    return True

 # Function to check if number is
# a perfect square number or not
def checkperfect_square(n):

    # Stores square root of n
    sr = math.sqrt(n)

    # If n is a perfect
    # square number
    if (sr - math.floor(sr)) == 0:
        return True

    return False

# Function to check if n is square
# of a prime number or not
def is_square(n):

    # If n is a perfect square
    if (checkperfect_square(n)):

        # Stores sqrt of n
        root = math.sqrt(n)

        # If root is a prime number
        if (CheckPrimeNumber(root)):
            return True

    return False

# Driver Code
if __name__ == "__main__" :

    LList = LinkedList()

    # Insert all data values
    # in the linked list
    LList.Push(5)
    LList.Push(4)
    LList.Push(2)
    LList.Push(1)

    print(LList.calculate_sum())

# This code is contributed by Virusbuddah
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Structure of a
// singly Linked List
public class Node
{

    // Stores data value
    // of a Node
    public int data;

    // Stores pointer
    // to next Node
    public Node next;
};

static  Node head = null;

// Function to insert a node at the
// beginning of the singly Linked List
static Node push(int new_data)
{

    // Create a new Node
    Node new_node = new Node();

    // Insert the data into
    // the Node
    new_node.data = new_data;

    // Insert pointer to
    // the next Node
    new_node.next = head;

    // Update head_ref
    return head = new_node;
}

// Function to check if a number
// is a prime number or not
static bool CheckPrimeNumber(int n)
{

    // Base Case
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If n is multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over the range
    // [5, Math.Sqrt(N)]
    for(int i = 5; i * i <= n; i = i + 6)
    {

        // If n is multiple of
        // i or (i + 2)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }
    return true;
}

// Function to check if number is
// a perfect square number or not
static bool checkperfect_square(int n)
{

    // Stores square root of n
    long sr = (long)Math.Sqrt(n);

    // If n is a perfect square number
    if (sr - Math.Floor((double)sr) == 0)
    {
        return true;
    }
    return false;
}

// Function to check if n is square
// of a prime number or not
static bool is_square(int n)
{

    // If n is a perfect square
    if (checkperfect_square(n))
    {

        // Stores sqrt of n
        int root = (int)Math.Sqrt(n);

        // If root is a prime number
        if (CheckPrimeNumber(root))
        {
            return true;
        }
    }
    return false;
}

// Function to find sum of node values
// which contains three distinct factors
static int calculate_sum(Node head)
{

    // Stores head of
    // the linked list
    Node curr = head;

    // Stores sum of nodes whose data value
    // contains three distinct factors
    int nodeSum = 0;

    // Traverse the linked list
    while (curr.next != null)
    {

        // If data value of curr is
        // square of a prime number
        if (is_square(curr.data))
        {

            // Update nodeSum
            nodeSum += curr.data;
        }

        // Update curr
        curr = curr.next;
    }

    // Return sum
    return nodeSum;
}

// Driver Code
public static void Main(String[] args)
{

    // Stores head node of
    // the linked list

    // Insert all data values
    // in the linked list
    head = push(5);
    head = push(4);
    head = push(2);
    head = push(1);

    Console.Write(calculate_sum(head));
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Structure of a
// singly Linked List
class Node
{
    constructor()
    {

    // Stores data value
    // of a Node
    this.data = 0;

    // Stores pointer
    // to next Node
    this.next = null;
    }

};

var head = null;

// Function to insert a node at the
// beginning of the singly Linked List
function push(new_data)
{

    // Create a new Node
    var new_node = new Node();

    // Insert the data into
    // the Node
    new_node.data = new_data;

    // Insert pointer to
    // the next Node
    new_node.next = head;

    // Update head_ref
    return head = new_node;
}

// Function to check if a number
// is a prime number or not
function CheckPrimeNumber(n)
{

    // Base Case
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If n is multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over the range
    // [5, Math.Sqrt(N)]
    for(var i = 5; i * i <= n; i = i + 6)
    {

        // If n is multiple of
        // i or (i + 2)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }
    return true;
}

// Function to check if number is
// a perfect square number or not
function checkperfect_square(n)
{

    // Stores square root of n
    var sr = Math.sqrt(n);

    // If n is a perfect square number
    if (sr - Math.floor(sr) == 0)
    {
        return true;
    }
    return false;
}

// Function to check if n is square
// of a prime number or not
function is_square(n)
{

    // If n is a perfect square
    if (checkperfect_square(n))
    {

        // Stores sqrt of n
        var root = Math.sqrt(n);

        // If root is a prime number
        if (CheckPrimeNumber(root))
        {
            return true;
        }
    }
    return false;
}

// Function to find sum of node values
// which contains three distinct factors
function calculate_sum(head)
{

    // Stores head of
    // the linked list
    var curr = head;

    // Stores sum of nodes whose data value
    // contains three distinct factors
    var nodeSum = 0;

    // Traverse the linked list
    while (curr.next != null)
    {

        // If data value of curr is
        // square of a prime number
        if (is_square(curr.data))
        {

            // Update nodeSum
            nodeSum += curr.data;
        }

        // Update curr
        curr = curr.next;
    }

    // Return sum
    return nodeSum;
}

// Driver Code
// Stores head node of
// the linked list

// Insert all data values
// in the linked list
head = push(5);
head = push(4);
head = push(2);
head = push(1);
document.write(calculate_sum(head));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * √ X)，其中 X 是链表中最大的元素*
***辅助空间:** O(1)*