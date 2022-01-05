# 用于就地重新排列给定链表的 Java 程序。

> 原文:[https://www . geeksforgeeks . org/Java-用于重新排列给定链接列表的程序-就地/](https://www.geeksforgeeks.org/java-program-for-rearranging-a-given-linked-list-in-place/)

给定一个单链表 L<sub>0</sub>->L<sub>1</sub>->……->L<sub>n-1</sub>->L<sub>n</sub>。重新排列列表中的节点，使新形成的列表为:L<sub>0</sub>->L<sub>n</sub>->L<sub>1</sub>->L<sub>n-1</sub>->L<sub>2</sub>->L<sub>n-2</sub>……
您需要在不改变节点值的情况下就地执行此操作。

**示例:**

```
Input: 1 -> 2 -> 3 -> 4
Output: 1 -> 4 -> 2 -> 3

Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 1 -> 5 -> 2 -> 4 -> 3
```

**简单解决方案:**

```
1) Initialize current node as head.
2) While next of current node is not null, do following
    a) Find the last node, remove it from the end and insert it as next
       of the current node.
    b) Move current to next to next of current
```

上述简单解法的时间复杂度为 O(n <sup>2</sup> )，其中 n 为链表中的节点数。

**更好的解决方案:**
1)将给定链表的内容复制到一个向量。
2)通过交换两端的节点来重新排列给定的向量。
3)将修改后的向量复制回链表。
此方法的实施:[https://ide.geeksforgeeks.org/1eGSEy](https://ide.geeksforgeeks.org/1eGSEy)
感谢阿鲁什·达美佳提出此方法。

**高效解决方案:**

```
1) Find the middle point using tortoise and hare method.
2) Split the linked list into two halves using found middle point in step 1.
3) Reverse the second half.
4) Do alternate merge of first and second halves.
```

该解决方案的时间复杂度为 0(n)。

下面是这个方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange linked list 
// in place

// Linked List Class
class LinkedList 
{
    // head of the list
    static Node head; 

    // Node Class 
    static class Node 
    {
        int data;
        Node next;

        // Constructor to create 
        // a new node
        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    void printlist(Node node)
    {
        if (node == null) 
        {
            return;
        }
        while (node != null) 
        {
            System.out.print(node.data + 
                             " -> ");
            node = node.next;
        }
    }

    Node reverselist(Node node)
    {
        Node prev = null, 
             curr = node, next;
        while (curr != null) 
        {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        node = prev;
        return node;
    }

    void rearrange(Node node)
    {
        // 1) Find the middle point using 
        // tortoise and hare method
        Node slow = node, fast = slow.next;
        while (fast != null && 
               fast.next != null) 
        {
            slow = slow.next;
            fast = fast.next.next;
        }

        // 2) Split the linked list in 
        // two halves
        // node1, head of first half- 
        // 1 -> 2 -> 3
        // node2, head of second half- 
        // 4 -> 5
        Node node1 = node;
        Node node2 = slow.next;
        slow.next = null;

        // 3) Reverse the second half, 
        // i.e., 5 -> 4
        node2 = reverselist(node2);

        // 4) Merge alternate nodes
        // Assign dummy Node
        node = new Node(0); 

        // curr is the pointer to this 
        // dummy Node, which will be 
        // used to form the new list
        Node curr = node;
        while (node1 != null || 
               node2 != null) 
        {
            // First add the element 
            // from first list
            if (node1 != null) 
            {
                curr.next = node1;
                curr = curr.next;
                node1 = node1.next;
            }

            // Then add the element from 
            // second list
            if (node2 != null) 
            {
                curr.next = node2;
                curr = curr.next;
                node2 = node2.next;
            }
        }

        // Assign the head of the new 
        // list to head pointer
        node = node.next;
    }

    // Driver code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();
        list.head = new Node(1);
        list.head.next = new Node(2);
        list.head.next.next = 
        new Node(3);
        list.head.next.next.next = 
        new Node(4);
        list.head.next.next.next.next = 
        new Node(5);

        // Print original list
        list.printlist(head); 

        // Rearrange list as per ques
        list.rearrange(head); 
        System.out.println("");

        // Print modified list
        list.printlist(head); 
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
1 -> 2 -> 3 -> 4 -> 5 
1 -> 5 -> 2 -> 4 -> 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
感谢高拉夫·阿希瓦尔提出上述方法。

**另一种做法:**
1。取两个指针 prev 和 curr，保存 head 和 head 的地址- >下一个。
2。比较他们的数据并交换。
之后，形成新的链表。

下面是实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to rearrange linked list 
// in place
class Geeks 
{
    static class Node 
    {
        int data;
        Node next;
    }

    // Function for rearranging a 
    // linked list with high and 
    // low value.
    static Node rearrange(Node head)
    {
        // Base case
        if (head == null) 
            return null;

        // Two pointer variable.
        Node prev = head, 
             curr = head.next;

        while (curr != null) 
        {
            // Swap function for swapping 
            // data.
            if (prev.data > curr.data) 
            {
                int t = prev.data;
                prev.data = curr.data;
                curr.data = t;
            }

            // Swap function for swapping data.
            if (curr.next != null && 
                curr.next.data > curr.data) 
            {
                int t = curr.next.data;
                curr.next.data = curr.data;
                curr.data = t;
            }

            prev = curr.next;

            if (curr.next == null)
                break;
            curr = curr.next.next;
        }
        return head;
    }

    // Function to insert a Node in
    // the linked list at the beginning.
    static Node push(Node head, int k)
    {
        Node tem = new Node();
        tem.data = k;
        tem.next = head;
        head = tem;
        return head;
    }

    // Function to display Node of 
    // linked list.
    static void display(Node head)
    {
        Node curr = head;
        while (curr != null) 
        {
            System.out.printf("%d ",
                              curr.data);
            curr = curr.next;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Node head = null;

        // Let create a linked list.
        // 9 . 6 . 8 . 3 . 7
        head = push(head, 7);
        head = push(head, 3);
        head = push(head, 8);
        head = push(head, 6);
        head = push(head, 9);
        head = rearrange(head);
        display(head);
    }
}
// This code is contributed by Arnab Kundu
```

**输出:**

```
6 9 3 8 7
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
感谢[阿迪蒂亚](https://auth.geeksforgeeks.org/user/aditya1011/articles)提出这个方法。

**另一种方法:**(使用递归)

1.  持有指向头节点的指针，并使用递归一直到最后一个节点
2.  到达最后一个节点后，开始将最后一个节点交换到下一个头节点
3.  将头指针移动到下一个节点
4.  重复此操作，直到头部和最后一个节点相遇或相邻
5.  一旦满足停止条件，我们需要丢弃左边的节点，以修复交换节点时在列表中创建的循环。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
import java.io.*;
// Java program to implement
// the above approach
// Creating the structure 
// for node
class Node 
{
    int data;
    Node next;

    // Function to create newNode 
    // in a linkedlist
    Node(int key)
    {
        data = key;
        next = null;
    }
}
class GFG 
{
    Node left = null;

    // Function to print the list
    void printlist(Node head)
    {
        while (head != null) 
        {
            System.out.print(head.data + 
                             " ");
            if (head.next != null) 
            {
                System.out.print("->");
            }
            head = head.next;
        }
        System.out.println();
    }

    // Function to rearrange
    void rearrange(Node head)
    {
        if (head != null) 
        {
            left = head;
            reorderListUtil(left);
        }
    }

    void reorderListUtil(Node right)
    {
        if (right == null) 
        {
            return;
        }

        reorderListUtil(right.next);

        // We set left = null, when we 
        // reach stop condition, so no 
        // processing required after that
        if (left == null) 
        {
            return;
        }

        // Stop condition: odd case : 
        // left = right, even
        // case : left.next = right
        if (left != right && 
            left.next != right) 
        {
            Node temp = left.next;
            left.next = right;
            right.next = temp;
            left = temp;
        }
        else 
        { 
            // stop condition , set null 
            // to left nodes
            if (left.next == right) 
            {
                // even case
                left.next.next = null; 
                left = null;
            }
            else 
            {
                // odd case
                left.next = null; 
                left = null;
            }
        }
    }

    // Drivers Code
    public static void main(String[] args)
    {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = 
        new Node(4);
        head.next.next.next.next = 
        new Node(5);

        GFG gfg = new GFG();

        // Print original list
        gfg.printlist(head);        

        // Modify the list
        gfg.rearrange(head);

        // Print modified list
        gfg.printlist(head);
    }
}
// This code is contributed by Vishal Singh
```

**输出:**

```
1 ->2 ->3 ->4 ->5 
1 ->5 ->2 ->4 ->3
```

请参考[上的完整文章，就地重新排列给定的链表。](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/)了解更多详情！