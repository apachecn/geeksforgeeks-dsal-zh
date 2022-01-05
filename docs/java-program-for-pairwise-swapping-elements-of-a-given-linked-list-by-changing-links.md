# 通过改变链接成对交换给定链表元素的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-通过改变链接来成对交换给定链表的元素/](https://www.geeksforgeeks.org/java-program-for-pairwise-swapping-elements-of-a-given-linked-list-by-changing-links/)

给定一个单链表，编写一个成对交换元素的函数。例如，如果链表是 1->2->3->4->5->6->7，那么函数应该把它改成 2->1->4->3->6->5->7，如果链表是 1->2->3->4->5->6，那么函数应该把它改成 2->1->4->3->6->5

这个问题已经在[这里](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)讨论过了。这里提供的解决方案交换节点的数据。如果数据包含许多字段，将会有许多交换操作。所以一般来说，改变链接是一个更好的主意。下面是更改链接而不是交换数据的实现。

## 爪哇

```
// Java program to swap elements of 
// linked list by changing links
class LinkedList 
{
    static Node head;

    static class Node 
    {
        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap elements 
       of a linked list */
    Node pairWiseSwap(Node node)
    {
        // If linked list is empty or 
        // there is only one node in list
        if (node == null || 
            node.next == null) 
        {
            return node;
        }

        // Initialize previous and 
        // current pointers
        Node prev = node;
        Node curr = node.next;

        // Change head before proceeding
        node = curr; 

        // Traverse the list
        while (true) 
        {
            Node next = curr.next;

            // Change next of current as 
            // previous node
            curr.next = prev; 

            // If next NULL or next is the 
            // last node
            if (next == null || 
                next.next == null) 
            {
                prev.next = next;
                break;
            }

            // Change next of previous to 
            // next next
            prev.next = next.next;

            // Update previous and curr
            prev = next;
            curr = prev.next;
        }
        return node;
    }

    /* Function to print nodes in a 
       given linked list */
    void printList(Node node)
    {
        while (node != null) 
        {
            System.out.print(node.data + 
                             " ");
            node = node.next;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        /* The constructed linked list is:
           1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = 
        new Node(4);
        list.head.next.next.next.next = 
        new Node(5);
        list.head.next.next.next.next.next = 
        new Node(6);
        list.head.next.next.next.next.next.next = 
        new Node(7);

        System.out.println(
        "Linked list before calling pairwiseSwap() ");
        list.printList(head);
        Node st = list.pairWiseSwap(head);
        System.out.println("");
        System.out.println(
        "Linked list after calling pairwiseSwap() ");
        list.printList(st);
        System.out.println("");
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

**时间复杂度:**上述程序的时间复杂度为 O(n)，其中 n 为给定链表中的节点数。while 循环遍历给定的链表。

以下是相同方法的**递归实现**。我们更改前两个节点，并对剩余的列表重复执行。感谢 geek 和 omer salem 提出这个方法。

## 爪哇

```
// Java program to swap elements of 
// linked list by changing links

class LinkedList 
{
    static Node head;

    static class Node 
    {
        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to pairwise swap elements 
       of a linked list. It returns head 
       of the modified list, so return 
       value of this node must be assigned */
    Node pairWiseSwap(Node node)
    {
        // Base Case: The list is empty or 
        // has only one node
        if (node == null || 
            node.next == null) 
        {
            return node;
        }

        // Store head of list after two 
        // nodes
        Node remaining = node.next.next;

        // Change head
        Node newhead = node.next;

        // Change next of second node
        node.next.next = node;

        // Recur for remaining list and change 
        // next of head
        node.next = pairWiseSwap(remaining);

        // Return new head of modified list
        return newhead;
    }

    /* Function to print nodes in a 
       given linked list */
    void printList(Node node)
    {
        while (node != null) 
        {
            System.out.print(node.data + 
                             " ");
            node = node.next;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        /* The constructed linked list is:
           1->2->3->4->5->6->7 */
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = new Node(3);
        list.head.next.next.next = 
        new Node(4);
        list.head.next.next.next.next = 
        new Node(5);
        list.head.next.next.next.next.next = 
        new Node(6);
        list.head.next.next.next.next.next.next = 
        new Node(7);

        System.out.println(
        "Linked list before calling pairwiseSwap() ");
        list.printList(head);
        head = list.pairWiseSwap(head);
        System.out.println("");
        System.out.println(
        "Linked list after calling pairwiseSwap() ");
        list.printList(head);
        System.out.println("");
    }
}
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

更多细节请参考完整的文章[通过改变链接来成对交换给定链表的元素](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/)！