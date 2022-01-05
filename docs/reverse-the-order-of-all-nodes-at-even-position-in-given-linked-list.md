# 反转给定链表中偶数位置所有节点的顺序

> 原文:[https://www . geeksforgeeks . org/反转给定链表中所有节点的顺序/](https://www.geeksforgeeks.org/reverse-the-order-of-all-nodes-at-even-position-in-given-linked-list/)

给定一个 **N** 个整数的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/) **A[]** ，任务是在偶数位置[反转所有整数](https://www.geeksforgeeks.org/reverse-a-linked-list/)的顺序。

**示例:**

> **输入:**A[]= 1->2->3->4->5->6->空
> T3】输出:1 6 3 4 5 2
> T6】说明:给定链表中偶数位置的节点为 2、4 和 6。所以，在颠倒了那里的顺序之后，新的链表将是 1->6->3->4->5->2->空。
> 
> **输入:** A[] = 1 - > 5 - > 3- >空
> T3】输出: 1 5 3

**方法:**给定的问题可以通过维护两个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)来解决，一个链表用于所有奇数位置的节点，另一个链表用于所有偶数位置的节点。[遍历给定的链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，该链表将被视为奇数链表。因此，对于偶数位置的所有节点，将其从奇数列表中移除，并将其插入偶数节点列表的前面。由于[节点添加在前面](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)处，它们的顺序将会颠倒。[将两个列表交替位置](https://www.geeksforgeeks.org/merge-a-linked-list-into-another-linked-list-at-alternate-positions/)合并，这是需要的答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node of the linked list
class Node {
public:
    int data;
    Node* next;
};

// Function to reverse all the even
// positioned node of given linked list
Node* reverse_even(Node* A)
{
    // Stores the nodes with
    // even positions
    Node* even = NULL;

    // Stores the nodes with
    // odd positions
    Node* odd = A;

    // If size of list is less that
    // 3, no change is required
    if (!odd || !odd->next || !odd->next->next)
        return odd;

    // Loop to traverse the list
    while (odd && odd->next) {

        // Store the even positioned
        // node in temp
        Node* temp = odd->next;
        odd->next = temp->next;

        // Add the even node to the
        // beginning of even list
        temp->next = even;

        // Make temp as new even list
        even = temp;

        // Move odd to it's next node
        odd = odd->next;
    }

    odd = A;

    // Merge the evenlist into
    // odd list alternatively
    while (even) {

        // Stores the even's next
        // node in temp
        Node* temp = even->next;

        // Link the next odd node
        // to next of even node
        even->next = odd->next;

        // Link even to next odd node
        odd->next = even;

        // Make new even as temp node
        even = temp;

        // Move odd to it's 2nd next node
        odd = odd->next->next;
    }

    return A;
}

// Function to add a node at
// the beginning of Linked List
void push(Node** head_ref, int new_data)
{
    Node* new_node = new Node();
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

// Function to print nodes
// in a given linked list
void printList(Node* node)
{
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
}

// Driver Code
int main()
{
    Node* start = NULL;

    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    start = reverse_even(start);
    printList(start);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Node of the linked list
static class Node {

    int data;
    Node next;
};
static Node start = null;
// Function to reverse all the even
// positioned node of given linked list
static Node reverse_even(Node A)
{
    // Stores the nodes with
    // even positions
    Node even = null;

    // Stores the nodes with
    // odd positions
    Node odd = A;

    // If size of list is less that
    // 3, no change is required
    if (odd==null || odd.next==null || odd.next.next==null)
        return odd;

    // Loop to traverse the list
    while (odd!=null && odd.next!=null) {

        // Store the even positioned
        // node in temp
        Node temp = odd.next;
        odd.next = temp.next;

        // Add the even node to the
        // beginning of even list
        temp.next = even;

        // Make temp as new even list
        even = temp;

        // Move odd to it's next node
        odd = odd.next;
    }

    odd = A;

    // Merge the evenlist into
    // odd list alternatively
    while (even!=null) {

        // Stores the even's next
        // node in temp
        Node temp = even.next;

        // Link the next odd node
        // to next of even node
        even.next = odd.next;

        // Link even to next odd node
        odd.next = even;

        // Make new even as temp node
        even = temp;

        // Move odd to it's 2nd next node
        odd = odd.next.next;
    }

    return A;
}

// Function to add a node at
// the beginning of Linked List
static void push(int new_data)
{
    Node new_node = new Node();
    new_node.data = new_data;
    new_node.next = start;
    start = new_node;
}

// Function to print nodes
// in a given linked list
static void printList(Node node)
{
    while (node != null) {
        System.out.print(node.data+ " ");
        node = node.next;
    }
}

// Driver Code
public static void main(String[] args)
{

    push(6);
    push(5);
    push(4);
    push(3);
    push(2);
    push(1);

    start = reverse_even(start);
    printList(start);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach
start = None

# Node of the linked list
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Function to reverse all the even
# positioned node of given linked list
def reverse_even(A):

    # Stores the nodes with
    # even positions
    even = None

    # Stores the nodes with
    # odd positions
    odd = A

    # If size of list is less that
    # 3, no change is required
    if (odd == None or odd.next == None or odd.next.next == None):
        return odd

    # Loop to traverse the list
    while (odd and odd.next):

        # Store the even positioned
        # node in temp
        temp = odd.next
        odd.next = temp.next

        # Add the even node to the
        # beginning of even list
        temp.next = even

        # Make temp as new even list
        even = temp

        # Move odd to it's next node
        odd = odd.next

    odd = A

    # Merge the evenlist into
    # odd list alternatively
    while (even):

        # Stores the even's next
        # node in temp
        temp = even.next

        # Link the next odd node
        # to next of even node
        even.next = odd.next

        # Link even to next odd node
        odd.next = even

        # Make new even as temp node
        even = temp

        # Move odd to it's 2nd next node
        odd = odd.next.next
    return A

# Function to add a node at
# the beginning of Linked List
def push(new_data):
    global start
    new_node = Node(new_data)
    new_node.next = start
    start = new_node

# Function to print nodes
# in a given linked list
def printList(node):
    while (node != None):
        print(node.data, end=" ")
        node = node.next

# Driver Code
start = None

push(6)
push(5)
push(4)
push(3)
push(2)
push(1)

start = reverse_even(start)
printList(start)

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
public class GFG{

// Node of the linked list
class Node {

    public int data;
    public Node next;
};
static Node start = null;

// Function to reverse all the even
// positioned node of given linked list
static Node reverse_even(Node A)
{

    // Stores the nodes with
    // even positions
    Node even = null;

    // Stores the nodes with
    // odd positions
    Node odd = A;

    // If size of list is less that
    // 3, no change is required
    if (odd==null || odd.next==null || odd.next.next==null)
        return odd;

    // Loop to traverse the list
    while (odd!=null && odd.next!=null) {

        // Store the even positioned
        // node in temp
        Node temp = odd.next;
        odd.next = temp.next;

        // Add the even node to the
        // beginning of even list
        temp.next = even;

        // Make temp as new even list
        even = temp;

        // Move odd to it's next node
        odd = odd.next;
    }

    odd = A;

    // Merge the evenlist into
    // odd list alternatively
    while (even!=null) {

        // Stores the even's next
        // node in temp
        Node temp = even.next;

        // Link the next odd node
        // to next of even node
        even.next = odd.next;

        // Link even to next odd node
        odd.next = even;

        // Make new even as temp node
        even = temp;

        // Move odd to it's 2nd next node
        odd = odd.next.next;
    }

    return A;
}

// Function to add a node at
// the beginning of Linked List
static void push(int new_data)
{
    Node new_node = new Node();
    new_node.data = new_data;
    new_node.next = start;
    start = new_node;
}

// Function to print nodes
// in a given linked list
static void printList(Node node)
{
    while (node != null) {
        Console.Write(node.data+ " ");
        node = node.next;
    }
}

// Driver Code
public static void Main(String[] args)
{
    push(6);
    push(5);
    push(4);
    push(3);
    push(2);
    push(1);

    start = reverse_even(start);
    printList(start);

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Node of the linked list
class Node {

    constructor(data) {
        this.data = data;
        this.next = null;
    }
};

// Function to reverse all the even
// positioned node of given linked list
function reverse_even(A) {
    // Stores the nodes with
    // even positions
    let even = null;

    // Stores the nodes with
    // odd positions
    let odd = A;

    // If size of list is less that
    // 3, no change is required
    if (odd == null || odd.next == null || odd.next.next == null)
        return odd;

    // Loop to traverse the list
    while (odd && odd.next) {

        // Store the even positioned
        // node in temp
        let temp = odd.next;
        odd.next = temp.next;

        // Add the even node to the
        // beginning of even list
        temp.next = even;

        // Make temp as new even list
        even = temp;

        // Move odd to it's next node
        odd = odd.next;
    }

    odd = A;

    // Merge the evenlist into
    // odd list alternatively
    while (even) {

        // Stores the even's next
        // node in temp
        let temp = even.next;

        // Link the next odd node
        // to next of even node
        even.next = odd.next;

        // Link even to next odd node
        odd.next = even;

        // Make new even as temp node
        even = temp;

        // Move odd to it's 2nd next node
        odd = odd.next.next;
    }

    return A;
}

// Function to add a node at
// the beginning of Linked List
function push(new_data) {
    let new_node = new Node();
    new_node.data = new_data;
    new_node.next = start;
    start = new_node;
}

// Function to print nodes
// in a given linked list
function printList(node) {
    while (node != null) {
        document.write(node.data + " ");
        node = node.next;
    }
}

// Driver Code
let start = null;

push(6);
push(5);
push(4);
push(3);
push(2);
push(1);

start = reverse_even(start);
printList(start);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
1 6 3 4 5 2 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)