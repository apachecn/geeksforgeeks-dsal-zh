# 对 K 排序的双向链表进行排序|集合 2(使用壳排序)

> 原文:[https://www . geesforgeks . org/sort-a-k-sorted-double-link-list-set-2-using-shell-sort/](https://www.geeksforgeeks.org/sort-a-k-sorted-doubly-linked-list-set-2-using-shell-sort/)

给定一个包含 N 个节点的[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，其中每个节点距离其在链表中的目标位置最多 K，任务是对给定的双链表进行排序。

**示例:**

> **输入:**dll:3<->【6】<->【2】>【12】>【56】<->8，K = 2
> 
> **输入:**dll:3<->【2】<<>><>输出:

**注意:**使用插入排序和使用[最小堆数据结构](https://www.geeksforgeeks.org/difference-between-min-heap-and-max-heap/)的方法[已经在](https://www.geeksforgeeks.org/insertion-sort/)[和](https://www.geeksforgeeks.org/sort-k-sorted-doubly-linked-list/)中讨论过。

**方法:** [Shell sort](https://www.geeksforgeeks.org/shellsort/) ，是 Insertion sort 的一个变种，也可以用来解决这个问题，用 **K** 代替 **N、**初始化间隙，因为列表已经是 **K-sorted 了。**

下面是上述方法的一个实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort a k sorted doubly

import java.util.*;

class DoublyLinkedList {
    static Node head;
    static class Node {
        int data;
        Node next, prev;
        Node(int d)
        {
            data = d;
            next = prev = null;
        }
    }

    // this method returns
    // the ceiling value of gap/2
    int nextGap(double gap)
    {
        if (gap < 2)
            return 0;
        return (int)Math.ceil(gap / 2);
    }

    // Sort a k sorted Doubly Linked List
    // Time Complexity: O(n*log k)
    // Space Complexity: O(1)
    Node sortAKSortedDLL(Node head, int k)
    {
        if (head == null || head.next == null)
            return head;

        // for all gaps
        for (int gap = k; gap > 0; gap = nextGap(gap)) {

            Node i = head, j = head;
            int count = gap;

            while (count-- > 0)
                j = j.next;

            for (; j != null; i = i.next, j = j.next) {

                // if data at jth node is less than
                // data at ith node
                if (i.data > j.data) {

                    // if i is head
                    // then replace head with j
                    if (i == head)
                        head = j;

                    // swap i & j pointers
                    Node iTemp = i;
                    i = j;
                    j = iTemp;

                    // i & j pointers are swapped because
                    // below code only swaps nodes by
                    // swapping their associated
                    // pointers(i.e. prev & next pointers)

                    // Now, swap both the
                    // nodes in linked list
                    Node iPrev = i.prev, iNext = i.next;
                    if (iPrev != null)
                        iPrev.next = j;
                    if (iNext != null)
                        iNext.prev = j;
                    i.prev = j.prev;
                    i.next = j.next;
                    if (j.prev != null)
                        j.prev.next = i;
                    if (j.next != null)
                        j.next.prev = i;
                    j.prev = iPrev;
                    j.next = iNext;
                }
            }
        }
        return head;
    }

    /* UTILITY FUNCTIONS */
    // Function to insert a node
    // at the beginning of the
    // Doubly Linked List
    void push(int new_data)
    {
        // allocate node
        Node new_node = new Node(new_data);

        // since we are adding at the beginning,
        // prev is always NULL
        new_node.prev = null;

        // link the old list off the new node
        new_node.next = head;

        // change prev of head node to new node
        if (head != null) {
            head.prev = new_node;
        }

        // move the head to point
        // to the new node
        head = new_node;
    }

    // Function to print nodes
    // in a given doubly linked list

    // This function is same as
    // printList() of singly linked list
    void printList(Node node)
    {
        while (node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        DoublyLinkedList list = new DoublyLinkedList();

        // 3<->6<->2<->12<->56<->8
        list.push(8);
        list.push(56);
        list.push(12);
        list.push(2);
        list.push(6);
        list.push(3);

        int k = 2;

        System.out.println("Original Doubly linked list:");
        list.printList(head);

        Node sortedDLL = list.sortAKSortedDLL(head, k);
        System.out.println("");
        System.out.println(
            "Doubly Linked List after sorting:");
        list.printList(sortedDLL);
    }
}
```

## C#

```
// C# implementation to sort a k sorted doubly
using System;

public class DoublyList {
    public static Node head;
   public  class Node {
      public   int data;
      public   Node next, prev;
      public   Node(int d)
        {
            data = d;
            next = prev = null;
        }
    }

    // this method returns
    // the ceiling value of gap/2
    int nextGap(double gap)
    {
        if (gap < 2)
            return 0;
        return (int)Math.Ceiling(gap / 2);
    }

    // Sort a k sorted Doubly Linked List
    // Time Complexity: O(n*log k)
    // Space Complexity: O(1)
    Node sortAKSortedDLL(Node head, int k)
    {
        if (head == null || head.next == null)
            return head;

        // for all gaps
        for (int gap = k; gap > 0; gap = nextGap(gap)) {

            Node i = head, j = head;
            int count = gap;

            while (count-- > 0)
                j = j.next;

            for (; j != null; i = i.next, j = j.next) {

                // if data at jth node is less than
                // data at ith node
                if (i.data > j.data) {

                    // if i is head
                    // then replace head with j
                    if (i == head)
                        head = j;

                    // swap i & j pointers
                    Node iTemp = i;
                    i = j;
                    j = iTemp;

                    // i & j pointers are swapped because
                    // below code only swaps nodes by
                    // swapping their associated
                    // pointers(i.e. prev & next pointers)

                    // Now, swap both the
                    // nodes in linked list
                    Node iPrev = i.prev, iNext = i.next;
                    if (iPrev != null)
                        iPrev.next = j;
                    if (iNext != null)
                        iNext.prev = j;
                    i.prev = j.prev;
                    i.next = j.next;
                    if (j.prev != null)
                        j.prev.next = i;
                    if (j.next != null)
                        j.next.prev = i;
                    j.prev = iPrev;
                    j.next = iNext;
                }
            }
        }
        return head;
    }

    /* UTILITY FUNCTIONS */
    // Function to insert a node
    // at the beginning of the
    // Doubly Linked List
    void Push(int new_data)
    {
        // allocate node
        Node new_node = new Node(new_data);

        // since we are adding at the beginning,
        // prev is always NULL
        new_node.prev = null;

        // link the old list off the new node
        new_node.next = head;

        // change prev of head node to new node
        if (head != null) {
            head.prev = new_node;
        }

        // move the head to point
        // to the new node
        head = new_node;
    }

    // Function to print nodes
    // in a given doubly linked list

    // This function is same as
    // printList() of singly linked list
    void printList(Node node)
    {
        while (node != null) {
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        DoublyList list = new DoublyList();

        // 3<->6<->2<->12<->56<->8
        list.Push(8);
        list.Push(56);
        list.Push(12);
        list.Push(2);
        list.Push(6);
        list.Push(3);

        int k = 2;

        Console.WriteLine("Original Doubly linked list:");
        list.printList(head);

        Node sortedDLL = list.sortAKSortedDLL(head, k);
        Console.WriteLine("");
        Console.WriteLine(
            "Doubly Linked List after sorting:");
        list.printList(sortedDLL);
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript implementation to sort a k sorted doubly
var  head;

    class Node {
        constructor(val) {
            this.data = val;
            this.prev = null;
            this.next = null;
        }
    }

    // this method returns
    // the ceiling value of gap/2
    function nextGap(gap) {
        if (gap < 2)
            return 0;
        return parseInt( Math.ceil(gap / 2));
    }

    // Sort a k sorted Doubly Linked List
    // Time Complexity: O(n*log k)
    // Space Complexity: O(1)
    function sortAKSortedDLL(head , k) {
        if (head == null || head.next == null)
            return head;

        // for all gaps
        for (var gap = k; gap > 0; gap = nextGap(gap)) {

    var i = head, j = head;
            var count = gap;

            while (count-- > 0)
                j = j.next;

            for (; j != null; i = i.next, j = j.next) {

                // if data at jth node is less than
                // data at ith node
                if (i.data > j.data) {

                    // if i is head
                    // then replace head with j
                    if (i == head)
                        head = j;

                    // swap i & j pointers
            var iTemp = i;
                    i = j;
                    j = iTemp;

                    // i & j pointers are swapped because
                    // below code only swaps nodes by
                    // swapping their associated
                    // pointers(i.e. prev & next pointers)

                    // Now, swap both the
                    // nodes in linked list
            var iPrev = i.prev, iNext = i.next;
                    if (iPrev != null)
                        iPrev.next = j;
                    if (iNext != null)
                        iNext.prev = j;
                    i.prev = j.prev;
                    i.next = j.next;
                    if (j.prev != null)
                        j.prev.next = i;
                    if (j.next != null)
                        j.next.prev = i;
                    j.prev = iPrev;
                    j.next = iNext;
                }
            }
        }
        return head;
    }

    /* UTILITY FUNCTIONS */
    // Function to insert a node
    // at the beginning of the
    // Doubly Linked List
    function push(new_data) {
        // allocate node
var new_node = new Node(new_data);

        // since we are adding at the beginning,
        // prev is always NULL
        new_node.prev = null;

        // link the old list off the new node
        new_node.next = head;

        // change prev of head node to new node
        if (head != null) {
            head.prev = new_node;
        }

        // move the head to point
        // to the new node
        head = new_node;
    }

    // Function to prvar nodes
    // in a given doubly linked list

    // This function is same as
    // printList() of singly linked list
    function printList(node) {
        while (node != null) {
            document.write(node.data + " ");
            node = node.next;
        }
    }

    // Driver code

        // 3<->6<->2<->12<->56<->8
        push(8);
        push(56);
        push(12);
        push(2);
        push(6);
        push(3);

        var k = 2;

        document.write("Original Doubly linked list:<br/>");
        printList(head);

var sortedDLL = sortAKSortedDLL(head, k);
        document.write("<br/>");
        document.write("Doubly Linked List after sorting:<br/>");
        printList(sortedDLL);
// This code contributed by umadevi9616
</script>
```

**Output:** 

```
Original Doubly linked list:
3 6 2 12 56 8 
Doubly Linked List after sorting:
2 3 6 8 12 56
```

**时间复杂度:** O(N*log K)
gap 用 K 初始化，每次迭代后降低到 gap/2 的上限值。因此，将计算 log k 间隙，并且对于每个间隙，将迭代列表。

**空间复杂度:** O(1)