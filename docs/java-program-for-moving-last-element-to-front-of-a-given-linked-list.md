# 将最后一个元素移到给定链表前面的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-用于将最后一个元素移动到给定链表前面的程序/](https://www.geeksforgeeks.org/java-program-for-moving-last-element-to-front-of-a-given-linked-list/)

编写一个函数，在给定的单链表中把最后一个元素移到前面。例如，如果给定的链表是 1->2->3->4->5，那么函数应该将链表改为 5->1->2->3->4。
**算法:**
遍历列表直到最后一个节点。使用两个指针:一个存储最后一个节点的地址，另一个存储第二个最后一个节点的地址。循环结束后，执行以下操作。

1.  将倒数第二个设为最后一个(倒数第二个->下一个=空)。
2.  将倒数第二个设置为标题(最后->下一个= *head_ref)。
3.  将最后一个作为标题(*head_ref =最后一个)。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to move last element to 
   front in a given linked list */
class LinkedList
{
    // Head of list
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

    void moveToFront()
    {
        /* If linked list is empty or 
           it contains only one node 
           then simply return. */
           if(head == null || 
              head.next == null) 
              return;

        /* Initialize second last and 
           last pointers */
        Node secLast = null;
        Node last = head;

        /* After this loop secLast contains 
           address of second last  node and 
           last contains address of last node 
           in Linked List */
        while (last.next != null)  
        {
           secLast = last;
           last = last.next; 
        }

        // Set the next of second last as null 
        secLast.next = null;

        // Set the next of last as head 
        last.next = head;

        // Change head to point to 
        // last node. 
        head = last;
    }              

     // Utility functions 
    /* Inserts a new Node at front 
       of the list. */
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point to 
        // new Node 
        head = new_node;
    }

    // Function to print linked list 
    void printList()
    {
        Node temp = head;
        while(temp != null)
        {
           System.out.print(temp.data + " ");
           temp = temp.next;
        }  
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist = new LinkedList();

        /* Constructed Linked List is 
           1->2->3->4->5->null */
        llist.push(5);
        llist.push(4);
        llist.push(3);
        llist.push(2);
        llist.push(1);

        System.out.println(
               "Linked List before moving last to front ");
        llist.printList();

        llist.moveToFront();

        System.out.println(
               "Linked List after moving last to front ");
        llist.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
Linked list before moving last to front 
1 2 3 4 5 
Linked list after removing last to front 
5 1 2 3 4
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

详情请参考完整文章[将最后一个元素移到给定链表](https://www.geeksforgeeks.org/move-last-element-to-front-of-a-given-linked-list/)的前面！