# 单链表快速排序的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-quick sort-on-single-link-list/](https://www.geeksforgeeks.org/javascript-program-for-quicksort-on-singly-linked-list/)

[在双链表上快速排序](https://www.geeksforgeeks.org/quicksort-for-linked-list/)在这里[讨论](https://www.geeksforgeeks.org/quicksort-for-linked-list/)。单链表上的快速排序是作为练习给出的。关于实现的重要事情是，它改变指针而不是交换数据，并且时间复杂度与双链表的实现相同。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

在**分区()**中，我们将最后一个元素视为轴心。我们遍历当前列表，如果一个节点的值大于 pivot，我们将它移到 tail 之后。如果节点的值较小，我们会将其保持在当前位置。

在**quick sort recursive()**中，我们首先调用 partition()将 pivot 放在正确的位置并返回 pivot。在枢轴被放置在正确的位置之后，我们找到左侧(枢轴之前的列表)的尾部节点，并为左侧列表重现。最后，我们重现正确的列表。

## java 描述语言

```
<script>
// Javascript program for Quick Sort on 
// Singly LinKed List

// Sort a linked list using quick sort
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

var head;

function addNode(data) 
{
    if (head == null) 
    {
        head = new Node(data);
        return;
    }

    var curr = head;
    while (curr.next != null)
        curr = curr.next;

    var newNode = new Node(data);
    curr.next = newNode;
}

function printList(n) 
{
    while (n != null) 
    {
        document.write(n.data);
        document.write(" ");
        n = n.next;
    }
}

// Takes first and last node,
// but do not break any links in
// the whole linked list
function paritionLast(start, end) 
{
    if (start == end || 
        start == null || 
        end == null)
        return start;

    var pivot_prev = start;
    var curr = start;
    var pivot = end.data;

    // Iterate till one before the end,
    // no need to iterate till the end
    // because end is pivot
    while (start != end) 
    {
        if (start.data < pivot) 
        {
            // Keep tracks of last modified 
            // item
            pivot_prev = curr;
            var temp = curr.data;
            curr.data = start.data;
            start.data = temp;
            curr = curr.next;
        }
        start = start.next;
    }

    // Swap the position of curr i.e.
    // next suitable index and pivot
    var temp = curr.data;
    curr.data = pivot;
    end.data = temp;

    // Return one previous to current
    // because current is now pointing
    // to pivot
    return pivot_prev;
}

function sort(start, end) 
{
    if (start == null || 
        start == end || 
        start == end.next)
            return;

    // Split list and partion recurse
    var pivot_prev = paritionLast(start, end);
    sort(start, pivot_prev);

    // If pivot is picked and moved to the start,
    // that means start and pivot is same
    // so pick from next of pivot
    if (pivot_prev != null && 
        pivot_prev == start)
        sort(pivot_prev.next, end);

    // If pivot is in between of the list,
    // start from next of pivot,
    // since we have pivot_prev, so we move two nodes
    else if (pivot_prev != null && 
             pivot_prev.next != null)
        sort(pivot_prev.next.next, end);
}

// Driver Code
addNode(30);
addNode(3);
addNode(4);
addNode(20);
addNode(5);

var n = head;
while (n.next != null)
    n = n.next;

document.write(
         "Linked List before sorting<br/>");
printList(head);

sort(head, n);

document.write(
         "<br/>Linked List after sorting<br/>");
printList(head);
// This code is contributed by umadevi9616 
</script>
```

**输出:**

```
Linked List before sorting 
30 3 4 20 5 
Linked List after sorting 
3 4 5 20 30 
```

详情请参考[单链表快速排序](https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)整篇文章！