# 在交替位置将一个链表合并到另一个链表的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-merge-a-link-list-in-other-link-list-at-alternate-position/](https://www.geeksforgeeks.org/java-program-to-merge-a-linked-list-into-another-linked-list-at-alternate-positions/)

给定两个链表，在第一个链表的交替位置将第二个链表的节点插入第一个链表。
例如，如果第一个列表是 5- > 7- > 17- > 13- > 11，第二个是 12- > 10- > 2- > 4- > 6，则第一个列表应该变成 5->12->7->10->17->2->13->4->11->仅当有位置可用时，才应插入第二个列表的节点。例如，如果第一个列表是 1- > 2- > 3，第二个列表是 4- > 5- > 6- > 7- > 8，那么第一个列表应该变成 1->4->2->5->3->6，第二个列表变成 7- > 8。
不允许使用额外的空间(不允许创建额外的节点)，即必须就地插入。预期的时间复杂度是 O(n)，其中 n 是第一个列表中的节点数。

想法是在第一个循环中有可用位置时运行一个循环，并通过更改指针来插入第二个列表的节点。下面是这种方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to merge a linked list 
// into another at alternate positions
class LinkedList
{
    // head of list
    Node head;  

    // Linked list Node
    class Node
    {
        int data;
        Node next;
        Node(int d) 
        {
            data = d; 
            next = null; 
        }
    }

    /* Inserts a new Node at front 
       of the list. */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        /* 4\. Move the head to point to new 
              Node */
        head = new_node;
    }

    // Main function that inserts nodes of 
    // linked list q into p at alternate positions. 
    // Since head of first list never changes and 
    // head of second list/ may change, we need single
    // pointer for first list and double pointer for 
    // second list.
    void merge(LinkedList q)
    {
        Node p_curr = head, 
             q_curr = q.head;
        Node p_next, q_next;

        // While there are available positions 
        // in p;
        while (p_curr != null && 
               q_curr != null) 
        {
            // Save next pointers
            p_next = p_curr.next;
            q_next = q_curr.next;

            // make q_curr as next of p_curr
            // change next pointer of q_curr
            q_curr.next = p_next; 

            // change next pointer of p_curr
            p_curr.next = q_curr; 

            // update current pointers for 
            // next iteration
            p_curr = p_next;
            q_curr = q_next;
        }
        q.head = q_curr;
    }

    // Function to print linked list 
    void printList()
    {
        Node temp = head;
        while (temp != null)
        {
           System.out.print(temp.data + " ");
           temp = temp.next;
        }
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist1 = 
        new LinkedList();
        LinkedList llist2 = 
        new LinkedList();
        llist1.push(3);
        llist1.push(2);
        llist1.push(1);

        System.out.println(
               "First Linked List:");
        llist1.printList();

        llist2.push(8);
        llist2.push(7);
        llist2.push(6);
        llist2.push(5);
        llist2.push(4);

        System.out.println(
               "Second Linked List:");

        llist1.merge(llist2);

        System.out.println(
               "Modified first linked list:");
        llist1.printList();

        System.out.println(
               "Modified second linked list:");
        llist2.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
First Linked List:
1 2 3
Second Linked List:
4 5 6 7 8
Modified First Linked List:
1 4 2 5 3 6
Modified Second Linked List:
7 8 
```

更多详情请参考[完整文章在](https://www.geeksforgeeks.org/merge-a-linked-list-into-another-linked-list-at-alternate-positions/)交替位置将链表合并成另一个链表！