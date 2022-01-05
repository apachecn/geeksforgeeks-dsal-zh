# 从三个和等于给定数的链表中寻找三元组的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-program-for-find-a-triple-from-three-link-list-sum-等于给定的数字/](https://www.geeksforgeeks.org/java-program-for-finding-a-triplet-from-three-linked-lists-with-sum-equal-to-a-given-number/)

给定三个链表，比如 a，b 和 c，从每个链表中找出一个节点，这样节点的值之和等于一个给定的数。
例如，如果三个链表是 12- > 6- > 29、23- > 5- > 8 和 90- > 20- > 59，给定的数字是 101，那么输出应该是三倍的“6 5 90”。
在以下解决方案中，为了分析简单，假设所有三个链表的大小相同。以下解决方案也适用于不同大小的链表。

解决这个问题的一个简单方法是运行三个嵌套循环。最外面的循环从列表 a 中挑选一个元素，中间的循环从 b 中挑选一个元素，最里面的循环从 c 中挑选。最里面的循环还检查 a、b 和 c 的当前节点的值之和是否等于给定的数字。这种方法的时间复杂度将是 O(n^3).
排序可以用来将时间复杂度降低到 O(n*n)。以下是详细步骤。
1)列表 b 按升序排序，列表 c 按降序排序。
2)在对 b 和 c 进行排序后，逐个从列表 a 中选择一个元素，并通过遍历 b 和 c 来找到这一对。思路类似于 [3 和问题](http://en.wikipedia.org/wiki/3SUM)的二次算法。

下面的代码只实现步骤 2。通过添加这里讨论的合并排序代码，可以轻松修改未排序列表的解决方案。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a triplet from three linked lists with
// sum equal to a given number
class LinkedList
{
    Node head;  // head of list

    /* Linked list Node*/
    class Node
    {
        int data;
        Node next;
        Node(int d) {data = d; next = null; }
    }

    /* A function to check if there are three elements in a, b
      and c whose sum is equal to givenNumber.  The function
      assumes that the list b is sorted in ascending order and
      c is sorted in descending order. */
   boolean isSumSorted(LinkedList la, LinkedList lb, LinkedList lc,
                       int givenNumber)
   {
      Node a = la.head;

      // Traverse all nodes of la
      while (a != null)
      {
          Node b = lb.head;
          Node c = lc.head;

          // for every node in la pick 2 nodes from lb and lc
          while (b != null && c!=null)
          {
              int sum = a.data + b.data + c.data;
              if (sum == givenNumber)
              {
                 System.out.println("Triplet found " + a.data +
                                     " " + b.data + " " + c.data);
                 return true;
              }

              // If sum is smaller then look for greater value of b
              else if (sum < givenNumber)
                b = b.next;

              else
                c = c.next;
          }
          a = a.next;
      }
      System.out.println("No Triplet found");
      return false;
   }

    /*  Given a reference (pointer to pointer) to the head
       of a list and an int, push a new node on the front
       of the list. */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        /* 3\. Make next of new Node as head */
        new_node.next = head;

        /* 4\. Move the head to point to new Node */
        head = new_node;
    }

     /* Driver program to test above functions */
    public static void main(String args[])
    {
        LinkedList llist1 = new LinkedList();
        LinkedList llist2 = new LinkedList();
        LinkedList llist3 = new LinkedList();

        /* Create Linked List llist1 100->15->5->20 */
        llist1.push(20);
        llist1.push(5);
        llist1.push(15);
        llist1.push(100);

        /*create a sorted linked list 'b' 2->4->9->10 */
        llist2.push(10);
        llist2.push(9);
        llist2.push(4);
        llist2.push(2);

        /*create another sorted linked list 'c' 8->4->2->1 */
        llist3.push(1);
        llist3.push(2);
        llist3.push(4);
        llist3.push(8);

        int givenNumber = 25;
        llist1.isSumSorted(llist1,llist2,llist3,givenNumber);
    }
} /* This code is contributed by Rajat Mishra */
```

**输出:**

```
Triplet Found: 15 2 8
```

**时间复杂度:**链表 b 和 c 可以使用合并排序在 O(nLogn)时间内排序(参见[本](https://www.geeksforgeeks.org/merge-sort-for-linked-list/))。第二步耗时 0(n * n)。所以整体时间复杂度是 O(nlogn) + O(nlogn) + O(n*n) = O(n*n)。
在这种方法中，链表 b 和 c 是先排序的，所以它们原来的顺序会丢失。如果我们想保留 b 和 c 的原始顺序，我们可以创建 b 和 c 的副本。

更多详情请参考[整篇文章，从三个和等于给定数](https://www.geeksforgeeks.org/find-a-triplet-from-three-linked-lists-with-sum-equal-to-a-given-number/)的链表中找出一个三元组！