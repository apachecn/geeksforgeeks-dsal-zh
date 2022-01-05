# 在新列表中合并两个排序链表的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序-合并-两个排序-链表-在新列表中/](https://www.geeksforgeeks.org/java-program-to-merge-two-sorted-linked-lists-in-new-list/)

我们得到了两个排序列表，我们的目标是将这两个列表合并成一个新列表。为此，我们必须编写一个函数，该函数将两个列表作为参数，并按升序排序。这个函数会将这两个列表以递增的顺序合并成一个列表。

```
Input
List 1 : 1-> 3-> 4-> 9->10
List 2 : 2-> 5-> 6-> 9

Output
New List : 1-> 2-> 3-> 4-> 5-> 6-> 9-> 9-> 10
```

**我们有两种方法可以解决这个问题:**

1.  重复的
2.  递归的

**方法 1:迭代方法**

*   这种方法背后的思想是，我们将在新列表中增加一个节点，即列表的头节点。
*   我们将取类型列表中的一个变量，它总是在列表的最后一个节点，这样添加新节点就变得更容易了。
*   我们将循环检查两个列表中较小的元素，并将该节点追加到结果列表中。
*   如果我们到达任何列表的末尾，那么我们将简单地追加第二个列表中的剩余节点。

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Merge Two Sorted
// Linked Lists in New List
// Iteratively

import java.io.*;

public class ListNode {

    int val;
    ListNode next;

    ListNode() {}
    ListNode(int val) { this.val = val; }

    ListNode(int val, ListNode next)
    {
        this.val = val;
        this.next = next;
    }
}

class GFG {
    public static ListNode mergeTwoLists(ListNode l1,
                                         ListNode l2)
    {
        // New List
        ListNode result = new ListNode(-1);

        // variable to point the last node of the list.
        ListNode p = result;

        // Iterate the loop
        while (l1 != null && l2 != null) {
            // Find the smaller element and append it to the
            // list.
            if (l1.val <= l2.val) {
                p.next = l1;
                l1 = l1.next;
            }

            else {
                p.next = l2;
                l2 = l2.next;
            }

            // Update the variable
            p = p.next;
        }

        // If anyone list become empty append the remaining
        // list element of othe list.
        if (l1 == null) {
            p.next = l2;
        }

        else if (l2 == null) {
            p.next = l1;
        }

        // Return the resultant list without first extra
        // node
        return result.next;
    }

    // A utility function to print linked list
    static void printList(ListNode node)
    {
        while (node != null) {
            System.out.print(node.val + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        ListNode head1 = new ListNode(1);
        head1.next = new ListNode(3);
        head1.next.next = new ListNode(5);

        // 1->3->5 LinkedList created
        ListNode head2 = new ListNode(0);
        head2.next = new ListNode(2);
        head2.next.next = new ListNode(4);

        // 0->2->4 LinkedList created
        ListNode mergedhead = mergeTwoLists(head1, head2);

        printList(mergedhead);
    }
}
```

**Output**

```
0 1 2 3 4 5 
```

**方法 2:递归方法**

人们可以用递归方法解决这个问题。

*   该函数将两个排序列表作为参数。
*   如果任何列表为空，那么它只返回另一个列表中的剩余元素。
*   否则，它将从两个列表中检查较小的元素，将较小的节点追加到结果列表中，并递归调用该列表和另一个列表的下一个节点的函数。

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Merge Two Sorted
// Linked Lists in New List
// Recursively

import java.io.*;

public class ListNode {

    int val;
    ListNode next;

    ListNode() {}
    ListNode(int val) { this.val = val; }

    ListNode(int val, ListNode next)
    {
        this.val = val;
        this.next = next;
    }
}

class GFG {

    public static ListNode mergeTwoLists(ListNode l1,
                                         ListNode l2)
    {

        // New List
        ListNode result = null;

        // If anyone list is empty then returns the
        // remaining elements of other list
        if (l1 == null) {
            return l2;
        }
        else if (l2 == null) {
            return l1;
        }

        // Find the smaller element and recusivly call the
        // function with next node
        if (l1.val <= l2.val) {
            result = l1;
            result.next = mergeTwoLists(l1.next, l2);
        }
        else {
            result = l2;
            result.next = mergeTwoLists(l1, l2.next);
        }

        // Return the resultant list
        return (result);
    }
    // A utility function to print linked list
    static void printList(ListNode node)
    {
        while (node != null) {
            System.out.print(node.val + " ");
            node = node.next;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        ListNode head1 = new ListNode(23);
        head1.next = new ListNode(35);
        head1.next.next = new ListNode(65);

        // 23->35->65 LinkedList created
        ListNode head2 = new ListNode(43);
        head2.next = new ListNode(59);
        head2.next.next = new ListNode(60);

        // 43->59->60 LinkedList created
        ListNode mergedhead = mergeTwoLists(head1, head2);

        printList(mergedhead);
    }
}
```

**Output**

```
23 35 43 59 60 65 
```