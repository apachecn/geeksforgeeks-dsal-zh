# 删除链表中第一个出现节点 X 之后的所有出现的键 Y

> 原文:[https://www . geesforgeks . org/remove-所有出现的键-y-在第一个出现的节点-x-in-link-list/](https://www.geeksforgeeks.org/remove-all-occurrences-of-key-y-after-the-first-occurrence-node-x-in-linked-list/)

给定一个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)和两个整数 **X** 和 **Y** ，任务是在第一次出现值为 **X** 和[的节点后删除所有出现的 **Y** ，打印修改后的链表](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)。

**示例:**

> **输入:** 7 → 20 → 9 → 10 → 20 → 14 → 15 → 20，X = 10，Y = 20
> T3】输出: 7 → 20 → 9 → 10 → 14 → 15
> 
> **输入:** LL: 10 → 20，X = 10，Y = 20
> T3】输出: LL: 10

**方法:**给定的问题可以通过[遍历给定的链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)并删除所有出现在值为 **X** 的节点之后的值为 **Y** 的节点来解决。按照以下步骤解决问题:

*   初始化两个列表节点 **K** 和 **prev** ，存储给定[链表的当前头](https://www.geeksforgeeks.org/data-structures/linked-list/)和链表当前头的前一个节点。
*   [遍历给定的链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)直到 **K** 变为 **NULL** 并执行以下步骤:
    *   迭代**节点 K** 直到找到值为 **X** 的节点，同时更新节点 **prev** 为之前的**节点 K** 。
    *   将**节点 K** 存储在另一个变量中，比如说**温度**，[遍历链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)直到出现值为 **Y** 的节点，同时将节点 **prev** 更新为之前的**节点 K** 。
    *   如果**温度**的值为**空**，则[脱离回路](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将 **prev** 的下一个指针更新为**temp**的下一个指针，并将 **temp** 更新为节点 **prev** 的下一个指针。
*   完成以上步骤后，[打印修改后的链表](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
import java.util.LinkedList;

class Main {

    // Head of the linked list
    static Node head;

    // Structure of a node
    // of a Linked List
    class Node {
        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    // Function to delete all occurrences
    // of key after first occurrence of A
    void deleteKey(int A, int key)
    {
        // Stores the head node
        Node k = head, prev = null;

        while (k != null) {

            // Iterate until the
            // node A occurrs
            while (k != null
                   && k.data != A) {

                prev = k;
                k = k.next;
            }

            Node temp = k;

            while (temp != null
                   && temp.data != key) {
                prev = temp;
                temp = temp.next;
            }

            // If the entire linked
            // list has been traversed
            if (temp == null)
                return;

            // Update prev and temp node
            prev.next = temp.next;
            temp = prev.next;
        }
    }

    // Function to insert a new Node
    // at the front of the Linked List
    public void push(int new_data)
    {
        // Create a new node
        Node new_node = new Node(new_data);

        // Insert the node at the front
        new_node.next = head;

        // Update the head of LL
        head = new_node;
    }

    // Function to print the Linked List
    public void printList()
    {
        // Stores the head node
        Node tnode = head;

        // Traverse the Linked List
        while (tnode != null) {

            // Print the node
            System.out.print(tnode.data + " ");

            // Update tnode
            tnode = tnode.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        Main list = new Main();
        list.push(20);
        list.push(15);
        list.push(10);
        list.push(20);
        list.push(10);
        list.push(9);
        list.push(20);
        list.push(7);
        int X = 10;
        int Y = 20;

        list.deleteKey(X, Y);

        // Print the updated list
        list.printList();
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a node
# of a Linked List
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Function to delete all occurrences
# of key after first occurrence of A
def deleteKey(head, A, key):

    # Stores the head node
    k, prev = head, None

    while (k != None):

        # Iterate until the
        # node A occurrs
        while (k != None and k.data != A):
            prev = k
            k = k.next

        temp = k

        while (temp != None and temp.data != key):
            prev = temp
            temp = temp.next

        # If the entire linked
        # list has been traversed
        if (temp == None):
            return

        # Update prev and temp node
        prev.next = temp.next
        temp = prev.next

        return head

# Function to insert a new Node
# at the front of the Linked List
def push(head, new_data):

    # Create a new node
    new_node = Node(new_data)

    # Insert the node at the front
    new_node.next = head

    # Update the head of LL
    head = new_node
    return head

# Function to print the Linked List
def printList(head):

    # Stores the head node
    tnode = head

    # Traverse the Linked List
    while (tnode.next != None):

        # Print the node
        print(tnode.data, end = " ")

        # Update tnode
        tnode = tnode.next

# Driver Code
if __name__ == '__main__':

    list = None
    list = push(list, 20)
    list = push(list, 15)
    list = push(list, 10)
    list = push(list, 20)
    list = push(list, 10)
    list = push(list, 9)
    list = push(list, 20)
    list = push(list, 7)
    X = 10
    Y = 20

    list = deleteKey(list, X, Y)

    # Print the updated list
    printList(list)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class Node
{
    public int data;
    public Node next;

    public Node(int d)
    {
        data = d;
        next = null;
    }
}

class GFG{

// Head of the linked list
static Node head;

// Function to delete all occurrences
// of key after first occurrence of A
void deleteKey(int A, int key)
{

    // Stores the head node
    Node k = head, prev = null;

    while (k != null)
    {

        // Iterate until the
        // node A occurrs
        while (k != null && k.data != A)
        {
            prev = k;
            k = k.next;
        }

        Node temp = k;

        while (temp != null &&
               temp.data != key)
        {
            prev = temp;
            temp = temp.next;
        }

        // If the entire linked
        // list has been traversed
        if (temp == null)
            return;

        // Update prev and temp node
        prev.next = temp.next;
        temp = prev.next;
    }
}

// Function to insert a new Node
// at the front of the Linked List
public void push(int new_data)
{

    // Create a new node
    Node new_node = new Node(new_data);

    // Insert the node at the front
    new_node.next = head;

    // Update the head of LL
    head = new_node;
}

// Function to print the Linked List
public void printList()
{

    // Stores the head node
    Node tnode = head;

    // Traverse the Linked List
    while (tnode != null)
    {
        // Print the node
        Console.Write(tnode.data + " ");

        // Update tnode
        tnode = tnode.next;
    }
}

// Driver Code
static public void Main()
{
    GFG list = new GFG();
    list.push(20);
    list.push(15);
    list.push(10);
    list.push(20);
    list.push(10);
    list.push(9);
    list.push(20);
    list.push(7);
    int X = 10;
    int Y = 20;

    list.deleteKey(X, Y);

    // Print the updated list
    list.printList();
}
}

// This code is contributed by patel2127
```

## java 描述语言

```
<script>
    // javascript program for the above approach

    // Head of the linked list
    var head;

    // Structure of a node
    // of a Linked List
    class Node {
        constructor(val) {
            this.data = val;
            this.next = null;
        }
    }
    // Function to delete all occurrences
    // of key after first occurrence of A
    function deleteKey(A , key) {
        // Stores the head node
        var k = head, prev = null;

        while (k != null) {

            // Iterate until the
            // node A occurrs
            while (k != null && k.data != A) {

                prev = k;
                k = k.next;
            }

            var temp = k;

            while (temp != null && temp.data != key) {
                prev = temp;
                temp = temp.next;
            }

            // If the entire linked
            // list has been traversed
            if (temp == null)
                return;

            // Update prev and temp node
            prev.next = temp.next;
            temp = prev.next;
        }
    }

    // Function to insert a new Node
    // at the front of the Linked List
    function push(new_data) {
        // Create a new node
        var new_node = new Node(new_data);

        // Insert the node at the front
        new_node.next = head;

        // Update the head of LL
        head = new_node;
    }

    // Function to print the Linked List
    function printList() {
        // Stores the head node
        var tnode = head;

        // Traverse the Linked List
        while (tnode != null) {

            // Print the node
            document.write(tnode.data + " ");

            // Update tnode
            tnode = tnode.next;
        }
    }

    // Driver Code

        push(20);
        push(15);
        push(10);
        push(20);
        push(10);
        push(9);
        push(20);
        push(7);
        var X = 10;
        var Y = 20;

        deleteKey(X, Y);

        // Print the updated list
        printList();

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
7 20 9 10 10 15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)