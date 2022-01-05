# 检查两个链表是否相同的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序检查两个链表是否相同/](https://www.geeksforgeeks.org/java-program-to-check-if-two-linked-lists-are-identical/)

当两个链表具有相同的数据并且数据的排列也相同时，它们是相同的。例如，链表 a (1->2->3)和 b(1->2->3)是相同的。。编写一个函数来检查给定的两个链表是否相同。

**方法 1(迭代):**
要确定两个列表是否相同，我们需要同时遍历两个列表，遍历时需要比较数据。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An iterative Java program to check if two 
// linked lists are identical or not
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

    /* Returns true if linked lists a and b 
       are identical, otherwise false */
    boolean areIdentical(LinkedList listb)
    {
        Node a = this.head, b = listb.head;
        while (a != null && b != null)
        {
            if (a.data != b.data)
                return false;

            /* If we reach here, then a and b 
               are not null and their data is 
               same, so move to next nodes in 
               both lists */
            a = a.next;
            b = b.next;
        }

        // If linked lists are identical, then 
        // 'a' and 'b' must be null at this point.
        return (a == null && b == null);
    }

    // UTILITY FUNCTIONS TO TEST fun1() and fun2() 
    /*  Given a reference (pointer to pointer) to 
        the head of a list and an int, push a new 
        node on the front of the list. */
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

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist1 = new LinkedList();
        LinkedList llist2 = new LinkedList();

        /* The constructed linked lists are :
           llist1: 3->2->1
           llist2: 3->2->1 */
        llist1.push(1);
        llist1.push(2);
        llist1.push(3);

        llist2.push(1);
        llist2.push(2);
        llist2.push(3);

        if (llist1.areIdentical(llist2) == true)
            System.out.println("Identical ");
        else
            System.out.println("Not identical ");

    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
Identical
```

**方法 2(递归):**
递归求解代码比迭代代码干净得多。然而，您可能不想将递归版本用于生产代码，因为它将使用与列表长度成比例的堆栈空间。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive Java method to check if two 
// linked lists are identical or not
boolean areIdenticalRecur(Node a, Node b)
{
    // If both lists are empty
    if (a == null && b == null)
        return true;

    // If both lists are not empty, then 
    // data of current nodes must match, 
    // and same should be recursively true 
    // for rest of the nodes.
    if (a != null && b != null)
        return (a.data == b.data) &&
               areIdenticalRecur(a.next, b.next);

    // If we reach here, then one of the lists
    // is empty and other is not
    return false;
}

/* Returns true if linked lists a and b 
   are identical, otherwise false */
boolean areIdentical(LinkedList listb)
{
    return areIdenticalRecur(this.head, 
                             listb.head);
}
```

**时间复杂度:** O(n)对于迭代和递归版本。n 是 a 和 b 中较小列表的长度。

更多详情请参考[完全相同链表](https://www.geeksforgeeks.org/identical-linked-lists/)的完整文章！