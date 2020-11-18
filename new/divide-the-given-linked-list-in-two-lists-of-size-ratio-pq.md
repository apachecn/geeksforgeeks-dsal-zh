# 将给定的链表分为两个比例为 p：q 的列表

> 原文：[https://www.geeksforgeeks.org/divide-the-given-linked-list-in-two-lists-of-size-ratio-pq/](https://www.geeksforgeeks.org/divide-the-given-linked-list-in-two-lists-of-size-ratio-pq/)

给定一个链表和两个整数 **p** 和 **q** ，任务是按 **p：q** 的比例划分链表，即第一个列表包含第一个[ **来自原始列表的 p 个**节点，第二个列表包含 **q** 个节点的其余部分。 如果无法按照给定的比例分割原始列表，请打印 **-1** 。

**示例**：

> **输入**：1-> 3-> 5-> 6-> 7-> 2-> NULL
> p = 2，q = 4 [
> **输出**：
> 1 3
> 5 6 7 2
> 
> **输入**：1-> 2-> 4-> 9->空
> p = 3，q = 2
> **输出**：-1

**方法**：首先找到链表的长度。 如果总和超过实际长度，则无法分割列表，因此打印 **-1** 。 如果可以划分列表，则只需遍历列表，直到长度为 **p** ，然后将其分解为 **p：q** 的比率即可。 下一个节点将成为第二个列表的头，然后打印两个列表。

下面是上述方法的实现：

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

// Node 
static class Node 
{ 
    int data; 
    Node next; 
    Node(int data) 
    { 
        this.data = data; 
    } 
} 

// Function to split the given linked list  
// into ratio of p and q  
static void splitAndPrint(Node head,int p,int q) 
{ 
    int n = 0; 
    Node temp; 
    temp = head; 

    // Find the length of the list 
    while(temp!=null) 
    { 
        n += 1; 
        temp = temp.next; 
    } 

    // If ration exceeds the actual length 
    if (p + q > n) 
    { 
        System.out.println("-1"); 
        return; 
    } 
    temp = head; 
    while(p > 1) 
    { 
        temp = temp.next; 
        p-= 1; 
    } 

    // second head node after splitting 
    Node head2 = temp.next; 
    temp.next = null; 

    // Print first linked list 
    printList(head); 
    System.out.println(); 

    // Print second linked list 
    printList(head2); 
} 

// Function to print the nodes  
// of the linked list 
static void printList(Node head) 
{ 
    if( head == null) 
        return; 
    System.out.print(head.data+" , "); 
    printList(head.next); 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node head = new Node(1); 
    head.next = new Node(3); 
    head.next.next = new Node(5); 
    head.next.next.next = new Node(6); 
    head.next.next.next.next = new Node(7); 
    head.next.next.next.next.next = new Node(2); 

    int p =2,q= 4; 
    splitAndPrint(head, p, q); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python3 implementation of the approach 

# Linked List node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to split the given linked list  
# into ratio of p and q  
def splitAndPrint(head, p, q): 
    n, temp = 0, head 

    # Find the length of the list 
    while(temp): 
        n += 1
        temp = temp.next

    # If ration exceeds the actual length 
    if p + q>n: 
        print("-1") 
        return

    temp = head 
    while(p>1): 
        temp = temp.next
        p-= 1

    # second head node after splitting 
    head2 = temp.next
    temp.next = None

    # Print first linked list 
    printList(head) 
    print() 

    # Print second linked list 
    printList(head2) 

# Function to print the nodes  
# of the linked list 
def printList(head): 
    if not head: 
        return
    print("{} ".format(head.data), end ="") 
    printList(head.next) 

# Driver code 
head = Node(1) 
head.next = Node(3) 
head.next.next = Node(5) 
head.next.next.next = Node(6) 
head.next.next.next.next = Node(7) 
head.next.next.next.next.next = Node(2) 

p, q = 2, 4
splitAndPrint(head, p, q) 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG  
{  

public class Node  
{  
    public int data;  
    public Node next;  
    public Node(int data)  
    {  
        this.data = data;  
    }  
}  

// Function to split the given linked list  
// into ratio of p and q  
static void splitAndPrint(Node head,int p,int q)  
{  
    int n = 0;  
    Node temp;  
    temp = head;  

    // Find the length of the list  
    while(temp != null)  
    {  
        n += 1;  
        temp = temp.next;  
    }  

    // If ration exceeds the actual length  
    if (p + q > n)  
    {  
        Console.WriteLine("-1");  
        return;  
    }  
    temp = head;  
    while(p > 1)  
    {  
        temp = temp.next;  
        p-= 1;  
    }  

    // second head node after splitting  
    Node head2 = temp.next;  
    temp.next = null;  

    // Print first linked list  
    printList(head);  
    Console.WriteLine();  

    // Print second linked list  
    printList(head2);  
}  

// Function to print the nodes  
// of the linked list  
static void printList(Node head)  
{  
    if( head == null)  
        return;  
    Console.Write(head.data+" ");  
    printList(head.next);  
}  

// Driver code  
public static void Main(String []args)  
{  
    Node head = new Node(1);  
    head.next = new Node(3);  
    head.next.next = new Node(5);  
    head.next.next.next = new Node(6);  
    head.next.next.next.next = new Node(7);  
    head.next.next.next.next.next = new Node(2);  

    int p = 2, q = 4;  
    splitAndPrint(head, p, q);  
}  
}  

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1 3 
5 6 7 2

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。