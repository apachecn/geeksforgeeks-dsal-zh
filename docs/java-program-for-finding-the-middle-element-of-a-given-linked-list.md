# 寻找给定链表中间元素的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序-寻找给定链表的中间元素/](https://www.geeksforgeeks.org/java-program-for-finding-the-middle-element-of-a-given-linked-list/)

给定一个单链表，找到链表的中间。例如，如果给定的链表是 1->2->3->4->5，那么输出应该是 3。
如果有偶数个节点，那么就会有两个中间节点，我们需要打印第二个中间元素。例如，如果给定的链表是 1->2->3->4->5->6，那么输出应该是 4。

**方法 1:**
遍历整个链表，统计节点数。现在再次遍历列表，直到 count/2，并在 count/2 返回节点。

**方法 2:**
使用两个指针遍历链表。将一个指针移动一个，将另一个指针移动两个。当快速指针到达末尾时，慢速指针将到达链表的中间。

下图显示了 printMiddle 函数在代码中的工作方式:

![middle-of-a-given-linked-list-in-C-and-Java1](img/493d25a626ee5c18546ea813c81295e6.png)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find middle of 
// the linked list
class LinkedList
{
    // Head of linked list
    Node head; 

    // Linked list node 
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

    // Function to print middle of 
    // the linked list 
    void printMiddle()
    {
        Node slow_ptr = head;
        Node fast_ptr = head;
        if (head != null)
        {
            while (fast_ptr != null && 
                   fast_ptr.next != null)
            {
                fast_ptr = fast_ptr.next.next;
                slow_ptr = slow_ptr.next;
            }
            System.out.println("The middle element is [" +
                                slow_ptr.data + "]");
        }
    }

    // Inserts a new Node at front of the list.
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point to new Node 
        head = new_node;
    }

    // This function prints contents of linked list
    // starting from  the given node 
    public void printList()
    {
        Node tnode = head;
        while (tnode != null)
        {
            System.out.print(tnode.data + "->");
            tnode = tnode.next;
        }
        System.out.println("NULL");
    }

    // Driver code
    public static void main(String [] args)
    {
        LinkedList llist = new LinkedList();
        for (int i = 5; i > 0; --i)
        {
            llist.push(i);
            llist.printList();
            llist.printMiddle();
        }
    }
}
// This code is contributed by Rajat Mishra
```

**输出:**

```
5->NULL
The middle element is [5]

4->5->NULL
The middle element is [5]

3->4->5->NULL
The middle element is [4]

2->3->4->5->NULL
The middle element is [4]

1->2->3->4->5->NULL
The middle element is [3]
```

**方法 3:**
将中间元素初始化为 head，将一个计数器初始化为 0。从头开始遍历列表，遍历时递增计数器，当计数器为奇数时，将中间变为下一个中间>。所以 mid 只会移动列表总长度的一半。
感谢纳伦德拉·康拉尔卡尔提出这个方法。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
class GFG
{
    static Node head;

    // Link list node
    class Node
    {
        int data;
        Node next;

        // Constructor
        public Node(Node next, 
                    int data)
        {
            this.data = data;
            this.next = next;
        }
    }

    // Function to get the middle of 
    // the linked list
    void printMiddle(Node head)
    {
        int count = 0;
        Node mid = head;

        while (head != null)
        {
            // Update mid, when 'count' 
            // is odd number 
            if ((count % 2) == 1)
                mid = mid.next;

            ++count;
            head = head.next;
        }

        // If empty list is provided 
        if (mid != null)
            System.out.println("The middle element is [" +
                                mid.data + "]\n");
    }

    void push(Node head_ref, int new_data)
    {

        // Allocate node 
        Node new_node = new Node(head_ref, 
                                 new_data);

        // Move the head to point to the new node 
        head = new_node;
    }

    // A utility function to print a 
    // given linked list
    void printList(Node head)
    {
        while (head != null)
        {
            System.out.print(head.data + "-> ");
            head = head.next;
        }
        System.out.println("null");
    }

    // Driver code
    public static void main(String[] args)
    {
        GFG ll = new GFG();

        for(int i = 5; i > 0; i--) 
        {
            ll.push(head, i);
            ll.printList(head);
            ll.printMiddle(head);
        }
    }
}
// This code is contributed by mark_3
```

**输出:**

```
5->NULL
The middle element is [5]

4->5->NULL
The middle element is [5]

3->4->5->NULL
The middle element is [4]

2->3->4->5->NULL
The middle element is [4]

1->2->3->4->5->NULL
The middle element is [3]
```

更多详情请参考[找到给定链表](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)中间的整篇文章！