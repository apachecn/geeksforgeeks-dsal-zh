# 寻找两个链表交点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-寻找两个链表交叉点的程序/](https://www.geeksforgeeks.org/java-program-for-finding-intersection-point-of-two-linked-lists/)

一个系统中有两个单链表。由于某种编程错误，其中一个链表的结束节点被链接到第二个链表，形成一个倒 Y 形链表。写一个程序来得到两个链表合并的点。

![Y ShapedLinked List](img/ab40c195e60241fe31989a627ddf41fc.png)

上图显示了一个例子，两个链表有 15 个交叉点。

**方法 1(简单使用两个循环):**
使用 2 嵌套循环。外部循环将用于第一个列表的每个节点，内部循环将用于第二个列表。在内部循环中，检查第二个列表的任何节点是否与第一个链表的当前节点相同。该方法的时间复杂度为 O(M * N)，其中 M 和 N 是两个列表中的节点数。

**方法 2(标记访问节点):**
该解决方案需要修改基本链表数据结构。每个节点都有一个访问标志。遍历第一个链表，并继续标记被访问的节点。现在遍历第二个链表，如果你再次看到一个被访问的节点，那么有一个交叉点，返回相交节点。该解决方案适用于 **O(m+n)** ，但需要每个节点的附加信息。这种解决方案的变体不需要修改基本数据结构，可以使用散列来实现。遍历第一个链表，并将访问节点的地址存储在一个散列中。现在遍历第二个链表，如果你看到散列中已经存在一个地址，那么返回相交节点。

**方法 3(利用节点数的差异):**

*   获取第一个列表中节点的计数，让计数为 c1。
*   获取第二个列表中节点的计数，让计数为 c2。
*   求计数之差**d = ABS(C1–C2)**
*   现在遍历更大的列表，从第一个节点到 d 个节点，这样从这里开始，两个列表的节点数相等
*   然后，我们可以并行遍历这两个列表，直到遇到一个公共节点。(请注意，获取公共节点是通过比较节点的地址来完成的)

下图是上述方法的模拟运行:

![](img/80d078e00182b28dfd0e2c284e5b12c1.png)

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get intersection point
// of two linked list
class LinkedList 
{
    static Node head1, head2;

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

    /* Function to get the intersection 
       point of two linked lists head1 
       and head2 */
    int getNode()
    {
        int c1 = getCount(head1);
        int c2 = getCount(head2);
        int d;

        if (c1 > c2) 
        {
            d = c1 - c2;
            return _getIntesectionNode(d, head1, 
                                       head2);
        }
        else 
        {
            d = c2 - c1;
            return _getIntesectionNode(d, head2, 
                                       head1);
        }
    }

    /* Function to get the intersection point
       of two linked lists head1 and head2 
       where head1 has d more nodes than head2 */
    int _getIntesectionNode(int d, Node node1, 
                            Node node2)
    {
        int i;
        Node current1 = node1;
        Node current2 = node2;
        for (i = 0; i < d; i++) 
        {
            if (current1 == null) 
            {
                return -1;
            }
            current1 = current1.next;
        }
        while (current1 != null && 
               current2 != null) 
         {
            if (current1.data == current2.data) 
            {
                return current1.data;
            }
            current1 = current2;
            current2 = current2.next;
        }

        return -1;
    }

    /* Takes head pointer of the linked list 
       and returns the count of nodes in the list */
    int getCount(Node node)
    {
        Node current = node;
        int count = 0;

        while (current != null) 
        {
            count++;
            current = current.next;
        }

        return count;
    }

   // Driver code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();

        // Creating first linked list
        list.head1 = new Node(3);
        list.head1.next = new Node(6);
        list.head1.next.next = new Node(9);
        list.head1.next.next.next = new Node(15);
        list.head1.next.next.next.next = new Node(30);

        // Creating second linked list
        list.head2 = new Node(10);
        list.head2.next = new Node(15);
        list.head2.next.next = new Node(30);

        System.out.println("The node of intersection is " + 
                            list.getNode());
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
The node of intersection is 15
```

**时间复杂度:**O(m+n)
T3】辅助空间: O(1)

**方法 4(第一个列表打圈):**
感谢**萨拉瓦南曼**提供以下解决方案。
1。遍历第一个链表(计算元素数量)并创建一个循环链表。(记住最后一个节点，这样我们以后就可以打破这个循环了)。
2。现在将问题视为在第二个链表中找到循环。这样问题就解决了。
3。由于我们已经知道循环的长度(第一个链表的大小)，我们可以遍历第二个链表中的许多节点，然后从第二个链表的开始处开始另一个指针。我们必须遍历，直到它们相等，这就是所需的交点。
4。从链接列表中删除该圆。

**时间复杂度:**O(m+n)
T3】辅助空间: O(1)

**方法 5(颠倒第一个列表，做等式):**
感谢**萨拉瓦南马尼**提供了这个方法。

```
1) Let X be the length of the first linked list until the intersection point.
   Let Y be the length of the second linked list until the intersection point.
   Let Z be the length of the linked list from the intersection point to End of
   the linked list including the intersection node.
   We Have
           X + Z = C1;
           Y + Z = C2;
2) Reverse first linked list.
3) Traverse Second linked list. Let C3 be the length of second list - 1\. 
     Now we have
        X + Y = C3
     We have 3 linear equations. By solving them, we get
       X = (C1 + C3 – C2)/2;
       Y = (C2 + C3 – C1)/2;
       Z = (C1 + C2 – C3)/2;
      WE GOT THE INTERSECTION POINT.
4)  Reverse the first linked list.
```

优点:没有指针的比较。
缺点:修改链表(反转列表)。
**时间复杂度:**O(m+n)
T5】辅助空间: O(1)

**方法 6(遍历两个列表，比较最后一个节点的地址):**这个方法只是检测是否有交点。(感谢纽泰萨沃的建议)

```
1) Traverse list 1, store the last node address
2) Traverse list 2, store the last node address.
3) If nodes stored in 1 and 2 are same then they are intersecting.
```

该方法的时间复杂度为 O(m+n)，使用的辅助空间为 O(1)

**方法 7(使用哈希):**
基本上，我们需要找到两个链表的公共节点。所以我们散列第一个列表的所有节点，然后检查第二个列表。
1)创建一个空的哈希集。
2)遍历第一个链表，在哈希集中插入所有节点的地址。
3)遍历第二个列表。对于每个节点，检查它是否存在于哈希集中。如果我们在哈希集中找到一个节点，返回该节点。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get intersection point 
// of two linked list
import java.util.*;
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
class LinkedListIntersect 
{
    public static void main(String[] args)
    {
        // list 1
        Node n1 = new Node(1);
        n1.next = new Node(2);
        n1.next.next = new Node(3);
        n1.next.next.next = new Node(4);
        n1.next.next.next.next = new Node(5);
        n1.next.next.next.next.next = new Node(6);
        n1.next.next.next.next.next.next = new Node(7);

        // list 2
        Node n2 = new Node(10);
        n2.next = new Node(9);
        n2.next.next = new Node(8);
        n2.next.next.next = n1.next.next.next;
        Print(n1);
        Print(n2);
        System.out.println(MegeNode(n1, n2).data);
    }

    // Function to print the list
    public static void Print(Node n)
    {
        Node cur = n;
        while (cur != null) 
        {
            System.out.print(cur.data + "  ");
            cur = cur.next;
        }
        System.out.println();
    }

    // Function to find the intersection
    // of two node
    public static Node MegeNode(Node n1, Node n2)
    {
        // define hashset
        HashSet<Node> hs = new HashSet<Node>();
        while (n1 != null) 
        {
            hs.add(n1);
            n1 = n1.next;
        }
        while (n2 != null) 
        {
            if (hs.contains(n2)) 
            {
                return n2;
            }
            n2 = n2.next;
        }
        return null;
    }
}
```

**输出:**

```
1  2  3  4  5  6  7  
10  9  8  4  5  6  7  
4
```

这种方法需要额外的空间，如果一个列表很大，效率就不高。

详情请参考[完整文章写一个函数得到两个链表](https://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)的交点！