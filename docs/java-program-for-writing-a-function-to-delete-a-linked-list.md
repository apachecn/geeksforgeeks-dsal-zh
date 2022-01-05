# 编写删除链表函数的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-写程序-函数-删除-链表/](https://www.geeksforgeeks.org/java-program-for-writing-a-function-to-delete-a-linked-list/)

**Java 的算法:**
在 Java 中，会发生自动垃圾收集，所以删除链表很容易。只需要将 head 改为 null。

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete a linked list
class LinkedList
{
    // Head of the list
    Node head; 

    // Linked List node 
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

    // Function deletes the entire 
    // linked list 
    void deleteList()
    {
        head = null;
    }

    // Inserts a new Node at front 
    // of the list. 
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

    public static void main(String [] args)
    {
        LinkedList llist = new LinkedList();

        // Use push() to construct list
        // 1->12->1->4->1  
        llist.push(1);
        llist.push(4);
        llist.push(1);
        llist.push(12);
        llist.push(1);

        System.out.println("Deleting the list");
        llist.deleteList();

        System.out.println("Linked list deleted");
    }
}
// This code is contributed by Rajat Mishra
```

**输出:**

```
Deleting linked list
Linked list deleted
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

更多详情请参考[写函数删除链表](https://www.geeksforgeeks.org/write-a-function-to-delete-a-linked-list/)整篇文章！