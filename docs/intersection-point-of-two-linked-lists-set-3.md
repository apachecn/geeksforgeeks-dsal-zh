# 两个链表的交点|集合 3

> 原文:[https://www . geesforgeks . org/两个链表的交叉点-set-3/](https://www.geeksforgeeks.org/intersection-point-of-two-linked-lists-set-3/)

给定两个由**正值节点**组成的 **N** 和 **M** 大小的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，它们有一个公共的交点，任务是[找到这两个链表的交点，它们在这里合并](https://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)。

**示例:**

> **输入:** L1: 3 → 6 → 9 → 15 → 30，L2: 10 → 15 → 30
> **输出:** 15
> **说明:**
> 
> [![](img/ab40c195e60241fe31989a627ddf41fc.png)](https://www.geeksforgeeks.org/wp-content/uploads/2009/10/Y-ShapedLinked-List.gif)
> 
> 从上图看，两个链表的交点是 15。
> 
> **输入:** L1: 1 → 2 → 3，L2:4→5→1→2→3
> T3】输出: 1

**方法:**思路是遍历第一个链表，将每个节点的值乘以-1，使其为负。然后，[遍历第二个链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，打印第一个节点的负值。按照以下步骤解决问题:

*   [遍历第一个链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)**【L1】**，将每个节点的值乘以 **-1** 。
*   现在，遍历第二个链表 **L2** ，如果存在任何具有负值的节点，则打印该节点值的绝对值，作为链表和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)的结果交集。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a node
// of a Linked List
class Node {
public:
    int data;
    Node* next;

    // Constructor
    Node(int x)
    {
        data = x;
        next = NULL;
    }
};

// Function to find the intersection
// point of the two Linked Lists
Node* intersectingNode(Node* headA,
                       Node* headB)
{

    // Traverse the first linked list
    // and multiply all values by -1
    Node* a = headA;

    while (a) {

        // Update a -> data
        a->data *= -1;

        // Update a
        a = a->next;
    }

    // Traverse the second Linked List
    // and find the value of the first
    // node having negative value
    Node* b = headB;

    while (b) {

        // Intersection point
        if (b->data < 0)
            break;

        // Update b
        b = b->next;
    }

    return b;
}

// Function to create linked lists
void formLinkList(Node*& head1,
                  Node*& head2)
{
    // Linked List L1
    head1 = new Node(3);
    head1->next = new Node(6);
    head1->next->next = new Node(9);
    head1->next->next->next = new Node(15);
    head1->next->next->next->next = new Node(30);

    // Linked List L2
    head2 = new Node(10);
    head2->next = head1->next->next->next;

    return;
}

// Driver Code
int main()
{
    Node* head1;
    Node* head2;
    formLinkList(head1, head2);

    cout << abs(intersectingNode(head1,
                                 head2)
                    ->data);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

static Node head1 = null;
static Node head2 = null;

// Structure of a node
// of a Linked List
static class Node
{
    int data;
    Node next;

    // Constructor
    Node(int x)
    {
        data = x;
        next = null;
    }
}

// Function to find the intersection
// point of the two Linked Lists
static Node intersectingNode(Node headA, Node headB)
{

    // Traverse the first linked list
    // and multiply all values by -1
    Node a = headA;

    while (a != null)
    {

        // Update a -> data
        a.data *= -1;

        // Update a
        a = a.next;
    }

    // Traverse the second Linked List
    // and find the value of the first
    // node having negative value
    Node b = headB;

    while (b != null)
    {

        // Intersection point
        if (b.data < 0)
            break;

        // Update b
        b = b.next;
    }
    return b;
}

// Function to create linked lists
static void formLinkList()
{

    // Linked List L1
    head1 = new Node(3);
    head1.next = new Node(6);
    head1.next.next = new Node(9);
    head1.next.next.next = new Node(15);
    head1.next.next.next.next = new Node(30);

    // Linked List L2
    head2 = new Node(10);
    head2.next = head1.next.next.next;

    return;
}

// Driver Code
public static void main(String[] args)
{
    formLinkList();

    System.out.println(Math.abs(
        intersectingNode(head1, head2).data));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a node
# of a Linked List
class Node:

    def __init__(self, d):

        self.data = d
        self.next = None

# Function to find the intersection
# point of the two Linked Lists
def intersectingNode(headA, headB):

    # Traverse the first linked list
    # and multiply all values by -1
    a = headA

    while (a):

        # Update a . data
        a.data *= -1

        # Update a
        a = a.next

    # Traverse the second Linked List
    # and find the value of the first
    # node having negative value
    b = headB

    while (b):

        # Intersection point
        if (b.data < 0):
            break

        # Update b
        b = b.next

    return b

# Function to create linked lists
def formLinkList(head1, head2):

    # Linked List L1
    head1 = Node(3)
    head1.next = Node(6)
    head1.next.next = Node(9)
    head1.next.next.next = Node(15)
    head1.next.next.next.next = Node(30)

    # Linked List L2
    head2 = Node(10)
    head2.next = head1.next.next.next

    return head1, head2

# Driver Code
if __name__ == '__main__':

    head1, head2 = formLinkList(None, None)

    print(abs(intersectingNode(head1, head2).data))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;

public class Node
{
    public int data;
    public Node next;

    // Constructor
    public Node(int x)
    {
        data = x;
        next = null;
    }
}

public class GFG{

    static Node head1 = null;
static Node head2 = null;
// Function to find the intersection
// point of the two Linked Lists
static Node intersectingNode(Node headA, Node headB)
{

    // Traverse the first linked list
    // and multiply all values by -1
    Node a = headA;

    while (a != null)
    {

        // Update a -> data
        a.data *= -1;

        // Update a
        a = a.next;
    }

    // Traverse the second Linked List
    // and find the value of the first
    // node having negative value
    Node b = headB;

    while (b != null)
    {

        // Intersection point
        if (b.data < 0)
            break;

        // Update b
        b = b.next;
    }
    return b;
}

// Function to create linked lists
static void formLinkList()
{

    // Linked List L1
    head1 = new Node(3);
    head1.next = new Node(6);
    head1.next.next = new Node(9);
    head1.next.next.next = new Node(15);
    head1.next.next.next.next = new Node(30);

    // Linked List L2
    head2 = new Node(10);
    head2.next = head1.next.next.next;

    return;
}

// Driver Code

    static public void Main ()
    {

        formLinkList();

    Console.WriteLine(Math.Abs(
        intersectingNode(head1, head2).data));

    }
}

// This code is contributed by unknown2108.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let head1 = null;
let head2 = null;

// Structure of a node
// of a Linked List
class Node
{
    constructor(x)
    {
        this.data=x;
        this.next=null;
    }
}

// Function to find the intersection
// point of the two Linked Lists
function intersectingNode(headA,headB)
{
    // Traverse the first linked list
    // and multiply all values by -1
    let a = headA;

    while (a != null)
    {

        // Update a -> data
        a.data *= -1;

        // Update a
        a = a.next;
    }

    // Traverse the second Linked List
    // and find the value of the first
    // node having negative value
    let b = headB;

    while (b != null)
    {

        // Intersection point
        if (b.data < 0)
            break;

        // Update b
        b = b.next;
    }
    return b;
}

// Function to create linked lists
function formLinkList()
{
    // Linked List L1
    head1 = new Node(3);
    head1.next = new Node(6);
    head1.next.next = new Node(9);
    head1.next.next.next = new Node(15);
    head1.next.next.next.next = new Node(30);

    // Linked List L2
    head2 = new Node(10);
    head2.next = head1.next.next.next;

    return;
}

// Driver Code
formLinkList();

document.write(Math.abs(
intersectingNode(head1, head2).data));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
15
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*