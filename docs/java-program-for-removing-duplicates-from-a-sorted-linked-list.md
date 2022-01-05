# 用于从排序链表中删除重复项的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-从排序链表中删除重复项的程序/](https://www.geeksforgeeks.org/java-program-for-removing-duplicates-from-a-sorted-linked-list/)

编写一个函数，接受按非递减顺序排序的列表，并从列表中删除任何重复的节点。该列表只能遍历一次。
例如，如果链接列表是 11->11->11->21->43->43->60，则 removeDuplicates()应该将列表转换为 11- > 21- > 43- > 60。

**算法:**
从头(或开始)节点遍历列表。遍历时，将每个节点与其下一个节点进行比较。如果下一个节点的数据与当前节点相同，则删除下一个节点。在删除节点之前，我们需要存储节点的下一个指针

**实现:**
removeDuplicates()之外的函数只是创建一个链表并测试 remove duplicates()。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates 
// from a sorted linked list
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

    void removeDuplicates()
    {
        // Another reference to head
        Node curr = head;

        // Traverse list till the 
        // last node 
        while (curr != null) 
        {
            Node temp = curr;

            /* Compare current node with the 
               next node and keep on deleting 
               them until it matches the current 
               node data */
            while(temp != null && 
                  temp.data == curr.data) 
            {
                temp = temp.next;
            }

            /* Set current node next to the next 
               different element denoted by temp */
            curr.next = temp;
            curr = curr.next;
        }
    }

    // Utility functions 

    // Inserts a new Node at front of 
    // the list. 
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
         while (temp != null)
         {
            System.out.print(temp.data+" ");
            temp = temp.next;
         }  
         System.out.println();
     }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist = new LinkedList();
        llist.push(20);
        llist.push(13);
        llist.push(13);
        llist.push(11);
        llist.push(11);
        llist.push(11);

        System.out.println(
               "List before removal of duplicates");
        llist.printList();

        llist.removeDuplicates();

        System.out.println(
               "List after removal of elements");
        llist.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**递归方法:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to remove duplicates
// from a sorted linked list 
class GFG
{
    // Link list node 
    static class Node 
    { 
        int data; 
        Node next; 
    }; 

    // The function removes duplicates
    // from a sorted list 
    static Node removeDuplicates(Node head) 
    { 
        /* Pointer to store the pointer
           of a node to be deleted*/
        Node to_free; 

        // Do nothing if the list is empty 
        if (head == null) 
            return null; 

        // Traverse the list till last node 
        if (head.next != null) 
        {         
            // Compare head node with next node 
            if (head.data == head.next.data) 
            { 
                /* The sequence of steps is important.
                   to_free pointer stores the next of 
                   head pointer which is to be deleted.*/
                to_free = head.next; 
                head.next = head.next.next;
                removeDuplicates(head);
            } 

            // This is tricky: only advance if no deletion 
            else 
            { 
                removeDuplicates(head.next);
            } 
        } 
        return head;
    } 

    // UTILITY FUNCTIONS 
    /* Function to insert a node at the 
       beginning of the linked list */
    static Node push(Node head_ref,
                     int new_data) 
    { 
        // Allocate node 
        Node new_node = new Node();

        // Put in the data 
        new_node.data = new_data; 

        // Link the old list off the 
        // new node 
        new_node.next = (head_ref);     

        // Move the head to point to the 
        // new node 
        (head_ref) = new_node; 
         return head_ref;
    } 

    // Function to print nodes in a given 
    // linked list 
    static void printList(Node node) 
    { 
        while (node != null) 
        { 
            System.out.print(" " + node.data); 
            node = node.next; 
        } 
    } 

    // Driver code
    public static void main(String args[])
    { 
        // Start with the empty list 
        Node head = null; 

        /* Let us create a sorted linked list
           to test the functions. Created 
           linked list will be 11.11.11.13.13.20 */
        head = push(head, 20); 
        head = push(head, 13); 
        head = push(head, 13); 
        head = push(head, 11); 
        head = push(head, 11); 
        head = push(head, 11);                                     

        System.out.println("Linked list before" + 
                           " duplicate removal "); 
        printList(head); 

        // Remove duplicates from linked list 
        head = removeDuplicates(head); 

        System.out.println("Linked list after" + 
                           " duplicate removal ");     
        printList(head);             
    }
}  
// This code is contributed by Arnab Kundu
```

**输出:**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**另一种方法:**创建一个指向每个元素第一次出现的指针和另一个将迭代到每个元素的指针 temp，当前一个指针的值不等于 temp 指针时，我们将前一个指针的指针设置为另一个节点的第一次出现。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates
// from a sorted linked list
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

    // Function to remove duplicates
    // from the given linked list
    void removeDuplicates()
    {
        // Two references to head temp will 
        // iterate to the whole Linked List
        // prev will point towards the first 
        // occurrence of every element
        Node temp = head,prev = head;

        // Traverse list till the last node
        while (temp != null) 
        {           
           // Compare values of both pointers
           if(temp.data != prev.data)
           {
               /* if the value of prev is not equal 
                  to the value of temp that means 
                  there are no more occurrences of 
                  the prev data. So we can set the 
                  next of prev to the temp node.*/
               prev.next = temp;
               prev = temp;
           }

            // Set the temp to the next node
            temp = temp.next;
        }

        /* This is the edge case if there are more 
           than one occurrences of the last element */
        if(prev != temp)
        {
            prev.next = null;
        }
    }

    // Utility functions 

    // Inserts a new Node at front 
    // of the list. 
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data */
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
         LinkedList llist = new LinkedList();
         llist.push(20);
         llist.push(13);
         llist.push(13);
         llist.push(11);
         llist.push(11);
         llist.push(11);

         System.out.print("List before ");
         System.out.println(
                "removal of duplicates");
         llist.printList();

         llist.removeDuplicates();

         System.out.println(
                "List after removal of elements");
         llist.printList();
     }
} 
// This code is contributed by Arshita
```

**输出:**

```
List before removal of duplicates
11 11 11 13 13 20 
List after removal of elements
11 13 20 
```

**另一种方法:使用地图**
这个想法是推送地图中的所有值并打印其关键点。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class Node
{
    int data;
    Node next;
    Node()
    {
        data = 0;
        next = null;
    }
}
class GFG 
{    
    /* Function to insert a node at the 
       beginning of the linked list */
    static Node push(Node head_ref, 
                     int new_data)
    {      
        // Allocate node 
        Node new_node = new Node();

        // Put in the data 
        new_node.data = new_data;

        /* Link the old list off 
           the new node */
        new_node.next = (head_ref);

        /* Move the head to point
           to the new node */
        head_ref = new_node;
        return head_ref;
    }

    /* Function to print nodes 
       in a given linked list */
    static void printList(Node node)
    {
        while (node != null) 
        {
            System.out.print(node.data + " ");
            node = node.next;
        }
    }

    // Function to remove duplicates
    static void removeDuplicates(Node head)
    {
        HashMap<Integer, Boolean> track = new HashMap<>(); 
        Node temp = head;

        while(temp != null)
        {
            if(!track.containsKey(temp.data))
            {
                System.out.print(temp.data + " ");
            }
            track.put(temp.data, true);
            temp = temp.next;
        }
    }

    // Driver Code
    public static void main (String[] args) 
    {
        Node head = null;

        /* Created linked list will be
           11->11->11->13->13->20 */
        head = push(head, 20);
        head = push(head, 13);
        head = push(head, 13);
        head = push(head, 11);
        head = push(head, 11);
        head = push(head, 11);
        System.out.print(
               "Linked list before duplicate removal ");
        printList(head);
        System.out.print(
               "Linked list after duplicate removal  ");
        removeDuplicates(head);
    }
}
// This code is contributed by avanitrachhadiya2155
```

**输出:**

```
Linked list before duplicate removal 11 11 11 13 13 20 
Linked list after duplicate removal 11 13 20 
```

**时间复杂度:** O(节点数)

**空间复杂度:** O(节点数)

更多详情请参考[从排序链表](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)中删除重复项的完整文章！