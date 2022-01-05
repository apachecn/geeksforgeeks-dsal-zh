# 删除链表中间的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序-删除-中间链表/](https://www.geeksforgeeks.org/java-program-to-delete-middle-of-linked-list/)

给定一个单链表，删除链表的中间。例如，如果给定的链表是 1->2->3->4->5，那么链表应该被修改为 1->2->4->5

如果有偶数个节点，那么就会有两个中间节点，我们需要删除第二个中间元素。例如，如果给定的链表是 1->2->3->4->5->6，那么它应该被修改为 1->2->3->5->6。
如果输入链表为空，那么应该保持为空。

如果输入的链表有 1 个节点，那么这个节点应该被删除，并返回一个新的头。

**简单的解决方案:**思路是先统计链表中的节点数，然后用简单的删除过程删除第 n/2 个节点。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete middle
// of a linked list
import java.io.*;
class GFG {

    // Link list Node 
    static class Node 
    {
        int data;
        Node next;
    }

    // Utility function to create 
    // a new node.
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.next = null;
        return temp;
    }

    // Count of nodes
    static int countOfNodes(Node head)
    {
        int count = 0;
        while (head != null) 
        {
            head = head.next;
            count++;
        }
        return count;
    }

    // Deletes middle node and returns
    // head of the modified list
    static Node deleteMid(Node head)
    {
        // Base cases
        if (head == null)
            return null;
        if (head.next == null) 
        {
            return null;
        }
        Node copyHead = head;

        // Find the count of nodes
        int count = countOfNodes(head);

        // Find the middle node
        int mid = count / 2;

        // Delete the middle node
        while (mid-- > 1) 
        {
            head = head.next;
        }

        // Delete the middle node
        head.next = head.next.next;

        return copyHead;
    }

    // A utility function to print
    // a given linked list
    static void printList(Node ptr)
    {
        while (ptr != null) 
        {
            System.out.print(ptr.data + 
                             "->");
            ptr = ptr.next;
        }
        System.out.println("NULL");
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with the empty list 
        Node head = newNode(1);
        head.next = newNode(2);
        head.next.next = newNode(3);
        head.next.next.next = newNode(4);

        System.out.println("Given Linked List");
        printList(head);
        head = deleteMid(head);
        System.out.println(
               "Linked List after deletion of middle");
        printList(head);
    }
}
// This code is contributed by rajsanghavi9
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    链表需要两次遍历
*   **辅助空间:** O(1)。
    不需要额外的空间。

**<u>高效解决方案:</u>**
**方法:**上述解决方案需要链表的两次遍历。中间节点可以通过一次遍历删除。想法是使用两个指针，slow_ptr 和 fast_ptr。两个指针都从列表头开始。当 fast_ptr 到达终点时，slow_ptr 到达中间。这个思路和[这个](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)帖子的方法二用的是一样的。这篇文章的额外内容是跟踪前一个中间节点，这样中间节点就可以被删除了。

下面是实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete the 
// middle of a linked list
class GfG 
{
    // Link list Node 
    static class Node 
    {
        int data;
        Node next;
    }

    // Deletes middle node and returns
    // head of the modified list
    static Node deleteMid(Node head)
    {
        // Base cases
        if (head == null)
            return null;
        if (head.next == null) 
        {
            return null;
        }

        // Initialize slow and fast pointers 
        // to reach middle of linked list
        Node slow_ptr = head;
        Node fast_ptr = head;

        // Find the middle and previous 
        // of middle.
        Node prev = null;

        // To store previous of slow_ptr
        while (fast_ptr != null && 
               fast_ptr.next != null) 
        {
            fast_ptr = fast_ptr.next.next;
            prev = slow_ptr;
            slow_ptr = slow_ptr.next;
        }

        // Delete the middle node
        prev.next = slow_ptr.next;

        return head;
    }

    // A utility function to print 
    // a given linked list
    static void printList(Node ptr)
    {
        while (ptr != null) 
        {
            System.out.print(ptr.data + "->");
            ptr = ptr.next;
        }
        System.out.println("NULL");
    }

    // Utility function to create a 
    // new node.
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.next = null;
        return temp;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with the empty list 
        Node head = newNode(1);
        head.next = newNode(2);
        head.next.next = newNode(3);
        head.next.next.next = newNode(4);

        System.out.println("Given Linked List");
        printList(head);
        head = deleteMid(head);
        System.out.println("Linked List after deletion of middle");
        printList(head);
    }
}
// This code is contributed by Prerna saini
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历链表一次
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

详情请参考[删除链表中间](https://www.geeksforgeeks.org/delete-middle-of-linked-list/)整篇文章！