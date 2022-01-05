# 寻找两个排序链表交集的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-寻找两个排序链表交集的程序/](https://www.geeksforgeeks.org/javascript-program-for-finding-intersection-of-two-sorted-linked-lists/)

给定两个按递增顺序排序的列表，创建并返回一个表示这两个列表交集的新列表。新的列表应该有自己的记忆——原来的列表不应该改变。

**示例:**

```
Input: 
First linked list: 1->2->3->4->6
Second linked list be 2->4->6->8, 
Output: 2->4->6.
The elements 2, 4, 6 are common in 
both the list so they appear in the 
intersection list. 

Input: 
First linked list: 1->2->3->4->5
Second linked list be 2->3->4, 
Output: 2->3->4
The elements 2, 3, 4 are common in 
both the list so they appear in the 
intersection list.
```

**<u>方法</u> :** 使用伪节点。
**方法:**
想法是在结果列表的开头使用一个临时伪节点。指针尾部总是指向结果列表中的最后一个节点，因此可以轻松添加新节点。伪节点最初给尾部一个内存空间来指向。这个虚拟节点是有效的，因为它只是临时的，并且是在堆栈中分配的。循环继续，从“a”或“b”中删除一个节点，并将其添加到尾部。当遍历给定的列表时，结果是伪的。接下来，当从虚拟的下一个节点分配值时。如果两个元素相等，则移除两个元素并将元素插入尾部。否则删除两个列表中较小的元素。

下面是上述方法的实现:

## java 描述语言

```
// Javascript program to implement 
// the above approach
<script>

// Head nodes for pointing to
// 1st and 2nd linked lists
var a = null, b = null;

// Dummy node for storing intersection
var dummy = null;

// Tail node for keeping track of
// last node so that it makes easy 
// for insertion
var tail = null;

// class - Node
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

// Function for printing the list
function printList(start) 
{
    var p = start;
    while (p != null) 
    {
        document.write(p.data + " ");
        p = p.next;
    }
    document.write();
}

// Inserting elements into list
function push(data) 
{
    var temp = new Node(data);
    if (dummy == null) 
    {
        dummy = temp;
        tail = temp;
    } 
    else 
    {
        tail.next = temp;
        tail = temp;
    }
}

// Function for finding intersection 
// and adding it to dummy list
function sortedIntersect() 
{
    // pointers for iterating
    var p = a, q = b;
    while (p != null && q != null) 
    {
        if (p.data == q.data) 
        {
            // Add to dummy list
            push(p.data);
            p = p.next;
            q = q.next;
        } 
        else if (p.data < q.data)
            p = p.next;
        else
            q = q.next;
    }
}

// Driver code

// Creating first linked list
a = new Node(1);
a.next = new Node(2);
a.next.next = new Node(3);
a.next.next.next = new Node(4);
a.next.next.next.next = new Node(6);

// Creating second linked list
b = new Node(2);
b.next = new Node(4);
b.next.next = new Node(6);
b.next.next.next = new Node(8);

// Function call for intersection
sortedIntersect();

// Print required intersection
document.write(
         "Linked list containing common items of a & b<br/>");
printList(dummy);
// This code is contributed by todaysgaurav 
</script>
```

**输出:**

```
Linked list containing common items of a & b 
2 4 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m+n)，其中 m 和 n 分别是第一和第二链表中的节点数。
    只需要遍历列表一次。
*   **辅助空间:** O(min(m，n))。
    输出列表最多可以存储(m，n)个节点。

更多详情请参考完整文章[两个排序链表的交集](https://www.geeksforgeeks.org/intersection-of-two-sorted-linked-lists/)！