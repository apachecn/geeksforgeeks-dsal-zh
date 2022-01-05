# 用于比较表示为链表的两个字符串的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-用于比较两个字符串的程序-表示为链表/](https://www.geeksforgeeks.org/java-program-for-comparing-two-strings-represented-as-linked-lists/)

给定两个字符串，表示为链表(每个字符都是链表中的一个节点)。编写一个与 strcmp()类似的函数 compare()，即如果两个字符串相同，则返回 0，如果第一个链表在字典序上更大，则返回 1，如果第二个字符串在字典序上更大，则返回-1。
**例:**

```
Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s->b
Output: -1

Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s
Output: 1

Input: list1 = g->e->e->k->s
       list2 = g->e->e->k->s
Output: 0
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare two strings 
// represented as a linked list

// Linked List Class
class LinkedList 
{
    // Head of list
    Node head;  
    static Node a, b;

    // Node Class 
    static class Node 
    {
        char data;
        Node next;

        // Constructor to create 
        // a new node
        Node(char d) 
        {
            data = d;
            next = null;
        }
    }

    int compare(Node node1, 
                Node node2) 
    {
        if (node1 == null && 
            node2 == null) 
        {
            return 1;
        }
        while (node1 != null && 
               node2 != null && 
               node1.data == node2.data) 
        {
            node1 = node1.next;
            node2 = node2.next;
        }

        // if the list are different 
        // in size
        if (node1 != null && 
            node2 != null) 
        {
            return (node1.data > 
                    node2.data ? 1 : -1);
        }

        // if either of the list has 
        // reached end
        if (node1 != null && 
            node2 == null) 
        {
            return 1;
        }
        if (node1 == null && 
            node2 != null) 
        {
            return -1;
        }
        return 0;
    }

    // Driver code
    public static void main(String[] args) 
    {
        LinkedList list = new LinkedList();
        Node result = null;

        list.a = new Node('g');
        list.a.next = new Node('e');
        list.a.next.next = new Node('e');
        list.a.next.next.next = 
             new Node('k');
        list.a.next.next.next.next = 
             new Node('s');
        list.a.next.next.next.next.next = 
             new Node('b');

        list.b = new Node('g');
        list.b.next = new Node('e');
        list.b.next.next = new Node('e');
        list.b.next.next.next = 
             new Node('k');
        list.b.next.next.next.next = 
             new Node('s');
        list.b.next.next.next.next.next = 
             new Node('a');

        int value;
        value = list.compare(a, b);
        System.out.println(value);
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
1
```

更多详细信息，请参考完整的文章[比较两个链表表示的字符串](https://www.geeksforgeeks.org/compare-two-strings-represented-as-linked-lists/)！