# 用于从链表中删除最后一个条目的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-用于从链接列表中删除最后出现的项目的程序/](https://www.geeksforgeeks.org/java-program-for-deleting-last-occurrence-of-an-item-from-linked-list/)

使用指针，循环遍历整个列表，并使用特殊指针跟踪包含最后一个出现键的节点之前的节点。在此之后，只需将特殊指针的下一个存储到特殊指针的下一个，以从链表中移除所需的节点。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement 
// the above approach
import java.io.*;

// A linked list Node
class Node
{
    int data; 
    Node next;

    Node(int data)
    {
        this.data = data;
        this.next = null;
    }
}

class GFG{

// Function to delete the last 
// occurrence
static Node deleteLast(Node head,
                       int x)
{
    Node temp = head;
    Node ptr = null;

    while (temp != null)
    {        
        // If found key, update
        if (temp.data == x)
            ptr = temp;

        temp = temp.next;
    }

    // If the last occurrence is the 
    // last node
    if (ptr != null && 
        ptr.next == null)
    {
        temp = head;

        while (temp.next != ptr)
        {
            temp = temp.next;
        }
        temp.next = null;
    }

    // If it is not the last node
    if (ptr != null && 
        ptr.next != null)
    {
        ptr.data = ptr.next.data;
        temp = ptr.next;
        ptr.next = ptr.next.next;
    }
    return head;
}

// This function prints contents of 
// linked list starting from the given 
// Node
static void display(Node head)
{
    Node temp = head;
    if (head == null)
    {
        System.out.print("NULL");
        return;
    }
    while (temp != null)
    {
        System.out.print(temp.data + 
                         " --> ");
        temp = temp.next;
    }
    System.out.print("NULL");
}

// Driver code
public static void main(String[] args)
{
    Node head = new Node(1);
    head.next = new Node(2);
    head.next.next = new Node(3);
    head.next.next.next = 
    new Node(4);
    head.next.next.next.next = 
    new Node(5);
    head.next.next.next.next.next = 
    new Node(4);
    head.next.next.next.next.next.next = 
    new Node(4);

    System.out.print(
           "Created Linked list: ");
    display(head);

    // Pass the address of the head 
    // pointer
    head = deleteLast(head, 4);
    System.out.print(
           "List after deletion of 4: ");
    display(head);
}
}
// This code is contributed by patel2127
```

**输出:**

```
Created Linked list: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> 4 --> NULL
List after deletion of 4: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> NULL
```

给定一个喜欢的列表和一个要删除的键。从链接中删除键的最后一次出现。该列表可能有重复项。

**示例**:

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

想法是从头到尾遍历链表。遍历时，跟踪最后一个出现的键。遍历完整列表后，通过复制下一个节点的数据并删除下一个节点来删除最后一个匹配项。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to demonstrate deletion 
// of last Node in singly linked list 
class GFG{

// A linked list Node 
static class Node 
{ 
    int key; 
    Node next; 
}; 

static Node deleteLast(Node head, 
                       int key) 
{ 
    // Initialize previous of Node to 
    // be deleted 
    Node x = null; 

    // Start from head and find the Node 
    // to be deleted 
    Node temp = head; 
    while (temp != null) 
    { 
        // If we found the key, 
        // update xv 
        if (temp.key == key) 
            x = temp; 

        temp = temp.next; 
    } 

    // Key occurs at-least once 
    if (x != null) 
    { 
        // Copy key of next Node to x 
        x.key = x.next.key; 

        // Store and unlink next 
        temp = x.next; 
        x.next = x.next.next; 

        // Free memory for next 
    } 
    return head;
} 

// Utility function to create a 
// new node with given key 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.key = key; 
    temp.next = null; 
    return temp; 
} 

// This function prints contents of 
// linked list starting from the given 
// Node 
static void printList( Node node) 
{ 
    while (node != null) 
    { 
        System.out.printf(" %d ", 
                          node.key); 
        node = node.next; 
    } 
} 

// Driver code
public static void main(String args[])
{ 
    // Start with the empty list
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = 
    newNode(5); 
    head.next.next.next.next = 
    newNode(2); 
    head.next.next.next.next.next = 
    newNode(10); 

    System.out.printf("Created Linked List: "); 
    printList(head); 
    deleteLast(head, 2); 
    System.out.printf(
           "Linked List after Deletion of 1: "); 
    printList(head); 
}
} 
// This code is contributed by Arnab Kundu
```

**输出:**

```
Created Linked List: 
1  2  3  5  2  10 
Linked List after Deletion of 1: 
1  2  3  5  10
```

**当要删除的节点是最后一个节点时，上述解决方案不起作用。**
以下方案处理所有案件。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate deletion 
// of last Node in singly linked list 
class GFG{

// A linked list Node 
static class Node 
{ 
    int data; 
    Node next; 
}; 

// Function to delete the last 
// occurrence 
static void deleteLast(Node head, 
                       int x) 
{ 
    Node temp = head, ptr = null; 
    while (temp!=null) 
    { 
        // If found key, update 
        if (temp.data == x) 
            ptr = temp;     
        temp = temp.next; 
    } 

    // If the last occurrence is the 
    // last node 
    if (ptr != null && 
        ptr.next == null) 
    { 
        temp = head; 
        while (temp.next != ptr) 
            temp = temp.next; 
        temp.next = null; 
    } 

    // If it is not the last node 
    if (ptr != null && 
        ptr.next != null)
    { 
        ptr.data = ptr.next.data; 
        temp = ptr.next; 
        ptr.next = ptr.next.next; 
        System.gc();
    } 
} 

/* Utility function to create a 
   new node with given key */
static Node newNode(int x) 
{ 
    Node node = new Node(); 
    node.data = x; 
    node.next = null; 
    return node; 
} 

// This function prints contents 
// of linked list starting from 
// the given Node 
static void display(Node head) 
{ 
    Node temp = head; 
    if (head == null) 
    { 
        System.out.print("null"); 
        return; 
    } 
    while (temp != null) 
    { 
        System.out.printf("%d --> ", 
                          temp.data); 
        temp = temp.next; 
    } 
    System.out.print("null"); 
} 

// Driver code
public static void main(String[] args) 
{
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = 
    newNode(4); 
    head.next.next.next.next = 
    newNode(5); 
    head.next.next.next.next.next = 
    newNode(4); 
    head.next.next.next.next.next.next = 
    newNode(4); 
    System.out.print(
    "Created Linked list: "); 
    display(head); 
    deleteLast(head, 4); 
    System.out.print(
    "List after deletion of 4: "); 
    display(head); 
}
}
// This code is contributed by PrinciRaj1992 
```

**输出:**

```
Created Linked List: 
1  2  3  4  5  4  4 
Linked List after Deletion of 1: 
1  2  3  4  5  4
```

详情请参考完整文章[从链表](https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/)中删除一项的最后一次出现！