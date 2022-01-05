# 用任意指针指向链表中下一个更高值节点的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-pointing-to-next-value-in-a-a-link-list-in-list-a-any-pointer/](https://www.geeksforgeeks.org/javascript-program-for-pointing-to-next-higher-value-node-in-a-linked-list-with-an-arbitrary-pointer/)

给定单链表，每个节点都有一个额外的“任意”指针，该指针当前指向空。需要使“任意”指针指向下一个更高值的节点。

![listwithArbit](img/8169f1fd5a3a7a6cf9da279cda5846a5.png)

**强烈建议尽量减少浏览器，先自己试试**

一个**简单的解决方法**就是逐个遍历所有节点，对于每个节点，找到当前节点下一个值较大的节点，改变下一个指针。该解决方案的时间复杂度为 0(n<sup>2</sup>)。

一个**有效的解决方案**在 0(nLogn)时间内有效。想法是对链表使用[合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)。
1)遍历输入列表，并将下一个指针复制到每个节点的仲裁指针。
2)对仲裁指针形成的链表进行合并排序。

以下是上述想法的实现。所有的合并排序功能都取自[这里的](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)。这里修改了所取的函数，以便它们在仲裁指针上工作，而不是在下一个指针上工作。

## java 描述语言

```
<script>
// Javascript program to populate 
// arbit pointers to next higher 
// value using merge sort
var head;

// Link list node 
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.arbit = null;
        this.next = null;
    }
}

// Utility function to print
// result linked list
function printList(node, anode) 
{
    document.write(
    "Traversal using Next Pointer<br/>");
    while (node != null) 
    {
        document.write(node.data + ", ");
        node = node.next;
    }

    document.write(
    "<br/>Traversal using Arbit Pointer<br/>");
    while (anode != null) 
    {
        document.write(anode.data + ", ");
        anode = anode.arbit;
    }
}

// This function populates arbit pointer 
// in every node to the next higher value. 
// And returns pointer to the node with
// minimum value
function populateArbit(start) 
{
    var temp = start;

    // Copy next pointers to arbit 
    // pointers
    while (temp != null) 
    {
        temp.arbit = temp.next;
        temp = temp.next;
    }

    // Do merge sort for arbitrary pointers 
    // and return head of arbitrary pointer 
    // linked list
    return MergeSort(start);
}

/* Sorts the linked list formed by arbit 
   pointers (does not change next pointer
   or data) */
function MergeSort(start) 
{
    // Base case -- length 0 or 1 
    if (start == null || 
        start.arbit == null) 
    {
        return start;
    }

    /* Split head into 'middle' and 
       'nextofmiddle' sublists */
    var middle = getMiddle(start);
    var nextofmiddle = middle.arbit;
    middle.arbit = null;

    // Recursively sort the sublists 
    var left = MergeSort(start);
    var right = MergeSort(nextofmiddle);

    /* answer = merge the two sorted lists 
       together */
    var sortedlist = SortedMerge(left, 
                                 right);

    return sortedlist;
}

// Utility function to get the
// middle of the linked list
function getMiddle(source) 
{
    // Base case
    if (source == null)
        return source;
    var fastptr = source.arbit;
    var slowptr = source;

    // Move fastptr by two and slow ptr
    // by one. Finally slowptr will point 
    // to middle node
    while (fastptr != null) 
    {
        fastptr = fastptr.arbit;
        if (fastptr != null) 
        {
            slowptr = slowptr.arbit;
            fastptr = fastptr.arbit;
        }
    }
    return slowptr;
}

function SortedMerge(a, b) 
{
    var result = null;

    // Base cases 
    if (a == null)
        return b;
    else if (b == null)
        return a;

    // Pick either a or b, and recur 
    if (a.data <= b.data) 
    {
        result = a;
        result.arbit = 
        SortedMerge(a.arbit, b);
    } 
    else 
    {
        result = b;
        result.arbit = SortedMerge(a, b.arbit);
    }
    return result;
}

// Driver code
/* Let us create the list shown above */
head = new Node(5);
head.next = new Node(10);
head.next.next = new Node(2);
head.next.next.next = new Node(3);

// Sort the above created Linked List 
var ahead = populateArbit(head);

document.write(
"Result Linked List is:<br/>");
printList(head, ahead);
// This code is contributed by gauravrajput1 
</script>
```

**输出:**

```
Result Linked List is:
Traversal using Next Pointer
5, 10, 2, 3,
Traversal using Arbit Pointer
2, 3, 5, 10,
```

更多详情请参考完整文章[用任意指针](https://www.geeksforgeeks.org/point-to-next-higher-value-node-in-a-linked-list-with-an-arbitrary-pointer/)指向链表中下一个更高值的节点！