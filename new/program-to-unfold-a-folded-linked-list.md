# 程序展开折叠的链表

> 原文：[https://www.geeksforgeeks.org/program-to-unfold-a-folded-linked-list/](https://www.geeksforgeeks.org/program-to-unfold-a-folded-linked-list/)

链表 **L <sub>0</sub> -> L <sub>1</sub> -> L <sub>2</sub> ->…..-> L <sub>N</sub>** 可以折叠为 **L <sub>0</sub> -> L <sub>N</sub> -> L <sub>1</sub> - > L <sub>N – 1</sub> -> L <sub>2</sub> ->…..**

给定一个折叠链表，任务是展开并 打印原始链表

**示例**：

> **输入**：1-> 6-> 2-> 5-> 3-> 4
> **输出**：1 2 3 4 5 6
> 
> **输入**：1-> 5-> 2-> 4-> 3
> **输出**：1 2 3 4 5

**方法**：进行递归调用并将下一个节点存储在 temp 指针中，第一个节点将充当头节点，而存储在 temp 指针中的节点将充当列表的尾部。 到达基本状态后返回时，将头和尾分别链接到先前的头和​​尾。

**基本条件**：如果节点数为偶数，则倒数第二个节点为 head，最后一个节点为 tail，如果节点数为奇数，则最后一个节点将同时充当 head 和 tail 。

下面是上述方法的实现：

## Java

```java

// Java implementation of the approach 
public class GFG { 

    // Node Class 
    private class Node { 
        int data; 
        Node next; 
    } 

    // Head of the list 
    private Node head; 

    // Tail of the list 
    private Node tail; 

    // Function to print the list 
    public void display() 
    { 

        if (head == null) 
            return; 
        Node temp = head; 

        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    // Funcion to add node in the list 
    public void push(int data) 
    { 

        // Create new node 
        Node nn = new Node(); 
        nn.data = data; 
        nn.next = null; 

        // Linking at first position 
        if (head == null) { 
            head = nn; 
        } 
        else { 
            Node temp = head; 

            while (temp.next != null) { 
                temp = temp.next; 
            } 

            // Linking at last in list 
            temp.next = nn; 
        } 
    } 

    // Function to unfold the given link list 
    private void unfold(Node node) 
    { 
        if (node == null) 
            return; 

        // This condition will reach if 
        // the number of nodes is odd 
        // head and tail is same i.e. last node 
        if (node.next == null) { 
            head = tail = node; 
            return; 
        } 

        // This base condition will reach if 
        // the number of nodes is even 
        // mark head to the second last node 
        // and tail to the last node 
        else if (node.next.next == null) { 
            head = node; 
            tail = node.next; 
            return; 
        } 

        // Storing next node in temp pointer 
        // before making the recursive call 
        Node temp = node.next; 

        // Recursive call 
        unfold(node.next.next); 

        // Connecting first node to head 
        // and mark it as a new head 
        node.next = head; 
        head = node; 

        // Connecting tail to second node (temp) 
        // and mark it as a new tail 
        tail.next = temp; 
        tail = temp; 
        tail.next = null; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        GFG l = new GFG(); 

        // Adding nodes to the list 
        l.push(1); 
        l.push(5); 
        l.push(2); 
        l.push(4); 
        l.push(3); 

        // Displaying the original nodes 
        l.display(); 

        // Calling unfold function 
        l.unfold(l.head); 

        // Displaying the list 
        // after modification 
        l.display(); 
    } 
} 

```

## C#

```cs

// C# implementation of the approach 
using System; 
public class GFG { 

    // Node Class 
    private class Node { 
        public int data; 
        public Node next; 
    } 

    // Head of the list 
    private Node head; 

    // Tail of the list 
    private Node tail; 

    // Function to print the list 
    public void display() 
    { 

        if (head == null) 
            return; 
        Node temp = head; 

        while (temp != null) { 
            Console.Write(temp.data + " "); 
            temp = temp.next; 
        } 
        Console.WriteLine(); 
    } 

    // Funcion to add node in the list 
    public void push(int data) 
    { 

        // Create new node 
        Node nn = new Node(); 
        nn.data = data; 
        nn.next = null; 

        // Linking at first position 
        if (head == null) { 
            head = nn; 
        } 
        else { 
            Node temp = head; 

            while (temp.next != null) { 
                temp = temp.next; 
            } 

            // Linking at last in list 
            temp.next = nn; 
        } 
    } 

    // Function to unfold the given link list 
    private void unfold(Node node) 
    { 
        if (node == null) 
            return; 

        // This condition will reach if 
        // the number of nodes is odd 
        // head and tail is same i.e. last node 
        if (node.next == null) { 
            head = tail = node; 
            return; 
        } 

        // This base condition will reach if 
        // the number of nodes is even 
        // mark head to the second last node 
        // and tail to the last node 
        else if (node.next.next == null) { 
            head = node; 
            tail = node.next; 
            return; 
        } 

        // Storing next node in temp pointer 
        // before making the recursive call 
        Node temp = node.next; 

        // Recursive call 
        unfold(node.next.next); 

        // Connecting first node to head 
        // and mark it as a new head 
        node.next = head; 
        head = node; 

        // Connecting tail to second node (temp) 
        // and mark it as a new tail 
        tail.next = temp; 
        tail = temp; 
        tail.next = null; 
    } 

    // Driver code 
    public static void Main() 
    { 

        GFG l = new GFG(); 

        // Adding nodes to the list 
        l.push(1); 
        l.push(5); 
        l.push(2); 
        l.push(4); 
        l.push(3); 

        // Displaying the original nodes 
        l.display(); 

        // Calling unfold function 
        l.unfold(l.head); 

        // Displaying the list 
        // after modification 
        l.display(); 
    } 
} 
/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
1 5 2 4 3 
1 2 3 4 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。