# 用于排序已按绝对值排序的链表的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-用于排序的程序-链表-绝对值排序/](https://www.geeksforgeeks.org/java-program-for-sorting-linked-list-which-is-already-sorted-on-absolute-values/)

给定一个基于绝对值排序的链表。根据实际值对列表进行排序。
**例:**

```
Input:  1 -> -10 
Output: -10 -> 1

Input: 1 -> -2 -> -3 -> 4 -> -5 
Output: -5 -> -3 -> -2 -> 1 -> 4 

Input: -5 -> -10 
Output: -10 -> -5

Input: 5 -> 10 
Output: 5 -> 10
```

来源:[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-258-for-sde1/)

一个简单的解决方案是从头到尾遍历链表。对于每个被访问的节点，检查它是否有问题。如果是，将其从当前位置移除，并将其插入正确的位置。这是链表的[插入排序的实现，这个解决方案的时间复杂度是 O(n*n)。
更好的解决方案是](http://geeksquiz.com/insertion-sort-for-singly-linked-list/)[使用合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对链表进行排序。这个解决方案的时间复杂度是 O(n Log n)。
高效的解决方案可以在 O(n)时间内工作。一个重要的观察是，所有的负元素都以相反的顺序出现。所以我们遍历列表，每当我们发现一个元素有问题，我们就把它移到链表的前面。
以下是上述思路的实现。

一旦我们发现一个元素有问题，我们就把它移到链表的前面。
以下是上述思路的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a linked list, 
// already sorted by absolute values
class SortList
{
    // Head of list
    static Node head;  

    // Linked list Node
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

    // To sort a linked list by actual values.
    // The list is assumed to be sorted by 
    // absolute values.
    Node sortedList(Node head)
    {
        // Initialize previous and current 
        // nodes
        Node prev = head;
        Node curr = head.next;

        // Traverse list
        while(curr != null)
        {
            // If curr is smaller than prev, 
            // then it must be moved to head
            if(curr.data < prev.data)
            {
                // Detach curr from linked list
                prev.next = curr.next;

                // Move current node to beginning
                curr.next = head;
                head = curr;

                // Update current
                curr = prev;
            }

            // Nothing to do if current element
            // is at right place
            else
            prev = curr;

            // Move current
            curr = curr.next;
        }
        return head;
    }

    /* Inserts a new Node at front of 
       the list. */
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point 
        // to new Node 
        head = new_node;
    }

    // Function to print linked list 
    void printList(Node head)
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
        SortList llist = new SortList();

        /* Constructed Linked List is 
           1->2->3->4->5->6->
           7->8->8->9->null */
        llist.push(-5);
        llist.push(5);
        llist.push(4);
        llist.push(3);
        llist.push(-2);
        llist.push(1);
        llist.push(0);

        System.out.println("Original List :");
        llist.printList(llist.head);

        llist.head = llist.sortedList(head);

        System.out.println("Sorted list :");
        llist.printList(llist.head);
    }
} 

// This code is contributed by Amit Khandelwal(Amit Khandelwal 1).
```

**输出:**

```
Original list :
0 -> 1 -> -2 -> 3 -> 4 -> 5 -> -5
Sorted list :
-5 -> -2 -> 0 -> 1 -> 3 -> 4 -> 5
```

详见[排序链表整篇文章，该链表已经按绝对值](https://www.geeksforgeeks.org/sort-linked-list-already-sorted-absolute-values/)排序！