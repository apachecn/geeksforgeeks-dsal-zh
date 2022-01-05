# 用于以之字形方式重新排列链表的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-program-for-重排-链接列表-以之字形方式/](https://www.geeksforgeeks.org/javascript-program-for-rearranging-a-linked-list-in-zig-zag-fashion/)

给定一个链表，重新排列它，使得转换后的列表应该是 a < b > c < d > e < f …的形式，其中 a，b，c…是链表的连续数据节点。

**示例:**

```
Input:  1->2->3->4
Output: 1->3->2->4 
Explanation: 1 and 3 should come first before 2 and 4 in
             zig-zag fashion, So resultant linked-list 
             will be 1->3->2->4\. 

Input:  11->15->20->5->10
Output: 11->20->5->15->10 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/probfunc-page.php?pid=700085)

一个简单的方法是使用合并排序对链表进行排序，然后交换替换，但是这需要 O(n Log n)的时间复杂度。这里 n 是链表中的元素个数。

一种需要 O(n)时间的**有效方法是，使用类似于冒泡排序的单次扫描，然后维护一个标志来表示我们当前所处的顺序()。如果当前的两个元素不是按这个顺序排列的，那么交换这些元素，否则就不是。关于对换顺序的详细说明，请参考[本](http://geeksquiz.com/converting-an-array-of-integers-into-zig-zag-fashion/)。**

## java 描述语言

```
<script>
// Javascript program to arrange
// linked list in zigzag fashion

// Link list Node 
class Node 
{
    constructor() 
    {
        this.data = 0;
        this.next = null;
    }
}

var head = null;
var temp = 0;

// This function distributes
// the Node in zigzag fashion
function zigZagList(head) 
{
    // If flag is true, then
    // next node should be greater
    // in the desired output.
    var flag = true;

    // Traverse linked list starting from 
    // head.
    var current = head;
    while (current != null && 
           current.next != null) 
    {
        // "<" relation expected 
        if (flag == true) 
        {
            /* If we have a situation like 
               A > B > C where A, B and C 
               are consecutive Nodes in list 
               we get A > B < C by swapping B 
               and C */
            if (current.data > 
                current.next.data) 
            {
                temp = current.data;
                current.data = current.next.data;
                current.next.data = temp;
            }
        } 

        // ">" relation expected 
        else 
        {
            /* If we have a situation like 
               A < B < C where A, B and C 
               are consecutive Nodes in list 
               we get A < C > B by swapping B 
               and C */
            if (current.data < 
                current.next.data) 
            {
                temp = current.data;
                current.data = current.next.data;
                current.next.data = temp;
            }
        }

        current = current.next;

        // flip flag for reverse checking 
        flag = !(flag);
    }
}

// UTILITY FUNCTIONS 
// Function to push a Node 
Function push(new_data) 
{
    // Allocate Node 
    var new_Node = new Node();

    // Put in the data 
    new_Node.data = new_data;

    // Link the old list off the 
    // new Node 
    new_Node.next = (head);

    // Move the head to point to 
    // the new Node 
    (head) = new_Node;
}

// Function to print linked list 
function printList(node) 
{
    while (node != null) 
    {
        document.write(node.data + "->");
        node = node.next;
    }
    document.write("NULL<br/>");
}

// Driver code 
// Start with the empty list 
// Node head = null;

// create a list 4 -> 3 -> 7 -> 
// 8 -> 6 -> 2 -> 1
// answer should be -> 3 7 4 8 
// 2 6 1
push(1);
push(2);
push(6);
push(8);
push(7);
push(3);
push(4);

document.write(
         "Given linked list <br/>");
printList(head);
zigZagList(head);
document.write(
         "Zig Zag Linked list <br/>");
printList(head);
// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Given linked list 
4->3->7->8->6->2->1->NULL
Zig Zag Linked list 
3->7->4->8->2->6->1->NULL
```

**另一种方法:**
在上面的代码中，push 函数推链表前面的节点，代码可以很容易地修改为推链表末尾的节点。另一件需要注意的事情是，两个节点之间的数据交换是通过按值交换而不是按链接交换来完成的，为了简单起见，有关按链接交换的技术，请参见[本](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)。

这也可以递归完成。想法保持不变，让我们假设标志的值决定了比较当前元素需要检查的条件。因此，如果标志为 0(或假)，则当前元素应该小于下一个元素，如果标志为 1(或真)，则当前元素应该大于下一个元素。如果没有，交换节点的值。

## java 描述语言

```
<script>
// Javascript program for the
// above approach
// Node class
class Node
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

var head;

// Print Linked List
function printLL() 
{
    var t = head;
    while (t != null) 
    {
        document.write(t.data + 
                       " ->");
        t = t.next;
    }
    document.write();
}

// Swap both nodes
function swap(a, b) 
{
    if (a == null || 
        b == null)
        return;
    var temp = a.data;
    a.data = b.data;
    b.data = temp;
}

// Rearrange the linked list
// in zig zag way
function zigZag(node, flag) 
{
    if (node == null || 
        node.next == null) 
    {
        return node;
    }
    if (flag == 0) 
    {
        if (node.data > 
            node.next.data) 
        {
            swap(node, node.next);
        }
        return zigZag(node.next, 1);
    } 
    else 
    {
        if (node.data < 
            node.next.data) 
        {
            swap(node, node.next);
        }
        return zigZag(node.next, 0);
    }
}

// Driver Code
head = new Node(11);
head.next = new Node(15);
head.next.next = new Node(20);
head.next.next.next = new Node(5);
head.next.next.next.next = 
new Node(10);
printLL();

// 0 means the current element
// should be smaller than the next
var flag = 0;
zigZag(head, flag);
document.write(
"<br/>LL in zig zag fashion : <br/>");
printLL();
// This code is contributed by umadevi9616
</script>
```

**输出:**

```
11 ->15 ->20 ->5 ->10 ->
LL in zig zag fashion : 
11 ->20 ->5 ->15 ->10 ->
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    遍历列表只做一次，它有‘n’个元素。
*   **辅助空间:** O(n)。
    用于存储值的 O(n)额外空间数据结构。

更多详情请参考[以之字形方式重新排列链表](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)的完整文章！