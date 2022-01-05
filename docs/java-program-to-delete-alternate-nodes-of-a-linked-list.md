# 删除链表备用节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-delete-alternate-nodes-of-a-link-list/](https://www.geeksforgeeks.org/java-program-to-delete-alternate-nodes-of-a-linked-list/)

给定一个单链表，从第二个节点开始删除它的所有替换节点。例如，如果给定的链表是 1->2->3->4->5，那么你的函数应该把它转换成 1->3->5，如果给定的链表是 1->2->3->4，那么把它转换成 1->3。

**方法 1(迭代):**
跟踪要删除的节点的前一个。首先，更改上一个节点的下一个链接，并迭代移动到下一个节点。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete alternate 
// nodes of a linked list
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

    void deleteAlt()
    {
       if (head == null) 
          return;

       Node prev = head;
       Node now = head.next;

       while (prev != null && 
              now != null) 
       {           
           // Change next link of previous node 
           prev.next = now.next;

           // Free node 
           now = null;

           // Update prev and now 
           prev = prev.next;
           if (prev != null) 
              now = prev.next;
       }
    }                 

    // Utility functions 
    // Inserts a new Node at front 
    // of the list. 
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
               "Linked List before calling deleteAlt() ");
        llist.printList();

        llist.deleteAlt();

        System.out.println(
               "Linked List after calling deleteAlt() ");
        llist.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
List before calling deleteAlt() 
1 2 3 4 5 
List after calling deleteAlt() 
1 3 5 
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**方法 2(递归):**
递归代码使用与方法 1 相同的方法。递归代码简单而简短，但会导致 O(n)个递归函数调用大小为 n 的链表。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Deletes alternate nodes of 
   a list starting with head */
static Node deleteAlt(Node head) 
{ 
    if (head == null) 
        return; 

    Node node = head.next; 

    if (node == null) 
        return; 

    // Change the next link of head 
    head.next = node.next; 

    /* Recursively call for the new 
       next of head */
    head.next = deleteAlt(head.next); 
} 
// This code is contributed by Arnab Kundu
```

**时间复杂度:** O(n)

更多详情请参考[删除链表备用节点](https://www.geeksforgeeks.org/delete-alternate-nodes-of-a-linked-list/)整篇文章！