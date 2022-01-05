# 用于合并链表排序的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-merge-sort-of-linked-list/](https://www.geeksforgeeks.org/javascript-program-for-merge-sort-of-linked-lists/)

[合并排序](http://en.wikipedia.org/wiki/Merge_sort)通常是对链表进行排序的首选。链表缓慢的随机访问性能使得其他一些算法(如 quicksort)性能很差，而其他算法(如 heapsort)则完全不可能。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

让 head 是要排序的链表的第一个节点，headRef 是指向 head 的指针。请注意，我们需要引用 MergeSort()中的 head，因为下面的实现会更改下一个链接以对链表进行排序(而不是节点处的数据)，因此如果原始 head 处的数据不是链表中的最小值，就必须更改 head 节点。

```
MergeSort(headRef)
1) If the head is NULL or there is only one element in the Linked List 
    then return.
2) Else divide the linked list into two halves.  
      FrontBackSplit(head, &a, &b); /* a and b are two halves */
3) Sort the two halves a and b.
      MergeSort(a);
      MergeSort(b);
4) Merge the sorted a and b (using SortedMerge() discussed here) 
   and update the head pointer using headRef.
     *headRef = SortedMerge(a, b);
```

## java 描述语言

```
<script>

// Javascript program to
// illustrate merge sorted
// of linkedList

    var head = null;

    // node a, b;
     class node {
            constructor(val) {
                this.val = val;
                this.next = null;
            }
        }

    function sortedMerge( a,  b)
    {
        var result = null;
        /* Base cases */
        if (a == null)
            return b;
        if (b == null)
            return a;

        /* Pick either a or b, and recur */
        if (a.val <= b.val) {
            result = a;
            result.next = sortedMerge(a.next, b);
        } else {
            result = b;
            result.next = sortedMerge(a, b.next);
        }
        return result;
    }

    function mergeSort( h) {
        // Base case : if head is null
        if (h == null || h.next == null) {
            return h;
        }

        // get the middle of the list
        var middle = getMiddle(h);
        var nextofmiddle = middle.next;

        // set the next of middle node to null
        middle.next = null;

        // Apply mergeSort on left list
        var left = mergeSort(h);

        // Apply mergeSort on right list
        var right = mergeSort(nextofmiddle);

        // Merge the left and right lists
        var sortedlist = sortedMerge(left, right);
        return sortedlist;
    }

    // Utility function to get the middle
    // of the linked list
    function getMiddle( head) {
        if (head == null)
            return head;

        var slow = head, fast = head;

        while (fast.next != null && fast.next.next != null)
        {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    function push(new_data) {
        /* allocate node */
        var new_node = new node(new_data);

        /* link the old list off the new node */
        new_node.next = head;

        /* move the head to point to the new node */
        head = new_node;
    }

    // Utility function to print the linked list
    function printList( headref) {
        while (headref != null) {
            document.write(headref.val + " ");
            headref = headref.next;
        }
    }

        /*
         Let us create a unsorted linked
         list to test the functions
         created. The list shall be
         a: 2->3->20->5->10->15
         */
        push(15);
        push(10);
        push(5);
        push(20);
        push(3);
        push(2);

        // Apply merge Sort
        head = mergeSort(head);
        document.write("
 Sorted Linked List is:
");
        printList(head);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
Sorted Linked List is: 
2 3 5 10 15 20
```