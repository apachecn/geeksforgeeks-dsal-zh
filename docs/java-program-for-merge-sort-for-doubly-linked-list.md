# 双链表合并排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-merge-sort-for-double-link-list/](https://www.geeksforgeeks.org/java-program-for-merge-sort-for-doubly-linked-list/)

给定一个双向链表，编写一个函数，使用合并排序按升序对双向链表进行排序。
例如，下面的双向链表应该改为 24810

![](img/61dcfe5f15a4317c70a1bea6d144f1b2.png)

[单链表的合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)已经讨论过了。这里重要的变化是在合并两个列表时也要修改前面的指针。

下面是双链表合并排序的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement merge sort in 
// singly linked list
// Linked List Class
class LinkedList 
{
    // Head of list
    static Node head;  

    // Node Class 
    static class Node 
    {
        int data;
        Node next, prev;

        // Constructor to create a 
        // new node
        Node(int d) 
        {
            data = d;
            next = prev = null;
        }
    }

    void print(Node node) 
    {
        Node temp = node;
        System.out.println(
        "Forward Traversal using next pointer");
        while (node != null) 
        {
            System.out.print(node.data + " ");
            temp = node;
            node = node.next;
        }
        System.out.println(
        "Backward Traversal using prev pointer");
        while (temp != null) 
        {
            System.out.print(temp.data + " ");
            temp = temp.prev;
        }
    }

    // Split a doubly linked list (DLL) into 
    // 2 DLLs of half sizes
    Node split(Node head) 
    {
        Node fast = head, slow = head;
        while (fast.next != null && 
               fast.next.next != null) 
        {
            fast = fast.next.next;
            slow = slow.next;
        }
        Node temp = slow.next;
        slow.next = null;
        return temp;
    }

    Node mergeSort(Node node) 
    {
        if (node == null || 
            node.next == null) 
        {
            return node;
        }
        Node second = split(node);

        // Recur for left and right halves
        node = mergeSort(node);
        second = mergeSort(second);

        // Merge the two sorted halves
        return merge(node, second);
    }

    // Function to merge two linked lists
    Node merge(Node first, Node second) 
    {
        // If first linked list is empty
        if (first == null) 
        {
            return second;
        }

        // If second linked list is empty
        if (second == null) 
        {
            return first;
        }

        // Pick the smaller value
        if (first.data < second.data) 
        {
            first.next = merge(first.next, 
                               second);
            first.next.prev = first;
            first.prev = null;
            return first;
        } 
        else 
        {
            second.next = merge(first, 
                                second.next);
            second.next.prev = second;
            second.prev = null;
            return second;
        }
    }

    // Driver code
    public static void main(String[] args) 
    {
        LinkedList list = new LinkedList();
        list.head = new Node(10);
        list.head.next = new Node(30);
        list.head.next.next = new Node(3);
        list.head.next.next.next = 
        new Node(4);
        list.head.next.next.next.next = 
        new Node(20);
        list.head.next.next.next.next.next = 
        new Node(5);        

        Node node = null;
        node = list.mergeSort(head);
        System.out.println(
        "Linked list after sorting :");
        list.print(node);
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
Linked List after sorting
Forward Traversal using next pointer
3 4 5 10 20 30
Backward Traversal using prev pointer
30 20 10 5 4 3
```

**时间复杂度:**上述实现的时间复杂度与[数组合并排序](http://geeksquiz.com/merge-sort/)的时间复杂度相同。需要θ(nLogn)时间。

**空间复杂度:** O(1)。我们只使用恒定量的额外空间。
你可能还想看[快速排序双链表](https://www.geeksforgeeks.org/quicksort-for-linked-list/)T5】详情请参考[合并排序双链表](https://www.geeksforgeeks.org/merge-sort-for-doubly-linked-list/)完整文章！