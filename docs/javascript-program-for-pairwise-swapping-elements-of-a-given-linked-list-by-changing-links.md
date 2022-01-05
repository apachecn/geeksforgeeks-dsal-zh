# 通过改变链接成对交换给定链表元素的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-program-for-pair-swapping-elements-of-给定-link-list-by-changing-link/](https://www.geeksforgeeks.org/javascript-program-for-pairwise-swapping-elements-of-a-given-linked-list-by-changing-links/)

给定一个单链表，编写一个成对交换元素的函数。例如，如果链表是 1->2->3->4->5->6->7，那么函数应该把它改成 2->1->4->3->6->5->7，如果链表是 1->2->3->4->5->6，那么函数应该把它改成 2->1->4->3->6->5

这个问题已经在[这里](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)讨论过了。这里提供的解决方案交换节点的数据。如果数据包含许多字段，将会有许多交换操作。所以一般来说，改变链接是一个更好的主意。下面是更改链接而不是交换数据的实现。

## java 描述语言

```
<script>
// Javascript program to swap elements
// of linked list by changing links
var head;

class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

/* Function to pairwise swap elements
   of a linked list */
function pairWiseSwap(node)
{
    // If linked list is empty or there
    // is only one node in list
    if (node == null ||
        node.next == null)
    {
        return node;
    }

    // Initialize previous and current
    // pointers
    var prev = node;
    var curr = node.next;

    // Change head before proceeding
    node = curr;

    // Traverse the list
    while (true)
    {
        var next = curr.next;

        // Change next of current as
        // previous node
        curr.next = prev;

        // If next NULL or next is the
        // last node
        if (next == null ||
            next.next == null)
        {
            prev.next = next;
            break;
        }

        // Change next of previous to next
        // next
        prev.next = next.next;

        // Update previous and curr
        prev = next;
        curr = prev.next;
    }
    return node;
}

/* Function to print nodes in a
   given linked list */
function printList(node)
{
    while (node != null)
    {
        document.write(node.data + " ");
        node = node.next;
    }
}

// Driver code
/* The constructed linked list is:
   1->2->3->4->5->6->7 */
head = new Node(1);
head.next = new Node(2);
head.next.next = new Node(3);
head.next.next.next = new Node(4);
head.next.next.next.next =
new Node(5);
head.next.next.next.next.next =
new Node(6);
head.next.next.next.next.next.next =
new Node(7);

document.write(
"Linked list before calling pairwiseSwap() ");
printList(head);
var st = pairWiseSwap(head);
document.write("<br/>");
document.write(
"Linked list after calling pairwiseSwap() ");
printList(st);
document.write("");
// This code is contributed by aashish1995
</script>
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

**时间复杂度:**上述程序的时间复杂度为 O(n)，其中 n 为给定链表中的节点数。while 循环遍历给定的链表。

下面是同样方法的**递归实现**。我们更改前两个节点，并对剩余的列表重复执行。感谢 geek 和 omer salem 提出这个方法。

## java 描述语言

```
<script>
// Javascript program to swap elements of
// linked list by changing links
var head;
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

/* Function to pairwise swap elements of
   a linked  It returns head of the modified
   list, so return value of this node must be
   assigned */
function pairWiseSwap(node)
{
    // Base Case: The list is empty or has
    // only one node
    if (node == null ||
        node.next == null)
    {
        return node;
    }

// Store head of list after
// two nodes
var remaining = node.next.next;

// Change head
var newhead = node.next;

// Change next of second node
node.next.next = node;

// Recur for remaining list and
// change next of head
node.next = pairWiseSwap(remaining);

// Return new head of modified list
return newhead;
}

/* Function to print nodes in a
   given linked list */
function printList(node)
{
    while (node != null)
    {
        document.write(node.data + " ");
        node = node.next;
    }
}

// Driver code
/* The constructed linked list is:
   1->2->3->4->5->6->7 */
head = new Node(1);
head.next = new Node(2);
head.next.next = new Node(3);
head.next.next.next = new Node(4);
head.next.next.next.next =
new Node(5);
head.next.next.next.next.next =
new Node(6);
head.next.next.next.next.next.next =
new Node(7);

document.write(
"Linked list before calling pairwiseSwap() ");
printList(head);
head = pairWiseSwap(head);
document.write("<br/>");
document.write(
"Linked list after calling pairwiseSwap() ");
printList(head);
document.write("");
// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

更多细节请参考完整的文章[通过改变链接来成对交换给定链表的元素](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/)！