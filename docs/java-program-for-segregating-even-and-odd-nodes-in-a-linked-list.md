# 用于在链表中分离偶数和奇数节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-隔离链表中奇偶节点的程序/](https://www.geeksforgeeks.org/java-program-for-segregating-even-and-odd-nodes-in-a-linked-list/)

给定一个整数链表，编写一个函数来修改链表，使得在修改后的链表中，所有偶数出现在所有奇数之前。此外，保持偶数和奇数的顺序相同。
**例:**

```
Input: 17->15->8->12->10->5->4->1->7->6->NULL
Output: 8->12->10->4->6->17->15->5->1->7->NULL

Input: 8->12->10->5->4->1->6->NULL
Output: 8->12->10->4->6->5->1->NULL

// If all numbers are even then do not change the list
Input: 8->12->10->NULL
Output: 8->12->10->NULL

// If all numbers are odd then do not change the list
Input: 1->3->5->7->NULL
Output: 1->3->5->7->NULL
```

**方法 1:**
思路是获取指向列表最后一个节点的指针。然后从头节点开始遍历列表，并将奇数值节点从它们的当前位置移动到列表的末尾。
感谢浮躁小子提出这个方法。
**算法:**

1.  获取指向最后一个节点的指针。
2.  将所有奇数节点移动到最后。
    *   考虑第一个偶数节点之前的所有奇数节点，并将它们移动到末尾。
    *   将头指针更改为指向第一个偶数节点。
    *   考虑第一个偶数节点之后的所有奇数节点，并将它们移动到最后。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to segregate even and
// odd nodes in a Linked List
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

    void segregateEvenOdd()
    {
        Node end = head;
        Node prev = null;
        Node curr = head;

        // Get pointer to last Node
        while (end.next != null)
            end = end.next;

        Node new_end = end;

        // Consider all odd nodes before
        // getting first eve node
        while (curr.data % 2 !=0 &&
               curr != end)
        {
            new_end.next = curr;
            curr = curr.next;
            new_end.next.next = null;
            new_end = new_end.next;
        }

        // Do following steps only if
        // there is an even node
        if (curr.data % 2 == 0)
        {
            head = curr;

            // Now curr points to first even node
            while (curr != end)
            {
                if (curr.data % 2 == 0)
                {
                    prev = curr;
                    curr = curr.next;
                }
                else
                {
                    /* Break the link between prev
                       and curr*/
                    prev.next = curr.next;

                    // Make next of curr as null
                    curr.next = null;

                    // Move curr to end
                    new_end.next = curr;

                    // Make curr as new end of list
                    new_end = curr;

                    // Update curr pointer
                    curr = prev.next;
                }
            }
        }

        /* We have to set prev before
           executing rest of this code */
        else prev = curr;

        if (new_end != end &&
            end.data %2 != 0)
        {
            prev.next = end.next;
            end.next = null;
            new_end.next = end;
        }
    }

    /*  Given a reference (pointer to pointer)
        to the head of a list and an int, push
        a new node on the front of the list. */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head
        new_node.next = head;

        // 4\. Move the head to point to
        //    new Node
        head = new_node;
    }

    // Utility function to print
    // a linked list
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
        llist.push(11);
        llist.push(10);
        llist.push(8);
        llist.push(6);
        llist.push(4);
        llist.push(2);
        llist.push(0);
        System.out.println(
               "Original Linked List");
        llist.printList();

        llist.segregateEvenOdd();

        System.out.println(
               "Modified Linked List");
        llist.printList();
    }
}
// This code is contributed by Rajat Mishra
```

**输出:**

```
Original Linked list 0 2 4 6 8 10 11
Modified Linked list 0 2 4 6 8 10 11
```

**时间复杂度:** O(n)

**方法二:**
思路是把链表一分为二:一个包含所有偶数节点，另一个包含所有奇数节点。最后，在偶数节点链表之后附加奇数节点链表。
要拆分链表，遍历原始链表，将所有奇数节点移动到所有奇数节点的单独链表中。在循环结束时，原始列表将包含所有偶数节点，奇数节点列表将包含所有奇数节点。为了保持所有节点的顺序相同，我们必须在奇数节点列表的末尾插入所有奇数节点。为了在恒定时间内做到这一点，我们必须跟踪奇数节点列表中的最后一个指针。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to segregate even and
// odd nodes in a Linked List
import java.io.*;

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

    public void segregateEvenOdd()
    {       
        Node evenStart = null;
        Node evenEnd = null;
        Node oddStart = null;
        Node oddEnd = null;
        Node currentNode = head;

        while(currentNode != null)
        {
            int element = currentNode.data;

            if(element % 2 == 0)
            {               
                if(evenStart == null)
                {
                    evenStart = currentNode;
                    evenEnd = evenStart;
                }
                else
                {
                    evenEnd.next = currentNode;
                    evenEnd = evenEnd.next;
                }

            }
            else
            {               
                if(oddStart == null)
                {
                    oddStart = currentNode;
                    oddEnd = oddStart;
                }
                else
                {
                    oddEnd.next = currentNode;
                    oddEnd = oddEnd.next;
                }
            }

            // Move head pointer one step
            // in forward direction
            currentNode = currentNode.next;   
        }       

        if(oddStart == null ||
           evenStart == null)
        {
            return;
        }

        evenEnd.next = oddStart;
        oddEnd.next = null;
        head=evenStart;
    }

    /*  Given a reference (pointer to pointer)
        to the head of a list and an int, push
        a new node on the front of the list. */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head
        new_node.next = head;

        // 4\. Move the head to point to new Node
        head = new_node;
    }

    // Utility function to print
    // a linked list
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
        llist.push(11);
        llist.push(10);
        llist.push(9);
        llist.push(6);
        llist.push(4);
        llist.push(1);
        llist.push(0);
        System.out.println(
               "Original Linked List");
        llist.printList();

        llist.segregateEvenOdd();

        System.out.println(
               "Modified Linked List");
        llist.printList();
    }
}
```

**输出:**

```
Original Linked List
0 1 4 6 9 10 11 
Modified Linked List
0 4 6 10 1 9 11 
```

**时间复杂度:** O(n)
更多详情请参考完整文章[在链表中隔离奇偶节点](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)！