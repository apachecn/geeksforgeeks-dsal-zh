# 两个链表并集和交集的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-两个链表的并集和交集程序/](https://www.geeksforgeeks.org/java-program-for-union-and-intersection-of-two-linked-lists/)

给定两个链接列表，创建包含给定列表中元素的并集和交集的并集和交集列表。输出列表中元素的顺序并不重要。
**例:**

```
Input:
List1: 10->15->4->20
List2:  8->4->2->10
Output:
Intersection List: 4->10
Union List: 2->8->20->4->15->10
```

**方法 1(简单):**
下面是分别获取并集和交集列表的简单算法。
**1。交集(列表 1、列表 2):**
将结果列表初始化为空。遍历列表 1，查找列表 2 中的每个元素，如果列表 2 中有该元素，则将该元素添加到结果中。
**2。联合(列表 1，列表 2):**
将结果列表初始化为空。遍历列表 1，并将其所有元素添加到结果中。
导线列表 2。如果结果中已经存在 list2 的元素，则不要将其插入到结果中，否则插入。
该方法假设给定列表中没有重复项。
感谢蛇湖提出这个方法。下面是这个方法的 C 和 Java 实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find union and
// intersection of two unsorted
// linked lists
class LinkedList 
{
    // head of list
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

    /* Function to get Union of 2 
       Linked Lists */
    void getUnion(Node head1, 
                  Node head2)
    {
        Node t1 = head1, t2 = head2;

        // Insert all elements of list1 
        // in the result
        while (t1 != null) 
        {
            push(t1.data);
            t1 = t1.next;
        }

        // Insert those elements of list2
        // that are not present
        while (t2 != null) 
        {
            if (!isPresent(head, t2.data))
                push(t2.data);
            t2 = t2.next;
        }
    }

    void getIntersection(Node head1, 
                         Node head2)
    {
        Node result = null;
        Node t1 = head1;

        // Traverse list1 and search each
        // element of it in list2.
        // If the element is present in
        // list 2, then insert the
        // element to result
        while (t1 != null) 
        {
            if (isPresent(head2, t1.data))
                push(t1.data);
            t1 = t1.next;
        }
    }

    // Utility function to print list 
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

    /*  Inserts a node at start of 
        linked list */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        /* 3\. Make next of new Node as head */
        new_node.next = head;

        /* 4\. Move the head to point to 
              new Node */
        head = new_node;
    }

    /* A utility function that returns true 
       if data is present in linked list 
       else return false */
    boolean isPresent(Node head, int data)
    {
        Node t = head;
        while (t != null) {
            if (t.data == data)
                return true;
            t = t.next;
        }
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist1 = new LinkedList();
        LinkedList llist2 = new LinkedList();
        LinkedList unin = new LinkedList();
        LinkedList intersecn = new LinkedList();

        /* Create a linked lits 10->15->5->20 */
        llist1.push(20);
        llist1.push(4);
        llist1.push(15);
        llist1.push(10);

        /* Create a linked lits 8->4->2->10 */
        llist2.push(10);
        llist2.push(2);
        llist2.push(4);
        llist2.push(8);

        intersecn.getIntersection(llist1.head, 
                                  llist2.head);
        unin.getUnion(llist1.head, llist2.head);

        System.out.println("First List is");
        llist1.printList();

        System.out.println("Second List is");
        llist2.printList();

        System.out.println("Intersection List is");
        intersecn.printList();

        System.out.println("Union List is");
        unin.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
First list is 
10 15 4 20 
Second list is 
8 4 2 10 
Intersection list is 
4 10 
Union list is 
2 8 20 4 15 10
```

**复杂度分析:**

*   **时间复杂度:** O(m*n)。
    这里的‘m’和‘n’分别是第一和第二列表中的元素数量。
    **对于联合:**对于列表-2 中的每个元素，我们检查该元素是否已经存在于使用列表-1 生成的结果列表中。
    **对于交集:**对于列表-1 中的每个元素，我们检查该元素是否也存在于列表-2 中。
*   **辅助空间:** O(1)。
    不使用任何数据结构来存储值。

**方法 2(使用合并排序):**
在该方法中，并集和交集的算法非常相似。首先，我们对给定的列表进行排序，然后遍历排序后的列表以获得并集和交集。
以下是获取并集和交集列表应遵循的步骤。

1.  使用合并排序对第一个链接列表进行排序。这一步需要 O(mLogm)时间。该步骤详见[本帖](https://www.geeksforgeeks.org/archives/7740)。
2.  使用合并排序对第二个链接列表进行排序。这一步需要 0(nLogn)时间。该步骤详见[本帖](https://www.geeksforgeeks.org/archives/7740)。
3.  线性扫描两个排序列表以获得并集和交集。这一步需要 O(m + n)个时间。这个步骤可以使用与这里讨论的排序数组算法相同的算法来实现。

该方法的时间复杂度为 O(mLogm + nLogn)，优于方法 1 的时间复杂度。
**方法 3(使用哈希):**
**1。Union (list1，list2):**
将结果列表初始化为 NULL，并创建一个空哈希表。逐个遍历这两个列表，对于每个被访问的元素，查看哈希表中的元素。如果元素不存在，则将该元素插入结果列表。如果元素存在，则忽略它。
**2。交集(列表 1，列表 2)**
将结果列表初始化为空，并创建一个空哈希表。遍历列表 1。对于列表 1 中被访问的每个元素，在哈希表中插入该元素。遍历列表 2，对于列表 2 中被访问的每个元素，在哈希表中查找该元素。如果该元素存在，则将该元素插入结果列表。如果元素不存在，则忽略它。
上述两种方法都假设没有重复。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Union and Intersection 
// of two Linked Lists
import java.util.HashMap;
import java.util.HashSet;

class LinkedList 
{
    // head of list
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

    // Utility function to print list 
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

    /* Inserts a node at start of 
       linked list */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        /* 3\. Make next of new Node as head */
        new_node.next = head;

        /* 4\. Move the head to point to 
              new Node */
        head = new_node;
    }

    public void append(int new_data)
    {
        if (this.head == null) 
        {
            Node n = new Node(new_data);
            this.head = n;
            return;
        }
        Node n1 = this.head;
        Node n2 = new Node(new_data);
        while (n1.next != null) 
        {
            n1 = n1.next;
        }

        n1.next = n2;
        n2.next = null;
    }

    /* A utility function that returns true 
       if data is present in linked list else 
       return false */
    boolean isPresent(Node head, int data)
    {
        Node t = head;
        while (t != null) 
        {
            if (t.data == data)
                return true;
            t = t.next;
        }
        return false;
    }

    LinkedList getIntersection(Node head1, 
                               Node head2)
    {
        HashSet<Integer> hset = new HashSet<>();
        Node n1 = head1;
        Node n2 = head2;
        LinkedList result = new LinkedList();

        // Loop stores all the elements of 
        // list1 in hset
        while (n1 != null) 
        {
            if (hset.contains(n1.data)) 
            {
                hset.add(n1.data);
            }
            else 
            {
                hset.add(n1.data);
            }
            n1 = n1.next;
        }

        // For every element of list2 present 
        // in hset loop inserts the element 
        // into the result
        while (n2 != null) 
        {
            if (hset.contains(n2.data)) 
            {
                result.push(n2.data);
            }
            n2 = n2.next;
        }
        return result;
    }

    LinkedList getUnion(Node head1, 
                        Node head2)
    {
        // HashMap that will store the
        // elements of the lists with their counts
        HashMap<Integer, Integer> hmap = 
                         new HashMap<>();
        Node n1 = head1;
        Node n2 = head2;
        LinkedList result = new LinkedList();

        // Loop inserts the elements and the 
        // count of that element of list1 into 
        // the hmap
        while (n1 != null) 
        {
            if (hmap.containsKey(n1.data)) 
            {
                int val = hmap.get(n1.data);
                hmap.put(n1.data, val + 1);
            }
            else 
            {
                hmap.put(n1.data, 1);
            }
            n1 = n1.next;
        }

        // Loop further adds the elements of 
        // list2 with their counts into the hmap
        while (n2 != null) 
        {
            if (hmap.containsKey(n2.data)) 
            {
                int val = hmap.get(n2.data);
                hmap.put(n2.data, val + 1);
            }
            else 
            {
                hmap.put(n2.data, 1);
            }
            n2 = n2.next;
        }

        // Eventually add all the elements
        // into the result that are present in the hmap
        for (int a : hmap.keySet()) {
            result.append(a);
        }
        return result;
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist1 = new LinkedList();
        LinkedList llist2 = new LinkedList();
        LinkedList union = new LinkedList();
        LinkedList intersection = new LinkedList();

        /*create a linked list 10->15->4->20 */
        llist1.push(20);
        llist1.push(4);
        llist1.push(15);
        llist1.push(10);

        /*create a linked list 8->4->2->10 */
        llist2.push(10);
        llist2.push(2);
        llist2.push(4);
        llist2.push(8);

        intersection = 
        intersection.getIntersection(llist1.head,
                                     llist2.head);
        union = union.getUnion(llist1.head, 
                               llist2.head);

        System.out.println("First List is");
        llist1.printList();

        System.out.println("Second List is");
        llist2.printList();

        System.out.println("Intersection List is");
        intersection.printList();

        System.out.println("Union List is");
        union.printList();
    }
}
// This code is contributed by Kamal Rawal
```

**输出:**

```
First List is
10 15 4 20 
Second List is
8 4 2 10 
Intersection List is
10 4 
Union List is
2 4 20 8 10 15
```

**复杂度分析:**

*   **时间复杂度:** O(m+n)。
    这里的‘m’和‘n’分别是第一和第二列表中的元素数量。
    **对于联合:**遍历两个列表，将元素存储在哈希映射中，并更新各自的计数。
    **对于交集:**首先遍历列表-1，将其元素存储在哈希映射中，然后对于列表-2 中的每个元素，检查它是否已经存在于映射中。这需要 0(1)时间。
*   **辅助空间:** O(m+n)。
    使用哈希映射数据结构存储值。

详情请参考完整的[两链表的并集和交集](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)一文！