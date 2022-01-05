# 用于展平多级链表的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-扁平化-多级链表/](https://www.geeksforgeeks.org/java-program-for-flattening-a-multilevel-linked-list/)

给定一个链表，其中除了下一个指针之外，每个节点都有一个子指针，这个子指针可以指向也可以不指向一个单独的列表。这些子列表可能有一个或多个自己的子列表，以此类推，从而产生多级数据结构，如下图所示。你被赋予列表第一层的头。展平列表，以便所有节点都出现在单级链接列表中。您需要将列表展平，使第一层的所有节点都应该首先出现，然后是第二层的节点，依此类推。
每个节点都是一个 C 结构，定义如下。

## Java 语言(一种计算机语言，尤用于创建网站)

```
static class List
{
    public int data;
    public List next;
    public List child;
};
// This code is contributed by pratham76
```

[![](img/55ec5b7c1827265a492de094d7906b79.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/flattenList.png)

以上列表应转换为 10-> 5-> 12-> 7-> 11-> 4-> 20-> 13-> 17-> 6-> 2-> 16-> 9-> 8-> 3-> 19-> 15

问题清楚地表明，我们需要一层一层地变平。一个解决方案的思路是，我们从第一层开始，逐个处理所有节点，如果一个节点有一个子节点，那么我们在列表的末尾追加这个子节点，否则，我们什么都不做。处理完第一级后，所有下一级节点将被追加到第一级之后。对于附加的节点，遵循相同的过程。

```
1) Take the "cur" pointer, which will point to the head 
        of the first level of the list
2) Take the "tail" pointer, which will point to the end of 
   the first level of the list
3) Repeat the below procedure while "curr" is not NULL.
    I) If the current node has a child then
    a) Append this new child list to the "tail"
        tail->next = cur->child
    b) Find the last node of the new child list and update 
       the "tail"
        tmp = cur->child;
        while (tmp->next != NULL)
            tmp = tmp->next;
        tail = tmp;
    II) Move to the next node. i.e. cur = cur->next
```

下面是上述算法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to flatten linked list with 
// next and child pointers
class LinkedList 
{    
    static Node head;

    class Node 
    {        
        int data;
        Node next, child;

        Node(int d) 
        {
            data = d;
            next = child = null;
        }
    }

    // A utility function to create a linked list 
    // with n nodes. The data of nodes is taken 
    // from arr[].  All child pointers are set 
    // as NULL
    Node createList(int arr[], int n) 
    {
        Node node = null;
        Node p = null;

        int i;
        for (i = 0; i < n; ++i) 
        {
            if (node == null) 
            {
                node = p = new Node(arr[i]);
            } 
            else 
            {
                p.next = new Node(arr[i]);
                p = p.next;
            }
            p.next = p.child = null;
        }
        return node;
    }

    // A utility function to print all 
    // nodes of a linked list
    void printList(Node node) 
    {
        while (node != null) 
        {
            System.out.print(node.data + " ");
            node = node.next;
        }
        System.out.println("");
    }

    Node createList() 
    {
        int arr1[] = new int[]{10, 5, 
                               12, 7, 11};
        int arr2[] = new int[]{4, 20, 13};
        int arr3[] = new int[]{17, 6};
        int arr4[] = new int[]{9, 8};
        int arr5[] = new int[]{19, 15};
        int arr6[] = new int[]{2};
        int arr7[] = new int[]{16};
        int arr8[] = new int[]{3};

        // Create 8 linked lists 
        Node head1 = createList(arr1,  
                                arr1.length);
        Node head2 = createList(arr2, 
                                arr2.length);
        Node head3 = createList(arr3, 
                                arr3.length);
        Node head4 = createList(arr4, 
                                arr4.length);
        Node head5 = createList(arr5, 
                                arr5.length);
        Node head6 = createList(arr6, 
                                arr6.length);
        Node head7 = createList(arr7, 
                                arr7.length);
        Node head8 = createList(arr8, 
                                arr8.length);

        // Modify child pointers to create 
        // the list shown above 
        head1.child = head2;
        head1.next.next.next.child = head3;
        head3.child = head4;
        head4.child = head5;
        head2.next.child = head6;
        head2.next.next.child = head7;
        head7.child = head8;

        /* Return head pointer of first linked list.  
           Note that all nodes are reachable from 
           head1 */
        return head1;
    }

    /* The main function that flattens a multilevel 
       linked list */
    void flattenList(Node node) 
    {        
        // Base case
        if (node == null) 
        {
            return;
        }

        Node tmp = null;

        /* Find tail node of first level 
           linked list */
        Node tail = node;
        while (tail.next != null) 
        {
            tail = tail.next;
        }

        // One by one traverse through all nodes 
        // of first level linked list till we 
        // reach the tail node
        Node cur = node;
        while (cur != tail) 
        {
            // If current node has a child
            if (cur.child != null) 
            {
                // Then append the child at the 
                // end of current list
                tail.next = cur.child;

                // And update the tail to new 
                // last node
                tmp = cur.child;
                while (tmp.next != null) 
                {
                    tmp = tmp.next;
                }
                tail = tmp;
            }

            // Change current node
            cur = cur.next;
        }
    }

    // Driver code
    public static void main(String[] args) 
    {
        LinkedList list = new LinkedList();
        head = list.createList();
        list.flattenList(head);
        list.printList(head);
    }
}
// This code has been contributed by Mayank Jaiswal
```

**输出:**

```
10 5 12 7 11 4 20 13 17 6 2 16 9 8 3 19 15
```

**时间复杂度:**由于每个节点最多被访问两次，因此时间复杂度为 O(n)，其中 n 是给定链表中的节点数。

更多详情请参考[整平多级链表](https://www.geeksforgeeks.org/flatten-a-linked-list-with-next-and-child-pointers/)整篇文章！